---
layout: default  
title : TremaでOpenFlow
---

## Ruby2のインストール

``rbenv``を使ってRuby2以上を入れる。  
普通に入れるとビルドで2時間くらいかかるので、バイナリだけコピーしてくる。

### 必要パッケージのインストール

~~~
$ sudo apt-get install openssl libssl-dev libreadline-dev
~~~

### rbenvのインストール

``rbenv``と``ruby-build``を入れて、パスを通す。

~~~
$ git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
$ git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
 
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
 
$ source ~/.bash_profile
~~~

インストール確認。

~~~
$ rbenv -v
rbenv 0.4.0-129-g7e0e85b
~~~

rbenvのディレクトリ構造はこんな感じ。  
ホーム直下に``.rbenv``ディレクトリを作って、その中に全ファイルが入る。

~~~
$ tree -L 2 -d
.
├── bin
├── completions
├── libexec
├── plugins
│   └── ruby-build
├── rbenv.d
│   └── exec
├── shims
├── src
├── test
│   └── libexec
└── versions
    └── 2.1.5
~~~

``versions``下にRuby2.1.5のファイルを置く。

### Ruby2.1.5のバイナリをコピー

ホストから``scp``でコピーし、``.rbenv/versions/``配下に展開。  

~~~
host$ scp 2.1.5.tar.gz pi@192.168.2.2:.rbenv/versions/ 
~~~

~~~
raspi$ cd ~/.rbenv/versions/
raspi$ tar xzvf 2.1.5.tar.gz
raspi$ rm 2.1.5.tar.gz
~~~

確認。

~~~
$ rbenv versions
* system (set by /home/pi/.rbenv/version)
  2.1.5
~~~

---

## Trema-Edgeのビルド

### 必要なパッケージのインストール

パケットキャプチャ系のライブラリ等を入れる。

~~~
$ sudo apt-get install gcc make libpcap-dev libssl-dev
~~~

### trema-edgeのリポジトリをクローン

~~~
$ cd ~
$ git clone https://github.com/trema/trema-edge
$ cd trema-edge
~~~

### Rubyバージョン切り替え、gem取得

~~~
$ rbenv local 2.1.5
$ rbenv exec gem install bundler
$ rbenv exec bundle install
~~~

### Rakefileの編集

そのままだと途中でコケるので、``gcc``のオプションを一部外す。

~~~
$ vi ./Rakefile
~~~

CFLAGSのうち42行目の``Wcast-align``をコメントアウトする。

~~~
  '-Wcast-align',
~~~

頭に``#``をつけた行はコメント。

~~~
#  '-Wcast-align',
~~~

### ビルド

~~~
$ rake
~~~

動作確認。

~~~
$ bin/trema -v
~~~

---

## Trema-Switchのビルド

Trema-EdgeにはオリジナルのOpenFlowSwitchも入っています。  

~~~
$ rake trema_switch
~~~

実行ファイルは変なところにできる。(開発中だから？）  

~~~
$ sudo TREMA_HOME=/tmp/trema ./objects/switch/switch/switch --server_ip=192.168.2.1 --server_port=6653 --datapath_id=1 -i 0x1 -t stdout
~~~



---

## 参考

* [自宅ラック勉強会 #2.8 2012
『RasPiとあのルータで始めるOpenFlow入門』](http://www.srchack.org/pub/JITAKU_RACK/2.8_OpenFlow/RasPi_and_whr-g301n_20121229v1.pdf)
* [Rubyで創るOpenFlowネットワーク - LLまつり](http://www.slideshare.net/yuyarin/ll2013-yuyarin-distpptx)
* [OpenFlow 1.3 対応ソフトウェアスイッチ Trema Switch を使ってみる](http://momijiame.tumblr.com/post/80381408957/openflow-1-3-trema-switch)
