---
templateKey: blog-post
title: 非公開グループにおけるFacebook API利用
date: 2019-06-08T09:30:26.555Z
description: FB中心のオンラインサロンにおけるアーカイブ構築の記録
featuredpost: false
featuredimage: /img/private-group.jpg
tags:
  - Facebook
  - Graph API
---
## 実現したいこと
Facebookの非公開グループ内にしかないコンテンツへのアクセシビリティを高める。
## issue
- Facebook GroupのUI上、情報キャッチアップが困難
    - フロー型
    - 一覧性の低さ
      - 現状ユニット、スプレッドシートで対応

## restriction
- コンテンツにはCLUBメンバーだけがアクセス出来て欲しい
     - 基本的にはFB上のリンクを表示するサイトを用意することで認証はFBに丸投げしたい

## 要検討
- データの置き場をどこにするか
  - Facebook APIで毎回参照する？


## survey
- Facebook Groups API
  - access token
    - 管理者・モデレータ・メンバー
    - 永続化
  - scope
  - app review
    - 開発用/公開用
  - resource (node - edge)
- アーカイブのような(簡易？)的なものを実装するのには何がいいか
  - netlify
  - Gatsby.js
  - GAS...(はやだなぁ)?

## Question
### モデレータのアクセストークンで要件は満たせるのか？
### アクセストークンの長期・永続化
- 2ヶ月まではデバッガで出来る
- 無期限には/me/accounts にmanage_pages認可付きのアクセストークンが必要 <- app reviewがいる
  - [https://stackoverflow.com/questions/29390945/how-can-i-access-the-posts-of-my-own-fb-page-using-graph-api-version-2-0](https://stackoverflow.com/questions/29390945/how-can-i-access-the-posts-of-my-own-fb-page-using-graph-api-version-2-0)
  - [https://sujipthapa.co/blog/generating-never-expiring-facebook-page-access-token](https://sujipthapa.co/blog/generating-never-expiring-facebook-page-access-token)

### app reviewを受けるか否か？
- 現状宇野さんに見せるプロトタイプって感じだしいらなそう？
  - アクセストークンの話もモデレータ用ログイン画面を用意(ここにレビューが要らなければ)すれば行けそう？
### Page/Group
