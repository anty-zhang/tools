
[TOC]

# 介绍

FAISS 是 Facebook AI 研究团队开源的针对聚类和相似性搜索库，它包含一种在任意大小的向量集合中搜索直到可能不适合在 RAM 中的新算法。它还包含用于评估和参数调整的支持代码。由于公司服务器没有连接外网，无法使用conda安装，所以直接源码安装，githup网站下载地址：

https://github.com/facebookresearch/faiss

安装方法参考安装说明：

https://github.com/facebookresearch/faiss/blob/master/INSTALL.md

faiss安装可以使用make工具或者cmake工具。make可以生成c++接口和python接口， cmake编译只能生成c++接口

# install

## Aanconda install

```bash
pip install faiss-cpu==1.6.0
```


