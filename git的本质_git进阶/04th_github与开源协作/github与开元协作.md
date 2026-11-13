[TOC]
纪律：开源项目协作流程
GitHub的原始仓库与fork
在本地管理多个远程仓库
【实战】将fork的仓库与上游进行同步
检索、发起、关注一个讨论
使用Pull request进行协作
在PR中进行日常code review与沟通
在PR中进行修改建议
三种合并方式详解
GitHub API简介与使用
【实战】搭建一个简单的GitHub机器人
【实战】GitHub pages搭建博客平台
## 大纲
![64177604.png](github与开元协作_files/64177604.png)

## 开源项目协作原则
![64208213.png](github与开元协作_files/64208213.png)

![64492787.png](github与开元协作_files/64492787.png)

提问题的时候最好能够复现现场!!!
经典提问题模板:
[https://youtrack.jetbrains.com/issue/IDEA-197550](https://youtrack.jetbrains.com/issue/IDEA-197550)

![66013697.png](github与开元协作_files/66013697.png)
 


![66069906.png](github与开元协作_files/66069906.png)
另外一个模板:
[https://github.com/gradle/gradle/issues/1861](https://github.com/gradle/gradle/issues/1861)

![66791889.png](github与开元协作_files/66791889.png)

![66823074.png](github与开元协作_files/66823074.png)



![66835649.png](github与开元协作_files/66835649.png)


![66853217.png](github与开元协作_files/66853217.png)


最好能新建一个复现问题的仓库:(类似下面这种)
[https://github.com/blindpirate/jdk-cp-option-file-issue](https://github.com/blindpirate/jdk-cp-option-file-issue)

## 如何参与开源项目的协作
## issue
有的issue不在github,需要搜索:
google: xxx issue tracker
![72201897.png](github与开元协作_files/72201897.png)



## commit message(重要)
google:commit message
![72298438.png](github与开元协作_files/72298438.png)


[https://chris.beams.io/posts/git-commit/](https://chris.beams.io/posts/git-commit/)
总结之后空一行而后详细描述你所做的
![72637169.png](github与开元协作_files/72637169.png)

## pull request
在分支上面创造的提交,Files changes: pr总的变更
![73702788.png](github与开元协作_files/73702788.png)


![73217776.png](github与开元协作_files/73217776.png)
创建pr的时候可以选择创建一个草稿pr,如下图所示:
![73451978.png](github与开元协作_files/73451978.png)
##  commit的三种状态
pending:集成测试正在进行中;暂时还不知道它是成功还是失败
success和failure就不用说了;
![74001189.png](github与开元协作_files/74001189.png)


## 从0开始向开源项目做贡献
![74680150.png](github与开元协作_files/74680150.png)


以spring-boot为例:

![74324876.png](github与开元协作_files/74324876.png)

 
![74354720.png](github与开元协作_files/74354720.png)

还有一种方式是利用spotbug来检查b  :
![74574329.png](github与开元协作_files/74574329.png)

## 探索issue tracker
![75688133.png](github与开元协作_files/75688133.png)

spring-boot相对不适合新手!

一般情况下:
如果需要对private级别的代码做单元测试,那么就把需要测试的代码写成包级私有的!!
只要两个类导入的包的名字一样,哪怕它们相隔天南海北,那么它们就是同一个包下面的!!

看一看groovy社区: 
![76751712.png](github与开元协作_files/76751712.png)
优先等级:
Critical:优先等级最高;
Blocker:优先级次之;
bug:优先等级一般;
issue:优先级排在bug之后,小问题
not a bug:优先级最低

![76900148.png](github与开元协作_files/76900148.png)
groovy社区:
[https://issues.apache.org/jira/projects/GROOVY/issues](https://issues.apache.org/jira/projects/GROOVY/issues)