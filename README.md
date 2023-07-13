# 多轮对话技术研究及在防洪减灾方面的应用

## 项目简介

本项目先实现基于管道的任务型多轮对话系统，对意图识别和对话策略进行建模，使得对话系统具有很好的性能，然后基于图数据库建立洪水传播时间的数据库，并采用最短路径算法计算洪水传播时间，最后讲将二者结合起来，开发一个任务型多轮对话防洪减灾系统，从而提升防灾减灾系统的人机交互能力，为政府决策提供更好的服务。

## 项目成员要求

要求项目成员具有编程基础，熟悉Java或Python语言，其中有深度学习基础的优先考虑。
本项目牵涉到的软件技术包括：Java EE、Python、NLP、知识图谱等，要求有较强的学习能力。

## 立项依据

洪水灾害是由于江河、湖泊、水库水位急剧上升，大坝发生溢流或决口，水流入境等原因造成的。洪水除了造成重大农业灾害外，还造成工业损失乃至生命财产损失，是对人类生存起到威胁作用的十大自然灾害之一。洪水灾害是我国发生频率最高、影响范围最广、对国民经济和社会经济发展影响最为严重的自然灾害，目前的防洪减灾系统都是基于传统方式开发的信息服务系统，很少和对话系统相结合，也很少采用图数据库技术来实现洪水传播时间的计算，少数地方开发了仅仅是简单的单轮对话，难以实用。对话系统依据对话的轮次可以分成单轮对话和多轮对话。单轮对话只会考虑当前轮次的信息，而多轮对话对人机对话的上下文、指代省略的补全和复杂需求的明确等问题都有着更为复杂的要求，也更加贴近现实生活中咨询、推荐、服务需求等应用场景。本项目主要研究的是任务型多轮对话系统，其是为了完成指定目标，如洪水传播时间的对话、降雨情况的时空分布等人机交互任务。

## 国内外现状

### 1、单轮对话和多轮对话

对话系统依据交互轮数的复杂程度来进行分类，可以划分为单轮对话和多轮对话。单轮对话交互轮次为一轮，就是在一轮人机对话之后，去完成用户相对简单的请求，只要完成一些已经被设置好的或简单的操作，系统判断用户相对简单的意图进而完成对应简单的任务，在对话过程中不需要考虑真实生活中人与人交流出现的与上下文相关指代词等，换而言之不用根据其他交互的内容就能顺利完成用户的请求，常见的单轮对话有“闲聊机器人”、“电商机器人”等等。

和单轮对话不同，多轮对话经常需要联系上下文，在回复用户请求的过程中，多轮对话系统围绕一个主题与用户进行多次信息交流来描述任务，进而让系统了解用户真正的意图。任务型多轮对话系统在日常生活中有着广泛的应用，目前学术界已经有很多相关方面的研究，与此同时自然语言具有灵活性的特点，用户的真实意图在一轮的人机交互中经常难以理解，所以多轮对话更贴近真实的对话场景，也是本项目的研究重点。

### 2、基于管道的任务型对话系统

基于管道的方法是模块化开发，程序设计者首先要开发各个子模块，然后把各个子模块结合起来，一个完整的对话系统就形成了。这种方法最大特点是模块之间彼此基本无关联，各个模块独立开发也意味着可以使用不同技术。

基于管道的任务型对话系统，其可以分为三个模块，对应的是自然语言理解（Natural Language Understanding, NLU）模块、对话管理（Dialogue Manager, DM）模块以及自然语言生成（Natural Language Generation, NLG）模块。

### 3、防洪减灾决策支持系统

防洪减灾决策支持系统（Decision Support System，DDS）是一门具有跨学科特点的前沿课题，包含了水力学、气象学、水利经济学、水力学、水文学、控制论、信息论、系统工程学、运筹学、GIS、数据库、计算机网络、复杂计算、专家系统、信息采集技术、可视化技术。所以，当前还未有一个功能完备、技术领先、具有较强人机交互的、实用好的为防洪决策全过程提供真正有效的系统。

## 项目研究内容

