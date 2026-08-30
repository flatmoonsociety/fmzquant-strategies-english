
> Name

Crossover-Strategy-of-Moving-Average-Lines-and-Resistance-Level-Breakout
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c03a19729a6000745e.png)
 [trans]
## Overview
This strategy comprehensively uses double moving average crossover technology and pressure level breakthrough technology to set buy signals and sell signals to achieve automatic trading. When the short-term moving average breaks through the mid-term moving average from bottom to top, and the stock price breaks through the pressure level, a buy signal is generated; when the stock price rises by 15%, a stop profit is set, and when the stock price falls by 3%, a stop loss is set. This strategy can automatically identify market trends, automatically enter the market when technical indicator signals appear, and set stop-profit and stop-loss to control risks. It is a relatively mature quantitative trading strategy.
## Strategy Principle
This strategy is mainly based on the following technical indicators and conditional judgments to generate trading signals:
1. Double moving average crossover technology: Calculate the 20-day and 44-day simple moving averages. When the 20-day moving average crosses the 44-day moving average, it is judged that the market is in an upward trend, and a buy signal is generated.
2. Pressure level breakthrough technology: The chart shows that the position where the stock price has been close to but failed to break through many times is called a pressure level. When the stock price successfully breaks through the pressure level, it indicates that the price has entered a new rising stage. This strategy determines that if the stock price breaks through the 0.7% range of the previous trading day's highest price, it can be regarded as breaking through the pressure level.
3. Overbought and oversold indicator RSI: Relative Strength Index, a technical indicator that determines whether the market is overbought or oversold. This strategy sets an overbought signal when the 14-day RSI indicator is greater than 50.
4. Trading volume analysis: Trading volume exceeding the average trading volume of the past 10 days indicates stronger buying or selling in the market.
5. Buy signal: If the short-term moving average crosses the medium-term moving average and the stock price breaks through the pressure level, the market is overbought, and the trading volume is higher than the average trading volume of the past 10 days, a buy signal is generated.
6. Sell signal: Set a stop-profit and stop-loss standard. If the stock price rises by 15% from the purchase price, take profit; if it falls by 3%, stop loss.
This strategy comprehensively uses a variety of technical indicators to determine the market structure and automatically generates trading signals when the indicated trend appears. It is a relatively mature and complete quantitative trading strategy.
## Strategic Advantages
1. Use moving average technology to judge the market structure and capture market trends stably;
2. Combined with trading volume analysis, avoid opening positions in false breakthroughs where trading volume does not match;
3. Set up a stop-profit and stop-loss exit mechanism, which can well control the risk-benefit ratio of a single transaction and avoid expanding losses;
4. Generally speaking, this strategy has accurate judgment on market structure, strict trading rules, and adequate risk control. It is a quantitative strategy with good effect.
## Strategy Risk
1. The double moving average trading system is more sensitive to parameter settings, and parameters need to be adjusted in different periods;
2. Strategies that purely follow trends cannot respond to emergencies, such as major bad news that inevitably encounters stop losses;
3. Although stop-profit and stop-loss are set, the number of stop-losses will inevitably increase when the number of transactions is large, and there is a risk of uneven profit levels.
4. In the long term, the time when technical indicators send signals has often passed the best point for market reversal.
## Strategy optimization direction
1. Parameter optimization method can be used to find the best double moving average parameter combination and optimize the take-profit and stop-loss levels;
2. Add other indicators to judge, such as Bollinger Bands to identify the consolidation range, MACD to identify overbought and oversold, etc., to increase the time point for sending signals;
3. Increase fundamental or news judgment to avoid stop losses caused by major negative news;
4. Optimize fund management strategies, such as fixed quantity transactions, fixed capital ratio transactions, etc., to control single risk.
## Summarize
The overall operation of this strategy is smooth, the judgment is accurate, the trading rules are strict, and the risk is controlled in place. It is one of the quantitative strategies with better effects. However, technical trading strategies still have limitations in judging market structure. The room for optimization lies in adding other indicator judgments and comprehensive consideration of fundamental news. In addition, further optimizing stop-profit and stop-loss settings and capital management strategies are also key. Overall, this strategy has reached a high level as a technical indicator strategy, but the next step still needs to be continued optimization in the direction of fundamental messages driving the full market cycle strategy.
||

## Overview

This strategy integrates the techniques of moving average crossover and resistance level breakout to set up buying and selling signals for automated trading. When the short-term moving average crosses over the medium-term moving average from below, and the stock price breaks through the resistance level, a buy signal is generated. The strategy sets take-profit at 15% price increase and stop-loss at 3% price decrease to control risks. This mature quantitative trading strategy can automatically identify market trends and get into positions when technical signals emerge, with proper risk management.

## Strategy Principles  

The strategy generates trading signals mainly based on the following technical indicators and judgements:

1. Moving average crossover technique: 20-day and 44-day simple moving averages are calculated. When the 20-day SMA crosses over the 44-day line, it is judged that the market is in an upward trend, generating a buy signal.

