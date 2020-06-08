

# 1. Git基础



## 1.1 安装Git





## 1.2 Git的配置

Git 自带一个 `git config` 的工具来帮助设置控制 Git 外观和行为的配置变量。 这些变量存储在三个不同的位置：

1. `/etc/gitconfig` 文件: **包含系统上每一个用户及他们仓库的通用配置**。 如果在执行 `git config` 时带上 `--system` 选项，那么它就会读写该文件中的配置变量。 （由于它是系统配置文件，因此你需要管理员或超级用户权限来修改它。）
2. `~/.gitconfig` 或 `~/.config/git/config` 文件：只针对**当前用户**。 你可以传递 `--global` 选项让 Git 读写此文件，这会对你系统上 **所有** 的仓库生效。
3. 当前使用仓库的 Git 目录中的 `config` 文件（即 `.git/config`）：**针对该仓库**。 你可以传递 `--local` 选项让 Git 强制读写此文件，虽然默认情况下用的就是它。。 （当然，你需要进入某个 Git 仓库中才能让该选项生效。）

每一个级别会覆盖上一级别的配置，所以 `.git/config` 的配置变量会覆盖 `/etc/gitconfig` 中的配置变量。

你可以通过以下命令查看所有的配置以及它们所在的文件：

```console
$ git config --list --show-origin
```



**用户信息**

```console
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```



**文本编辑器**

```console
$ git config --global core.editor emacs
```

```console
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

**检查配置信息**

```console
$ git config --list
user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

```console
$ git config user.name
John Doe
```



**Note**

由于 Git 会从多个文件中读取同一配置变量的不同值，因此你可能会在其中看到意料之外的值而不知道为什么。 此时，你可以查询 Git 中该变量的 **原始** 值，它会告诉你哪一个配置文件最后设置了该值：  `$ git config --show-origin rerere.autoUpdate file:/home/johndoe/.gitconfig	false`





## 1.3	获取帮助

若你使用 Git 时需要获取帮助，有三种等价的方法可以找到 Git 命令的综合手册（manpage）：

```console
$ git help <verb>
$ git <verb> --help   or  git <verb> -h
$ man git-<verb>
```

这些命令很棒，因为你随时随地可以使用而无需联网。 如果你觉得手册或者本书的内容还不够用，你可以尝试在 Freenode IRC 服务器 https://freenode.net 上的 `#git` 或 `#github` 频道寻求帮助。 这些频道经常有上百人在线，他们都精通 Git 并且乐于助人。

此外，如果你不需要全面的手册，只需要可用选项的快速参考，那么可以用 `-h` 选项获得更简明的 “help” 输出：

```console
$ git add -h
usage: git add [<options>] [--] <pathspec>...

    -n, --dry-run         dry run
    -v, --verbose         be verbose

    -i, --interactive     interactive picking
    -p, --patch           select hunks interactively
    -e, --edit            edit current diff and apply
    -f, --force           allow adding otherwise ignored files
    -u, --update          update tracked files
    --renormalize         renormalize EOL of tracked files (implies -u)
    -N, --intent-to-add   record only the fact that the path will be added later
    -A, --all             add changes from all tracked and untracked files
    --ignore-removal      ignore paths removed in the working tree (same as --no-all)
    --refresh             don't add, only refresh the index
    --ignore-errors       just skip files which cannot be added because of errors
    --ignore-missing      check if - even missing - files are ignored in dry run
    --chmod (+|-)x        override the executable bit of the listed files
```





## 1.4	获取Git仓库

#### 获取 Git 仓库

通常有两种获取 Git 项目仓库的方式：

1. 将尚未进行版本控制的本地目录转换为 Git 仓库；
2. 从其它服务器 **克隆** 一个已存在的 Git 仓库。

两种方式都会在你的本地机器上得到一个工作就绪的 Git 仓库。



**在已存在的目录中初始化仓库**

```console
$ cd <dir>
$ git init
```

该命令将创建一个名为 `.git` 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。 但是，在这个时候，我们仅仅是做了一个初始化的操作，你的项目里的文件还没有被跟踪。

如果在一个已存在文件的文件夹（而非空文件夹）中进行版本控制，你应该开始追踪这些文件并进行初始提交。

```console
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```



**克隆现有的仓库**

如果你想获得一份已经存在了的 Git 仓库的拷贝，比如说，你想为某个开源项目贡献自己的一份力，这时就要用到 `git clone` 命令。 如果你对其它的 VCS 系统（比如说 Subversion）很熟悉，请留心一下你所使用的命令是"clone"而不是"checkout"。 这是 Git 区别于其它版本控制系统的一个重要特性，Git 克隆的是该 Git 仓库服务器上的几乎所有数据，而不是仅仅复制完成你的工作所需要文件。 当你执行 `git clone` 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来

