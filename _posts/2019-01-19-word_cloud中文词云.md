---
layout:     post
title:      word_cloud 中文词云
subtitle:   制作冰心散文诗词云
date:       2019-01-19
author:     Nino Lau
header-img: img/post-bg-swift.jpg
catalog: true
tags:
    - 实验
    - 数据可视化

---

>  在[word_cloud 初体验](https://lovelybuggies.github.io/2019/01/17/word_cloud-%E5%88%9D%E4%BD%93%E9%AA%8C/)中，我成功地实现了英文词云（采用了原图色 mask 和按频率比重）。这次利用 jieba 和 wordcloud，将冰心的散文诗用词云表示了出来。

![WordCloud_Chinese](http://upload-images.jianshu.io/upload_images/3220531-98db43ac2bdbbe3b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 工具

我是在**OS X**上完成的进行的词云构建。为了完成这个实验，需要用到以下几个工具：

- 用 Python 3 及其 IDE PyCharm 编写源代码
- Anaconda 用来搭建环境
- 一个抠图软件*（我用的“搞定抠图”）*



### 原料

完成这次实验还需要一些“原料”：

- 从 Python [wordcloud 库](https://github.com/amueller/word_cloud) 下载的 [sample 代码](https://amueller.github.io/word_cloud/auto_examples/wordcloud_cn.html#sphx-glr-auto-examples-wordcloud-cn-py)
- 网上找到 color 图片和冰心的散文诗节选
- 除了用到了 `os` `PIL` `numpy` `matplotlib` 等 Python 包，还用到了自然语义处理的 `jieba` 包



### 环境

因为之前说过了英文环境的配置，中文环境的配置基本一样，只不过多了一个` jieba` 包。[“结巴”](https://pypi.org/project/jieba/)是一个强大的分词库，完美支持中文分词，分为三种模式：精确模式（默认）、全模式和搜索引擎模式。

#### 分词包

⚠️ jieba 属于第三方包，不能用 `conda install`直接下载，需要用一些特殊的方法。

需要首先寻找模块，找到合适的版本 **condo-forge/jieba**，然后安装：

 ```shell
$ anaconda search -t conda jieba
$ anaconda show conda-forge/jieba
$ conda install --channel https://conda.anaconda.org/conda-forge jieba
 ```

找到我们刚才配置好的 `WordCloud 环境`，加入到 PyCharm。

#### Python 版本

当然你可能会遇到这个问题：导入其他库（如numpy，pandas），并跑了一些简单的程序都一切正常，唯独导入matplotlib 库的时候，不管怎样也画不了图。

![NSInvalidArgumentException](http://upload-images.jianshu.io/upload_images/3220531-03dfe995437cc58f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[有的解释](https://blog.csdn.net/Jancydc/article/details/84500912)说这是因为 Python 的版本问题，由于我已经被 Mac 自带的 Python 2 和 我下载的 Python 3 困扰多时， 我决定不理它了，直接采用最丑陋但很简洁的办法，加两行代码在 `import matplotlib.pyplot as plt` 之前：


``` python
import matplotlib as mpl
mpl.use("TkAgg")
```

问题解决了，现在可以真正设计我们的词云图了！



### 词云

接下来我们就可以设计自己的词云了！复制冰心散文诗到 text_ch.txt，并抠图生成 heart.png 用作 mask。

![Mask](http://upload-images.jianshu.io/upload_images/3220531-4e7643400ba67b66.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 问题一：汉化字体

一开始出现了问题，发现**识别不了汉字——出现了一堆框框**：
![Font Disabled](http://upload-images.jianshu.io/upload_images/3220531-d030cde0d8b888f1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这时候需要从网上下载一些[汉化字体格式](https://github.com/adobe-fonts)*（比如simhei.ttf）*，然后在我们的代码中加入：

```python 
# the font from github: https://github.com/adobe-fonts
font = '/资源库/Fonts/Simhei.ttf'
wc = WordCloud(font_path=font).generate(cut_text)
```

这样就可以用汉化字体了！

#### 问题二：句云→词云

但是还有一个问题就是一开始生成的词云是句子，因为没有用到“结巴”分词包。

![SentensesCloud](http://upload-images.jianshu.io/upload_images/3220531-77abd601a6cded0d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

得到“句子云”的原因有2个：

- 没有使用 jieba.cut() 进行分词，txt 被直接用于 WordCloud.generate()
- 使用了 jieba.cut() 但是没有用特殊符号使得分好词的句子又变成了原始 txt 格式，这时WordCloud.generate() 只能按标点符号得到“句子云”

进行如下的分词操作处理：

```python 
# 分词
d = path.dirname(__file__) if "__file__" in locals() else os.getcwd()
text = open(path.join(d, 'text_ch.txt')).read()
cut_text = ' '.join(jieba.cut(text))
j_text = jieba.cut(text)
cut1_text = ''.join(jieba.cut(text))

# 用分词做词云 cut_text
wc = WordCloud(background_color="white", font_path=font).generate(cut_text)
```

#### 成果

通过运行下面这段代码，可以发现做出了完美的中文词云：

```python 
# -*- coding: utf-8 -*-
from os import path
import jieba
from wordcloud import WordCloud
import matplotlib as mpl
import numpy as np
from PIL import Image
mpl.use("TkAgg")
import matplotlib.pyplot as plt
from wordcloud import WordCloud, STOPWORDS, ImageColorGenerator

# 分词
d = path.dirname(__file__) if "__file__" in locals() else os.getcwd()
text = open(path.join(d, 'text_ch.txt')).read()
cut_text = ' '.join(jieba.cut(text))
j_text = jieba.cut(text)
cut1_text = ''.join(jieba.cut(text))

# the font from github: https://github.com/adobe-fonts
font = '/资源库/Fonts/Simhei.ttf'
Heart_coloring = np.array(Image.open(path.join(d, "heart.png")))
stopwords = set(STOPWORDS)
stopwords.add("said")
# 用分词做词云
wc = WordCloud(background_color="white", collocations=False, font_path=font, width=4400, height=4400, margin=2, mask=Heart_coloring,
                                    max_font_size=120, min_font_size=20).generate(cut_text)
image_colors = ImageColorGenerator(Heart_coloring)
plt.imshow(wc.recolor(color_func=image_colors), interpolation="bilinear")
#plt.imshow(wc)
plt.axis("off")
plt.show()

# 把词云保存下来
wc.to_file('show_Chinese.png')  

```

最终的词云效果如图所示：

![WordCloud_Chinese](http://upload-images.jianshu.io/upload_images/3220531-98db43ac2bdbbe3b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

美丽的词云就这样做好了！😄