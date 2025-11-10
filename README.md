*Quantitative Finance Project – University of Texas at Austin*

---

### 📍 Overview

We developed a flexible, data-driven portfolio optimization tool using **CRSP stock return data**. The project explored **mean-variance optimization (MVO)**, **Ledoit-Wolf shrinkage**, and the difference between **in-sample (IS)** and **out-of-sample (OOS)** performance. Our tool allowed dynamic user inputs and produced **efficient frontier visualizations**, **risk-return metrics**, and **exportable Excel reports**.

---

### 🎯 Project Goals

- Build a **reusable portfolio optimizer** with support for modern and classical techniques
- Test how well optimized portfolios **generalize to future market data**
- Use **real-world CRSP returns** to ensure institutional realism
- Evaluate estimation risk, shrinkage, shorting constraints, and rebalancing tradeoffs

---

### 🧠 Data Science & Machine Learning Methods Used

| Category | Techniques Applied |
| --- | --- |
| **Data Cleaning** | CRSP monthly return merging, delisting return handling, outlier filtering |
| **Feature Engineering** | Custom return matrices (IS/OOS), Ledoit-Wolf shrinkage of covariance matrix |
| **Optimization Models** | Global Minimum Variance (GMV), Efficient Portfolio, Optimal Risky Portfolio (ORP), Quadratic Programming (QP-ORP) |
| **Statistical Tools** | Sample vs shrunk covariance, shrinkage tuning, Frobenius norm deltas |
| **Evaluation Metrics** | Expected return, standard deviation, Sharpe ratio (monthly & annualized) |
| **Generalization Testing** | Out-of-sample performance vs. in-sample overfitting |
| **Software Engineering** | Excel report builder, interactive weight input validation, permno-based ticker mapping |

---

### 📊 Modeling Pipeline

1. **User Inputs**: Tickers, date ranges (IS/OOS), and weights (equal or user-specified)
2. **Return Matrix Construction**: Monthly return matrices built from WRDS CRSP with validation
3. **Covariance Estimation**:
    - Sample Covariance
    - Ledoit-Wolf Shrinkage (reduces noise, improves stability)
4. **Optimization**:
    - GMV (lowest variance)
    - Efficient Portfolio (target return match)
    - ORP (tangency portfolio)
    - QP-ORP (Scipy-constrained optimizer)
5. **Backtesting**:
    - Evaluate all portfolios IS and OOS
    - Sharpe ratios dropped significantly OOS due to overfitting
6. **Reporting**:
    - Efficient frontiers, CAL lines, summary tables
    - Excel report with formatted sheets, plots, and user inputs

---

### 📈 Results & Insights

| Model | Sharpe (IS) | Sharpe (OOS) | Key Takeaway |
| --- | --- | --- | --- |
| **ORP** | 0.437 | 0.153 | Performs best in-sample but collapses out-of-sample |
| **GMV** | 0.261 | 0.094 | Consistent low-risk but underwhelming return |
| **Efficient** | 0.428 | 0.153 | Good in-sample match, unstable OOS |
| **QP-ORP** | 0.437 | 0.153 | Matches ORP with shorting constraints |
| **Ledoit-Wolf** | Slightly improved Sharpe ratios OOS, more stable weights |  |  |

---

### 🔍 Key Technical Lessons Learned

- **Estimation Risk** is real: portfolios that look optimal in-sample often perform poorly out-of-sample
- **Shrinkage** improves robustness but doesn’t eliminate instability
- **Constraints Matter**: imposing bounds (e.g., long-only) drastically changes allocation
- **Scalable Design**: writing generalized, user-driven code (with validation, error handling, formatting) is as important as the models
- **Backtest ≠ Live Performance**: emphasized the importance of out-of-sample evaluation in applied finance

---

### 🧠 What I Gained

- Deepened my understanding of **mean-variance optimization** theory and its practical shortcomings
- Applied **scikit-learn-style thinking** (train/test split, generalization error) in a financial context
- Implemented **matrix math + optimization from scratch** using NumPy, SciPy, and pandas
- Learned the importance of **robust engineering** for financial applications (e.g., ticker/permno mapping, data cleaning, modularized scripts)
- Gained insight into how **shrinkage, regularization, and constraints** shape real-world portfolio behavior

---

### 📦 Deliverables

- 🧾 Excel report with:
    - In-Sample & Out-of-Sample returns
    - Sharpe ratios (monthly & annualized)
    - Efficient frontiers & CAL overlays
    - Auto-formatted tabs (inputs, weights, metrics, returns, plots)
- 📈 Frontier Plots and Capital Allocation Line (CAL)
- 💻 Reusable Python scripts with parameterized inputs

---

### 📚 Sample Ticker Portfolio (10-stock test)

- `DE`, `LMT`, `DIS`, `MCD`, `WMT`, `NKE`, `LUV`, `AMD`, `AMZN`, `TSLA`
- IS Period: 2014–2020 | OOS Period: 2021–2023
- In-sample Sharpe Ratios consistently **overestimated** out-of-sample performance

---

### 💡 Impact

This project mirrors real-world portfolio modeling workflows and bridges the gap between **quant theory** and **practical implementation**. It highlighted the risks of **overfitting in financial ML**, and taught us to be skeptical of models that perform too well on historical data.
