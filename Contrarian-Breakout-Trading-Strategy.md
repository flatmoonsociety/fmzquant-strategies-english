
> Name

Contrarian-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/81e6e8e24031c52ab5c0ca8b9240940d447ec12ff8a481a796cb867577aea0fb.png)
[trans]


## Overview
The reverse breakout trading strategy is a trading strategy that performs reverse operations based on continuous rising or falling price breakthroughs. This strategy sets a cycle of continuous price increases or decreases, and then performs reverse operations to make profits after the price forms a certain trend.
## Strategy Principle
This strategy is mainly implemented through the following parts:
1. Set the cycle length of continuous price rise and fall, namely coherentBarsUp and coherentBarsDown. The trading signal is triggered when the price trend of the current cycle reaches the set length.
2. Calculate the rise and fall of the current price relative to the price of the previous cycle, and calculate the current continuous rise or fall cycle length ups and dns based on the rise and fall.
3. Set the time range of the backtest and use time_cond to limit the strategy to only operate during the backtest time.
4. Set the daily trading time and use timetobuy to limit the trading signal to only be issued within the set time period.
5. When the price continues to rise for a period that reaches the set length, a long signal is sent through strategy.long; when the price continues to fall for a period that reaches the set length, a short signal is sent through strategy.short.
6. You can set stop loss and take profit prices. Set a short-term stop loss when going long, and set a long-term stop loss when going short; set a long-term stop loss when going long, and set a short-term stop profit when going short.
7. You can set a message prompt when sending a trading signal.
8. Based on the above parameters and price judgment, send a long or short signal when the conditions are met.
## Advantage Analysis
This reverse breakout strategy has the following advantages:
1. Capture price reversal points and reverse operations to obtain better profits. When the price forms a trend, you can perform reverse operations to make profits when the price reverses.
2. The configurable parameters are flexible and can be adjusted according to the market. The number of consecutive rising and falling cycles can be adjusted, the stop-profit and stop-loss points can be adjusted, the trading time period can be limited, and the parameters can be optimized according to the actual situation.
3. Stop loss and stop profit can be added to control risks. After going long or short, you can set stop loss and take profit in advance, which helps control transaction risks.
4. You can set transaction reminder messages to facilitate automated transactions. You can set a message prompt when sending a trading signal and use it with the automatic trading system.
5. The backtest time range can be set to facilitate testing strategies. The setting of backtest time range has been added to facilitate observation of strategy effects under different market conditions.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. Avoid important news events. It is impossible to judge the price trend when major news is released, and the strategy will send out long and short signals at the same time, resulting in losses. Avoid the release time of important financial news.
2. It has little effect when the reversal is not obvious. When the trend is not obvious, reverse operations are not effective and need to be used with caution.
3. Backtest data fitting risks. Strategy optimization should avoid over-reliance on backtest data, as backtest data does not represent future trends. Parameters should be adjusted appropriately during real offer.
4. If the trading frequency is too high, it is easy to mark the market. If the set period is too short, the trading frequency is too high, which is not conducive to long-term stable profits.
5. Stop-loss and take-profit strategies can be appropriately optimized to reduce risks. The existing fixed stop loss and take profit can be further optimized into methods such as trend following stop loss.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Add a trend judgment mechanism to avoid random reversals in non-trending markets. It can detect price volatility, channels and other indicators to determine the extent of the trend and avoid missing price reversal points.
2. Optimize the stop-loss and take-profit strategy so that it can automatically adjust according to market fluctuations. You can use balance percentage stop loss, ATR stop loss and other methods to make stop loss and profit settings more intelligent.
3. The added amount can be judged by the indicator. Combined with indicators such as changes in trading volume, avoid erroneous signals generated solely based on K-line patterns.
4. Multi-variety combination. Applying strategies to different varieties and combining them can diversify the risks of a single variety.
5. Parameter optimization and machine learning. Collect more historical data and use machine learning methods to automatically optimize parameters to make the strategy more stable.
## Summarize
The reverse breakout trading strategy can obtain good trading signals by capturing price reversal points and performing reverse operations. The advantage of this strategy is that it has flexible configuration, can control risks, and is suitable for automated trading. However, there are also certain risks, and parameters and strategies need to be continuously optimized and improved in order to achieve long-term stable profits.
||

