# 数据获取说明

## 数据集
Freddie Mac Single Family Loan-Level Dataset
官方地址：https://www.freddiemac.com/research/datasets/sf-loanlevel-dataset

## 获取步骤
1. 在 Freddie Mac 官网免费注册账号
2. 进入 Single Family Loan-Level Dataset 页面
3. 下载 **Sample Dataset**（每年 50,000 笔贷款的简单随机抽样，含 origination + performance 两类文件）
4. 解压后放入本目录，按年份组织：

```
data/
├── 2016/
│   ├── sample_orig_2016.txt
│   └── sample_svcg_2016.txt
├── 2017/
└── ...
```

## 注意
- 原始数据为管道符（|）分隔文本，无表头，列定义见官方 User Guide
- 缺失值以 `999` / `9999` / 空白等编码表示，处理策略见主 README 第五节
- 原始数据体积较大，已加入 .gitignore，不提交本仓库
