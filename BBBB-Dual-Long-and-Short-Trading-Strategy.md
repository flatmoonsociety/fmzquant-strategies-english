
> Name

BB-Dual-Long-and-Short-Trading-Strategy BB-Dual-Long-and-Short-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/196bee854f7add8d8b0.png)
[trans]


## Overview
The BB double long and short trading strategy is a two-way trading strategy that uses Bollinger Bands. It combines the Bollinger middle track, upper track and lower track to realize the two-way opening and closing of long and short positions. Open a short position when the price touches the upper track, open a long position when it touches the lower track, and set stop loss and take profit prices. The strategy is simple and easy to operate and can capture the main trends of the market.
## Principle analysis
This strategy is mainly based on the principle of Bollinger Bands. Bollinger Bands are composed of the middle track, upper track and lower track, which represent the moving trend of prices. The middle track is the n-day moving average, the upper track is the middle track + k times the standard deviation, and the lower track is the middle track - k times the standard deviation. When the price breaks through the upper band, it means that the market is overbought, and you should consider opening a short position; when the price falls below the lower band, it means that the market is oversold, and you should consider opening a long position.
Specifically, this strategy first calculates the Bollinger middle track, upper track, and lower track. Then judge whether the price touches the upper rail, and if so, open a short position; judge whether the price touches the lower rail, and if so, open a long position. Stop loss and take profit prices are also set after opening a position. For example, after opening a long position, the stop-loss price is the opening price minus a certain percentage, and the take-profit price is the opening price plus a certain percentage. Finally, the strategy also defines the conditions for closing positions, including conditions such as stop loss, take profit, and Bollinger Bands re-entering the range.
The entire strategy makes full use of Bollinger Bands to reflect the overbought and oversold characteristics of the market and achieves more accurate long and short transactions. When the market is at different stages, the Bollinger Bands indicator can also be used to judge the current market trend and adopt corresponding trading strategies.
## Advantage Analysis
This strategy has the following advantages:
1. Capture the trend. Bollinger Bands can identify the main trend direction and open positions in time to capture the trend.
2. Two-way trading, long and short transactions can be carried out at the same time, not limited to unilateral direction.
3. Risk control, set stop loss and stop profit to ensure that each transaction has loss blocking measures.
4. Simple and clear, based on the Bollinger Bands indicator, the strategy rules are straightforward and easy to understand.
5. Easy to optimize, the strategy can be optimized by adjusting parameters such as period length, standard deviation multiple, etc.
6. Applicable to different markets, including stocks, foreign exchange, cryptocurrency and other markets.
## Risk Analysis
There are also some risks with this strategy:
1. Risk of Bollinger Bands failure. Bollinger Bands may fail when the market fluctuates violently.
2. Risk of stop loss being breached. Stop loss may be breached when the market trend changes drastically.
3. Risk of over-optimizing the strategy. Over-optimizing the strategy may lead to over-fitting.
4. Risk of too high trading frequency. When Bollinger Bands fluctuate frequently, trading will be too frequent.
5. The risk of leaving the market at points. Relying solely on Bollinger Bands for points may lead to premature departure.
Corresponding solutions:
1. Combined with trend indicators, determine the strategy of closing the Bollinger Bands promptly after failure.
2. Use trailing stop loss and let the stop loss track the price.
3. Multi-market and multi-time frame backtesting to prevent over-optimization.
4. Appropriately relax the Bollinger Bands fluctuation range and reduce the frequency of transactions.
5. Added exit indicators such as MACD to confirm Bollinger Band signals.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Adjust Bollinger Band parameters, such as adjusting cycle parameters to match different cycle trends, and adjusting standard deviation multiples to adapt to market volatility.
2. Add trend filtering and use indicators such as moving averages to determine trends to avoid false signals from Bollinger Bands when there is no clear trend.
3. Optimize the stop loss strategy, such as moving the stop loss to make the stop loss follow the price more closely, or setting the stop loss range based on ATR.
4. Add entry filtering, such as the closing price breaking through the Bollinger Band, etc., to avoid false breakthroughs in the middle of the Bollinger Band indicator.
5. Use machine learning technology to automatically optimize parameters and achieve intelligent parameter adjustment.
6. Add exit indicators, such as the divergence of MACD and other indicators, as exit indicators to assist Bollinger Band signals.
## Summarize
Overall, the BB double long and short trading strategy is a very typical and practical Bollinger Bands strategy. It uses the Bollinger Bands indicator to determine overbought and oversold to capture market trends, conduct two-way trading, and set take-profit and stop-loss to control risks. This strategy has the advantages of catching trends, two-way trading, and risk control, but it also has problems such as Bollinger Band failure. We can improve the effectiveness of the strategy by adjusting Bollinger Band parameters, adding trend filtering, and optimizing stop-loss strategies. This strategy has strong practicality and development potential, and is a simple and practical trading strategy worth recommending.
||

## Overview

The BB dual long and short trading strategy is a strategy that utilizes Bollinger Bands for two-way trading. It combines the middle band, upper band and lower band of the Bollinger Bands to implement opening and closing long and short positions. It opens short positions when the price touches the upper band, and opens long positions when it touches the lower band, with stop loss and take profit prices set. The strategy is simple to operate and captures the main trends of the market.

## Principle Analysis 

This strategy is mainly based on the principle of Bollinger Bands. Bollinger Bands consist of a middle band, an upper band and a lower band, representing the moving trend of prices. The middle band is the n-day moving average, the upper band is the middle band + k standard deviations, and the lower band is the middle band - k standard deviations. When the price breaks through the upper band, it indicates the market is in an overbought state, and opening short positions should be considered; when the price breaks through the lower band, it indicates the market is in an oversold state, and opening long positions should be considered.