* （1）提出基于外部记忆的意图识别模型。多轮对话更多的是考虑历史信息记录，使用循环神经网络来进行意图识别比较适合。随着人机对话的复杂性增加，循环神经网络因为内部记忆单元存储容量太小，容易丢失关键信息，所以需要设计基于外部记忆的意图识别模型。此模型是以BiLSTM为基础，同时引入外部记忆单元和自注意力机制，最后添加Dropout防止神经网络出现过拟合。

* （2）使用DQN算法实现对话策略模块。在传统基于最大似然估计模型中每一轮对话中所获得的回复是对话系统生成概率最大的句子，很多万能回复容易被选中，当系统和用户出现相似或者相同的语句的时候，系统容易陷入死循环；对话系统一般有很大的状态空间或动作空间，对话策略使用的Q-Learning要想建立一个Q表去维护要消耗大量的内存。为了解决上述问题在对话策略中引入DQN算法，其是计算的是每个回复语句能够为对话系统中输入带来多少的未来奖励，进而来挑选能够为系统带来最大未来奖励的语句。

* （3）设计实现河流的防洪指标知识图谱，包括：图数据库建设；知识图谱可视化；河道站查询；洪水传播时间查询；水位流量关系曲线查询，降水的时空分布查询。

* （4）实现基于任务型多轮对话的防洪减灾系统。重点对将前面提出的模型并结合相关算法应用到防灾减灾服务的对话上，最后很好的为政府防灾减灾决策提供支持。  

## 项目实施方案

### 一、相关理论和技术学习

* 1、自然语言处理：
重点是词向量、序列到序列（Seq2Seq）模型等。

* 2、深度学习
包括循环神经网络、注意力机制、Q-Learning、BiLSTM等。

* 3、 开发相关技术
包括图数据库Neo4j、Java EE开发技术、Python、Layui框架、Echarts和D3(data driver document)等。

### 二、基于DQN的对话策略模型

* 1、DQN算法学习

DQN算法属于深度强化学习算法经典算法之一，其结构是“环境—代理”（environment-agent）框架，其原理是代理依据目前状态挑选一个合适动作作用于环境，接着环境的状态会发生相应的改变并且返回对应奖励，代理的本质目标是获取最大化未来能够拿到的全部奖励之和，由奖励调整动作并且形成一个循环的过程。

在对话策略中使用DQN算法，是为了获取到一个有助于多轮对话系统持续有效进行的对话策略。这个目的具体到每一轮的对话中可以等价成每一轮对话都是挑选出为整个对话过程带来最大收益的语句。回复带来的具体收益是可以从对话是否产生万能回复、是否插入新的信息、是否与历史信息差不多等多个方面来判断。有了上面的判断规则，在人机对话可以把对话策略的具体学习过程建模成为典型的强化学习过程。

DQN算法的核心是深度价值网络Q，这个网络根据对应的算法进行迭代更新，目的是通过估算每一个状态s来进一步选择相应动作a的价值q(s,a)。这个价值q是代表了目前状态s下挑选动作a能带过来的将来折扣奖励之和。在人机多轮对话的过程中，把目前的输入语句序列记为，输入经过回复生成的模型可以得到若干等候选择的回复列表。

* 2、模型训练

详细介绍基于DQN的对话策略模型的训练。对于强化学习，其核心目标就是获取最大化未来的累积奖励，所以在模型中定义合适奖励函数对多轮对话系统是非常重要的。奖励函数的作用是为了指引人机对话向任务完成度越高、对话信息更加丰富、万能通用回复更少的方向进行，这种指引是有利于任务型人机对话顺利完成的。

* 3、实验设计与结果

从评价指标、实验数据集、实验结果分析等方面进行描述。

### 三、基于多轮对话技术的防洪减灾决策支持系统实现

包括需求分析、系统设计、系统实现等内容。

人机对话窗口

系统登录

水位流量关系线

知识图谱

洪水传播时间

河道站查询

降水查询

主要功能

## 项目目标、主要特色及工作进度

### 一、系统目标

1、完成多伦对话技术研究

2、实现防洪指标的图数据库建设

3、实现多伦对话管理系统

4、基于多伦对话管理系统实现防洪减灾决策支持系统

### 二、主要特色

1、基于知识图谱的矢量分析与展示

2、基于最短路径的洪水传播时间

3、便捷的人际对话功能

### 三、工作进度

目前已经完成前期理论研究和相关的技术选型，后续安排：

