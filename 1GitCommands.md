# Git 命令


## 设置与配置

### git config
Git 做的很多工作都有一个默认方式。 对于绝大多数工作而言，你可以改变 Git 的默认方式，或者根据你的偏好来设置。 这些设置涵盖了所有的事，从告诉 Git 你的名字，到指定偏好的终端颜色，以及你使用的编辑器。 此命令会从几个特定的配置文件中读取和写入配置值，以便你可以从全局或者针对特定的仓库来进行设置。

    Config file location
        --[no-]global         use global config file
        --[no-]system         use system config file
        --[no-]local          use repository config file
        --[no-]worktree       use per-worktree config file
        -f, --[no-]file <file>
                            use given config file
        --[no-]blob <blob-id> read config from given blob object


### git help
git help 命令用来显示任何命令的 Git 自带文档。 但是我们仅会在此附录中提到大部分最常用的命令，对于每一个命令的完整的可选项及标志列表，你可以随时运行 `git help <command>` 命令来了解。




## 获取与创建项目
### git init
你只需要简单地运行 `git init` 就可以将一个目录转变成一个 Git 仓库，这样你就可以开始对它进行版本管理了。


### git clone
git clone 实际上是一个**封装**了其他几个命令的命令。 它创建了一个新目录，切换到新的目录，然后 `git init` 来初始化一个空的 Git 仓库， 然后为你指定的 URL 添加一个（默认名称为 origin 的）远程仓库（`git remote add`），再针对远程仓库执行 `git fetch`，最后通过 `git checkout` 将远程仓库的最新提交检出到本地的工作目录。




## 快照基础
### git add
git add 命令将内容从工作目录**添加到暂存区**（或称为索引（index）区），以备下次提交。

当 `git commit` 命令执行时，默认情况下它只会检查暂存区域，因此 `git add` 是用来确定下一次提交时快照的样子的。


### git status
git status 命令将为你展示工作区及暂存区域中不同状态的文件。 这其中包含了已修改但未暂存，或已经暂存但没有提交的文件。 一般在它显示形式中，会给你展示一些关于如何在这些暂存区域之间移动文件的提示。


### git diff
当需要查看任意两棵树的差异时你可以使用 git diff 命令。 此命令可以查看你工作环境与你的暂存区的差异（git diff 默认的做法），你暂存区域与你最后提交之间的差异（git diff --staged），或者比较两个提交记录的差异（git diff master branchB）


### git difftool
当你不想使用内置的 git diff 命令时。git difftool 可以用来简单地启动一个外部工具来为你展示两棵树之间的差异。


### git commit
git commit 命令将所有通过 git add 暂存的文件内容在数据库中创建一个持久的快照，然后将当前分支上的分支指针移到其之上。


### git reset
git reset 命令主要用来根据你传递给动作的参数来执行撤销操作。 它可以移动 HEAD 指针并且可选的改变 index 或者暂存区，如果你使用 --hard 参数的话你甚至可以改变工作区。 如果错误地为这个命令附加后面的参数，你可能会丢失你的工作，所以在使用前你要确定你已经完全理解了它。


### git rm
git rm 是 Git 用来从工作区，或者暂存区移除文件的命令。 在为下一次提交暂存一个移除操作上，它与 `git add` 有一点类似。


### git mv
git mv 命令是一个**便利命令**，用于移到一个文件并且在新文件上执行`git add`命令及在老文件上执行`git rm`命令。


### git clean
git clean 是一个用来从工作区中移除不想要的文件的命令。 可以是编译的临时文件或者合并冲突的文件。




## 分支与合并
Git 有几个实现大部的分支及合并功能的实用命令。

### git branch
git branch 命令实际上是某种程度上的分支管理工具。 它可以列出你所有的分支、创建新分支、删除分支及重命名分支。


### git checkout
git checkout 命令用来切换分支，或者检出内容到工作目录。


### git merge
git merge 工具用来合并一个或者多个分支到你已经检出的分支中。 然后它将当前分支指针移动到合并结果上。


### git mergetool
当你在 Git 的合并中遇到问题时，可以使用 git mergetool 来启动一个外部的合并帮助工具。


### git log
git log 命令用来展示一个项目的可达历史记录，从最近的提交快照起。 默认情况下，它只显示你当前所在分支的历史记录，但是可以显示不同的甚至多个头记录或分支以供遍历。 此命令通常也用来在提交记录级别显示两个或多个分支之间的差异。


### git stash
git stash 命令用来临时地保存一些还没有提交的工作，以便在分支上不需要提交未完成工作就可以清理工作目录。


### git tag
git tag 命令用来为代码历史记录中的某一个点指定一个永久的书签。 一般来说它用于发布相关事项。




## 项目分享与更新
在 Git 中没有多少访问网络的命令，几乎所以的命令都是在操作本地的数据库。 当你想要分享你的工作，或者从其他地方拉取变更时，这有几个处理远程仓库的命令。

### git fetch
git fetch 命令与一个远程的仓库交互，并且将远程仓库中有但是在当前仓库的没有的所有信息拉取下来然后存储在你本地数据库中。


### git pull
git pull 命令基本上就是 git fetch 和 git merge 命令的组合体，Git 从你指定的远程仓库中抓取内容，然后马上尝试将其合并进你所在的分支中。


### git push
git push 命令用来与另一个仓库通信，计算你本地数据库与远程仓库的差异，然后将差异推送到另一个仓库中。 它需要有另一个仓库的写权限，因此这通常是需要验证的。