## Overview

The contrarian breakout trading strategy is a strategy that takes contrarian signals based on consecutive price rises or falls to go long when the short condition is met or go short when the long condition is met. It aims to produce a profit by taking the opposing trade when an asset produces only losses with a given strategy.  

## Strategy Logic

The strategy is mainly implemented through the following parts:

1. Set the consecutive periods for price rises and falls, i.e. consecutiveBarsUp and consecutiveBarsDown. When the current period trend reaches the set length, a trading signal is triggered.

2. Calculate the rise and fall of the current price relative to the previous period price. Calculate the length of the current consecutive rise or fall periods ups and dns based on the rise and fall.

3. Set the backtesting time range to limit the strategy to operate only within the backtesting time through time_cond. 

4. Set the daily trading time to limit trading signals to be issued only within the set time frame through timetobuy.

5. When the consecutive rising cycle reaches the set length, issue a long signal through strategy.long. When the consecutive falling cycle reaches the set length, issue a short signal through strategy.short.

6. Stop loss and take profit prices can be set. Set short-term stops for long positions and long-term stops for short positions. Set long-term take profits for long positions and short-term take profits for short positions.

7. Trade signal messages can be set during sending.

8. Issue long or short signals when conditions are met based on the above parameters and price levels.

## Advantage Analysis

This contrarian breakout strategy has the following advantages:

1. Captures price reversal points. Contrarian operation can obtain good profits. Operations in the opposite direction when the price forms a trend can profit at price reversals.

2. Flexible configurable parameters. Parameters such as consecutive periods can be adjusted, stop loss and take profit levels can be set, trading time frame can be limited. Parameters can be optimized according to market conditions. 

3. Stop loss and take profit can control risks. Setting stop loss and take profit in advance helps control trading risks after going long or short.

4. Trade messages facilitate automated trading. Setting trade signal messages facilitates integration with automated trading systems.

5. Backtesting time range facilitates strategy testing. Adding backtesting time range settings allows easy observation of strategy performance under different market conditions.

## Risk Analysis

The strategy also has some risks to note:

1. Avoid significant news events. Price trends are unpredictable during major announcements, causing simultaneous long and short signals and losses. Major economic releases should be avoided.

2. Less effective when reversals are unclear. Less effective when trends are ambiguous, contrarian trading should be used with caution.

3. Backtesting data overfitting risk. Optimization should avoid over-reliance on backtesting data, which does not represent future trends. Parameters should be adjusted appropriately during live trading.

4. High trading frequency risks overtrading. Short cycle settings may result in excessive trading frequency and risks for long-term steady gains.

5. Stop loss and take profit strategies can be optimized to reduce risks. The fixed stops can be further improved to trailing stops.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Add trend detection to avoid random reversals in non-trending markets, using volatility, channels etc to gauge trends and capture reversals.

2. Optimize stops and takes to adjust based on market volatility, using percentage-based, ATR or other adaptive methods.

3. Add volume analysis to avoid false signals from price patterns alone.

4. Portfolio diversification across multiple products to reduce single asset risk.

5. Parameter optimization and machine learning. Collect more historical data and use machine learning to auto-optimize parameters for more robust strategies.

## Conclusion

