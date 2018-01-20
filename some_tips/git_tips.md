# git_tips


## Gitで削除したファイルをコミット
```
$ git rm <file1>
```

###もし削除したファイルをすべてコミットしたい場合
```
$ git rm $(git ls-files --deleted)  
```

## localブランチ一覧
```
$ git branch
```

## remoteブランチ一覧
```
$ git branch --remote
```

## すべてのブランチ一覧
```
$ git branch --all
```

## localブランチ削除
```
$ git rm -d branch_name     <-- After Merge
$ git rm -D branch_name     <-- Any case
```

## remoteブランチ削除
```
$ git push --delete origin branch_name
```


# reference
- <a href="https://qiita.com/iorionda/items/c7e0aca399371068a9b8">Git で不要になったローカルブランチ・リモートブランチを削除する方法 - Qiita</a>
