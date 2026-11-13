[TOC]
## git历史

![43887398.png](Github高级命令详解与实战下_files/43887398.png)
下图中两个相邻的提交没有任何关系(只不过他们的提交顺序比较相近),上一讲里面也讲的下面的提交不一定是上面的父亲!!!
优先按照父子关系排列,但有时候(使用merge的时候)也会按照时间顺序排列!!
![43962135.png](Github高级命令详解与实战下_files/43962135.png)
![44142089.png](Github高级命令详解与实战下_files/44142089.png)
名字,邮箱,提交时间都是不可信任的;
提交是可以捏造的!!!
![44281535.png](Github高级命令详解与实战下_files/44281535.png)
多线历史:
![44658519.png](Github高级命令详解与实战下_files/44658519.png)
## checkout实战与工作区,缓存区
[https://github.com/richard1230/advanced-git](https://github.com/richard1230/advanced-git)
需求:
现在5.0有一个bug,现在想要发布一个5.1版本;
![45961859.png](Github高级命令详解与实战下_files/45961859.png)

### checkout相关知识点与实战
![46130805.png](Github高级命令详解与实战下_files/46130805.png)

```
##
$git checkout v6.0
Note: checking out 'v6.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at d3c84fe Version 6.0
##
$git checkout -b release-6x
Switched to a new branch 'release-6x'
$git status
On branch release-6x
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified: Product.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/

no changes added to commit (use "git add" and/or "git commit -a")

```
 release-6x是刚刚创建的一个分支;
![46633730.png](Github高级命令详解与实战下_files/46633730.png)
修完bug之后:
```
$git add Product.java
$git commit -m "fix a bug for 6.0"
[release-6x 15bdd40] fix a bug for 6.0
 1 file changed, 1 deletion(-)

```
![46854030.png](Github高级命令详解与实战下_files/46854030.png)

### checkout 基本命令:
```
• git checkout v1.0.0
• git checkout fd56bd
• git checkout master
•git checkout origin/master
```
### checkout的命令扩展:(四种用法)
```
git checkout -b new-branch commitid/tag/another-branch/HEAD(HEAD可以省略,就是基于当前分支创建一个新分支)
```
checkout高阶命令:(在工作目录和暂存区移动文件)


 空目录git无法识别:
![47445187.png](Github高级命令详解与实战下_files/47445187.png)
增加文件之后识别出来了:
![47577214.png](Github高级命令详解与实战下_files/47577214.png)
下面出问题了:
![47817646.png](Github高级命令详解与实战下_files/47817646.png)
tmp.txt是不想提交的,但是这是手滑把它给add了!
先讲几个概念:
```
$touch it_is_nothing_todo_with_current_respository.txt
$git status
On branch release-6x
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file: .gitignore
        modified: Product.java
        new file: a/1.txt
        new file: a/tml.txt
        new file: a/tmp.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        it_is_nothing_todo_with_current_respository.txt

```
![48196966.png](Github高级命令详解与实战下_files/48196966.png)
stage:舞台--->在舞台上排列======>预发布环境
### 工作区,暂存区与版本库(git checkout 高级用法)
[https://www.cnblogs.com/qdhxhz/p/9757390.html](https://www.cnblogs.com/qdhxhz/p/9757390.html)
Workspace： 工作区，就是你平时存放项目代码的地方
`git add xxx`之后,xxx就会被转移到暂存区!
Index / Stage： 暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息;
缓存区又称为stage!!!
`git commit -m "yyy"`,提交的只是暂存区里面的文件!
Repository:仓库区（或版本库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
Remote:远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换
![54861399.png](Github高级命令详解与实战下_files/54861399.png)

对tmp.txt再次修改一下:
![55085217.png](Github高级命令详解与实战下_files/55085217.png)
注意里面的提示:如果想要放弃刚刚在tmp.txt里面的修改,那么请使用
`$git checkout -- a/tmp.txt`
```
$git checkout -- filename
```
![55045217.png](Github高级命令详解与实战下_files/55045217.png)

![55338545.png](Github高级命令详解与实战下_files/55338545.png)
下面再次手滑,我不想把txt文件加入到stage,怎么办呢?
![56082955.png](Github高级命令详解与实战下_files/56082955.png)
```

$git add .
$git status
On branch release-6x
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file: .gitignore
        modified: Product.java
        new file: a/1.java
        new file: a/1.txt
        new file: a/tml.txt
        new file: a/tmp.txt
        new file: it_is_nothing_todo_with_current_respository.txt
##注意这里一定要有一对引号
$git reset HEAD "*.txt"
$git status
On branch release-6x
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file: .gitignore
        modified: Product.java
        new file: a/1.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        a/1.txt
        a/tml.txt
        a/tmp.txt
        it_is_nothing_todo_with_current_respository.txt

```
再看一个`git checkout --`的例子
![58526316.png](Github高级命令详解与实战下_files/58526316.png)
![58597335.png](Github高级命令详解与实战下_files/58597335.png)


### 总结:
一定要看说明!!!git会提示你的;
![56312806.png](Github高级命令详解与实战下_files/56312806.png)
## git reset详解
强行将当前分⽀支HEAD指针移动到指定状态(这个状态指的就是上一节提到的能识别仓库的4个东西--->"bcth")
reset常见用法:
```
git reset HEAD --hard (grhh)
git reset origin/master
git reset 3da2dfe
git reset HEAD~3
git reset tag
```
![60267868.png](Github高级命令详解与实战下_files/60267868.png)
目前master在v10.0
下面想把它强行重置为v5.0
![60396764.png](Github高级命令详解与实战下_files/60396764.png)

![60434474.png](Github高级命令详解与实战下_files/60434474.png)

![60532714.png](Github高级命令详解与实战下_files/60532714.png)

注意:此时这两个版本之间的文件变更还留着!!!并且默认是以mixed的方式存在的!!
![60715642.png](Github高级命令详解与实战下_files/60715642.png)

![60737725.png](Github高级命令详解与实战下_files/60737725.png)

此时可以把v5.0和v10.0之间的多次提交捏合成一个提交;如下所示:
![61051162.png](Github高级命令详解与实战下_files/61051162.png)
![61078894.png](Github高级命令详解与实战下_files/61078894.png)
注意此时master和origin/master分叉了:(可以push的唯一条件是远程分支是本地分支的祖先,而此时不满足这个条件)
如果强行使用`git push --force`,本地分支会把远程分支覆盖,此时远程分支的6个提交会消失了!
![61117878.png](Github高级命令详解与实战下_files/61117878.png)

现在有点后悔上面的操作了,原来本地分支和远程分支是齐头并进的!
![61355340.png](Github高级命令详解与实战下_files/61355340.png)
怎么反悔呢?即:怎么将master和origin/master 再次齐头并进？
注意:此时是在master分支上面的!!!
![61503271.png](Github高级命令详解与实战下_files/61503271.png)
![61613177.png](Github高级命令详解与实战下_files/61613177.png)
由此可见,reset命令可以随心所欲地移动指针！
即:` git reset branch`表示的是将当前分支的指针移动到branch!!!
`git reset HEAD~3`将当前指针回退3步!(即:回退了3个commit)

### --hard参数
![62128699.png](Github高级命令详解与实战下_files/62128699.png)
代表的是直接将当前指针强行回退到指定的状态！同时清空当前状态和指定状态之间存在的若干个提交(注意:mixed是保存的)
### mixed与soft区别
先修改`production.java`:
![63761885.png](Github高级命令详解与实战下_files/63761885.png)
 而后将上面这个修改进入暂存区:
![63867260.png](Github高级命令详解与实战下_files/63867260.png)
再次修改:
![63910362.png](Github高级命令详解与实战下_files/63910362.png)
到目前为止有两个变更:(一个变更留在工作区,一个变更进入舞台)
![63949014.png](Github高级命令详解与实战下_files/63949014.png)
下面使用mixed命令:
![64036014.png](Github高级命令详解与实战下_files/64036014.png)
mixed是把所有的没有commit的文件修改全部合并起来捏到一起; 放到工作区!
即:如果使用--mixed，就将头恢复掉，已经add的缓存也会丢失掉，工作空间的代码什么的是不变的!!!
使用--soft就仅仅将头指针恢复，已经add的缓存以及工作空间的所有东西都不变。
重复上面的过程:
![64529684.png](Github高级命令详解与实战下_files/64529684.png)
 可以发现soft仅仅只是回退了一个指针,其他的没变!
![64591618.png](Github高级命令详解与实战下_files/64591618.png)

一般工作的时候只用到mixed(默认)和hard;
### soft,hard,mixed区别小结
[https://www.cnblogs.com/kidsitcn/p/4513297.html](https://www.cnblogs.com/kidsitcn/p/4513297.html)
[https://www.jianshu.com/p/c6927e80a01d](https://www.jianshu.com/p/c6927e80a01d)
git reset 命令可以将当前的HEAD重置到特定的状态。
首先要搞清楚下面几个概念

HEAD: HEAD就是指向当前分支当前版本的指针
Index: Index即为暂存区，当你修改了你的git仓库里的一个文件时，这些变化一开始是unstaged状态，为了提交这些修改，你需要使用git add把它加入到index，使它成为staged状态。当你提交一个commit时，index里面的修改被提交。
working tree: 即当前的工作目录。
`git reset` 的用法
`git reset [<mode>] [<commit>]`或者`git reset [<commit>]  [<mode>] `

`git reset` 将当前分支的HEAD指向给定的版本，并根据模式的不同决定是否修改`index`和`working tree`。
常用的有三种模式，--soft, --mixed, --hard，如果没有给出<mode>则默认是`--mixed`
1.soft:
![65896368.png](Github高级命令详解与实战下_files/65896368.png)
即:使用soft参数的话,下一步直接git commit即可!
2.mixed:
即:使用mixed参数(默认)的话,下一步还要加git add xxx===>而后git commit才可可!
![65973588.png](Github高级命令详解与实战下_files/65973588.png)
3.hard:
使用--hard同时也会修改working tree，也就是当前的工作目录，如果我们执行`git reset --hard HEAD~`，那么最后一次提交的修改，包括本地文件的修改都会被清除，彻底还原到上一次提交的状态且无法找回。所以在执行`reset --hard`之前一定要小心,下面要继续的话,必须先改源代码,而后`Git add`===>`git commit`
## git cherry-pick
使用场合:
把弄错分支的提交移动到正确的地方
把其他分支的提交新增到现在的分支

![66442499.png](Github高级命令详解与实战下_files/66442499.png)

修了一个bug:
![66762710.png](Github高级命令详解与实战下_files/66762710.png)
此时master修的这个bug和7系列的分支以及9系列的分支没有半毛钱关系;
 但是现在想让7系列的分支以及9系列的分支也能享受到修bug的成果,怎么做呢??
![66913676.png](Github高级命令详解与实战下_files/66913676.png)
![a04e8034-77ec-4a60-a23e-80c2c52d2562.png](Github高级命令详解与实战下_files/a04e8034-77ec-4a60-a23e-80c2c52d2562.png)
其实这里commitid可能搞错了,但是不影响吧,逻辑是相通的;
cherry-pick只会产生一个commit!
![68444152.png](Github高级命令详解与实战下_files/68444152.png)
出现冲突,那么就按照git提示来修改:

![68494742.png](Github高级命令详解与实战下_files/68494742.png)
![68512186.png](Github高级命令详解与实战下_files/68512186.png)
而后继续:
![68581064.png](Github高级命令详解与实战下_files/68581064.png)
![68680970.png](Github高级命令详解与实战下_files/68680970.png)
虽然内容commit的内容一样,但是这两个commit不是同一个对象!
![68787497.png](Github高级命令详解与实战下_files/68787497.png)

### git cherry-pick 多个:
git cherry-pick 多个:
[https://blog.csdn.net/w958796636/article/details/78492017](https://blog.csdn.net/w958796636/article/details/78492017)
```
git cherry-pick ba51861..023sb6f299849a1f
注意中间的两个点，表示把两个commit区间的所有commit都复制过去

```
## git revert(反向提交:即撤销)
  git revert commitid :将commit里面所做的操作进行反操作!
![69703417.png](Github高级命令详解与实战下_files/69703417.png)
## git bisect(重点)
bi:二;
sect:分区;
bisect:二分;
找bug的时候经常用到这个命令;
利用二分查找的思想找bug:(查找commit)
 
![70066510.png](Github高级命令详解与实战下_files/70066510.png)


举个例子:(很多人利用这种方法定位到bug)
![70285366.png](Github高级命令详解与实战下_files/70285366.png)


### 常见bisect命令
```
git bisect start/reset
git bisect good/bad/skip(这个命令也很重要!!!)
git bisect run
#注意:  git bisect skip 这个命令:
当你在查找的时候,某一个commit无法进行测试其是好的还是坏的时候,就用git bisect skip
```
![78622405.png](Github高级命令详解与实战下_files/78622405.png)
告诉git一个好的版本,再告诉它一个坏的版本,它会自动帮我们定位到中间那个版本:
![76037071.png](Github高级命令详解与实战下_files/76037071.png)
### bisect实战
```
##
$git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file: .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        a/
        it_is_nothing_todo_with_current_respository.txt

$ls
Product.java a test.txt
README.md it_is_nothing_todo_with_current_respository.txt
$javac Product.java
$ls
Product.class README.md it_is_nothing_todo_with_current_respository.txt
Product.java    
## 发现bug                  
$java Product
I'm version 10.0!
I have a bug!
A bad feature!
## 告诉git这是一个坏的bug
$git bisect bad
You need to start by "git bisect start"
Do you want me to do it for you [Y/n]? Y
## 跳转到一个好的版本
$git checkout v1.0
A .gitignore
Note: checking out 'v1.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 37dfaa7 Version 1.0
$javac Product.java
$java Product
I'm version 1.0!
## 告诉git这是一个好的版本
$git bisect good
Bisecting: 5 revisions left to test after this (roughly 3 steps)
[0e12342d81bffee591623c13a3bfa83d7aeb5ec0] Version 7.0


```
整个查找流程:
```
##
$git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class

nothing added to commit but untracked files present (use "git add" to track)
##
$javac Product.java && java Product
I'm version 10.0!
I have a bug!
A bad feature!
##
$git bisect bad
You need to start by "git bisect start"
##
Do you want me to do it for you [Y/n]? y 
## 想到一个没有bug的版本
$git checkout v1.0
Note: checking out 'v1.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 37dfaa7 Version 1.0
##
$javac Product.java && java Product
I'm version 1.0!
##
$git bisect good
Bisecting: 5 revisions left to test after this (roughly 3 steps)
[0e12342d81bffee591623c13a3bfa83d7aeb5ec0] Version 7.0
##
$git status
HEAD detached at 0e12342
You are currently bisecting, started from branch 'master'.
  (use "git bisect reset" to get back to the original branch)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class

nothing added to commit but untracked files present (use "git add" to track)
##
$javac Product.java && java Product
I'm version 7.0!
I have a bug!
##
$git bisect bad
Bisecting: 2 revisions left to test after this (roughly 2 steps)
## 其实这里是自动切换的
[23997e502671c7b6220115ed2ed6fe72be33eeff] Version 4.0
$git status
HEAD detached at 23997e5
You are currently bisecting, started from branch 'master'.
  (use "git bisect reset" to get back to the original branch)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class

nothing added to commit but untracked files present (use "git add" to track)
##
$javac Product.java && java Product
I'm version 4.0!
##
$git bisect good
Bisecting: 0 revisions left to test after this (roughly 1 step)
[d3c84fe32615597c06b2fa2f2e2768f6ca979195] Version 6.0
##
$javac Product.java && java Product
I'm version 6.0!
I have a bug!
##
$git bisect bad
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[5c4ef2305d8180405039c91ff2d363a3529b5628] Version 5.0
##
$git status
HEAD detached at 5c4ef23
You are currently bisecting, started from branch 'master'.
  (use "git bisect reset" to get back to the original branch)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class

nothing added to commit but untracked files present (use "git add" to track)
##
$javac Product.java && java Product
I'm version 5.0!
I have a bug!
##
$git bisect bad
5c4ef2305d8180405039c91ff2d363a3529b5628 is the first bad commit
commit 5c4ef2305d8180405039c91ff2d363a3529b5628
Author: Bo Zhang <zhangbodut@gmail.com>
Date: Fri Oct 18 19:45:02 2019 +0800

    Version 5.0

:100644 100644 bd1213f49dca1c0ccbf200d2bdc740435813b243 774a7d95d65e388f5ed780f4967b66913cf10056 M Product.java
$

```
![78226196.png](Github高级命令详解与实战下_files/78226196.png)
注意:如果中途哪一步手滑了,可以输入如下命令:
`git bisect reset`
![78062503.png](Github高级命令详解与实战下_files/78062503.png)
下面写一个脚本将上面这个过程实现自动化:
![79115094.png](Github高级命令详解与实战下_files/79115094.png)

注意空格:
![79209369.png](Github高级命令详解与实战下_files/79209369.png)
### 自动化查找过程:(前面一好一坏是手工的)
```
$git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class
        run.sh

nothing added to commit but untracked files present (use "git add" to track)
#
$git bisect bad
You need to start by "git bisect start"
Do you want me to do it for you [Y/n]? y
$git checkout v1.0
Note: checking out 'v1.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 37dfaa7 Version 1.0
##
$git bisect good
Bisecting: 5 revisions left to test after this (roughly 3 steps)
[0e12342d81bffee591623c13a3bfa83d7aeb5ec0] Version 7.0
## 自动化
$git bisect run ./run.sh
running ./run.sh
bad!
Bisecting: 2 revisions left to test after this (roughly 2 steps)
[23997e502671c7b6220115ed2ed6fe72be33eeff] Version 4.0
running ./run.sh
good!
Bisecting: 0 revisions left to test after this (roughly 1 step)
[d3c84fe32615597c06b2fa2f2e2768f6ca979195] Version 6.0
running ./run.sh
bad!
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[5c4ef2305d8180405039c91ff2d363a3529b5628] Version 5.0
running ./run.sh
bad!
5c4ef2305d8180405039c91ff2d363a3529b5628 is the first bad commit
commit 5c4ef2305d8180405039c91ff2d363a3529b5628
Author: Bo Zhang <zhangbodut@gmail.com>
Date: Fri Oct 18 19:45:02 2019 +0800

    Version 5.0

:100644 100644 bd1213f49dca1c0ccbf200d2bdc740435813b243 774a7d95d65e388f5ed780f4967b66913cf10056 M Product.java
bisect run success

```
### Git bisect在真是项目中的实战
见另外一个讲义

## Git stash
git stash(储藏)
![38735737.png](Github高级命令详解与实战下_files/38735737.png)

![38824964.png](Github高级命令详解与实战下_files/38824964.png)
工作正在进行,突然来了个线上bug!!!怎么办===>用git stash

![38959671.png](Github高级命令详解与实战下_files/38959671.png)

![39053071.png](Github高级命令详解与实战下_files/39053071.png)

![39070516.png](Github高级命令详解与实战下_files/39070516.png)

![39091371.png](Github高级命令详解与实战下_files/39091371.png)

![39112704.png](Github高级命令详解与实战下_files/39112704.png)

![39127941.png](Github高级命令详解与实战下_files/39127941.png)
一般流程:
```
$touch a.java
$touch b.java
$touch c.java
$git add *.java
$git status
On branch master
Your branch is up to date with 'origin/master'.

You are currently bisecting, started from branch 'master'.
  (use "git bisect reset" to get back to the original branch)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file: a.java
        new file: b.java
        new file: c.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class
        run.sh
##存储
$git stash
Saved working directory and index state WIP on master: f39147f Update README.md
##切换去修bug
$git checkout -b fix-bug
Switched to a new branch 'fix-bug'
##修好了返回
$git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
##
$git status
On branch master
Your branch is up to date with 'origin/master'.

You are currently bisecting, started from branch 'master'.
  (use "git bisect reset" to get back to the original branch)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class
        run.sh

nothing added to commit but untracked files present (use "git add" to track)
## 之前存储的拿出来
$git stash pop
On branch master
Your branch is up to date with 'origin/master'.

You are currently bisecting, started from branch 'master'.
  (use "git bisect reset" to get back to the original branch)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file: a.java
        new file: b.java
        new file: c.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class
        run.sh

Dropped refs/stash@{0} (2ace36aa57f01b3934b584cc0466b93b597df98e)
## 有多个紧急任务的时候
$git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
$vi Product.java
$git stash
Saved working directory and index state WIP on master: f39147f Update README.md
$git checkout fixbug2
Switched to branch 'fixbug2'
## 查看存储的列表
$git stash list
stash@{0}: WIP on master: f39147f Update README.md
stash@{1}: WIP on master: f39147f Update README.md
## 返回对应的存储的地方
$git stash apply stash@{0}
On branch fixbug2
You are currently bisecting, started from branch 'master'.
  (use "git bisect reset" to get back to the original branch)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified: Product.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        Product.class
        run.sh



```
## git 工作流
![66384506.png](Github高级命令详解与实战下_files/66384506.png)
## 自行搭建git服务器
![67512952.png](Github高级命令详解与实战下_files/67512952.png)

![67838006.png](Github高级命令详解与实战下_files/67838006.png)

![67854100.png](Github高级命令详解与实战下_files/67854100.png)


### 流程
[https://ecs.console.aliyun.com/?spm=5176.12818093.recommends.decs.488716d0vraTHT#/server/region/cn-shanghai](https://ecs.console.aliyun.com/?spm=5176.12818093.recommends.decs.488716d0vraTHT#/server/region/cn-shanghai)
创建一个实例
![78302702.png](Github高级命令详解与实战下_files/78302702.png)
![78405693.png](Github高级命令详解与实战下_files/78405693.png)



![78466942.png](Github高级命令详解与实战下_files/78466942.png)



![78669282.png](Github高级命令详解与实战下_files/78669282.png)




![78819245.png](Github高级命令详解与实战下_files/78819245.png)
下次再用就用现成的了:
![78881232.png](Github高级命令详解与实战下_files/78881232.png)

![78998433.png](Github高级命令详解与实战下_files/78998433.png)


![79067424.png](Github高级命令详解与实战下_files/79067424.png)



![79114625.png](Github高级命令详解与实战下_files/79114625.png)


![79351135.png](Github高级命令详解与实战下_files/79351135.png)


用户名:root
密码: 7TvL3AT*7Jap4YV

![79785639.png](Github高级命令详解与实战下_files/79785639.png)
注意:日常在服务器里面不要用root用户!!!
```
##安装docker:
apt-get update && apt-get install docker.io
##创建git用户:
root@iZuf65xna3is11pcie9ge4Z:~# adduser git
Adding user `git' ...
Adding new group `git' (1000) ...
Adding new user `git' (1000) with group `git' ...
Creating home directory `/home/git' ...
Copying files from `/etc/skel' ...
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
Changing the user information for git
Enter the new value, or press ENTER for the default
        Full Name []: git
        Room Number []: git
        Work Phone []: git
        Home Phone []: git
        Other []:                 //默认回车
Is the information correct? [Y/n] y
##切换到git用户
root@iZuf65xna3is11pcie9ge4Z:~# su git
git@iZuf65xna3is11pcie9ge4Z:/root$ 
## 切换回root用户将剩下的命令执行完
git@iZuf65xna3is11pcie9ge4Z:/root$ exit
exit
root@iZuf65xna3is11pcie9ge4Z:~# usermod -aG docker git
root@iZuf65xna3is11pcie9ge4Z:~# mkdir -p /app/gogs
root@iZuf65xna3is11pcie9ge4Z:~# chown git:git /app/gogs
root@iZuf65xna3is11pcie9ge4Z:~# 
## root用户的使命完成,切换回Git用户
root@iZuf65xna3is11pcie9ge4Z:~# su git
git@iZuf65xna3is11pcie9ge4Z:/root$ mkdir -p ~/gogs/git/.ssh
git@iZuf65xna3is11pcie9ge4Z:/root$ ln -s ~/gogs/git/.ssh ~/.ssh
git@iZuf65xna3is11pcie9ge4Z:/root$ ssh-keygen -t rsa -P ''
Generating public/private rsa key pair.
Enter file in which to save the key (/home/git/.ssh/id_rsa): 
Your identification has been saved in /home/git/.ssh/id_rsa.
Your public key has been saved in /home/git/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:k9PK/PP8KdH5mbXmCQ7jvHGl0CxONWGSJaeteulr6/k git@iZuf65xna3is11pcie9ge4Z
The key's randomart image is:
+---[RSA 2048]----+
| oo= |
| .B . |
| . + |
| o = . |
| S .= + o |
| o ++ = = .|
| +. B = .=|
| .*oO .*o|
| +%BE=o |
+----[SHA256]-----+
git@iZuf65xna3is11pcie9ge4Z:/root$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
git@iZuf65xna3is11pcie9ge4Z:/root$ chmod 700 ~/.ssh && chmod 600 ~/.ssh/*
##下面这个命令行的意思是cat将一个文件内容(就是下面的脚本)输出到一个文件中,以end为结尾
git@iZuf65xna3is11pcie9ge4Z:/root$ cat >/app/gogs/gogs <<'END' 
> #!/bin/sh
> ssh -p 10022 -o StrictHostKeyChecking=no git@127.0.0.1 \
> "SSH_ORIGINAL_COMMAND=\"$SSH_ORIGINAL_COMMAND\" $0 $@"
> END
git@iZuf65xna3is11pcie9ge4Z:/root$ 
git@iZuf65xna3is11pcie9ge4Z:/root$ chmod 755 /app/gogs/gogs
```
## 总的命令行总结:
```
##as root
##安装docker:
apt-get update && apt-get install [docker.io](http://docker.io/)
##创建git用户:
adduser git
##使git⽤用户可以运⾏行行docker:
usermod -aG docker git
##创建gogs运行⽬录
mkdir -p /app/gogs
##改变目录的所有⼈
chown git:git /app/gogs
## as git user
##创建SSH⽬录:
mkdir -p ~/gogs/git/.ssh
ln -s ~/gogs/git/.ssh ~/.ssh
##生成SSH key:
ssh-keygen -t rsa -P ''
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
更严格的权限:(.ssh这个目录只有自己能访问,目录里面的东西也是只有自己能访问)
chmod 700 ~/.ssh && chmod 600 ~/.ssh/*
#注意:下面这个shell脚本的作用:将外界转发给阿里云服务器的22端口的请求转发给docker的git服务器里面
cat >/app/gogs/gogs <<'END' 
#!/bin/sh
ssh -p 10022 -o StrictHostKeyChecking=no git@[127.0.0.1](file:///var/folders/rn/r6_l2xln77j0bv69j2c_5rg00000gp/T/WizNote/87f39b2b-669e-49ba-ad2e-d17f268b9fc4/index.html) \
"SSH_ORIGINAL_COMMAND=\"$SSH_ORIGINAL_COMMAND\" $0 $@"
END


##给与脚本执行的权限
chmod 755 /app/gogs/gogs
## 启动docker
git@iZuf65xna3is11pcie9ge4Z:~/.ssh$ docker run -v ~git/gogs:/data -p 127.0.0.1:10022:22 -p 3000:3000 gogs/gogs
```
设置安全组:
![82525536.png](Github高级命令详解与实战下_files/82525536.png)
服务器启动:
![82772711.png](Github高级命令详解与实战下_files/82772711.png)


下面运行`/app/gogs/gogs`这个脚本:
看到 git service字样说明成功了;
![83875382.png](Github高级命令详解与实战下_files/83875382.png)
```
git@iZuf65xna3is11pcie9ge4Z:/root$ docker ps -a
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
2ccbb733ae0b gogs/gogs "/app/gogs/docker/st…" 26 minutes ago Exited (0) 22 minutes ago suspicious_hofstadter
e6a359c6f64f gogs/gogs "/app/gogs/docker/st…" 32 minutes ago Up 9 minutes 0.0.0.0:3000->3000/tcp, 127.0.0.1:10022->22/tcp laughing_tharp
git@iZuf65xna3is11pcie9ge4Z:/root$ docker ps
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
e6a359c6f64f gogs/gogs "/app/gogs/docker/st…" 32 minutes ago Up 10 minutes 0.0.0.0:3000->3000/tcp, 127.0.0.1:10022->22/tcp laughing_tharp
git@iZuf65xna3is11pcie9ge4Z:/root$ ls -alh ~git/gogs
total 20K
drwxr-xr-x 5 git git 4.0K May 28 22:50 .
drwxr-xr-x 3 git git 4.0K May 28 22:23 ..
drwxr-xr-x 3 git git 4.0K May 28 22:23 git
drwxr-xr-x 5 git git 4.0K May 28 22:50 gogs
drwx------ 2 git git 4.0K May 28 22:50 ssh
git@iZuf65xna3is11pcie9ge4Z:/root$ docker start e6a3
e6a3
git@iZuf65xna3is11pcie9ge4Z:/root$ /app/gogs/gogs
Warning: Permanently added '[127.0.0.1]:10022' (ECDSA) to the list of known hosts.
NAME:
   Gogs - A painless self-hosted Git service

USAGE:
   gogs [global options] command [command options] [arguments...]

VERSION:
   0.12.0+dev

COMMANDS:
   web Start web server
   serv This command should only be called by SSH shell
   hook Delegate commands to corresponding Git hooks
   cert Generate self-signed certificate
   admin Perform admin operations on command line
   import Import portable data as local Gogs data
   backup Backup files and database
   restore Restore files and database from backup
   help, h Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h show help
   --version, -v print the version
```
SQLite不需要启一个额外的服务器:
![84053682.png](Github高级命令详解与实战下_files/84053682.png)


![84104553.png](Github高级命令详解与实战下_files/84104553.png)

报了个错:
![84149924.png](Github高级命令详解与实战下_files/84149924.png)


![84537899.png](Github高级命令详解与实战下_files/84537899.png)

![84669165.png](Github高级命令详解与实战下_files/84669165.png)
![84727274.png](Github高级命令详解与实战下_files/84727274.png)
![84764596.png](Github高级命令详解与实战下_files/84764596.png)


  

![84791854.png](Github高级命令详解与实战下_files/84791854.png)

![84866623.png](Github高级命令详解与实战下_files/84866623.png)]]


![84914788.png](Github高级命令详解与实战下_files/84914788.png)

![85057512.png](Github高级命令详解与实战下_files/85057512.png)




![85074897.png](Github高级命令详解与实战下_files/85074897.png)


![85143826.png](Github高级命令详解与实战下_files/85143826.png)


![85185533.png](Github高级命令详解与实战下_files/85185533.png)


![85212282.png](Github高级命令详解与实战下_files/85212282.png)



![85234072.png](Github高级命令详解与实战下_files/85234072.png)

下面的命令是保证git服务器持续运行的:
```
docker run -d --restart=always-v ~git/gogs:/data -p 127.0.0.1:10022:22 -p 3000:3000 gogs/gogs
```
![85320471.png](Github高级命令详解与实战下_files/85320471.png)