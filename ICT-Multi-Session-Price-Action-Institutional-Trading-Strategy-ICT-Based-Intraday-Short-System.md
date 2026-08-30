
> Name

Multi-Session-Price-Action-Institutional-Trading-Strategy-ICT-Based-Intraday-Short-System
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d7e40632fbab41f7f128.png)
![IMG](https://www.fmz.com/upload/asset/2d87a352b683e654be68f.png)



[trans]

#### Overview
The Multi-Period Price Action Institutional Trading Strategy is an intraday trading system based on the ICT (Internal Bank Trading) concept, specifically designed to capture market downtrends. This strategy tracks price behavior during three major trading sessions in London, New York and Asia, identifies institutional capital flows, and looks for high-probability shorting opportunities in key price areas. The core of the strategy is to use the linkage relationship and price structure between different trading periods, combined with institutional trading concepts such as the "Judas Swing", to make accurate entries in areas of concentrated liquidity.
#### Strategy Principle
The operation of this strategy is based on the analysis of price structure over multiple trading periods and mainly includes the following key components:
1. **London opening setting (New York time 2:00-8:20)**: The code sets the start time of the London session through the variable `sessionLondon`, and updates the highest price `londonHigh` and lowest price `londonLow` ​​of the period in real time. The London session usually establishes the initial direction for the day.
2. **New York opening killing zone (8:20-10:00 New York time)**: Code setting `sessionNYOpen` captures the New York opening time. When the price breaks through the high in the London session during the New York session and then falls back (called the "Judas Swing"), and the conditions `judasSwing = high >= londonHigh and time >= sessionNYOpen` are met, the system is ready to go short.
3. **London closing buy setting (New York time 10:30-13:00)**: The `londonCloseBuy` condition in the code determines whether to trigger a long signal during the London closing period. The price needs to fall below the low of the London session, and the goal is to capture the callback rebound.
4. **Asian opening short setting (New York time 19:00-2:00)**: The code identifies the start of the Asian session through `sessionAsia`. When the price breaks through the high point of the Asian session (`close > asiaHigh`), the short entry is triggered.
The core trading logic of the strategy is to utilize the "Judas Swing" concept, that is, when the price briefly breaks through the London high during the New York session and then falls back, it indicates that large institutions may ship at high levels, and short selling has a higher winning rate at this time. At the same time, the strategy also includes a long reversal during the London closing period and a short selling strategy during the Asian session, forming an all-weather trading system.
#### Strategic Advantages
By deeply analyzing the code, this strategy offers the following significant advantages:
1. **Multi-period collaborative analysis**: The strategy integrates the price data of three major trading periods, and comprehensively tracks the price performance of different markets through variables `londonHigh`, `nyHigh` and `asiaHigh`, etc., avoiding the limitations of single-period analysis.
2. **Entry logic based on institutional concepts**: The "Judas Swing" concept at the core of the strategy (`judasSwing` conditional judgment) directly targets the trading behavior of institutional funds and can effectively identify the inductive behavior and true intentions of large institutions.
3. **Precise time control**: Use the `timestamp` function to accurately set the start and end time of each trading period to ensure that transactions are conducted during the most active market periods and improve the effectiveness of transactions.
4. **Clear Risk Management**: The code contains clear stop loss settings (`stopLoss = high + 10 * syminfo.mintick`) and profit targets (`profitTarget = low - 20 * syminfo.mintick`), making the risk of each transaction controllable.
5. **Visual support**: The strategy draws the high and low points of each period through the `plot` function, providing an intuitive visual reference for trading decisions and enhancing the practicality of the strategy.
#### Strategy Risk
Although this strategy is well designed, there are still potential risks:
1. **False Breakout Risk**: In highly volatile markets, the "Judas Swing" signal may produce a false breakout, leading to erroneous shorting. The solution is to add filters such as combining volume confirmation or waiting for a clearer price pullback pattern.
2. **Strong time dependence**: The strategy is highly dependent on market behavior during a specific period of time. If market characteristics change or major news is released at atypical times, the effectiveness of the strategy may be reduced. It is recommended to use it in conjunction with the market news calendar and suspend trading before major data releases.
3. **Stop loss setting is fixed**: The stop loss setting in the code is a fixed number of points (`10 * syminfo.mintick`), which does not take into account the differences in volatility in different markets and time periods. It can be improved to dynamic stop loss based on volatility indicators such as ATR.
4. **Lack of filtering mechanism**: The strategy does not take into account the overall market trend and volatility environment, and may frequently generate erroneous short selling signals during strong rising markets. It is recommended to add trend filters such as moving average direction or momentum indicators.
5. **Backtest bias risk**: Since the strategy relies on price behavior in a specific time period, there may be a forward-looking bias when backtesting at low time periods. In actual trading, attention should be paid to the difference between strategy performance and backtest results.
#### Strategy optimization direction
Based on code analysis, this strategy can be optimized in the following directions:
1. **Dynamic stop loss mechanism**: Change the fixed point stop loss (`stopLoss = high + 10 * syminfo.mintick`) to a dynamic stop loss based on ATR, such as `stopLoss = high + atr(14) * 1.5`, which can better adapt to the fluctuation characteristics of different market environments.
2. **Added trend filter**: Adding trend judgment conditions of a higher time period, such as the direction of the moving average on the daily or 4-hour chart, and only trading in the direction consistent with the general trend can improve the winning rate of the strategy.
3. **Volume Confirmation**: Add volume analysis when the "Judas Swing" signal is triggered, and execute shorting only when the price falls back with an increase in trading volume. This can reduce losses caused by false breakthroughs.
4. **Add market sentiment indicators**: Combined with VIX or other market volatility indicators, adjust or suspend strategies in extreme volatile environments to avoid trading in unstable markets.
5. **Optimize entry timing**: The current short-selling entry condition is only `close < open`, which can be improved to wait for the price to fall back to a key support level (such as the London session opening price or VWAP) before entering to improve the accuracy of entry.
6. **Add multi-period confirmation**: Combined with the price structure of a lower time period, after meeting the main entry conditions, find a more precise entry point to reduce slippage and unnecessary risks.
These optimization directions aim to improve the stability and reliability of the strategy so that it can maintain good performance in different market environments.
#### Summarize
The multi-period price action institutional trading strategy is a comprehensive intraday trading system that integrates ICT trading concepts. By analyzing the price structure of the three major trading periods in London, New York and Asia, it captures high-probability trading opportunities brought by institutional capital flows. The biggest feature of this strategy is to follow the flow of institutional funds and trade, especially using the "Judas Swing" concept to capture short-selling opportunities. It also includes reversal long and Asian session short-selling strategies to form a comprehensive trading system.
Although the strategy is well designed and includes clear entry conditions and risk management rules, it still has shortcomings such as the risk of false breakthroughs and strong dependence on a specific time. By adding optimization measures such as dynamic stop loss, trend filtering, and volume confirmation, the stability and adaptability of the strategy can be further improved.
For traders pursuing intraday trading opportunities, this strategy provides a structured approach to understanding and exploiting the market characteristics of different trading sessions, and is particularly suitable for traders who wish to master institutional trading concepts and profit from short-term intraday trading. ||
#### Overview

The Multi-Session Price Action Institutional Trading Strategy is an intraday trading system based on ICT (Inner Circle Trader) concepts, specifically designed to capture market downtrends. The strategy tracks price action across three major trading sessions—London, New York, and Asia—to identify institutional money flow and seek high-probability shorting opportunities at key price levels. The core of the strategy lies in utilizing the interconnected relationships between different trading sessions and price structures, combined with institutional trading concepts such as the "Judas Swing," to execute precise entries in areas of concentrated liquidity.

#### Strategy Principles

The strategy operates based on price structure analysis across multiple trading sessions, comprising several key components:

1. **London Open Setup (2:00-8:20 NY time)**: The code uses the variable `sessionLondon` to set the London session start time and continuously updates the session high `londonHigh` and low `londonLow`. The London session typically establishes the initial direction for the day.

2. **New York Open Kill Zone (8:20-10:00 NY time)**: The code sets `sessionNYOpen` to capture the New York opening time. When price breaks above the London session high and then reverses during the NY session (known as the "Judas Swing"), meeting the condition `judasSwing = high >= londonHigh and time >= sessionNYOpen`, the system prepares for a short entry.

3. **London Close Buy Setup (10:30-13:00 NY time)**: The code's `londonCloseBuy` condition determines whether to trigger a long signal during the London closing session, requiring price to drop below the London session low, aiming to capture retracement bounces.

4. **Asia Open Sell Setup (19:00-2:00 NY time)**: The code identifies the start of the Asian session with `sessionAsia`, triggering a short entry when price breaks above the Asian session high (`close > asiaHigh`).

The core trading logic leverages the "Judas Swing" concept, where price temporarily breaks above the London high during the New York session before reversing, indicating that large institutions may be distributing at higher levels, making short positions highly probable. The strategy also incorporates a long reversal during the London closing session and a short strategy during the Asian session, forming a round-the-clock trading system.

#### Strategy Advantages

Through deep code analysis, this strategy demonstrates the following significant advantages:

1. **Multi-Session Collaborative Analysis**: The strategy integrates price data from three major trading sessions, comprehensively tracking different markets' price performance through variables like `londonHigh`, `nyHigh`, and `asiaHigh`, avoiding the limitations of single-session analysis.

2. **Institution-Based Entry Logic**: The strategy's core "Judas Swing" concept (the `judasSwing` condition) directly aligns with institutional trading behavior, effectively identifying manipulative actions and true intentions of large institutions.

3. **Precise Time Control**: Through the `timestamp` function, the strategy precisely sets the start and end times of each trading session, ensuring trades occur during the most active market periods, enhancing trading effectiveness.

4. **Clear Risk Management**: The code includes explicit stop-loss settings (`stopLoss = high + 10 * syminfo.mintick`) and profit targets (`profitTarget = low - 20 * syminfo.mintick`), making the risk controllable for each trade.

5. **Visualization Support**: The strategy uses the `plot` function to draw the highs and lows of each session, providing intuitive visual references for trading decisions, enhancing the strategy's practicality.

#### Strategy Risks

Despite its rational design, the strategy still faces several potential risks:

1. **False Breakout Risk**: In highly volatile markets, the "Judas Swing" signal may generate false breakouts, leading to incorrect short entries. A solution is to add filtering conditions, such as volume confirmation or waiting for more definitive price reversal patterns.

2. **Strong Time Dependency**: The strategy heavily relies on market behavior during specific time periods. If market characteristics change or major news is released at atypical times, the strategy's effectiveness may decrease. It's recommended to use it in conjunction with a market news calendar and pause trading before major data releases.

3. **Fixed Stop-Loss Setting**: The stop-loss in the code is set as a fixed number of points (`10 * syminfo.mintick`), not accounting for volatility differences across markets and sessions. This could be improved by implementing dynamic stops based on indicators like ATR.

4. **Lack of Filtering Mechanisms**: The strategy doesn't consider overall market trends and volatility environments, potentially generating frequent false short signals in strong upward markets. Adding trend filtering conditions, such as moving average direction or momentum indicators, is recommended.

5. **Backtest Bias Risk**: Since the strategy relies on price behavior during specific time periods, there may be forward-looking bias in low timeframe backtests. Traders should be aware of potential differences between strategy performance and backtest results in actual trading.

#### Strategy Optimization Directions

Based on code analysis, the strategy can be optimized in these directions:

1. **Dynamic Stop-Loss Mechanism**: Replace the fixed-point stop-loss (`stopLoss = high + 10 * syminfo.mintick`) with an ATR-based dynamic stop, such as `stopLoss = high + atr(14) * 1.5`, to better adapt to volatility characteristics in different market environments.

2. **Add Trend Filtering**: Incorporate trend determination conditions from higher timeframes, such as daily or 4-hour chart moving average directions, to trade only in the direction consistent with the larger trend, improving the strategy's win rate.

3. **Volume Confirmation**: Add volume analysis when the "Judas Swing" signal triggers, executing shorts only when price reversal is accompanied by increasing volume, reducing losses from false breakouts.

4. **Incorporate Market Sentiment Indicators**: Combine with VIX or other market volatility indicators to adjust or pause the strategy in extremely volatile environments, avoiding trading in unstable markets.

5. **Optimize Entry Timing**: The current short entry condition is simply `close < open`. This could be improved by waiting for price to retrace to key support levels (such as London session opening price or VWAP) before entering, increasing entry precision.

6. **Add Multi-Timeframe Confirmation**: Combine price structures from lower timeframes to find more precise entry points after meeting the main entry conditions, reducing slippage and unnecessary risk.

These optimization directions aim to enhance the strategy's stability and reliability, enabling it to maintain good performance across different market environments.

#### Summary

The Multi-Session Price Action Institutional Trading Strategy is a comprehensive intraday trading system integrating ICT trading concepts, capturing high-probability trading opportunities driven by institutional money flow by analyzing price structures across the London, New York, and Asian trading sessions. The strategy's most distinctive feature is trading in alignment with institutional money flow, particularly using the "Judas Swing" concept to capture shorting opportunities, while also incorporating reversal long trades and Asian session shorts to form a complete trading system.

Although the strategy is well-designed with clear entry conditions and risk management rules, it still has drawbacks such as false breakout risks and strong dependency on specific time periods. By incorporating dynamic stop-losses, trend filtering, volume confirmation, and other optimization measures, the strategy's stability and adaptability can be further enhanced.

For traders pursuing intraday opportunities, this strategy provides a structured approach to understanding and capitalizing on market characteristics across different trading sessions, particularly suitable for those who wish to master institutional trading concepts and profit from intraday short-term positions.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-26 00:00:00
end: 2025-03-25 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("ICT Bread and Butter Sell-Setup", overlay=true)

// Get current date values
t = time
currentYear = year(t)
currentMonth = month(t)
currentDay = dayofmonth(t)

// Time Settings
sessionNYOpen  = timestamp(currentYear, currentMonth, currentDay, 08, 20) // CME Open
sessionLondon  = timestamp(currentYear, currentMonth, currentDay, 02, 00) // London Open
sessionAsia    = timestamp(currentYear, currentMonth, currentDay, 19, 00) // Asia Open
sessionEnd     = timestamp(currentYear, currentMonth, currentDay, 16, 00) // Market Close

// Session Ranges (Initialize to the first bar values)
var float londonHigh = high
var float londonLow = low
var float nyHigh = high
var float nyLow = low
var float asiaHigh = high
var float asiaLow = low

// Update Highs & Lows for Each Session
if (time >= sessionLondon and time < sessionNYOpen)
    londonHigh := math.max(londonHigh, high)
    londonLow := math.min(londonLow, low)

if (time >= sessionNYOpen and time < sessionEnd)
    nyHigh := math.max(nyHigh, high)
    nyLow := math.min(nyLow, low)

if (time >= sessionAsia and time < sessionLondon)
    asiaHigh := math.max(asiaHigh, high)
    asiaLow := math.min(asiaLow, low)

// New York Judas Swing (Temporary Rally)
judasSwing = high >= londonHigh and time >= sessionNYOpen and time < sessionEnd

// Short Entry in NY Kill Zone
shortEntry = judasSwing and close < open
stopLoss = high + 10 * syminfo.mintick
profitTarget = low - 20 * syminfo.mintick

if shortEntry
    strategy.entry("Short", strategy.short)
    strategy.exit("Take Profit", from_entry="Short", limit=profitTarget, stop=stopLoss)

// London Close Buy Setup
londonCloseBuy = time >= timestamp(currentYear, currentMonth, currentDay, 10, 30) and time <= timestamp(currentYear, currentMonth, currentDay, 13, 00) and close < londonLow
if londonCloseBuy
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit Buy", from_entry="Buy", limit=close + 20 * syminfo.mintick, stop=low - 10 * syminfo.mintick)

// Asia Open Sell Setup
asiaSell = time >= sessionAsia and time < sessionLondon and close > asiaHigh
if asiaSell
    strategy.entry("Asia Short", strategy.short)
    strategy.exit("Asia Profit", from_entry="Asia Short", limit=close - 15 * syminfo.mintick, stop=high + 10 * syminfo.mintick)

// Plot High/Low of Sessions
plot(londonHigh, color=color.blue, title="London High")
plot(londonLow, color=color.blue, title="London Low")
plot(nyHigh, color=color.red, title="NY High")
plot(nyLow, color=color.red, title="NY Low")
plot(asiaHigh, color=color.orange, title="Asia High")
plot(asiaLow, color=color.orange, title="Asia Low")

```

> Detail

https://www.fmz.com/strategy/488283

> Last Modified

2025-03-26 15:40:23
