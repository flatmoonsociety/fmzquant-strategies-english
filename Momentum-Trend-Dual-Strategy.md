
> Name

Momentum-Trend-Dual-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/874d90cb2e7e47c812.png)
 [trans]
## Overview
This strategy combines two indicators, the Relative Strength Index (RSI) and Bollinger Bands, to implement a double-confirmed opening and closing logic. This strategy will only issue a trading signal when the RSI and Bollinger Bands both display overbought or oversold signals. This can effectively reduce false signals and improve strategy stability.
## Strategy Principle
1. RSI indicator judgment logic
   - When RSI crosses 45, it is considered an oversold signal
   - When RSI falls below 55, it is considered an overbought signal
2. Bollinger Bands judgment logic
   - When the price crosses the upper and lower Bollinger Bands, it is considered oversold.
   - When the price crosses the upper limit of Bollinger Bands, it is considered overbought.
3. Double confirmation logic
   - Long positions will only be opened when RSI and Bollinger Bands simultaneously show oversold signals
   - Short positions will only be opened when RSI and Bollinger Bands simultaneously show overbought signals
The above logic implements a stable double confirmation strategy for opening and closing positions.
## Advantage Analysis
1. The double confirmation mechanism can filter out a large number of noise transactions and avoid unnecessary transactions, thereby reducing transaction costs and increasing profitability.
2. The RSI indicator can effectively identify trends and reversals, and the Bollinger Bands indicator can effectively determine support and resistance. The two combine to form a perfect fit.
3. The parameter settings are flexible and can be adjusted according to different varieties and trading preferences, with strong adaptability.
## Risk Analysis
1. In a volatile market, RSI and Bollinger Band indicators may send wrong signals at the same time, leading to unnecessary losses. The probability of misjudgment can be reduced by optimizing parameters.
2. The double confirmation mechanism will slightly increase the entry delay and may miss very short-term trading opportunities. Not suitable for strategies that are very sensitive to latency.
3. This strategy is very sensitive to parameters, and inappropriate parameter settings may significantly reduce the rate of return. Full backtesting and review are needed to find the best parameter combination.
## Optimization direction
1. You can test RSI indicators of different periods, find the most matching period parameters, and improve the indicator effect.
2. You can add stop loss logic, set reasonable moving stop loss or fixed stop loss, and control the risk of single loss.
3. You can test the Bollinger Bands channel width parameters, optimize the channel range, and improve the identification effect of Bollinger Bands.
4. You can test different price inputs, such as closing price, highest price, lowest price, etc., to find the best price input to improve the stability of the strategy.
## Summarize
This strategy successfully combines the RSI indicator and the Bollinger Bands indicator to implement double confirmation logic, which not only ensures sufficient trading opportunities, but also effectively reduces noise trading. Through reasonable parameter optimization and risk control, this strategy can become a very stable and reliable trend tracking and trading strategy.
||

## Overview

This strategy combines the Relative Strength Index (RSI) and Bollinger Bands indicators to implement a dual confirmation logic for entries and exits. It generates trading signals only when both RSI and Bollinger Bands show overbought or oversold signals at the same time. This can effectively reduce false signals and improve the stability of the strategy.

## Strategy Logic

1. RSI Judgment Logic
    - RSI crossing above 45 is considered oversold signal  
    - RSI crossing below 55 is considered overbought signal
2. Bollinger Bands Judgment Logic
    - Price crossing above Bollinger Lower Band is considered oversold
    - Price crossing below Bollinger Upper Band is considered overbought
3. Dual Confirmation Logic
    - Long position is opened only when both RSI and Bollinger Bands show oversold signal  
    - Short position is opened only when both RSI and Bollinger Bands show overbought signal  

The above logic implements a stable dual confirmation strategy for entries and exits.

## Advantage Analysis  

1. The dual confirmation mechanism filters out a lot of noise trades, avoids unnecessary trades, reduces trading costs, and improves profitability.

2. RSI is effective in identifying trends and reversals. Bollinger Bands is effective in judging supports and resistances. The two complement each other perfectly.  

3. Flexible parameter settings, can be adjusted based on different products and trading preferences, highly adaptable.

## Risk Analysis

1. In ranging markets, RSI and Bollinger Bands may give out wrong signals at the same time, causing unnecessary losses. The misjudgment probability can be reduced by optimizing parameters.

