(1)WorkSpace---------Temporary Storage--------Local Repository--------Remote Repository
--------------------------------------------------------------------------------------------

(2)local branch\remote branch\tracking branch的概念？本地分支和跟踪分支的区别与联系？

(3)如何在本地显示远程分支？建立跟踪分支？将本地分支push到远程？以及删除远程分支？



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


Q:文件提交到本地后，发现有的文件漏提交了，如何补提交？或者如何修改上一次commit 的message信息？
---------------------------------------------
A: git commit --amend,会将暂存区中的内容提交，如果暂存区中没有要commit到本地的内容，则只会修改message信息。


Q:如何撤消暂存区(staged)的文件修改，即取消文件的staged状态改为modified？撤消工作区中文件的修改？
--------------------------
A: git reset HEAD <file>, git checkout -- <file>
note: git status会有提示，git reset HEAD <file>是一个非常危险的操作，有可能丢失本地修改！！！


Q:git push origin master中origin,master的含义？
------------------------
A: orgin是远程仓库的简写，如https://github.com/xipudatayumc/CDN.git；master是远程仓库中的哪个branch；
即把内容push到远程仓库origin的master分支,在git clone时若不指定远程仓库简写，则其default name 为origin；


Q:如何查看需要读写远程仓库使用的Git保存的简写与其对应的URL?
-----------------------------------
A:git remote -v


Q:如何查看本地、远程、所有branch列表？
---------------------
A: git branch -v(v) \ git branch -r -v(v) \git branch -a -v(v),以下是git branch -a -v的显示信息：

* learning                bc0b46b add notes of pro git 2.3 and 2.4
  master                  78170e2 Create a file to record my learning in Git.
  test                    c52addf just a test!additonal commit.
  remotes/origin/HEAD     -> origin/master
  remotes/origin/learning bc0b46b add notes of pro git 2.3 and 2.4
  remotes/origin/master   78170e2 Create a file to record my learning in Git.
  remotes/origin/test     c52addf just a test!additonal commit.
其中前三个显示的是本地分支，后面的是remote分支。


Q:When you have your project at a point that you want to share,you have to push it to upstream,how to do it?
-----------------------------
A:git push [remote-name] [branch-name],如git push origin master


Q:When you want to get more information about remote repository,how to do it?
-------------------------
A:git remote show [remote-name]


Q:How to rename a remote repository` shortname?For instance,you want to rename pb to paul,how to do it?
----------------
A:To rename a remote repository`s shortname,you can run git remote rename .For instance, git remote rename sb paul.
This changes all your remote-tracking branches ,too.What used to be referenced at pb/master is now at paul/master.


Q:如果要使用新的远程code mirror(remote repository name 变了)，应如何做？
----------------------
A:首先remove老的远程仓库，然后添加新的远程仓库即可；
git remote rm old_name; git remote add short_name repository_name.


Q:Which types of tags does Git supports?
---------------
A:lightweight and annotated.A lightweight tag is very much like a branch that doesn`t change--it just 
like a pointer to a specific commit.Annotated tags,however,are stored as full objects in the Git database.


Q:如何列出tags(只显示tag列表，不显示提交信息)?列出v0.1.*相关的tag?同时显示tag信息和commit信息？
------------------
A:(1)git tag(tag是按字母顺序列出的，不是时间顺序);    
(2) git tag -l v0.1.*;                           (3) git show [tag_name].


Q:How to create annotated tags and lightweight tags?
----------------
A:Creating a annotated tag:  git tag -a [tag_name] -m'message';     Creating a lightweight tag:git tag [tag_name];
(Any parameters isNOT necessitated for a lightweight tag.)


Q:How to create a tag for a specific commit?
------------------
A: git tag -a [tag_name] [commitid];


Q:How to share your tags?
-----------
A:默认情况下，git push 命令并不会传送标签到远程仓库服务器上。 在创建完标签后你必须显式地推送标签到共享服务器上。
git push origin [tagname]
Note:如果想要一次性推送很多标签，也可以使用带有 --tags 选项的 git push 命令。 这将会把所有不在远程仓库服务器上的
标签全部传送到那里。


Q:如何删除本地tag\远程tag?
------------
A:
因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
如何要删除一个remote tag，则应先在本地删除,git tag -d [tag_name];
然后删除远程的tag，git push origin :ref/tags/tag_name


Q:当做commit操作时，git保存什么？
----------------
A:When you make a commit,Git stores a commit object that contains a pointer to the snapshot of the content you 
<<staged>>.This object also contains the author`s name and email address,the message that you typed, and pointers 
to the commit or commits that directly came before this commit(its parent or parents):zero parents for initial commit,
one parent for a normal commit,and multiple parents for a commit that result from a merge of two or more branches.


