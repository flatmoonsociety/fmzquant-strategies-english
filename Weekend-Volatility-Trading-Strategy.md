
> Name

Weekend-Volatility-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11b42fbd318f4ddcab1.png)
[trans]

## Overview
This strategy sets the entry conditions for long and short positions based on Friday's closing price, going long and short when the market opens on Saturday and Sunday, and closing the position before the market opens on Monday. The strategy achieves profit by capturing price movements near Friday's closing price.
## Principle
1. Record Friday’s closing price as a reference price
2. When the market opens on Saturday and Sunday:
   - Go short if the price is above 4.5% of Friday's closing price
   - Go long if price is below 4.5% of Friday's closing price
3. The take profit is set to 3% of the initial capital.
4. Close all positions before the market opens on Monday
## Advantage Analysis
1. Take advantage of the price fluctuations caused by low trading volume on Saturdays and Sundays to trade and reduce market risks
2. Clear entry and exit conditions to reduce the difficulty of strategy implementation
3. Short-term operations, pursuing stable small profits
4. Short cycle and fast capital turnover
## Risk Analysis
1. Price fluctuations on Saturdays and Sundays may be smaller than expected and positions cannot be opened.
2. Excessive fluctuations lead to stop loss
3. Major events on Monday caused the price to jump short and the loss could not be stopped in time.
Risk Solutions:
1. Adjust the fluctuation range of entry conditions
2. Set stop loss points reasonably
3. Close positions in advance and do not hold positions over the weekend
## Optimization direction
1. Adjust the entry range according to the characteristics of different varieties
2. Optimize take-profit conditions based on backtest results
3. Choose different leverage according to fund size
4. Use moving average indicators to filter entry opportunities
## Summarize
As a short-term trading strategy, this strategy has very clear trading logic and risk control measures. Through reasonable parameter settings and continuous testing and optimization, stable investment returns can be obtained. At the same time, you also need to pay attention to the risk of loss caused by excessive price fluctuations on weekends, and control losses through risk management.
||


## Overview

This strategy sets long and short entry conditions based on Friday's closing price, and goes long or short after Saturday's and Sunday's opening, exiting all positions before Monday's opening. The strategy aims to profit from price fluctuations around Friday's closing price over the weekend.

## Principles 

1. Record Friday's closing price as the reference price
2. On Saturday and Sunday's opening:
   - If price is above 105% of Friday's close, go short
   - If price is below 95% of Friday's close, go long
3. Take profit is set at 3% of initial capital 
4. Close all positions before Monday's opening

## Advantage Analysis

1. Trade on weekend's low volume and volatility to reduce market risk
2. Clear entry and exit rules simplify strategy execution 
3. Pursue steady small profits with short-term trades
4. High capital turnover with short cycle

## Risk Analysis

1. Weekend price fluctuation may be smaller than expected, unable to open positions
2. Excessive volatility may cause stop loss
3. Significant events on Monday may cause price gaps, unable to stop loss in time

Risk Solutions:

1. Adjust fluctuation range for entries
2. Set proper stop loss points
3. Close positions early, avoid holding over weekends

## Optimization Guidelines

1. Adjust entry thresholds based on different products' characteristics
2. Optimize take profit rules based on backtest results
3. Select leverage based on capital size
4. Add indicator filters such as moving average to time entries

## Summary

This short-term trading strategy has very clear logic and risk control measures. With proper parameter tuning and continuous testing and optimization, it can generate steady investment returns. At the same time, the risk of large weekend losses due to excessive volatility needs to be managed via proper risk control.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Leverage|
|v_input_2|0.03|Profit Taking Percent Threshold|
|v_input_3|2017|Backtest Start Year|
|v_input_4|12|Backtest Start Month|
|v_input_5|10|Backtest Start Day|
|v_input_6|2025|Backtest Stop Year|
|v_input_7|12|Backtest Stop Month|
|v_input_8|30|Backtest Stop Day|
|v_input_9|true|Color Background?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-16 00:00:00
end: 2023-11-15 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Copyright Boris Kozak 
strategy("XBT Weekend Trade Strategy", overlay=true, default_qty_type=strategy.percent_of_equity,initial_capital=20000)
leverage = input(1,"Leverage")
profitTakingPercentThreshold = input(0.03,"Profit Taking Percent Threshold")

//****Code used for setting up backtesting.****///
testStartYear = input(2017, "Backtest Start Year")
testStartMonth = input(12, "Backtest Start Month")
testStartDay = input(10, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

testStopYear = input(2025, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(30, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,0,0)

// A switch to control background coloring of the test period
testPeriodBackground = input(title="Color Background?", type=bool, defval=true)
testPeriodBackgroundColor = testPeriodBackground and (time >= testPeriodStart) and (time <= testPeriodStop) ? #00FFFF : na
bgcolor(testPeriodBackgroundColor, transp=50)

testPeriod() => true
    
//****END Code used for setting up backtesting.****///


//*** Main entry point is here***//
// Figure out how many days since the Friday close 
days_since_friday = if dayofweek == 6
    0
else 
    if dayofweek == 7
        1
    else
        if dayofweek == 1
            2
        else
            if dayofweek == 2
                3
            else
                if dayofweek == 3
                    4
                else
                    if dayofweek == 4
                        5
                    else
                        6
    
// Grab the Friday close price
fridaycloseprice = request.security(syminfo.tickerid,'D',close[days_since_friday])
plot(fridaycloseprice)
strategy.initial_capital = 50000
// Only perform backtesting during the window specified 
if testPeriod()
    // If we've reached out profit threshold, exit all positions 
    if ((strategy.openprofit/strategy.initial_capital) > profitTakingPercentThreshold)
        strategy.close_all()
    // Only execute this trade on saturday and sunday (UTC)
    if (dayofweek == 7.0 or dayofweek == 1.0)
        // Begin - Empty position (no active trades)
        if (strategy.position_size == 0)
            // If current close price > threshold, go short 
            if ((close>fridaycloseprice*1.045))
                strategy.entry("Short Entry", strategy.short, leverage)
            else
                // If current close price < threshold, go long
                if (close<(fridaycloseprice*0.955))
                    strategy.entry("Long Entry",strategy.long, leverage)
        // Begin - we already have a position
        if (abs(strategy.position_size) > 0)
            // We are short 
            if (strategy.position_size < 0)
                if ((close>strategy.position_avg_price*1.045))
                    // Add to the position
                    strategy.entry("Adding to Short Entry", strategy.short, leverage)
            else
                strategy.entry("Long Entry",strategy.long,leverage)
    // On Monday, if we have any open positions, close them 
    if (dayofweek==2.0)
        strategy.close_all()
 





```

> Detail

https://www.fmz.com/strategy/432304

> Last Modified

2023-11-16 10:53:01
