[TOC]
## 前言(主要内容)大纲
![65896155.png](github高级命令详解与实战_files/65896155.png)

# 仓库/提交/分支的本质
## 查看是谁修改的以及提交记录
可以查看是谁修改的以及修改了什么,还有提交记录统统都可以查到
![66494836.png](github高级命令详解与实战_files/66494836.png)
双击某个时间戳即可;
![66465269.png](github高级命令详解与实战_files/66465269.png)

## 仓库的本质
* 一个所有的历史都可追溯的文件夹
 * 历史的最⼩单位是仓库在某个时刻的状态(快照)
 * 通常用SHA-1表示
* 哪些东西可以标识仓库的某个状态？(这下面四个东西极其重要)
 * commit对象的SHA-1(无需写全)
 * 分支(branch)
 * HEAD
 * 标签(tag)

### 想要穿梭到历史的某个状态
```
#
$git log
commit 969016aa5039038b5f6245f0ef89f9fc66aa0e95 (HEAD -> master, origin/master, origin/HEAD)
Author: Bo Zhang <zhangbodut@gmail.com>
Date: Sun Apr 26 13:34:46 2020 +0800

    Only test Linux

commit fc148e17d846661b1fb5aa84425fac47cdd19016
Author: Bo Zhang <zhangbodut@gmail.com>
Date: Sun Apr 26 11:45:10 2020 +0800

    Remove debug output

commit 1f9b88ee38b8b38d215fb0a06950622395cc41b4
Author: Bo Zhang <zhangbodut@gmail.com>
Date: Sun Apr 26 11:14:35 2020 +0800

    Update README.md

commit 3750dd43bec84d1ffd1adaef42a8c6d7965884ea
#
$ git checkout commitid
```
在github上面只需要
`https://github.com/xxx/yyy/tree/committid`


![67194798.png](github高级命令详解与实战_files/67194798.png)

Head指的是当前分支的指针;
### commit的一些理解
![79005242.png](github高级命令详解与实战_files/79005242.png)
`git checkout commit1id`之后;仓库将处于t2时刻的状态!
举个例子来说明:
原来处于最新状态:
![33707630.png](github高级命令详解与实战_files/33707630.png)

![33602543.png](github高级命令详解与实战_files/33602543.png)

![33574573.png](github高级命令详解与实战_files/33574573.png)

![33542769.png](github高级命令详解与实战_files/33542769.png)
### 想要回到某个版本怎么办
```
$Git tag
0.9
v0.10
v0.10.2
v0.10.3
v0.11
v0.11.1
v0.11.2
v0.11.3
$git checkout v0.11.1(版本号)
```
`https://github.com/xxx/yyy/tree/v0.zz.w`


![75281897.png](github高级命令详解与实战_files/75281897.png)


## 提交的本质(commit)
* 仓库从⼀个状态转移到另外⼀个状态时发生的变化
* commit对象是不可变的
* 那git commit --amend是什么
* 持续的⼯作和提交，在仓库中建立了一棵树


author是编写代码的人(是一个贡献者),committer是提交代码到仓库的人(对仓库有写权限);
  
![76456693.png](github高级命令详解与实战_files/76456693.png)

![77235228.png](github高级命令详解与实战_files/77235228.png)
注意:下面的这个commit不一定是上面的这个commit提交的父亲,我这里举的例子碰巧罢了!
![78060580.png](github高级命令详解与实战_files/78060580.png)
![77292902.png](github高级命令详解与实战_files/77292902.png)
![78098416.png](github高级命令详解与实战_files/78098416.png)
在看一个例子:
![33973546.png](github高级命令详解与实战_files/33973546.png)

![33989932.png](github高级命令详解与实战_files/33989932.png)
![79005242.png](github高级命令详解与实战_files/79005242.png)

 

git commit --amend
![78485699.png](github高级命令详解与实战_files/78485699.png)
如何进行amend?见下面:(amend是说我不是产生一个新的提交,而是修改了最近的一个提交!!!)
![78690354.png](github高级命令详解与实战_files/78690354.png)

![79155546.png](github高级命令详解与实战_files/79155546.png)

## 分支的本质
   
