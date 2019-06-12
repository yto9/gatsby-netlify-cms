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
  - 検索、フィルターをかけるなら


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

### Node/Edge 等型
[Nodes](https://developers.facebook.com/docs/graph-api/using-graph-api)
> Reading operations almost always begin with a node. A node is an individual object with a unique ID. ...(中略)... To read a node, you query a specific object's ID.  

> would return fields (node properties)

[Edges](https://developers.facebook.com/docs/graph-api/using-graph-api)
> Nodes have edges, which usually can return collections of other nodes which are attached to them. To read an edge, you must include both the node ID and the edge name in the path.

[Fields](https://developers.facebook.com/docs/graph-api/using-graph-api)
> Fields are node properties. When you query a node it returns a set of fields by default
### Graph API
latest: Graph API v3.3 release on April 30, 2019
#### limitation
> Notice that instead of specifying the Feed edge in the path URL (/user/feed), you specify it in the fields parameter (?fields=feed), which allows you to append the .limit(3) argument.

#### Application level rate limitation
> The total number of calls your app can make per hour is 200 times the number of Users. This is not a per User limit. Any individual User can make more than 200 calls per hour, as long as the total for all Users does not exceed the app maximum. For example, if your app has 100 Users, the app can make 20,000 calls per hour. However, your top ten most engaged Users could make 19,000 of those calls.

The number of Users
> The number of Users for your app is calculated using the number of daily active Users and today's new logins. In cases where there are slow periods of daily usage, the weekly active or even monthly active Users are used to calculate the number of Users for your app. Apps with high daily engagement will have higher rate limits than apps with low daily engagement, regardless of the actual number of app installs.