2. The dual confirmation mechanism slightly increases entry delay, possibly missing very short-term trading opportunities. Not suitable for strategies that are very sensitive to delay.

3. The strategy is very sensitive to parameters. Inappropriate parameter settings may greatly reduce profitability. Sufficient backtesting and review are needed to find the optimal parameter combination.  

## Optimization Directions  

1. Test RSI indicators with different periods to find the best matching period parameter to improve efficiency.

2. Add stop loss logic, set reasonable moving stop loss or fixed stop loss to control single trade loss risk.   

3. Test Bollinger bandwidth parameter to optimize the channel range and improve efficiency. 

4. Test different price inputs like close, high, low etc to find the best price input to enhance stability.

## Summary

The strategy successfully combines the RSI and Bollinger Bands indicators to implement a dual confirmation logic, ensuring sufficient trading opportunities while effectively reducing noise trades. With proper parameter optimization and risk control, it can become a very stable and reliable trend tracking and trading strategy.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|16|RSI Period Length|
|v_input_2|45|RSI Value Range|
|v_input_3|20|Bollinger Bands SMA Period Length|
|v_input_4|2|Bollinger Bands Standard Deviation|
|v_input_5|true|Enable Bar Color?|
|v_input_6|true|Enable Background Color?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-22 00:00:00
end: 2024-01-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Bollinger + RSI, Double Strategy (by ChartArt)", shorttitle="CA_-_RSI_Bol_Strat", overlay=true)

// ChartArt's RSI + Bollinger Bands, Double Strategy
//
// Version 1.0
// Idea by ChartArt on January 14, 2015.
//
// This strategy uses a modfied RSI to sell
// when the RSI increases over the value of 55
// (or to buy when the value falls below 45),
// with the classic Bollinger Bands strategy
// to sell when the price is above the
// upper Bollinger Band (and to buy when
// this value is below the lower band).
//
// This simple strategy only triggers when
// both the RSI and the Bollinger Bands
// indicators are at the same time in
// a overbought or oversold condition.
//
// List of my work: 
// https://www.tradingview.com/u/ChartArt/
// 
//  __             __  ___       __  ___ 
// /  ` |__|  /\  |__)  |   /\  |__)  |  
// \__, |  | /~~\ |  \  |  /~~\ |  \  |  
// 
// 


///////////// RSI
RSIlength = input( 16 ,title="RSI Period Length") 
RSIvalue = input( 45 ,title="RSI Value Range") 
RSIoverSold = 0 + RSIvalue
RSIoverBought = 100 - RSIvalue
price = close
vrsi = rsi(price, RSIlength)


///////////// Bollinger Bands
BBlength = input(20, minval=1,title="Bollinger Bands SMA Period Length")
BBmult = input(2.0, minval=0.001, maxval=50,title="Bollinger Bands Standard Deviation")
BBbasis = sma(price, BBlength)
BBdev = BBmult * stdev(price, BBlength)
BBupper = BBbasis + BBdev
BBlower = BBbasis - BBdev
source = close
buyEntry = crossover(source, BBlower)
sellEntry = crossunder(source, BBupper)
plot(BBbasis, color=aqua,title="Bollinger Bands SMA Basis Line")
p1 = plot(BBupper, color=silver,title="Bollinger Bands Upper Line")
p2 = plot(BBlower, color=silver,title="Bollinger Bands Lower Line")
fill(p1, p2)


///////////// Colors
switch1=input(true, title="Enable Bar Color?")
switch2=input(true, title="Enable Background Color?")
TrendColor = RSIoverBought and (price[1] > BBupper and price < BBupper) ? red : RSIoverSold and (price[1] < BBlower and price > BBlower)  ? green : na
barcolor(switch1?TrendColor:na)
bgcolor(switch2?TrendColor:na,transp=50)


///////////// RSI + Bollinger Bands Strategy
if (not na(vrsi))

    if (crossover(vrsi, RSIoverSold) and crossover(source, BBlower))
        strategy.entry("RSI_BB_L", strategy.long, stop=BBlower,  comment="RSI_BB_L")
    else
        strategy.cancel(id="RSI_BB_L")
        
    if (crossunder(vrsi, RSIoverBought) and crossunder(source, BBupper))
        strategy.entry("RSI_BB_S", strategy.short, stop=BBupper, comment="RSI_BB_S")
    else
        strategy.cancel(id="RSI_BB_S")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/439640

> Last Modified

2024-01-22 17:04:36
