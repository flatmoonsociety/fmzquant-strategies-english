
> Name

Trendless-MACD-Strategy Trendless-MACD-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17bc569daa955e78c8e.png)

[trans]


### Overview
This strategy uses detrending in stock prices to more clearly observe the pattern of the MACD indicator. By calculating the DEMA fast line and the DEMA slow line, the MACD straight line and signal line are obtained, and their intersection is judged to generate trading signals. This strategy also combines conditional filtering of months and dates, as well as stop-loss closing logic, to form a relatively complete strategy system.
### Strategy Principles
First, calculate the price EMA to eliminate the price trend and obtain the price EMA after the trend is eliminated. Then calculate the fast line DEMA, slow line DEMA and MACD straight line respectively based on EMA. Among them, the calculation method of fast line DEMA is: first calculate the EMA1 of the fast line, then calculate the EMA2 of EMA1, and then calculate DEMA=(2*EMA1-EMA2). The calculation of slow line DEMA and signal line is the same. After obtaining the MACD straight line (fast line DEMA - slow line DEMA) and the signal line, if the MACD straight line crosses the signal line, a buy signal is generated; if the MACD straight line crosses the signal line, a sell signal is generated. Finally, filter signals based on month and date conditions, and set stop loss logic.
The core logic of this strategy is:
1. Eliminate the price trend and see the MACD indicator pattern more clearly
2. Calculate the DEMA fast line and slow line, and obtain the MACD straight line and signal line
3. The intersection of the MACD straight line and the signal line generates a trading signal
4. Add date and month conditions to filter
5. Set stop loss logic
### Advantage Analysis
The main advantages of this strategy are:
1. Eliminate the price trend, and you can see the intersection of the MACD indicator more clearly, and avoid being misled by the trend.
2. Using the DEMA algorithm to calculate the MACD indicator can filter out some noise and make the signal clearer.
3. Filtering by combining date and month can reduce some unnecessary transactions.
4. Set stop loss logic to stop losses in time and control risks.
5. Using crossovers to generate signals can reduce erroneous transactions.
6. Overall, this strategy combines trend elimination, DEMA calculation and conditional filtering to produce clearer and more reliable trading signals.
### Risk Analysis
There are also some risks to be aware of with this strategy:
1. After the trend is eliminated, MACD cross signals may increase, and it needs to be verified by real trading to see if it is feasible.
2. Although the DEMA algorithm filters out some noise, there may still be many false signals in the indicator calculation.
3. The day and month filter conditions may be too rigid, missing some trading opportunities.
4. The stop loss position setting needs to be considered whether it is reasonable. If it is too loose, it will increase the risk, and if it is too strict, it will cause frequent stop losses.
5. This strategy mainly relies on the MACD indicator. If the market is not suitable for using this indicator, the effect may be affected.
6. There is still a lot of room for optimization of strategy parameters, which needs to be further tested through backtesting and real trading.
Countermeasures:
1. Add other indicator confirmations to avoid false signals.
2. Optimize the date filtering conditions and relax them appropriately.
3. Carefully test and optimize stop loss points.
4. Add a trend judgment mechanism to avoid trading against the trend.
5. Comprehensive backtesting and optimization of parameters to improve stability.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Test different price average lines and find a more suitable line type that replaces EMA.
2. Try different parameter combinations to optimize the fast line length, slow line length and signal line length of MACD.
3. Add auxiliary judgment indicators such as volume and energy indicators to avoid false signals.
4. Optimize the stop loss strategy and set a reasonable trailing stop loss or pending order stop loss.
5. Optimize date and month filter conditions to make them more flexible.
6. Add trend judgment to avoid counter-trend operations.
7. Carry out comprehensive parameter optimization to improve strategy stability.
8. Conduct backtesting over a longer time period to check the long-term effects of the strategy.
9. Conduct real offer verification and further modify the strategy parameters based on the actual offer situation.
### Summarize
Generally speaking, this strategy uses the idea of ​​​​eliminating the trend, calculates the MACD indicator in the form of DEMA, and combines date filtering to generate trading signals. It is a simple but feasible strategy idea. Its biggest advantage is that it can clearly see the MACD pattern and avoid being affected by price trends. However, this strategy also has certain risks, and parameter optimization and risk control measures need to be added before it can be actually applied. This strategy still has a lot of room for optimization. If it is fully verified and optimized, it can become a stable and reliable short-term strategy.
||


### Overview

This strategy uses the method of eliminating the trend of stock prices to observe the MACD indicator more clearly. By calculating the DEMA fast line and DEMA slow line, the MACD line and signal line are derived. Trading signals are generated by crossing between the MACD line and signal line. The strategy also incorporates date and month condition filters and stop loss logic to form a more complete system.

### Strategy Logic

Firstly, the EMA of price is calculated to eliminate the price trend and obtain the detrended EMA. Then the fast line DEMA, slow line DEMA and MACD line are calculated based on EMA. The fast line DEMA is calculated by: first calculating EMA1 of the fast line, then calculating EMA2 of EMA1, and finally calculating DEMA=(2*EMA1-EMA2). The slow line DEMA and signal line are calculated similarly. After obtaining the MACD line (fast line DEMA - slow line DEMA) and the signal line, a buy signal is generated when the MACD line crosses above the signal line, and a sell signal is generated when the MACD line crosses below the signal line. Finally, combine the date and month filters, and set stop loss logic.  

The core logic of this strategy is:

