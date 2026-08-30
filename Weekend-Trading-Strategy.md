
> Name

Weekend-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18faa73293da2f128bd.png)
[trans] 

## Overview
This strategy is a strategy for short-term trading using Bitcoin on weekends, using 10x leverage for trading. The main idea of ​​the strategy is to record the price at the close on Friday, and then compare the increase or decrease between the closing price on that day and the closing price on Friday on Saturday and Sunday. If it exceeds the threshold, go long or short, and close the position on Monday.
## Strategy Principle
This strategy first records Friday's closing price, and then calculates the number of days from the current date to Friday. On Saturday and Sunday, if the closing price of the day rises by more than 4.5% from the closing price of Friday, then go short; if the closing price of the day falls by more than 4.5% from the closing price of Friday, go long. Use 10 times leverage for each transaction. If the profit reaches 10% of the initial capital, all positions will be closed. Regardless of whether there are positions on Monday, all positions will be closed.
Specifically, the strategy obtains Friday's closing price, and then compares the increase or decrease between the current closing price and Friday's closing price on Saturday and Sunday. If the current closing price rises by more than 4.5% from Friday's closing price, go short through `strategy.short`; if the current closing price falls by more than 4.5% from Friday's closing price, go long through `strategy.long`. Set the leverage to 10 times through the `leverage` ​​parameter. If the profit reaches 10% of the initial capital, all positions will be closed through `strategy.close_all()`. On Monday, close all positions via `strategy.close_all()`.
## Advantage Analysis
- Take advantage of the increased trading volume of Bitcoin on weekends and conduct short-term trading on weekends to capture the short-term trend over the weekend.
- Use 10 times leverage to trade, which can magnify profits
- Set profit-taking conditions to facilitate timely profit-taking and avoid loss expansion.
- Close positions on Monday to avoid the risks caused by large fluctuations in the market opening on Monday
## Risk Analysis
- Bitcoin prices fluctuate greatly over the weekend, and there is a risk of loss
- 10x leverage will magnify losses
- Improper stop loss setting may result in larger losses
- The opening price on Monday fluctuates violently, and it may not be possible to take profits entirely
For risks, the following optimization measures can be considered:
1. Set a stop loss point to control single loss.
2. Adjust the leverage ratio to reduce risks.
3. Optimize the setting of profit stop points and stop profits in batches when the profit reaches a certain proportion.
4. Set a trading volume or time take profit before Monday’s opening to avoid violent fluctuations at Monday’s opening.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add other indicators to judge and optimize the selection of entry points. You can combine moving averages, RSI and other indicators to filter entry opportunities and improve entry accuracy.
2. Optimize the stop loss and take profit strategy, lock in profits and control risks through moving stop loss, batch take profit, etc.
3. Adjust the leverage size to reduce risks. You can set the leverage ratio to dynamically adjust and reduce the leverage during retracement.
4. Add multi-variety transactions. You can add other common cryptocurrencies and use their weekend trading characteristics to conduct multi-variety arbitrage transactions.
5. Use machine learning algorithms to optimize parameters. A large amount of historical data can be collected, and machine learning algorithms can be used to automatically optimize parameters and achieve dynamic adjustment of parameters.
## Summarize
This strategy is a typical short-term trading strategy that takes advantage of the amplification of Bitcoin’s weekend trading volume. The strategy takes advantage of the amplified trading volume of Bitcoin on weekends to judge trends on Saturdays and Sundays and go long or short. The strategy has the advantages of profit amplification and risk control, but it also has certain risks. The next step can be optimization from aspects such as entry, stop loss and profit, leverage management, variety expansion, etc. to make the strategy more robust and intelligent.
||
## Overview

This is a short-term trading strategy that utilizes Bitcoin's increased weekend trading volume using 10x leverage. The main idea is to record the Friday closing price, compare the daily closing prices on Saturday and Sunday with the Friday closing price, and go long or short if the threshold is exceeded. Positions will be closed on Monday.  

## Strategy Logic

The strategy first records the Friday closing price, then calculates the number of days since Friday. On Saturday and Sunday, if the daily closing price is more than 4.5% above the Friday closing price, go short; if the daily closing price is more than 4.5% below the Friday closing price, go long. Each trade uses 10x leverage. If the profit reaches 10% of the initial capital, close all positions. On Monday, close all positions regardless.

Specifically, the strategy gets Friday's closing price, then compares the current closing price with Friday's on Saturday and Sunday. If the current closing price is more than 4.5% higher than Friday's, go short via `strategy.short`; if the current closing price is more than 4.5% lower than Friday's, go long via `strategy.long`. Leverage is set to 10x via the `leverage` parameter. If profit reaches 10% of initial capital, close all positions via `strategy.close_all()`. On Monday, close all positions via `strategy.close_all()`.

## Advantage Analysis 

- Utilizes Bitcoin's increased weekend trading volume for short-term trading, capturing weekend trends
- 10x leverage amplifies returns
- Take profit condition helps lock in profits and prevent losses from expanding 
- Closing positions on Monday avoids risks from volatile Monday openings

## Risk Analysis

- Bitcoin prices are volatile on weekends, risk of losses
- 10x leverage amplifies losses
- Improper stop loss placement could lead to large losses
- Volatile Monday openings may prevent full profit taking

Potential improvements to mitigate risks:

1. Set stop loss to control loss per trade.  
2. Adjust leverage to reduce risk.
3. Optimize take profit points, take profits in batches after reaching certain profit levels.  
4. Set volume or time take profits before Monday opening to avoid volatility.

## Optimization Directions

The strategy can be improved in the following aspects:

1. Add other indicators for better entry timing. Incorporate moving averages, RSI etc to filter entries and improve accuracy.

2. Optimize stop loss and take profit strategies. Use trailing stops, staged profit taking etc to lock in profits and control risk.

3. Adjust leverage size to reduce risk. Implement dynamic leverage adjustment, lowering leverage during drawdowns. 

4. Add other cryptocurrencies. Trade additional cryptos with weekend patterns for multi-asset arbitrage.

5. Use machine learning to optimize parameters. Collect large historical datasets and use ML to automatically optimize dynamic parameter adjustment.

## Summary 

This is a typical short-term trading strategy utilizing Bitcoin's increased weekend volume. It capitalizes on weekend volume by judging trends on Saturday and Sunday, going long or short. The strategy has advantages like profit amplification and risk control, but also has some risks. Next steps are to optimize areas like entry, stop loss, leverage management, asset expansion etc to make the strategy more robust and intelligent.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Leverage|
|v_input_2|0.1|Profit Taking Percent Threshold|
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
start: 2023-10-14 00:00:00
end: 2023-11-13 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Copyright Boris Kozak 
strategy("XBT Weekend Trade Strategy", overlay=false)
leverage = input(10,"Leverage")
profitTakingPercentThreshold = input(0.10,"Profit Taking Percent Threshold")

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

https://www.fmz.com/strategy/432078

> Last Modified

2023-11-14 11:29:12
