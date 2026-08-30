
> Name

Bull-Market-Buy-Dips-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/183ffaf14d365535c5c.png)
[trans]


## Overview
The bull market chasing up and killing down strategy aims to use the RSI indicator to capture retracement buying during the bull market stage, and use the double moving average to confirm the trend buying. When the price returns to the bull trend, use the moving average confirmation signal to close the position and take profits.
## Strategy Principle
This strategy first sets the start date and end date of the backtest, and then sets the RSI parameters and fast and slow moving average parameters.
The logic of strategy signal sending is:
1. When RSI is less than the set threshold (default 35), it means it is in the oversold zone and a buy signal is issued;
2. At the same time, the fast moving average is higher than the slow moving average, indicating that it is currently in a bullish trend, so avoid buying during consolidation;
3. When the price is higher than the fast moving average and the fast moving average is higher than the medium moving average, a closing signal is issued.
The above rationally applies the crossover principle of the RSI indicator and the double moving average to capture the callback buying opportunity in the bull market and take profits in a timely manner when the price returns to the trend.
## Strategic advantage analysis
- Use RSI indicator to effectively identify oversold points
- Use fast and slow moving averages to determine the general trend and avoid buying that may shock the market
- When the moving average crosses again, judge the trend and make a profit in time
The RSI indicator is great for capturing reversal points. Buying when RSI enters the oversold zone can effectively lock in the buying opportunity in the oversold zone. At the same time, combined with the moving average to judge the trend, it can filter the volatile market and avoid repeated buying during consolidation. Finally, use the moving average crossover to reconfirm the trend and take profits in time to avoid losses on the retracement.
## Strategy risk analysis
- The RSI parameters are improperly set and cannot effectively identify the oversold zone.
- Improper selection of moving average parameters, resulting in multiple false signals
- Take profit and close position too early or too late
If the RSI parameter is set too large or too small, the effect of accurately judging the oversold zone will be lost. If the moving average parameters are improperly selected, the fast line is too fast or the slow line is too slow, and the wrong trend will be judged. If you choose the wrong time to take profit and close a position, you will not be able to make full profits if you close the position too early, and you will easily lose profits if you close the position too late.
You can optimize the take-profit effect by adjusting the RSI parameters, selecting an appropriate moving average period, and testing different take-profit methods.
## Strategy optimization direction
- Test RSI parameters of different periods
- Test different moving average combinations
- Try other take-profit methods, such as trailing take-profit, breakthrough take-profit, etc.
- Optimize position management
- Consider the impact of transaction fees
The oversold zone judgment can be optimized by testing the RSI cycles of different parameters. Adjust the moving average period combination to find the best parameters for judging the trend. In addition, you can test other take-profit methods such as moving take-profit and resistance take-profit. Optimizing position management can better control risks. Finally, considering the impact of transaction fees can make the strategy closer to real trading.
## Summarize
The overall idea of ​​the bull market chasing up and killing down strategy is clear and reasonable. It comprehensively uses RSI and moving average principles to effectively grasp the buying opportunities and profit-taking opportunities in the trend market. Through parameter optimization, profit-taking method testing and position management optimization, strategy stability and real-time performance can be further enhanced. This strategy is simple and practical, suitable for capturing callback opportunities in the bull market stage, and can bring better returns to the investment portfolio.
||


## Overview

The Bull Market Buy Dips strategy aims to buy the dips in bull market by utilizing RSI indicator and confirm the trend by double moving averages. When the price gets back to the uptrend, the moving averages crossover is used as profit taking signal.

## Strategy Logic

The strategy first sets the backtesting start and end date, then configures the parameters for RSI and fast/slow moving averages. 

The strategy signal logic is:

1. When RSI drops below the threshold (default 35), it triggers buy signal as it indicates oversold area.

2. The fast MA needs to be above slow MA, which confirms the current uptrend and avoids buying in consolidation. 

3. When price goes above fast MA and fast MA is above medium MA, it triggers close signal to take profit.

The reasonable application of RSI and MA crossover principles helps catch pullback opportunities in bull market and take profits once the price resumes trend.

## Advantage Analysis 

- RSI effectively identifies oversold levels
- Fast/slow MAs determine the major trend and avoid buying in ranging market
- MA crossover again suggests the resumption of trend for timely profit taking

