---
statistics: True
comments: true
---

# Git

!!! Abstract
    以下是我在网站上练习时所做的梳理。这边指路[精简版🔗](https://slides.tonycrane.cc/PracticalSkillsTutorial/2023-fall-ckc/lec2/)。

!!! Info "一个练习 `git` 的网站"
    [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)

## 提交

1. `git status` 文件查看当前状态
2. `git add .` 添加所有/ `git add <file>` 添加文件
3. `git status` 查看状态
4. `git commit -m "Your commit message"`
5. `git push origin main`

## 创建新分支

- `git branch xxx` 创建分支
- `git checkout xxx` 切换到分支
- `git checkout -b xxx` 创建名为 `xxx` 的分支并切换到该分支

## `git merge`

- `git merge bugFix` 在 `main` 分支时，执行该指令得到指向新节点，该新节点指向 `bugFix` 和上一个 `main`

## `git rebase`

- `git rebase main bugFix` 当前在 `main` 执行该语句将 `bugFix` 复制粘贴到 `main` 之下。而 `bugFix` 之前的不是同一分支的没有被复制过的也会被复制过去。

## `HEAD`

- 如果想看 `HEAD` 指向，可以通过 `cat .git/HEAD` 查看。如果 `HEAD` 指向的是一个引用，还可以用 `git symbolic -ref HEAD` 查看它的指向。

## `git log`

因为 `git checkout abcjhsgd` 长长的哈希值十分不便。因此引入相对引用。

相对引用非常给力，这里我介绍两个简单的用法：

- 使用 `^` 向上移动 1 个提交记录
- 使用 `~<num>` 向上移动多个提交记录，如 `~3`。该操作符后面可以跟一个数字（可选，不跟数字时与 `^` 相同，向上移动一次），指定向上移动多少次。

```
git branch -f main HEAD~3
```

上面的命令会将 main 分支强制指向 HEAD 的第 3 级 parent 提交。`-f` 则容许我们将分支强制移动到那个位置。

## 撤销变更

- `git reset HEAD~1`

  Git 把 main 分支移回到 `C1`；现在我们的本地代码库根本就不知道有 `C2` 这个提交了。

- `git revert HEAD`

  为了撤销更改并分享给别人，我们需要使用 `git revert` 。在我们要撤销的提交记录后面居然多了一个新提交！这是因为新提交记录 `C2'` 引入了更改 —— 这些更改刚好是用来撤销 `C2` 这个提交的。也就是说 `C2'` 的状态与 `C1` 是相同的。 `revert` 之后就可以把你的更改推送到远程仓库与别人分享啦。

## `git cherry-pick`

- `git cherry-pick c2 c4` 将 `c2` 和 `c4` 都复制到当前分支下面来。只要不是自己上游即可。

## `git rebase -i`

- `git rebase -i HEAD~4` 交互式， `HEAD` 之前四个都参与。

## `git tag`

- `git tag v0 c1` 给 `c1` 上 `v0` 标签。

## `git describe`

`git describe` 的语法是：

```
git describe <ref>
```

`<ref>` 可以是任何能被 Git 识别成提交记录的引用，如果你没有指定的话，Git 会使用你目前所在的位置（ `HEAD` ）。

它输出的结果是这样的：

```
<tag>_<numCommits>_g<hash>
```

`tag` 表示的是离 `ref` 最近的标签， `numCommits` 是表示这个 `ref` 与 `tag` 相差有多少个提交记录， `hash` 表示的是你所给定的 `ref` 所表示的提交记录哈希值的前几位。当 `ref` 提交记录上有某个标签时，则只输出标签名称。

## 两个parent节点

- `git checkout HEAD^2` 到不是自己本支的第二个 `parent` 节点。且该操作符支持链式操作。例如 `git checkout HEAD~^2~2` 。

## `git fetch`

`git fetch` 并不会改变你本地仓库的状态。它不会更新你的 `main` 分支，也不会修改你磁盘上的文件。所以, 你可以将 `git fetch` 的理解为单纯的下载操作。

“如果我们指定 `<source>:<destination>` 会发生什么呢？”

如果你觉得直接更新本地分支很爽，那你就用冒号分隔的 refspec 吧。不过，你不能在当前切换的分支上干这个事，但是其它分支是可以的。

这里有一点是需要注意的 —— `source` 现在指的是远程仓库中的位置，而 `<destination>` 才是要放置提交的本地仓库的位置。它与 `git push` 刚好相反，这是可以讲的通的，因为我们在往相反的方向传送数据。

`git fetch origin :bar` 如果远程仓库中没有 `bar` ，则是将本地仓库中的 `bar` 删除。

## `git pull`

其实有很多方法的 —— 当远程分支中有新的提交时，你可以像合并本地分支那样来合并远程分支。也就是说就是你可以执行以下命令:

- `git cherry-pick o/main`
- `git rebase o/main`
- `git merge o/main`
- 等等

`git pull` 是 `git fetch` 和 `git merge` 的缩写。

`git pull --rebase` 就是 fetch 和 rebase 的简写！



## `git push`

我们可以为 push 指定参数，语法是：

```
git push <remote> <place>
```

```
git push origin main
```

把这个命令翻译过来就是：

*切到本地仓库中的“main”分支，获取所有的提交，再到远程仓库“origin”中找到“main”分支，将远程仓库中没有的提交记录都添加上去，搞定之后告诉我。*

要同时为源和目的地指定 `<place>` 的话，只需要用冒号 `:` 将二者连起来就可以了：

```
git push origin <source>:<destination>
```

这个参数实际的值是个 refspec，“refspec” 是一个自造的词，意思是 Git 能识别的位置（比如分支 `foo` 或者 `HEAD~1`）

例如 `git push origin foo^:main` 则将 `foo^` 之上没有推送过的推送一遍，并为远程仓库中复制的该一段命名为 `main` 。

`git push origin :foo` 通过给 `push` 传空值 `source` ，成功删除了远程仓库中的 `foo` 分支。

## 远程跟踪

`git checkout -b totallyNotMain o/main` 这意味着你可以在分支 `totallyNotMain` 上执行 `git push` ，将工作推送到远程仓库的 `main` 分支上。

另一种设置远程追踪分支的方法就是使用：`git branch -u` 命令，执行：

```
git branch -u o/main foo
```

这样 `foo` 就会跟踪 `o/main` 了。如果当前就在 foo 分支上, 还可以省略 foo：

```
git branch -u o/main
```

# `GitHub`

`git clone https://...`

- 来`clone`一个仓库

`git config --global user.email "Test@gmail.com"` 

- 初始化时要用，不过第一次用的话跟着 [菜鸟教程](https://www.runoob.com/git/git-tutorial.html) 走就可以了。
