---
layout: default  
title: Raspberry Pi+Ruby 準備
---

### 開発環境 足りないもの追加

#### ruby-dev

gemのビルドに必要。

```
$ sudo apt-get install ruby-dev
```

#### Vim

Raspbianに最初から入っているviはtinyvimというショボいVimなので本物を入れる。

```
$ sudo apt-get install vim
```


#### screen

ターミナルで複数画面を使えるようにする。

```
$ sudo apt-get install screen
```

``screen``で起動。

* ``CTRL+A`` ``CTRL+C`` 新規画面作成
* ``CTRL+A`` ``CTRL+N`` ひとつ次の画面に移動
* ``CTRL+A`` ``"`` 画面の一覧を表示

---

### 必須gemを入れる

#### Bundler

[Bundler](http://bundler.io/)

プロジェクトごとにgemのバージョンやインストールの有無を分けてくれる。  
依存関係の解決もBundlerに任せることが多い。

```
$ sudo gem install bundler --no-rdoc --no-ri
```


#### Pry

[pry/pry](https://github.com/pry/pry)

Ruby用のREPL(Read-eval-print loop)。  
最初から入っているIRBよりも高機能。

```
$ sudo gem install pry --no-rdoc --no-ri
```
