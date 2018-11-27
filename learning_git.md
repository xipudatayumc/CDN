(1)WorkSpace---------Temporary Storage--------Local Repository--------Remote Repository
--------------------------------------------------------------------------------------------

(2)local branch\remote branch\tracking branch的概念？本地分支和跟踪分支的区别与联系？

(3)如何在本地显示远程分支？建立跟踪分支？将本地分支push到远程？以及删除远程分支？

(4)git branch是指向commit，其实质是一个包含该commit对象校验和的文件。

(5)git branch [branch_name]建一个分支指向当前commit,git checkout branch_name,切换当前分支(HEAD指针),在你切换分支之前，保持好一个干净的状态.

(6)--cached(--staged) HEAD分别指什么？

(7) git diff [filename]?比较工作区与暂存区; git diff --cached [filename]比较暂存区与上交提交的差异;都是靠近用户的文件在后面。
（以上都会列出详细变,若只想查看概况加--stat）
(8)git branch --no-merged,git branch --merged,列出未合并和已合并的分支,如果分支未合并git branch -d删除时会失败。
(9)分支开发工作流:master,develop,topic;  合并某一个branch的commitgit cherry-pick (commitid1..commitid100]
   (像pick樱桃一样的小心)
(10)cherry-pick产生的提交日志中会显示:
"开发者B" commited with "开发者C" on "某年某月某日"
问题是: B和C谁才是原始作者呢?
答案是B是原作者, C是cherry-pick者

(11)合并时若有冲突会有多个commitid，自动合并的一个commitid，解决冲突后又是一个commitid
(12)git ls-remote (remote)显示远程分支列表,git remote show (remote)显示远程分支的详细信息
git remote show origin
* remote origin
  Fetch URL: https://github.com/xipudatayumc/test.git
  Push  URL: https://github.com/xipudatayumc/test.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (fast-forwardable)

(13)推送本地的serverfix分支来更新远程repository的awesomebranch分支，
   git push origin serverfix:awesomebranch
   git push origin refs/heads/serverfix:refs/heads/awesomebranch
(14)git fetch origin ,(更新远程仓库引用)这个命令查找 “origin” 是哪一个服务器，从中抓取本地没有的数据，并且更新本地数据库，移动 origin/master 指针指向新的、更新后的位置。
(15) 远程跟踪分支是远程分支状态的引用,它们以 (remote)/(branch) 形式命名,其是只读的不能直接编辑。
跟踪分支是与远程分支有直接关系的本地分支。 如果在一个跟踪分支上输入 git pull/push，Git 能自动地识别去哪个服务器上抓取、合并到哪个分支。

(16)建立远程跟踪分支: git branch dev origin/master
设置一个本地分支(当前分支)跟踪一个远程分支:git branch -u [remote_branch],可以通过 @{upstream} 或 @{u} 快捷方式来引用它。
(17) git branch -vv -a
  master                7ea67db [origin/master] Initial commit //本地分支及其对应的远程分支
* test                  fb89f93 [origin/master: ahead 1] first modify on test branch
  remotes/origin/master 7ea67db Initial commit

(18)git 删除远程branch,git push origin --delete branch_name 
(19)提交的代码不能包含不必要的空行(git diff --check),提交的注释用标题+加行+说明的格式(git commit 直接调出文档，
而不是-m加注释)且imperative mood
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


Q:通过git rebase让提交者解决conflict，而不是让code maintainer去解决?
--------
A:


Q:Git commit时生成的提交对象，是包含_____的指针？
git add README test.rb LICENSE;git commit -m 'The initial commit of my project'创建的提交对象、树对象？
-------
A:我们可以很自然的想到——该提交对象会包含一个指向<<暂存内容快照>>的指针.


Q:解释git log --oneline --graph --all的输出:git log --oneline --graph --all
------------
* 7ea67db (HEAD -> topic, origin/master, origin/HEAD, master) Initial commit.
本地有哪些分支？远端有哪些分支？本地的当前分支是？这些分支分别指向哪些提交对象？


Q:git log --oneline --graph --all和git log --oneline --graph的区别？
-------
A:--all显示所有分支的commit，没有--all只显示当前分支的commit.


