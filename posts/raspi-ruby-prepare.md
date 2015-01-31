---
layout: default  
title: Raspberry Pi+Ruby 準備
---

### 開発環境 足りないもの追加

#### ruby-dev

gemのビルドに必要。

~~~
$ sudo apt-get install ruby-dev
~~~

#### Vim

Raspbianに最初から入っているviはtinyvimというショボいVimなので本物を入れる。

~~~
$ sudo apt-get install vim
~~~


#### screen

ターミナルで複数画面を使えるようにする。

~~~
$ sudo apt-get install screen
~~~

``screen``で起動。

* ``CTRL+A`` ``CTRL+C`` 新規画面作成
* ``CTRL+A`` ``CTRL+N`` ひとつ次の画面に移動
* ``CTRL+A`` ``"`` 画面の一覧を表示

---

### Bundler

[Bundler](http://bundler.io/)

プロジェクトごとにgemのバージョンやインストールの有無を分けてくれる。  
依存関係の解決もBundlerに任せることが多い。

~~~
$ sudo gem install bundler --no-rdoc --no-ri
~~~

プロジェクトのルートに``Gemfile``というファイルを置いておいた状態で``bundle install``すると、そのプロジェクト専用にGemをインストールしてくれます。  
特定のバージョンに固定したかったり、システムのGemを汚したくないときに便利。

~~~ruby
source 'https://rubygems.org'

gem 'pry'
~~~

こんな感じで``Gemfile``を書いて、``bundle install``でGemがインストールされます。

~~~shellscript
$ bundle install
Fetching gem metadata from https://rubygems.org/..........
Resolving dependencies...
Installing coderay 1.1.0
Installing method_source 0.8.2
Installing slop 3.6.0
Installing pry 0.10.1
Using bundler 1.7.12
Your bundle is complete!
Use `bundle show [gemname]` to see where a bundled gem is installed.
~~~

---

### Pry

[pry/pry](https://github.com/pry/pry)

Ruby用のREPL(Read-eval-print loop)。  
最初から入っているIRBよりも高機能。

~~~
$ sudo gem install pry --no-rdoc --no-ri
~~~

ソースに``require``で取り込んで、``binding.pry``を呼ぶと、スクリプト実行途中でPryに制御を移すことができます。

~~~ruby
require 'pry'

data = %w['Taro', 'Jiro', 'Saburo']
data.each do |name|
  binding.pry
end
~~~

---

### Lチカお試し

とりあえずRubyでLチカするスクリプトです。 
Raspberry Piから以下を実行してみて下さい。

~~~
$ cd ~ 
$ git clone https://github.com/honeniq/raspi 
$ cd raspi/led_blink 
$ bundle install 
$ sudo ruby led_blink.rb 
~~~

#### やっている内容

1. ``/home/pi``に移動
2. GitHubからスクリプトを取ってくる
3. 取ってきたスクリプトのディレクトリに移動
4. 必要なプラグインを入れる(Bundlerが必要です)
5. スクリプトを実行(Raspberry PiのGPIOを操作するのにroot権限が必要)

スクリプト上でGPIO25番を決め打ちしているので、違うところを使いたい場合は変更して下さい。
