
> Name

Multi-level-Moving-Average-Crossing-Strategy-for-Quant-Masters
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/a4084cb7316bb1d874.png)
[trans]

## Overview
This strategy uses the crossover principle of multi-level moving averages to capture medium and long-term trends and achieve stable profits. The strategy uses three groups of fast, medium and slow moving averages with different parameters, and makes trading decisions based on their intersections. This multi-level moving average crossover strategy, compared with the traditional strategy of only two sets of moving averages, can filter out more false signals and improve the strategy's winning rate.
## Strategy Principle
This strategy uses three groups of moving averages: fast moving average MAshort, medium moving average MAmid and slow moving average MAlong. Among them, the MAshort parameter is 9, the fastest response, used to capture short-term signals; the MAmid parameter is 50, the speed is moderate, used to confirm the trend; the MAlong parameter is 100, the slowest response, used to determine the long-term trend direction.
The specific trading logic of the strategy is: when the medium-speed moving average MAmid crosses the slow moving average MAlong, it indicates that the rising momentum of the stock price is forming, and the strategy is long; when the fast moving average MAshort crosses below the medium-speed moving average MAmid, it means that the short-term trend has turned, and the strategy will close the position at this time.
The biggest advantage of this strategy is that through the combination and matching of multiple sets of moving averages, false signals can be effectively filtered, and only the more powerful breakthroughs in the medium and long-term upward trend are selected to build long positions.
## Advantage Analysis
This strategy has the following advantages:
1. The strategy parameters have been optimized to effectively match the medium and long-term trends and have a high winning rate.
2. Multi-level moving average design can filter out noise and false signals
3. Applicable to all types of stocks and digital currencies, with good historical backtesting results
4. The operation frequency is not high, each opening of a position takes up 30% of the funds, and the risk is controllable.
5. Configurable time period, high flexibility of real offer
## Risk Analysis
This strategy also has the following risks:
1. The probability of a sudden turning point in the long-term trend is small, but once it occurs, the stop loss range may be larger
2. The transaction frequency is not high, and there is a certain degree of low capital utilization.
3. Strategy parameters need to be optimized according to different trading varieties, and their applicability may be limited.
In response to the above risks, we will further expand the applicable scope of the strategy and combine it with stop-loss technology to control the maximum drawdown. When the mid- to long-term trend turns, we will respond by reducing our positions.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Optimize the daily parameters of the moving average and find a better parameter combination
2. Increase trading volume indicators for confirmation to avoid curve fitting problems
3. Set the maximum loss value of the strategy, such as a maximum retracement of 20% and forced stop loss.
4. Add machine learning models to judge trends and improve the adaptive ability of the strategy
## Summary
This strategy is a typical medium- and long-term quantitative strategy. It matches WebDriverWait==long term trend through the multi-level moving average to achieve sustained profits while controlling transaction risks. Compared with a single indicator, this strategy integrates multiple sets of parameters and can effectively identify stronger medium and long-term trend signals. Through further optimization, this strategy can be applied to more varieties and play an important role in the field of quantitative trading.
|| 

# Overview
This strategy utilizes the principle of multi-level moving average line crossing to capture medium-long term trends and achieve steady profits. It employs fast, medium, and slow three sets of moving averages with different parameters and makes trading decisions based on their crossovers. Compared to traditional strategies with only two sets of moving averages, this multi-level moving average crossing strategy can filter out more false signals and improve the win rate of the strategy.  

## Strategy Logic
The strategy uses three sets of moving averages: the fast moving average MAshort, the medium speed moving average MAmid, and the slow moving average MAlong. MAshort has a parameter of 9, responds the fastest, and is used to capture short-term signals; MAmid has a parameter of 50, has a medium speed and is used to confirm the trend; MAlong has a parameter of 100, responds the slowest and is used to determine long-term trend direction.  

The specific trading logic of the strategy is: when the medium speed moving average line MAmid crosses above the slow moving average line MAlong, it indicates that the upward momentum of the stock price is forming. At this time, the strategy goes long; when the fast moving average MAshort crosses below the medium speed moving average MAmid, it indicates that a short-term trend reversal has occurred, and the strategy exits its position at this time.  

