
> Name

Triple-Moving-Average-Momentum-Trend-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/167f5b47f7de70a374a.png)

[trans]
#### Overview
This is a triple moving average trend following strategy based on the Oliver Valez trading methodology. This strategy uses crossover signals from the 20-period, 50-period, and 200-period moving averages to identify market trends and trading opportunities. The 200-period moving average serves as the primary trend filter, and the intersection of the 20-period and 50-period moving averages is used to generate specific trading signals. The strategy has built-in risk management features, including stop-loss and take-profit settings.
#### Strategy Principle
The core logic of the strategy consists of three key levels:
1. Trend identification: Use the 200-period moving average as the trend dividing line. When the price is above the 200 EMA, an uptrend is confirmed; when the price is below the 200 EMA, a downtrend is confirmed.
2. Trading signals: In an upward trend, when the 20-period moving average crosses upwards from the 50-period moving average, a long signal is triggered; in a downward trend, when the 20-period moving average crosses downwards from the 50-period moving average, a short signal is triggered.
3. Risk control: The strategy sets a default stop loss of 2% and a take profit of 4%, and automatically closes the position when a reverse cross signal occurs.
#### Strategic Advantages
1. Multiple confirmation mechanism: Through the combined use of three moving averages, more reliable trading signals are provided.
2. Trend filtering: The trend filtering function of the 200 moving average effectively reduces the risk of false breakthroughs.
3. Strong flexibility: supports switching between SMA and EMA, and can adjust parameters according to different market characteristics.
4. Perfect risk management: built-in stop-loss and stop-profit mechanisms to protect the safety of funds.
5. Visualization effect: Visually display the trend status through background color changes.
#### Strategy Risk
1. Lagging: The moving average is essentially a lagging indicator, which may cause a slight delay in entry or exit timing.
2. Not applicable to volatile markets: During the sideways consolidation phase, frequent moving average crossovers may produce false signals.
3. Fixed Stop Loss Risk: Using a fixed percentage stop loss may not be suitable for all market environments.
4. Parameter sensitivity: Different moving average period settings may produce significantly different results.
#### Strategy optimization direction
1. Introduce trading volume analysis: you can add trading volume confirmation indicators to improve signal reliability.
2. Dynamic stop loss setting: Consider using ATR or volatility indicators to dynamically adjust stop loss positions.
3. Add trend strength filtering: Trend strength indicators such as ADX can be introduced to filter weak trend environments.
4. Optimize entry timing: combine price patterns and support and resistance levels to improve entry accuracy.
5. Add time filtering: You can set trading time windows to avoid periods of greater volatility.
#### Summary
This is a trend following strategy with complete structure and clear logic. Through the cooperation of the triple moving average, it not only ensures the accuracy of trend identification, but also provides clear trading signals. The risk management mechanism of the strategy is relatively complete, but there is still room for optimization. It is recommended that traders conduct sufficient backtesting before using it in real trading, and adjust parameter settings according to the characteristics of specific trading varieties. ||
#### Overview
This is a triple moving average trend following strategy based on Oliver Valez's trading methodology. The strategy utilizes 20-period, 50-period, and 200-period moving averages to identify market trends and trading opportunities. The 200-period MA serves as the primary trend filter, while crossovers between the 20-period and 50-period MAs generate specific trading signals. The strategy includes built-in risk management features with stop-loss and take-profit settings.

#### Strategy Principles
The core logic consists of three key aspects:
1. Trend Identification: Uses the 200-period MA as a trend boundary. When price is above the 200 MA, an uptrend is confirmed; when below, a downtrend is confirmed.
2. Trading Signals: In uptrends, long entries are triggered when the 20-period MA crosses above the 50-period MA; in downtrends, short entries occur when the 20-period MA crosses below the 50-period MA.
3. Risk Control: The strategy implements a default 2% stop-loss and 4% take-profit, with automatic position closure on reverse crossover signals.

#### Strategy Advantages
1. Multiple Confirmation System: The combination of three moving averages provides more reliable trading signals.
2. Trend Filtering: The 200 MA trend filter effectively reduces false breakout risks.
3. High Flexibility: Supports switching between SMA and EMA, with adjustable parameters for different market characteristics.
4. Comprehensive Risk Management: Built-in stop-loss and take-profit mechanisms protect capital.
5. Visual Enhancement: Trend status is intuitively displayed through background color changes.

