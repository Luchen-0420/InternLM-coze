# 1. 教程简介

## 1.1 涵盖功能

1. 微信内一键收藏至飞书多维表格并自动整理分类
2. 智能匹配，从已收藏中推荐最相关内容
3. 可生成阅读卡片分享

## 1.2 设计思路

## 1.3 插件整理

```商城内插件```

1. 飞书多维表格插件
   
```自建插件```

1. InternLM调用插件
2. jina调用插件    （商城内有现成jina插件，教程还是会重新自建jina插件，带大家熟悉下流程）

# 2. 准备工作

## 2.1 设计飞书表格元数据

```链接```：文章、视频链接

```摘要```：AI自动生成摘要

```来源```：可自定义，如B站、小红书等

```分类```：可自定义，如AI、软件、硬件、产品设计等

```状态```：已阅读、未阅读

```收集日期```：自动填入日期

```收藏原因```：用户自输入

```阅读日期```：标记完"已阅读"后，自动填入日期

```灵感记录```：用户自输入阅读完的灵感记录（读后感）

![1726640439008](https://github.com/user-attachments/assets/8ab4f48f-d968-4714-b989-9aa4eef87261)


## 2.2 新建bot

![1726641681662](https://github.com/user-attachments/assets/7346093e-386d-42dc-9481-ee39386ddce3)


## 2.3 创建浦语API Token

登录

![1726645539860](https://github.com/user-attachments/assets/3abfa68c-1864-4b6d-856f-e9c0237f5e22)


# 3. 搭建整理入库工作流

![image](https://github.com/user-attachments/assets/25bd9f09-b49c-4423-9bac-9c0217f332fe)


## 3.1 新建article_arrange工作流

![image](https://github.com/user-attachments/assets/a516bafd-d3c9-4c2b-be63-6bf54a5f3fff)

![1726642271289](https://github.com/user-attachments/assets/33307810-4794-4c2d-a023-8e43d3ac23ea)

## 3.2 对输入的url进行处理

有些平台的分享链接会包含其他符号，例如小红书、B站等。这里第一步要先对输入的url进行```https://```开头链接提取。

```
86 【为了这1️⃣5️⃣个机位，我特意飞了趟大连‼️ - 猪甜菜的旅行手记 | 小红书 - 你的生活指南】 😆 SmN73Z1FIahYCR8 😆 https://www.xiaohongshu.com/discovery/item/66e306730000000027004c9f?source=webshare&xsec_token=ABvDkzrNj9V0qrp5F0givNOHph1ZJyNLzGweDxy2AQvt4=&xsec_source=pc_share
```

点击添加"插件"，选择```InternLM_api```插件

![1726645170089](https://github.com/user-attachments/assets/618625f7-720c-45a7-80d7-0dc0a96b2b60)


# 2.3 搭建内容推荐工作流

# 2.4 

# 2.5 接入微信公众号