![79336898.png](github高级命令详解与实战_files/79336898.png)

 新建一个分支:(但是此时什么事情都还没做,此时feature只是一个提交的指针,指向当前仓库的状态,此时master也指向这个状态 )
![79699134.png](github高级命令详解与实战_files/79699134.png)
![79802948.png](github高级命令详解与实战_files/79802948.png)

![79897669.png](github高级命令详解与实战_files/79897669.png)

继续创建一个新的分支,创建了一个文本并提交:
![79955483.png](github高级命令详解与实战_files/79955483.png)
![80143470.png](github高级命令详解与实战_files/80143470.png)
每个commit都只是仓库在某个时间点上的代码副本;
此时feature-2指向了某一个状态
  
![80104087.png](github高级命令详解与实战_files/80104087.png)
`git checkout -b -new-branch v0.5.3`以某个版本为基础创建一个新分支并切换到这个分支上面;
![80395060.png](github高级命令详解与实战_files/80395060.png)
### HEAD相关
HEAD:一个活动的指针,指代当前分支的头;
### `^`和`~`的含义(重要)
`^`和`~`的含义
![80761981.png](github高级命令详解与实战_files/80761981.png)
git是一个仓库中所有代码副本(状态)的集合;
任何一个状态,只要你可以把它表示出来,就可以找它的父亲,找它的祖先;

![81507700.png](github高级命令详解与实战_files/81507700.png)
![81716903.png](github高级命令详解与实战_files/81716903.png)
## 本地仓库,远程仓库,push和pull
![81996956.png](github高级命令详解与实战_files/81996956.png)

clone:也可以从本地clone到本地:
![83414703.png](github高级命令详解与实战_files/83414703.png)

### git push
git push能成功的原则是:本地远端仓库(即origin/master)必须是你的分支(master)的祖先!!!
![86043189.png](github高级命令详解与实战_files/86043189.png)
git push能成功的原则是:远端分支必须是你的分支的祖先!!!
即:当前本地分支一定要领先于远端分支才可push
![540614.png](github高级命令详解与实战_files/540614.png)

![86076409.png](github高级命令详解与实战_files/86076409.png)


## 合并与冲突
## 合并的本质
合并的本质:
* 将两个或者多个状态（代码快照/代码副本）合并
* git逐⾏检查冲突，并尝试⾃动解决 
* 解决失败，报错


### 合并与冲突解决
两个人同时修改了同一行,可能会发生冲突:
![64389602.png](github高级命令详解与实战_files/64389602.png)


![64590839.png](github高级命令详解与实战_files/64590839.png)


解决冲突 :
* 通过⼈人类的智慧，挑选正确的版本
* 严格按照命令提示进⾏冲突解决 
* --continue/--abort/--skip
![64888995.png](github高级命令详解与实战_files/64888995.png)

## rebase与merge(面试重点)
每一个commit都代表了仓库的代码的一个快照:
![65636687.png](github高级命令详解与实战_files/65636687.png)

