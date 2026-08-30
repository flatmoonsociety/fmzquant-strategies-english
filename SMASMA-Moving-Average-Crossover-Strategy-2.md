
> Name

SMA Moving Average Crossover Strategy SMA-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a simple trend following strategy based on SMA moving average crossovers, suitable for trading Bitcoin and other cryptocurrencies on higher time periods.
## Strategy Principle
This strategy is based on two SMA moving averages with different periods. One is a 10-period SMA and the other is a 100-period SMA. The strategy continues to monitor the values ​​of these two SMAs. When the shorter 10-period SMA crosses the longer 100-period SMA from below, it indicates that the price trend has changed to an upward trend. At this time, the strategy takes a long direction and enters the market. On the contrary, when the 10-period SMA crosses the 100-period SMA from above, it indicates that the price trend has turned downward, and the strategy will enter the market in the short direction.
Specifically, this strategy compares the values ​​of the 10-period SMA and the 100-period SMA to determine their crossover. If the 10-period SMA crosses above the 100-period SMA, set the longCondition condition to true. At this time, the strategy enters the market in the long direction through the strategy.entry function. On the contrary, if the 10-period SMA crosses below the 100-period SMA, set the shortCondition condition to true. At this time, the strategy takes the short direction and enters the market through strategy.entry.
Through this simple SMA cross judgment, this strategy can seize the turning point of the price trend and achieve timely entry and exit. When the short-period SMA crosses above the long-period SMA, seize the opportunity to rise; when the short-period SMA crosses below the long-period SMA, seize the opportunity to fall.
## Strategic Advantages
1. The strategic ideas are simple and clear, easy to understand and implement, and suitable for novices to learn.
2. Based on SMA cross judgment, you can effectively capture the turning point of the price trend and enter the market in time.
3. Moving averages can effectively filter market noise and identify trend directions.
4. The SMA cycle can be adjusted to adapt to different market environments. For example, the cycle can be shortened in a bull market, and the cycle can be lengthened in a bear market.
5. This strategy has been proven for a long time and works well in the cryptocurrency market.
## Strategy Risk
1. There is a lag in the SMA crossover, which may lead to late entry points and stop loss risks.
2. Short-period SMA is prone to false breakthroughs, which may lead to unnecessary repeated transactions.
3. When holding positions for a long time, stop loss points need to be set to control risks.
4. If the market shock is effectively filtered, trading losses will occur frequently. It needs to be judged in conjunction with other indicators.
5. Improper parameter settings will also affect the strategy effect. The SMA cycle needs to be adjusted according to the market.
## Strategy optimization
1. Other indicators can be introduced to combine with SMA judgment, such as RSI, Bollinger Bands, etc., to improve the accuracy of the strategy.
2. A stop loss mechanism can be added. Stop loss if the price breaks through the SMA.
3. SMA parameters can be dynamically adjusted according to market conditions, appropriately shortening the cycle in a bull market and lengthening the cycle in a bear market.
4. Different position sizes can be set according to the strength of the long and short period SMA crossover.
5. You can set up a re-entry mechanism. If the price returns to the SMA, enter again.
6. Parameter settings and strategy effects can be evaluated through backtesting and simulation exercises.
## Summarize
The overall idea of ​​the SMA moving average crossover strategy is simple and clear, easy to understand and implement. It uses the crossover judgment of two different period SMAs to capture the turning point of the price trend. It is a relatively classic trend following strategy. The advantage of this strategy is that it has direct ideas, clear trading signals, and can effectively track trends; its disadvantage is that it may lag entry and produce false breakthroughs. We can optimize by introducing other indicators and cooperate with the stop-loss mechanism to control risks, thereby comprehensively improving the actual effectiveness of this strategy. Through continuous optimization and verification, this strategy can become a very practical trend strategy choice in cryptocurrency trading.
||

## Overview

This is a simple trend following crossover strategy based on SMA moving averages, suitable for higher timeframes for trading BTCUSD and other crypto pairs.

## Strategy Logic

