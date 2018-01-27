# git_tips


## Gitで削除したファイルをコミット
```
$ git rm <file1>
```

###もし削除したファイルをすべてコミットしたい場合
```
$ git rm $(git ls-files --deleted)  
```

## revert commit

```
$ git checkout --hard <hash_value>
```

- <a href="https://stackoverflow.com/questions/4114095/how-to-revert-git-repository-to-a-previous-commit>git checkout - How to revert Git repository to a previous commit? - Stack Overflow</a>

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

## local branch -> remote branch
```
$ git push --set-upstream origin feature_ar_model_sugisaki
```

## localブランチ削除
```
$ git rm -d branch_name     <-- After Merge
$ git rm -D branch_name     <-- Any case
```

## remoteブランチ削除
```
$ git push --delete origin <branch_name>
```

- <a href="https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-both-locally-and-remotely>How do I delete a Git branch both locally and remotely? - Stack Overflow</a>

## gitのコミットログに'#'を先頭に書くことはできない
- <a href='https://stackoverflow.com/questions/9725160/aborting-commit-due-to-empty-commit-message'>git - Aborting commit due to empty commit message - Stack Overflow</a>

## commit log を変更する
```
$ git commit --amend
$ git rebase -i HEAD~3
$ git rebase --continue
```
- <a href="https://www.granfairs.com/blog/staff/git-commit-fix">Gitのコミットメッセージを後から変更する方法をわかりやすく書いてみた | 株式会社グランフェアズ</a>
- <a href="http://www-creators.com/archives/1116">git commit の取り消し&やり直し、完全攻略。 | WWWクリエイターズ</a>

## git merge を取り消す
```
$ git reset --hard ORG_HEAD
$ git reset --hard HEAD^
```
- <a href="http://tweeeety.hateblo.jp/entry/2015/06/13/183036">【git】git mergeを取り消す - tweeeetyのぶろぐ的めも</a>
- <a href="http://labs.timedia.co.jp/2011/01/git-undo-merge.html">gitでマージ作業を中止して元の状態に戻す - TIM Labs</a>

## git reset でブランチの状態を戻す
```
$ git log --oneline
$ git reset --hard <commit>
```
- <a href="http://www-creators.com/archives/1116">git commit の取り消し&やり直し、完全攻略。 | WWWクリエイターズ</a>

## 
```
git push -f
```
<a href="https://qiita.com/ppworks/items/94c0107d98e55f903ea9">反則技 git push -f - Qiita</a>


# reference
- <a href="https://qiita.com/iorionda/items/c7e0aca399371068a9b8">Git で不要になったローカルブランチ・リモートブランチを削除する方法 - Qiita</a>
- <a href="http://www-creators.com/archives/1116">git commit の取り消し&やり直し、完全攻略。 | WWWクリエイターズ</a>



