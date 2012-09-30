---
layout: post
title: "RubyMotion の files_dependencies をちょっと助けてくれる gem 'motion-dependencies'"
date: 2012-10-01 00:48
comments: true
categories: [RubyMotion, Ruby]
---

ひとまず、RubyMotion の files_dependencies がとても面倒であるということを伝えたい。
最近 Ruby でコードを書くときは大抵 ActiveSupport::Dependencies のちからを借りて、複雑な依存関係の解決をすべて任せている。

当然のことながら RubyMotion ではこの恩恵はいただくことができない。全く残念である。

# motion-dependencies

ちょっとでも RubyMotion でコンパイルされるファイルの依存関係を指定できないだろうかと探していたらこんなものが。

[motion-dependencies](https://github.com/fleitz/motion-dependencies)

README を見てもちょっとわかりにくいのだが、ソースコード中に '# depends path/to/code.rb' のようなコメントを書けば、
そのソースコードファイルは 'path/to/code.rb' に依存している、ということを指定できるというものだ。

```ruby
    # depends your-mixin.rb
    class FooViewController < UIViewController
      include YourMixin
    end
```

こうすることで、

```ruby
    Motion::Dependencies.find_dependencies(app.files)
    # => {"./foo_view_controller.rb" => ["./your-mixin.rb"]}
```

という結果が得られる。
なので、これを Rakefile に書いてあるように app.file_dependencies に突っ込めばよい。
詳細は README を！

# ひとまずこれで

今作ってるアプリはこれを使っていこうと思う。