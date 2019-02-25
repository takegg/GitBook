# gerrit

---

### gerrit 不能 merge

原因：gerrit代码冲突,按以下步骤解决：

1. 更新你本地仓库 (git fetch) 
>例如：git fetch origin develop,fetch要合并的两个分支
2. 手动运行rebase (git rebase)
3. 解决冲突 (git mergetool)
> 如果REBASE 1/2状态，则git rebase --continue,如不行则尝试git rebase --skip，直到合并完成。
4. 以amend方式commit代码 (git commit --amend)
5. 推送新布丁到Gerrit (git push)

---

### 提交远程报错“implicit merges detected”

原因：git pull origin branchName后没有commit

### 提交后有“submit incloud parents”按钮
原因：有其他人的分支提交后未合入
1. 取消本地提交至最后一个提交正常的指针
2. 审核完所有新的提交后从最后的commit逐一提交，或“submit include parents”可用时一次提交