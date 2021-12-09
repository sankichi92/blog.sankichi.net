---
title: Tokyo OSS Party!! 2021 に参加した
categories:
  - Dev
---

11月20日から12月4日の2週間にかけてオンラインで開催された [Tokyo OSS Party!!](https://tokyo-oss-party.com/) 2021 という東京都主催のハッカソンに参加した。
1人チーム「Ruby が好き」として [shikuchoson-hazardmap-template](https://github.com/sankichi92/shikuchoson-hazardmap-template) をつくり、結果として最優秀賞をいただいた。

- イベント詳細: https://tokyo-oss.connpass.com/event/229199/
- 成果発表: https://www.youtube.com/watch?v=FivWsvLAAyE

## 参加の動機

参加の動機は大きく以下の2つ。

- 行政（東京都）の OSS 活用の現状やノウハウが知りたかった
- コードを書く目的がほしかった

まず、前者について。
この10月、Web サービスの会社からある独立行政法人に転職した。
Web 業界とはそれなりにギャップがあることは覚悟していたが、Web システムの開発・運用やクラウド移行がメインの業務と聞いていて、前職の経験を活かせるだろうと思っていた。
しかし、行政機関の情報システムと Web 業界とのギャップは想像以上で、転職して2ヶ月経ったいまも本番環境で動くコードを1行も書いていない。
東京都は[新型コロナウイルス感染症対策サイト](https://github.com/tokyo-metropolitan-gov/covid19)（前職の同僚が関わっていた）等でいわゆる Web 的な開発や OSS の活用をはじめていることは知っていたので、そのノウハウを得て仕事に還元したいと考えた。

後者については、すでに書いたとおりコードを書く機会が減ったので、ただただ単純に何かしらコードを書きたかった。
ハッカソンでなくともコードは書けるが、参加すれば「課題」と「締切」が自動的に与えられるという点が大きい。

ちなみに、ハッカソンを知ったきっかけは、[@GitHubJapan](https://twitter.com/GitHubJapan) がリツイートしていた次のツイートだった。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">東京都がOSS（オープン・ソース・ソフトウェア）活用を推進するための「東京都OSSガイドライン」を作ったので、Tokyo OSS Party!というアイデアソン＆ワークショップを開催します。明日の夜にキックオフイベントがあるので、興味ある方はぜひご参加を！<a href="https://t.co/9dXzk5arDk">https://t.co/9dXzk5arDk</a></p>&mdash; Hal Seki (@hal_sk) <a href="https://twitter.com/hal_sk/status/1452804698130374656?ref_src=twsrc%5Etfw">October 26, 2021</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## 成果物について

プロダクトの背景や目的については以下のリンクに書いたので、そちらを参照してほしい。

- リポジトリ: https://github.com/sankichi92/shikuchoson-hazardmap-template
- 事前審査資料: https://hackmd.io/@hackcamp89/Hk7-Y7HuK
- 発表資料: https://speakerdeck.com/sankichi92/shikuchoson-hazardmap-template

「Ruby が好き」というチーム名だが、プロジェクトは [Create React App](https://create-react-app.dev/) と [TypeScript](https://www.typescriptlang.org/) で作成している。
はじめは [Next.js](https://nextjs.org/) でつくろうとしたが、[React Leaflet をつかうのがちょっと面倒だった](https://stackoverflow.com/questions/57704196/leaflet-with-next-js)のと、シンプルな SPA で完結できそうだったのではやい段階で切りかえた。

地図ライブラリとしては、[Leaflet](https://leafletjs.com/)（および [React Leaflet](https://react-leaflet.js.org/)）を利用した。
ほぼ初めてだったが、レイヤーの概念に慣れさえすれば、いろいろな情報を簡単に地図上へ重ねることができる。

難しかったのは地理空間データの取り扱いで、これに関しては [GIS オープン教材](https://gis-oer.github.io/gitbook/book/)を参考にした。

## ハッカソンの様子

先頭集団で入賞を競い合うというよりは、みんなで完走を目指すようなハッカソンだったと思う。

期間中のコミュニケーションは [Tokyo OSS Party!! の Slack ワークスペース](https://join.slack.com/t/tokyoossparty/shared_invite/zt-xj39veiu-cr_1brEP_VeNWMQCXs~fPw)で行われていた。
初日に各チームのチャンネルがつくられたが、すべてパブリックチャンネルで、他のチームの開発の様子も見られるようになっている。

Slack だけでなく、優秀賞（Hazard Map 賞）のチーム「Arumon」は、開催期間中から得られた知見や途中経過を Qiita や note に投稿していた。
この記事で [OpenStreetMap](https://www.openstreetmap.org/) の [Overpass API](https://osmlab.github.io/learnoverpass/en/docs/) の存在を知り、自分のプロダクトでも利用させてもらった。

- https://qiita.com/t-kurasawa/items/03e5bc9c9a07d8ff99b7
- https://note.com/arumon_team/n/n228986f88be1

また、行政が主催するだけあって入賞のインセンティブも独特だった。

> 選出チームに選ばれると、その後の自治体とのワークショップに参加することができ、その場でその後の具体的な実装について検討がされます。

動機の1つめにも書いたように、行政のつくったソフトウェアを OSS 化するにあたってのノウハウに興味があったので、これに関してはけっこう期待していた。

しかし、実際のワークショップは、「行政による地域課題解決のための OSS 活用」というハッカソン全体のテーマで自治体職員とシンプルに意見を交わすというものだった。
開発したプロダクトの具体的な実装や今後の利用に関する言及はほぼなく、それらをつかって実際に「地域課題を解決する」というより単に「OSS をテーマに東京都がハッカソンを開催する」ことが目的だったのかと感じられて少しさびしかった。
一方で、東京都の OSS 活用も本当にはじまったばかりで、ハッカソンで生まれたようなプロダクトを実際に活用するにはまだまだハードルがたくさんあるということもよくわかった。

## おわりに

前職に「リリース後9割」という言葉があった。
リリースがゴールではなく、リリースしてからがスタートというような意味である。

今回つくったプロダクトもかろうじて表に出せたという感じで、まだまだ改善の余地がある。
アイデア自体はそれほどわるくない気がしているので、のんびりと改善していけたらと思う。