1、3个月内容完成多伦对话技术的实验及分析；

2、6个月内完成完成Java EE技术学习、Python学习、图数据库应用学习；

3、9个月内完成多伦对话管理系统功能；完成图数据库相关应用；

4、10个月内完成多伦对话管理系统与图数据库应用的集成，同时完成整个项目的内容。

## 项目文件组成结构

```shell

rasa_project/
├── actions/              # 包含用于处理自定义动作的 Python 文件
├── config.yml           # 包含 Rasa 配置的文件
├── credentials.yml      # 包含与外部系统进行身份验证所需的凭据信息的文件
├── data/                # 包含训练数据和 NLU 语料库
│   ├── nlu.yml          # 包含自然语言理解 (NLU) 训练数据的文件
│   └── stories.yml      # 包含对话流程的训练数据的文件
├── domain.yml           # 包含对话领域的定义
├── endpoints.yml        # 包含与外部系统进行通信所需的终端点信息的文件
|—— index.html           # 本地网页对话窗口
├── models/              # 包含已训练的 Rasa 模型
└── tests/               # 包含测试脚本

```

## For Teammates

### 一，在Windows操作系统上部署rasa项目

[Rasa官方教程](https://rasa.com/docs/rasa/installation/installing-rasa-open-source/)

[官方视频教程](https://www.bilibili.com/video/BV1A94y1U7Sr/)

1，安装Python 3.10版本

去官网或者微软商店安装

[python](https://www.python.org/)

2，安装Anaconda

[Anaconda](https://www.anaconda.com/)

（非必要)建议在VSCode中运行项目，下载插件Python Environment Manager管理python环境

3，使用conda部署rasa

```shell
conda activate base
```

```shell
pip3 install rasa
```

```shell
pip3 install spacy
```

```shell
python -m spacy download zh_core_web_trf
```

至此所需要的所有依赖包都安装完毕

4，运行rasa项目

```shell
rasa shell  @REM 在命令行中运行项目
```

```shell
rasa run -m --enable-api --cors "*"  @REM 在后台运行，可在本地网页进行交互
```

### 二，使用docker部署rasa项目
1. 拉取rasa镜像
```shell
docker pull philoboy/rasa_zh_md
```

2. 初始化<br>
先初始化，但如果不设定用户的话会出现权限问题。
按官方的解释为了避免容器使用root权限，因此容器默认被uid为1001的用户拥有，因此如果linux用户的uid不是1001就会碰到权限问题
进入创建的rasa文件夹，运行以下指令
```shell
docker run --name=rasa_init --user 1000(这里输入自己用的用户的uid) -v $PWD:/app philoboy/rasa_zh_md:1.0 init --no-prompt
```

3. 部署rasa shell与rasa机器人对话<br>
因为init容器不会一直运行，因此我们还需要弄一个执行rasa shell命令的容器。
```shell
docker run -it --name=rasa_shell --user 1000 -v $PWD:/app rasa/rasa shell
```
无错误运行下，应该会直接进入rasa的对话入口。输入/stop退出rasa shell，容器也会退出。
那么再次运行就不再是docker run了，而是docker start -i rasa_shell
如果之前使用的是docker run -id而不是-it或者docker start rasa_shell没有-i标签那么rasa服务就会在后台持续运行，那么此时应该
```shell
rasa attach rasa_shell
```
4. 训练新模型
修改训练数据和相关配置后
```shell
docker run --name=rasa_train -v $(pwd):/app philoboy/rasa_zh_md:1.0 train --domain domain.yml --data data --out models
```
容器创建好之后下次训练模型只需要docker start rasa_train就可以了。
新模型会放入models文件夹，启动rasa_shell会自动加载最新模型。
5. 开放api端口
首先要在credentials.yml中rest:后面加上
url: "http:localhost:5005/webhooks/rest/webhook"
之后就是通过这个url与rasa交互
然后创建新容器
```shell
docker run --name=rasa_run -p 5005:5005 -v $PWD:/app philoboy/rasa_zh_md:1.0 run --enable-api --cors "*"
```
端口直接映射为5005。
这之后会在rasa server is up and running停住不出去，这个时候直接ctrl + c手动终止
然后docker start rasa_run就可以后台运行。
