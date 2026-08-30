
> Name

Breakout with the trend-Momentum-Breakout-Strategy-with-Volatility-Stop
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1d09e78abbf3275a2533fd31168019ff324f70f40afec246d031184bf28bda3b.png)
[trans]

### Overview
This strategy is a mid- to long-term trend following strategy designed based on breakouts and momentum stop-loss indicators. The strategy uses the price to break through the dynamic stop-loss line to determine the trend direction, enter the market when the price breaks through the stop-loss line, and then use the stop-loss line to track the trend and lock in profits. The strategy aims to capture medium and long-term trends while using dynamic stop loss to control risks.
### Strategy Principles
This strategy uses the Volatility Stop dynamic stop loss indicator to determine the trend direction and trail the stop loss. Volatility Stop calculates a dynamic stop loss line based on the price fluctuation range. The specific calculation method is:
1. Calculate the ATR (average true range) of the price
2. Get the stop loss line based on the ATR value multiplied by a stop loss coefficient
3. When the price rises, the highest price is recorded, and the stop loss line is the highest price minus ATR multiplied by the coefficient
4. When the price falls, the lowest price is recorded, and the stop loss line is the lowest price plus ATR multiplied by the coefficient
In this way, the stop loss line will fluctuate up and down as the price fluctuates, forming a dynamic channel.
When the price breaks through the stop-loss line, it indicates a trend reversal and the strategy will open a position:
- When the price breaks through the stop loss line from bottom to top, the strategy will open a long position
- When the price breaks through the stop loss line from top to bottom, the strategy will open a short position
After the position is opened, the strategy will use the stop loss line to track the stop loss:
- The stop loss line for long positions is the highest price minus ATR multiplied by the coefficient
- The stop loss line for short positions is the lowest price plus ATR multiplied by the coefficient
When the price reaches the stop loss line again, the strategy will close the position and stop the loss.
In this way, the strategy can ride the trend and track trend reversals in a timely manner, while using stop losses to control risk.
### Advantage Analysis
This strategy has the following advantages:
1. You can seize the trend reversal in time and follow the trend to avoid missing opportunities.
2. Using dynamic stop loss, you can adjust the stop loss position according to market fluctuations to make the stop loss more reasonable.
3. The stop loss position will be updated with the trend, which can lock in profits to the maximum extent
4. Take advantage of the trend and pursue it to gain greater profits from the trend.
5. Effectively control risks and avoid excessive losses
### Risk Analysis
There are also some risks with this strategy:
1. In volatile market conditions, stop loss may be triggered frequently.
2. The stop loss coefficient needs to be set reasonably. If it is too small, it will be too sensitive, and if it is too large, it will lose the meaning of stop loss.
3. You need to pay attention to the impact of transaction fees. Frequent transactions will occupy income.
4. Some profits from the early stages of the trend may be missed.
5. You need to pay attention to the risks caused by setting the stop loss line too far from the price.
Countermeasures:
1. You can optimize the stop loss coefficient through backtesting and find the best parameters.
2. Properly lengthen the trading time period and reduce the trading frequency
3. You can consider adding the filtrter filter to avoid too frequent transactions.
4. The stop loss line distance can be appropriately relaxed, but not too large
### Optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize the stop loss coefficient and find the best parameter combination
2. Add filters to avoid being caught in volatile market conditions
3. Combine multiple time periods for verification to improve signal quality
4. Optimize position management and gradually increase positions
5. Consider dynamically adjusting trading time periods
6. Select stocks based on stock fundamentals and grasp mainstream trends
### Summarize
This trend breakout-momentum stop loss strategy is overall a very practical trend following strategy. It can seize the opportunity of trend reversal and follow the trend, while using dynamic stop loss to effectively control risks. If the parameters are optimized properly, you can get better returns in the trend market. However, this strategy also needs to pay attention to some problems, such as too sensitive stop loss and too high trading frequency. Through further optimization, this strategy can become an efficient and stable quantitative trading system.
||

## Overview

This is a trend-following strategy based on breakout and volatility stop. The strategy identifies trend direction by price breakout of dynamic stop loss line. It enters trade when price penetrates the stop loss line and uses the stop loss line to track trends and lock in profits. The strategy aims to capture mid-long term trends while controlling risk with dynamic stops.

## Strategy Logic

The strategy utilizes Volatility Stop indicator to determine trend direction and track stop loss. Volatility Stop calculates a dynamic stop loss line based on price fluctuation range. The specific steps are:

1. Calculate ATR (Average True Range) of price 
2. Get stop loss line by multiplying ATR with a stop loss coefficient
3. When price goes up, record highest price, stop loss line is highest price minus ATR * coefficient
4. When price goes down, record lowest price, stop loss line is lowest price plus ATR * coefficient