The strategy is based on two SMA moving averages with different periods. One is a 10-period SMA, the other is a 100-period SMA. The strategy keeps monitoring the values of the two SMAs. When the shorter 10-period SMA crosses above the longer 100-period SMA, it signals an uptrend, and the strategy goes long. When the 10-period SMA crosses below the 100-period SMA, it signals a downtrend, and the strategy goes short.

Specifically, the strategy determines the crossover by comparing the values of the 10-period SMA and 100-period SMA. If the 10-period SMA crosses above the 100-period SMA, the longCondition is set to true. The strategy then goes long through the strategy.entry function. Conversely, if the 10-period SMA crosses below the 100-period SMA, the shortCondition is set to true. The strategy then goes short through strategy.entry.

Through this simple SMA crossover system, the strategy can capture trend reversal points and get in and out of the market in a timely manner. It goes long when the shorter SMA crosses above the longer SMA, and goes short when the shorter SMA crosses below the longer SMA.

## Advantages

1. The logic is simple and clear, easy to understand and implement, suitable for beginners.

2. SMA crossover can effectively capture trend reversal points and enter the market in a timely manner. 

3. Moving averages can filter out market noise and identify trend directions.

4. The SMA periods can be adjusted for different market environments. For example, shorter periods for bull market and longer periods for bear market.

5. The strategy has been validated for a long time and works well in crypto markets.

## Risks

1. SMA crossover may lag and cause late entry and stop loss risks.

2. Shorter SMA may generate false breakouts and cause unnecessary whipsaws.

3. Need to set stop loss when holding positions for long term.

4. May lead to frequent losing trades in ranging markets. Need to combine with other indicators.

5. Inappropriate parameter settings may affect strategy performance. SMA periods need to be adjusted per market conditions.

## Enhancements

1. Combine SMA with other indicators like RSI, Bollinger Bands to improve accuracy.

2. Add stop loss mechanisms, like SMA breakout stop loss. 

3. Dynamically adjust SMA parameters based on market conditions, shorter periods for bull market and longer periods for bear market.

4. Use different position sizing based on crossover strength of short and long SMAs.

5. Add re-entry rules, like re-enter when price reverts to SMA.

6. Evaluate parameters and strategy through backtesting and paper trading.

## Summary

The SMA crossover strategy has simple and clear logic, easy to understand and implement. It captures trend reversal points through crossover of two SMAs with different periods. It is a classical trend following strategy. The advantages are direct logic and clear trading signals, able to track trends effectively. The disadvantages are possible lagging entry and false breakouts. We can optimize it by introducing other indicators and stop loss mechanisms to control risks and improve practical results. With continuous optimization and verification, this strategy can become a very useful trend following strategy for crypto trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|10|1st MA Length|
|v_input_3|0|1st MA Type: SMA|EMA|
|v_input_4|100|2nd MA Length|
|v_input_5|0|2nd MA Type: SMA|EMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-22 00:00:00
end: 2023-09-21 00:00:00
period: 6h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//study(title="MA Crossover Strategy", overlay = true)
// Simple MA crossover strategy with a 10/100 MA crossover)

strategy("MA Crossover Strategy", overlay=true)
src = input(close, title="Source")

price = security(syminfo.tickerid, timeframe.period, src)
ma1 = input(10, title="1st MA Length")
type1 = input("SMA", "1st MA Type", options=["SMA", "EMA"])

ma2 = input(100, title="2nd MA Length")
type2 = input("SMA", "2nd MA Type", options=["SMA", "EMA"])

price1 = if (type1 == "SMA")
    sma(price, ma1)
else
    ema(price, ma1)
    
price2 = if (type2 == "SMA")
    sma(price, ma2)
else
    ema(price, ma2)


//plot(series=price, style=line,  title="Price", color=black, linewidth=1, transp=0)
plot(series=price1, style=line,  title="1st MA", color=blue, linewidth=2, transp=0)
plot(series=price2, style=line, title="2nd MA", color=green, linewidth=2, transp=0)


longCondition = crossover(price1, price2)
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = crossunder(price1, price2)
if (shortCondition)
    strategy.entry("Short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/427593

> Last Modified

2023-09-22 14:40:03
