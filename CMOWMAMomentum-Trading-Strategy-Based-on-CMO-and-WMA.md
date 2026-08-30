
> Name

Momentum-Trading-Strategy-Based-on-CMO-and-WMA
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1e3fed8ade8249390bd.png)
[trans]


## Overview
The strategy name is "Momentum Trading Strategy Based on CMO and WMA". This strategy utilizes the Chande Momentum Oscillator (CMO) and its Weighted Moving Average (WMA) to construct trading signals. The core idea is to go long when the CMO crosses above its WMA and go short when it crosses below its WMA. Also consider the option of reverse trading.
## Strategy Principle
The core metric of this strategy is CMO. CMO is closely related to other momentum indicators such as RSI, but it also has unique features. CMO directly measures price change momentum. Its calculations are based on raw, unsmoothed data, so they reflect short-term extreme price movements. The CMO value range is fixed between +100 and -100, so it is convenient to compare the absolute momentum size of different stocks.
The strategy first calculates the single-day change abs(close - close[1]) of close price as the original momentum xMom. Then calculate the Length day SMA of xMom, recorded as xSMA_mom. Then calculate the price change xMomLength for Length days, that is, close - close[Length]. The final CMO value is xMomLength divided by xSMA_mom multiplied by 100. The CMO is smoothed by WMA (parameter LengthWMA) to obtain the smoothed CMO xWMACMO. The strategy signal is: go long (short) when CMO crosses above (crosses below) its WMA.
## Strategic Advantages
The biggest advantage of this strategy is to capture the momentum characteristics of price trends. The bounded design of CMO makes it reflect momentum changes more directly. Compared with SMA, WMA can smooth out short-term noise better. Therefore, this strategy can effectively identify entry points in medium and long-term trends. In addition, compared with a single indicator, the combination of CMO and WMA can improve stability.
## Strategy Risk
The biggest risk of this strategy is the slippage cost caused by frequent trading. CMO and WMA are short-term parameters that may be too sensitive and produce multiple unnecessary reversals. This is especially serious when varieties fluctuate greatly. In addition, fixed parameters cannot adapt to changes in the market environment.
You can consider introducing adaptive parameters to optimize the parameters of CMO and WMA so that they can be dynamically adjusted; or add filtering conditions to reduce unnecessary transactions. Of course, reducing the volatility of varieties through combination is also an option.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Add adaptive CMO parameter mechanism. Find optimal parameters under different fluctuation environments;
2. Add adaptive WMA parameter mechanism. The smoothing effect varies with volatility;
3. Add filtering conditions, such as introducing Volatility Index, etc., to control unnecessary reversal;
4. Consider combining with other indictors to improve stability;
5. Optimize the stop loss mechanism. Set a dynamic stop loss line to proactively control single-round losses.
## Summarize
This strategy implements simple and effective trend following based on CMO and WMA. The advantage of the strategy is to clearly capture the price momentum characteristics. However, there is also the disadvantage of poor position holding ability after certain profits are made. Stability can be greatly improved through parameter optimization and combination. Overall, this strategy has great room for improvement and value.
||


## Overview

The strategy is named "Momentum Trading Strategy Based on CMO and WMA". It utilizes Chande Momentum Oscillator (CMO) and its Weighted Moving Average (WMA) to construct trading signals. The core idea is to go long when CMO crosses above its WMA and go short when crossing below. It also considers the option of reverse trading.

## Strategy Logic

The core indicator of this strategy is CMO. CMO is closely related to other momentum indicators like RSI, but also has its uniqueness. CMO directly measures price change momentum. Its calculation is based on raw unsmoothed data, so it reflects extreme short-term price changes. The CMO value ranges from +100 to -100, which makes it convenient to compare absolute momentum strength across securities.

The strategy first calculates the one-day price change abs(close - close[1]) as the original momentum xMom. Then it calculates the SMA of xMom over Length days, denoted as xSMA_mom. After that, it calculates the price change over Length days xMomLength, namely close - close[Length]. Finally, CMO is calculated as xMomLength divided by xSMA_mom then multiplied by 100. This CMO is smoothed by a WMA (parameter LengthWMA) to derive xWMACMO. The trading signal is to go long (short) when CMO crosses above (below) its WMA.  

## Advantages

The biggest advantage of this strategy is capturing momentum characteristics within price trends. The bounded design of CMO reflects momentum changes more directly. Compared to SMA, WMA smoothes out short-term noise better. So this strategy can effectively identify entry points within medium-to-long term trends. In addition, the combination of CMO and WMA provides better stability than a single indicator.

## Risks

The biggest risk of this strategy is the high trading frequency leading to increased slippage costs. Both CMO and WMA have short-term parameters, which may cause excessive meaningless whipsaws. This is especially severe when the trading vehicle has large fluctuations. In addition, fixed parameters fail to adapt to changing market environments.

We can consider introducing adaptive optimization of CMO and WMA parameters, enabling them to adjust dynamically. Adding filter conditions to reduce unnecessary trading is another option. Lowering volatility via portfolio diversification also helps.  

## Enhancement Directions 

The strategy can be enhanced from the following aspects:

1. Add adaptive CMO parameter mechanism to find optimal parameters for different volatility regimes;  

2. Add adaptive WMA parameter mechanism so the smoothing effect changes accordingly;

3. Add filter conditions such as Volatility Index to control meaningless whipsaws;  

4. Consider combining with other indicators to improve stability;

5. Optimize stop loss mechanism. Set dynamic stop loss line to actively control single round loss.

## Conclusion  

The strategy realizes simple and effective trend following based on CMO and WMA. Its advantage lies in clearly capturing price momentum characteristics. But it also has some weakness in profit retention capability after opening positions. Both parameter tuning and combo can greatly improve stability. Overall, this strategy has lots of room and value for improvement.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Length|
|v_input_2|9|LengthWMA|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-21 00:00:00
end: 2023-11-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 13/02/2017
//    This indicator plots Chandre Momentum Oscillator and its WMA on the 
//    same chart. This indicator plots the absolute value of CMO.
//    The CMO is closely related to, yet unique from, other momentum oriented 
//    indicators such as Relative Strength Index, Stochastic, Rate-of-Change, 
//    etc. It is most closely related to Welles Wilder?s RSI, yet it differs 
//    in several ways:
//    - It uses data for both up days and down days in the numerator, thereby 
//        directly measuring momentum;
//    - The calculations are applied on unsmoothed data. Therefore, short-term 
//        extreme movements in price are not hidden. Once calculated, smoothing 
//        can be applied to the CMO, if desired;
//    - The scale is bounded between +100 and -100, thereby allowing you to clearly 
//        see changes in net momentum using the 0 level. The bounded scale also allows 
//        you to conveniently compare values across different securities.
////////////////////////////////////////////////////////////
strategy(title="CMO & WMA", shorttitle="CMO & WMA")
Length = input(9, minval=1)
LengthWMA = input(9, minval=1)
reverse = input(false, title="Trade reverse")
hline(0, color=gray, linestyle=line)
xMom = abs(close - close[1])
xSMA_mom = sma(xMom, Length)
xMomLength = close - close[Length]
nRes = 100 * (xMomLength / (xSMA_mom * Length))
xWMACMO = wma(nRes, LengthWMA)
pos = iff(nRes > xWMACMO, 1,
	   iff(nRes <= xWMACMO, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
         iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue)
plot(nRes, color=blue, title="CMO")
plot(xWMACMO, color=red, title="WMA")
```

> Detail

https://www.fmz.com/strategy/433583

> Last Modified

2023-11-28 16:42:54
