# 删除远程仓库某文件夹


首先进入你的master文件夹下, Git Bash Here ,打开命令窗口

```shell
$ git pull origin master                    # 将远程仓库里面的项目拉下来

$ dir                                                # 查看有哪些文件夹

$ git rm -r --cached target              # 删除target文件夹
$ git commit -m '删除了target'        # 提交,添加操作说明
$ git push -u origin master               # 将本次更改更新到github项目上去
```