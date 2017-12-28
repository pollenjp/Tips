# git_tips

したいです。
そんなときはこれ。

```
# Gitで削除したファイルをコミット
$ git rm <file1>
#もし削除したファイルをすべてコミットしたい場合
$ git rm $(git ls-files --deleted)  
```
