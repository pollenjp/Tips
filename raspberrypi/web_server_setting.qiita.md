# Web Server on Raspberry Pi

Let's Encytpt を用いてApache2をHTTPS化

# Apache2 install
```
$ sudo apt install apach2
```

ルーターやMyDNSなどでドメイン名の処理は終わらせておきます。

# HTTPS

## Let's Encrypt! (Stretch)
次のサイトでは現段階では(Stretch)の方法は掲載されていませんがJessieと同様にできました。
<a href="https://letsencrypt.jp/usage/">let's encrypt の使い方 - let's encrypt 総合ポータル</a>

## 1st : Stretch backports
<a href="https://backports.debian.org/Instructions/">Debian Backports ›› Instructions</a>
上のサイトに書かれている通り"/etc/apt/source.list"に以下の内容を書き加えます。
一番下とかに追記して問題ないとおもいます。
```
# /etc/apt/source.list

# add for let's encrypt
deb http://ftp.debian.org/debian Stretch-backports main  # Stretch
```

その状態でアップデートします。
```
pi@raspberrypi:~ $ sudo apt update
取得:1 http://ftp.jp.debian.org/debian stretch-backports InRelease [91.8 kB]
ヒット:2 http://mirrordirector.raspbian.org/raspbian stretch InRelease
エラー:1 http://ftp.jp.debian.org/debian stretch-backports InRelease                                
  公開鍵を利用できないため、以下の署名は検証できませんでした: NO_PUBKEY 8B48AD6246925553 NO_PUBKEY 7638D0442B90D010
ヒット:3 http://archive.raspberrypi.org/debian stretch InRelease
パッケージリストを読み込んでいます... 完了                                                      
W: GPG エラー: http://ftp.jp.debian.org/debian stretch-backports InRelease: 公開鍵を利用できないため、以下の署名は検証できませんでした: NO_PUBKEY 8B48AD6246925553 NO_PUBKEY 7638D0442B90D010
E: リポジトリ http://ftp.jp.debian.org/debian stretch-backports InRelease は署名されていません。
N: このようなリポジトリから更新を安全に行うことができないので、デフォルトでは更新が無効になっています。
N: リポジトリの作成とユーザ設定の詳細は、apt-secure(8) man ページを参照してください。
```

しかし、どうやらエラーが出てしまったようです。
<a href="https://raspberrypi.stackexchange.com/questions/12258/where-is-the-archive-key-for-backports-debian-org">software installation - Where is the archive.key for backports.debian.org? - Raspberry Pi Stack Exchange</a>

```
pi@raspberrypi:~ $ gpg --keyserver pgpkeys.mit.edu --recv-key 8B48AD6246925553
gpg: keybox '/home/pi/.gnupg/pubring.kbx' created
gpg: failed to start the dirmngr '/usr/bin/dirmngr': そのようなファイルやディレクトリはありません
gpg: connecting dirmngr at '/run/user/1000/gnupg/S.dirmngr' failed: そのようなファイルやディレクトリはありません
gpg: keyserver receive failed: dirmngrがありません
```
error
I didn't know what to do.
But there are same people.
<a href="https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=193536">gpg: keyserver receive failed: No dirmngr - Raspberry Pi Forums</a>

```
pi@raspberrypi:~ $ sudo apt install dirmngr
パッケージリストを読み込んでいます... 完了
依存関係ツリーを作成しています                
状態情報を読み取っています... 完了
提案パッケージ:
  pinentry-gnome3 tor
以下のパッケージが新たにインストールされます:
  dirmngr
アップグレード: 0 個、新規インストール: 1 個、削除: 0 個、保留: 88 個。
546 kB のアーカイブを取得する必要があります。
この操作後に追加で 963 kB のディスク容量が消費されます。
取得:1 http://ftp.tsukuba.wide.ad.jp/Linux/raspbian/raspbian stretch/main armhf dirmngr armhf 2.1.18-8~deb9u1 [546 kB]
546 kB を 3秒 で取得しました (177 kB/s)
以前に未選択のパッケージ dirmngr を選択しています。
(データベースを読み込んでいます ... 現在 125615 個のファイルとディレクトリがインストールされています。)
.../dirmngr_2.1.18-8~deb9u1_armhf.deb を展開する準備をしています ...
dirmngr (2.1.18-8~deb9u1) を展開しています...
man-db (2.7.6.1-2) のトリガを処理しています ...
dirmngr (2.1.18-8~deb9u1) を設定しています ...
```

```
pi@raspberrypi:~ $ gpg --keyserver pgpkeys.mit.edu --recv-key 8B48AD6246925553
gpg: /home/pi/.gnupg/trustdb.gpg: trustdb created
gpg: key 8B48AD6246925553: public key "Debian Archive Automatic Signing Key (7.0/wheezy) <ftpmaster@debian.org>" imported
gpg: no ultimately trusted keys found
gpg: Total number processed: 1
gpg:               imported: 1
pi@raspberrypi:~ $ 
```

```
pi@raspberrypi:~ $ gpg -a --export 8B48AD6246925553 | sudo apt-key add -
OK
```
Work!

## 2nd : 
```
(Jessie)
$ sudo apt-get install certbot python-certbot-apache -t jessie-backports
(Stretch)
$ sudo apt-get install certbot python-certbot-apache -t stretch-backports
```
>cron ジョブの自動追加について
>
>Debian パッケージ版の Certbot クライアントは、自動的に cron ジョブを /etc/cron.d/certbot に追加します。この cron ジョブは、毎日2回 certbot renew を実行して、有効期限が近い SSL/TLS サーバ証明書を自動的に更新します。
>
>※有効期限が近い証明書が存在しない場合には、証明書の更新は行われません。

## 3rd : Excute certbot
```
pi@raspberrypi:~ $ certbot
The following error was encountered:
[Errno 13] Permission denied: '/var/log/letsencrypt'
Either run as root, or set --config-dir, --work-dir, and --logs-dir to writeable paths.
```

You have to do with root authentication.
```
pi@raspberrypi:~ $ sudo certbot
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache
Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel): polleninjp@gmail.com

-------------------------------------------------------------------------------
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v01.api.letsencrypt.org/directory
-------------------------------------------------------------------------------
(A)gree/(C)ancel: A

-------------------------------------------------------------------------------
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about EFF and
our work to encrypt the web, protect its users and defend digital rights.
-------------------------------------------------------------------------------
(Y)es/(N)o: N
No names were found in your configuration files. Please enter in your domain
name(s) (comma and/or space separated)  (Enter 'c' to cancel): c 
Please specify --domains, or --installer that will help in domain names autodiscovery, or --cert-name for an existing certificate name.

IMPORTANT NOTES:
 - Your account credentials have been saved in your Certbot
   configuration directory at /etc/letsencrypt. You should make a
   secure backup of this folder now. This configuration directory will
   also contain certificates and private keys obtained by Certbot so
   making regular backups of this folder is ideal.
```

# 4th : 
```
$ sudo certbot certonly --webroot -w /var/www/html -d example.com -d www.example.com
```
```
pi@raspberrypi:~ $ sudo certbot certonly --webroot -w /var/www/html -d example.com -d www.example.com
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator webroot, Installer None
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for example.com
http-01 challenge for www.example.com
Using the webroot path /var/www/html for all unmatched domains.
Waiting for verification...
Cleaning up challenges

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/example.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/example.com/privkey.pem
   Your cert will expire on 2018-05-05. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

```


ref:
- <a href="https://letsencrypt.jp/usage/">let's encrypt の使い方 - let's encrypt 総合ポータル</a>


