---
templateKey: blog-post
title: Docker化したMySQLが激重い。。。
date: 2019-06-24T07:39:12.524Z
description: 原因調査
featuredpost: true
featuredimage: /img/products-grid1.jpg
tags:
  - Docker
  - Docker Compose
  - MySQL
---
ん？ホストのmysqlでも23sかかったぞ
Docker上32sだけど
ホストは二回目以降キャッシュがきいて0.xsになる
dockerは効かない。
文字コードのせい？

