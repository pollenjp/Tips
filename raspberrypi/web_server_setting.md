# Web Server on Raspberry Pi

# Apache2 install
```
$ sudo apt install apach2
```

# Domain Name Setting
```
```

## Inform my_ipaddress to MyDNS with "crontab"
```
$ crontab -e
# and choose your favarite editor like 'vim'
```
add as below
```
# this command is excuted hourly, at 20 minutes past the hour
20 * * * * <path_to_shell_file>
```

ref:
- <a href="http://usicolog.nomaki.jp/engineering/raspberryPi/raspberryPi_Apache2.html">Apache2でラズパイをWebサーバに</a>
- <a href="https://qiita.com/kaishero/items/ae9c4c845e0176d3d3e3">Raspberry PiでMyDNS.JPにIPアドレスを定期的に通知する - Qiita</a>



# HTTPS
# Let's Encrypt!
```
# /etc/apt/source.list

# add for let's encrypt
deb http://ftp.debian.org/debian jessie-backports main
```

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

I don't have a key, so excute following command to request the key
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

ref:
- <a href="https://letsencrypt.jp/usage/">Let's Encrypt の使い方 - Let's Encrypt 総合ポータル</a>


