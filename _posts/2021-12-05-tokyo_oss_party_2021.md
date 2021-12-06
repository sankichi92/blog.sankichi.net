---
title: Tokyo OSS Party!! 2021 に参加した
categories:
  - Dev
  - Essay
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
東京都は[新型コロナウイルス感染症対策サイト](https://github.com/tokyo-metropolitan-gov/covid19)（前職の同僚が関わっていた）等でいわゆる Web 的な開発や OSS の活用をはじめていることは知っていたので、そのノウハウをきいて仕事に還元したいと考えた。

後者については、すでに書いたとおりコードを書く機会が減ったので、ただただ単純に何かしらコードを書きたかった。

ちなみに、ハッカソンを知ったきっかけは、[@GitHubJapan](https://twitter.com/GitHubJapan) がリツイートしていた次のツイートである。

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

ハッカソンはマラソンが由来だが、先頭集団で入賞を競い合うというよりは、全員で完走を目指すようなハッカソンだったと思う。

期間中のコミュニケーションは [Tokyo OSS Party!! の Slack ワークスペース](https://join.slack.com/t/tokyoossparty/shared_invite/zt-xj39veiu-cr_1brEP_VeNWMQCXs~fPw)で行われていた。
初日に各チームのチャンネルがつくられたが、すべてパブリックチャンネルで、他のチームの開発様子も見られるようになっている。

Slack だけでなく、優秀賞（Hazard Map 賞）のチーム「Arumon」は、開催期間中から得られた知見や途中経過を Qiita や note に投稿していた。
この記事で [OpenStreetMap](https://www.openstreetmap.org/) の [Overpass API](https://osmlab.github.io/learnoverpass/en/docs/) の存在を知り、自分のプロダクトでも利用させてもらった。

- https://qiita.com/t-kurasawa/items/03e5bc9c9a07d8ff99b7
- https://note.com/arumon_team/n/n228986f88be1

また、行政が主催するだけあって入賞のインセンティブも独特だった。

> 選出チームに選ばれると、その後の自治体とのワークショップに参加することができ、その場でその後の具体的な実装について検討がされます。

ただ、入賞後のワークショップでは「具体的な実装について検討」というようなものはなかった（とぼくは感じている）。
実のところ、現実に自治体でプロダクトを利用するにあたってのハードルをフィードバックしてもらって、そのハードルを乗り越えるための今後の具体的な実装を検討することを期待していた。
実際には、開発したプロダクトから離れて、「行政による地域課題解決のための OSS 活用」というハッカソンのテーマのもと、自治体職員とシンプルに意見を交わすというものだった。
勘ちがいしたぼくが悪いのだが、「地域課題を解決する」というよりは「OSS をテーマに東京都がハッカソンを開催する」ことが目的だったのかと感じられ、少し寂しかった。

とはいえ、
運営の皆様には感謝している。

## おわりに

利用者が現れる限りはメンテしたい。
「リリース後9割」

---


実際には、というテーマで、



実際には、今後について具体的なことは「東京都の GitHub org で入賞リポジトリを fork するが、[東京都OSS公開ガイドライン](https://github.com/Tokyo-Metro-Gov/tokyo-oss-guideline/blob/main/%E6%9D%B1%E4%BA%AC%E9%83%BD%E3%82%AA%E3%83%BC%E3%83%97%E3%83%B3%E3%83%BB%E3%82%BD%E3%83%BC%E3%82%B9%E3%83%BB%E3%82%BD%E3%83%95%E3%83%88%E3%82%A6%E3%82%A7%E3%82%A2%E5%85%AC%E9%96%8B%E3%82%AC%E3%82%A4%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3.md#5-%E9%96%8B%E7%99%BA%E4%BF%9D%E5%AE%88%E3%81%AE%E7%B5%82%E4%BA%86)にのっとり1年間利用がなかったら削除する」という説明しかなかった。

寂しかった




個人的に「その後の具体的な実装について検討」という点を意識していて、単にプロトタイプで終わるのではなく、実際に市区町村で利用されることを目指して開発に取り組んだ。

しかし、入賞後のワークショップは残念ながら少し期待外れだった。

私が期待していたのは、以下のような具体的な「検討」である。

- 実際に自治体でプロダクトを利用するにはどんなハードルがあるか
- 実際に自治体でプロダクトを利用するにあたって足りない機能は何か
- 私個人ができる範囲でメンテするのか、都や市のサポートはあるのか

前職に「リリース後9割」という言葉があったが、検討の内容によっては

フィードバックを得て日曜大工的に


良くも悪くも「完走を目指す」ハッカソン



前職に「リリース後9割」という言葉があったが、もし市区町村で採用されてユーザーが




学生のときに参加したハッカソン型インターンのメンターの言葉が印象に残っている。

> ハッカソンで優勝したプロダクトがその後も続いたって話聞いたことない。
> サービスをつくるうえで本当に大事なのはリリースしてから。

細かいニュアンスはちがう気がするが、大体こんな趣旨の言葉だった。
たしか入賞を逃したときにかけられた言葉だったと思う。

「リリース後9割」

動機には書かなかったが、行政が主催するだけあって入賞のインセンティブが独特なのも、このハッカソンに惹かれたポイントだった。



選出されれば、プロダクトが実際に自治体で使われる可能性があるのだ。

魅力的だった。

ソフトウェアエンジニア冥利に尽きる。

オープン、協力的

ハッカソンの開催自体が目的

学生時代に参加したインターンで
「優勝したプロダクトが継続的に開発されたのを見たことがない」

## おわりに
