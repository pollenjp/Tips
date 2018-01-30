# Useful command on Linux


## xargs

## ファイルのエンコーディング形式変換
```
$ iconv -f <from> -t <to> <file_name> > <output_file_name>
$ iconv -f <from> -t <to> <file_name> -o <output_file_name>
```

### 一括
```
$ find . -type f | xargs file | grep  ":.*" | cut -d: -f1 | xargs -t -I{} iconv -f EUC-JP -t UTF-8 {} -o {}
```

<a href="https://qiita.com/yocifico/items/316bf6fd22b277cf2aa6">テキストファイルを一括でiconv - Qiita</a>


## テキストファイル内の各行の末尾から指定した文字列を取り除く
sed
- <a href="http://itpro.nikkeibp.co.jp/article/COLUMN/20060227/230879/">Linuxコマンド集 - 【 sed 】 文字列の置換，行の削除を行う：ITpro</a>
- <a href="https://qiita.com/takech9203/items/b96eff5773ce9d9cc9b3">sedコマンドの備忘録 - Qiita</a>







