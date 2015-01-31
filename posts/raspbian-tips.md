---
layout: default  
title: Raspbian Tips 
---

### sshの証明書認証

RasPiに証明書を登録しておくと、ssh時にパスワード入力がいらなくなります。ついでにセキュリティ面も強化されます。

#### ssh鍵生成

以下、Macの場合のssh鍵生成方法。(Windowsの人はputtyにジェネレータがついてくるので、それでやって下さい。)

~~~
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/honeniq/.ssh/id_rsa):  # そのままEnter
Enter passphrase (empty for no passphrase):  # そのままEnter
Enter same passphrase again:  # そのままEnter
Your identification has been saved in /Users/honeniq/.ssh/id_rsa.
Your public key has been saved in /Users/honeniq/.ssh/id_rsa.pub.
The key fingerprint is:
74:0f:b0:32:81:53:dc:ca:ea:28:e6:7f:98:00:7b:bc honeniq@usamba.local
The key's randomart image is:
+--[ RSA 2048]----+
|     +o..        |
|    o ...o       |
|     oo.o o      |
|.     o+ . o     |
|.o   .  S   .    |
|..o .            |
| ..+o            |
|..Eo..           |
|oo...            |
+-----------------+
~~~

これで、``~/.ssh``配下にファイルが2つ生成されます。

* ``id_rsa`` 秘密鍵。誰にも見せてはいけない。
* ``id_rsa.pub`` 公開鍵。こっちをRasPiに登録します。

#### RasPiに登録

RasPiの``~/.ssh/authorized_keys``に公開鍵を入れます。  
以下、RasPiのIPアドレスが``192.168.2.2``の場合。

まずPC側から``id_rsa.pub``を転送。

~~~
$ scp ~/.ssh/id_rsa.pub pi@192.168.2.2:.ssh/
~~~

RasPi側で``id_rsa.pub``を``authorized_keys``に追記。

~~~
Mac$ ssh pi@192.168.2.2
RasPi$ cd ~/.ssh
RasPi$ touch authorized_keys
RasPi$ cat id_rsa >> authorized_keys
~~~

---
