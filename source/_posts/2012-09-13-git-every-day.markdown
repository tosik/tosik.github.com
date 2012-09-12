---
layout: post
title: "日常 Git"
date: 2012-09-13 03:14
comments: true
categories: [git]
---

git で普段使ってる自分の操作を紹介。

## 前提

remotes は origin のみ。

いつでも最新にしておきたい fetch

    % git fetch

これで origin の全部を取ってきてる。
これをわかってない人がびっくりするくらい多い。

## トピックブランチづくり

foo というフィーチャーブランチから bar トピックブランチを作りたいとき。

    % git fetch
    % git checkout origin/foo -b foo/bar

ぼくは手元に remote の写しをおいておかない。つねに origin/foo のように remotes refspec から参照している。

## なるべく早めのリベース

git を覚えたての人たちは

    % git checkout foo
    % git pull
    % git checkout foo_bar
    % git rebase foo

などしてるけど、長いし怖いし foo_bar って書きたくない。

だからぼくはいつも

    % git pull --rebase origin foo

ってしてる。ちなみに後述するが、git up って alias にしてる。

## release management をしてるときにもってこい

    % git shortlog origin/foo..origin/master

origin/master とどれくらい離れてるかを author で分類してくれるので、非常にすっきりして見やすい。

誰が何をしてるかだいたい把握してるので、リリースマネージメントをしていた頃は重宝した。

## 過去の修正を過去に戻らず行う

トピックブランチが進むと過去の修正をしたくなることは多々ある。
そういうとき、おもむろに git rebase -i HEAD~5 とかして該当箇所を edit するが、rebase 中の編集ほど怖いものはない。
だからぼくはいつもこうしてる。

編集中に修正が必要だと思ったらまず、コードを修正する！
そして

    % git add -p

で該当する修正のみ選択的にステージへ。

    % git commit -m 'fugafuga'

と、修正したものだけのコミットを適当に作る。

    % git stash
    % git rebase -i HEAD~5

でさかのぼって、さっきの fugafuga を修正したいコミットの直後に移動して squash にして rebase スタート！

だいたいコンフリクトは発生しない。発生するような修正はこの手順だと修正は辛いが、コンフリクトのお陰でこの時点で気づいたりする。
コミットメッセージの編集で fugafuga を消せば、rebase が無事終了して何事もなかったように再開できる。

    % git stash pop

## alias

    git branch -> git br
    git fetch -> git fe
    git pull --rebase origin __current_branch__ -> git up

その設定は

    [alias]
      topic = "!sh -c 'git co $1 -b $1/$2' __dummy__"
      up = "!sh -c 'git pull --rebase origin $1' __dummy__"

詳細は [https://github.com/tosik/dotfiles/blob/master/.gitconfig](https://github.com/tosik/dotfiles/blob/master/.gitconfig)

## 読んでおくべき本

![実用GIT](http://www.oreilly.co.jp/books/images/picture978-4-87311-440-8.gif)

[http://www.oreilly.co.jp/books/9784873114408/](http://www.oreilly.co.jp/books/9784873114408/)

この本を読んでおけば Refspec や git branch の仕組みなど、内部技術に近い理解が進むので、迷うことなく git が取り扱えるようになる。
