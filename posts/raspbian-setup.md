---
layout: default  
title: Raspbian セットアップ 
---

SDカードにRaspbianを入れて起動するまで。

[NOOBS SETUP](http://www.raspberrypi.org/help/noobs-setup/)

#### 必要なもの

* ディスプレイ
    * HDMI接続の方がおすすめです
* キーボード
* マウス
    * 必須ではないけど、ないと辛い
* LANケーブル(もちろんインターネットに出られるように)


### SDカードのフォーマット

SDアソシエーションのサイトからSDフォーマッターをダウンロード。

* [SDフォーマッター4.0 Windows版](https://www.sdcard.org/jp/downloads/formatter_4/eula_windows/)
* [SDフォーマッター4.0 Mac版](https://www.sdcard.org/jp/downloads/formatter_4/eula_mac/)

たぶん、普通にOSの機能でフォーマットしても同じですが、一応推奨の方法でやります。


### NOOBSのファイルを投入

フォーマット済みのSDカードに、NOOBSのファイルを入れます。

[NOOBS DOWNLOADS](http://www.raspberrypi.org/downloads/)

ZIPを展開して、中身をSDカードに入れるだけ。  
実際のOSインストールに必要なファイルは、インターネットから持ってきます。


### Raspberry Piの電源を入れる

必要な入出力系を繋いだら、Raspberry Piの電源を入れます。  
Raspbianを選択して、あとは待つだけ。

### NOOBSインストーラー

1. Raspbianにチェックを入れてInstallを押す
2. 2GBちょいダウンロードするので、コーヒーでも飲んで待ちましょう
3. イメージのインストールが終わると再起動が掛かります

#### キーボード設定

初期設定では英語キーボードになっているので、ここだけは変えておきましょう。

1. 4.Internationalization Options
2. L3 Keyboard Layout
3. Generic 105 Key
4. Other
5. Japanese
6. OADG109A


### 最初の一歩

初期状態のRaspbianはCUIで立ち上がります。

* ユーザー名 : pi
* パスワード : raspberry

GUIにしたい場合は、ログイン後``startx``しましょう。 
