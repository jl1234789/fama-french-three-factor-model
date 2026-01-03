# Fama-French 模型学习笔记（Python）

- reference: https://github.com/nkuguanrui/FamaFrenchThreeFacorModel/
- 月度
# 数据
借用清洗好的数据集

- price.csv
  > PERMNO: 股票唯一永久 ID 整数（CRSP 内部标识）<br>
  > date: 交易日期 YYYY-MM-DD <br>
  > PRCT收盘价美元，负值表示 Bid 价 <br>
  > SHROUT流通股数千股（×1000 = 实际股数） <br>
  > EXCHCD:交易所代码 1=NYSE, 2=AMEX, 3=NASDAQ <br>

- value.csv
  > LPERMNO:Compustat 公司对应的 CRSP 股票 PERMNO, 连接财务数据与市场数据 <br>
  > datadate: 财报截止日期, 时间对齐，避免未来函数 <br>
  > bkvlps: 每股账面价值（美元), 计算 B/M，构建价值因子（HML）<br>

- rf.csv
  > date: 月份
  > rf： 每月无风险收益率（CRSP计算）


# Fama–French 三因子模型公式

## 模型公式

超额收益公式：

$$
R_{i,t} - R_{f,t} = \alpha_i + \beta_{MKT,i} (R_{m,t} - R_{f,t}) + \beta_{SMB,i} \cdot SMB_t + \beta_{HML,i} \cdot HML_t + \varepsilon_{i,t}
$$

### 说明

- $$\(R_{i,t}\)$$：股票 \(i\) 在时间 \(t\) 的收益率  
- $$\(R_{f,t}\)$$：无风险利率  
- $$\(R_{m,t}\)$$：市场组合收益率  
- $$\(MKT_t = R_{m,t} - R_{f,t}\)$$：市场超额收益  
- $$\(SMB_t\)$$：规模因子（Small Minus Big）  
- $$\(HML_t\)$$：价值因子（High Minus Low）  
- $$\(\beta_{MKT,i}\)$$：股票对市场因子的暴露  
- $$\(\beta_{SMB,i}\)$$：股票对规模因子的暴露  
- $$\(\beta_{HML,i}\)$$：股票对价值因子的暴露  
- $$\(\alpha_i\)$$：异常收益（无法被因子解释的部分）  
- $$\(\varepsilon_{i,t}\)$$：随机误差项


## 步骤

## 数据
- 处理 rf 表格，形成月度数据
- 处理 price 数据
- 处理 value 数据
- 清洗三张表 NaN、不合理值
- shares(price) 保留年度数据
- values 保留年度数据
- 合并股票股价和市值数据
- 计算 bm（年度）
- 计算市值
- 计算股票收益率
- 转化国债收益率单位
- 计算因变量超额收益率（因变量）
- bm 年份值向前 shift 一年（会计年度 t 的 BM → t+1 可用）
- 论文的 “July t – June t+1” 规则（BM Ratio）
- 合并股票和 BM 表
- FF 模型 6 月时间点规则（“年”不是时间点）
- 时间颗粒度变月
- exchange_code_x / y

## 因子计算
- 分组
- BM 分组（账面价值分三组）
- 市值规模分 2 组
- 交叉分组筛选股票池
- 组合的市值加权月收益
- 根据论文重命名标签
- 计算 SMB 因子
- 计算 HML 因子
- 计算 RM_RF
- 整合 SMB, HML, RM_RF 三个因子
- Plot 并分析因子历史行为与经济含义
- 3 个因子的相关性分析

## 因变量计算
- 理解因变量的计算过程

## 模型回归
- 回归分析





