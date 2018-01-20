# ctags tips

再帰的にタグを作成
```
$ ctags -R
```

<Ctrl-]>:ジャンプ
<Ctrl-t>:タグに戻る

<Ctrl-w><Ctrl-]>:画面分割＋ジャンプ
<:q>:戻る


```
set tags=tags;
```
を.vimrcに追加すると親ディレクトリからルートまで再帰的にtagsファイルをサーチする


