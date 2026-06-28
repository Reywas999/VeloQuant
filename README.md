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
