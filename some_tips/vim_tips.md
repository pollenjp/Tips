# vim tips


<vim>
:sp
    - (split)現在編集中にファイルを複製してhorizantalに分割
:vp
    - (vertical)現在編集中にファイルを複製してverticalに分割
:%s/^ *$//g
    - 行頭から行末まで空白だけで構成されている行をの空白を削除
:%s/ *$//g
    - 行末にある空白行をすべて削除
Ctrl-s
    - vimではなくterminalの機能であり、terminalへの入力をロックする
Ctrl-q
    - vimではなくterminalの機能であり、terminalへの入力ロックを解除する

<.vimrc>
https://qiita.com/rita_cano_bika/items/2ae9c8304f8f12b1b443
