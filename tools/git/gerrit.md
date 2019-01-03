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