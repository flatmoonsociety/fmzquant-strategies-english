
> Name

Exponential-Moving-Average-Candle-Stop-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d908a8ae46c428e44daa.png)
![IMG](https://www.fmz.com/upload/asset/2d94edf4ec0247ec232b9.png)



[trans]#### Overview
The Exponential Moving Average Candlestick Stop Trading Strategy is a quantitative trading system based on candlestick patterns and moving average trend confirmation. This strategy works primarily by identifying specific candlestick patterns (i.e. "candlestick stop" signals) as entry points, while incorporating EMA (exponential moving average) crosses to confirm the overall market trend, and using dynamic support and resistance levels to identify market breakouts. This strategy adopts a strict risk management mechanism, including preset stop-loss positions and a take-profit strategy based on risk-reward ratio, to ensure that the risk of each transaction is controlled.
#### Strategy Principle
The core principle of this strategy is to identify specific candlestick patterns in the market, which often represent the possibility of a short-term market reversal. The strategy works as follows:
1. Trend judgment: Judge the market trend by comparing the relative positions of EMA20 and EMA90. When EMA20 is above EMA90, it is judged to be an upward trend; when EMA20 is below EMA90, it is judged to be a downtrend.
2. Candlestick Stop Signal Recognition:
   - Candlestick stop signals in an uptrend require: the length of the lower shadow is at least 0.8 times that of the real body, the upper shadow is smaller than the real body, and the closing price is higher than the opening price (positive line).
   - Candlestick stop signals in a downtrend require: the length of the upper shadow line is at least 0.8 times that of the real body, the lower shadow line is smaller than the real body, and the closing price is lower than the opening price (yin line).
3. Breakout Detection: Identify market breakouts by comparing the current closing price to support/resistance levels (calculated based on 30 periods of lowest/highest prices).
4. Entry conditions: When the market is in a specific trend and is not in a breakthrough state, if a candlestick stop signal occurs, the strategy will enter the market according to the preset risk parameters (2.5% risk per transaction).
5. Stop loss setting: For long positions, the stop loss is set to 2.5% below the entry price; for short positions, the stop loss is set to 2.5% above the entry price.
6. Take-profit conditions: a combination of profit percentage and risk-reward ratio. Long positions require a profit of at least 7% and a risk-reward ratio of no less than 3; short positions require a profit of at least 6% and a risk-reward ratio of no less than 3.
#### Strategic Advantages
1. Clear entry and exit signals: Provide clear trading signals through specific candlestick patterns and moving average trends, reducing the emotional impact of subjective judgments.
2. Comprehensive trend confirmation mechanism: Use EMA indicators of multiple time periods to confirm market trends and improve the reliability of trading signals.
3. Dynamic support and resistance identification: Dynamic support and resistance levels calculated using rolling windows enable the strategy to adapt to different market stages.
4. Strict risk management: preset risk parameters (2.5% risk for each transaction) and profit-taking conditions based on risk-return ratio to ensure the rationality of fund management.
5. Differentiated long and short trading standards: Set different entry conditions and profit targets for long and short transactions to adapt to the asymmetric characteristics of the market.
6. Dynamic position calculation: Automatically calculate the appropriate position size based on the stop loss distance to ensure risk consistency for each transaction.
#### Strategy Risk
1. Indicator lag: EMA, as a lagging indicator, may provide delayed signals in a rapidly changing market, resulting in poor entry timing.
2. False breakthrough risk: The market may have false breakthroughs, resulting in false signals. The solution is to introduce volume confirmation or increase the breakout confirmation period.
3. Sensitivity adjustment challenges: The parameters of the candlestick stop signal (such as the ratio of shadow line to real body) need to be adjusted according to different markets and cycles. Being too sensitive may lead to over-trading, while being too strict may lead to missed opportunities.
4. Trend conversion period risk: During the trend conversion period, the strategy may produce a series of losing transactions. The solution is to increase the trend strength filter or trade less frequently when the trend is unclear.
5. Unsuitability of fixed stop loss distance: Using the same percentage stop loss (2.5%) for all trades may not adapt to different market volatility. Consider using volatility-based dynamic stop distance.
6. Limitations of RSI filter conditions: Using RSI filter only for short trades may result in unbalanced trading frequency. Consider introducing a similar filtering mechanism for long transactions or optimizing the current RSI parameters.
#### Strategy optimization direction
1. Volatility adaptive parameters: Introduce volatility indicators (such as ATR) to dynamically adjust the shadow ratio requirements and stop loss distance of candlestick stop signals, so that the strategy can better adapt to different market conditions.
2. Multi-time frame confirmation: Re-introduce trend confirmation in higher time frames (such as 1-hour chart) to improve the reliability of trading signals and reduce the impact of false signals.
3. Optimization of entry timing: Optimize entry timing and improve transaction success rate by adding additional filtering conditions (such as trend strength indicators, trading volume confirmation).
4. Partial take-profit mechanism: Introduce a segmented take-profit mechanism, and after reaching a certain profit, move the stop loss to the cost price or lock in part of the profit to better balance risks and rewards.
5. Backtest cycle expansion: Conduct more comprehensive backtests under different market cycles and conditions to verify the robustness and adaptability of the strategy.
6. Machine learning optimization: Use machine learning methods to automatically optimize strategy parameters and find the optimal parameter combination for a specific market.
7. Transaction frequency control: Introduce transaction limit or cooling period mechanism to avoid excessive trading under adverse market conditions.
#### Summary
The Exponential Moving Average Candlestick Stop Trading Strategy is a quantitative trading system that combines technical analysis and risk management to generate trading signals by identifying specific candlestick patterns and combining them with trend confirmations. The main advantages of this strategy are clear trading rules and strict risk control mechanisms, making trading decisions more systematic and disciplined. However, as any technical analysis strategy, it also faces challenges such as indicator lag and adaptability to market changes.
By introducing improvements such as volatility adaptive parameters, multi-time frame confirmation and optimized entry timing, this strategy has the potential to achieve more stable performance in different market environments. In particular, applying machine learning methods to parameter optimization may greatly improve the adaptability and overall performance of the strategy. Regardless, before actually deploying this strategy, it is recommended to conduct adequate backtesting and forward testing to verify its performance under actual market conditions. ||
#### Overview
The Exponential Moving Average Candle Stop Trading Strategy is a quantitative trading system based on candlestick patterns and moving average trend confirmation. This strategy primarily identifies specific candlestick formations (known as "candle stop" signals) as entry points, while using EMA (Exponential Moving Average) crossovers to confirm the overall market trend and dynamic support and resistance levels to identify market breakouts. The strategy implements strict risk management mechanisms, including preset stop-loss positions and a take-profit strategy based on risk-reward ratios, ensuring controlled risk for each trade.

#### Strategy Principles
The core principle of this strategy is to identify specific candlestick patterns in the market that typically represent the possibility of short-term market reversals. The operational mechanism of the strategy is as follows:

1. Trend Determination: Market trends are determined by comparing the relative positions of EMA20 and EMA90. When EMA20 is above EMA90, an uptrend is identified; when EMA20 is below EMA90, a downtrend is identified.

2. Candle Stop Signal Identification:
   - In an uptrend, a candle stop signal requires: a lower shadow length at least 0.8 times the body, an upper shadow smaller than the body, and a closing price higher than the opening price (bullish candle).
   - In a downtrend, a candle stop signal requires: an upper shadow length at least 0.8 times the body, a lower shadow smaller than the body, and a closing price lower than the opening price (bearish candle).

3. Breakout Detection: Market breakouts are identified by comparing the current closing price with support/resistance levels (calculated based on the lowest/highest prices over 30 periods).

4. Entry Conditions: When the market is in a specific trend and not in a breakout state, if a candle stop signal appears, the strategy enters positions according to preset risk parameters (2.5% risk per trade).

5. Stop-Loss Setting: For long positions, the stop-loss is set at 2.5% below the entry price; for short positions, the stop-loss is set at 2.5% above the entry price.

6. Take-Profit Conditions: Based on a combination of profit percentage and risk-reward ratio conditions. Long positions require at least 7% profit and a risk-reward ratio of no less than 3; short positions require at least 6% profit and a risk-reward ratio of no less than 3.

#### Strategy Advantages
1. Clear Entry and Exit Signals: Provides clear trading signals through specific candlestick patterns and moving average trends, reducing the emotional impact of subjective judgment.

2. Comprehensive Trend Confirmation Mechanism: Uses EMA indicators from multiple time periods to confirm market trends, improving the reliability of trading signals.

3. Dynamic Support and Resistance Identification: Uses dynamically calculated support and resistance levels with a rolling window, allowing the strategy to adapt to different market phases.

4. Strict Risk Management: Preset risk parameters (2.5% risk per trade) and take-profit conditions based on risk-reward ratios ensure reasonable capital management.

5. Differentiated Long and Short Trading Standards: Sets different entry conditions and profit targets for long and short trades, adapting to the asymmetric characteristics of markets.

6. Dynamic Position Sizing: Automatically calculates appropriate position sizes based on stop-loss distance, ensuring consistent risk for each trade.

#### Strategy Risks
1. Indicator Lag: EMA, as a lagging indicator, may provide delayed signals in rapidly changing markets, resulting in suboptimal entry timing.

2. False Breakout Risk: Markets may exhibit false breakout phenomena, leading to erroneous signals. The solution is to introduce volume confirmation or increase breakout confirmation periods.

3. Sensitivity Adjustment Challenges: The parameters of candle stop signals (such as the ratio of shadows to body) need to be adjusted according to different markets and periods. Being too sensitive may lead to overtrading, while being too strict may miss opportunities.

4. Trend Transition Period Risk: During trend transition periods, the strategy may generate a series of losing trades. The solution is to add trend strength filters or reduce trading frequency when trends are unclear.

5. Inflexibility of Fixed Stop-Loss Distance: Using the same percentage stop-loss (2.5%) for all trades may not adapt to different market volatilities. Consider using volatility-based dynamic stop-loss distances.

6. Limitations of RSI Filter Conditions: Using RSI filtering only for short trades may create an imbalanced trading frequency. Consider introducing similar filtering mechanisms for long trades or optimizing current RSI parameters.

#### Strategy Optimization Directions
1. Volatility Adaptive Parameters: Introduce volatility indicators (such as ATR) to dynamically adjust the shadow ratio requirements of candle stop signals and stop-loss distances, allowing the strategy to better adapt to different market conditions.

2. Multi-Timeframe Confirmation: Reintroduce higher timeframe (such as 1-hour chart) trend confirmation to improve the reliability of trading signals and reduce the impact of false signals.

3. Entry Timing Optimization: Optimize entry timing by adding additional filtering conditions (such as trend strength indicators, volume confirmation) to increase trade success rates.

4. Partial Take-Profit Mechanism: Introduce a tiered take-profit mechanism that moves the stop-loss to breakeven or locks in partial profits after reaching certain profit levels, better balancing risk and reward.

5. Backtesting Period Extension: Conduct more comprehensive backtesting under different market cycles and conditions to verify the strategy's robustness and adaptability.

6. Machine Learning Optimization: Use machine learning methods to automatically optimize strategy parameters and find the optimal parameter combinations for specific markets.

7. Trading Frequency Control: Introduce trade count limits or cooling-off period mechanisms to avoid overtrading under unfavorable market conditions.

#### Summary
The Exponential Moving Average Candle Stop Trading Strategy is a quantitative trading system combining technical analysis and risk management, generating trading signals by identifying specific candlestick patterns and confirming trends. The main advantages of this strategy lie in its clear trading rules and strict risk control mechanisms, making trading decisions more systematic and disciplined. However, as with any technical analysis strategy, it also faces challenges such as indicator lag and adaptability to market changes.

By introducing improvements such as volatility adaptive parameters, multi-timeframe confirmation, and optimizing entry timing, this strategy has the potential to achieve more stable performance across different market environments. Particularly, applying machine learning methods to parameter optimization could significantly enhance the strategy's adaptability and overall performance. Regardless, before deploying this strategy in practice, it is recommended to conduct thorough backtesting and forward testing to verify its performance under actual market conditions.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-26 00:00:00
end: 2025-02-23 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=6
strategy("Advanced Candle Stop Strategy Backtest - Tuned v9 - Max Trades", overlay=true)

// --- EMA Variables ---
ema5_length = 5
ema20_length = 20
ema90_length = 90

ema5 = ta.ema(close, ema5_length)
ema20 = ta.ema(close, ema20_length)
ema90 = ta.ema(close, ema90_length)

// --- Support, Resistance, and Volume Calculation ---
lookback_support_resistance = 30
support_level = ta.lowest(low, lookback_support_resistance)
resistance_level = ta.highest(high, lookback_support_resistance)

// --- Volume Condition for Short (Removed) ---
avg_volume_lookback = 20
avg_volume = ta.sma(volume, avg_volume_lookback)

// --- RSI Condition for Short (Removed) ---
rsi_length = 14
rsi_overbought = 70
rsi = ta.rsi(close, rsi_length)


// --- Candle Stop Function ---
is_candle_stop(trend) =>
    body = math.abs(close - open)
    upper_shadow = high - math.max(open, close)
    lower_shadow = math.min(open, close) - low

    if trend == "up"
        lower_shadow >= 0.8 * body and upper_shadow < body and close > open // Shadow ratio reduced to 0.8 for longs
    else if trend == "down"
        upper_shadow >= 0.8 * body and lower_shadow < body and close < open // Shadow ratio reduced to 0.8 for shorts - EMA5 and Volume conditions removed
    else
        false

// --- Trend Determination (only 15m, no 1H confirmation) ---
trend = ema20 > ema90 ? "up" : ema20 < ema90 ? "down" : "neutral"
final_trend = trend  // حذف تأیید با تایم‌فریم 1H

// --- Breakout Detection ---
var bool breakout_detected = false
if final_trend == "up" and close > resistance_level
    breakout_detected := true
    alert("شکست صعودی تشخیص داده شد! منتظر پولبک ?", alert.freq_once_per_bar)
else if final_trend == "down" and close < support_level
    breakout_detected := true
    alert("شکست نزولی تشخیص داده شد! منتظر پولبک ?", alert.freq_once_per_bar)

// --- Entry and Exit Conditions ---
var float position = 0.0
var float entry_price = 0.0
var float stop_loss_price = na
var bool take_profit_long = false  // Declare take_profit_long
var bool stop_loss_hit_long = false // Declare stop_loss_hit_long
var bool take_profit_short = false // Declare take_profit_short
var bool stop_loss_hit_short = false // Declare stop_loss_hit_short
risk_per_trade_percent = 2.5  // افزایش ریسک به 2.5٪ برای موقعیت‌های بیشتر


if not breakout_detected
    if position == 0 and is_candle_stop(final_trend)
        risk_amount_usd = strategy.initial_capital * (risk_per_trade_percent / 100)
        if final_trend == "up"
            stop_loss_price := close * 0.975 // Stop loss at 2.5% below entry for longs
            if (close - stop_loss_price) != 0
                position_size_usd = risk_amount_usd / (close - stop_loss_price)
                amount = position_size_usd / close
                strategy.entry("Long", strategy.long, qty=amount)
                position := amount
                entry_price := close
        else if final_trend == "down"
            stop_loss_price := close * 1.025 // Stop loss at 2.5% above entry for shorts
            if (stop_loss_price - close) != 0
                position_size_usd = risk_amount_usd / (stop_loss_price - close)
                amount = position_size_usd / close
                if rsi >= rsi_overbought // RSI condition for short entry - No Change, still using RSI but not enforcing it for now - Consider removing RSI condition as well for max trades
                    strategy.entry("Short", strategy.short, qty=amount)
                    position := amount
                    entry_price := close

if position > 0
    profit_percent_long = (close - entry_price) / entry_price * 100
    profit_percent_short = (entry_price - close) / entry_price * 100
    loss_percent_long = (entry_price - close) / entry_price * 100
    loss_percent_short = (close - entry_price) / entry_price * 100

    risk_reward_long = loss_percent_long != 0 ? profit_percent_long / loss_percent_long : (profit_percent_long != 0 ? 99999 : 0)
    risk_reward_short = loss_percent_short != 0 ? profit_percent_short / loss_percent_short : (profit_percent_short != 0 ? 99999 : 0)


    take_profit_long := profit_percent_long >= 7 and risk_reward_long >= 3
    stop_loss_hit_long := close <= stop_loss_price
    take_profit_short := profit_percent_short >= 6 and risk_reward_short >= 3 // Reduced Take Profit for Shorts to 6% - No Change
    stop_loss_hit_short := close >= stop_loss_price

    if (final_trend == "up" and (take_profit_long or stop_loss_hit_long)) or (final_trend == "down" and (take_profit_short or stop_loss_hit_short))
        if final_trend == "up"
            strategy.close("Long")
        else
            strategy.close("Short")
        position := 0
        entry_price := 0.0
        breakout_detected := false

// --- Plotting EMAs and Support/Resistance Levels ---
plot(ema5, color=color.blue, title="EMA5")
plot(ema20, color=color.red, title="EMA20")
plot(ema90, color=color.green, title="EMA90")
plot(resistance_level, color=color.orange, style=plot.style_line, title="Resistance")
plot(support_level, color=color.orange, style=plot.style_line, title="Support")
```

> Detail

https://www.fmz.com/strategy/483680

> Last Modified

2025-02-25 11:11:35