克隆仓库的命令是 `git clone `。比如，要克隆 Git 的链接库 `libgit2`，可以用下面的命令：

```console
$ git clone https://github.com/libgit2/libgit2
```

这会在当前目录下创建一个名为 “libgit2” 的目录。

如果你想在克隆远程仓库的时候，自定义本地仓库的名字，你可以通过额外的参数指定新的目录名：

```console
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

这会执行与上一条命令相同的操作，但目标目录名变为了 `mylibgit`。





## 1.5	记录每次更新到仓库

![Git 下文件生命周期图。](https://git-scm.com/book/en/v2/images/lifecycle.png)

Figure 8. 文件的状态变化周期

请记住，你工作目录下的每一个文件都不外乎这两种状态：**已跟踪** 或 **未跟踪**。 已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后， 它们的状态可能是未修改，已修改或已放入暂存区。简而言之，已跟踪的文件就是 Git 已经知道的文件。

工作目录中除已跟踪文件外的其它所有文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有被放入暂存区。 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态，因为 Git 刚刚检出了它们， 而你尚未编辑过它们。



#### 检查当前文件状态

```
$ git status -h
usage: git status [<options>] [--] <pathspec>...

    -s, --short           show status concisely
    -b, --branch          show branch information
```

如果你使用 `git status -s` 命令或 `git status --short` 命令，你将得到一种格式更为紧凑的输出。

```console
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

新添加的未跟踪文件前面有 `??` 标记，新添加到暂存区中的文件前面有 `A` 标记，修改过的文件前面有 `M` 标记。 输出中有两栏，左栏指明了暂存区的状态，右栏指明了工作区的状态。



#### 跟踪新文件

使用命令 `git add` 开始跟踪一个文件。`git add` 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。



**忽略文件**

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。在这种情况下，我们可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件的模式。

文件 `.gitignore` 的格式规范如下：

- 所有空行或者以 `#` 开头的行都会被 Git 忽略。
- 可以使用标准的 glob 模式匹配，它会递归地应用在整个工作区中。
- 匹配模式可以以（`/`）开头防止递归。
- 匹配模式可以以（`/`）结尾指定目录。
- 要忽略指定模式以外的文件或目录，可以在模式前加上叹号（`!`）取反。

> 所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。 
>
> 星号（`*`）匹配零个或多个任意字符；
>
> `[abc]` 匹配任何一个列在方括号中的字符 （这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）； 
>
> 问号（`?`）只匹配一个任意字符；
>
> 如果在方括号中使用短划线分隔两个字符， 表示所有在这两个字符范围内的都可以匹配（比如 `[0-9]` 表示匹配所有 0 到 9 的数字）。
>
>  使用两个星号（`**`）表示匹配任意中间目录，比如 `a/**/z` 可以匹配 `a/z` 、 `a/b/z` 或 `a/b/c/z` 等。

我们再看一个 `.gitignore` 文件的例子：

```
# 忽略所有的 .a 文件
*.a

# 但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
!lib.a

# 只忽略当前目录下的 TODO 文件，而不忽略 subdir/TODO
/TODO

# 忽略任何目录下名为 build 的文件夹
build/

# 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
doc/*.txt

# 忽略 doc/ 目录及其所有子目录下的 .pdf 文件
doc/**/*.pdf
```



**忽略文件模板集合**

https://github.com/github/gitignore



#### 暂存已修改的文件

可以使用`git add <file>`来暂存已修改的文件。

**文件同时出现在暂存区和非暂存区**

README.md文件被修改，运行`git add README.md`把文件的修改放入暂存区，没有提交，再次对README.md文件进行修改。运行`git status -s`查看文件状态，就会发现README.md文件同时出现在暂存区和非暂存区。这种情况下，如果现在提交，`git commit`只会提交暂存区内的修改。

```console
$ git status -s
MM README.md
```

**查看已暂存和未暂存的修改**

如果 `git status` 命令的输出对于你来说过于简略，而你想知道具体修改了什么地方，可以用 `git diff` 命令。

```
git diff [ <a> [<b>] ] （b版本相较于a版本的差异）
```

一般<b>可以缺省或者<a>、<b>同时缺省。<b>缺省表示b版本默认为工作副本；<a>、<b>同时缺省，表示b版本为工作副本，a版本为暂存区版本。

