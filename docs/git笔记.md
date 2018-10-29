```git remote prune origin``` 清理远程分支，把远程不存在的分支从本地删除


 放弃本地修改，强制同步远程的master
 ```
 git fetch --all
 git reset --hard origin/master
 ```
