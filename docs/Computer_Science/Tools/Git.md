---
statistics: True
comments: true
---

# Git

!!! Abstract
    以下是我在网站上练习时所做的梳理。这边指路[精简版🔗](https://slides.tonycrane.cc/PracticalSkillsTutorial/2023-fall-ckc/lec2/)。

## git 配置

!!! note 
    第一次用的话跟着 [菜鸟教程](https://www.runoob.com/git/git-tutorial.html) 走就可以了。

### 用户信息

```
$ git config --global user.name "Melody"
$ git config --global user.email melody12020831@outlook.com
```

这里设置你的用户名称与邮件地址，如果使用了 `–global` 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事情，Git 都会使用那些信息。

---

### 检查配置信息

如果想要检查你的配置，可以使用 `git config –list` 命令来列出所有 `Git` 当时能找到的配置。

也可以通过输入 `git config` 来检查 `Git` 的某一项配置:

```
$ git config user.name
Melody
```

---

### 获取帮助

有三种查阅方式：

```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```

### 获取 `git` 仓库

```
$ git init
```

该命令将创建一个名为 .git 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。

如果你想获得一份已经存在了的 Git 仓库的拷贝，可以使用 `git clone`

```
$ git clone https://github.com/melody12020831/Notebook/
```

或者下面这条这将执行与上一个命令相同的操作，不过在本地创建的仓库名字变为 `myrepository` 。

```
$ git clone https://github.com/melody12020831/Notebook/ myrepository
```

### 生成新 SSH 密钥

!!! tip
    有关这部分可以移步 [官方文档](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh)

```
$ ssh-keygen -t ed25519 -C "melody12020831@outlook.com"
```

这将以提供的电子邮件地址为标签创建新 SSH 密钥。

```
> Generating public/private ALGORITHM key pair.
```

当系统提示您“Enter a file in which to save the key（输入要保存密钥的文件）”时，可以按 Enter 键接受默认文件位置。 请注意，如果以前创建了 SSH 密钥，则 ssh-keygen 可能会要求重写另一个密钥，在这种情况下，我们建议创建自定义命名的 SSH 密钥。 为此，请键入默认文件位置，并将 id_ALGORITHM 替换为自定义密钥名称。**(直接 `Enter` )**

```
Enter file in which to save the key (/c/Users/YOU/.ssh/id_ALGORITHM):[Press enter]
```

在提示符下，键入安全密码。**(可以直接两个 `Enter` )**

```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

最后得到了两个文件：id_rsa和id_rsa.pub文件已经生成。并且生成的路径也已显示。

- `id_rsa` 文件是私钥，要保存好，放在本地，私钥可以生产公钥，反之不行。
- `id_rsa.pub` 文件是公钥，可以用于发送到其他服务器，或者 `git` 上
- 用记事本之类的软件打开 `id_rsa.pub` 文件，并且复制全部内容。
- 把复制内容放进 `GitHub SSH keys` 中即可。

最后可用 

```
ssh -T git@github.com
```

测试是否成功。

---

!!! Info "一个练习 `git` 的网站"
    [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)

## 常用命令

### 提交

1. `git status` 文件查看当前状态
2. `git add .` 添加所有/ `git add <file>` 添加文件
3. `git status` 查看状态
4. `git commit -m "Your commit message"`
5. `git push origin main`

---

### 创建新分支

- `git branch xxx` 创建分支
- `git checkout xxx` 切换到分支
- `git checkout -b xxx` 创建名为 `xxx` 的分支并切换到该分支

---

### `git merge`

- `git merge bugFix` 在 `main` 分支时，执行该指令得到指向新节点，该新节点指向 `bugFix` 和上一个 `main`

---

### `git rebase`

- `git rebase main bugFix` 当前在 `main` 执行该语句将 `bugFix` 复制粘贴到 `main` 之下。而 `bugFix` 之前的不是同一分支的没有被复制过的也会被复制过去。

---

### `HEAD`

- 如果想看 `HEAD` 指向，可以通过 `cat .git/HEAD` 查看。如果 `HEAD` 指向的是一个引用，还可以用 `git symbolic -ref HEAD` 查看它的指向。

---

### `git log`

因为 `git checkout abcjhsgd` 长长的哈希值十分不便。因此引入相对引用。

相对引用非常给力，这里我介绍两个简单的用法：

- 使用 `^` 向上移动 1 个提交记录
- 使用 `~<num>` 向上移动多个提交记录，如 `~3`。该操作符后面可以跟一个数字（可选，不跟数字时与 `^` 相同，向上移动一次），指定向上移动多少次。

```
git branch -f main HEAD~3
```

上面的命令会将 main 分支强制指向 HEAD 的第 3 级 parent 提交。`-f` 则容许我们将分支强制移动到那个位置。

---

### 撤销变更

- `git reset HEAD~1`

  Git 把 main 分支移回到 `C1`；现在我们的本地代码库根本就不知道有 `C2` 这个提交了。

- `git revert HEAD`

  为了撤销更改并分享给别人，我们需要使用 `git revert` 。在我们要撤销的提交记录后面居然多了一个新提交！这是因为新提交记录 `C2'` 引入了更改 —— 这些更改刚好是用来撤销 `C2` 这个提交的。也就是说 `C2'` 的状态与 `C1` 是相同的。 `revert` 之后就可以把你的更改推送到远程仓库与别人分享啦。

---

### `git cherry-pick`

- `git cherry-pick c2 c4` 将 `c2` 和 `c4` 都复制到当前分支下面来。只要不是自己上游即可。

---

### `git rebase -i`

- `git rebase -i HEAD~4` 交互式， `HEAD` 之前四个都参与。

---

### `git tag`

- `git tag v0 c1` 给 `c1` 上 `v0` 标签。

---

### `git describe`

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

---

### 两个parent节点

- `git checkout HEAD^2` 到不是自己本支的第二个 `parent` 节点。且该操作符支持链式操作。例如 `git checkout HEAD~^2~2` 。

---

### `git fetch`

`git fetch` 并不会改变你本地仓库的状态。它不会更新你的 `main` 分支，也不会修改你磁盘上的文件。所以, 你可以将 `git fetch` 的理解为单纯的下载操作。

“如果我们指定 `<source>:<destination>` 会发生什么呢？”

如果你觉得直接更新本地分支很爽，那你就用冒号分隔的 refspec 吧。不过，你不能在当前切换的分支上干这个事，但是其它分支是可以的。

这里有一点是需要注意的 —— `source` 现在指的是远程仓库中的位置，而 `<destination>` 才是要放置提交的本地仓库的位置。它与 `git push` 刚好相反，这是可以讲的通的，因为我们在往相反的方向传送数据。

`git fetch origin :bar` 如果远程仓库中没有 `bar` ，则是将本地仓库中的 `bar` 删除。

---

### `git pull`

其实有很多方法的 —— 当远程分支中有新的提交时，你可以像合并本地分支那样来合并远程分支。也就是说就是你可以执行以下命令:

- `git cherry-pick o/main`
- `git rebase o/main`
- `git merge o/main`
- 等等

`git pull` 是 `git fetch` 和 `git merge` 的缩写。

`git pull --rebase` 就是 fetch 和 rebase 的简写！

---

### `git push`

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

---

### 远程跟踪

`git checkout -b totallyNotMain o/main` 这意味着你可以在分支 `totallyNotMain` 上执行 `git push` ，将工作推送到远程仓库的 `main` 分支上。

另一种设置远程追踪分支的方法就是使用：`git branch -u` 命令，执行：

```
git branch -u o/main foo
```

这样 `foo` 就会跟踪 `o/main` 了。如果当前就在 foo 分支上, 还可以省略 foo：

```
git branch -u o/main
```

---

## `GitHub`

`git clone https://...`

- 来`clone`一个仓库

---

## 使用 `git` 时的一些报错解决

由于本人水平实在有限，初始阶段总是遇到一些问题，以下是一些对应的解决方法。

### `git push` 时出现 `rejected`

```
To https://github.com/melody12020831/Slides.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/melody12020831/Slides.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

出现这个错误的原因是你本地的分支落后于远程分支，导致 Git 无法直接执行 git push 操作。远程仓库中的内容已经更新，而你的本地分支没有包含这些更新。

解决方法如下：

1. 拉取远程更改

```
git pull origin main
```

- 如果没有冲突，Git 会自动将远程分支的更改合并到你的本地分支。
- 如果有冲突，Git 会提示冲突文件，你需要手动解决冲突后再继续。

2. 解决冲突（如果有）

- 打开冲突文件，根据冲突标记 (<<<<<<、======、>>>>>>) 手动编辑文件，保留需要的代码。
- 编辑完冲突文件后，运行以下命令：

```
git add <冲突文件>
git commit -m "解决冲突"
```

3. 推送更改

在完成合并或解决冲突后，再次尝试推送：

```
git push origin main
```

如果你不想合并远程更改，而是直接覆盖远程分支，可以强制推送（但一般不建议这样做）：

```
git push origin main --force
```

!!! Tip
    注意： 这会删除远程仓库的历史记录，适用于远程仓库没有重要内容的情况。

### `git pull` 时出现 `fatal: refusing to merge unrelated histories`

```
git pull origin main
From https://github.com/melody12020831/Slides
 * branch            main       -> FETCH_HEAD
fatal: refusing to merge unrelated histories
```

解决办法有如下几种：

1. 允许合并不相关的历史

可以通过 --allow-unrelated-histories 参数强制合并：

```
git pull origin main --allow-unrelated-histories
```

- Git 会将本地和远程的历史合并，可能需要手动解决冲突（如果文件内容有冲突）。

2. 覆盖远程仓库

强制推送：

```
git push origin main --force
```

3. 如果你想保留远程仓库的内容

如果远程仓库已有重要内容，而本地仓库还没有修改，可以先克隆远程仓库：

1. 备份本地仓库的更改（例如复制到其他地方）。
2. 克隆远程仓库：

```
git clone https://github.com/melody12020831/Slides.git
```

将本地更改手动复制到克隆的仓库目录，然后提交和推送。

---