---
templateKey: blog-post
title: ThinkPad A285の環境構築
date: 2019-06-18T01:53:17.902Z
description: laptop PCを買い替えたので構成を記録する。
featuredpost: true
featuredimage: /img/00100lportrait_00100_burst20190618131710899_cover.jpg
tags:
  - 環境構築
  - デュアルブート
---
## SSD換装(128GB -> 1TB)

今回は購入直後の端末でOSをクリーンインストールするが、lenovoのサポートページを見るとWindowsのライセンスの認証を確認してから吹っ飛ばした方が安全に思えたので一度Windows 10にログインし、以下の手順でactivationされていることを確認してからSSDを換装した。

> Before you reinstall Windows 10 make sure that your current version of Windows is activated. Select the Start button, then select Settings > Update & security > Activation. If Windows 10 isn’t activated on your device, see Get help with Windows 10 activation errors for more info. 【引用:[lenovo support](https://support.lenovo.com/jp/en/solutions/ht501288)】

[参考](https://superuser.com/questions/1095980/is-the-windows-10-product-key-in-bios)

最小のSSDを選択したので以下の画像のSanDiskの128GB SSDが載っていた。

![](/img/00000img_00000_burst20190616174322515_cover.jpg)

これを[WD BLACK 1TB](https://www.biccamera.com/bc/item/5110430/)に換装した。
筐体を開けるときにネジ穴をなめてしまい絶望していたが、[ネジ外し](https://www.amazon.co.jp/gp/product/B002YMJJ4U/ref=ppx_yo_dt_b_asin_title_o03_s00?ie=UTF8&psc=1)を利用することで無事開けることが出来た。
換装後起動すると以下の画像のようにSSDが認識されていることがわかる。

![](/img/00100lportrait_00100_burst20190616175239633_cover.jpg)

この状態では空のSSDのみで何も出来ないので、OSのbootable USBを用意し適宜インストールしていく。

## Windows 10 + Ubuntu 19.04 dual boot

### bootable USBを用意する

#### Windows 10

#### Ubuntu 19.04

### Secure bootをDisableにする

### Windows 10をインストールする
用意したbootable USBをから起動し、あとはインストーラの指示に従う。インストール後にWindowsからDisk Partitionの割り当てを変更してもいいので必須ではないが、この段階でUbuntu用の領域をfree spaceとしておくと手間が省ける。
Windows環境CTF以外で使うとは思えないがSSDに余裕があるので250GB割り当てた。
### Ubuntu 19.04をインストールする
以下を参考に
- / :20GB
- swap :20GB
- /home :空き容量残りすべて

という割り当てにした。

[参考](https://www.youtube.com/watch?v=u5QyjHIYwTQ) \
[参考](https://help.ubuntu.com/community/DiskSpace)

### 確認

以下のようにGRUBからUbuntuとWindows Boot Managerが選べるようになった。

![](/img/00000img_00000_burst20190618132202040_cover.jpg)
