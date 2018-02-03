## raspiに固定IPアドレス

```
/etc/network/interfaces # <-- 通常のLinux
/etc/dhcpcd.conf        # <-- raspiにおけるdhcpcd設定
```

```
$ man dhcpcd.conf
```
で開き、"static"でファイル内検索をかけると見つかる
```
# /etc/dhcpcd.conf
interface wlan0
static ip_address=192.168.BBB.XXX/24
static routers=192.168.BBB.YYY              # check your own router setting
static domain_name_servers=192.168.BBB.YYY  # check your own router setting
```

ref:
- <a href="https://qiita.com/MarieKawasuji/items/b088ffb252a92eee8f5d">Raspberry Pi に固定IPアドレスを割り当てる方法（Raspbian Jessie）- Qiita</a>
