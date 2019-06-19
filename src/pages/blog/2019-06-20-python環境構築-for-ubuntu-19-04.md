---
templateKey: blog-post
title: Python環境構築 for Ubuntu 19.04
date: 2019-06-19T18:58:57.594Z
description: 'pyenv, virtualenv/venvとかシステムのpython使いたくない話'
featuredpost: true
featuredimage: /img/chemex.jpg
tags:
  - Python
  - Python3
  - Python2
  - pip
  - 環境構築
---
## 前提
### Ubuntu 19.04のPythonの前提
Python 3.7.3 が/usr/binに配置されている。pipは初期装備には存在していない。
```
$ which python
#

$ which python3
/usr/bin/python3

$ python3 --version
Python 3.7.3
```
[Release Note for DiscoDingo](https://wiki.ubuntu.com/DiscoDingo/ReleaseNotes)

### PyPAの推奨する仮想環境の管理方法
3系の最新を追う場合や、今回の用にUbuntu 19.04の初期装備(Python 3.7.3)を使う場合はvenvが推奨。
> If you are using Python 3.3 or newer, the venv module is the preferred way to create and manage virtual environments. venv is included in the Python standard library and requires no additional installation.

2系ならvirtualenv使ってねとのこと。
> venv (for Python 3) and virtualenv (for Python 2) allow you to manage separate package installations for different projects. They essentially allow you to create a “virtual” isolated Python installation and install packages into that virtual installation. 
[Installing packages using pip and virtual environments](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)


### (要検証) Pythonの*マイナーバージョン*の指定はvenvでは出来ない？
virtualenvでは以下で指定できる。
```
$ virtualenv -p {指定したいpythonのインタプリタへのpath} hoge
```

## 3系の環境構築
Python3に紐づくpipとvenvを入れる。
```
$ sudo apt install python3-pip
$ sudo apt install python3-venv
```

## 確認
```
$ python3 -m venv hoge

$ source hoge/bin/activate

(hoge) $ which python
/{path-to-hoge}/hoge/bin/python

(hoge) $ python --version
Python 3.7.3

(hoge) $ which pip
/{path-to-hoge}/hoge/bin/pip

(hoge) $ deactivate
$
```
### (要検証) apt で入れるvirtualenvと挙動違うのかな？
### (要検証) 仮想環境内でpip使うからpipは必須っぽい？
### (要検証) 仮想環境内のデフォのpipは外のpipとversionが必ずしも対応していなそう
### (要検証) apt install / purgeでもとの環境は復元できない？(apt cleanしてなかったからキャッシュが効いてた？)