#### Strategy Risks
1. Lag Effect: Moving averages are inherently lagging indicators, potentially causing delayed entries or exits.
2. Poor Performance in Ranging Markets: Frequent MA crossovers during consolidation periods may generate false signals.
3. Fixed Stop-Loss Risk: Using fixed percentage stops may not suit all market conditions.
4. Parameter Sensitivity: Different MA period settings can produce significantly different results.

#### Optimization Directions
1. Incorporate Volume Analysis: Add volume confirmation indicators to improve signal reliability.
2. Dynamic Stop-Loss: Consider using ATR or volatility indicators for dynamic stop-loss adjustment.
3. Add Trend Strength Filtering: Introduce ADX or other trend strength indicators to filter weak trend environments.
4. Optimize Entry Timing: Integrate price patterns and support/resistance levels for more precise entries.
5. Include Time Filtering: Set trading time windows to avoid highly volatile periods.

#### Summary
This is a well-structured trend following strategy with clear logic. The coordination of triple moving averages ensures accurate trend identification while providing definitive trading signals. While the strategy's risk management mechanisms are relatively comprehensive, there is room for optimization. Traders are advised to conduct thorough backtesting before live implementation and adjust parameters according to specific trading instrument characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-10 00:00:00
end: 2025-02-08 08:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Oliver Valez Triple MA Strategy", overlay=true, margin_long=100, margin_short=100)

// Inputs
ma20_length = input.int(20, "20-period MA Length", minval=1)
ma50_length = input.int(50, "50-period MA Length", minval=1)
ma200_length = input.int(200, "200-period MA Length", minval=1)
use_ema = input.bool(false, "Use EMA Instead of SMA")
sl_percent = input.float(2.0, "Stop Loss %", minval=0.0)
tp_percent = input.float(4.0, "Take Profit %", minval=0.0)

// Calculate MAs
ma20 = use_ema ? ta.ema(close, ma20_length) : ta.sma(close, ma20_length)
ma50 = use_ema ? ta.ema(close, ma50_length) : ta.sma(close, ma50_length)
ma200 = use_ema ? ta.ema(close, ma200_length) : ta.sma(close, ma200_length)

// Plot MAs
plot(ma20, "MA 20", color=color.new(color.blue, 0), linewidth=2)
plot(ma50, "MA 50", color=color.new(color.orange, 0), linewidth=2)
plot(ma200, "MA 200", color=color.new(color.red, 0), linewidth=2)

// Trend Filter
bullish_trend = close > ma200
bearish_trend = close < ma200

// Entry Conditions
long_condition = ta.crossover(ma20, ma50) and bullish_trend
short_condition = ta.crossunder(ma20, ma50) and bearish_trend

// Exit Conditions
exit_long = ta.crossunder(ma20, ma50)
exit_short = ta.crossover(ma20, ma50)

// Risk Management
stop_loss = strategy.position_avg_price * (1 - sl_percent/100)
take_profit = strategy.position_avg_price * (1 + tp_percent/100)

// Execute Trades
if (long_condition)
    strategy.entry("Long", strategy.long)
    strategy.exit("XL", "Long", stop=stop_loss, limit=take_profit)

if (short_condition)
    strategy.entry("Short", strategy.short)
    strategy.exit("XS", "Short", stop=stop_loss, limit=take_profit)

// Close trades on opposite signals
if (exit_long)
    strategy.close("Long")

if (exit_short)
    strategy.close("Short")

// Plot Signals
plotshape(long_condition, "Buy", shape.labelup, location.belowbar, color=color.green, text="BUY", textcolor=color.white)
plotshape(short_condition, "Sell", shape.labeldown, location.abovebar, color=color.red, text="SELL", textcolor=color.white)

// Background Color for Trend
bgcolor(bullish_trend ? color.new(color.green, 90) : bearish_trend ? color.new(color.red, 90) : na)
```

> Detail

https://www.fmz.com/strategy/481350

> Last Modified

2025-02-10 14:37:15
