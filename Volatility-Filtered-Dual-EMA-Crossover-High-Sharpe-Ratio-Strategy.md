
> Name

Volatility-Filtered-Dual-EMA-Crossover-High-Sharpe-Ratio-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d88906700d1d5fe3c7cd.png)
![IMG](https://www.fmz.com/upload/asset/2d86a1b922d04f1883a99.png)



[trans]#### Overview
This strategy is a quantitative trading system based on dual exponential moving average (EMA) crossover and average true volatility (ATR) filtering, specifically designed for high-volatility market environments. It combines the advantages of trend following and volatility filtering to seek the best risk-adjusted returns in high IV (implied volatility) markets. The core of the strategy is to determine the trend direction through the golden cross of the fast EMA (10-day) and the slow EMA (30-day). At the same time, ATR and its related derived indicators are used to identify high-volatility market environments, ensuring that transactions are entered only when the volatility is high enough, thereby improving the Sharpe Ratio.
#### Strategy Principle
The strategy is based on a combination of two core technical indicators:
1. Trend indicators:
   - Fast exponential moving average (EMA_fast): 10-day EMA, used to capture short-term trend changes
   - Slow exponential moving average (EMA_slow): 30-day EMA, used to determine the long-term trend direction
2. Volatility indicator:
   - Average True Volatility (ATR): 14-day ATR, measuring market volatility
   - ATR mean (ATR_mean): the simple moving average of 20-day ATR, used as a volatility benchmark
   - ATR standard deviation (ATR_std): the standard deviation of the 20-day ATR, used to judge extreme fluctuation changes
The trading logic of the strategy is clear: when the short-term moving average (EMA_fast) crosses the long-term moving average (EMA_slow) upward to form a golden cross, and the current ATR is higher than its mean plus one standard deviation, a long signal is generated; when the short-term moving average crosses downwards across the long-term moving average to form a dead cross, and the same ATR conditions are met, a short signal is generated. Exit conditions are a trend reversal (the moving average crosses again) or a significant drop in volatility (ATR below the mean minus one standard deviation).
In order to control risks, the strategy sets up dynamic stop loss (entry price ±2*ATR) and take profit (entry price ±4*ATR) based on ATR, and implements dynamic position management based on account capital ratio and market volatility to ensure that the risk of a single transaction does not exceed 1%-2% of the account capital.
#### Strategic Advantages
1. High Volatility Environment Capture: The strategy ensures trading only in high volatility environments through the ATR filter, which allows it to make full use of price fluctuations during market turbulence and increase profit potential.
2. Risk-adjusted return: Combining trend tracking and volatility filtering avoids invalid trading during low volatility periods and significantly improves the ratio of return to risk, known as the Sharpe ratio.
3. Strong adaptability: The dynamic stop loss and position management mechanism based on ATR can automatically adjust according to market conditions, allowing the strategy to maintain appropriate risk control in different volatile environments.
4. Large space for parameter optimization: Multiple key parameters of the strategy (such as EMA cycle, ATR threshold, risk factors) can be optimized according to specific market conditions to improve the adaptability of the system.
5. Implementation is simple and efficient: The design based on daily data makes the strategy implementation relatively simple, with a small amount of calculation, suitable for medium-frequency traders, and does not require complex high-frequency data support.
#### Strategy Risk
1. False breakthrough risk: In a volatile market, moving average crossovers may produce false signals, leading to frequent trading and losses. The solution is to add other confirmation indicators such as trading volume or RSI to filter out false signals.
2. Impact on transaction costs: Frequent transactions in highly volatile markets may result in higher transaction costs, including commissions and slippage. It is recommended to fully consider these costs in backtesting and possibly reduce trading frequency by extending the holding time or raising the entry threshold.
3. Drawback risk: Although the strategy has a stop-loss mechanism, under extreme market conditions (such as short gaps or flash crashes), actual losses may exceed expectations. It is recommended to set the total risk limit of the account to ensure that the cumulative risk of all positions is within an acceptable range.
4. Parameter sensitivity: Strategy performance may be sensitive to parameter selection, and different market environments may require different parameter settings. The solution is to re-optimize the parameters regularly or adopt an adaptive parameter method.
5. Changes in the market environment: In a low-volatility environment or a market with an unclear trend, the strategy may have no trading signals for a long time or generate signals with poor results. You can consider switching to different strategies in different market environments.
#### Strategy optimization direction
1. Multi-level volatility filtering: Volatility indicators of multiple time frames can be introduced, such as short-term, mid-term and long-term ATR, to ensure that high volatility conditions are met on different time scales before entering the market, reducing false signals.
2. Machine learning enhancement: Machine learning algorithms can be introduced to predict trends and volatility, such as using LSTM or random forest models to predict future ATR levels and price trends to improve signal quality.
3. Adaptive parameters: Realize adaptive adjustment of EMA cycle and ATR threshold, such as automatically adjusting parameters in different market cycles to adapt to changes in market conditions and improve the robustness of the strategy.
4. Integration of sentiment indicators: Introduce market sentiment indicators such as VIX (Volatility Index), capital flow or options market data to increase the basis for confirmation of entry signals and improve signal quality.
5. Take-profit and stop-loss optimization: More complex take-profit and stop-loss strategies can be implemented, such as ATR-based trailing stop or smart take-profit based on support/resistance levels to improve the profit-loss ratio.
6. Multi-market adaptability: Expand the strategy so that it can run in multiple related markets simultaneously, using correlation and volatility differences between markets to diversify risks and increase opportunities.
7. Market environment classification: Develop a market environment identification module to adjust strategy parameters or trading logic under different market environments (trends, shocks, high volatility, low volatility, etc.) to improve the all-weather performance of the strategy.
#### Summary
The Volatility Filtered Double Moving Average Crossover High Sharpe Ratio Strategy is a quantitative trading system that combines trend following and volatility filtering to pursue high risk-adjusted returns by only trading in high volatility environments. This strategy determines the trend direction through the intersection of fast and slow moving averages, and uses ATR related indicators to ensure that the market is in a state of high volatility, thereby improving the quality of trading signals.
Dynamic stop-loss, take-profit and position management mechanisms enable strategies to effectively control risks and adapt to different market conditions. Although there are risks such as false breakthroughs, transaction costs and parameter sensitivity, the robustness and performance of the strategy are expected to be further improved by introducing optimization directions such as multi-level volatility filtering, sentiment indicator integration, and machine learning enhancement.
This is a strategic framework worth considering for quantitative traders looking to capture higher risk-adjusted returns in high-volatility markets. Before actual deployment, it is recommended to conduct sufficient historical backtesting and parameter optimization, and adjust the strategy parameters according to specific market characteristics to obtain the best trading results. || #### Overview
This strategy is a quantitative trading system based on dual Exponential Moving Average (EMA) crossovers and Average True Range (ATR) filtering, specifically designed for high volatility market environments. It combines the advantages of trend following and volatility filtering to seek optimal risk-adjusted returns in high IV (Implied Volatility) markets. The core of the strategy is to determine trend direction through golden crosses and death crosses between the fast EMA (10-day) and slow EMA (30-day), while using ATR and its related derivative indicators to identify high volatility market environments, ensuring trades are only entered when volatility is sufficiently high, thereby improving the Sharpe Ratio.
#### Strategy Principles
The strategy is based on a combination of two core technical indicators:

1. Trend Indicators:
   - Fast Exponential Moving Average (EMA_fast): 10-day EMA, used to capture short-term trend changes
   - Slow Exponential Moving Average (EMA_slow): 30-day EMA, used to determine long-term trend direction

2. Volatility Indicators:
   - Average True Range (ATR): 14-day ATR, measures market volatility
   - ATR Mean (ATR_mean): Simple moving average of 20-day ATR, serves as a volatility benchmark
   - ATR Standard Deviation (ATR_std): Standard deviation of 20-day ATR, used to judge extreme volatility changes

The strategy's trading logic is clear: when the short-term moving average (EMA_fast) crosses above the long-term moving average (EMA_slow) forming a golden cross, and the current ATR is higher than its mean plus one standard deviation, a long signal is generated; when the short-term moving average crosses below the long-term moving average forming a death cross, and the same ATR condition is met, a short signal is generated. Exit conditions are trend reversal (moving averages cross again) or a significant decrease in volatility (ATR below its mean minus one standard deviation).

To control risk, the strategy sets up dynamic stop-losses based on ATR (entry price ±2*ATR) and take-profits (entry price ±4*ATR), and implements dynamic position sizing based on account equity percentage and market volatility, ensuring that the risk of a single trade does not exceed 1%-2% of account equity.

#### Strategy Advantages
1. High Volatility Environment Capture: The strategy ensures trading only in high volatility environments through ATR filtering, enabling it to fully exploit price movements during market turbulence, enhancing profit potential.

2. Risk-Adjusted Returns: By combining trend following and volatility filtering, it avoids ineffective trades during low volatility periods, significantly improving the ratio of returns to risk, i.e., the Sharpe Ratio.

3. Strong Adaptability: The dynamic stop-loss and position sizing mechanisms based on ATR can automatically adjust according to market conditions, allowing the strategy to maintain appropriate risk control in different volatility environments.

4. Large Parameter Optimization Space: Multiple key parameters of the strategy (such as EMA periods, ATR thresholds, risk factors) can be optimized according to specific market conditions, enhancing the system's adaptability.

5. Simple and Efficient Implementation: The design based on daily data makes the strategy relatively simple to implement, with low computational requirements, suitable for medium-frequency traders without the need for complex high-frequency data support.

#### Strategy Risks
1. False Breakout Risk: In oscillating markets, moving average crossovers may generate false signals, leading to frequent trading and losses. The solution could be to add additional confirmation indicators such as volume or RSI to filter out false signals.

2. Trading Cost Impact: Frequent trading in high volatility markets may lead to higher trading costs, including commissions and slippage. It is recommended to fully consider these costs in backtesting, and possibly reduce trading frequency by extending holding periods or raising entry thresholds.

3. Drawdown Risk: Although the strategy has stop-loss mechanisms, actual losses may exceed expectations under extreme market conditions (such as gaps or flash crashes). It is advisable to set total account risk limits to ensure the cumulative risk of all positions remains within an acceptable range.

4. Parameter Sensitivity: Strategy performance may be sensitive to parameter selection, and different market environments may require different parameter settings. The solution is to regularly re-optimize parameters or adopt adaptive parameter methods.

5. Market Environment Changes: In low volatility environments or markets without clear trends, the strategy may have no trading signals for extended periods or generate suboptimal signals. Consider switching to different strategies under different market environments.

#### Strategy Optimization Directions
1. Multi-level Volatility Filtering: Introduce volatility indicators from multiple timeframes, such as short-term, medium-term, and long-term ATR, ensuring that conditions for high volatility are met across different time scales before entry, reducing false signals.

2. Machine Learning Enhancement: Incorporate machine learning algorithms to predict trends and volatility, such as using LSTM or Random Forest models to predict future ATR levels and price trends, improving signal quality.

3. Adaptive Parameters: Implement adaptive adjustment of EMA periods and ATR thresholds, such as automatically adjusting parameters in different market cycles to adapt to changing market conditions, enhancing strategy robustness.

4. Sentiment Indicator Integration: Introduce market sentiment indicators such as VIX (Volatility Index), fund flows, or options market data to provide additional confirmation for entry signals, improving signal quality.

5. Stop-Loss and Take-Profit Optimization: Implement more sophisticated stop-loss and take-profit strategies, such as ATR-based trailing stops or intelligent take-profits based on support/resistance levels, improving the profit-to-loss ratio.

6. Multi-Market Adaptability: Extend the strategy to run simultaneously across multiple related markets, leveraging inter-market correlations and volatility differences to diversify risk and increase opportunities.

7. Market Environment Classification: Develop a market environment recognition module to adjust strategy parameters or trading logic under different market environments (trending, oscillating, high volatility, low volatility, etc.), enhancing the strategy's all-weather performance.

#### Summary
The Volatility-Filtered Dual EMA Crossover High Sharpe Ratio Strategy is a quantitative trading system that combines trend following and volatility filtering, pursuing risk-adjusted high returns by trading only in high volatility environments. The strategy determines trend direction through fast and slow moving average crossovers, while using ATR-related indicators to ensure the market is in a high volatility state, thereby improving the quality of trading signals.

Dynamic stop-loss, take-profit, and position sizing mechanisms enable the strategy to effectively control risk and adapt to different market conditions. Although risks such as false breakouts, trading costs, and parameter sensitivity exist, the robustness and performance of the strategy can be further enhanced through optimization directions such as multi-level volatility filtering, sentiment indicator integration, and machine learning enhancement.

For quantitative traders seeking higher risk-adjusted returns in high volatility markets, this is a strategy framework worth considering. Before actual deployment, it is recommended to conduct thorough historical backtesting and parameter optimization, and adjust strategy parameters according to specific market characteristics to achieve optimal trading results.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-17 00:00:00
end: 2025-02-24 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=6
strategy("Aggressive Strategy for High IV Market", overlay=true)

// 用户输入
ema_fast_length = input.int(10, title="Fast EMA Length")
ema_slow_length = input.int(30, title="Slow EMA Length")
atr_length = input.int(14, title="ATR Length")
atr_mean_length = input.int(20, title="ATR Mean Length")
atr_std_length = input.int(20, title="ATR Std Dev Length")
risk_factor = input.float(0.01, title="Risk Factor")  // 单笔交易风险占账户资金的百分比
slippage = input.float(0.001, title="Slippage") // 假设滑点

// 计算EMA、ATR、均值、标准差
ema_fast = ta.ema(close, ema_fast_length)
ema_slow = ta.ema(close, ema_slow_length)
atr_value = ta.atr(atr_length)
atr_mean = ta.sma(atr_value, atr_mean_length)
atr_std = ta.stdev(atr_value, atr_std_length)

// 进场条件
long_condition = ta.crossover(ema_fast, ema_slow) and atr_value > (atr_mean + atr_std)
short_condition = ta.crossunder(ema_fast, ema_slow) and atr_value > (atr_mean + atr_std)

// 止损与止盈设置
long_stop_loss = close - 2 * atr_value  // 基于ATR的止损
long_take_profit = close + 4 * atr_value  // 基于ATR的止盈
short_stop_loss = close + 2 * atr_value  // 基于ATR的止损
short_take_profit = close - 4 * atr_value  // 基于ATR的止盈

// 动态仓位控制
position_size_calc = (strategy.equity * risk_factor) / (2 * atr_value)
position_size = math.min(position_size_calc, strategy.equity)  // 限制仓位不能大于账户总值

// 进场与出场信号
if (long_condition)
    strategy.entry("Long", strategy.long, qty=position_size)

if (short_condition)
    strategy.entry("Short", strategy.short, qty=position_size)

// 止损与止盈
strategy.exit("Take Profit/Stop Loss Long", "Long", stop=long_stop_loss, limit=long_take_profit)
strategy.exit("Take Profit/Stop Loss Short", "Short", stop=short_stop_loss, limit=short_take_profit)

// 绘制图表
plot(ema_fast, title="Fast EMA", color=color.blue, linewidth=2)
plot(ema_slow, title="Slow EMA", color=color.orange, linewidth=2)
plot(long_stop_loss, title="Long Stop Loss", color=color.red, linewidth=1, style=plot.style_line)
plot(long_take_profit, title="Long Take Profit", color=color.green, linewidth=1, style=plot.style_line)
plot(short_stop_loss, title="Short Stop Loss", color=color.red, linewidth=1, style=plot.style_line)
plot(short_take_profit, title="Short Take Profit", color=color.green, linewidth=1, style=plot.style_line)

// 显示信号
bgcolor(long_condition ? color.new(color.green, 90) : na, title="Long Signal Background")
bgcolor(short_condition ? color.new(color.red, 90) : na, title="Short Signal Background")

```

> Detail

https://www.fmz.com/strategy/483682

> Last Modified

2025-02-25 11:23:13
