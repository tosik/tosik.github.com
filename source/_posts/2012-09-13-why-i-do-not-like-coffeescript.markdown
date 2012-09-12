---
layout: post
title: "CofeeScript 書きたくない"
date: 2012-09-13 03:50
comments: true
categories: [CoffeeScript]
---

「Ruby と似た感じにかけるからいいよ」
はじめはそういう謳い文句を聞いて使い始めた CoffeeScript。

```coffeescript
class Hope
  doSomething: () ->
    @eat @getWonderful()
  getWonderful: () ->
    "coffee and donuts"
  eat: (thing) ->
    console.log thing
```


```ruby
class Hope
  def do_something
    eat wonderful
  end

  def wonderful
    "coffee and donuts"
  end

  def eat(thing)
    p thing
  end
end
```

同じようにかけてないよね...


CoffeeScript では、eat は function の呼び出しのための () が引数を与えることで省略できるが、
getWonderful は引数がないので () は省略できない。
これどうしても間違えるよね。今日もコードレビューでこれを１つ訂正してあげた。

記号の多さを見てると perl を思い出して辛い。

underscore.js? backbone.js? jasmine? mocha? しんどい＞＜
jquery だけはぼくの味方。

Rails で CoffeeScript を書いてる時は、ペアプロなのに間違って Ruby で書いてても実行するまで気づかないし、大幅修正が必要になる始末。

みんな JavaScript よりマシだからって理由で妥協してるけど、ほんとにいいの？
node.js が一瞬でも流行った理由が納得出来ない。

