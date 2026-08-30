
> Name

Triangle-Breakout-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a trend following strategy. Go long when price breaks out of the upward triangle pattern and close when the fast EMA crosses below the mid-term EMA. Set stop loss and take profit points at the same time to control risk.
## Strategy Principle
1. Use fast EMA and medium-term EMA to determine the trend direction. A fast EMA crossing above the mid-term EMA is a bullish sign.
2. Use the highest and lowest prices of the most recent N K lines to determine whether an upward triangle is formed. A triangle is formed to make a long signal.
3. After entering the market, when the fast EMA crosses the mid-term EMA, it is considered that the trend is reversed and a closing signal is issued.
4. Set the stop loss point to a certain percentage below the entry price and exit with stop loss.
5. Set the take-profit point to a certain percentage above the entry price, and exit with partial take-profit.
6. Use the 200-day EMA to determine the overall trend direction and only operate when the trend is upward.
## Advantage Analysis
1. Use triangle patterns to filter out false breakthroughs and improve entry accuracy.
2. Use fast EMA and mid-term EMA to reasonably divide trends and shocks to avoid being trapped.
3. The stop loss and take profit settings are reasonable and single losses can be controlled.
4. Only operate when the trend is upward to avoid the consolidation phase.
## Risk Analysis
1. If the triangle range is too small, the trend may be missed, and if it is too large, it may increase unnecessary transactions. Parameter N needs to be optimized.
2. If the stop loss point is too close, it is easy to be hit, but if it is too far, it is difficult to control the loss. Parameter effects need to be evaluated and optimized.
3. Improper setting of some take-profits may cause profits to overflow. A reasonable proportion needs to be assessed.
4. Improper parameters of trend judgment indicators may lead to wrong position direction. Multiple varieties of backtest optimization are required.
## Optimization direction
1. Optimize the parameter N of triangle determination and find the best value.
2. Test different EMA cycle combinations to improve the accuracy of trend judgment.
3. Optimize stop-loss and take-profit parameters according to the characteristics of different varieties.
4. Add other indicator judgments, such as MACD patterns, Bollinger Band breakthroughs, etc., to improve signal quality.
5. Add a reopen mechanism to extend the profit time when the trend continues.
## Summarize
This strategy is relatively stable overall, and can effectively filter out false breakthroughs through triangle judgment. The parameter optimization space is larger and better results are expected. In addition, you can try to add more auxiliary judgment indicators, or improve the stop loss and take profit strategy to further improve the strategy effect. Overall, this strategy has the potential to be a quality trend following strategy.
|| 

## Overview 

This is a trend following strategy. It goes long when price breaks out of an ascending triangle formation, and closes position when fast EMA crosses below medium EMA. Stop loss and take profit are also set to control risks.

## Strategy Logic

1. Use fast EMA and medium EMA to determine trend direction. Fast EMA crossing above medium EMA is long signal.

2. Use highest and lowest prices of last N bars to determine if an ascending triangle is formed. Triangle formation gives long signal.

3. After entry, when fast EMA crosses below medium EMA, it indicates trend reversal and gives exit signal.

4. Set stop loss at certain percentage below entry price for stop loss exit. 

5. Set take profit target at certain percentage above entry price for partial profit taking.

6. Use 200-day EMA to determine overall trend direction, only trade when trend is up.

## Advantage Analysis

1. Triangle formation filters false breakout and improves entry accuracy.

2. Fast EMA vs medium EMA reasonably divides trend and consolidation to avoid whipsaws.

3. Reasonable stop loss and take profit settings control single trade loss.

4. Only trading in uptrend avoids choppy periods.

## Risk Analysis

1. Too narrow triangle range may miss trends, while too wide range may increase unnecessary trades. Parameter N needs to be optimized.

2. Stop loss too close tends to get stopped out prematurely, while too wide fails to control loss. Evaluate and optimize parameter. 

3. Improper partial take profit setting may lead to profit overflow. Evaluate proper ratio.

4. Wrong trend indicator parameters may lead to wrong position direction. Multi-product backtest optimization needed.

## Improvement Directions

1. Optimize parameter N for triangle determination to find optimum value.

2. Test different EMA period combinations to improve trend accuracy.

3. Optimize stop loss and take profit parameters based on product characteristics. 

4. Add other indicators like MACD pattern, Bollinger breakout etc to improve signal quality.

5. Add reopen mechanism to extend profit when trend continues.

## Summary

The strategy is overall robust with triangle formation improving signal accuracy. Large parameter optimization space exists for further enhancement. Also try adding more auxiliary indicators or improving stop loss/take profit for greater efficacy. Overall this strategy has the potential to become a quality trend following strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Number of Bars|
|v_input_2|13|fast EMA|
|v_input_3|65|slow EMA|
|v_input_4|5|Stop Loss%|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-20 00:00:00
end: 2023-09-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mohanee

//@version=4

strategy(title="TrianglePoint strategy", overlay=true,pyramiding=2, default_qty_value=3, default_qty_type=strategy.fixed,    initial_capital=10000, currency=currency.USD)
// variables  BEGIN

numPeriods=input(9,title="Number of Bars")
fastEMA = input(13, title="fast EMA", minval=1)
slowEMA = input(65, title="slow EMA", minval=1)

stopLoss = input(title="Stop Loss%", defval=5, minval=1)


HH = highest(close[1],numPeriods)
LL = lowest(close[1],numPeriods)
tringlePoint =  low > LL and high < HH

fastEMAval= ema(close, fastEMA)
slowEMAval= ema(close, slowEMA)
two100EMAval= ema(close, 200)

//plot emas
plot(fastEMAval, color = color.green, linewidth = 1, transp=0)
plot(slowEMAval, color = color.orange, linewidth = 1, transp=0)
plot(two100EMAval, color = color.purple, linewidth = 2, transp=0)

longCondition=fastEMAval>two100EMAval and tringlePoint

//plotshape(triP,style=shape.triangleup,text="Buy",color=color.green,location=location.belowbar)
//plotshape(longCondition,style=shape.triangleup,text="Buy",color=color.green,location=location.belowbar)

//Entry
strategy.entry(id="TBT LE", comment="TBT LE" , long=true,  when= longCondition and strategy.position_size<1)   

//Add
strategy.entry(id="TBT LE", comment="Add" , long=true,  when= longCondition and strategy.position_size>=1 and close<strategy.position_avg_price)   


//barcolor(strategy.position_size>=1 ? color.blue : na)

//Take profit
takeProfitVal=   strategy.position_size>=1 ?  (strategy.position_avg_price * (1+(stopLoss*0.01) )) : 0.00
//strategy.close(id="TBT LE", comment="Profit Exit",  qty=strategy.position_size/2,  when=close>=takeProfitVal and close<open and close<fastEMAval)   //crossunder(close,fastEMAval)
barcolor(strategy.position_size>=1  ? (close>takeProfitVal? color.purple : color.blue): na)

//Exit
strategy.close(id="TBT LE", comment="TBT Exit",   when=crossunder(fastEMAval,slowEMAval))


//stoploss
stopLossVal=   strategy.position_size>=1 ?  (strategy.position_avg_price * (1-(stopLoss*0.01) )) : 0.00

//stopLossVal= close> (strategy.position_avg_price * (1+(stopLoss*0.01) )) ? lowest(close,numPeriods) : (strategy.position_avg_price * (1-(stopLoss*0.01) ))


strategy.close(id="TBT LE", comment="SL Exit",   when= close < stopLossVal)
```

> Detail

https://www.fmz.com/strategy/427367

> Last Modified

2023-09-20 14:24:16