```
git diff 本身只显示尚未暂存的改动，即看暂存前后的变化
git diff --staged (暂存文件与最后一次提交的文件差异)
git diff --cached 查看已经暂存起来的变化（ --staged 和 --cached 是同义词）
```

```
$ git diff HEAD^ HEAD
diff --git "a/Git/git/1. Git\345\237\272\347\241\200/README.md" "b/Git/git/1. Git\345\237\272\347\241\200/README.md"
index 0c46179..0531583 100644
--- "a/Git/git/1. Git\345\237\272\347\241\200/README.md"
+++ "b/Git/git/1. Git\345\237\272\347\241\200/README.md"
@@ -183,21 +183,107 @@ Figure 8. 文件的状态变化周期

 #### 检查当前文件状态

+```
+$ git status -h
+usage: git status [<options>] [--] <pathspec>...
+
+    -s, --short           show status concisely
+    -b, --branch          show branch information
+```
+

```

```
$ git diff HEAD HEAD^
diff --git "a/Git/git/1. Git\345\237\272\347\241\200/README.md" "b/Git/git/1. Git\345\237\272\347\241\200/README.md"
index 0531583..0c46179 100644
--- "a/Git/git/1. Git\345\237\272\347\241\200/README.md"
+++ "b/Git/git/1. Git\345\237\272\347\241\200/README.md"
@@ -183,107 +183,21 @@ Figure 8. 文件的状态变化周期

 #### 检查当前文件状态

-```
-$ git status -h
-usage: git status [<options>] [--] <pathspec>...
-
-    -s, --short           show status concisely
-    -b, --branch          show branch information
-```
-

```

| Note                                                         |
| ------------------------------------------------------------ |
| Git Diff 的插件版本 在本书中，我们使用 `git diff` 来分析文件差异。 但是你也可以使用图形化的工具或外部 diff 工具来比较差异。 可以使用 `git difftool` 命令来调用 emerge 或 vimdiff 等软件（包括商业软件）输出 diff 的分析结果。 使用 `git difftool --tool-help` 命令来看你的系统支持哪些 Git Diff 插件。 |

**移动文件**

```console
$ git mv README.md README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
```

其实，运行 `git mv` 就相当于运行了下面三条命令：

```console
$ mv README.md README
$ git rm README.md
$ git add README
```

如此分开操作，Git 也会意识到这是一次重命名，所以不管何种方式结果都一样。 两者唯一的区别是，`mv` 是一条命令而非三条命令，直接用 `git mv` 方便得多



#### 提交更新

现在的暂存区已经准备就绪，可以提交了。 在此之前，请务必确认还有什么已修改或新建的文件还没有 `git add` 过， 否则提交的时候不会记录这些尚未暂存的变化。 这些已修改但未暂存的文件只会保留在本地磁盘。 所以，每次准备提交前，先用 `git status` 看下，你所需要的文件是不是都已暂存起来了， 然后再运行提交命令 `git commit`：

```console
$ git commit
```

这样会启动你选择的文本编辑器来输入提交说明。