Q:以下信息表明总共有多少local\remote分支？所有的分支分别指向哪些commit？本地当前分支是？
(1)
* aad98da (HEAD -> topic) edit topic branch--1
* 7ea67db (origin/master, origin/HEAD, master) Initial commit
(2)
* aad98da (topic) edit topic branch--1
* 7ea67db (HEAD -> master, origin/master, origin/HEAD) Initial commit

(3)总共有哪些分支？分别指向哪些commit？本地当前分支为？本地分支是否diverged？当个分支先diverged？
* c238f33 (HEAD -> master) edit master branch--1
| * aad98da (topic) edit topic branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(4)有哪些分支？分别指向？本地当前分支是？
* c238f33 (HEAD -> hotfix, master) edit master branch--1
| * aad98da (topic) edit topic branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(5)有哪些分支？分别指向哪些commit？本地当前分支是？
* 2154097 (HEAD -> hotfix) fix a bug on master branch
* c238f33 (master) edit master branch--1
| * aad98da (topic) edit topic branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(6)git checkout master
Switched to branch 'master' //切换到本地master分支
Your branch is ahead of 'origin/master' by 1 commit.//现在的分支(本地master领先远端master origin/master一个提交)
  (use "git push" to publish your local commits)//可以通过git push发布local commits(到远端master,origin/master)

(7)git merge hotfix   //(假设HEAD->master,c238f33..2154097)
Updating c238f33..2154097()//更新master使其指向新的commitid(所提交对象的checksum)
Fast-forward          //做一次Fast-forward
 README.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

由:
* 2154097 (hotfix) fix a bug on master branch
* c238f33 (HEAD -> master) edit master branch--1
| * aad98da (topic) edit topic branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

到:
* 2154097 (HEAD -> master, hotfix) fix a bug on master branch
* c238f33 edit master branch--1
| * aad98da (topic) edit topic branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(8)git diff HEAD aad98da //表示把HEAD变为aad98da需要减去一行...,加上一行...
diff --git a/README.md b/README.md  //a/README.md表示HEAD,b/README.md表示aad98da
index 208e24a..9b7f600 100644
--- a/README.md   //-表示a/README.md,即HEAD
+++ b/README.md    //+表示b/README.md,即aad98da
@@ -1,3 +1,3 @@   //-即a/README.md,HEAD的1到3行为#test;   just a test ;和-edit master branch 1. with hotfix
 # test           //+即a/README.md,aad98da的1到3行为 ...   ...         和+edit topic branch   1.
 just a test
-edit master branch 1. with hotfix
+edit topic branch   1.

(9)git merge topic      //没有conflict的文件会自动merge,如topic 分支中新加的topic1文件,有冲突的文件要手动解决conflict
Auto-merging README.md   //自动合并README.md
CONFLICT (content): Merge conflict in README.md  //该文件有conflict了
Automatic merge failed; fix conflicts and then commit the result.
打开README.md解决conflict:

# test
just a test
<<<<<<< HEAD   //HEAD，即当前分支上的文件为：
edit master branch 1. with hotfix
=======       //下面为要合并的分支上的文件为:
edit topic branch   1.
>>>>>>> topic

