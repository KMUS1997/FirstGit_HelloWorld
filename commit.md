
## 1. commit message format(信息域)

commit message一般分为三个部分Header，Body 和 Footer

```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
其中，Header 是必需的，Body 和 Footer 可以省略

Example:
PS D:\git\pythonPractice> git log
commit 58a7a966acb9aa2fffc0e02c9ce3be64b8949991 (HEAD -> master)
Author: Zhiwei Tian <hebeitianzhiwei@outlook.com>
Date:   Fri Aug 17 17:38:36 2018 +0800

    feat(serve): add grpc server



```

## 1.1 HEAD

type用于说明 commit 的类别，只允许使用下面7个标识

```
feat：新功能（feature）
fix：修补bug
docs：文档（documentation）
style： 格式（不影响代码运行的变动）
refactor：重构（即不是新增功能，也不是修改bug的代码变动）
test：增加测试
chore：构建过程或辅助工具的变动

```

scope 用来说明本次Commit影响的范围，即简要说明修改会涉及的部分,比如数据层、控制层、视图层等,

subjectcomment所在的位置,这次提交的简短描述

## 1.2 Body 是对本次 commit 的详细描述，可以分成多行

## 1.3 Footer 部分只用于两种情况

**不兼容变动**

如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法

**关闭 Issue**

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue (可依次关闭过个issueCloses #123, #245, #992)

## 1.4 Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header

```
revert: type(scope):  some comment
This reverts commit bfe307ce57d87677c6c473c228e6c2ed8b81dcec.

```

Body部分的格式是固定的，必须写成This reverts commit <hash>.，其中的hash是被撤销 commit 的 HSHA 标识符。
如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面

2. 使用commitizen来执行规范

前提需要安装node(官网下载地址)
如果看到 EACCES 错误, 请阅读 fixing npm permissions 获取帮助)
以下操作均参考cz-cli仓库所给出的指导,需要获取更加详细的信息请前往cz-cli.

全局安装commitizennode模块

```
npm install -g commitizen

```

在项目目录下运行命令
如果你的项目不是node项目,下面的内容可以直接忽略,请直接翻到 一级标题3

```
commitizen init cz-conventional-changelog --save --save-exact

```

此时可能会报找不到package.json的错误,使用下面命令来自动生成一个项目的package,然后在运行2中的命令.

```
npm init --yes

```

运行完以上一律使用git cz 代替git commit来提交代码,同时会显示一下选项来自动生成符合格式的commit message.

```
PS ~/git> git cz
cz-cli@2.10.1, cz-conventional-changelog@2.1.0


Line 1 will be cropped at 100 characters. All other lines will be wrapped after 100 characters.

? Select the type of change that you're committing: (Use arrow keys)
> feat:     A new feature
  fix:      A bug fix
  docs:     Documentation only changes
  style:    Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
  refactor: A code change that neither fixes a bug nor adds a feature
  perf:     A code change that improves performance
  test:     Adding missing tests or correcting existing tests
(Move up and down to reveal more choices)

```

按照提示,你可以写出规范的message了
idea有插件可以使用git commit template(可能需要科~学上网)

commitizen同时可以检查commit message是否符合格式.
生成change log,还又一些高级用法比如ghooks
这里就不细说了.详细请查看参考链接和validate-commit-msg

现在项目中可能多出来dir:node_nodules, file:package.json, package-lock.json这些目录和文件,这是node安装模块产生的,如果不是node项目都可以忽略掉,熟悉node的同学肯定都知道哪些是有用的了.

3. 在非node项目中,优雅的使用git-cz

此处可接2.1上下文,安装git-cz

```
npm install -g commitizen git-cz

```

使用git-cz这个adapter还可以自定义一些内容,默认也会附带一些表情,如下图
详细的设置操作请参考仓库 git-cz 给出的详细信息




作者：TinChiWay
链接：https://www.jianshu.com/p/36d970a2b4da
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。