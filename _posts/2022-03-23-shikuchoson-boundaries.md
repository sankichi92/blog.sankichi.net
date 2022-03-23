---
title: 市区町村の境界を GeoJSON で返す Web API もどきをつくった
categories:
  - Dev
custome_css:
  - https://unpkg.com/leaflet@1.7.1/dist/leaflet.css
---

市区町村のハザードマップを手軽につくれるソフトウェア [shikuchoson-hazardmap-template](https://github.com/sankichi92/shikuchoson-hazardmap-template) をつくっている（詳細は「[Tokyo OSS Party!! 2021 に参加した]({% post_url 2021-12-09-tokyo_oss_party_2021 %})」）。
shikuchoson-hazardmap-template には、設定ファイルの都道府県名と市区町村名から市区町村の境界を取得し、全画面表示の地図の中心に表示する機能がある。
初期実装ではこの市区町村の境界を [OpenStreetMap](https://www.openstreetmap.org/) の [Overpass API](https://osmlab.github.io/learnoverpass/) から取得していたのだが、国土地理院の地図上に表示される行政区域界とはズレてしまう問題があった。

たとえば、https://www.openstreetmap.org/relation/2682891 は OpenStreetMap の茨城県つくば市の行政区域界である。
OpenStreetMap 上にこれを表示するのはなんの違和感もないが、これを[地理院タイル](https://maps.gsi.go.jp/development/ichiran.html)の淡色地図上に表示すると、地図のもつ行政区域界とところどころ重ならない部分が出てくる。

解決策として、ベースマップを地理院タイルではなく OpenStreetMap にするという方法もあるが、

- 災害情報を目立たせるためシンプルな淡色地図を使いたい
- 自治体で利用・公開することを想定しているため、行政から提供されている地図を使いたい

という理由から、行政区域界の取得元を国のオープンデータから取得することにした。

市区町村の行政区域界は、[国土交通省国土数値情報ダウンロードサイト](https://nlftp.mlit.go.jp/)で提供されている。
ただし、都道府県または全国単位で1ファイルまとめられた Shapefile または GeoJSON（を圧縮した ZIP ファイル）しか配布されていない。
そのため、任意の市区町村の行政区域界をフロントエンドで動的に取得するのは現実的ではない。

そこで、全国の行政区域界がまとまった GeoJSON を市区町村単位に分割する Ruby スクリプトを書いて、それを GitHub Pages で配布するようにした。
詳細は GitHub リポジトリ [sankichi92/shikuchoson-boundaries](https://github.com/sankichi92/shikuchoson-boundaries) にある。

単に静的なファイルを置いているだけだが、API-like に使えるので、たとえば [Leaflet](https://leafletjs.com/) を使って次のようなコードで市区町村の行政区域界を表示できる（[実行例はこちら](/misc/shikuchoson-boundaries.html)）。

```javascript
const map = L.map("map");

// 地理院タイルの淡色地図をベースマップにする
L.tileLayer("https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png", {
  attribution:
    "<a href='https://maps.gsi.go.jp/development/ichiran.html' target='_blank'>地理院タイル</a>",
}).addTo(map);

(async () => {
  const code = "08220"; // つくば市の行政区域コード
  const response = await fetch(
    `https://shikuchoson-boundaries.sankichi.app/${code}.geojson`
  );
  const geojson = await response.json();

  // 地図の表示領域を行政区域界に合わせる
  map.fitBounds([
    [geojson.bbox[1], geojson.bbox[0]],
    [geojson.bbox[3], geojson.bbox[2]],
  ]);

  // 行政区域界を地図に追加する
  L.geoJSON(geojson).addTo(map);
})();
```

静的なものなので、もちろん複数の行政区域界を同時に取得したり、市区町村名や緯度経度で検索したりといったことはできない。
が、shikuchoson-hazardmap-template で使うにはこれで十分である。

また、GeoJSON の分割にあたって次のような加工をおこなっている。

- 飛び地の Polygon を MultiPolygon にマージ
- Feature のプロパティのキーを「N03_001」から「都道府県名」のように意味のあるものに変更
- bbox フィールドの追加

行政区域界のデータソースを置き換えた結果については、[sankichi92/shikuchoson-hazardmap-template#20](https://github.com/sankichi92/shikuchoson-hazardmap-template/issues/20#issuecomment-1073950680) に  Before / After のスクリーンショットがある。

---

今回は用途に十分かつ無料ということで静的ファイルを置くだけという方法を取ったが、さまざまなユースケースに応用できる柔軟な API が国から提供されるのが理想だと思う。

たとえば、こうした地物データを提供する標準化された API 仕様の一つに [OGC API - Features](https://ogcapi.ogc.org/features/overview.html) がある。
また、その OSS 実装として [pygeoapi](https://pygeoapi.io/) というものもある。

もちろん ZIP ファイルを置いておくだけよりずっと手間もお金もかかるが、需要の高いデータについてはやる価値があると思う。
地理院タイルや[ハザードマップポータルサイト](https://disaportal.gsi.go.jp/hazardmap/copyright/opendata.html) なんかはとても扱いやすい。

---

最後に余談だが、緯度経度の数値の扱いでハマった。
Ruby で行政区域界データの緯度経度を含む JSON をパースすると次のようになる。

```ruby
require 'json'
JSON.parse('[140.059931051377021,36.236172864686012]')
#=> [140.05993105137702, 36.23617286468601]
```

Float 型として読み込まれて値が丸められてしまっている。

パース時に BigDecimal として扱う方法を探すと、[Ruby のドキュメント](https://rubyapi.org/3.1/o/json#module-JSON-label-Parsing+Options) にはないが、https://github.com/flori/json/pull/223 より、`decimal_class` というオプションがあるようだった。

```ruby
require 'bigdecimal'
require 'json'
hash = JSON.parse('[140.059931051377021,36.236172864686012]', decimal_class: BigDecimal)
#=> [0.140059931051377021e3, 0.36236172864686012e2]
```

しかし、これだと JSON にシリアライズするとき、数値ではなく文字列になってしまう。

```ruby
hash.to_json
#=> "[\"0.140059931051377021e3\",\"0.36236172864686012e2\"]"
```

最終的に「[freee の API では BigDecimal をどう扱うべきなのか？](https://developers.freee.co.jp/entry/freee-api-bigdecimal)」を参考に ActiveSupport と [Oj](https://github.com/ohler55/oj) を使って次のように書いた。

```ruby
require 'active_support/core_ext/big_decimal/conversions'
require 'oj'
hash = Oj.load('[140.059931051377021,36.236172864686012]')
#=> [0.140059931051377021e3, 0.36236172864686012e2]
Oj.dump(hash)
#=> "[140.059931051377021,36.236172864686012]"
```
