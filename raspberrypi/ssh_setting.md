# Raspberry Pi SSH quick setting

# raspi enable ssh
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


# ssh connection
## [Error] Too many authentication failures
raspiにパスワード認証でsshする必要が有る場合に、Client側の設定で自動で鍵認証してしまい弾かれるパターンがある。それを回避するために明示的パスワード認証であることを示す。
```
ssh -o PreferredAuthentications=password <server_username>@<IP_Address>
```

"$ man ssh"でoオプションについて見てみるとよい。

ref:
- <a href="https://www.google.co.jp/search?client=ubuntu&channel=fs&q=+Too+many+authentication+failures&ie=utf-8&oe=utf-8&gfe_rd=cr&dcr=0&ei=mUFEWr2hN67K8geugISwCQ">Google検索</a>
- <a href="http://d.hatena.ne.jp/kou_i/20101121/1290352589">sshで接続時の「Too many authentication failures for username」エラーの対処法</a>

# generate ssh key
```
$ ssh-keygen
```

# [SCP] transport ssh-key file
```
$ scp -o PreferredAuthentications=password ~/.ssh/<id_rsa_key.pub> <server_username>@<ip_address>:~
```

# set public-key
```
$ mkdir .ssh
$ chmod 700 .ssh
$ mv <id_rsa_key.pub> .ssh
$ cd .ssh/
$ touch authorized_keys
$ chmod 600 .ssh
$ cat <id_rsa_key.pub> >> authorized_keys
```

# sshd_config
```
$ sudo vi /etc/ssh/sshd_config
```

# connect raspi server with ssh-key
```
$ ssh -i ~/.ssh/<id_rsa_key> <server_username>@<IP_Address>
```
Note: scp command option of ssh-key is "-I" (large "i")



