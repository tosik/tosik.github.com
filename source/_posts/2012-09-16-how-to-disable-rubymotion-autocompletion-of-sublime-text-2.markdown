---
layout: post
title: "Sublime Text 2 の RubyMotion AutoComplete を無効にする方法"
date: 2012-09-16 16:03
comments: true
categories: [RubyMotion, Sublime Text 2]
---

最近、VIM から Sublime Text 2 に乗り換えた。
ファイルの検索が早くて、これなしじゃ生きていけなくなってきてる。

前置きはさておき

## でしゃばりやさんの RubyMotion AutoComplete

Sublime Text 2 の RubyMotionSublimeCompletions という自動補完プラグインがあるのだが、
どうも普段の Ruby を書いてる時に、この補完がでしゃばってきて仕方がない。

![でしゃばった補完の例](/images/uploaded/0e49fc87e854a527e52487118f187b87.png)

これは困った。
Command + Shift + p で 'Set Syntax: Ruby' を実行しても改善されない。

## お前の出る幕ではない！

Package Control が入った環境を用意しよう。そしてそれを使って RubyMotion Autocomplete をインストールしよう。Sublime ザムライならみんな入ってると思うけど。

次に、RubyMotion が背中を見せた瞬間をついて Command + Shift + p で 'Package Control: Disable Package' を実行して、'RubyMotion Autocomplete' を選択する。

![不意をついた様子1](/images/uploaded/25d56d7f616991999be4c00a01dfc437.png)

![不意をついた様子2](/images/uploaded/2d97a45a810bf12ba3c4443e7e50cae5.png)

この間 0.5 秒！
パッケージを無効化してやれば、どうあがこうがでしゃばることなどできない。どうだ！

![どうだ、無効化されただろうの例](/images/uploaded/27b506a40114bace8613736a66974cc0.png)

かわいそうなので RubyMotion を書くときは有効化してあげたいので、Command + Shift + p で 'Package Control: Enable Package' を実行して、'RubyMotion Autocomplete' を選択してあげてね。


## もっといい方法

あったらおしえてください。
