---
title: 個人開発 Web アプリに GraphQL API を生やして Auth0 で保護した
categories:
  - Dev
---

[『OAuth徹底入門』を読んだ](2020-04-01-oauth_2_in_action.md)流れで、学生のころ個人開発した [LiveLog](https://livelog.ku-unplugged.net/) に GraphQL API を生やして、[Auth0](https://auth0.com/) を使って OAuth 2 で保護してみた。
ドキュメントは https://github.com/sankichi92/LiveLog/wiki にあり、 https://livelog.ku-unplugged.net/graphiql から試すことができる。

## Auth0 を使った API の保護

[Auth0](https://auth0.com/) は認証認可等の Identity に関する機能を提供するマネージドサービスである。
[LiveLog の認証周りは Auth0 を利用して実装している](https://qiita.com/sankichi92/items/a853cc814705884d92b3)ので、これを API の保護にも使うようにした。

実装に関しては、Auth0 のドキュメントやコミュニティの QA が豊富なので、だいたいこれを読むだけでできた。
起点になるドキュメントは https://auth0.com/docs/microsites/protect-api/protect-api である。
リソースサーバーの実装は、アクセストークンが JWT になっているのでこれをいい感じに検証すればよい。

少し工夫したのはクライアントアプリケーションの登録である。
利用者は LiveLog のユーザー（=サークル構成員）だけに限定したかった。
そこで、Third-Party アプリケーションは許可せず、LiveLog から [Auth0 Management API](https://auth0.com/docs/api/management/v2/#!/Clients/post_clients) を介して First-Party アプリケーションを登録できるようにした。

## GraphQL

今回 LiveLog に API を生やすことは決めたものの、それがどう使われるかは不明だった。
とりあえず生やしておけば誰かがいい感じに使ってくれるだろう、とだけ考えていたのである。
そこで、どんなユースケースにもおそらくもっとも柔軟に対応できるであろう [GraphQL](https://graphql.org/) を採用することにした。

GraphQL は職場の一部アプリケーションにも導入されており、どんなものかはなんとなく知っていた。
ただ、ぼく自身はまだ使ったことがなかった。
GraphQL を採用した背景には、一度自分で実装してみたかったというのもある。

LiveLog は Ruby on Rails アプリなので、[graphql-ruby gem](https://graphql-ruby.org/) を使って実装した。
また、設計にあたっては[『初めてのGraphQL』](https://www.oreilly.co.jp/books/9784873118932/)を購入してつまみ読みした。

初めて触った感想としては、[GraphiQL](https://github.com/graphql/graphiql/tree/master/packages/graphiql) や [GraphQL Playground](https://github.com/prisma-labs/graphql-playground) のような API の実験環境が整っているのがとても便利だった。
また、型を定義するだけでドキュメントを自動生成できるのも非常に楽である。
そして何より、クエリを書いてねらい通りのデータを取ってこれると気持ちがよい。

実装に苦労したのは（GraphQL に限らないが）ページング周りである。
まず、Relay Connection の概念を理解するのに苦労した。
次に、N+1 クエリを避けるのに既存の ActiveRecord の仕組みが使えないので [batch-loader gem](https://github.com/exAspArk/batch-loader) を使ったのだが、これも慣れが必要だった。

GraphQL API に関してはまだまだ導入したてで、基本的な query しか実装しておらず利用者もいない。
機能追加したり利用者が現れるようになれば、運用上の難しい点も見えてくるだろうと思う。