merge的优点:
![66953893.png](github高级命令详解与实战_files/66953893.png)
练习:
[https://github.com/hcsp/advanced-git](https://github.com/hcsp/advanced-git)

练习:
1.我在一个分支上面开发了一些功能
2.我的同事将master向前推进了
怎么合并??
1.切换到主分支;
2.合并
![67951442.png](github高级命令详解与实战_files/67951442.png)



![68060920.png](github高级命令详解与实战_files/68060920.png)
发生了冲突:
![68106567.png](github高级命令详解与实战_files/68106567.png)

商量好保留哪一行即可:
![78795514.png](github高级命令详解与实战_files/78795514.png)
处理好后:
![78853993.png](github高级命令详解与实战_files/78853993.png)
```
#
$git checkout test-master-1
Switched to branch 'test-master-1'
Your branch is up to date with 'origin/test-master-1'.
#
$git merge test-my-feature-1
Auto-merging C.java
CONFLICT (content): Merge conflict in C.java
Auto-merging B.java
CONFLICT (content): Merge conflict in B.java
Auto-merging A.java
CONFLICT (content): Merge conflict in A.java
Automatic merge failed; fix conflicts and then commit the result.
#
$git status
On branch test-master-1
Your branch is up to date with 'origin/test-master-1'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified: A.java
        both modified: B.java
        both modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        advanced-git.iml

no changes added to commit (use "git add" and/or "git commit -a"
#
$git status
On branch test-master-1
Your branch is up to date with 'origin/test-master-1'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified: A.java
        both modified: B.java
        both modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        advanced-git.iml

no changes added to commit (use "git add" and/or "git commit -a")
#
$git add *.java
#
$git commit
[test-master-1 cc6d9a3] Merge branch 'test-my-feature-1' into test-master-1

```
### rebase
git-rebase :Reapply commits on top of another base tip
[](https://git-scm.com/docs/git-rebase#_synopsis)
基于另外一个分支尖端重演当前分支的变更;
![80173519.png](github高级命令详解与实战_files/80173519.png)



### rebase实战:
```
#
$git checkout test-master-2
Branch 'test-master-2' set up to track remote branch 'test-master-2' from 'origin'.
Switched to a new branch 'test-master-2'
#
$git rebase remotes/origin/test-my-feature-2
First, rewinding head to replay your work on top of it...
Applying: Comment A
Using index info to reconstruct a base tree...
M A.java
Falling back to patching base and 3-way merge...
Auto-merging A.java
CONFLICT (content): Merge conflict in A.java
error: Failed to merge in the changes.
Patch failed at 0001 Comment A
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".



```
![81042408.png](github高级命令详解与实战_files/81042408.png)

![81086199.png](github高级命令详解与实战_files/81086199.png)

![81196674.png](github高级命令详解与实战_files/81196674.png)

![81350907.png](github高级命令详解与实战_files/81350907.png)


![81376885.png](github高级命令详解与实战_files/81376885.png)
又发生冲突了;
 
![81456672.png](github高级命令详解与实战_files/81456672.png)
![81473377.png](github高级命令详解与实战_files/81473377.png)


![81583589.png](github高级命令详解与实战_files/81583589.png)

继续:
```

$git status
rebase in progress; onto bbec5ba
You are currently rebasing branch 'test-master-2' on 'bbec5ba'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

        both modified: B.java
        both modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        advanced-git.iml

no changes added to commit (use "git add" and/or "git commit -a")
$git add *.java
$git status
rebase in progress; onto bbec5ba
You are currently rebasing branch 'test-master-2' on 'bbec5ba'.
  (all conflicts fixed: run "git rebase --continue")

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified: B.java
        modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        advanced-git.iml
$git rebase --continue
Applying: Comment B/C

```
此时发现新问题了:
![82044950.png](github高级命令详解与实战_files/82044950.png)
![82127851.png](github高级命令详解与实战_files/82127851.png)
### rebase的禁忌(重要)
在和别人共享的分支上面千万不要用git push --force ！！！！！(就是说当前如果在master主分支上面的时候千万不要用这条命令)
那么此时怎么办呢???
换个思路:
![82415940.png](github高级命令详解与实战_files/82415940.png)


```
$git reset origin/test-master-2 --hard
#注意:此时是在分支上面了
$git checkout test-my-feature-2
Branch 'test-my-feature-2' set up to track remote branch 'test-my-feature-2' from 'origin'.
Switched to a new branch 'test-my-feature-2'
#
$git rebase test-master-2
First, rewinding head to replay your work on top of it...
Applying: Feature for A
Using index info to reconstruct a base tree...
M A.java
Falling back to patching base and 3-way merge...
Auto-merging A.java
CONFLICT (content): Merge conflict in A.java
error: Failed to merge in the changes.
Patch failed at 0001 Feature for A
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".


$git add A.java
$git status
rebase in progress; onto def866f
You are currently rebasing branch 'test-my-feature-2' on 'def866f'.
  (all conflicts fixed: run "git rebase --continue")

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified: A.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        advanced-git.iml

$git rebase --continue
Applying: Feature for A
Applying: Feature for B
Using index info to reconstruct a base tree...
M B.java
Falling back to patching base and 3-way merge...
Auto-merging B.java
CONFLICT (content): Merge conflict in B.java
error: Failed to merge in the changes.
Patch failed at 0002 Feature for B
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
###
$git add B.java
###
$git rebase --continue
Applying: Feature for B
Applying: Feature for C
Using index info to reconstruct a base tree...
M C.java
Falling back to patching base and 3-way merge...
Auto-merging C.java
CONFLICT (content): Merge conflict in C.java
error: Failed to merge in the changes.
Patch failed at 0003 Feature for C
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
###
$git add C.java
$git rebase --continue
Applying: Feature for C

```
![83795900.png](github高级命令详解与实战_files/83795900.png)
但是此时是可以用git push --force的!!!

### rebase 的优缺点
![84188516.png](github高级命令详解与实战_files/84188516.png)


### 解决重复冲突的方法(想把重复的变成一次解决)
 
方法一:
![84635091.png](github高级命令详解与实战_files/84635091.png)
![84679730.png](github高级命令详解与实战_files/84679730.png)

![84700760.png](github高级命令详解与实战_files/84700760.png)

![84746853.png](github高级命令详解与实战_files/84746853.png)


![84768555.png](github高级命令详解与实战_files/84768555.png)

![84880930.png](github高级命令详解与实战_files/84880930.png)

![84894992.png](github高级命令详解与实战_files/84894992.png)

但是上面这个方法有个缺点,丢失了一些提交历史

![85334396.png](github高级命令详解与实战_files/85334396.png)

![85375487.png](github高级命令详解与实战_files/85375487.png)
此时feature是master的祖先!!!
那么此时只要移动一下master指针即可!!!
### rebase的另外一种场景(定期和主干同步)
![85492568.png](github高级命令详解与实战_files/85492568.png)
由于很长时间没有和主干合并,你开发了很多功能,主干也向前移动了很多;
某一天你想合并的时候发现冲突太多了而无法合并,怎么办,需要定期和主干同步:
![85615437.png](github高级命令详解与实战_files/85615437.png)

![85627303.png](github高级命令详解与实战_files/85627303.png)


merge:比较杂乱

![85739114.png](github高级命令详解与实战_files/85739114.png)

### 第三种选择(git merge --squash)
除了rebase master以外的第三种选项;
![2830793.png](github高级命令详解与实战_files/2830793.png)
想把feature上面的变更移动到master上面:
![2886584.png](github高级命令详解与实战_files/2886584.png)
方法1:使用merge
方法2:在featutre分支上面使用rebase master;而后只是需要移动指针即可;
方法3:在master上面使用`git merge --squash`
实战:
![3097929.png](github高级命令详解与实战_files/3097929.png)
![3267298.png](github高级命令详解与实战_files/3267298.png)
![3130843.png](github高级命令详解与实战_files/3130843.png)

![3143430.png](github高级命令详解与实战_files/3143430.png)
下面解决冲突:
![3173159.png](github高级命令详解与实战_files/3173159.png)
解决好冲突:
![3323264.png](github高级命令详解与实战_files/3323264.png)
![3421918.png](github高级命令详解与实战_files/3421918.png)

![3462066.png](github高级命令详解与实战_files/3462066.png)

  
![3481992.png](github高级命令详解与实战_files/3481992.png)
![3535260.png](github高级命令详解与实战_files/3535260.png) 
### squash小结(重点推荐这个命令)
就是将当前分支上面所有提交捏扁为一个而后和master合并;
一般步骤:
1.切换到主分支(`git checkout master`)
2.而运用命令`git merge branch --squash`
3.一般是解决冲突
4.`git add *.java`
5.git commit -m "xxx"
## 使用merge还是rebase
![4123484.png](github高级命令详解与实战_files/4123484.png)
## 作业题:
[https://github.com/richard1230/advanced-git](https://github.com/richard1230/advanced-git)
### merge实战
```
 $git checkout test-master-1
Branch 'test-master-1' set up to track remote branch 'test-master-1' from 'origin'.
Switched to a new branch 'test-master-1'
$Git merge test-my-feature-1
merge: test-my-feature-1 - not something we can merge

Did you mean this?
        
$Git merge remotes/origin/test-my-feature-1
Auto-merging C.java
CONFLICT (content): Merge conflict in C.java
Auto-merging B.java
CONFLICT (content): Merge conflict in B.java
Auto-merging A.java
CONFLICT (content): Merge conflict in A.java
Automatic merge failed; fix conflicts and then commit the result.
$git status
On branch test-master-1
Your branch is up to date with 'origin/test-master-1'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified: A.java
        both modified: B.java
        both modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/

no changes added to commit (use "git add" and/or "git commit -a")
$git add *.java
$git status
On branch test-master-1
Your branch is up to date with 'origin/test-master-1'.

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

        modified: A.java
        modified: B.java
        modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/

$git commit -m "merge ok"
[test-master-1 0d1de2f] merge ok
$git status
On branch test-master-1
Your branch is ahead of 'origin/test-master-1' by 4 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/

nothing added to commit but untracked files present (use "git add" to track)
$git push
Everything up-to-date
```
### rebase实战
使用rebase前:
主要观察 test-master-2和test-my-feature-2这两个分支:
![41256027.png](github高级命令详解与实战_files/41256027.png)
![41288538.png](github高级命令详解与实战_files/41288538.png)

```
$git checkout test-my-feature-2
Already on 'test-my-feature-2'
Your branch is up to date with 'origin/test-my-feature-2'.
$git rebase test-master-2
First, rewinding head to replay your work on top of it...
Applying: Feature for A
Using index info to reconstruct a base tree...
M A.java
Falling back to patching base and 3-way merge...
Auto-merging A.java
CONFLICT (content): Merge conflict in A.java
error: Failed to merge in the changes.
Patch failed at 0001 Feature for A
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

$git add A.java
$git rebase --continue
Applying: Feature for A
Applying: Feature for B
Using index info to reconstruct a base tree...
M B.java
Falling back to patching base and 3-way merge...
Auto-merging B.java
CONFLICT (content): Merge conflict in B.java
error: Failed to merge in the changes.
Patch failed at 0002 Feature for B
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

$git add B.java
$git rebase --continue
Applying: Feature for B
Applying: Feature for C
Using index info to reconstruct a base tree...
M C.java
Falling back to patching base and 3-way merge...
Auto-merging C.java
CONFLICT (content): Merge conflict in C.java
error: Failed to merge in the changes.
Patch failed at 0003 Feature for C
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

$git add C.java
$git rebase --continue
Applying: Feature for C
$git push
To github.com:richard1230/advanced-git.git
 ! [rejected] test-my-feature-2 -> test-my-feature-2 (non-fast-forward)
error: failed to push some refs to 'git@github.com:richard1230/advanced-git.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
$git push --force
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 8 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.11 KiB | 1.11 MiB/s, done.
Total 9 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:richard1230/advanced-git.git
 + bbec5ba...a50857d test-my-feature-2 -> test-my-feature-2 (forced update)
$

```
使用rebase之后:
![42295905.png](github高级命令详解与实战_files/42295905.png)

### squash实战
```
$git checkout test-master-3 
Branch 'test-master-3' set up to track remote branch 'test-master-3' from 'origin'.
Switched to a new branch 'test-master-3'
$git merge test-my-feature-3 --squash
merge: test-my-feature-3 - not something we can merge

Did you mean this?
        
$git merge remotes/origin/test-my-feature-3 --squash
Auto-merging C.java
CONFLICT (content): Merge conflict in C.java
Auto-merging B.java
CONFLICT (content): Merge conflict in B.java
Auto-merging A.java
CONFLICT (content): Merge conflict in A.java
Squash commit -- not updating HEAD
Automatic merge failed; fix conflicts and then commit the result.
$git status
On branch test-master-3
Your branch is up to date with 'origin/test-master-3'.

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

        both modified: A.java
        both modified: B.java
        both modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/

no changes added to commit (use "git add" and/or "git commit -a")
$git add *.java
$git status
On branch test-master-3
Your branch is up to date with 'origin/test-master-3'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified: A.java
        modified: B.java
        modified: C.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/

$git commit -m "Merge --squash的提交"
[test-master-3 7a85239] Merge --squash的提交
 3 files changed, 3 insertions(+), 3 deletions(-)

```
![43076419.png](github高级命令详解与实战_files/43076419.png)

![43119080.png](github高级命令详解与实战_files/43119080.png)




