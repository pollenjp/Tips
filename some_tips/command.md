# Useful command on Linux


# xargs

# iconv
## ファイルのエンコーディング形式変換
```
$ iconv -f <from> -t <to> <file_name> > <output_file_name>
$ iconv -f <from> -t <to> <file_name> -o <output_file_name>
```

## 一括
```
$ find . -type f | xargs file | grep  ":.*" | cut -d: -f1 | xargs -t -I{} iconv -f EUC-JP -t UTF-8 {} -o {}
```

<a href="https://qiita.com/yocifico/items/316bf6fd22b277cf2aa6">テキストファイルを一括でiconv - Qiita</a>


# sed
## CR+LFからLFへの置換
改行コードがWindowsのものからLinuxのものへと変換する。
```
$ sed -e s/// <file_name> > <file_name>
# '^M'のところは'Ctrl-V' と'Ctrl-M'の同時押しで出力する。つまり、'Ctrl-V-M'
# 標準出力を上書き
```
どうやら'Ctrl-M'は制御コードらしいので、'^M'と表示してくれないらしい。

- <a href="http://www.atmarkit.co.jp/flinux/rensai/linuxtips/164linendm.html">テキストファイルの行末に^Mが表示される</a>
- <a href="http://www.koikikukan.com/archives/2013/10/15-013333.php">改行コードの「^M」を削除する方法: 小粋空間</a>
- <a href="http://itpro.nikkeibp.co.jp/article/COLUMN/20060227/230879/">Linuxコマンド集 - 【 sed 】 文字列の置換，行の削除を行う：ITpro</a>
- <a href="https://qiita.com/takech9203/items/b96eff5773ce9d9cc9b3">sedコマンドの備忘録 - Qiita</a>







