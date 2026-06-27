# VeloQuant
**IndexPulse** is an interactive, quantitative trading dashboard that extracts the complete asset composition of any major ETF to construct institutional-grade momentum strategies.

### 🛠️ Strategic Architecture

* **Full-Basket Extraction:** Programmatically bypasses web-scraping paywalls and dynamic JavaScript pagination limits, pulling 100% of the underlying components for any fund—including all 503 stocks in SPY, 101 in QQQ, or specialized thematic sector pools like PHO and XLK.
* **Vectorized Analytical Engine:** Eliminates single-threaded Python looping bottlenecks entirely. It evaluates cross-sectional risk-adjusted performance rankings across hundreds of stocks simultaneously using optimized C-arrays:

$$\text{Score} = \frac{\text{Total Return}}{\text{Rolling Volatility} \times \sqrt{252} + 1e^{-8}}$$

* **Walk-Forward Simulation:** Models multi-year rebalancing regimes over user-defined horizons, accurately penalizing returns for transaction friction ($0.05\%$) and executing trades using next-day opening price boundaries.
* **Granular Verification Logs:** Provides a clean paper trail for institutional auditing by rendering scrollable ledgers of the exact extracted asset pool and historical monthly ranking changes.
* **Active Trading Signals Desk:** Concludes by feeding raw historical backtests directly into a real-time signal monitor, outputting the specific tickers and precise portfolio allocation weights to execute on a brokerage account for the current month.
