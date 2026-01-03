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
