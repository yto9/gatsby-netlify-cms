---
templateKey: blog-post
title: Mac OSX で Redash の develop 環境を構築する
date: 2019-09-10T01:19:11.859Z
description: 'Redashの公式サイトにあるDockerを利用した環境構築をUbuntu, Mac OSで実践する。'
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
### (Homebrew未インストールの場合) Homebrewをインストールする
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
#### (git未インストールの場合)gitをインストールする
```sh
$ brew update
$ brew install git
$ git --version
```
インストールされたgitのバージョンが表示される。
#### (node.js未インストールの場合)node.jsをインストールする
```sh
$ brew install node
$ node -v
```
インストールされたnodeのバージョンが表示される。([参考](https://nodejs.org/en/download/package-manager/#macos))

### (Docker未インストールの場合)Docker Composeのインストール
[Docker comuntiyのforum](https://forums.docker.com/t/installation-docker-toolbox-vs-docker-desktop-mac-mojave/72320)によると[ここ](https://docs.docker.com/docker-for-mac/install/)のrequirementsを満たしている場合はDocker for Mac、そうでない場合にDocker Toolboxを利用することが推奨されている。
#### 確認
Docker Toolboxによる環境変数がセットされていないことを確認する。
```
$ env | grep DOCKER
```
なにも返ってこなければ問題なし。[参考](https://docs.docker.com/docker-for-mac/docker-toolbox/)


#### Docker for Macの環境構築
[Docker hub](https://hub.docker.com/editions/community/docker-ce-desktop-mac)からDockerのアカウントを作成し、インストーラ(Docker.dmg)をダウンロード。

#### Dockerの起動
インストーラを起動し、インストールに成功すると``/Applications``にDockerが入るので`LaunchPad`からDockerを起動する。(PCのuserのpasswordを聞かれる(先程作ったDockerのpasswordではない))
#### 確認
```
$ docker version
```
動いているDockerのclient/server側のバージョンが表示される。
