### X实验 结构图


```flow
st=>start: 内容抓取装置
e=>end: 数据存储/检索
op=>operation: 识别
op2=>operation: 特征提取
cond=>condition: 确认？

st->op->cond->op2->e
cond(yes)->op2
cond(no)->op
```

### 遇到问题

- [ ] 内容获取器
	- [ ] 爬虫？
- [ ] 词向量过拟合
	- [ ] 如何拆解内容（识别）


#### 下载器/爬虫/内容获取

> 内容下载器
> >> 目标选择-> 时间 ， 地点 ， 事件 ， 人[?] 新闻
> > 内容提取
> > 内容清洗

1. 全部新闻
2. 压缩图片
3. link


#### 识别器
---

```flow
st=>start: 拆内容
op1=>operation: 从数据库中找相似
op2=>operation: 抓标签，相似，属性
e=>end: 特征提取

st->op1->op2->e
```

神经网络训练内容的分类（无监督）

> 词向量的条件下

```py
step1: 提取内容|提取描述（来源描述，html，docx）
step2: 拆分内容
```


#### 特征提取器

> 词向量
> 词属性

```flow
st0=>start: 从识别器
st=>operation: 调整初始化词向量
e=>end: 数据存储/检索
op4=>operation: 词属性，格（基于web，知识库）
cc=>condition: 是否更新词向量
cond2=>condition: 更新
op2=>operation: 更抽象组合
cond=>condition: 确认？


st0->cc->op2->e
cc(yes)->st->e
cc(no)->op2


```

```flow
st0=>start: 从识别器
st=>operation: 调整初始化词向量
e=>end: 数据存储/检索
op4=>operation: 词属性，格（基于web，知识库）
cc=>condition: 是否更新词向量
cond1=>condition: 是否属性歧义
op6=>operation: 判断

st0->op4->cond1->e
cond1(yes)->op6->e
cond1(no)->e

```




#### 数据存储

> wikibase 知识库

结果的可视化

Wiki search ：
> 文章

WDQS： wiki data query service

> 地图， 表，等的内容可视化

支持**API**

 * python
 * bash
 * rest



### X实验 结构图


```flow
st=>start: 内容抓取装置
e=>end: 数据存储/检索
op=>operation: 识别
op2=>operation: 特征提取
cond=>condition: 确认？

st->op->cond->op2->e
cond(yes)->op2
cond(no)->op
```

### 遇到问题

- [ ] 内容获取器
	- [ ] 爬虫？
- [ ] 词向量过拟合
	- [ ] 如何拆解内容（识别）


#### 下载器/爬虫/内容获取

> 内容下载器
> >> 目标选择-> 时间 ， 地点 ， 事件 ， 人[?] 新闻
> > 内容提取
> > 内容清洗

1. 全部新闻
2. 压缩图片
3. link


#### 识别器
---

```flow
st=>start: 拆内容
op1=>operation: 从数据库中找相似
op2=>operation: 抓标签，相似，属性
e=>end: 特征提取

st->op1->op2->e
```

#### 特征提取器

> 词向量

```flow
st0=>start: 从识别器
st=>operation: 调整初始化词向量
e=>end: 数据存储/检索
cc=>condition: 是否更新词向量
cond2=>condition: 更新
op2=>operation: 更抽象组合
cond=>condition: 确认？


st0->cc->op2->e
cc(yes)->st->e
cc(no)->op2

```




#### 数据存储

> wikibase 知识库

结果的可视化

Wiki search ：
> 文章

WDQS： wiki data query service

> 地图， 表，等的内容可视化

支持**API**

 * python
 * bash
 * rest







## wikibase-docker

This repo contains images needed to setup wikibase and a query service using Docker.

### Issue tracking

We use [Phabricator to track
issues](https://phabricator.wikimedia.org/maniphest/task/edit/form/1/?projects=wikibase-containers). See the [list of current issues](https://phabricator.wikimedia.org/maniphest/?project=wikibase-containers&statuses=open&group=none&order=newest#R).

### Images

Image name               | Description   | README
------------------------ | ------------- | ----------
[`wikibase/wikibase`](https://store.docker.com/community/images/wikibase/wikibase) | MediaWiki with the Wikibase extension| [README](https://github.com/wmde/wikibase-docker/blob/master/wikibase/README.md)
[`wikibase/wdqs`](https://store.docker.com/community/images/wikibase/wdqs) | Blazegraph SPARQL query service backend | [README](https://github.com/wmde/wikibase-docker/blob/master/wdqs/README.md)
[`wikibase/wdqs-proxy`](https://store.docker.com/community/images/wikibase/wdqs-proxy) | Proxy to make the query service READONLY and enforce query timeouts | [README](https://github.com/wmde/wikibase-docker/blob/master/wdqs-proxy/README.md)
[`wikibase/wdqs-frontend`](https://store.docker.com/community/images/wikibase/wdqs-frontend) | UI for the SPARQL query service | [README](https://github.com/wmde/wikibase-docker/blob/master/wdqs-frontend/README.md)

### Docker compose example

This repo contains an example docker compose setup for wikibase.

[README](https://github.com/wmde/wikibase-docker/blob/master/README-compose.md)
