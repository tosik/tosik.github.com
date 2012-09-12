---
layout: post
title: "Octopress のバージョン管理"
date: 2012-09-12 13:50
comments: true
categories: [Octopress, git, version]
---

## 前提
Octopress を正常な方法で github で使える状態にしていれば次のようになっているはず。（もちろん tosik の部分はあなたのユーザ名）

    % git remote -v
    octopress       git://github.com/imathis/octopress.git (fetch)
    octopress       git://github.com/imathis/octopress.git (push)
    origin  git@github.com:tosik/tosik.github.com.git (fetch)
    origin  git@github.com:tosik/tosik.github.com.git (push)

## 記事のソースや Gemfile をバージョン管理したい

    % git branch
    * source

と出るので、ローカルのブランチは Octopress により自動的に source になっている。
なので、そのまま github

    % git push origin source:source

もしくは単に git push で origin すなわち github に source を保存できる。
もちろんコミットしていなければ push されないのは git ユーザならご承知なので割愛。


## Octopress のバージョンは？

次のようにすれば Octopress のバージョンを自分のリポジトリに取り込める。

    % git fetch
    % # octopress の tag が動いてる？
    % git merge v2.0

こうすれば、origin の source では Gemfile や記事のソースとは別で Octopress 自身の差分を取り込むことができる。
エッジバージョンが使いたければ

    % git merge octopress/master

としてしまうこともできるが要注意。
