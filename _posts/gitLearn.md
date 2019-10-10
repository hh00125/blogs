# 学习git的测试库
# git reset 
> 将HEAD和branch指向一个新的commitId

# git revert
> 回退到指定commitId(c1)并在当前commitId(c2)基础上完成一次commit会产生c3

# git rebase
> HEAD和分支会移动到新的操作订单<br>
 1.复制当前commitId(c1)之前所有提交到指定commitId(c2)之后<br> git rebase remotes/origin/dev
 2.--interactive 缩写:-i 调整顺序或者选择之前的commit到指定的commitId之后

# git cherry-pick 
> 复制指定commitId(c1)到当前HEAD上

# git commit 
>    -m '需要提交的消息'<br>
    --amend 将当前的commit保留,创建一个commit
git commit ./ -m 'add当前目录文件并提交'
git commit -a -m '提交所有文件'
git commit -am '提交所有文件'


# git stage

# git describe
> 查看tag
# git stage

# git describe
> 查看tag

# 解决冲突

```
git fetch; git rebase origin/master; git push

git pull --rebase; git push



git fetch; git merge origin/master; git commit; git push

git commit; git fetch; git merge origin/master;  git push

git commit; git pull;git push

```

# git checkout 
```
创建新分支并关联原分支
notMaster origin/master
```

# git branch
```
关联原分支
git branch -u origin/master notMaster

git branch --set-upstream-to=origin/<branch> test
Branch 'test' set up to track remote branch 'test' from 'origin'.

```

# git push
```
git push origin <source>:<destination>
git push origin master

git push origin commit1:master
```

# git delete
删除本地分支： git branch -d dev20181018
如果删除不了可以强制删除，git branch -D dev20181018
有必要的情况下，删除远程分支：git push origin --delete dev20181018
本地会删除foo分支 git push origin :foo

# git clear
> git clear -dfx

# git fetch
```
git fetch origin foo
本地会创建一个foo分支
git fetch origin :foo

本地创建一个pre分支
git fetch origin master:pre
```


# git diff

# git stage
# git stash

# git rm 
```
--cached
```

# git status
>  git status -s 查看变动的的文件

# 解决gitk窗口乱码
git config --global gui.encoding utf-8

# 
