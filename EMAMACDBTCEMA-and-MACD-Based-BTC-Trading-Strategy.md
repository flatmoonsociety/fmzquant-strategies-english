
> Name

BTC trading strategy EMA-and-MACD-Based-BTC-Trading-Strategy based on EMA moving average and MACD indicator
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b336c791d267e6313ad00c3c8db2eacdc5796274eacc892c28a6ec09273ebdf1.png)
 [trans]

## Overview
This strategy is a composite strategy based on the EMA moving average difference and the MACD indicator, which is used for short-term trading of BTC. It combines the signals of EMA and MACD to generate buy and sell signals under specific conditions.
## Strategy Principle
When the difference is negative and less than the threshold, and there is a short MACD cross, a buy signal is generated. When the difference is positive and greater than the threshold, and a bullish cross occurs on MACD, a sell signal is generated.
By combining the signals of the EMA moving average difference and the MACD indicator, some false signals can be filtered out and the reliability of the signal can be improved.
## Advantage Analysis
1. Using composite indicators, the signal is more reliable
2. Adopt short-cycle parameter settings, suitable for short-term trading
3. There are stop loss and take profit settings to control risks
## Risk Analysis
1. When the market fluctuates violently, the stop loss may be breached
2. Parameters need to be optimized to make them more suitable for different market environments
3. Need to test the effects of different currencies and different exchanges
## Optimization direction
1. Optimize the parameters of EMA and MACD to make them more consistent with the fluctuation environment of BTC
2. Increase opening positions and increase or decrease strategies to optimize capital utilization efficiency
3. Add stop loss methods, such as trailing stop loss, oscillating stop loss, etc., to reduce risks
4. Test the effects of different exchanges and currencies
## Summarize
This strategy integrates the advantages of moving average and MACD, and uses composite signals, which can effectively filter out false signals. By optimizing parameters and opening strategies, you can get stable returns. However, we also need to be alert to the risk of stop loss being breached, and further testing and improvement are needed.
||

## Overview

This strategy is a composite strategy based on EMA difference and MACD indicator for short-term BTC trading. It combines the signals from EMA and MACD to generate buy and sell signals under certain conditions.

## Strategy Logic

It generates buy signals when the difference is negative and below a threshold and MACD has a bearish crossover. It generates sell signals when the difference is positive and above a threshold and MACD has a bullish crossover.  

By combining the signals from both EMA difference and MACD, some fake signals can be filtered out and the reliability of signals is improved.

## Advantage Analysis  

1. Uses composite indicators, more reliable signals
2. Adopts short-term parameters, suitable for short-term trading  
3. Has stop loss and take profit settings to control risks

## Risk Analysis

1. Stop loss may be broken during huge market swings
2. Parameters need to be optimized for different market environments  
3. Effects need to be tested on different coins and exchanges

## Optimization Directions  

1. Optimize EMA and MACD parameters to fit BTC volatility
2. Add position sizing and pyramiding strategies to improve capital efficiency
3. Add stop loss methods like trailing stop loss to reduce risks
4. Test effects on different exchanges and coins  

## Conclusion

This strategy integrates the strengths of both EMA and MACD indicators and uses composite signals to effectively filter out false signals. With optimized parameters and position strategies, stable returns can be achieved. But risks like stop loss being hit need attention and further testing and improvement is required.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|18|EMA|
|v_input_2|12|MACDfast|
|v_input_3|26|MACDslow|
|v_input_4|8|EMADiffThreshold|
|v_input_5|80|MACDThreshold|
|v_input_6|65|TargetValidityThreshold|
|v_input_7|120|Target|
|v_input_8|650|StopLoss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-24 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("EMA50Diff & MACD Strategy", overlay=false)
EMA = input(18, step=1)
MACDfast = input(12)
MACDslow = input(26)
EMADiffThreshold = input(8)
MACDThreshold = input(80)
TargetValidityThreshold = input(65, step=5)
Target = input(120, step=5)
StopLoss = input(650, step=5) 
ema = ema(close, EMA)
hl = plot(0, color=white, linewidth=1)
diff = close - ema
clr = color(blue, transp=100)
if diff>0
    clr := lime
else 
    if diff<0
        clr := red

fastMA = ema(close, MACDfast)
slowMA = ema(close, MACDslow)
macd = (fastMA - slowMA)*3
signal = sma(macd, 9)
plot(macd, color=aqua, linewidth=2)
plot(signal, color=purple, linewidth=2)

macdlong = macd<-MACDThreshold and signal<-MACDThreshold and crossover(macd, signal)
macdshort = macd>MACDThreshold and signal>MACDThreshold and crossunder(macd, signal)
position = 0.0
position := nz(strategy.position_size, 0.0)
long = (position < 0 and close < strategy.position_avg_price - TargetValidityThreshold and macdlong) or 
     (position == 0.0 and diff < -EMADiffThreshold and diff > diff[1] and diff[1] < diff[2] and macdlong)

short = (position > 0 and close > strategy.position_avg_price + TargetValidityThreshold and macdshort) or 
      (position == 0.0 and diff > EMADiffThreshold and diff < diff[1] and diff[1] > diff[2] and macdshort)
amount = (strategy.equity / close) //- ((strategy.equity / close / 10)%10)
bgclr = color(blue, transp=100) //#0c0c0c
if long
    strategy.entry("long", strategy.long, amount)
    bgclr := green
if short
    strategy.entry("short", strategy.short, amount)
    bgclr := maroon
bgcolor(bgclr, transp=20)
strategy.close("long", when=close>strategy.position_avg_price + Target)
strategy.close("short", when=close<strategy.position_avg_price - Target)
strategy.exit("STOPLOSS", "long", stop=strategy.position_avg_price - StopLoss)
strategy.exit("STOPLOSS", "short", stop=strategy.position_avg_price + StopLoss)
//plotshape(long, style=shape.labelup, location=location.bottom, color=green)
//plotshape(short, style=shape.labeldown, location=location.top, color=red)
pl = plot(diff, style=histogram, color=clr)
fill(hl, pl, color=clr)

```

> Detail

https://www.fmz.com/strategy/439963

> Last Modified

2024-01-25 12:54:16
