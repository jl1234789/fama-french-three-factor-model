# Fama-French 模型学习笔记（Python）

- reference: https://github.com/nkuguanrui/FamaFrenchThreeFacorModel/

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

### 1.计算账面市值比 (Book-to-Market, BM) 

- 1. 计算账面价值 (BV)

每股账面价值乘以总股数：

$$\
BV = \text{bookvaluepershare} \times \text{shares}
\$$

- $$BV\$$：公司总账面价值  
- $$\\text{bookvaluepershare}\$$：每股账面价值  
- $$\\text{shares}\$$：总股本数

---

- 2. 计算市值 (Market Capitalization)

股票价格乘以总股数：

$$\
\text{MktCap} = \text{price} \times \text{shares}
\$$

- $$\\text{MktCap}\$$：公司市值  
- $$\\text{price}\$$：股票价格  
- $$\\text{shares}\$$：总股本数

---

- 3. 计算账面市值比 (BM)

$$\
BM = \frac{BV}{\text{MktCap}}
\$$

- $$BM\$$：账面市值比（Book-to-Market Ratio）  
- 用于构造 **价值因子 HML**




