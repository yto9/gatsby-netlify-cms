---
templateKey: blog-post
title: CloudForamtion/SAM cliコマンドの環境構築
date: 2019-06-19T20:52:40.825Z
description: CloudFormation/SAMを利用する時の環境構築ログ。
featuredpost: true
featuredimage: /img/chemex.jpg
tags:
  - CloudFormation
  - SAM
  - awscli
  - aws-sam-cli
---
## 環境構築
基本的に[公式](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install-linux.html)に従う。

### 事前準備
公式のガイドを読むとAWS SAM CLIのインストール前に、
- Docker
- AWS CLI
のインストールが必須とのこと。

### Dockerの環境構築
2019/06/20現在、[disco向けのstableのrepoはない](https://github.com/docker/for-linux/issues/533)ので[cosmic](https://docs.docker.com/install/linux/docker-ce/ubuntu/)向けのものを利用する。[Docker ce 19.03のリリースと共にdiscoがサポートされる](https://github.com/docker/for-linux/issues/533#issuecomment-485914608)ようなのでそしたら貼り替える予定。

[こちら](https://docs.docker.com/install/linux/docker-ce/ubuntu/)の手順に従い、
以下の部分のみ
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
cosmicを見るように変更。
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   cosmic \
   stable"
```

#### (optional)dockerをsudoなしで利用する
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04

### docker-composeのインストール
[ここの](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04)ステップ１ \
以下のエラーが出たが、再ダウンロードすることで解決した。(ダウンロードが途中で失敗していたのか)
```
$ docker-compose --version
Cannot open self /usr/bin/docker-compose or archive /usr/bin/docker-compose.pkg
```

### AWS CLIのインストール
#### wheelを最新にする
awscliのインストール時にSuccessfully installed PyYAML-5.1となっているが、以下のようにerrorを吐いていた。
```
Collecting six>=1.5 (from python-dateutil<3.0.0,>=2.1; python_version >= "2.7"->botocore==1.12.172->awscli)
  Cache entry deserialization failed, entry ignored
  Downloading https://files.pythonhosted.org/packages/73/fb/00a976f728d0d1fecfe898238ce23f502a721c0ac0ecfedb80e0d88c64e9/six-1.12.0-py2.py3-none-any.whl
Building wheels for collected packages: PyYAML
  Running setup.py bdist_wheel for PyYAML ... error
  Complete output from command /home/yto9/repos/cloudformation/bin/python3 -u -c "import setuptools, tokenize;__file__='/tmp/pip-install-i_zqv6b3/PyYAML/setup.py';f=getattr(tokenize, 'open', open)(__file__);code=f.read().replace('\r\n', '\n');f.close();exec(compile(code, __file__, 'exec'))" bdist_wheel -d /tmp/pip-wheel-md3vr1ss --python-tag cp37:
  usage: -c [global_opts] cmd1 [cmd1_opts] [cmd2 [cmd2_opts] ...]
     or: -c --help [cmd1 cmd2 ...]
     or: -c --help-commands
     or: -c cmd --help
  
  error: invalid command 'bdist_wheel'
  
  ----------------------------------------
  Failed building wheel for PyYAML
  Running setup.py clean for PyYAML
Failed to build PyYAML
Installing collected packages: docutils, jmespath, urllib3, six, python-dateutil, botocore, s3transfer, colorama, pyasn1, rsa, PyYAML, awscli
  Running setup.py install for PyYAML ... done
Successfully installed PyYAML-5.1 awscli-1.16.182 botocore-1.12.172 colorama-0.3.9 docutils-0.14 jmespath-0.9.4 pyasn1-0.4.5 python-dateutil-2.8.0 rsa-3.4.2 s3transfer-0.2.1 six-1.12.0 urllib3-1.25.3

```
これを解消するために事前にwheelを最新にしておく。[参考](https://github.com/miguelgrinberg/flasky/issues/379#issuecomment-414116225)\
[この人の言うように](https://github.com/miguelgrinberg/flasky/issues/379#issuecomment-414118324)pythonの仮想環境を作るたびにpipとwheelは最新にしておくことにしてもいいかもしれない。

```
$ python -m pip install wheel --upgrade
Collecting wheel
  Using cached https://files.pythonhosted.org/packages/bb/10/44230dd6bf3563b8f227dbf344c908d412ad2ff48066476672f3a72e174e/wheel-0.33.4-py2.py3-none-any.whl
Installing collected packages: wheel
Successfully installed wheel-0.33.4

```
#### awscliのインストール
[公式のガイド](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)を参照し、
```
$ pip install --upgrade awscli
```
先のwheelを最新にすることで、エラーなくawsコマンドがインストールされたことが確認できた。
```
$ aws --v
aws-cli/1.16.182 Python/3.7.3 Linux/5.0.0-17-generic botocore/1.12.172
```

### SAMコマンドのインストール
こちらはすんなり以下で入った。
```
$ pip install aws-sam-cli
$ sam --version
SAM CLI, version 0.17.0

```