合并之前为:
* 7303cbb (topic) commit topic1  //topic分支
* aad98da edit topic branch--1
| * 2154097 (HEAD -> master) fix a bug on master branch  //master分支
| * c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit
合并之后为:
*   c2f8689 (HEAD -> master) merge branch topic with file topic1  //在master分支上合并topic分支
|\
| * 7303cbb (topic) commit topic1
| * aad98da edit topic branch--1
* | 2154097 fix a bug on master branch
* | c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit
删除原来的topic分支(分支只是一个指针，指向某个commitid)：
*   c2f8689 (HEAD -> master) merge branch topic with file topic1
|\
| * 7303cbb commit topic1
| * aad98da edit topic branch--1
* | 2154097 fix a bug on master branch
* | c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(10)当前有几个分支，每一个分支指向哪个commit，commitid "8e11cbe"属于哪个分支
* 9b14b5b (HEAD -> develop) add a line develop 2 to topic1
* 8e11cbe add a line develop1 to file topic1
*   c2f8689 (master) merge branch topic with file topic1
|\
| * 7303cbb commit topic1
| * aad98da edit topic branch--1
* | 2154097 fix a bug on master branch
* | c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(11)有多少个分支？每个分支指向哪个commit？当前分支是？
* 9fc719b (HEAD -> experiment) add a line experiment3 to file experiment
* 154f225 add a line experiment1 to file experiment
* 87cfb87 touch file experiment and add a line experiment1 to it
* 9b14b5b (develop) add a line develop 2 to topic1
* 8e11cbe add a line develop1 to file topic1
*   c2f8689 (master) merge branch topic with file topic1
|\
| * 7303cbb commit topic1
| * aad98da edit topic branch--1
* | 2154097 fix a bug on master branch
* | c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit
1)git checkout develop; git cherry-pick 9b14b5b..154f225
* bebeef9 (HEAD -> develop) add a line experiment1 to file experiment
* 9b7adde touch file experiment and add a line experiment1 to it //cherry-pick了两个commit,作为develop分支的一个新的commit
| * 9fc719b (experiment) add a line experiment3 to file experiment
| * 154f225 add a line experiment1 to file experiment
| * 87cfb87 touch file experiment and add a line experiment1 to it
|/
* 9b14b5b add a line develop 2 to topic1
* 8e11cbe add a line develop1 to file topic1
*   c2f8689 (master) merge branch topic with file topic1
|\
| * 7303cbb commit topic1
| * aad98da edit topic branch--1
* | 2154097 fix a bug on master branch
* | c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(12)合并分支一个commitid,若有冲突解决conflict后提交又是一个commitid
*   b73bea1 (HEAD -> master) Merge branch 'develop'
|\
| * bebeef9 (develop) add a line experiment1 to file experiment
| * 9b7adde touch file experiment and add a line experiment1 to it
* | e5a9a85 add a line develop 2 to topic1
* | 32eaadb add a line develop1 to file topic1
| | * 9fc719b (experiment) add a line experiment3 to file experiment
| | * 154f225 add a line experiment1 to file experiment
| | * 87cfb87 touch file experiment and add a line experiment1 to it
| |/
| * 9b14b5b add a line develop 2 to topic1
| * 8e11cbe add a line develop1 to file topic1
|/
*   c2f8689 merge branch topic with file topic1
|\
| * 7303cbb commit topic1
| * aad98da edit topic branch--1
* | 2154097 fix a bug on master branch
* | c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit
合并手动解决冲突：
*   863208f (HEAD -> master) settle merging conflict
|\
| * 9fc719b (experiment) add a line experiment3 to file experiment
| * 154f225 add a line experiment1 to file experiment
| * 87cfb87 touch file experiment and add a line experiment1 to it
* |   b73bea1 Merge branch 'develop'
|\ \
| * | bebeef9 (develop) add a line experiment1 to file experiment
| * | 9b7adde touch file experiment and add a line experiment1 to it
| |/
| * 9b14b5b add a line develop 2 to topic1
| * 8e11cbe add a line develop1 to file topic1
* | e5a9a85 add a line develop 2 to topic1
* | 32eaadb add a line develop1 to file topic1
|/
*   c2f8689 merge branch topic with file topic1
|\
| * 7303cbb commit topic1
| * aad98da edit topic branch--1
* | 2154097 fix a bug on master branch
* | c238f33 edit master branch--1
|/
* 7ea67db (origin/master, origin/HEAD) Initial commit

(13)git branch -vv
  iss53     7e424c3 [origin/iss53: ahead 2] forgot the brackets 
  master    1ae2a45 [origin/master] deploying index fix
* serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] this should do it
  testing   5ea463a trying something new
这里可以看到 iss53 分支正在跟踪 origin/iss53 并且 “ahead” 是 2，意味着本地有两个提交还没有推送到服务器上。 也能看到 master 分支正在跟踪 origin/master 分支并且是最新的。 接下来可以看到 serverfix 分支正在跟踪 teamone 服务器上的 server-fix-good 分支并且领先 3 落后 1，意味着服务器上有一次提交还没有合并入同时本地有三次提交还没有推送。 最后看到 testing 分支并没有跟踪任何远程分支。


