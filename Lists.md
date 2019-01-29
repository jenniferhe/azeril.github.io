---
layout: page
title: "Past Projects"
description: 
header-img: "img/1.jpg"
---





## 餐厅食品质量安全监测预测 **Restaurant Inspection Outcome Forcast**

It is a coursework we did following full data science pipeline: 

**Business Understanding**: forecast restaurant inspection outcomes in order to offer insight to NYC health department, i.e. whether they should give priority to inspect certain restaurant. 

**Data Preparation**: Crawled, selected and feature engineered geological, time and syntax data from various sources

![Data](https://i.imgur.com/s27f3q9.png)

![Data2](https://i.imgur.com/qMWhTnt.png)

![Data3](https://i.imgur.com/s771ydx.png)

**Modeling and Evaluation**:  Explored multiple models and delivered a [report](https://github.com/jenniferhe/Restaurant_Inspection_Forcasting/blob/master/New%20York%20City%20Restaurant%20Inspection%20Analysis%20and%20Forecasting.pdf)  listed the outstanding model results including Random Forest, LightGBM and Ensemble method. The best AUC score we reached was 0.74 which is around the same level to the highest scores we seen on the web

![Data4](https://i.imgur.com/5ee60fD.png)

![Data5](https://i.imgur.com/vr0Fp1q.png)

[See more on my Github page](https://github.com/jenniferhe/Restaurant_Inspection_Forcasting)

## 鸟类图片图像识别 Bird Picture Image Recognition Project

利用Python Theano/Lasagne库实现的基于神经网络的图像识别项目

Applying Machinge Learning Techniques to Bird Species Classification

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

Cooperated with multiple teams to design an internal logging system that supported securely logging, indexing, searching, storing, visualizing and analyzing of billions of confidential log records stored across multiple data centers 

![ELK project](http://1.bp.blogspot.com/-TevQjxdj-zw/VBKq7O7T9wI/AAAAAAAAAjk/gy16GLD6Rpg/s1600/elk.png)
(Due to company policy, the Github page is not available)


## 在线即时餐厅搜索项目 Webbased online resestaurant search project
利用Algolia提供的搜索云服务，导入湾区餐厅数据，通过实时系统建立了索引，完成高时效性的立即查询

Use Algolia's search as a service to build a small prototype that able to provide instantaneous, multi-platform and type-tolerant search on local restaurants.



<img src="https://raw.githubusercontent.com/jenniferhe/algolia_final/master/test1.gif" width="600" height="400" />

[Github page](https://github.com/jenniferhe/algolia_final)



# LinkedIn_Hackday_2016

这是一个24小时的hackthon项目，智能礼物推荐网站。它是基于node.js + express + bootstrap framework实现的。由用户提交送礼对象的Twitter页面或Linkedin页面或Pinterest页面，然后页面后台进行文字抓取，然后根据文字频率找出相关的amazon礼物页面

Won Linkedin Intern Hackday Top Finalists with an online gift recommendation service that offer gift suggestions from Amazon based on people social media information 

  <img src="https://raw.githubusercontent.com/jenniferhe/LinkedinHackDay_GiftRecommendation/master/Screen%20Shot%202018-02-27%20at%2011.26.52%20PM.png" width="600"/>