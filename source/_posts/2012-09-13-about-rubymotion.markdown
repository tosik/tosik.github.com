---
layout: post
title: "RubyMotion について感想"
date: 2012-09-13 21:24
comments: true
categories: [RubyMotion, Ruby]
---

個人的な事情で RubyMotion を触り始めた。感想

## iOS SDK が全部そのまま使える

iOS SDK をほとんど制約を受けずにそのまま利用可能だった。
すなわち、UIViewController などのクラスが Ruby から利用できる。

言い換えれば、それ以外のことはほとんどしてくれていないってこと。
Objective-C でやっていた時と同じように使えるので、じゃあ Objective-C で書けばいいじゃんって思う人もいるだろうね。


## Ruby でかける素晴らしさ

RubyMotion の重要なところは、Ruby という言語を扱えることだ。
Ruby が今までに培った文化、思想が iOS アプリケーション開発でも利用できることは Rubyist にとって非常に
大きな事であることは間違いない。

ただ、残念なことがある。


## Ruby っぽくないところは排除されていない

Rubyist なら以下のコードに奇妙さを覚えるだろう。

    def initWithNibName(name, bundle: bundle)
      super
      self.navigationItem.title = 'メインビュー'
      self.tabBarItem = UITabBarItem.alloc.initWithTabBarSystemItem(UITabBarSystemItemFavorites, tag: 1)
    end

これが Ruby だって！？
Camel-Case が非常に気持ち悪い。長ったらしいメソッドが腹立たしい。

こういうコードはいたるところに登場してしまう。
それは、iOS SDK を Objective-C のときと同じインターフェイスでそのまま使用しているからだ。
RubyMotion は iOS SDK を Ruby で扱えるようにしてくれてはいるが、
iOS SDK を Ruby らしいライブラリに置き換えてくれているわけではない。

RubyMotion を初めて使う人はその点を注意していただきたい。


## gems の悲鳴

実は、RubyGems などに上がっているほとんどの gem は RubyMotion では使えない。
まず、require が使えない。また OS に近い操作やメタプログラミングなどがかなり制限されている。
これらの理由により、既存の gem はほぼ使えない。
Rubyist たちがこれまで多くの知恵を絞って生み出されてきた宝石箱は RubyMotion の体質には合わないのだ。

そのかわり、RubyMotion 用に作った gem は bundle install でうまく入れられる。


## Ruby っぽくないところの排除を試みる gem たち

RubyMotion のための gem はいくつかある。
例えば、[sugarcube](https://github.com/fusionbox/sugarcube) は helper collection で、

    self.view.addSubview(subview)

と書かなければならないところを

    self.view << subview

と Ruby らしく書かせてくれるなど、様々な Ruby らしさを RubyMotion に与えてくれる。
似たようなものに [BubbleWrap](https://github.com/mattetti/BubbleWrap) というものもある。


## 結局 iOS SDK

結局のところ、iOS SDK について理解する必要は排除できなかった。
そのために知識を得るために Objective-C が読めなくてはいけなくなり、
Objective-C で書かれたコードをどうやって Ruby に直せばよいか考えるのが面倒になるなんて皮肉は毎日存在する。

DSL で書きたいな、なんて発想が芽生えてしまえば1日はあっという間に過ぎてしまう。
できれば出来上がっていくスピードに驚きながら夜更かししたいものだ。

