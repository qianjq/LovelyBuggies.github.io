---
layout:     post
title:      word_cloud 初体验
subtitle:   制作 Adele 轮廓的词云图
date:       2019-01-17
author:     Nino Lau
header-img: img/tag-bg.jpg
catalog: true
tags:
    - 实验

---

> 云图前两天看见朋友圈有人转了一个爬了自己的个性签名做了一个词云图，突然发现词云图确实是一个可以很好反应程序员艺术审美的好东西。另外，[在我之前看到的一个论文](https://www.researchgate.net/publication/324509423_Detecting_Ponzi_Schemes_on_Ethereum_Towards_Healthier_Blockchain_Technology)中插了一个词云。阿黛尔是我很喜欢的一个女歌手，在此做一个Adele 轮廓的词云图，未来也许能用来送礼或者给我的文章插图。



### 工具

完成这个实验，需要用到以下几个工具：

- 用 Python 3 及其 IDE PyCharm 编写源代码
- Anaconda 用来搭建环境
- 一个抠图软件*（我用的“[搞定抠图](https://www.gaoding.com/)”）*



### 原料

完成这次实验还需要一些“原料”：

- 从 Python [wordcloud 库](https://github.com/amueller/word_cloud) 下载的 [sample 代码](https://github.com/amueller/word_cloud/blob/master/examples/simple.py)
- 网上找到 [Adele 图片](https://ws1.sinaimg.cn/large/006tNc79gy1fz9vn43m3xj31hn0u0kjl.jpg) 和 Wiki 上截取的 [Adele 简介](https://en.wikipedia.org/wiki/Adele)
- 用到了 `os` `PIL` `numpy` `matplotlib` 等 Python 包



### 环境

搭建实验用到的环境：一个配置完备 `os` `PIL` `numpy` `matplotlib` 等 Python 包的 conda env。

为什么要用 conda，用本机自带的 Python 和 pip 不就好了？

conda 可以为我们创造独立的 Python 环境，也就是说我们可以运行多个 Python 虚拟机，每个虚拟机都有独立的功能。这样可以明确分工，但同时也会造成不同环境的包重复，带来了内存负担。Anyway，conda 当然有解决办法啦，**我们这里还是创建了 conda 的 WordCloud 环境作为我们这次的词云 Python 环境。**

关于 anaconda 的安装，这里需要提醒一下：*一定要用清华镜像！一定要用清华镜像！一定要用清华镜像！因为 conda 官网的速度实在是特别慢，有时候要下载一天——镜像地址在[这里](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)，根据自己的系统下载镜像就好了。一路顺着走，就能成功安装了（注意安装路径）。*

输入 conda 出现下列东西就成功了：

```shell
$ conda
usage: conda [-h] [-V] command ...

conda is a tool for managing and deploying applications, environments and packages.

Options:

positional arguments: ...
```

成功下好了 conda 创建我们实验需要的 WordCloud 环境。

``` shell
$ conda create -n WordCloud  # 创建环境
$ conda activate WordCloud   # 激活环境
$ conda install [packages]   # 下载包，这里需要下载的包有 os, PIL, multidict, numpy, matplotlib 等等（根据需要还有的要下载scipy、jieba等等）
```

装好了之后看看我们有哪些环境和包：

``` shell
$ conda env list
# conda environments:
#
base                     /Users/nino/anaconda3
WordCloud             *  /Users/nino/anaconda3/envs/WordCloud

$ conda list
# packages in environment at /Users/nino/anaconda3/envs/WordCloud:
#
# Name                    Version                   Build  Channel
blas                      1.0                         mkl  
ca-certificates           2018.03.07                    0  
certifi                   2018.11.29               py36_0  
cycler                    0.10.0           py36hfc81398_0  
freetype                  2.9.1             h5a5313f_1004    conda-forge
intel-openmp              2019.1                      144  
jieba                     0.39                       py_1    conda-forge
jpeg                      9c                h1de35cc_1001    conda-forge
kiwisolver                1.0.1            py36h0a44026_0  
libcxx                    7.0.0                h2d50403_2    conda-forge
libffi                    3.2.1             h0a44026_1005    conda-forge
libgfortran               3.0.1                h93005f0_2  
libpng                    1.6.36            ha441bb4_1000    conda-forge
libtiff                   4.0.10            h79f4b77_1001    conda-forge
llvm-meta                 7.0.0                         0    conda-forge
matplotlib                3.0.2            py36h54f8f79_0  
mkl                       2019.1                      144  
mkl_fft                   1.0.10           py36h470a237_1    conda-forge
mkl_random                1.0.2                    py36_0    conda-forge
multidict                 4.5.2            py36h1de35cc_0  
ncurses                   6.1               h0a44026_1002    conda-forge
numpy                     1.15.4           py36hacdab7b_0  
numpy-base                1.15.4           py36h6575580_0  
olefile                   0.46                       py_0    conda-forge
openssl                   1.1.1a               h1de35cc_0  
pillow                    5.4.1           py36hbddbef0_1000    conda-forge
pip                       18.1                  py36_1000    conda-forge
pyparsing                 2.3.0                    py36_0  
python                    3.6.8                haf84260_0  
python-dateutil           2.7.5                    py36_0  
pytz                      2018.7                   py36_0  
readline                  7.0               hcfe32e1_1001    conda-forge
scipy                     1.1.0            py36h1410ff5_2  
setuptools                40.6.3                   py36_0    conda-forge
six                       1.12.0                   py36_0  
sqlite                    3.26.0            h1765d9f_1000    conda-forge
tk                        8.6.9             ha441bb4_1000    conda-forge
tornado                   5.1.1            py36h1de35cc_0  
wheel                     0.32.3                   py36_0    conda-forge
wordcloud                 1.5.0           py36h1de35cc_1000    conda-forge
xz                        5.2.4             h1de35cc_1001    conda-forge
zlib                      1.2.11            h1de35cc_1004    conda-forge
```

⚠️ jieba 属于第三方包，不能用 `conda install`直接下载，需要用一些特殊的方法。

需要首先寻找模块，找到合适的版本 **condo-forge/jieba**，然后安装：

 ```shell
$ anaconda search -t conda jieba
$ anaconda show conda-forge/jieba
$ conda install --channel https://conda.anaconda.org/conda-forge jieba
 ```

打开 Pycharm，从偏好设置中打开 project interpreter，点击 `show all`：

![](https://ws3.sinaimg.cn/large/006tNc79gy1fz9wjqufyhj317z0u044z.jpg)

找到我们刚才配置好的 `WordCloud 环境`，加入到 PyCharm。

![](https://ws3.sinaimg.cn/large/006tNc79gy1fz9wpxwrueg30rw0j2qvb.gif)

运行  [examples/simple.py](https://github.com/amueller/word_cloud/blob/master/examples/simple.py) ，如果成功运行则说明环境已经搭建好了。

当然你可能会遇到这个问题：导入其他库（如numpy，pandas），并跑了一些简单的程序都一切正常，唯独导入matplotlib 库的时候，不管怎样也画不了图。

![](https://ws4.sinaimg.cn/large/006tNc79gy1fz9x00ehivj31i80u04hq.jpg)

[有的解释](https://blog.csdn.net/Jancydc/article/details/84500912)说这是因为 Python 的版本问题，由于我已经被 Mac 自带的 Python 2 和 我下载的 Python 3 困扰多时， 我觉得不理它了，直接采用最丑陋但很简洁的办法，加两行代码在 `import matplotlib.pyplot as plt` 之前：


``` python
import matplotlib as mpl
mpl.use("TkAgg")
```

问题解决了，现在可以真正设计我们的词云图了！


### 词云图

从 Wiki 上复制一段 Adele 的描述到 text.txt ，然后用抠图软件扣了背景，**弄成白色背景**（这个很重要），取名叫 Adele.png ：

![](https://ws3.sinaimg.cn/large/006tNc79gy1fz9x0ma8f5j31hn0u0tjv.jpg)

运行以下代码：

``` python
from os import path
from PIL import Image
import numpy as np
import matplotlib as mpl
mpl.use("TkAgg")
import matplotlib.pyplot as plt
import os

from wordcloud import WordCloud, STOPWORDS, ImageColorGenerator

# get data directory (using getcwd() is needed to support running example in generated IPython notebook)
d = path.dirname(__file__) if "__file__" in locals() else os.getcwd()

# Read the whole text.
text = open(path.join(d, 'text.txt')).read()

# read the mask / color image taken from
# http://jirkavinse.deviantart.com/art/quot-Real-Life-quot-Alice-282261010
Adele_coloring = np.array(Image.open(path.join(d, "Adele.png")))
stopwords = set(STOPWORDS)
stopwords.add("said")

wc = WordCloud(background_color="white", max_words=2000, mask=Adele_coloring,
               stopwords=stopwords, max_font_size=180, min_font_size=30, random_state=42)
# generate word cloud
wc.generate(text)

# create coloring from image
image_colors = ImageColorGenerator(Adele_coloring)

# show
plt.axis("off")
plt.imshow(wc.recolor(color_func=image_colors), interpolation="bilinear")
plt.show()
```

结果还是很”漂亮“的——*Adele 看到我把她做成了大蘑菇估计得气死* 😅。。。

![](https://ws3.sinaimg.cn/large/006tNc79gy1fz9x4yc898j30po0fojta.jpg)

用另一个轮廓试了试：

![](https://ws2.sinaimg.cn/large/006tNc79gy1fz9x6m5ugmj31ti0oiwix.jpg)

当然还有别的风格的词云图，考虑到我这里只是一个“初体验”，我就不多赘述了，可以去看 [amueller](https://github.com/amueller)[/word_cloud](/word_cloud) 或者 [API 文档](https://amueller.github.io/word_cloud/auto_examples/wordcloud_cn.html)，还有很多风格很好的 samples 呢！*p.s. 我最喜欢原图片色字色渐变*

当然也有**命令行**工具，方便使用！

![](https://ws4.sinaimg.cn/large/006tNc79gy1fz9x9e5xzxj30ee0g43zi.jpg)



### 感悟

为了讨女朋友欢心，我又做了一个她形状的关于 love lyrics 的词云图：

![](https://ws1.sinaimg.cn/large/006tNc79gy1fz9xaouy85j30gg0mmjsf.jpg)

- 看起来人形状的效果真的不好，调了很多次字体大小和间隔都不是很好看，不如试试爱心形的。

- 另外，汉字词云图用到了自然语义处理的 jieba ，这个还没有尝试，日后进行体验！

