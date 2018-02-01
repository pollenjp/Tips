# vim tips
- console
- Command mode
- Insert mode
- Others
- reference

<a href="https://qiita.com/hachi8833/items/7beeee825c11f7437f54">この記事まじでいい</a>

<vim>

## console
### 画面分割
(split)現在編集中にファイルを複製してhorizantalに分割
(vertical)現在編集中にファイルを複製してverticalに分割
```
:sp (<file_name>)
:vp (<file_name>)
```

### 空白除去
```
# 行頭から行末まで空白だけで構成されている行の空白を削除
:%s/^ *$//g
# 行末にある空白行をすべて削除
:%s/ *$//g
```

### エンコーディング (encoding)
FORCING AN ENCODING: If the automatic detection doesn't work you must tell Vim what encoding the file is. <a href="http://vimdoc.sourceforge.net/htmldoc/usr_45.html">Vim documentation: usr_45</a>
```
:e ++enc=CP932
```
- <a href="http://nanasi.jp/articles/howto/file/open-with-format.html">ファイルの文字コード、フォーマットを指定して、読み直す。 </a>
file is.<a href=""></a>


## Command mode
### Searching word
```
*
```
    - 単語の上にカーソルを持ってきて打ち込むと、カーソルより下にある__単語__を後方検索する。
    - ex) 'vi'という単語の上で打つと'vim'という単語はマッチしない。
```
#
```
    - 単語の上にカーソルを持ってきて打ち込むと、カーソルより下にある__単語__を前方検索する。
```
g + *
```
    - 単語の上にカーソルを持ってきて打ち込むと、カーソルより下にある単語が含まれる__文字列__を後方検索する。
    - ex) 'vi'という単語の上で打つと'vi', 'vim'という単語がマッチする。
```
g + #
```
    - 単語の上にカーソルを持ってきて打ち込むと、カーソルより下にある単語が含まれる__文字列__を前方検索する。
    - ex) 'vi'という単語の上で打つと'vi', 'vim'という単語がマッチする。



## Insert mode
> - インサートモードで行頭に何か入力してctrl+xctrl-lと押すと、そのファイルの中にある行のうち入力とマッチした行がずらりと下に表示されて補完できる。つまり「行補完」。ちょうどExcelのセル入力時に上のセルの内容がドロップボックスに表示されるようなあれ。
> インサートモードで何か入力してctrl+pを押すと、現在vimで開かれているすべてのファイルに出現した単語が補完候補として表示される。
> - ファイルパスを入力しかけてctrl-xctrl-fを押すと、現在の環境でのファイルパスを補完してくれる。/etcと打ってからこのキーを押せば/etc/passwdなどの候補が表示される。
> - とここまで書いておいて何だけど、neocomplete というプラグインを入れておくと入力するだけでどんどん補完候補が表示される(ファイルパス補完も行われる)。インストール方法はググればすぐ見つかる。


## Others
Ctrl-s
    - vimではなくterminalの機能であり、terminalへの入力をロックする
Ctrl-q
    - vimではなくterminalの機能であり、terminalへの入力ロックを解除する



<.vimrc>
https://qiita.com/rita_cano_bika/items/2ae9c8304f8f12b1b443


## reference
- <a href="http://kaworu.jpn.org/kaworu/2008-03-29-1.php">vim カーソルの単語を検索する方法</a>
- 
