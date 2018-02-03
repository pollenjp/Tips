# raspi 初回時に注意すること
新しく購入したraspiの初期設定をスムーズにするためにいくつかメモ



## raspi usb Wi-Fi

ref:
- <a href="http://denshikousaku.net/raspberry-pi-wifi-lan-usb">Raspberry Piに無線LANのUSBアダプタをつける</a>
- <a href="http://totech.hateblo.jp/entry/2016/12/01/172703">Raspberry Pi 2にWi-Fi USBアダプタで無線LAN接続したときのメモ</a>




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



