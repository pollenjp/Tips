# raspi 初回時に注意すること
新しく購入したraspiの初期設定をスムーズにするためにいくつかメモ



## raspi usb Wi-Fi

ref:
- <a href="http://denshikousaku.net/raspberry-pi-wifi-lan-usb">Raspberry Piに無線LANのUSBアダプタをつける</a>
- <a href="http://totech.hateblo.jp/entry/2016/12/01/172703">Raspberry Pi 2にWi-Fi USBアダプタで無線LAN接続したときのメモ</a>

## raspi enable ssh

>2. Enable SSH
>
>As of the November 2016 release, Raspbian has the SSH server disabled by default. It can be enabled manually from the desktop:
>
> 1. Launch Raspberry Pi Configuration from the Preferences menu
> 2. Navigate to the Interfaces tab
> 3. Select Enabled next to SSH
> 4. Click OK
>
>Alternatively, raspi-config can be used in the terminal:
>
> 1. Enter sudo raspi-config in a terminal window
> 2. Select Interfacing Options
> 3. Navigate to and select SSH
> 4. Choose Yes
> 5. Select Ok
> 6. Choose Finish
>
>Alternatively, use systemctl to start the service
>
>```
>sudo systemctl enable ssh
>sudo systemctl start ssh
>```


ref:
- <a href="https://www.raspberrypi.org/documentation/remote-access/ssh/">SSH (Secure Shell) - official</a>


## Too many authentication failures
raspiにパスワード認証でsshする必要が有る場合に、Client側の設定で自動で鍵認証してしまい弾かれるパターンがある。それを回避するために明示的パスワード認証であることを示す。

```
ssh username@IPAddress -o PreferredAuthentications=password
```

"$ man ssh"でoオプションについて見てみるとよい。

ref:
- <a href="https://www.google.co.jp/search?client=ubuntu&channel=fs&q=+Too+many+authentication+failures&ie=utf-8&oe=utf-8&gfe_rd=cr&dcr=0&ei=mUFEWr2hN67K8geugISwCQ">Google検索</a>
- <a href="http://d.hatena.ne.jp/kou_i/20101121/1290352589">sshで接続時の「Too many authentication failures for username」エラーの対処法</a>



## raspiに固定IPアドレス

```
/etc/network/interfaces # <-- 通常のLinux
/etc/dhcpcd.conf        # <-- raspiにおけるdhcpcd設定
```

```
$ man dhcpcd.conf
```

で開き、"static"でファイル内検索をかけると見つかる

ref:
- <a href="https://qiita.com/MarieKawasuji/items/b088ffb252a92eee8f5d">Raspberry Pi に固定IPアドレスを割り当てる方法（Raspbian Jessie）- Qiita</a>



## raspi Web server (Apache2)

ref:
- <a href="http://usicolog.nomaki.jp/engineering/raspberryPi/raspberryPi_Apache2.html">Apache2でラズパイをWebサーバに</a>


## raspiに外付けHDDとりつけ

ref:
- <a href="http://denshikousaku.net/raspberry-pi-part2-external-hdd">Raspberry Piでファイルサーバ、Part2 外付けハードディスクの導入編</a>

## raspiでftp server

ref:
- <a href="http://yamaryu0508.hatenablog.com/entry/2014/12/02/102648">Raspberry Piの設定【FTPサーバ（vsftpd）の設定】</a>



