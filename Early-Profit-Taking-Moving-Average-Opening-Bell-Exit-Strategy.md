
> Name

Early-Profit-Taking-Moving-Average-Opening-Bell-Exit-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10ea8fd0712717d263e.png)

[trans]

## Overview
This strategy is based on the golden cross and dead cross of the moving average to achieve long and short long and short positions. At the same time, based on the statistical data of profit opportunities, only stop loss and take profit are closed in the afternoon to avoid being trapped by the high volatility in early trading.
## Strategy Principle
This strategy uses 3 moving averages with different parameters: the 14-day line, the 28-day line, and the 56-day line. Go long when the 14-day line crosses the 56-day line; go short when the 14-day line crosses below the 56-day line. This is the basic method of tracking long-term trends. In order to filter out some noise, the strategy also adds the 28-day line as a reference. A trading signal will be issued only when the 14-day line is above or below the 28-day line at the same time.
The key innovation of this strategy is that it only takes profits and stops between 4pm and 5pm. According to statistics, there is a 70% probability that the highest price and lowest price of a day will occur within the first hour of opening. In order to avoid the impact of high volatility on the strategy during the opening hours, stop loss and take profit are only conducted during the afternoon trading session.
## Advantage Analysis
This strategy has several advantages:
1. Track mid- to long-term trends and avoid being affected by too much noise
2. Use the statistical characteristics of high opening volatility to design stop-loss and take-profit logic to effectively avoid false breakthroughs
3. Simple and intuitive ideas, easy to understand and modify
## Risks and Solutions
This strategy also has the following risks:
1. If the trend reverses in early trading, you will miss the opportunity. Can be tested for suitability for the characteristics of the stock itself.  
2. If the market continues to fluctuate significantly after the market opens, there is still a risk of being trapped. You can test to appropriately relax the stop loss range.  
3. Improper setting of the backtest time interval may lead to overfitting. The backtesting period should be expanded.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Test different moving average combinations to find optimal parameters
2. Fine-tune the stop loss range according to the fluctuation characteristics of specific stocks.
3. Filter signals based on trading volume to avoid being trapped
4. Add dynamic stop loss and track the retracement after the breakthrough
## Summarize
The overall idea of ​​this strategy is clear and easy to understand. It effectively uses the opening characteristics to design stop-loss logic, which can avoid being stuck in the high volatility of early trading. It is worthy of further testing and optimization. However, there are also risks of being trapped and missing opportunities, and parameters need to be adjusted for individual stocks. Overall, this strategy provides a simple and effective quantitative trading idea for beginners.
||

## Overview  

This strategy implements long and short based on moving average crossovers, and exits only in the afternoon based on early profit-taking statistics to avoid being trapped by high opening volatility.

## Strategy Logic   

The strategy uses 3 moving averages with different parameters: 14-day, 28-day and 56-day lines. It goes long when the 14-day line crosses above the 56-day one, and goes short when crossing below. This basic approach tracks long-term trends. To filter out some noise, the 28-day line is added as a reference, so that signals are triggered only when the 14-day line is also above or below the 28-day one.  

The key innovation is that it stops loss and takes profit only between 4 pm and 5 pm. Statistics show 70% chance of daily high/low happening in the first hour after opening. To avoid impact from high opening volatility, exits are enabled only during regular afternoon trading hours.  

## Advantage Analysis

The advantages of this strategy include:

1. Track mid-long term trends, avoid excessive noise  
2. Utilize statistics of opening volatility for stop loss logic to avoid false breakouts
3. Simple and intuitive logic, easy to understand and modify

## Risks and Solutions  

There are also some risks:   

1. Missing opportunities if reversal happens early in the day. Can test compatibility with specific stocks.
2. Still risks of being trapped after hours. Can test loosening stop loss range.   
3. Bad setting of backtest period leading to overfitting. Should expand backtest duration.  

## Enhancement Opportunities   

Some ways to further optimize the strategy:  

1. Test different moving average combinations to find optimum parameters
2. Fine tune stop loss range based on volatility patterns of specific stocks  
3. Add volume filter to avoid traps
4. Add dynamic stops to trail pullbacks after breakouts
  
## Conclusion
  
The strategy has clear and simple logic, effectively uses opening features for stop loss to avoid volatility traps. But risks exist of missing chances and being trapped. Parameters should be adjusted per stock. Overall a simple yet effective idea for novice quants.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2014|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|2|Backtest Start Day|
|v_input_4|2025|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|30|Backtest Stop Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-23 00:00:00
end: 2023-11-30 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("MAC 1st Trading Hour Walkover", overlay=true)

// Setting up timeperiod for testing
startPeriodYear = input(2014, "Backtest Start Year")
startPeriodMonth = input(1, "Backtest Start Month")
startPeriodDay = input(2, "Backtest Start Day")
testPeriodStart = timestamp(startPeriodYear, startPeriodMonth, startPeriodDay, 0, 0)

stopPeriodYear = input(2025, "Backtest Stop Year")
stopPeriodMonth = input(12, "Backtest Stop Month")
stopPeriodDay = input(30, "Backtest Stop Day")
testPeriodStop = timestamp(stopPeriodYear, stopPeriodMonth, stopPeriodDay, 0, 0)

// Moving Averages
ema14 = ema(close, 14)
ema28 = ema(close, 28)
sma56 = sma(close, 56)

// Plot
plot(ema14, title="ema14", linewidth=2, color=green)
plot(ema28, title="ema28", linewidth=2, color=red)
plot(sma56, title="sma56", linewidth=3, color=blue)

// Strategy
goLong = cross(ema14, sma56) and ema14 > ema28
goShort = cross(ema14, sma56) and ema14 < ema28

// Strategy.When to enter
if time >= testPeriodStart
    if time <= testPeriodStop
        strategy.entry("Go Long", strategy.long, 1.0, when=goLong)
        strategy.entry("Go Short", strategy.short, 1.0, when=goShort)

// Strategy.When to take profit 
if time >= testPeriodStart 
    if time <= testPeriodStop 
        strategy.exit("Close Long", "Go Long", profit=2000) 
        strategy.exit("Close Short", "Go Short", profit=2000) 

// Strategy.When to stop out 
// Some studies show that 70% of the days high low happen in the first hour 
// of trading. To avoid having that volatility fire our loss stop we 
// ignore price action in the morning, but allow stops to fire in the afternoon. 
if time("60", "1000-1600") 
    strategy.exit("Close Long", "Go Long", loss=500) 
    strategy.exit("Close Short", "Go Short", loss=500)
```

> Detail

https://www.fmz.com/strategy/433918

> Last Modified

2023-12-01 14:32:48
