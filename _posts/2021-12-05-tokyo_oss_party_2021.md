---
title: Tokyo OSS Party!! 2021 に参加した
categories:
  - Dev
  - Essay
---

11月20日から12月4日の2週間にかけてオンラインで開催された [Tokyo OSS Party!!](https://tokyo-oss-party.com/) 2021 という東京都主催のハッカソンに参加した。
1人チーム「Ruby が好き」として [shikuchoson-hazardmap-template](https://github.com/sankichi92/shikuchoson-hazardmap-template) を開発し、結果として最優秀賞をいただいた。

- イベント詳細: https://tokyo-oss.connpass.com/event/229199/
- 成果発表: https://www.youtube.com/watch?v=FivWsvLAAyE

## 参加の動機

参加の動機は大きく以下の2つである。

- 行政（東京都）の OSS 活用の現状やノウハウが知りたかった
- コードを書く目的が欲しかった

まず、前者について。
この10月、私は Web サービスの会社から独立行政法人に転職した。
Web 業界とはある程度ギャップがあることは想定していたが、Web システムの開発・運用やクラウド移行がメインの業務と聞いており、前職の経験を活かせるだろうと思っていた。
しかし、行政機関の情報システムと Web 業界とのギャップは想像以上で、転職して2ヶ月経った今も本番環境で動くコードを1行も書いていない。
東京都は[新型コロナウイルス感染症対策サイト](https://github.com/tokyo-metropolitan-gov/covid19)（前職の同僚が関わっていた）等でいわゆる Web 業界的な開発や OSS の活用を始めていることは知っていたので、そのノウハウを得て仕事に還元したいと考えた。

後者については、すでに書いたとおりコードを書く機会が減ったので、ただただ単純に何かしらコードを書きたかった。

ちなみに、ハッカソンを知ったきっかけは、[@GitHubJapan](https://twitter.com/GitHubJapan) がリツイートしていた次のツイートだった。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">東京都がOSS（オープン・ソース・ソフトウェア）活用を推進するための「東京都OSSガイドライン」を作ったので、Tokyo OSS Party!というアイデアソン＆ワークショップを開催します。明日の夜にキックオフイベントがあるので、興味ある方はぜひご参加を！<a href="https://t.co/9dXzk5arDk">https://t.co/9dXzk5arDk</a></p>&mdash; Hal Seki (@hal_sk) <a href="https://twitter.com/hal_sk/status/1452804698130374656?ref_src=twsrc%5Etfw">October 26, 2021</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## 成果物について

設定ファイル等で容易にカスタマイズ可能な Web ハザードマップ shikuchoson-hazardmap-template を開発した。
プロダクトの背景や目的については以下のリンクに書いたので、そちらを参照してほしい。

- リポジトリ: https://github.com/sankichi92/shikuchoson-hazardmap-template
- 事前審査資料: https://hackmd.io/@hackcamp89/Hk7-Y7HuK
- 発表資料: https://speakerdeck.com/sankichi92/shikuchoson-hazardmap-template

「Ruby が好き」というチーム名だが、プロジェクトは `npx create-react-app --template typescript` で始めている。
発表時間が短く自己紹介の時間がなかったので、チーム名は自己紹介代わりにつけた。

地図ライブラリとしては、[Leaflet](https://leafletjs.com/)（および [React Leaflet](https://react-leaflet.js.org/)）を使用した。
ほぼ初めて使ったが、思ったより簡単に Web 地図を作成できた。

難しかったのは地理空間データの取り扱いで、これに関しては [GIS オープン教材](https://gis-oer.github.io/gitbook/book/)を大いに参考にした。

## ハッカソンの様子



オープン、協力的

ハッカソンの開催自体が目的

学生時代に参加したインターンで
「優勝したプロダクトが継続的に開発されたのを見たことがない」

## おわりに
