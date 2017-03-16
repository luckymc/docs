### Git笔记

**git配置**
```
git config --local user.name "xxx"     local优先级高于global
git config --local user.email "xxx"
git config --global user.name "xxx"
git config --list

git config --global core.quotepath false
core.quotepath设为false的话，就不会对0x80以上的字符进行quote。中文显示正常。
```

**差异对比**
```
git diff    当前文件和暂存文件差异

git diff --cached   已经暂存起来的文件和上次提交时的快照之间的差异

git diff —-staged：同--cached
```

**取消跟踪**
```
git rm [file]           取消跟踪并删除文件
git rm --cached [file]  取消跟踪不删除
```

**重命名**
```
git mv [file_from] [file_to]    重命名
```

**提交历史**
```
git log     历史提交
 -p：展开显示每次提交的内容差异
 -2：仅显示最近的两次更新
 --stat：仅显示简要的增改行数统计
 --pretty=[oneline|short|full|fuller|format] 不同格式显示
 --graph：图形显示
 --[sine|after|until|before|author|committer]
```

**提交修改**
```
git commit  提交
     -am "xxxx"：     不需要add暂存直接提交并添加注释
     --amend：修改最后一次提交（先修改后执行此语句）
```

**取消暂存**
```
git reset HEAD [file]   取消commit（保留修改）
git reset --hard commit_id（不保留修改）
```

**取消修改**
```
git checkout -- [file]  取消文件修改（危险）
```

**远程仓库**
```
git remote -v：显示远程仓库及地址
git remote add [shortname] [url]     添加远程仓库
git remote show
git remote rename [from] [to]     重命名
git remote rm [remote-name] 移除
```

**拉取和推送**
```
拉取branch合并到本地当前分支
git pull --rebase origin branch

推送本地分支到远端（会创建远程分支）
git push [remote] [branch]     推送
git push [remote] [local-branch]:[remote-branch]
     # git push origin master
```

**分支**
```
git branch
     -b [branch-name]：创建并切换
     -d [branch-name]：删除
     -v：查看各分支最后一个提交信息
     --merged：查看哪些分支已被并入当前分支
     --no-merged：查看尚未合并的工作
     -a：本地+远程分支
     -r：列出远程分支
     -m [old-name] [new-name]：重命名

查看跟踪分支
git branch -vv
git config -l (--list)

自己创建并push的分支没有track信息，可以手动设置
git branch --set-upstream test origin/test

git checkout [branch-name]

更新远程分支到本地分支
git fetch origin remote-branch:local-branch

git merge [branch-name]     将branch-name合并到当前分支

git checkout -b [branch-name1] [remote-name]/[branch-name2]
git checkout --track origin/serverfix     跟踪分支

git fetch origin
git rebase origin/master
```

**其他**
```
giy中文支持：
locale
git config --global core.quotepath false
git config --unset

git diff HEAD 头指针
```