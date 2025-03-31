#交通预测--机器学习相关代码
学校项目复刻学习
Traffic_analysis
## 一、代码整体流程

数据加载→数据清洗→可视化→建模→评估

## 二、分步解析

### 1. 数据准备阶段

```
# 加载原始数据（单元88）
traffic_df = pd.read_csv("Traffic.csv")          # 1个月的数据
traffic_two_month_df = pd.read_csv("TrafficTwoMonth.csv")  # 2个月的数据

# 合并数据集（单元92）
combined_df = pd.concat([traffic_df, traffic_two_month_df]) # 把两个表格上下拼接
combined_df['Source'] = 'OneMonth'               # 添加来源标识
```

#### 2.数据可视化

```
# 车辆数量分布（单元93）
fig = make_subplots(rows=2, cols=2, subplot_titles=("Car Counts", "Bike Counts", "Bus Counts", "Truck Counts"))
fig.add_trace(go.Histogram(x=combined_df['CarCount'], name='Car Counts'), row=1, col=1)
# ... 其他车辆类型的直方图

# 交通状况分布（单元94）
fig = px.pie(combined_df, names='Traffic Situation', title='Traffic Situation Distribution')
```

##### 2.1. 基础分布分析

实现原理 ：

- 直方图：统计各车辆类型数量分布的频次（
- 饼图：计算各类交通状况的占比
- 箱线图：展示工作日车流量的四分位分布

##### 2.2 时间序列分析

分析方法 ：

- 小时粒度：解析24小时车流量波动规律
- 周粒度：对比工作日/周末分布模式
- 长周期：捕捉月度趋势变化

#### 3.数据清洗与预处理



```
graph TD
A[原始特征] --> B{ColumnTransformer}
B --> C[数值标准化]
B --> D[类别编码]
B --> E[特征联合]
E --> F[随机森林]
F --> G[预测交通状况]
```



#### 4.特征工程与模型训练