The biggest advantage of this strategy is that by combining multiple moving averages, it can effectively filter out false signals and only choose relatively strong breakouts during a medium-long term uptrend to open long positions.

## Advantage Analysis  
The advantages of this strategy are:
1. The strategy parameters are optimized to effectively match the medium and long term trends with a relatively high win rate.  
2. The multi-level moving average design filters noise and false signals.  
3. It is suitable for all kinds of stocks and cryptocurrencies with relatively good historical backtesting results.  
4. The operation frequency is low and each opening position occupies 30% of the funds and the risk is controllable.  
5. The time period is configurable, which provides flexibility for live trading.

## Risk Analysis
This strategy also has the following risks:  
1. The probability of long-term trend reversals is relatively small but when it does happen, the stop loss magnitude may be large.  
2. The trading frequency is low and therefore has the problem of inefficient capital utilization.
3. The parameters of the strategy need to be optimized for different trading varieties, which limits the applicable scope. 

To address these risks, we will further expand the applicability of the strategy while controlling maximum drawdown with stop loss techniques. We will respond to the reversal of the medium and long term trend by reducing positions.

## Optimization Directions
This strategy can also be optimized in the following ways:
1. Optimize the days parameter of the moving average to find the best parameter combination  
2. Add volume indicators to confirm and avoid curve fitting problems  
3. Set the maximum loss for the strategy, such as 20% max drawdown, to force stop loss  
4. Incorporate machine learning models to judge trends and improve the adaptability of the strategy   

## Summary
This strategy belongs to a typical medium-long term quantitative strategy which, with the premise of controlling trading risks, continuously profits by matching multi-level moving averages with medium-long term trends. Compared with a single indicator, this strategy incorporates multiple parameters and can effectively identify strong medium and long term trend signals. Through further optimization, this strategy can be applied to more varieties and play an important role in quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|true|From Day|
|v_input_3|2020|From Year|
|v_input_4|true|Thru Month|
|v_input_5|true|Thru Day|
|v_input_6|2112|Thru Year|
|v_input_7|true|Show Date Range|
|v_input_8|100|MAlong|
|v_input_9|50|MAmid|
|v_input_10|9|MAfast|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-12 00:00:00
end: 2024-01-11 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=4
strategy(shorttitle='Multi Moving Average Crossing',title='Multi Moving Average Crossing (by Coinrule)', overlay=true, initial_capital=1000,  default_qty_type = strategy.percent_of_equity, default_qty_value = 30, commission_type=strategy.commission.percent, commission_value=0.1)

//Backtest dates
fromMonth = input(defval = 1,    title = "From Month",      type = input.integer, minval = 1, maxval = 12)
fromDay   = input(defval = 1,    title = "From Day",        type = input.integer, minval = 1, maxval = 31)
fromYear  = input(defval = 2020, title = "From Year",       type = input.integer, minval = 1970)
thruMonth = input(defval = 1,    title = "Thru Month",      type = input.integer, minval = 1, maxval = 12)
thruDay   = input(defval = 1,    title = "Thru Day",        type = input.integer, minval = 1, maxval = 31)
thruYear  = input(defval = 2112, title = "Thru Year",       type = input.integer, minval = 1970)

showDate  = input(defval = true, title = "Show Date Range", type = input.bool)

start     = timestamp(fromYear, fromMonth, fromDay, 00, 00)        // backtest start window
finish    = timestamp(thruYear, thruMonth, thruDay, 23, 59)        // backtest finish window
window()  => true       // create function "within window of time"

//MA inputs and calculations
inlong=input(100, title='MAlong')
inmid=input(50, title='MAmid')
inshort=input(9, title='MAfast')

MAlong = sma(close, inlong)
MAshort= sma(close, inshort)
MAmid= sma(close, inmid)


//Entry 
bullish = crossover(MAmid, MAlong)

strategy.entry(id="long", long = true, when = bullish and window())

//Exit
bearish = crossunder(MAshort, MAmid)

strategy.close("long", when = bearish and window())

plot(MAshort, color=color.orange, linewidth=2)
plot(MAmid, color=color.red, linewidth=2)
plot(MAlong, color=color.blue, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/438470

> Last Modified

2024-01-12 12:11:02