Specifically, the strategy first calculates the Bollinger middle, upper and lower bands. It then judges if the price touches the upper band. If yes, it opens short positions. It also judges if the price touches the lower band. If yes, it opens long positions. After opening positions, it also sets stop loss and take profit prices. For example, after opening long positions, the stop loss price would be the opening price minus a certain percentage, and the take profit price would be the opening price plus a certain percentage. Finally, the strategy also defines the closing conditions, including stop loss, take profit being hit, and the price re-entering the Bollinger Bands.

The strategy fully utilizes the ability of Bollinger Bands to reflect overbought and oversold market conditions, and implements relatively accurate long and short trading. When the market is in different stages, the trend of current market conditions can also be judged through Bollinger Bands indicators, and corresponding trading strategies can be adopted.

## Advantage Analysis

The strategy has the following advantages:

1. Catching trends. Bollinger Bands can identify the main trend direction and open positions in time to capture trends.

2. Two-way trading. It allows simultaneous long and short trading, without being limited to one direction.

3. Risk control. Stop loss and take profit setup ensures each trade has loss mitigation measures.

4. Simple and clear. Based on the Bollinger Bands indicator, the strategy rules are direct and easy to understand.

5. Easy to optimize. Parameters like cycle length and standard deviation multiplier can be adjusted to optimize the strategy.

6. Applicable to different markets. Can be applied to stocks, forex, cryptocurrencies etc.

## Risk Analysis

The strategy also has some risks:

1. Bollinger Bands failure risk. Bollinger Bands may fail during violent market fluctuations.

2. Stop loss being hit risk. Stop loss may be hit during drastic trend changes. 

3. Over-optimization risk. Excessive optimization may lead to overfitting.

4. High trading frequency risk. Frequent Bollinger Bands fluctuations may lead to over-trading.

5. Band touch exit risk. Exiting solely based on band touch may be premature.

The solutions are:

1. Combine with trend indicators, close strategy in time when bands fail.

2. Adopt trailing stop loss. 

3. Backtest across markets and timeframes to prevent overfitting.

4. Relax the fluctuation range to reduce trade frequency.

5. Add exit indicators like MACD divergence to confirm bands signal.

## Optimization Directions 

The strategy can be optimized in the following aspects:

1. Adjust Bollinger parameters like cycle length to match different cycle trends, and standard deviation multiplier to suit market volatility.

2. Add trend filter, combine indicators like moving average to determine trend, avoid false signals when no clear trend.

3. Optimize stop loss strategy, like trailing stop loss to track price closer, or set stop loss based on ATR.

4. Add entry filters like closing price breaking bands to avoid mid-band false breakouts.

5. Use machine learning to auto optimize parameters.

6. Add exit indicators like MACD divergence to supplement band signals.

## Summary

Overall, the BB dual long and short trading strategy is a very typical and practical Bollinger Bands strategy. It uses the Bollinger Bands to judge overbought and oversold conditions to capture trends, implements two-way trading, and sets stop loss and take profit for risk control. The strategy has the advantages of catching trends, two-way trading, and risk control, and also has problems like Bollinger Bands failure. We can improve the strategy by adjusting Bollinger parameters, adding trend filters, optimizing stop loss etc. The strategy has great practicality and potential, and is a simple useful trading strategy worth recommending.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Longitud|
|v_input_float_1|2|Desvio estandar|
|v_input_2_close|0|Fuente: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_2|5|Take Profit|
|v_input_float_3|true|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-25 00:00:00
end: 2023-11-01 00:00:00
period: 2m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © samuelkanneman

//@version=5
strategy('MI_BB ', overlay=true)
// i_startTime = input.time(title='Start Date Filter', defval=timestamp('01 Nov 2020 13:30 +0000'), tooltip='Date & time to begin trading from')
// i_endTime = input.time(title='End Date Filter', defval=timestamp('1 Nov 2022 19:30 +0000'), tooltip='Date & time to stop trading')

dateFilter = true

longitud = input(20, title='Longitud')
Desv = input.float(2.0, title='Desvio estandar', step=0.1)
fuente = input(close, title='Fuente')

TakeP = input.float(5.0, title='Take Profit', step=0.1)
StopL = input.float(1.0, title='Stop Loss', step=0.1)
var SL = 0.0
var TP = 0.0

[banda_central, banda_sup, banda_inf] = ta.bb(fuente, longitud, Desv)

comprado = strategy.position_size > 0
vendido = strategy.position_size < 0



if not vendido and not comprado and dateFilter
// Short
    if close >= banda_sup
    //cantidad= (strategy.equity/close)
        strategy.entry('venta', strategy.short)
        SL := close * (1 + StopL / 100)
        TP := close*(1-TakeP/100)
        
//Long
    else if close <= banda_inf
    //cantidad= (strategy.equity/close)
        strategy.entry('compra', strategy.long)
        SL := close * (1 - StopL / 100)
        TP := close*(1+TakeP/100)
    
//cierrres short
if close <= TP and vendido
    strategy.close ("venta" , comment="Salto TP")
if close <= banda_inf and vendido
    strategy.close ("venta" , comment="Banda Inferior")
if close >= SL and vendido
    strategy.close ("venta" , comment="Salto SL")
    
   
//cierre long
if close >= TP and comprado
    strategy.close ("compra" , comment="Salto TP")  
if close >= banda_sup and comprado
    strategy.close ("compra" , comment="Banda Superior")
    
if close <= SL and comprado
    strategy.close ("compra" , comment="Salto SL")
    


p1 = plot(banda_central)
p2 = plot(banda_sup)
p3 = plot(banda_inf)
fill(p2, p3, transp=90)



```

> Detail

https://www.fmz.com/strategy/430868

> Last Modified

2023-11-02 15:40:00
