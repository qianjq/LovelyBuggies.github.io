---
layout:     post
title:      实习感受
subtitle:   我在中科院自动化所的实习感受
date:       2018-08-29
author:     Nino Lau
header-img: img/post-bg-scenery.jpg
catalog: true
tags:
    - experience
    - essays
---

> 2018年7月至8月，我在中科院自动化所CASIA进行了关于强化学习方向的实习。实习主要是把open AI的一个新算法——MADDPG算法应用大暴雪游戏的星际争霸2强化学习环境中去。这次实习增加了我对机器学习的理解，同时也磨练了我应对困难的能力。


### 1 大北京啊

北京，这座城市，不仅仅给人带来车水马龙的喧嚣，也有劳碌过后的疲倦与孤独。

![night](http://wx2.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswp15ad6j30k00qo75f.jpg)

![night](http://wx2.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswpmxzumj30xc0m8gri.jpg)

中科院自动化所CASIA，坐落于知春路北。和其他中科院的研究所一样，南望西土城，北接清北，周围拥趸着各大高校和科研单位。”雄州雾列，俊采星驰“，这里聚集了五湖四海的人才，有着丰富的资源，是逐梦者的天堂。早高峰的马路上，四处可见背着公文包的上班族；午市的咖啡厅内，常常可以旁听到投资与市场，客户与需求的字眼；夕阳落下，各个所里的研究员带着小牌子成群结队地走向食堂...


### 2 CASIA——中关村里的桃花源

我所实习的自动化位于中科院研究所群的东南角。自动化所大厦，给我的第一感觉就是，它在北京这种高楼林立的都市，的确一眼看上去相貌平平。深入其中才发现，这里面是一片环境优雅的公园。每年，数以百计的前沿科学成果从这里诞生；从各个学校的实习生络绎不绝，撑起了这个知识高地。

![CASIA](http://wx3.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswo5lw8jj30u0140jxn.jpg)

![CASIA](http://wx1.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswoi2nbhj31400u0dkz.jpg)

![CASIA](http://wx1.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswdeqbp3j31400u0te0.jpg)


### 3 Office is really decent!!!

踱步到办公室的四周，就可以听到IT男们敲代码的声音，也算是“未见其室，先闻其声”了。

一进门，放眼望去，每个人都在小隔间里钻研着自己的project。

![office](http://wx1.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswpwyz97j30u0140wi6.jpg)

我很喜欢这里的办公桌，比起我在学校实验室的办公桌更好的利用了空间。双屏显示大大提升了效率（想象不到我这次的实习项目如果用台式机单屏显示有多麻烦），配合上我用我的PC看文档（Mac人性化的显示看文档简直美哒哒），给我营造了一个很舒适的办公环境。

![office](http://wx2.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswpr4watj31400u0787.jpg)


### 4 项目起步

在分配好了座位之后，我就开始接手了这个[项目](https://github.com/LovelyBuggies/Python_MADDPG_SC2LE)。

第一个星期主要是阅读有关的[论文](https://github.com/LovelyBuggies/Python_MADDPG_SC2LE/tree/master/Papers)，包括DQN、DDPG、sc2le（当然还有灭霸MADDPG——集长难算法于一体）。当然了，又长又难的英文论文怎么也是块硬核桃，那么这些[参考资料和网站博客](https://github.com/LovelyBuggies/Python_MADDPG_SC2LE/blob/master/README.md)就是我的核桃夹。


### 5 群蛇乱舞

第二个星期开始，我开始配置环境，熟悉前人的文档和代码。正所谓**“打代码一天，配环境一周”**，真是个艰苦卓绝的过程！

首先我先用我电脑自带的python2，但是出现了各种玄学的问题。加之听了[莫烦python](https://morvanzhou.github.io)（不得不说，这个教程挺良心的）的[神经网络](https://morvanzhou.github.io/tutorials/machine-learning/theano/)教程，我坚定了下载python3的决心。但是"**魔高一尺，道高一丈**"，python3下好了之后，pip3获取不了Tensorflow，用网站上的各种不靠谱方法尝试了之后，我的电脑上涌现出了各种各样老的、过时的、无效的python版本。

在蟒蛇们（python就是巨蟒的意思）纠缠不清的时刻，在师兄的帮助下，我获得了anaconda这把利剑。剑刃出鞘，我卸载了所有的python（除了本机自带的python2）
，安装了anaconda这个美丽的虚拟环境。确实成功了，已经可以运行open AI的maddpg.py。当然这还不够，我还需要运行一下实验室已经写好的接口。临近第二周末，接口的运行还是停滞不前。

这时候，实验室唯一做星际争霸2的师兄去另一个实习了。好处是，我可以用他已经搭建好的环境了；但是另外，也意味着我将独自面对更多的挑战。


### 6 良好代码，始于风格

星际争霸2这个项目的代码风格真的不好，原因啊，我估计有一下几条：

* 流水实习生，接手项目人多，每个人风格迥异
* 实习生实习周期短，没法长期跟进
* 实习生为了纯粹追求效率，没有考虑代码健壮性和优雅性（哈哈哈，这词我编的）
* 甚至没有建立git repo，成员组织性较差

所以，我刚开始的时候，是想从底层改动reward方法的，可是由于每一层文件都有涉及到reward，考虑到巨量工作和时间成本，我还是选择随波逐流了。。。（我估计之前的几个实习生也是这么想的）

虽然没能做什么大的改动，但是我还是一心向善，建立了一个[organization——pysc2RL](https://github.com/pysc2RL)，带我们的导师也不是很熟悉，而且组织成语的git好像也没有多么丰富，所以未来可能被弃坑。

但是我还是希望[这个组织](https://github.com/pysc2RL)能够持续发展这项成果。


### 7 教育孩子真不容易

刚开始进行这个任务的时候，发现胜率可达到90%，简直是复仇者联盟般的存在。

![marvel-heros](http://wx3.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswowebrfj30um0fi1kx.jpg)

后来发现，哈哈哈，初始化的时候作弊了。代码把小兵动作初始化为攻击，这是做好的行为。一旦去掉这个初始化，高能战士们纷纷泯然众人。

于是我尝试改进reward，具体改进策略可以看我的[git repo](https://github.com/LovelyBuggies/Python_MADDPG_SC2LE)。

总之，就是进行了种种尝试，发现这群小兵，是真的熊孩子，死活不听话。**不仅感慨，“教育孩子真是不容易”。**


### 8 日常插曲

天天吃饭、睡觉、打代码的生活这是无聊，人生当然要有点别的乐趣。

每周我都会去北航打几次球，自己看看电影啥的（比如最近痴迷漫威）。。。

繁忙的工作中总是掺杂着些许饕餮，安慰我疲惫的心灵，融科天地便是我的栖息所，是我味蕾的港湾（哈哈哈，我编不下去了，上图吧）

![environment](http://wx3.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswdpecq6j30u0140q9s.jpg)

![environment](http://wx3.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswd7861oj30u0140n2q.jpg)

![environment](http://wx3.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswdjhhu5j31400u0jxj.jpg)

午酣一酌冷萃亦是美好体验：

![coffe](http://wx3.sinaimg.cn/mw690/bmiddle/006zGYyogy1fuswopnxegj31400u042p.jpg)


### 9 项目完结

不知不绝，一个多月过去了。我实习篇章即将完结，幸福快乐和压抑烦躁的句读也将停止。

写好了总结，为实习部门建了一个组织，交接了任务，say了goodbye，收拾好了包袱...

2018年8月28日，余晖洒落在办公室的每一处角落，我最后看了一眼我工作的地方，踏出了门。这是一处我曾经工作一个月的地方，虽然贡献甚微，但是对于我来说，这里意义非凡。

### 10 曲终人散

撰此博客，主要是为了纪念我在中科院自动化所实习的时光。

**“然后在某个不经意的瞬间，我发现，原本费尽心机想要忘记的事情，就真的这么容易就忘记了。”**

