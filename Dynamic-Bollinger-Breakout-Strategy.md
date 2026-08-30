
> Name

Dynamic-Bollinger-Breakout-Strategy Based on Bollinger Bands Indicator Breakout Trading Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/145d2fdb3688f8d594b.png)
[trans]

## Overview
This strategy is a breakout trading strategy based on the Bollinger Bands indicator. It realizes automated trading on Binance BTCUSDT by calculating the upper and lower rails of the Bollinger Band and combining it with dynamically adjusted buy and sell thresholds.
## Strategy Principle
The core indicator of this strategy is Bollinger Bands. Bollinger Bands consists of an N-day moving average and its upper and lower standard deviation channels. The Bollinger Band length in this strategy is 20 days, and the standard deviation multiple is 2. When the price is close to or touches the lower track of the Bollinger Band, it is considered excessively oversold, and the strategy will open a long position at this time; when the price is close to or touches the upper track of the Bollinger Band, it is considered excessively bullish, and the strategy will close the long position.
In addition to the Bollinger Bands indicator, this strategy also introduces two adjustable parameters: buy threshold and sell threshold. The buying threshold defaults to 58 points below the Bollinger Band, which is the condition for opening long orders. The selling threshold defaults to 470 points above the Bollinger Band, which is the condition for closing the position. These two thresholds can be dynamically adjusted according to the actual situation and backtest results, making the strategy more flexible.
When the buying conditions are met, the strategy will use 10% of the account equity to open a long position. After going long, if the price rise reaches the stop loss condition (-125%), the position will be stopped and closed. When the sell threshold is triggered after the price rises, the strategy will choose to close all positions and recover profits.
## Advantage Analysis
This strategy has several major advantages:
1. Using the Bollinger Bands indicator, you can seize the opportunity when the price abnormally leaves the track and profit from the reversal.
2. Introduce dynamically adjusted buying and selling thresholds to optimize entry and exit opportunities
3. Taking part of the position to go long can control risks
4. Set stop loss conditions to avoid further expansion of losses
5. The backtest data uses a 5-minute line, which can capture shorter period trading opportunities in a timely manner.
## Risk Analysis
This strategy also has certain risks:
1. The Bollinger Bands indicator itself is not 100% reliable, and the price may fluctuate at a low level for a long time and then fall again.
2. Improper threshold setting may lead to missing the best entry or exit point
3. The stop loss setting is too loose and the loss cannot be stopped in time, or it is too strict and the stop loss is too sensitive.
4. If the backtest cycle is improperly selected, some accidental profits may be regarded as stable profits.
Countermeasures:
1. Combine more indicators to judge the market and avoid Bollinger Bands from sending out wrong signals.
2. Test and optimize threshold parameters to find the best parameter combination
3. Test and optimize stop loss conditions and find the balance point
4. Use a longer backtest period to test the stability of the strategy
## Optimization direction
This strategy can also be optimized from the following directions:
1. Try to combine with other indicators, such as KD, RSI, etc., to set stricter entry rules to avoid entering the market too early or too late.
2. Test different Bollinger Band parameter combinations and optimize the length and standard deviation multiple of the Bollinger Band.
3. Optimize the buying and selling thresholds and find the best parameters to increase profitability
4. Try to dynamically adjust the stop loss ratio based on ATR to make the stop loss more in line with market volatility.
5. Optimize position management, for example, you can add positions appropriately after making profits to control the risk of single loss.
## Summarize
This strategy overall is a relatively simple and practical breakthrough strategy. It uses the Bollinger Bands indicator to determine market reversal opportunities and sets dynamic thresholds for entry and exit. At the same time, the strategy also uses reasonable position management, stop loss conditions, etc. to control risks. After optimizing several key parameters, this strategy can achieve relatively stable returns. It is suitable for quantitative trading and can also be used as an auxiliary tool for stock selection or judging market sentiment. In general, this strategy has strong practicality and scalability.
||

## Overview  

This strategy is a breakout trading strategy based on the Bollinger Bands indicator. It calculates the upper and lower rails of the Bollinger Bands and combines them with dynamically adjustable buy and sell thresholds to automate trading of BTCUSDT on Binance.

## Strategy Logic

The core indicator of this strategy is Bollinger Bands. Bollinger Bands consist of an N-day moving average and upper and lower bands plotted at a standard deviation level above and below it. The Bollinger Bands in this strategy have a length of 20 days and a standard deviation multiplier of 2. When the price approaches or touches the lower rail of the Bollinger Bands, it is considered oversold, and the strategy will open a long position. When the price approaches or touches the upper rail, it is considered overbought, and the strategy will close long positions.

