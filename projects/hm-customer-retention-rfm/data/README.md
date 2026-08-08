# 数据获取说明

## 数据集
H&M Personalized Fashion Recommendations
地址：https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations/data

## 文件
| 文件 | 内容 | 规模 |
|---|---|---|
| transactions_train.csv | 交易记录（2018-09 至 2020-09） | 约 3.7GB，三千余万行 |
| articles.csv | 商品属性（品类、颜色、价位等） | 10.5 万行 |
| customers.csv | 客户属性（年龄、会员状态等） | 137 万行 |

## 注意
- 交易表体积大，读取时必须分块（`pd.read_csv(chunksize=...)`）并只保留所需列
- 原始数据体积较大，已加入 .gitignore，不提交本仓库
- 图片目录（images/）本项目不使用，无需下载
