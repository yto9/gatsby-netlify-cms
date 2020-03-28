---
templateKey: blog-post
title: 'angstromCTF 2020 Writeup | Web: The Magic Word'
date: 2020-03-28T18:04:45.314Z
description: |-
  Ask and you shall receive...that is as long as you use the magic word. 
  Hint: Change "give flag" to "please give flag" somehow.

  (20pts, solved: 1371/1782)
featuredpost: true
featuredimage: /img/screen-shot-2020-03-29-at-2.54.30.png
tags:
  - CTF
  - angstromCTF2020
  - Writeup
  - Web
---

## 解法

これはヒントが全てで言われた通りに`give flag`と表示している部分をブラウザのdev toolで`please give flag`に書き換えるとflagがゲットできる。

![](/img/screen-shot-2020-03-29-at-2.56.33.png)

### 問題把握

順を追って考えてみると以下のソースをみる。

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

![](/img/screen-shot-2020-03-29-at-2.56.10.png)

ここで一つ気になることを見つけた。`magic`と`msg`の二つが存在している。\
`msg`は[document.getElementById()](https://developer.mozilla.org/ja/docs/Web/API/Document/getElementById)経由で取得したElementなのはわかるが、`magic`は宣言が存在しない、未定義にならないのだろうかと言うことである。実際にconsoleで挙動を見てみると`msg`と同じくid='magic'のElementが取得されているが、どのような機構なのか気になったので調べてみる。(これが可能なら`getElementById(#id)`とかjqueryの`$(#id)`セレクタとか要らないのではと思えてくる。)

![](/img/screen-shot-2020-03-29-at-2.57.15.png)

また、fetchの返り値に対してbit演算を施している様子だがそこの復号はこちらでやる必要はなく上の画像のようにflag formatに整形されたものが画面上に表示される。(`/flag?msg=please give flag`のresponse自体は画像右下の様になっている。)