In addition to the Bollinger Bands indicator, this strategy also introduces two adjustable parameters: buy threshold and sell threshold. The buy threshold defaults to 58 points below the lower band and serves as the entry condition for opening long positions. The sell threshold defaults to 470 points above the lower band and serves as the exit condition for closing positions. These thresholds can be dynamically adjusted based on actual market conditions and backtest results to make the strategy more flexible.  

When the buy condition is met, the strategy will open a long position using 10% of the account equity. After opening the long position, if the price rises to hit the stop loss level (-125%), positions will be closed by stop loss orders. When the price rises to trigger the sell threshold, the strategy will choose to close all positions to collect profits.

## Advantage Analysis

The main advantages of this strategy include:

1. Using Bollinger Bands can capture opportunities when prices abnormally deviate from bands and profit from reversals
2. Introducing adjustable buy and sell thresholds optimizes entry and exit points  
3. Taking partial position sizes controls risk 
4. Setting stop loss condition avoids further losses
5. Backtesting with 5-min intervals can capture short-term trading opportunities in a timely manner

## Risk Analysis

There are also some risks with this strategy:

1. Bollinger Bands itself is not 100% reliable, prices may oscillate lower for a long time before dropping again
2. Improper threshold settings may cause missing the best entry or exit points
3. Stop loss setting too loose may fail to stop loss in time, or too tight may cause stop loss too sensitive
4. Improper backtesting period selection may take some occasional profits as stable income

Countermeasures:

1. Combine more indicators to judge market conditions and avoid false signals of Bollinger Bands  
2. Test and optimize threshold parameters to find optimal combination
3. Test and optimize stop loss conditions to find a balance
4. Adopt longer backtesting period to examine stability of the strategy

## Optimization Directions 

The strategy can be further optimized in the following aspects:

1. Try combining other indicators like KD, RSI to set stricter entry rules, avoid entering too early or too late
2. Test different combinations of Bollinger Bands parameters to optimize band length and standard deviation multiplier
3. Optimize buy and sell thresholds to improve profit rate
4. Try adopting dynamic ATR-based stop loss ratio to match market volatility
5. Optimize position sizing, e.g. appropriately pyramiding positions when in profit to control single loss risk

## Summary   

In summary, this is an overall simple and practical breakout strategy. It adopts Bollinger Bands to identify reversal opportunities and sets dynamic thresholds for entry and exit. Meanwhile, reasonable position sizing and stop loss conditions are utilized to control risks. After optimizing several key parameters, this strategy can yield relatively steady returns. It is suitable for algorithmic trading and can also serve as an auxiliary tool for stock picking or gauging market sentiment. Generally speaking, this strategy has strong practicality and extensibility.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20| Bollinger Bands Period|
|v_input_2|2|Standard deviation multiple|
|v_input_3|58|Buy threshold|
|v_input_4|470|Sell threshold|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SuperDS_BTC

//@version=5
strategy("布林通道策略多5min", overlay=true) 

// 布林通道计算
length = input(20, title="布林通道周期")
mult = input(2.0, title="标准差倍数")
basis = ta.sma(close, length)
dev = mult * ta.stdev(close, length)
upper = basis + dev
lower = basis - dev

// 计算买入数量：每次检查仓位的大小 
// 每次买入使用总资金的10%
position_size = strategy.equity * 10 / close 

// 定義可調整的閾值
buy_threshold = input(58, title="買入閾值")
exit_threshold = input(470, title="賣出閾值")

// 买入条件：当现价低于布林通道的下限减去 buy_threshold
buy_condition = close < lower - buy_threshold

// 卖出条件和结清仓位条件
exit_condition = close > lower + exit_threshold

// 买入逻辑
if buy_condition
    strategy.entry("BuyLong", strategy.long, qty=position_size, comment="LongBTC")

// 卖出逻辑
if exit_condition
    strategy.close("BuyLong")

// 止损逻辑
stop_loss_percent = -1.25 //止损百分比为-125%
if strategy.position_size > 0
    position_profit_percent = (strategy.position_avg_price - close) / strategy.position_avg_price * 100
    if position_profit_percent <= stop_loss_percent
        strategy.close("BuyLong")
```

> Detail

https://www.fmz.com/strategy/440081

> Last Modified

2024-01-26 14:52:59
