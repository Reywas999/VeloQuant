# VeloQuant
**VeloQuant** is an interactive, quantitative trading dashboard that extracts the complete asset composition of any major ETF to construct institutional-grade momentum strategies.

### 🛠️ Strategic Architecture

* **Full-Basket Extraction:** Programmatically bypasses web-scraping paywalls and dynamic JavaScript pagination limits, pulling 100% of the underlying components for any fund—including all 503 stocks in SPY, 101 in QQQ, or specialized thematic sector pools like PHO and XLK.
* **Vectorized Analytical Engine:** Eliminates single-threaded Python looping bottlenecks entirely. It evaluates cross-sectional risk-adjusted performance rankings across hundreds of stocks simultaneously using optimized C-arrays:

$$\text{Score} = \frac{\text{Total Return}}{\text{Rolling Volatility} \times \sqrt{252} + 1e^{-8}}$$

* **Walk-Forward Simulation:** Models multi-year rebalancing regimes over user-defined horizons, accurately penalizing returns for transaction friction ($0.05\%$) and executing trades using next-day opening price boundaries.
* **Granular Verification Logs:** Provides a clean paper trail for institutional auditing by rendering scrollable ledgers of the exact extracted asset pool and historical monthly ranking changes.
* **Active Trading Signals Desk:** Concludes by feeding raw historical backtests directly into a real-time signal monitor, outputting the specific tickers and precise portfolio allocation weights to execute on a brokerage account for the current month.
<img width="511" height="712" alt="Screenshot 2026-06-26 180600" src="https://github.com/user-attachments/assets/c2fd72a6-5a60-443a-a188-7bc6a5fb6d08" />

## 🔄 UPDATE: Parametric Optimization & Deep-Research Engine (06/27/2026)

The repository has been expanded to include a high-performance, non-UI quantitative engine designed to run native parametric sweeps directly within terminal or Jupyter Notebook environments. While the original interactive dashboard application acts as a point-in-time visual backtester, this programmatic optimization suite acts as a hyper-parameter search engine to discover optimal portfolio settings.

## 🛠️ Optimization Engine Architecture

The standalone script introduces a customizable **Weighted Objective Matrix Scoring System**. Instead of evaluating metrics in isolation, it applies a multi-criteria penalty function where every single portfolio permutation is ranked against the field. Users define exact percentage priorities for what matters most to their mandate:

$$\text{Composite Score} = (w_{\text{Return}} \times \text{Rank}_{\text{Return}}) + (w_{\text{Drawdown}} \times \text{Rank}_{\text{Drawdown}}) + (w_{\text{Sharpe}} \times \text{Rank}_{\text{Sharpe}})$$

*The asset configuration that minimizes this combined weighted rank floats instantly to the top of your leaderboard.*

### Key Quantitative Features Added:
1. **Granular Win/Loss Distributions:** Calculates the precise count of positive and negative trading days, alongside the strict mathematical expectation of average wins versus average losses.
2. **Opposing-Window Weekly Stress Testing:** Evaluates a rolling 5-trading-day window to isolate the absolute 5 worst and 5 best weeks for both strategies, forcing the opposing asset allocation to reveal its performance during those identical cross-sections of market stress.
3. **Dedicated Category Winners:** Automatically isolates the raw top-performing variables for each core metric into independent dataframes (`engine.df_best_return`, `engine.df_best_drawdown`, `engine.df_best_sharpe`).
4. **Data Verification Audits:** Prints an explicit count verification directly to the console logging exactly how many underlying equities were parsed, successfully processed, and evaluated.
<img width="822" height="963" alt="Screenshot 2026-06-27 180811" src="https://github.com/user-attachments/assets/1616bf49-7c4e-4403-8cb9-48e16b807578" />
<img width="820" height="1139" alt="Screenshot 2026-06-27 180834" src="https://github.com/user-attachments/assets/3854db53-0913-4725-95f5-a903a6f561ac" />


## 🦅 Active Execution Desk: actionable_dynamic_etf.py

Once your hyper-parameters have been mathematically finalized by the optimizer, the **`actionable_dynamic_etf.py`** script acts as your live operational trading desk. It removes manual tape-reading by fetching real-time market data, extracting the target index structure, and calculating exact transactional share quantities customized to your personal investment capital.

### ⚠️ Critical Processing Order Dependency
The live tracking desk operates entirely on a decoupled architecture. To run successful execution scripts, **`Parametric_Optimization` must be executed first**.

The optimizer locks in the winning $N$ choice and weighted percentage parameters to a localized shared cache vector (`Dynamic_etf_optimized_variables.csv`), which this execution desk reads upon initialization.

---

## 🛠️ Dynamic Rebalancing & Execution Features

* **Instant Order Ticket Generation:** Input your current target capital balance (e.g., `$25,000.00`) directly at the top of the file. The engine instantly converts momentum scores into precise cash distributions and decimal share counts based on up-to-the-minute market pricing.
* **Chronological Ledger Logging:** Every time a rebalance routine is processed, the system timestamps your exact position slip into a distinct historical archive named in an explicit `MMDDYYYY_Reallocations.csv` data format.
* **Cross-Month Variance Analytics:** On rebalance day, the execution script automatically scans your workspace directory for the prior calendar month's output ledger (e.g., if today is June, it matches against any `05XX2026_Reallocations.csv` files). 
* **Prior-Rank Sorted Adjustment Slips:** It automatically runs a cross-sectional index comparison between your old assets and new allocations, instantly printing an optimized, itemized trade ticket sorted cleanly by your **Prior Position Rank**.

### 📊 Understanding the Rebalance Output Ledger
The variance calculation engine categorizes portfolio shifts into four explicit, step-by-step brokerage actions:

1. **🔴 FULL LIQUIDATION:** The asset has completely dropped out of the top risk-adjusted momentum clusters and must be fully sold out of your account.
2. **🟢 NEW POSITION ENTRY:** A stock has surged to leadership rank over the trailing quarter, triggering a brand-new cash buy signal.
3. **⚡ INCREASE POSITION:** The stock's rank or risk-profile has strengthened, requiring you to buy a specific positive fractional share delta ($+$).
4. **📉 TRIM POSITION:** The asset remains in the momentum basket but has shifted to a lower allocation tier, requiring you to shave off a precise fraction of shares ($-$).


<img width="728" height="976" alt="Screenshot 2026-06-27 184519" src="https://github.com/user-attachments/assets/c0b74f1d-c89d-4b51-ab21-0684972583aa" />