Q:一个branch在git中可理解成什么？
--------------
A:A branch in Git is simply a lightweight pointer to one of commits.The default branch name in Git is master.As you 
start making commits,you are given a master branch that points to the last commit you made.Every time you commit,the
master branch moved automatically.


Q:git中如何新建branch?branch既然是一个movable pointer,那么新建的分支point to___?
------------------
A:git branch [branch_name];  This create a new pointer to the same commit you`re currently on.
The git branch command only created a new branch--It DOESNOT SWITCH TO THAT BRANCH!!!


Q:How does Git know what branch you`re currently on?
-----------------
A:It keeps a special pointer called <<HEAD>>,it is a pointer to the <<LOCAL BRANCH>> you`re currently on.


Q:如何查看当前分支(既HEAD指针指向哪？)以及每一个branch pointer指向哪个commit?
------------
A: git log --oneline --decorate;


Q:git如何创建、检出、查看、删除、合并branch，合并冲突时如何解决conflict?
----------
A:

Q:下面是git log --oneline --graph --all的输出，对其信息作出解释？
A:
*   51f96d4 (HEAD -> learning, origin/learning, merged) merged test branch!
|\
| * c52addf (origin/test, test) just a test!additonal commit.
| *   d8daff7 wMerge branch 'test' of https://github.com/xipudatayumc/CDN into test
| |\
| | * e8411ba modify README.md and learning_file!
| * | 160783a modify README.md and learning_file,just a test!
| |/
* | a9a97f4 add some contents of chapter3!
* | bc0b46b (tag: v0.1-lw, tag: v0.1) add notes of pro git 2.3 and 2.4
* | 8c2936f add some basic contents of pro git 2.1 and 2.2.
|/
* 78170e2 (tag: show, origin/master, origin/HEAD, master) Create a file to record my learning in Git.
* 207fcb6 Initial commit


Q:如何查看当前branch合并了哪些分支？以及还有哪些<<LOCAL>> branch未合并到当前分支？
-------------
A: git branch --merged


Q:git merge合并branch时，合并的是本地还是远程的分支?
------------------
A:当你在使用分支及合并的时候，一切都是在你自己的 Git 仓库中进行的 — 完全不涉及与服务器的交互。


Q:git clone -o name URL 的含义？
--------------


Q:git push origin serverfix:awesomebranch(refs/heads/serverfix:refs/heads/awesomebranch)含义？
--------------
A:将本地的serverfix分支push到远程，其分支名为awesomebranch


Q:如何将远程有而本地没有的数据同步到本地？(如别人push了一个新的分支到远程，如何将其取到本地？)
------------
A:git fetch [remote_name],如git fetch origin;


Q:说明拥有多个远程分支(在不同的服务器上)的项目是如何工作的？
----------


Q:git fetch 做什么工作？通过git fetch获取到的远程分支是否可以直接合并到当前分支？是否可以直接编辑？
----------
A:值得注意的是，在 fetch 操作下载好新的远程分支之后，你仍然无法在本地编辑该远程仓库中的分支。
  换句话说，在本例中，你不会有一个新的 serverfix 分支，有的只是一个你无法移动的 origin/serverfix 指针。
可以通过git merge origin/serverfix合并到当前分支，如果需要在此基础上做开发，需要通过checkout建立该远程分支的跟踪分支
(tracking branch)  git checkout -b serverfix origin/serverfix


Q:如何删除一个远程分支？
------
A:git push [远程名]:[branch_name],即把本地的空白分支，推送到远程作为branch_name分支。 


Q:使用rebase时，应注意什么(什么情况下不应该用rebase操作)？
-----------
A:一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行衍合操作。
When you rebase stuff,you`re abandoning existing commits and createing new ones that are similar buf different.
If you push commits somewhere and others pull them down and base work on them,and then you rewrite those commits
with git rebase and push them up again,you collaborators will have to re-merge their work and things will get messy
when you try to pull their work back into yours.


Q:当执行git checkout experiment; git rebase master;git checkout master;git merge experiment命令时做什么操作？
-------------
A: rebase master,即重新以master为基(即把当前进程合并到master进程，又作为其一个子集了)



