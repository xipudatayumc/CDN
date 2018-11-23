WorkSpace---------Temporary Storage--------Local Repository--------Remote Repository
--------------------------------------------------------------------------------------------

>FAQ:
------
Q:GIT 文件有哪四种状态及状态转移？
--------------------------
A:unmodified\modified\staged\untracked,其中staged表示文件已被添加到Temporary Storage。

Q:git status
-------------
A:显示WorkSpace、Temporary storage和Local Ropository的差别(列出untracked 和 modified状态的文件)。

Q:git commit [-a]?
-------------
A:Git commit把Temporary Storage区的内容提交到本地仓库(由staged->unmodified).

Q:git add [parameters can be file,path,or regular expression.]?
-----------
A:把在Workspace中的新增或修改的文件添加到暂存区（由untracked或modified -> staged）

Q:忽略.swp文件？
----------------
A: .gitignore   *.swp

Q:git diff?
-----------
A:git diff 尚未暂存的内容，此命令比较的是工作目录中当前文件和暂存区域快照之间的差异

  git diff --cached(staged) 已暂存的将要添加到下次提交里的内容(即暂存区与本地仓库的差异)

note:请注意，git diff 本身只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动。 
  所以有时候你一下子暂存了所有更新过的文件后，运行 git diff 后却什么也没有，就是这个原因。


Q:git rm[parameters can be file,path or regular express.]
-----------
A:把文件从暂存区中移除(工作区中的也删除);此命令后git commit即可将文件从Git中移除(本地目录)
git rm --cached 将文件只从暂存区中删除，工作区中的保留。


Q:git mv
---------
A: 相当于以下三条命令：mv ,git rm ,git add  


