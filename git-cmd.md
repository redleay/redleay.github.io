# GIT常用命令总结

## 常用
| 功能 | 命令 | 说明 | 
| ------------ | ------------ | ------------ |
| 添加修改 | git add file/dir |  |
| 提交修改 | git commit -m "mesage" |  |
| 拉取更新 | git pull origin branch |  |
| 推送更新 | git push origin branch |  |

## 提交
| 功能 | 命令 | 说明 |
| ------------ | ------------ | ------------ |
| 查看提交记录 | git log |  |
| 查看当前commit | git rev-parse --short HEAD |  |
| 查看提交内容 | git show commit |  |
| 对比修改 | git diff | 针对未添加到暂存区的情况 |
| 对比修改 | git diff --cached | 针对已添加到暂存区的情况 |
| 撤销修改 | git checkout file | 未添加到暂存区 |
| 撤销修改 | git reset HEAD file | 已添加到暂存区 |
| 取消刚刚的合并 | git reset –merge |  |

## 版本
| 功能 | 命令 | 说明 |
| ------------ | ------------ | ------------ |
| 修改最新commit的信息 | git commit --amend |  |
| 回滚到某个commit | git reset --hard commitid | 新增内容全部丢失 |
| 回滚到某个commit | git reset --soft commitid | 新增内容处于已添加到暂存区状态 |
| 回滚到某个commit | git reset --mixed commitid | 新增内容处于未添加到暂存区状态 |

## 分支
| 功能 | 命令 | 说明 | 
| ------------ | ------------ | ------------ |
| 新建分支 | git branch branch  |  |
| 切换分支 | git checkout branch |   |
| 新建并切换分支 | git checkout -b branch |   |
| 切换分支 | git checkout branch|   |
| 重命名分支  | git branch -m oldbranch newbranch  |   |
| 对比分支 | git diff branch1 branch2 | 显示出所有有差异的文件的详细差异 |
| 删除分支 | git branch -D branch  |   |
| 合并分支 | git merge branch | 将branch的commit合并到当前分支 |
| 合并另一个分支的特定commit到当前分支 | git cherry-pick commit |   |
| 拉取远程分支 | git checkout remote-branch -b local-branch  |   |
| 删除远程分支 | git push origin :remote-branch  |  |
| 清理远程分支 | git remote prune origin |  |

## 文件
| 功能 | 命令 | 说明 | 
| ------------ | ------------ | ------------ |
| 删除文件 | git rm file |  |
| 重命令文件 | git mv fileA fileB |  |
| 删除未跟踪的文件和目录 | git clean -fd |  |

## 归档
| 功能 | 命令 | 说明 | 
| ------------ | ------------ | ------------ |
| 导出代码 | git archive -o output.tar master |  |
| 导出新修改的文件的未修改版本 | git archive -o update.tar HEAD $(git diff --name-only HEAD) |  |
| 提取本地修改的文件并打包 | tar -cvf update.tar $(git diff --name-only HEAD) |  |
