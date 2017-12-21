---
title: WordPress から Jekyll へ移行した
categories:
  - Dev
toc: true
---

## 移行の理由

ブログシステムを WordPress から Jekyll へ移行した。
理由はおおよそ次に書いているとおりであるが，WordPress を使いこなせていたわけではないので誤解があるかもしれず，また，Jekyll に至っては使ったことがないので色々と勘違いしているかもしれない。

### 運用費が高かった

ろくにアクセスもない割に，サーバー代が高額だった。
ある時から AWS の1年間の無料利用枠で運用していたのだが，それが切れると1,500円/月ほどかかるようになってしまっていた。

Jekyll なら GitHub Pages でずっと無料運用できる。

### 管理画面がつらかった

記事を投稿・管理しにくかった。
使い慣れたエディタで記事を書いて，それをコピペして投稿するなどしていたが，どう考えても非効率だった。
また，ブログの状態を Git 等で管理したかったが，WordPress ではそれができそうになかった。

Jekyll ならターミナルと好きなエディタだけで完全にコントロールできる。

### PHP を書かなくなった

WordPress を始めた頃は PHP をよく書いていたが，ここ2，3年で全く書かなくなってしまった。
当時はプラグインやテーマにも少し手を入れていたが，なかなか複雑で面倒だった記憶があり，改めて手を出す気にはならなかった。

Jekyll は最近よく書いている Ruby でできており，仕組み自体も比較的単純そうである。

### Jekyll の名前をよく耳にした

Jekyll に新しさはないけれど，長期運用が前提だったので無難な選択肢を選んだ。
はてなブログなんかも選択肢にないわけではなかったけれど，できる限り自分でコントロールしたかった。
この点は WordPress で運用していた頃と同じである。

## 移行の手順

次に，備忘録がてら移行手順について簡単に書いておく。
ソースコードは [sankichi92/blog.sankichi.net](https://github.com/sankichi92/blog.sankichi.net) に公開しているので，コミットログを見ればより具体的な手順を知ることができるだろう。

### Jekyll によるブログ作成

びっくりするくらい簡単だった。
[公式ドキュメント](https://Jekyllrb.com/)を参照。

### WordPress のインポート

はじめ [`jekyll-import`](http://import.jekyllrb.com/docs/wordpress/) を使ったが，これは完全に失敗だった。
以下の点がよくなかった。

- DB へ接続する必要がある
  - ローカルに DB をコピーしてきてそちらに接続したけど面倒だった
- Front Matter に余計なメタ情報が出力される
  - 後述の Minimal Mistakes を適用した際，author に余計な情報があるせいでレイアウトが崩れた
- コメントが全て Front Matter に出力される
  - [Staticman](https://staticman.net/) で扱えない

これに関して，Minimal Mistakes のドキュメントで紹介されていた [wordpress2jekyll](https://github.com/arthurlacoste/wordpress2jekyll) が便利だった。
これは，WordPress の標準のエクスポート機能を使って出力された XML を用いる。
記事に余計なメタ情報はなく，コメントは Staticman 形式で出力してくれる。
もし WordPress から Jekyll に移行するのであれば，断然こちらをお勧めしたい。

### GitHub Pages へのデプロイとカスタムドメインの使用

それぞれ以下二つのドキュメントを見ながら行った。

- [Using Jekyll as a static site generator with GitHub Pages](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)
- [Using a custom domain with GitHub Pages](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)

### HTTPS 化

カスタムドメインの GitHub Pages は，そのままでは HTTPS 化されない。
そこで，以下の二つの記事を参考に，CloudFlare を用いて HTTPS 化した。
（CloudFlare が何をしているかはまだよくわかっていない。）

- [CloudflareでブログをHTTPS化 | To Be Decided](https://www.kaitoy.xyz/2016/07/01/https-support-by-cloudflare/)
- [GitHub Pages + CloudFlare で独自ドメインをSSL化する - Qiita](https://qiita.com/noraworld/items/89dd85a434a7b759e00c)

### Minimal Mistakes テーマの適用

ブログのテーマとして [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) を選んだ。
理由は，GitHub で "jekeyll theme" で検索した際に圧倒的にスター数が多かったから。

ドキュメントを読みながら `_config.yml` を設定していった。
気をつけたのは，パーマリンクが WordPress の頃と一致するようにしたことくらいだったと思う。

また，`ui-text.yml` に日本語がなかったので，[Pull Request](https://github.com/mmistakes/minimal-mistakes/pull/1411) を送った。

さらに，デフォルトテーマのままというのもつまらないので，[独自の skin](https://github.com/sankichi92/blog.sankichi.net/blob/master/_sass/minimal-mistakes/skins/_sankichi.scss) を書いてフォントや色なんかを少し変えた。

## 移行の感想

Jekyll に移行してみて2点ほど微妙だなあと思うことがあった。

まず，画像や音楽，コメントといった投稿以外のリソースが扱いづらい。
WordPress だとこの辺りはよしなにやってくれるが，Jekyll にはそういったサポートはなく，自前でうまくやる必要がある。
ただ，画像やコメント，音楽等のメディアに関しては外部サービスもあるので，それらをうまく利用するのが良さそう。

次に，カテゴリーのような形で記事をまとめるのが難しい。
一応このブログにも[カテゴリーページ](https://blog.sankichi.net/categories/)はあるが，全カテゴリが1ページに表示されるだけでなく，全投稿も pagenate なしで1ページに表示されてしまっている。
DB のリレーションで実現されるような機能はやはり弱く感じた。

ただ，文章ベースで淡々と記事を書く分には特に困らなさそうだった。
また，Minimal Mistakes はよくできていて，SEO なんかは項目を単純に埋めていくだけで，いい感じにしてくれていそうだった。

ブログもリニューアルしたので，また少しずつ記事を書いていきたい。
