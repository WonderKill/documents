### 目录
- [Git版本控制](#gitversion)
- [文档规范](#documents)
- [项目进度沟通](#protime)
- [代码规范](#coderule)

---

### 前言


我们之前项目开发过程中，有很多规范方面的问题做得不好，因此综合之前开发中存在的问题，提出一些开发规范方面的建议，希望大家能够遵守，让合作开发变得更加高效顺利。

<a name="gitversion" />

### Git版本控制

#### 主分支
- 首先，代码库应该有一个、且仅有一个主分支。所有提供给用户使用的正式版本，都在这个主分支上发布。注意每次发布到master分支时，都打一个tag，标记此次发布的版本号。如**dianxia_release_v1.0.1**

![image](http://www.terabits-wx.cn/master.png)
#### dev开发分支

- 主分支只用来发布重大版本，日常开发应该在dev分支上完成。当开发完成后，如果想正式对外发布，就在master分支上，对dev分支进行合并。

![image](http://www.terabits-wx.cn/dev.png)

- 由于一期项目新功能的开发和二期项目架构的更新是同步进行的，所以目前约定一期项目**新功能**开发在**tbtest**分支上进行，**二期项目**架构更新在**dev**分支上进行，如下图所示。新功能在tbtest分支上开发测试完成后，合并到master分支上，然后再切换到dev分支，将最新的master分支与dev分支合并。

![image](http://www.terabits-wx.cn/threebranchnew.png)

#### feature新功能分支
- 软件开发中，总有无穷无尽的新的功能要不断添加进来。添加一个新功能时，最好不要因为一些试验性质的代码，把大家公用的dev分支搞乱，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。feature分支可以按照**feature_[功能名]_20180107**这种格式来命名。

![image](http://www.terabits-wx.cn/feature.png)

#### fixbug修补分支
- 修补bug分支。软件正式发布以后，难免会出现bug。这时就需要创建一个分支，进行bug修补。修补bug分支是从master分支上面分出来的。修补结束以后，再合并进master和dev分支。它的命名，可以采用**fixbug_[bug名称]_20180107**的格式。

![image](http://www.terabits-wx.cn/bugxiubu.png)

<a name="documents" />

### 文档规范

#### 文档格式

- 出自平台组成员的开发文档，统一使用markdown格式，请大家抽空自学markdown语法的使用。

#### 文档存放位置

- 公共文档，比如项目规划书，数据库设计手册，硬件通信格式等，统一存放在这个[github仓库](https://github.com/xiaoheifish/documents)，每一个新的项目，只需要新建一个项目文件夹，存放与这个项目有关的文档。大家有想要与他人分享的学习笔记，也可以传上来，共同学习进步。
- 前后端接口文档，由于前后端接口文档只与相关分项目的开发人员有关，所以前后端接口文档放在各个子项目仓库的Wiki目录下，有新人参与到项目中来，仓库负责人把这个人添加为合作者即可。

![image](http://www.terabits-wx.cn/wiki.png)

<a name="protime" />

### 项目进度沟通

- 之前开发的时候，出现了前期时间把控不好，后期熬夜的现象，所以项目时间的控制很重要。我们统一用一款在线项目管理工具，[trello](https://trello.com/b/QqE5Q558/%E5%85%85%E7%94%B5%E5%A1%94%E9%A1%B9%E7%9B%AE)，每一个新项目，都会使用一个新的看板。
- 请还没有trello账号的小伙伴自行注册，并联系潘总将大家拉入群里。
- 平台开发过程，我大致分为以下几个步骤，需求定义，设计，开发，测试发布，bug修改，我也将目前trello上的充电桩项目的卡片分成了这几大块。请大家及时更新自己那部分的进度，已完成就归档到已完成面板。

![image](http://www.terabits-wx.cn/trello.png)
- trello下载文件速度极慢，请大家有上传文件的需求时，在钉钉群内上传。

<a name="coderule" />

### 代码规范

- 我们统一按照[阿里巴巴Java 开发手册](http://techforum-img.cn-hangzhou.oss-pub.aliyun-inc.com/%E9%98%BF%E9%87%8C%E5%B7%B4%E5%B7%B4Java%E5%BC%80%E5%8F%91%E6%89%8B%E5%86%8C%28%E7%BB%88%E6%9E%81%E7%89%88%29.pdf)这份文档里的要求，来规范代码，请大家下载手册配套的IDE插件，按照[这篇教程](https://yq.aliyun.com/articles/224817)里的方法安装，每次写完代码，都用插件检查一遍，并根据提示修改自己代码书写不规范的地方。
- 请大家写代码的时候，一定要认真写注释，方便其他看代码的人。
