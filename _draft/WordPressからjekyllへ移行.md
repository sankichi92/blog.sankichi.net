---
title: WordPress から Jekyll へ移行
categories:
  - Dev
  - Info
toc: true
---

## 移行した理由

ブログシステムを WordPress から jekyll へ移行した

- サーバー代がかかる
- 管理画面・投稿画面がつらい
- バージョン管理が厳しい
- 個人的に PHP 書かなくなった

ここ1，2年まともに使ってなかったので誤解あるかも
1番の理由はサーバー代 http://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/hosting-wordpress.html

いまさら jekyll かよ
枯れた技術でユーザーも多い
Ruby なので読める
GitHub Pages で無料

## 移行手順

コミットログみてくれ https://github.com/sankichi92/blog.sankichi.net/commits/master

### jekyll によるブログ作成

びっくりするくらい簡単だった
公式ドキュメント

jekyll ブログの作成

https://jekyllrb.com/

### WordPress のインポート

http://import.jekyllrb.com/docs/wordpress/
https://github.com/arthurlacoste/wordpress2jekyll

写真を使ってた記事は削除した
あまり大量のメディアを扱うのは得策ではなさそう

### GitHub Pages

https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/
https://help.github.com/articles/using-a-custom-domain-with-github-pages/

これもドキュメント読みながらやれば簡単

### HTTPS 化

https://www.kaitoy.xyz/2016/07/01/https-support-by-cloudflare/
https://qiita.com/noraworld/items/89dd85a434a7b759e00c

### Minimal Mistakes テーマの適用

https://mmistakes.github.io/minimal-mistakes/
パーマリンクの一致
skin の作成

## 感想
