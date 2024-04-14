
假设有两个Git仓库：

1. github: <https://github.com/jiangxincode/thesis.git>
2. bitbucket: <https://jiangxincode@bitbucket.org/jiangxincode/thesis.git>

现在需要进行合并，保留双方的历史提交记录，并将github的内容删除，合并之后的内容推送到bitbucket中。

从Github上clone仓库到github目录：

```bash
$ git clone https://github.com/jiangxincode/thesis.git github
Cloning into 'github'...
remote: Enumerating objects: 29, done.
remote: Total 29 (delta 0), reused 0 (delta 0), pack-reused 29
Unpacking objects: 100% (29/29), done.
```

从Bitbucket上clone仓库到bitbucket目录：

```bash
$ git clone https://jiangxincode@bitbucket.org/jiangxincode/thesis.git bitbucket
Cloning into 'bitbucket'...
remote: Counting objects: 153, done.
remote: Compressing objects: 100% (150/150), done.
remote: Total 153 (delta 63), reused 0 (delta 0)
Receiving objects: 100% (153/153), 26.68 MiB | 2.64 MiB/s, done.
Resolving deltas: 100% (63/63), done.
```

在合并前根据实际需要分别处理两个目录的内容，并提交上传到远程仓库。

在仓库bitbucket中添加远程仓库github，命名为github:

```bash
$ cd bitbucket/
$ git remote add github ../github/
$ git remote
github
origin
```

检出历史信息:

```bash
$ git fetch github
warning: no common commits
remote: Enumerating objects: 32, done.
remote: Counting objects: 100% (32/32), done.
remote: Compressing objects: 100% (29/29), done.
remote: Total 32 (delta 8), reused 0 (delta 0)
Unpacking objects: 100% (32/32), done.
From ../github
 * [new branch]      master     -> github/master
```

基于github的master分支创建并检出新的分支，名字为github_master:

```bash
$ git checkout -b github_master github/master
Switched to a new branch 'github_master'
Branch 'github_master' set up to track remote branch 'master' from 'github'.
```

切到bitbucket仓库的主线分支:

```bash
$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```

合并基于github创建的分支github_master到仓库bitbucket的master分支上:

```bash
$ git merge github_master  --allow-unrelated-histories
Auto-merging .gitignore
CONFLICT (add/add): Merge conflict in .gitignore
Automatic merge failed; fix conflicts and then commit the result.
```

此处可以看出出现了冲突，需要先解决冲突:

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:

        new file:   tex-source/LICENSE
        new file:   tex-source/Makefile
        new file:   tex-source/abstract.tex
        new file:   tex-source/dtx-style.sty
        new file:   tex-source/englishabstract.tex
        new file:   tex-source/gbt7714-2005.bst
        new file:   tex-source/get_texmf_dir.sh
        new file:   tex-source/jiangxin.bib
        new file:   tex-source/jiangxin.tex
        new file:   tex-source/njulogo.eps
        new file:   tex-source/njuname.eps
        new file:   tex-source/njuthesis.cfg
        new file:   tex-source/njuthesis.cls
        new file:   tex-source/njuthesis.dtx
        new file:   tex-source/njuthesis.ins
        new file:   tex-source/preface.tex

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both added:      .gitignore

$ git add .gitignore

$ git commit
[master 3d6cb22] Merge branch 'github_master'
```

最后push本地所有分支到bitbucket:

```bash
$ git push origin master
Enumerating objects: 37, done.
Counting objects: 100% (37/37), done.
Delta compression using up to 4 threads.
Compressing objects: 100% (32/32), done.
Writing objects: 100% (35/35), 320.42 KiB | 3.56 MiB/s, done.
Total 35 (delta 9), reused 0 (delta 0)
To https://bitbucket.org/jiangxincode/thesis.git
   f92ef9e..3d6cb22  master -> master

$ git push origin github_master:github_master
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create pull request for github_master:
remote:   https://bitbucket.org/jiangxincode/thesis/pull-requests/new?source=github_master&t=1
remote:
To https://bitbucket.org/jiangxincode/thesis.git
* [new branch]      github_master -> github_master
```

此时查看本地和远程的所有分支:

```
$ git branch -a
  github_master
* master
  remotes/github/master
  remotes/origin/HEAD -> origin/master
  remotes/origin/github_master
  remotes/origin/master
  origin/master
```