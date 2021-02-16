[原文地址](https://www.cnblogs.com/spec-dog/p/11043371.html)
## 分支管理

创建项目时（一般是服务型项目，工具型或辅助型项目可以简单一些），会针对不同环境创建三个常设分支：

- develop：开发环境的稳定分支，公共开发环境基于该分支构建。

- pre-release：测试环境的稳定分支，测试环境基于该分支构建。

- master：生产环境的稳定分支，生产环境基于该分支构建。仅用来发布新版本，除了从pre-release或生产环境Bug修复分支进行merge，不接受任何其它修改

平时开发工作中，会根据需要由开发人员创建两类临时分支：

- 功能（feature）分支：为了开发某个特定功能，从develop分支上面分出来的。开发完成后，要merge到develop分支。功能分支的命名，可以采用feature-*的形式命名(*为任务单号)

- Bug修复（fixbug）分支：为了修复某个bug，从常设分支上面分出来的。修复完成后，再merge到对应的分支。Bug修复分支的命名，可以采用fixbug-*的形式命名（*为bug单号）

## 流程规范

### 正常开发流程

1. 从develop分支切出一个新分支，根据是功能还是bug，命名为feature-* 或 fixbug-*。

2. 开发者完成开发，提交分支到远程仓库。

3. 开发者发起merge请求（可在gitlab页面“New merge request”），将新分支请求merge到develop分支，并提醒code reviewer进行review

4. code reviewer对代码review之后，若无问题，则接受merge请求，新分支merge到develop分支，同时可删除新建分支；若有问题，则不能进行merge，可close该请求，同时通知开发者在新分支上进行相应调整。调整完后提交代码重复review流程。

5. 转测时，直接从当前develop分支merge到pre-release分支，重新构建测试环境完成转测。

6. 测试完成后，从pre-release分支merge到master分支，基于master分支构建生产环境完成上线。并对master分支打tag，tag名可为v1.0.0_2019032115（即版本号_上线时间）

流程示意图如下所示
![image.png](/d/2MWcU035pdcO)
 

 

## 并行开发测试环境Bug修复流程

并行开发（即前一个版本已经转测但未上线，后一个版本又已在开发中并部分合并到了develop分支）过程中，转测后测试环境发现的bug需要修复，但是develop分支此时又有新内容且该部分内容目前不计划转测，可以pre-release切出一个bug修复分支。完成之后需要同时merge到pre-release分支与develop分支。merge时参考“正常开发流程”。流程示意图如下

 ![image.png](/d/2gPWfw3KSO4i)

 

## 生产环境Bug修复流程

生产环境的Bug分两种情况：

- 紧急Bug：严重影响用户使用的为紧急Bug，需立即进行修复。如关键业务流程存在问题，影响用户正常的业务行为。

- 非紧急Bug或优化：非关键业务流程问题，仅影响用户使用体验，或出现频率较小等，为非紧急Bug，可规划到后续版本进行修复。

非紧急Bug修复参考“正常开发流程”。

紧急Bug修复，需要从master分支切出一个bug修复分支，完成之后需要同时merge到master分支与develop分支（如果需要测试介入验证，则可先merge到pre-release分支，验证通过后再merge到master分支上线）。merge时参考“正常开发流程”。流程示意图如下

![image.png](/d/C6kmj0mVyYo)
=======
My very first helloworld is a diary that keep trace on my progress in Unity.
And I will share my experience to you. 
You can connect with me by QQ:554825519


add Line for testing prository branch


test merge form branch new to main 

