### 1. git pull的时候发生冲突的解决方法

报错提示内容：

```
error: Your local changes to the following files would be overwritten by merge”
```

**方法一、stash**

```
1 git stash
2 git commit
3 git stash pop
```

```
git stash: 备份当前的工作区的内容，从最近的一次提交中读取相关内容，让工作区保证和上次提交的内容一致。同时，将当前的工作区内容保存到Git栈中。
git stash pop: 从Git栈中读取最近一次保存的内容，恢复工作区的相关内容。由于可能存在多个Stash的内容，所以用栈来管理，pop会从最近的一个stash中读取内容并恢复。
git stash list: 显示Git栈内的所有备份，可以利用这个列表来决定从那个地方恢复。
git stash clear: 清空Git栈。此时使用gitg等图形化工具会发现，原来stash的哪些节点都消失了。
```

**方法二、放弃本地修改，直接覆盖**

```
1 git reset --hard
2 git pull
```

**Git回滚代码到某个commit**

```
回退命令：
git reset --hard HEAD^ 回退到上个版本

git reset --hard HEAD~3 回退到前3次提交之前，以此类推，回退到n次提交之前

git reset --hard commit_id 退到/进到，指定commit的哈希码（这次提交之前或之后的提交都会回滚）
```

