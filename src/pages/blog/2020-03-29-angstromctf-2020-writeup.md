---
templateKey: blog-post
title: angstromCTF 2020 Writeup
date: 2020-03-28T14:37:01.723Z
description: angstrom 2020 Writeup
featuredpost: true
featuredimage: /img/screen-shot-2020-03-28-at-23.55.59.png
tags:
  - CTF
  - Writeup
---
![](/img/screen-shot-2020-03-29-at-0.55.16.png)

## 総評
20200313 08:00 pm(EPT)-20200318 08:00 pm(EPT) (5days)\
今回は一人で参戦。1782チーム中349位。 Binary/Revにはほとんど手を付けられなかったのでそろそろチームアップを真剣に考えていきたい。
このCTFを通してGitのオブジェクト管理について詳しくなった。`.git `からgit flowを復元する問題は楽しかった。

## WEB
### The Magic WordWeb (20pts, 1371/1782)
#### 問題
> Ask and you shall receive...that is as long as you use the magic word.
> Change "give flag" to "please give flag" somehow.
#### 解法
これはヒントが全てで言われた通りに`give flag`と表示している部分をブラウザのdev toolで`please give flag`に書き換えるとflagがゲットできる。\
一応順を追って考えてみると以下のソースをみる。
```html
<div>
    <div class="flexmagic">
        <p id="magic">give flag</p>
    </div>
</div>
<div>
    <p class="hidden">you passed it chief</p>
</div>
<script>
    var msg = document.getElementById("magic");
    setInterval(function() {
        if (magic.innerText == "please give flag") {
            fetch("/flag?msg=" + encodeURIComponent(msg.innerText))
                .then(res => res.text())
                .then(txt => magic.innerText = txt.split``.map(v => String.fromCharCode(v.charCodeAt(0) ^ 0xf)).join``);
        }
    }, 1000);
</script>

```
1s毎にif文内が呼び出されている。(ref. [setInterval()](https://developer.mozilla.org/ja/docs/Web/API/Window/setInterval))

ここで一つ気になることを見つけた。`magic`と`msg`の二つが存在している。\
`msg`は[document.getElementById()](https://developer.mozilla.org/ja/docs/Web/API/Document/getElementById)経由で取得したElementなのはわかるが、`magic`は宣言が存在しない、未定義にならないのだろうかと言うことである。実際にconsoleで挙動を見てみると`msg`と同じくid='magic'のElementが取得されているが、どのような機構なのか気になったので調べてみた(これが可能なら`getElementById()`とかjqueryの`$(#id)`セレクタとか要らないのでは。。。


## CRYPTO
## MISC
### Sanity Check (5pts, solved: 1029/1782)
#### 問題
> Join our Discord! https://discord.gg/Dduuscw
> Hint: Flags are in the format actf{this_is_the_flag}. Check the channel topic of #general.
#### 解法
指定されたDiscordの#generalチャンネルのtopicに書いてあった。これ後で確認しようとした時にたどり着けなかったので途中から非表示になっていた可能性がある。(正解率が低すぎる)
