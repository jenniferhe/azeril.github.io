---
layout: page
title: "Past Projects"
description: 
header-img: "img/2.jpg"
---

## 鸟类图片图像识别 Bird Picture Image Recognition Project
利用Python Theano/Lasagne库实现的基于神经网络的图像识别项目
![Sample Bird Images](http://i.imgur.com/R2rdTBe.png)
[Github page](https://github.com/jenniferhe/Bird_Recognition_Lasagne)

最佳结果出自sx3_ffc_b32.py， 因为它不但在时间花费上比较短（CPU和GPU两种情况都考虑时）且最终达到90%以上的准确率

#### Network architecture:

| Layer Structure | Specifics   |
| --------------- | ----------- |
| Input           | 3x128x128   |
| conv3-32        | Pad=1       |
| pool2           | Stride=2    |
| conv3-64        | Pad=1       |
| pool2           | Stride=2    |
| conv3-128       | Pad=1       |
| pool2           | Stride=2    |
| FC:512          | Dropout 50% |
| FC:512          | Dropout 50% |
| Softmax         | 9-way       |

After running with stratified random data splits for ~100 runs, mean validation accuracy was found to be 92.9%. 

![Graph of Data](http://i.imgur.com/GeW4UUM.png)

***

## 领英广告数据可视化系统 Linkedin Marketing Solution Private Logging System
在领英广告组负责管理广告数据库并支持公司内部和第三方对广告的使用，使用Couchbase, ElasticSearch, Restli filters, Kibana等技术建立可视化日志文件，支持跨数据中心的加密存储、搜索、可视化和分析，帮助提升组内员工的效率
![ELK project](http://1.bp.blogspot.com/-TevQjxdj-zw/VBKq7O7T9wI/AAAAAAAAAjk/gy16GLD6Rpg/s1600/elk.png)
(Due to company policy, the Github page is not available)


## 在线即时餐厅搜索项目 Webbased online resestaurant search project
利用Algolia提供的搜索云服务，导入湾区餐厅数据，通过实时系统建立了索引，完成高时效性的立即查询

<img src="https://raw.githubusercontent.com/jenniferhe/algolia_final/master/test1.gif" width="600" height="400" />

[Github page](https://github.com/jenniferhe/algolia_final)



# LinkedIn_Hackday_2016

这是一个24小时的hackthon项目，智能礼物推荐网站。它是基于node.js + express + bootstrap framework实现的。由用户提交送礼对象的Twitter页面或Linkedin页面或Pinterest页面，然后页面后台进行文字抓取，然后根据文字频率找出相关的amazon礼物页面

  <img src="https://raw.githubusercontent.com/jenniferhe/LinkedinHackDay_GiftRecommendation/master/misty.gif" width="600" height="400" />