
> Name

Quant-Trading-Strategy-Based-on-Monthly-and-Quarterly-Moving-Average-Operation based on monthly moving average operation
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ad964b62e655ee3ba9dca49ba20594bdbe6f27ff9928bf56999db99b6b96d4c2.png)
[trans]

## Overview
This strategy is mainly based on the monthly and quarterly moving averages. Specifically, the 20-day line is used as the monthly line, and the 60-day line is used as the quarterly line. The source of the strategy signal is the golden cross of the two moving averages. When the monthly line crosses the quarterly line, a long signal is formed; when the monthly line crosses the quarterly line, the position is cleared. This strategy is suitable for medium and long-term operations and makes profits by capturing consolidation and divergence opportunities.
## Strategy Principle
This strategy uses the 20-day simple moving average as the monthly indicator and the 60-day simple moving average as the quarterly indicator. The specific trading signal generation logic is as follows:
1. When the 20-day line crosses the 60-day line, that is, when a golden cross occurs, enter the market long.  
2. When the stock price retraces more than 10% from the highest point within 10 days, close the position and take profit.  
3. When the 20-day line crosses below the 60-day line, a dead cross occurs, clear the position.
4. When the loss reaches 10%, stop loss and exit.
The mid- and long-term trends are judged by the intersection of the monthly and quarterly moving averages. A long golden cross indicates entry into a mid- to long-term bull market, and a short dead cross indicates entry into a mid- to long-term bear market. At the same time, control risks by combining take-profit and stop-loss strategies.
## Strategic Advantages
1. Use monthly moving averages to filter out market noise and capture medium and long-term trends.
2. The strategy parameters are simple and easy to implement.
3. You can configure stop-profit and stop-loss parameters to control risks.
## Risk Analysis
1. The trend reversal point cannot be determined and there is a risk of loss.  
2. There is a lag between the monthly and quarterly moving averages, and short-term opportunities may be missed.
3. It is necessary to select an appropriate stop loss point to avoid being too aggressive and being out immediately.
**Solution:**
1. Use trailing stop loss tracking to stop losses in time.
2. Combine with other indicators to filter signals and determine trends. 
3. Adjust the moving average parameters and optimize the strategy.
## Strategy optimization direction
1. Add other indicator filters, such as KD indicator, etc., to avoid false breakthroughs. 
2. Optimize the moving average parameters and find the best moving average period combination.
3. Add take-profit strategies, such as moving take-profit, etc., to obtain more profits.
## Summarize
This strategy's Overall XXXXX system atically takes advantage of the monthly and quarterly moving averages and determines the medium and long-term trend direction through the gold and silver crosses of the moving averages. At the same time, configure a reasonable stop-profit and stop-loss mechanism to control risks. There is still a lot of room for strategy optimization, which deserves further testing and optimization.
||

## Overview

This strategy is mainly based on the moving averages of monthly and quarterly lines for operation. Specifically, the 20-day line is used as the monthly line and the 60-day line as the quarterly line. The strategy signals come from the golden cross and death cross of the two moving averages. When the monthly line crosses above the quarterly line, go long; when the monthly line falls below the quarterly line, close positions. This strategy is suitable for medium- and long-term operations to capture consolidation and divergence opportunities.  

## Strategy Logic

This strategy uses the 20-day simple moving average as the monthly line indicator and the 60-day simple moving average as the quarterly line indicator. The specific trading signal generation logic is as follows:

1. When the 20-day line crosses above the 60-day line, that is, a golden cross occurs, go long.
2. When the price retreats more than 10% from the highest point in the last 10 days, close long positions for profit taking.
3. When the 20-day line crosses below the 60-day line, that is, a death cross occurs, close all positions. 
4. When the loss reaches 10%, stop loss.

Use the moving average crossovers of monthly and quarterly lines to determine medium- and long-term trends. The golden cross for going long indicates the start of a medium- and long-term bull market, while the death cross for going short indicates the start of a medium- and long-term bear market. At the same time, use stop profit and stop loss strategies to control risks.  

## Advantages of the Strategy  

1. Using monthly and quarterly moving averages filters out market noise and captures medium- and long-term trends.  
2. The strategy parameters are simple and easy to implement.
3. Customizable take profit and stop loss parameters to control risks.   

## Risk Analysis   

1. Unable to determine trend reversal points, with risk of losses.
2. Monthly and quarterly moving averages have lagging effects, potentially missing short-term opportunities.  
3. Need to select appropriate stop loss points to avoid being stopped out too quickly.   

**Solutions:**   

1. Adopt trailing stop loss to stop out in a timely manner.  
2. Incorporate other indicators to filter signals and determine trends.   
3. Adjust moving average parameters to optimize the strategy.   

## Directions for Strategy Optimization  

1. Add other indicators for filtering, such as KD indicator, etc., to avoid false breakouts.   
2. Optimize moving average parameters to find the best parameter combination. 
3. Incorporate additional take profit strategies such as trailing take profit to capture more profits.   

## Summary

This strategy systematically utilizes the advantages of monthly and quarterly moving averages by judging medium- and long-term trend directions through golden cross and death cross of the moving averages. At the same time, reasonable stop loss and take profit mechanisms are configured to control risks. There is still much room for optimizing this strategy, worth further testing and optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2020|backtest_year|
|v_input_2|10|backtest_month|
|v_input_3|true|backtest_date|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-08 00:00:00
end: 2023-12-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("均線操作-月季", overlay=true, initial_capital = 100000, default_qty_type = strategy.percent_of_equity, default_qty_value = 30)
sma20 = sma(close, 20)
sma60 = sma(close, 60)

plot(sma20, title="月線", color=color.purple,linewidth=2)
plot(sma60, title="季線", color=color.yellow,linewidth=2)

backtest_year = input(title="backtest_year",type=input.integer,defval=2020)
backtest_month = input(title="backtest_month",type=input.integer,defval=10)
backtest_date = input(title="backtest_date",type=input.integer,defval=1)
backtest_start_time = timestamp(backtest_year,backtest_month,backtest_date,0,0,0)

to_long = sma20 > sma60  and close > highest(10)*0.9 // 黃金交叉
to_close = sma20 < sma60 // 死亡交叉
to_exit = close < highest(10)*0.9 //股價嚴重回檔
to_stop = close < 0.9*strategy.position_avg_price 

// to_long = crossover(sma20, sma60)   // 黃金交叉
// to_close = crossunder(sma20, sma60) // 死亡交叉

//plotchar(to_long, char="B", text="買", color=color.red, location=location.belowbar)
//plotchar(to_close, char="S", text="賣", color=color.green, location=location.abovebar)
//strategy.close("open long",when = tslide, comment="多單滑價7%出場")
if true
    strategy.entry("golden", strategy.long,  when=to_long,comment="多單入場")
    strategy.close("golden",  when=to_exit,comment="多單滑價7%出場")
    strategy.close("golden",  when=to_close,comment="月線季線死亡交叉")
    strategy.close("golden",  when=to_stop,comment="虧損10%強迫停損")

```

> Detail

https://www.fmz.com/strategy/435484

> Last Modified

2023-12-15 11:49:06