The stop loss line fluctuates up and down with price, forming a dynamic channel. 

When price penetrates the stop loss line, it signals a trend reversal. The strategy will open position:

- When price breaks above stop loss line, go long
- When price breaks below stop loss line, go short

After opening position, the strategy tracks stop loss with the line:

- For long, stop loss is highest price minus ATR * coefficient 
- For short, stop loss is lowest price plus ATR * coefficient

When price hits the stop loss line again, the position will be closed.

This way, the strategy can follow trends in a timely manner while controlling risk with stops.

## Advantage Analysis 

The strategy has the following advantages:

1. Can capture trend reversals in a timely manner and follow the trend
2. Uses dynamic stop loss to adjust stop position based on market volatility
3. Stop loss updates with trend to lock in maximum profits
4. Rides the trend to achieve significant profit
5. Effectively controls risk and avoids huge losses

## Risk Analysis

There are also some risks to consider:

1. Stop loss may be triggered frequently during ranging markets
2. Need to set proper stop loss coefficient, too small may be too sensitive
3. Trading fees may eat up profits with frequent trading 
4. May miss some profits at early stage of trends
5. Risk when stop loss is too far from price

Solutions:

1. Optimize stop loss coefficient through backtest to find best parameter
2. Use longer time frames to lower trade frequency
3. Add filter to avoid over-trading
4. Allow some flexibility in stop distance but not too large

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Optimize stop loss coefficient to find best parameter combination
2. Add filters to avoid whipsaws in ranging market
3. Combine multiple timeframes for signal verification 
4. Optimize position sizing, gradually increase size
5. Consider dynamic adjustment of time frame
6. Combine with stock fundamentals to catch main trends

## Summary

Overall this momentum breakout strategy with volatility stop is a very practical trend following system. It can capture trend reversal opportunities and follow the trend while controlling risk effectively with dynamic stops. With proper parameter tuning, it can achieve good return during trending markets. But some issues need to be addressed like over-sensitive stops, high trading frequency etc. Further optimizations can turn it into an efficient and robust quant trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|true|From Day|
|v_input_3|2021|From Year|
|v_input_4|true|Thru Month|
|v_input_5|true|Thru Day|
|v_input_6|2112|Thru Year|
|v_input_7|true|Show Date Range|
|v_input_8|20|Length|
|v_input_9_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_10|3|vStop Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-11 00:00:00
end: 2023-11-12 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
//@version=4
strategy(shorttitle='Volatility Stop Strategy',title='Volatility Stop Strategy (by Coinrule)', overlay=true, initial_capital = 100, process_orders_on_close=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, commission_type=strategy.commission.percent, commission_value=0.1)

// Works better on 3h, 1h, 2h, 4h
// Best time frame 2H

//Backtest dates
fromMonth = input(defval = 1,    title = "From Month",      type = input.integer, minval = 1, maxval = 12)
fromDay   = input(defval = 1,    title = "From Day",        type = input.integer, minval = 1, maxval = 31)
fromYear  = input(defval = 2021, title = "From Year",       type = input.integer, minval = 1970)
thruMonth = input(defval = 1,    title = "Thru Month",      type = input.integer, minval = 1, maxval = 12)
thruDay   = input(defval = 1,    title = "Thru Day",        type = input.integer, minval = 1, maxval = 31)
thruYear  = input(defval = 2112, title = "Thru Year",       type = input.integer, minval = 1970)

showDate  = input(defval = true, title = "Show Date Range", type = input.bool)

start     = timestamp(fromYear, fromMonth, fromDay, 00, 00)        // backtest start window
finish    = timestamp(thruYear, thruMonth, thruDay, 23, 59)        // backtest finish window
window()  => time >= start and time <= finish ? true : false       // create function "within window of time"

length = input(20, "Length", minval = 2)
src = input(close, "Source")
factor = input(3.0, "vStop Multiplier", minval = 0.25, step = 0.25)
volStop(src, atrlen, atrfactor) =>
    var max     = src
    var min     = src
    var uptrend = true
    var stop    = 0.0
    atrM        = nz(atr(atrlen) * atrfactor, tr)
    max         := max(max, src)
    min         := min(min, src)
    stop        := nz(uptrend ? max(stop, max - atrM) : min(stop, min + atrM), src)
    uptrend     := src - stop >= 0.0
    if uptrend != nz(uptrend[1], true)
        max    := src
        min    := src
        stop   := uptrend ? max - atrM : min + atrM
    [stop, uptrend]

[vStop, uptrend] = volStop(src, length, factor)


//Entry 


strategy.entry(id="long", long = true, when = crossover(close, vStop) and window())

//Exit
strategy.close("long", when = crossunder(close, vStop))

plot(vStop,"Vstop", color.black, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/431962

> Last Modified

2023-11-13 17:20:51