### git remote
git remote 命令是一个是你远程仓库记录的管理工具。 它允许你将一个长的 URL 保存成一个简写的句柄，例如 origin ，这样你就可以不用每次都输入他们了。 你可以有多个这样的句柄，git remote 可以用来添加，修改，及删除它们。


### git archive
git archive 命令用来创建项目一个指定快照的归档文件。


### git submodule
git submodule 命令用来管理一个仓库的其他外部仓库。 它可以被用在库或者其他类型的共享资源上。 submodule 命令有几个子命令, 如（add、update、sync 等等）用来管理这些资源。




## 检查与比较
### git show
git show 命令可以以一种简单的人类可读的方式来显示一个 Git 对象。 你一般使用此命令来显示一个标签或一个提交的信息。


### git shortlog
git shortlog 是一个用来归纳 git log 的输出的命令。 它可以接受很多与 git log 相同的选项，但是此命令并不会列出所有的提交，而是展示一个根据作者分组的提交记录的概括性信息


### git describe
git describe 命令用来接受任何可以解析成一个提交的东西，然后生成一个人类可读的字符串且不可变。 这是一种获得一个提交的描述的方式，它跟一个提交的 SHA-1 值一样是无歧义，但是更具可读性。




## 调试
Git 有一些命令可以用来帮你调试你代码中的问题。 包括找出是什么时候，是谁引入的变更。

### git bisect
git bisect 工具是一个非常有用的调试工具，它通过自动进行一个二分查找来找到哪一个特定的提交是导致 bug 或者问题的第一个提交。


### git blame
git blame 命令标注任何文件的行，指出文件的每一行的最后的变更的提交及谁是那一个提交的作者。 当你要找那个人去询问关于这块特殊代码的信息时这会很有用。


### git grep
git grep 命令可以帮助在源代码中，甚至是你项目的老版本中的任意文件中查找任何字符串或者正则表达式。




## 补丁
Git 中的一些命令是以引入的变更即提交这样的概念为中心的，这样一系列的提交，就是一系列的补丁。 这些命令以这样的方式来管理你的分支。

### git cherry-pick
git cherry-pick 命令用来获得在单个提交中引入的变更，然后尝试将作为一个新的提交引入到你当前分支上。 从一个分支单独一个或者两个提交而不是合并整个分支的所有变更是非常有用的。


### git rebase
git rebase 命令基本是是一个自动化的 cherry-pick 命令。 它计算出一系列的提交，然后再以它们在其他地方以同样的顺序一个一个的 cherry-picks 出它们。


### git revert
git revert 命令本质上就是一个逆向的 git cherry-pick 操作。 它将你提交中的变更的以完全相反的方式的应用到一个新创建的提交中，本质上就是撤销或者倒转。




## 邮件
很多 Git 项目，包括 Git 本身，基本是通过邮件列表来维护的。 从方便地生成邮件补丁到从一个邮箱中应用这些补丁,Git 都有工具来让这些操作变得简单。

### git apply
git apply 命令应用一个通过 git diff 或者甚至使用 GNU diff 命令创建的补丁。 它跟补丁命令做了差不多的工作，但还是有一些小小的差别。


### git am
git am 命令用来应用来自邮箱的补丁。特别是那些被 mbox 格式化过的。 这对于通过邮件接受补丁并将他们轻松地应用到你的项目中很有用。


### git format-patch
git format-patch 命令用来以 mbox 的格式来生成一系列的补丁以便你可以发送到一个邮件列表中。


### git imap-send
git imap-send 将一个由 git format-patch 生成的邮箱上传至 IMAP 草稿文件夹。 我们在 通过邮件的公开项目 一节中见过一个通过使用 git imap-send 工具向一个项目发送补丁进行贡献的例子。

### git send-email
git send-mail 命令用来通过邮件发送那些使用 git format-patch 生成的补丁。


### git request-pull
git request-pull 命令只是简单的用来生成一个可通过邮件发送给某个人的示例信息体。 如果你在公共服务器上有一个分支，并且想让别人知道如何集成这些变更，而不用通过邮件发送补丁，你就可以执行此命令的输出发送给这个你想拉取变更的人。




## 外部系统
Git 有一些可以与其他的版本控制系统集成的命令。

### git svn
git svn 可以使 Git 作为一个客户端来与 Subversion 版本控制系统通信。 这意味着你可以使用 Git 来检出内容，或者提交到 Subversion 服务器。


### git fast-import
对于其他版本控制系统或者从其他任何的格式导入，你可以使用 git fast-import 快速地将其他格式映射到 Git 可以轻松记录的格式。




## 管理
如果你正在管理一个 Git 仓库，或者需要通过一个复杂的方法来修复某些东西，Git 提供了一些管理命令来帮助你。

### git gc
git gc 命令在你的仓库中执行 “garbage collection” ，删除数据库中不需要的文件和将其他文件打包成一种更有效的格式。

此命令一般在背后为你工作，虽然你可以手动执行它。

### git fsck
git fsck 命令用来检查内部数据库的问题或者不一致性。


### git reflog
git reflog 命令分析你所有分支的头指针的日志来查找出你在重写历史上可能丢失的提交。


### git filter-branch
git filter-branch 命令用来根据某些规则来重写大量的提交记录，例如从任何地方删除文件，或者通过过滤一个仓库中的一个单独的子目录以提取出一个项目。




## 底层命令





