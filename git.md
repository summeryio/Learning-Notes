##### Git branch使用

```
https://www.jianshu.com/p/305723736c7c
```



##### 初次提交

```
git init
git add -A
git commit -m ''
git remote add origin <仓库地址>
git push -u origin master
```



##### 当我想从远程仓库里拉取一条本地不存在的分支时

```
git fetch origin dev
git checkout -b 本地分支名 origin/远程分支名
```



##### 推送本地分支到远程分支

```
git checkout -b feature-branch    //创建并切换到分支feature-branch  
git push origin feature-branch:feature-branch    //推送本地的feature-branch(冒号前面的)分支到远程origin的feature-branch(冒号后面的)分支(没有会自动创建)
```

https://www.cnblogs.com/qyf404/p/git_push_local_branch_to_remote.html



##### 删除本地分支并推送

```
git branch -d fix
git push origin :fix
```

