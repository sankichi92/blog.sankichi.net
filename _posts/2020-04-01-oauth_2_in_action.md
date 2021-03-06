---
title: 『OAuth徹底入門』を読んだ
categories:
  - Dev
---

『OAuth徹底入門 セキュアな認可システムを適用するための原則と実践』を読んだ。
https://www.shoeisha.co.jp/book/detail/9784798159294

昨年からユーザー・決済基盤部というところに異動して主に決済を担当しているが、ユーザーの方もわかるようにならないとな、という漠然とした思いがあった。
さらに、1月には [OpenID Summit Tokyo 2020](https://www.openid.or.jp/summit/2020/) に参加して、認証・認可周りの技術についてモチベーションが高まっていた。
そんな折、2月に翔泳社 Kindle でセールで本書が安くなっていたので購入。

内容は、

- クライアント
- リソースサーバー
- 認可サーバー

の3つを実装しながら OAuth 2 のプロトコルを説明していくというもの。
後半では、OpenID Connect など OAuth 2 の拡張についても触れられている。

演習のコードは https://github.com/oauthinaction/oauth-in-action-code で公開されているが、 Node.js v4.4.1 (+ Express) で書かれており、現在の stable である v12 では動かない。
せっかくなので、一番書きなれた Ruby (+ Sinatra) を使ってスクラッチでやることにした。書いたコードは https://github.com/sankichi92/oauth-in-action-ruby に公開している。

OAuth 2 に関しては、ライブラリを使ってクライアントを実装したり、仕事で API サーバーに機能追加したりしたことはあった。
ただ、必要に迫られて言われるがままに書いたという感じで、ライブラリや認可サーバーが内部で何をしているのかや、なぜ OAuth 2 を使うのかはよくわからないままだった。

本書で一からクライアント・リソースサーバー・認可サーバーを実装することで、それぞれが何をしているのか・何をする必要があるのかがよく理解できたと思う。
[Ruby on Rails チュートリアル](https://railstutorial.jp/) は、その大半をログイン周りの実装に割いているが、それを初めてやったときの感覚に近いものがあった。