RSI is very suitable for catching reversal points. Buying when RSI enters oversold area allows accurately locking oversold opportunities. Using MAs to determine the trend can filter ranging market and prevent repeated buying in consolidation. Finally, the MA crossover confirms the trend again for timely taking profit and avoiding pullback loss.

## Risk Analysis

- Improper RSI parameter may fail to identify oversold area effectively
- Wrong selection of MA parameters may generate multiple false signals
- Premature or delayed profit taking

If RSI parameter is set too wide or too narrow, it may lose the accuracy in judging oversold levels. Wrongly chosen fast or slow MA periods could also lead to false trend determination. If profit taking timing is improper, too early may miss further profits while too late may sacrifice gained profits.

Parameters of RSI can be optimized, suitable MA periods can be selected, and different profit taking mechanisms can be tested to improve profit taking performance.

## Optimization Directions

- Test RSI parameters of different periods
- Try different MA combinations 
- Attempt other profit taking mechanisms like trailing stop, breakout stop etc
- Optimize position sizing  
- Consider trading cost impact

Different RSI periods can be tested to optimize oversold area judgment. Different MA period combinations can be tried to find the best parameters for trend determination. Other profit taking mechanisms like trailing stop, resistance stop can also be tested. Optimizing position sizing can better control risks. Finally, considering trading costs can make the strategy closer to live trading.

## Summary

The Bull Market Buy Dips strategy has clear and sensible logic overall, skillfully utilizes RSI and MA principles to capture buying and profit taking timing in trending market. Through parameter optimization, profit taking tests and position sizing management, the robustness and real trading performance can be further enhanced. With simple and practical idea, this strategy is suitable for catching pullbacks in bull market and can bring decent profits to the portfolio.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|10|From Day|
|v_input_3|2020|From Year|
|v_input_4|true|Thru Month|
|v_input_5|true|Thru Day|
|v_input_6|2112|Thru Year|
|v_input_7|true|Show Date Range|
|v_input_8|14|RSI period|
|v_input_9|9|MAfast|
|v_input_10|50|MAslow|
|v_input_11|200|MAslow|
|v_input_12|35|RSI Buy Signal|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-02 00:00:00
end: 2023-11-01 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(shorttitle='Buy The Dips in Bull Market',title='Buy The Dips in Bull Market (by Coinrule)', overlay=true, initial_capital = 1000, default_qty_type = strategy.percent_of_equity, default_qty_type = strategy.percent_of_equity, default_qty_value = 30, commission_type=strategy.commission.percent, commission_value=0.1)
    
//Backtest dates
fromMonth = input(defval = 1,  title = "From Month")     
fromDay   = input(defval = 10,    title = "From Day")       
fromYear  = input(defval = 2020, title = "From Year")       
thruMonth = input(defval = 1,    title = "Thru Month")     
thruDay   = input(defval = 1,    title = "Thru Day")     
thruYear  = input(defval = 2112, title = "Thru Year")       
    
showDate  = input(defval = true, title = "Show Date Range")
    
start     = timestamp(fromYear, fromMonth, fromDay, 00, 00)        // backtest start window
finish    = timestamp(thruYear, thruMonth, thruDay, 23, 59)        // backtest finish window
window()  => time >= start and time <= finish ? true : false       // create function "within window of time"
    
    
// RSI inputs and calculations
lengthRSI = input(14, title = 'RSI period', minval=1)
RSI = rsi(close, lengthRSI)

//MA inputs and calculations
inSignal=input(9, title='MAfast')
inlong1=input(50, title='MAslow')
inlong2=input(200, title='MAslow')


MAfast= sma(close, inSignal)
MAslow= sma(close, inlong1)
MAlong= sma(close, inlong2)


RSI_buy_signal= input(35, title='RSI Buy Signal')

    
//Entry
    
    
strategy.entry(id="long", long = true, when = RSI < RSI_buy_signal and MAlong < MAslow and window()) 
    
//Exit
    
    
strategy.close("long", when = close > MAfast and MAfast > MAslow and window())


plot(MAslow, color=color.orange, linewidth=1)
plot(MAfast, color=color.purple, linewidth=1)
plot(MAlong, color=color.blue, linewidth=2)


```

> Detail

https://www.fmz.com/strategy/430878

> Last Modified

2023-11-02 16:21:21