| Note                                                         |
| ------------------------------------------------------------ |
| 启动的编辑器是通过 Shell 的环境变量 `EDITOR` 指定的，一般为 vim 或 emacs。 当然也可以按照 [起步](https://git-scm.com/book/zh/v2/ch00/ch01-getting-started) 介绍的方式， 使用 `git config --global core.editor` 命令设置你喜欢的编辑器。 |

```
git commit
-m, --message <message> commit message
-v, --verbose         show diff in commit message template
-a, --all             commit all changed files
```



#### 移除文件跟踪

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。 可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。

```
$ git rm -h
usage: git rm [<options>] [--] <file>...
    --cached              only remove from the index
    -f, --force           override the up-to-date check
    -r                    allow recursive removal
```

如果要删除之前修改过或已经放到暂存区的文件，则必须使用强制删除选项 `-f`（译注：即 force 的首字母）。 这是一种安全特性，用于防止误删尚未添加到快照的数据，这样的数据不能被 Git 恢复。

另外一种情况是，我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。 换句话说，你想让文件保留在磁盘，但是并不想让 Git 继续跟踪。使用 `--cached` 选项

删除非空目录需要递归删除，使用`-r`选项。

```sh
Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio
$ git init
Initialized empty Git repository in C:/Users/Druihng/Desktop/sudio/.git/

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ echo "hello" >> hello

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ echo "world" >> world

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git add .
warning: LF will be replaced by CRLF in hello.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in world.
The file will have its original line endings in your working directory.

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git commit -m "init"
[master (root-commit) 091d271] init
 2 files changed, 2 insertions(+)
 create mode 100644 hello
 create mode 100644 world

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
nothing to commit, working tree clean

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git log
commit 091d271951be66e3bde880366d8e5996868eca9c (HEAD -> master)
Author: druihng <druihng@yeah.net>
Date:   Fri May 29 11:11:44 2020 +0800

    init

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm --cached hello
rm 'hello'

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    hello

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello


Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git commit "rm hello"
error: pathspec 'rm hello' did not match any file(s) known to git.

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git log
commit 091d271951be66e3bde880366d8e5996868eca9c (HEAD -> master)
Author: druihng <druihng@yeah.net>
Date:   Fri May 29 11:11:44 2020 +0800

    init

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git commit -m "rm hello"
[master b904b18] rm hello
 1 file changed, 1 deletion(-)
 delete mode 100644 hello

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git log
commit b904b185804fc76d8ace73da16ea5325d3f592b6 (HEAD -> master)
Author: druihng <druihng@yeah.net>
Date:   Fri May 29 11:13:08 2020 +0800

    rm hello

commit 091d271951be66e3bde880366d8e5996868eca9c
Author: druihng <druihng@yeah.net>
Date:   Fri May 29 11:11:44 2020 +0800

    init

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ vim world

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello

no changes added to commit (use "git add" and/or "git commit -a")

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm world
error: the following file has local modifications:
    world
(use --cached to keep the file, or -f to force removal)

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm world --cached
rm 'world'

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello
        world


Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ cat world
world  dd

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git add world
warning: LF will be replaced by CRLF in world.
The file will have its original line endings in your working directory.

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello

no changes added to commit (use "git add" and/or "git commit -a")

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm world
error: the following file has local modifications:
    world
(use --cached to keep the file, or -f to force removal)

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm world --cached
rm 'world'

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello
        world


Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ cat world
world  dd

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git add world
warning: LF will be replaced by CRLF in world.
The file will have its original line endings in your working directory.

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello


Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm world
error: the following file has changes staged in the index:
    world
(use --cached to keep the file, or -f to force removal)

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm -f world
rm 'world'

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello


Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ ll
total 1
-rw-r--r-- 1 Druihng 197121 6 5月  29 11:11 hello

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$
```

注意：空目录不是Git的关注点，文件才是！

```sh
Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
nothing to commit, working tree clean

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ mkdir empty

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
nothing to commit, working tree clean
```

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm world
error: the following file has changes staged in the index:
    world
(use --cached to keep the file, or -f to force removal)

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git rm -f world
rm 'world'

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    world

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello


Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ ll
total 1
-rw-r--r-- 1 Druihng 197121 6 5月  29 11:11 hello

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$
```

注意：空目录不是Git的关注点，文件才是！

​```sh
Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
nothing to commit, working tree clean

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ mkdir empty

Druihng@DESKTOP-CNMOUGE MINGW64 ~/Desktop/sudio (master)
$ git status
On branch master
nothing to commit, working tree clean
```



## 1.6	查看提交历史





## 1.7	撤销操作

在任何一个阶段，你都有可能想要撤消某些操作。注意，有些撤消操作是不可逆的。 这是在使用 Git 的过程中，会因为操作失误而导致之前的工作丢失的少有的几个地方之一。

**撤销对文件的修改**

```
git checkout -- <file>...
```



**取消暂存的文件**

```
git reset HEAD <file>...
```



**修改最后一次提交**【修补提交】

有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 `--amend` 选项的提交命令来重新提交：

```console
$ git commit --amend
```

最终你只会有一个提交——第二次提交将代替第一次提交的结果。

注意：修补提交最明显的价值是可以稍微改进你最后的提交，而不会让“啊，忘了添加一个文件”或者 “小修补，修正笔误”这种提交信息弄乱你的仓库历史。



#### 重置和回滚

**三颗树**

“树” 在我们这里的实际意思是 “文件的集合”。

Git 作为一个系统，是以它的一般操作来管理并操纵这三棵树的：

| 树                | 用途                                             |
| ----------------- | ------------------------------------------------ |
| HEAD              | 上一次提交的快照，下一次提交的父结点【提交节点】 |
| Index             | 预期的下一次提交的快照【暂存区节点】             |
| Working Directory | 沙盒【工作区节点】                               |









**重置 reset**



**回滚**





## 1.8	远程仓库的使用

#### git remote

> Manage the set of repositories ("remotes") whose branches you track.
>
> 

#### 查看远程仓库

```
git remote
git remote -v
```



#### 添加远程仓库

```
git remote add <name> <url>
```



#### 从远程仓库中抓取和拉取



#### 推送到远程仓库





#### 远程仓库的重命名和移除









## 1.9	打标签



## 1.10	Git别名



