
> Name

Dual-EMA-Retest-Reversal-Strategy-A-Trend-Following-System-Based-on-EMA-Crossovers-and-Retest-Tolerance
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d880164818d481822fb4.png)
![IMG](https://www.fmz.com/upload/asset/2d8aaa37d8ea97578ad51.png)



[trans]
#### Overview
The double moving average pullback reversal trading strategy is a trend following system based on the exponential moving average (EMA). Its core concept is "not to chase every moving average crossover, but to wait for the market to pull back to the fast EMA line for confirmation before entering the market." This strategy combines the moving average cross signal and price callback confirmation mechanism in technical analysis. By setting reasonable backtest tolerance, risk-reward ratio and daily trading limit, it conducts high-probability transactions at the callback point after the trend changes. The strategy uses the 200-period and 800-period EMAs as benchmarks. When the fast EMA (200 period) crosses the slow EMA (800 period) to form a long signal, wait for the price to pull back to near the fast EMA (default tolerance 0.2%) to buy; otherwise, wait for the pullback to go short after forming a short signal. At the same time, each transaction is set with percentage-based stop loss and take profit levels, and the risk-reward ratio defaults to 4:1 to ensure the rationality of fund management.
#### Strategy Principle
The core principles of this strategy are based on the following technical analysis concepts:
1. **Moving Average Cross Signal Identification**: The strategy uses the 200-period and 800-period EMA to determine the overall trend direction of the market. When the fast EMA (200) crosses the slow EMA (800), the system recognizes that the bullish trend has begun; when the fast EMA crosses below the slow EMA, the system recognizes that the short trend has begun. This stage only determines the trend and does not trigger transactions.
2. **Trend State Tracking**: The strategy continuously tracks the current trend state through Boolean variables (in_bullish_trend and in_bearish_trend) to ensure that transactions are only conducted in the confirmed trend direction.
3. **Calibration confirmation mechanism**: Different from the traditional moving average crossover strategy, this strategy does not enter the market directly at the crossover point, but waits for the price to pull back to near the fast EMA. Specifically, when the deviation percentage between the price and the fast EMA is less than the preset backtest tolerance (default 0.2%), the system considers the callback confirmation to be complete, and the trading signal is triggered at this time.
4. **Risk Control Mechanism**: The strategy sets a fixed proportion of stop loss (default 0.5%) and a take-profit level based on the risk-reward ratio (default 4:1) for each transaction. At the same time, excessive trading is avoided by limiting the maximum number of transactions per day (default 2).
5. **Date Switch Reset**: The strategy resets the trade counter at the beginning of daily trading, ensuring that trading frequency limits are calculated on a daily basis.
#### Strategic Advantages
By deeply analyzing the code, this strategy has the following significant advantages:
1. **Trading after trend confirmation**: The strategy only considers entry after the moving average crosses to confirm the trend direction, avoiding losses caused by frequent trading in a consolidating market.
2. **Callback entry improves winning rate**: By waiting for the price to pull back to the key support/resistance level (fast EMA) before entering the market, the probability of success of the transaction is increased and the risk of entering the market when the price is overextended is avoided.
3. **Clear Risk Management**: Each transaction has predefined stop loss and take profit levels, and the risk-reward ratio is set to 4:1, ensuring the possibility of long-term profits even if the winning rate is not high.
4. **Over-Trading Protection**: Prevent over-trading in volatile markets by limiting the maximum number of transactions per day, which helps reduce transaction costs and improve overall strategy stability.
5. **Visualized trading signals**: The strategy uses labels and background color changes to visually display trading signals and position status, which facilitates backtest analysis and real-time monitoring.
6. **Parameter Adjustability**: All key parameters such as EMA period, backtest tolerance, risk-reward ratio, stop loss ratio and maximum daily number of transactions can be adjusted through the input box, making the strategy highly adaptable.
#### Strategy Risk
Although this strategy is well designed, there are still the following potential risks:
1. **Lagging identification of trend reversal**: Due to the use of longer-period EMAs (200 and 800), the strategy may have a significant lag in identifying trend reversals, resulting in missing part of the market in the early stages of the trend. Solution: You can consider combining shorter-period indicators to assist judgment, or adjusting the EMA period according to market characteristics.
2. **False breakthrough risk**: In a volatile market, EMA crossovers may frequently produce false breakthroughs, resulting in false signals. Solution: You can add a cross confirmation mechanism, such as requiring the price to maintain the trend direction for a certain period of time after the cross, or increasing transaction volume confirmation.
3. **Frequent triggering under narrow range fluctuations**: In a low volatility environment, the price may frequently fluctuate near the EMA, and then leave quickly after meeting the backtest conditions, forming an invalid signal. Solution: Consider adding a volatility filter, or increasing backtest tolerance requirements in low volatility environments.
4. **Fixed stop loss risk**: The strategy uses a fixed percentage stop loss and does not take into account differences in market volatility, which may cause the stop loss to be too small and trigger frequently in highly volatile markets. Solution: You can consider using ATR (average true range) to dynamically adjust the stop loss level.
5. **Reliance on a single technical indicator**: The strategy mainly relies on the EMA indicator and lacks multi-dimensional market analysis. Solution: Consider combining other types of indicators (such as momentum indicators, volatility indicators) for signal confirmation.
#### Strategy optimization direction
Based on the above analysis, the strategy can be optimized in the following directions:
1. **Dynamic parameter adjustment**: Change the fixed backtest tolerance and stop loss ratio to dynamic adjustment based on market volatility (such as ATR) to adapt to different market environments. The reason for this is that market volatility characteristics change over time and fixed parameters may not apply to all market conditions.
2. **Multiple time frame analysis**: Increase the judgment of the trend of higher time frames, only trade in the direction of the overall trend, and avoid reverse trading in the consolidation trend. This optimization can improve signal quality and reduce the risk of contrarian trading.
3. **Trading volume confirmation**: Add trading volume confirmation conditions when the entry signal is generated, such as requiring a heavy-volume support/resistance breakthrough at the callback point. Trading volume is the driving force behind price changes, and combined with trading volume analysis can improve signal effectiveness.
4. **Dynamic adjustment of profit-loss ratio**: Dynamically adjust the risk-return ratio based on market fluctuation characteristics and historical price structure, instead of using a fixed 4:1 ratio. This allows the strategy to better adapt to different stages and characteristics of the market.
5. **Add filter conditions**: Add the market trend strength indicator (such as ADX) as a filter to only enable the strategy in strong trending markets. This avoids too many false signals in weak trends or choppy markets.
6. **Partial Profit Locking Mechanism**: Add batch profit taking function, lock part of the profit when the price reaches a certain profit level, and continue to hold the remaining part to track the trend. This mechanism balances the needs of short-term profit taking with long-term trend following.
7. **Backtest time period optimization**: Add trading period filtering to avoid high volatility periods before the market opens and closes, or focus on specific efficient trading periods. Market efficiency and characteristics vary greatly in different time periods. Choosing the time period trading that best suits the strategy logic can improve overall performance.
#### Summary
The Double Moving Average Pullback Reversal trading strategy creates a complete trend following trading system by combining moving average crossover signals and price pullback confirmation mechanisms. This strategy not only contains clear entry and exit logic, but also has good fund management and risk control mechanisms. Its core advantage lies in the concept of "waiting for confirmation". By avoiding chasing the moving average cross signal directly, but waiting for the price to pull back to the key technical position before entering the market, it can increase the probability of successful transaction.
However, the strategy still has limitations such as reliance on long-period EMA, single technical indicator judgment, and fixed parameter settings. By introducing optimization measures such as dynamic parameter adjustment, multi-time frame analysis, transaction volume confirmation, and trend strength filtering, the adaptability and robustness of the strategy can be further improved. Especially in market environments with high volatility or unclear trends, these optimization measures will play a greater role.
Ultimately, this strategy represents a trading idea that balances aggressiveness and stability, and is suitable for traders who have a certain risk tolerance and pursue medium- and long-term stable returns. Through reasonable setting of parameters and continuous strategy optimization, it can maintain relatively stable performance in various market environments.
 ||
#### Overview
The Dual EMA Retest Reversal Strategy is a trend following system based on Exponential Moving Averages (EMA), with the core philosophy of "not chasing every EMA cross, but waiting for the market to retest the fast EMA for confirmation before entering." This strategy combines technical analysis concepts of EMA crossovers with price retest confirmation mechanisms. By setting reasonable retest tolerances, risk-reward ratios, and daily trade limits, it executes high-probability trades at retracement points after trend The strategy uses 200-period and 800-period EMAs as benchmarks. When the fast EMA (200-period) crosses above the slow EMA (800-period) forming a bullish signal, it waits for price to pull back to near the fast EMA (default tolerance 0.2%) before buying; conversely, it waits for pullbacks to short after bearish signals. Each trade is equipped with percentage-based stop-loss and changes. Take-profit levels, with a default risk-reward ratio of 4:1, ensure sound money management.
#### Strategy Principles
The core principles of this strategy are built upon several technical analysis concepts:

1. **EMA Crossover Signal Identification**: The strategy uses 200-period and 800-period EMAs to determine the overall market trend direction. When the fast EMA (200) crosses above the slow EMA (800), the system identifies this as the beginning of a bullish trend; when the fast EMA crosses below the slow EMA, the system identifies this as the beginning of a bearish trend. This stage only determines the trend and does not trigger trades.

2. **Trend State Tracking**: The strategy continuously tracks the current trend state through boolean variables (in_bullish_trend and in_bearish_trend), ensuring trades are only executed in the confirmed trend direction.

3. **Retest Confirmation Mechanism**: Unlike traditional EMA crossover strategies, this strategy does not enter directly at the crossover point but waits for the price to pull back to near the fast EMA. Specifically, when the percentage deviation between price and fast EMA is less than the preset retest tolerance (default 0.2%), the system considers the retest confirmation complete and triggers a trading signal.

4. **Risk Control Mechanism**: The strategy sets a fixed percentage stop-loss (default 0.5%) and a risk-reward ratio-based take-profit level (default 4:1) for each trade. At the same time, it limits the maximum number of trades per day (default 2) to avoid overtrading.

5. **Daily Reset**: The strategy resets the trade counter at the beginning of each trading day, ensuring the trade frequency limit is calculated on a daily basis.

#### Strategy Advantages
Through in-depth code analysis, this strategy has the following significant advantages:

1. **Trading After Trend Confirmation**: The strategy only considers entry after EMA crossovers confirm the trend direction, avoiding losses from frequent trading in consolidating markets.

2. **Retest Entry Improves Win Rate**: By waiting for price to pull back to key support/resistance levels (fast EMA) before entering, it improves the probability of successful trades and avoids the risk of entering when price is overextended.

3. **Clear Risk Management**: Each trade has predefined stop-loss and take-profit levels with a risk-reward ratio set at 4:1, ensuring the possibility of long-term profitability even with a moderate win rate.

4. **Overtrading Protection**: Through daily maximum trade limits, it prevents excessive trading in volatile markets, which helps reduce trading costs and enhance overall strategy stability.

5. **Visualization of Trading Signals**: The strategy uses labels and background color changes to intuitively display trading signals and position status, facilitating backtest analysis and real-time monitoring.

6. **Parameter Adjustability**: All key parameters such as EMA periods, retest tolerance, risk-reward ratio, stop-loss percentage, and maximum daily trades are adjustable through input fields, giving the strategy strong adaptability.

#### Strategy Risks
Despite its reasonable design, the strategy still has the following potential risks:

1. **Delayed Trend Reversal Recognition**: Due to the use of longer-period EMAs (200 and 800), the strategy may experience significant lag in identifying trend reversals, causing missed opportunities in the early stages of trends. Solution: Consider incorporating shorter-period indicators for auxiliary judgment, or adjust EMA periods according to market characteristics.

2. **False Breakout Risk**: In oscillating markets, EMA crossovers may frequently produce false breakouts, leading to erroneous signals. Solution: Add crossover confirmation mechanisms, such as requiring price to maintain a certain trend direction after crossing, or add volume confirmation.

3. **Frequent Triggers in Narrow Range Fluctuations**: In low-volatility environments, price may frequently fluctuate near the EMA, meeting retest conditions but quickly departing, forming invalid signals. Solution: Consider adding volatility filters, or increase retest tolerance requirements in low-volatility environments.

4. **Fixed Stop-Loss Risk**: The strategy uses fixed percentage stop-losses without considering market volatility differences, potentially leading to too-small stops that trigger frequently in high-volatility markets. Solution: Consider using ATR (Average True Range) to dynamically adjust stop-loss levels.

5. **Single Technical Indicator Dependency**: The strategy primarily relies on EMA indicators, lacking multi-dimensional market analysis. Solution: Consider combining other types of indicators (such as momentum indicators, volatility indicators) for signal confirmation.

#### Strategy Optimization Directions
Based on the above analysis, the strategy can be optimized in the following directions:

1. **Dynamic Parameter Adjustment**: Change fixed retest tolerance and stop-loss percentages to be dynamically adjusted based on market volatility (such as ATR) to adapt to different market environments. This is done because market volatility characteristics change over time, and fixed parameters may not be suitable for all market conditions.

2. **Multi-Timeframe Analysis**: Add assessment of higher timeframe trends, only trading in the direction of the overall trend to avoid counter-trend trading in consolidating major trends. This optimization can improve signal quality and reduce the risk of counter-trend trading.

3. **Volume Confirmation**: Add volume confirmation conditions when generating entry signals, such as requiring volume support/resistance breakouts at retest points. Volume is the source of price movement dynamics, and incorporating volume analysis can improve signal effectiveness.

4. **Dynamic Profit-Loss Ratio Adjustment**: Dynamically adjust the risk-reward ratio based on market volatility characteristics and historical price structure, rather than using a fixed 4:1 ratio. This allows the strategy to better adapt to different market phases and characteristics.

5. **Add Filtering Conditions**: Incorporate market trend strength indicators (such as ADX) as filters, only activating the strategy in strong trend markets. This can avoid generating too many false signals in weak trend or oscillating markets.

6. **Partial Profit Locking Mechanism**: Add partial profit-taking functionality, locking in some profits when price reaches certain profit levels while continuing to hold the remainder to track the trend. This mechanism can balance short-term profit-taking and long-term trend-following needs.

7. **Backtest Time Period Optimization**: Add trading session filters to avoid high-volatility periods around market open and close, or focus on specific high-efficiency trading sessions. Different sessions have significant differences in market efficiency and characteristics; selecting the most suitable periods for the strategy logic can improve overall performance.

#### Summary
The Dual EMA Retest Reversal Strategy creates a complete trend-following trading system by combining EMA crossover signals with price retest confirmation mechanisms. The strategy not only includes clear entry and exit logic but also features sound money management and risk control mechanisms. Its core advantage lies in the "wait for confirmation" philosophy, improving the probability of successful trades by avoiding direct pursuit of EMA crossover signals and instead waiting for price to pull back to key technical levels before entering.

However, the strategy still has limitations such as dependence on long-period EMAs, single technical indicator judgment, and fixed parameter settings. By introducing dynamic parameter adjustments, multi-timeframe analysis, volume confirmation, and trend strength filtering, the strategy's adaptability and robustness can be further enhanced. These optimization measures will be particularly effective in highly volatile or trend-unclear market environments.

Ultimately, this strategy represents a trading approach that balances aggression with stability, suitable for traders with certain risk tolerance who pursue medium to long-term stable returns. Through reasonable parameter settings and continuous strategy optimization, it can maintain relatively stable performance in various market environments.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-04-13 00:00:00
end: 2025-04-15 10:00:00
period: 2m
basePeriod: 2m
exchanges: [{"eid":"Futures_Binance","currency":"TRX_USD"}]
*/

//@version=6
strategy("200/500 EMA Retest Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=1)

// INPUTS
ema_fast_length = input.int(200, title="Fast EMA Length")
ema_slow_length = input.int(500, title="Slow EMA Length")
retest_tolerance = input.float(0.002, title="Retest Tolerance (%)") // 0.2% by default
risk_reward_ratio = input.float(4.0, title="Risk-Reward Ratio (TP:SL)")
stop_loss_perc = input.float(0.005, title="Stop Loss % (e.g., 0.5%)") // 0.5% default
max_trades_per_day = input.int(2, title="Max Trades Per Day")

// EMA CALCULATIONS
ema_fast = ta.ema(close, ema_fast_length)
ema_slow = ta.ema(close, ema_slow_length)

// PLOT EMAs
plot(ema_fast, color=color.blue)
plot(ema_slow, color=color.orange)

// CROSS DETECTION
bullish_cross = ta.crossover(ema_fast, ema_slow)
bearish_cross = ta.crossunder(ema_fast, ema_slow)

// STATE TRACKING
var bool in_bullish_trend = false
var bool in_bearish_trend = false
var int trades_today = 0

if ta.change(time("D")) != 0

    trades_today := 0

if bullish_cross
    in_bullish_trend := true
    in_bearish_trend := false

if bearish_cross
    in_bullish_trend := false
    in_bearish_trend := true

// RETEST CONDITION
bullish_retest = in_bullish_trend and (math.abs(close - ema_fast) / ema_fast <= retest_tolerance)
bearish_retest = in_bearish_trend and (math.abs(close - ema_fast) / ema_fast <= retest_tolerance)

// ENTRIES WITH SL/TP AND TRADE LIMIT
if bullish_retest and trades_today < max_trades_per_day
    strategy.entry("Long", strategy.long)
    strategy.exit("Long TP/SL", from_entry="Long", stop=close * (1 - stop_loss_perc), limit=close * (1 + stop_loss_perc * risk_reward_ratio))
    label.new(bar_index, low, "BUY", color=color.green, style=label.style_label_up, textcolor=color.white, size=size.small)
    trades_today += 1

if bearish_retest and trades_today < max_trades_per_day
    strategy.entry("Short", strategy.short)
    strategy.exit("Short TP/SL", from_entry="Short", stop=close * (1 + stop_loss_perc), limit=close * (1 - stop_loss_perc * risk_reward_ratio))
    label.new(bar_index, high, "SELL", color=color.red, style=label.style_label_down, textcolor=color.white, size=size.small)
    trades_today += 1

// BACKGROUND COLOR WHEN IN POSITION
bgcolor(strategy.position_size > 0 ? color.new(color.green, 90) : na)
bgcolor(strategy.position_size < 0 ? color.new(color.red, 90) : na)

// ALERTS
if bullish_retest
    alert("BUY Retest Triggered!", alert.freq_once_per_bar)

if bearish_retest
    alert("SELL Retest Triggered!", alert.freq_once_per_bar)

```

> Detail

https://www.fmz.com/strategy/491506

> Last Modified

2025-04-21 15:58:18
