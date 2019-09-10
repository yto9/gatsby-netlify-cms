---
templateKey: blog-post
title: Mac OSX で Redash の develop 環境を構築する
date: 2019-09-10T01:19:11.859Z
description: 'Ubuntu 上で用意したDocker Compose '
featuredpost: true
featuredimage: /img/jumbotron.jpg
tags:
  - Mac
  - 環境構築
  - Docker
  - Docker Compose
  - Redash
  - 可視化
---
## Macでの環境構築
以下の`$`から始まる行はシェルコマンドを想定しているのでそれぞれ$を除き、`Terminal`上で実行する。
### Homebrew
#### install (cf.[Homebrew公式](https://brew.sh/))
```sh
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
(途中passwordを2回聞かれる)
#### 確認
```sh
$ brew -v
```
インストールされたHomebrewのバージョンが表示される。
### Docker Composeのインストール
#### Docker環境構築