2. Resistance level breakout technique: Price levels that the stock price has repeatedly reached but failed to break through are called resistance levels. Breaking through them indicates the price is entering a new uptrend. This strategy regards a breakout above 0.7% of previous close as a resistance breakout. 

3. RSI Oscillator: Relative Strength Index, a momentum indicator for identifying overbought and oversold conditions. This strategy uses the 14-day RSI value above 50 as an overbought signal.  

4. Volume analysis: Volume exceeding past 10-day average often suggests stronger buying or selling interest and momentum in price movement.

5. Buy signals: Triggered when the short SMA crosses over medium SMA, with overbought RSI value and higher than average trading volume, indicating an upward trend.

6. Sell signals: 15% take-profit from entry price, 3% stop-loss.

This mature quantitative trading strategy integrates multiple technical analysis methods to identify market structure and trend, automatically generating trading signals during trend formations, with proper risk management.

## Advantages of the Strategy

1. Captures market trends smoothly with moving average technique.

2. Avoids opening positions during false breakouts by incorporating volume analysis. 

3. Effective risk control by setting stop-loss and take-profit, optimizing risk-reward ratio.

4. Overall excellent market structure judgement, rigorous trading rules and risk control make this a robust quantitative trading strategy.


## Risks of the Strategy

1. Double moving average systems can be sensitive to parameter tuning for different periods.

2. Trend following systems cannot respond swiftly to sudden fundamental events, facing stop loss risks.

3. Although with stop loss set up, high trading frequency leads to unavoidable number of stop loss executions, resulting in uneven profit levels.

4. Signals from technical indicators often lag behind the best reversal points of the markets.

## Optimization Directions

1. Optimize parameters like moving average lengths, stop loss/profit target by parameter tuning methods to find optimum.

2. Add other technical indicators like Bollinger Bands for range detection, MACD for spotting divergences etc. to improve signal accuracy.  

3. Incorporate fundamental and event driven signals to avoid stop loss triggered by negative news.

4. Optimize money management by fixed quantity, fixed percentage methods to control per trade risks.

## Conclusion
This strategy demonstrates smooth operations, accurate judgements and rigorous trading rules, representing one of the more effective quantitative trading techniques. But technical analysis alone has limitations in reading markets, so further improvements lie in incorporating more indicators and fundamental/event signals, optimizing stop loss/profit taking levels and money management mechanisms. In summary, this strategy has reached high level among technical analysis strategies, but should head towards fundamental/event driven cycles trading strategies in next evolution steps.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Advanced Strategy with Conditional Stop Loss", overlay=true)

// Parameters
ma_length_20 = 20
ma_length_44 = 44
ma_length_100 = 100
rsi_length = 14
volume_length = 10
profit_target = 1.15 // 15% above the buy price
stop_loss_target = 0.97 // 3% below the buy price
wait_candles = 10 // Number of candles to wait after selling, unless MA cross condition met

// Indicators
moving_average_20 = ta.sma(close, ma_length_20)
moving_average_44 = ta.sma(close, ma_length_44)
moving_average_100 = ta.sma(close, ma_length_100)
rsi = ta.rsi(close, rsi_length)
volumeAvg = ta.sma(volume, volume_length)

// Variables to manage the wait period after a sell
var int last_sell_candle = 0

// Update last sell candle
if (strategy.position_size[1] > 0 and strategy.position_size == 0)
    last_sell_candle := bar_index

// Trend identification
uptrend = close > moving_average_20
above_ma20_by_1_percent = close > moving_average_20 * 1.01
ma_cross = ta.crossover(moving_average_20, moving_average_44) or ta.crossunder(moving_average_20, moving_average_44)
close_near_high = (close >= high * 0.993) and (close <= high)

// Buy condition (only in uptrend, above 1% from 20-day MA, and respecting new filter)
can_buy_after_cross = ma_cross and close > high[1]
can_buy_after_wait = (bar_index - last_sell_candle) > wait_candles
buy_condition = (can_buy_after_cross or can_buy_after_wait) and uptrend and above_ma20_by_1_percent and close > moving_average_44 and close > moving_average_100 and close > high[1] and rsi > 50 and volume > volumeAvg and not close_near_high

// Entry
if (buy_condition and strategy.position_size == 0)
    strategy.entry("Buy", strategy.long)

// Exit conditions
if (strategy.position_size > 0)
    // Profit target
    profit_level = strategy.position_avg_price * profit_target
    strategy.exit("Take Profit", "Buy", limit=profit_level)

    // Dynamic Stop Loss - Check on every bar if the price has dropped 3% below the buy price
    stop_loss_level = strategy.position_avg_price * stop_loss_target
    if (low < stop_loss_level)
        strategy.close("Buy", comment="Stop Loss")

// Plotting
plot(moving_average_20, color=color.green, title="20-Day Moving Average")
plot(moving_average_44, color=color.blue, title="44-Day Moving Average")
plot(moving_average_100, color=color.red, title="100-Day Moving Average")

```

> Detail

https://www.fmz.com/strategy/440535

> Last Modified

2024-01-31 14:34:16