1. Eliminate the price trend to see the MACD indicator more clearly.

2. Calculate DEMA fast line, DEMA slow line to derive MACD line and signal line.

3. MACD line and signal line crossover generate trading signals. 

4. Add date and month filters.

5. Set stop loss logic.

### Advantage Analysis

The main advantages of this strategy are:

1. Eliminating the price trend can reveal the crossover situation of MACD more clearly without being misled by the trend.

2. Using DEMA algorithm to calculate MACD filters out some noise and makes the signal clearer.

3. Combining date and month filters can reduce unnecessary trades.

4. The stop loss logic can cut losses in time and control risks.

5. Using crossover to generate signals reduces incorrect trades.

6. Overall, combining trend elimination, DEMA calculation and condition filters, this strategy can generate relatively clear and reliable trading signals.

### Risk Analysis 

Some risks of this strategy need attention:

1. After eliminating the trend, MACD crossover signals may increase, which needs live testing to verify feasibility.

2. Although DEMA algorithm filters some noise, there can still be many false signals in the indicator calculation.

3. The date and month filter conditions may be too rigid, missing some trading opportunities. 

4. The stop loss position needs to be reasonably set, too loose will increase risk, too tight will stop loss frequently.

5. The strategy relies mainly on MACD, if the market is not suitable for this indicator, the performance may be affected.

6. There is still large room for parameter optimization, which needs further testing through backtest and live trading.

Solutions:

1. Add other indicator confirmation to avoid false signals.

2. Optimize date filter conditions appropriately. 

3. Test and optimize stop loss points carefully.

4. Add trend judgment mechanism to avoid trading against the trend.

5. Comprehensive backtest and parameter optimization to improve stability.

### Optimization Directions

The strategy can be optimized in the following aspects:

1. Test different price moving averages to find a better alternative to EMA.

2. Try different parameter combinations to optimize the MACD fast line, slow line and signal line lengths.

3. Add auxiliary indicators like volume to avoid false signals. 

4. Optimize stop loss strategies, set reasonable moving or order stop loss.

5. Optimize the date and month filter conditions to make them more flexible.

6. Add trend judgment to avoid trading against the trend.

7. Comprehensive parameter optimization to improve stability. 

8. Backtest on longer time period to check long term performance.

9. Live trading to verify and further modify the parameters based on real trading.

### Summary

In summary, this strategy uses the idea of eliminating the trend and calculating DEMA MACD combined with date filters to generate trading signals, which is a simple but feasible strategy idea. Its biggest advantage is revealing the MACD pattern clearly without being affected by the price trend. However, there are still some risks of this strategy that need parameter optimization and risk control measures to be implemented for practical application. There is also large room for optimization, and with sufficient verification and optimization, this strategy can become a stable and reliable short-term trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|maperiod|
|v_input_2|12|MACD Fast  Line Length|
|v_input_3|26|MACD Slow Line Length|
|v_input_4|9|Signal Line Length|
|v_input_5|true|monthfrom|
|v_input_6|12|monthuntil|
|v_input_7|true|dayfrom|
|v_input_8|31|dayuntil|
|v_input_9|2018|yearfrom|
|v_input_10|2021|yearuntil|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-23 00:00:00
end: 2023-10-29 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2

strategy(title = "Trendless MACD  Strategy",shorttitle="MACD-T Strategy",default_qty_type = strategy.percent_of_equity, default_qty_value = 100,commission_type=strategy.commission.percent,commission_value=0.01,initial_capital=100000)



maperiod=input(9)
ema=ema(close,maperiod)


fastmacd = input(12,title='MACD Fast  Line Length')
slowmacd = input(26,title='MACD Slow Line Length')
signalmacd = input(9,title='Signal Line Length')

macdslowline1 = ema(ema,slowmacd)
macdslowline2 = ema(macdslowline1,slowmacd)
DEMAslow = ((2 * macdslowline1) - macdslowline2 )

macdfastline1 = ema(ema,fastmacd)
macdfastline2 = ema(macdfastline1,fastmacd)
DEMAfast = ((2 * macdfastline1) - macdfastline2)

MACDLine = (DEMAfast - DEMAslow)

SignalLine1 = ema(MACDLine, signalmacd)
SignalLine2 = ema(SignalLine1, signalmacd)
SignalLine = ((2 * SignalLine1) - SignalLine2 )


MACDSignal = MACDLine-SignalLine


colorbar= MACDSignal>0?green:red

plot(MACDSignal,color=colorbar,style=columns,title='Histogram',histbase=0)
p1 = plot(MACDLine,color=blue,title='MACDLine')
p2=plot(SignalLine,color=red,title="SignalLine")
fill(p1,p2,color=blue)


longCond =  crossover(MACDLine,SignalLine) 

shortCond =  crossunder(MACDLine,SignalLine) 




monthfrom =input(1)
monthuntil =input(12)
dayfrom=input(1)
dayuntil=input(31)

yearfrom= input(2018)
yearuntil=input(2021)

if (  longCond   ) 
    strategy.entry("LONG", strategy.long, stop=close, oca_name="TREND",  comment="LONG")
    
else
    strategy.cancel(id="LONG")
    



if ( shortCond  ) 

    strategy.entry("SHORT", strategy.short,stop=close, oca_name="TREND", comment="SHORT")
else
    strategy.cancel(id="SHORT")




```

> Detail

https://www.fmz.com/strategy/430595

> Last Modified

2023-10-30 17:08:16
