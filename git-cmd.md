# GIT常用命令总结

## 常用
| 功能         | 命令                   | 说明         |
| ------------ | ------------           | ------------ |
| 添加修改     | git add file/dir       |              |
| 提交修改     | git commit -m "mesage" |              |
| 拉取更新     | git pull origin branch |              |
| 推送更新     | git push origin branch |              |

## 提交
| 功能           | 命令                       | 说明                     |
| ------------   | ------------               | ------------             |
| 查看提交记录   | git log                    |                          |
| 查看当前commit | git rev-parse --short HEAD |                          |
| 查看提交内容   | git show commit            |                          |
| 对比修改       | git diff                   | 针对未添加到暂存区的情况 |
| 对比修改       | git diff --cached          | 针对已添加到暂存区的情况 |
| 对比提交差异   | git diff commit1 commit2   | 针对已添加到暂存区的情况 |
| 撤销修改       | git checkout file          | 未添加到暂存区           |
| 撤销修改       | git reset HEAD file        | 已添加到暂存区           |
| 取消刚刚的合并 | git reset --merge          |                          |

## 版本
| 功能                          | 命令                       | 说明                           |
| ------------                  | ------------               | ------------                   |
| 回滚到某个commit              | git reset --hard commitid  | 新增内容全部丢失               |
| 回滚到某个commit              | git reset --soft commitid  | 新增内容处于已添加到暂存区状态 |
| 回滚到某个commit              | git reset --mixed commitid | 新增内容处于未添加到暂存区状态 |
| 查看某个commit修改的文件列表  | git log --name-only        |                                |
| 修改最新commit的信息          | git commit --amend         |                                |
| 批量修改commit的作者信息      | git filter-branch --env-filter 'export GIT\_AUTHOR\_EMAIL=new\_author\_email' -- | |

## 分支
| 功能           | 命令                                      | 说明                                 |
| ------------   | ------------                              | ------------                         |
| 新建分支       | git branch branch                         |                                      |
| 新建空白分支   | git checkout --orphan branch              |                                      |
| 切换分支       | git checkout branch                       |                                      |
| 新建并切换分支 | git checkout -b branch                    |                                      |
| 拉取远程新分支 | git checkout -b localbranch origin/branch |                                      |
| 重命名分支     | git branch -m oldbranch newbranch         |                                      |
| 对比分支       | git diff branch1 branch2                  | 显示出所有有差异的文件的详细差异     |
| 删除分支       | git branch -D branch                      |                                      |
| 合并分支       | git merge branch                          | 将branch的commit合并到当前分支       |
| 合并commit     | git cherry-pick commit                    | 将一个分支的特定commit合并到当前分支 |
| 拉取远程分支   | git checkout remotebranch -b localbranch  |                                      |
| 删除远程分支   | git push origin :remote-branch            | 适合所有版本                         |
| 删除远程分支   | git push origin --delete remotebranch     | 适合v1.7.0之后版本                   |
| 清理远程分支   | git remote prune origin                   |                                      |

## 文件
| 功能                   | 命令               | 说明         |
| ------------           | ------------       | ------------ |
| 删除文件               | git rm file        |              |
| 重命令文件             | git mv fileA fileB |              |
| 删除未跟踪的文件和目录 | git clean -fd      |              |

## 归档
| 功能                         | 命令                                                        | 说明         |
| ------------                 | ------------                                                | ------------ |
| 导出代码                     | git archive -o output.tar master                            |              |
| 导出新修改的文件的未修改版本 | git archive -o update.tar HEAD $(git diff --name-only HEAD) |              |
| 提取本地修改的文件并打包     | tar -cvf update.tar $(git diff --name-only HEAD)            |              |

## 配置
| 功能             | 命令                                   | 说明         |
| ------------     | ------------                           | ------------ |
| 设置用户用户名   | git config --global user.name USERNAME |              |
| 设置用户邮箱     | git config --global user.email EMAIL   |              |
| 查看系统配置     | git config --system --list             |              |
| 查看当前用户配置 | git config --global --list             |              |
| 查看当前仓库配置 | git config --local --list              |              |

## 子模块
| 功能                     | 命令                                    | 说明         |
| ------------             | ------------                            | ------------ |
| 添加子模块               | git submodule add URL PATH              |              |
| 克隆所有子模块           | git clone --recursive URL               |              |
| 更新所有子模块           | git submodule foreach git pull          |              |
| 初始化子模块             | git submodule init                      |              |
| 更新子模块               | git submodule update                    |              |
| 初始化(克隆)并更新子模块 | git submodule update --init --recursive |              |

## 远程地址
| 功能                  | 命令                          | 说明         |
| ------------          | ------------                  | ------------ |
| 添加关联的远程仓库URL | git remote add new-origin URL |              |
| 修改关联的远程仓库URL | git remote set-url origin URL |              |
| 删除关联的远程仓库    | git remote rm origin          |              |

## 别名

### 命令行设置
git config --global alias.co checkout
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.df diff
git config --global alias.dft difftool
git config --global alias.dfs 'diff --staged'
git config --global alias.dfts 'difftool --staged'
git config --global alias.mg merge
git config --global alias.mgt mergetool
git config --global alias.lg 'log --abbrev-commit --name-status'
git config --global alias.gp 'log --graph --pretty=format:"%C(auto)%h %C(green)[%an] %C(magenta)(%ad) %Creset%C(auto)%d %s" --date=format:"%Y-%m-%d %H:%M:%S"'
git config --global alias.last 'log -1 HEAD'
git config --global alias.rb 'rebase -i'
git config --global alias.cp 'cherry-pick'

### .gitconfig设置
co = checkout
st = status
ci = commit
br = branch
df = diff
dft = difftool
dfs = diff --staged
dfts = difftool --staged
mg = merge
mgt = mergetool
lg = log --abbrev-commit --name-status
gp = log --graph --pretty=format:\"%C(auto)%h %C(green)[%an] %C(magenta)(%ad) %Creset%C(auto)%d %s\" --date=format:\"%Y-%m-%d %H:%M:%S\"
last = log -1 HEAD
rb = rebase -i
cp = cherry-pick