The contrarian breakout strategy provides good trading signal by capturing price reversals through contrarian operations. The advantages include flexible configuration, risk control and suitability for automated trading. But risks exist and continuous improvements in parameters and logic are needed for long-term steady profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Consecutive Bars Up|
|v_input_2|true|Consecutive Bars Down|
|v_input_3|timestamp(2021-01-01T00:00:00)|Backtesting Start Date|
|v_input_4|timestamp(2021-12-31T00:00:00)|Backtesting End Date|
|v_input_5||Time Frame To Enter Trades|
|v_input_6|false|Enable Close Trade At End Of Time Frame|
|v_input_7|false|Enable Take Profit & Stop Loss|
|v_input_8|5|Stop Loss Ticks|
|v_input_9|10|Take Profit Ticks|
|v_input_10||Long Entry message|
|v_input_11||Short Entry message|
|v_input_12||Close Long message|
|v_input_13||Close Short message|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-17 00:00:00
end: 2023-10-24 00:00:00
period: 45m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

// Strategy
strategy("Up/Down Strategy - Contrarian", overlay=true, initial_capital = 10000, default_qty_value = 10000, default_qty_type = strategy.cash)

consecutiveBarsUp = input(1, title='Consecutive Bars Up')
consecutiveBarsDown = input(1, title='Consecutive Bars Down')

price = close

ups = 0.0
ups := price > price[1] ? nz(ups[1]) + 1 : 0

dns = 0.0
dns := price < price[1] ? nz(dns[1]) + 1 : 0

// Strategy Backtesting
startDate  = input(timestamp("2021-01-01T00:00:00"), type = input.time, title='Backtesting Start Date')
finishDate = input(timestamp("2021-12-31T00:00:00"), type = input.time, title='Backtesting End Date')

time_cond  = true

//Time Restriction Settings
startendtime = input("", title='Time Frame To Enter Trades')
enableclose = input(false, title='Enable Close Trade At End Of Time Frame')
timetobuy = true
timetoclose = true

// Stop Loss & Take Profit Tick Based
enablesltp = input(false, title='Enable Take Profit & Stop Loss')
stopTick = input(5.0, title='Stop Loss Ticks', type=input.float) / 100
takeTick = input(10.0, title='Take Profit Ticks', type=input.float) / 100

longStop = strategy.position_avg_price - stopTick
shortStop = strategy.position_avg_price + stopTick
shortTake = strategy.position_avg_price - takeTick
longTake = strategy.position_avg_price + takeTick

plot(strategy.position_size > 0 and enablesltp ? longStop : na, style=plot.style_linebr, color=color.red, linewidth=1, title="Long Fixed SL")
plot(strategy.position_size < 0 and enablesltp ? shortStop : na, style=plot.style_linebr, color=color.red, linewidth=1, title="Short Fixed SL")
plot(strategy.position_size > 0 and enablesltp ? longTake : na, style=plot.style_linebr, color=color.green, linewidth=1, title="Long Take Profit")
plot(strategy.position_size < 0 and enablesltp ? shortTake : na, style=plot.style_linebr, color=color.green, linewidth=1, title="Short Take Profit")

// Alert messages
message_enterlong  = input("", title="Long Entry message")
message_entershort = input("", title="Short Entry message")
message_closelong = input("", title="Close Long message")
message_closeshort = input("", title="Close Short message")

// Strategy Execution
if (dns >= consecutiveBarsDown) and time_cond and timetobuy
    strategy.entry("Long", strategy.long, stop = high + syminfo.mintick, alert_message = message_enterlong)
    
if (ups >= consecutiveBarsUp) and time_cond and timetobuy
    strategy.entry("Short", strategy.short, stop = low + syminfo.mintick, alert_message = message_entershort)
    
if strategy.position_size < 0 and timetoclose and enableclose
    strategy.close_all(alert_message = message_closelong)
if strategy.position_size > 0 and timetoclose and enableclose
    strategy.close_all(alert_message = message_closeshort)
    
if strategy.position_size < 0 and enablesltp and time_cond
    strategy.exit(id="Close Long", stop=longStop, limit=longTake, alert_message = message_closelong)
if strategy.position_size > 0 and enablesltp and time_cond
    strategy.exit(id="Close Short", stop=shortStop, limit=shortTake, alert_message = message_closeshort)





```

> Detail

https://www.fmz.com/strategy/430130

> Last Modified

2023-10-25 12:38:23
