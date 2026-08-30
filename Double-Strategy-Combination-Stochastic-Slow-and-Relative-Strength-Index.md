
> Name

Double-Strategy-Combination-Stochastic-Slow-and-Relative-Strength-Index Double-Strategy-Combination-Stochastic-Slow-and-Relative-Strength-Index
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12848735667b4fbe6b8.png)
[trans]

## Overview
This strategy uses a combination of the classic stochastic slow indicator strategy and the relative strength indicator strategy to form a dual strategy. When the stochastic indicator exceeds 80, it is short and when it is below 20, it is long; at the same time, when the RSI exceeds 70, it is short and when it is below 30, it is long. Only when both are triggered at the same time, the position will be opened.
## Strategy Principle
This strategy is mainly based on two classic indicators - the stochastic slow indicator and the RSI indicator, and sets a threshold to determine overbought and oversold conditions.
**Stochastic Slow Indicator Section:**
- Set Stochlength to 14 to calculate the lookback length of the stochastic indicator
- Set StochOverBought to 80 and StochOverSold to 20 as the threshold for judging overbought and oversold.
- Set smoothK to 3 and smoothD to 3, which are the smoothing parameters of the %K line and %D line respectively.
The calculated %K line and %D line are named k and d in the code.
When the %K line breaks through the %D line from bottom to top, it is a bullish signal. When crossing from top to bottom, it is a bearish signal. At the same time, combined with the judgment of overbought and oversold, it can be used to judge opportunities.
**RSI Section:**
- Set RSIlength to 14 to calculate the lookback length of the RSI indicator.
- Set RSIOverBought to 70 and RSIOverSold to 30 as the threshold for judging overbought and oversold.
The calculated RSI indicator is named vrsi.
When the RSI indicator rises above 70, it is an overbought signal, and when it falls below 30, it is an oversold signal.
**Dual strategy trigger conditions:**
This strategy will only open a position when the stochastic indicator and the RSI indicator simultaneously display overbought or oversold signals, that is, both exceed their respective thresholds.
This combination uses the complementarity of the two indicators, which can reduce false signals and improve signal reliability.
## Advantage Analysis
This dual strategy combination combines two classic strategies, the stochastic slow indicator and the RSI indicator, and has the following advantages:
1. Dual indicator combination can verify each other, reduce false signals, and improve signal quality and reliability.
2. Stochastic indicator determines overbought and oversold conditions, and RSI also determines overbought and oversold conditions. The combination of the two makes the results more reliable and accurate.
3. The random indicator uses %K and %D, and the smoothing parameters are adjustable to avoid being affected by einzelnen extreme values.
4. The RSI indicator responds quickly, and the stochastic indicator determines mid- and long-term trends and turning points. The combination of the two makes the strategy more complete.
5. The trading style is conservative and only opens positions when both indicators are displayed to avoid rash advances and reduce the frequency of transactions.
## Risks and Solutions
There are also some risks in this strategy, mainly including:
1. Parameter setting risks
Improperly set threshold parameters can result in missed opportunities or false signals. The best parameters can be found through optimization and repeated testing.
2. Insufficient signals from the dual strategy
Due to the dual strategy, the signal generation frequency will be relatively low and the position utilization rate will not be high. The parameters can be appropriately relaxed and the number of signals can be increased.
3. Indicator lag problem
Both the stochastic indicator and the RSI indicator have a certain lag and may miss opportunities for rapid changes. It can be assisted by combining more sensitive indicators.
4. The problem of inapplicability of specific varieties
This strategy is more suitable for some relatively stable and volatile products, such as stock indexes, precious metals, etc. It may not be suitable for some less volatile varieties.
## Optimization ideas
This strategy can also be optimized from the following aspects:
1. Parameter optimization
The best parameter combination can be found through automatic optimization of the algorithm or manual optimization of parameters.
2. Add a stop loss mechanism
You can set a trailing stop loss or a percentage stop loss to control single losses.
3. Combined with other indicators
Energy indicators, moving averages, etc. can be introduced as indicators to assist in judging signal quality.
4. Appropriately relax the conditions for dual strategies
The trigger threshold of the dual strategy can be appropriately relaxed and the number of signals can be increased.
## Summarize
This strategy uses a dual combination of the stochastic slow indicator and the RSI indicator. It is triggered when both show overbought and oversold signals at the same time. It has the advantages of accurate and reliable signals and a conservative trading style. There are also some problems such as parameter setting risks and a small number of signals. We can improve and optimize through parameter optimization, stop loss setting, and introduction of other indicators to make the strategy more stable and reliable.
||


## Overview

This strategy combines the classic Stochastic Slow strategy and Relative Strength Index (RSI) strategy to form a double strategy. It will open position when Stochastic exceeds 80 (short) or drops below 20 (long) meanwhile RSI exceeds 70 (short) or drops below 30 (long).

## Strategy Logic  

This strategy mainly utilizes two classic indicators – Stochastic Slow indicator and RSI indicator, and sets threshold values to determine overbought and oversold conditions.

**Stochastic Slow Part:**  

- Set Stochlength as 14, the lookback period for Stochastic calculation   
- Set StochOverBought as 80 and StochOverSold as 20, threshold values for overbought and oversold  
- Set smoothK as 3 and smoothD as 3, smoothing parameters for %K and %D line

The calculated %K and %D lines are named as k and d in the code. 

When %K crosses over %D from below, it is a long signal. When crosses under from above, it is a short signal. Combine with overbought/oversold judgment, it can be used to identify opportunities.

**RSI Part:**

- Set RSIlength as 14, the lookback period for RSI calculation  
- Set RSIOverBought as 70 and RSIOverSold as 30, threshold values for overbought and oversold

The calculated RSI indicator is named as vrsi in the code.  

When RSI rises above 70, it sends an overbought signal. When drops below 30, it sends an oversold signal.

**Double Strategy Entry Logic:**

This strategy will only open position when both Stochastic and RSI indicate overbought/oversold signals at the same time, meaning passing their own threshold values.

This combination utilizes the complementary property of two indicators to increase signal reliability and decrease false signals.  

## Advantage Analysis   

The advantages of this double strategy combination are:

1. Combination of two indicators can validate each other, decrease false signals and increase signal quality  
2. Stochastic judges overbought/oversold conditions, RSI does the same job. Combination makes the results more reliable.   
3. Stochastic uses %K and %D crossover system, smoothing parameters make it robust to outliers
4. RSI reacts fast to latest changes, Stochastic judges middle-to-long term trends and turning points. Complete strategy.
5. Conservative trading style, only open positions when both indicators agree. Less trades, avoid over-trading.

## Risks and Solutions

There are some risks associated with this strategy:

1. Parameter tuning risk

   Improper parameter settings may lead to missing good opportunities or generating false signals. We can optimize parameters through quantitative algorithms or manual tuning to find the best combination.  

2. Lack of signals

   Due to the dual indicator system, signal frequency could be relatively low and position utilization ratio is not high. We can properly relax the parameters to generate more entry signals.

3. Lagging risk 

   Both Stochastic and RSI have some lagging effect, which may cause missing rapid chances. More sensitive indicators can be introduced for assistance.

4. Instruments specificity

   This strategy may fits better for some violent fluctuated instruments like stock indices and gold. For smooth instruments, it may not be applicable.

## Optimization Directions  

This strategy can be further optimized in the following aspects:  

1. Parameter optimization

   Optimize the parameters quantitatively or manually to find the best parameter combination.  

2. Introduce stop loss mechanism

   Set stop loss based on price movement or percentage to control single trade loss.  

3. Combine with other indicators

   Introduce other indicators like volume, moving average to assist judging signal quality.

4. Relax double strategy conditions

   Appropriately relax the thresholds of double strategy to generate more entry signals.

## Conclusion

This strategy combines Stochastic Slow and RSI in double-confirmation mode, entering positions only when both indicators agree on overbought/oversold signals. It features high signal reliability, conservative trading style etc. Also has some risks like parameter tuning, lack of signals. Further improvements can be made through parameter optimization, stop loss introduction, adding assisting indicators to enhance stability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|lookback length of Stochastic|
|v_input_2|80|Stochastic overbought condition|
|v_input_3|20|Stochastic oversold condition|
|v_input_4|3|smoothing of Stochastic %K |
|v_input_5|3|moving average of Stochastic %K|
|v_input_6|14|lookback length of RSI|
|v_input_7|70|RSI overbought condition|
|v_input_8|30|RSI oversold condition|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-19 00:00:00
end: 2023-12-26 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Stochastic + RSI, Double Strategy (by ChartArt)", shorttitle="CA_-_RSI_Stoch_Strat", overlay=true)

// ChartArt's Stochastic Slow + Relative Strength Index, Double Strategy
//
// Version 1.0
// Idea by ChartArt on October 23, 2015.
//
// This strategy combines the classic RSI
// strategy to sell when the RSI increases
// over 70 (or to buy when it falls below 30),
// with the classic Stochastic Slow strategy
// to sell when the Stochastic oscillator
// exceeds the value of 80 (and to buy when
// this value is below 20).
//
// This simple strategy only triggers when
// both the RSI and the Stochastic are together
// in overbought or oversold conditions.
//
// List of my work: 
// https://www.tradingview.com/u/ChartArt/


///////////// Stochastic Slow
Stochlength = input(14, minval=1, title="lookback length of Stochastic")
StochOverBought = input(80, title="Stochastic overbought condition")
StochOverSold = input(20, title="Stochastic oversold condition")
smoothK = input(3, title="smoothing of Stochastic %K ")
smoothD = input(3, title="moving average of Stochastic %K")
k = sma(stoch(close, high, low, Stochlength), smoothK)
d = sma(k, smoothD)

 
///////////// RSI 
RSIlength = input( 14, minval=1 , title="lookback length of RSI")
RSIOverBought = input( 70  , title="RSI overbought condition")
RSIOverSold = input( 30  , title="RSI oversold condition")
RSIprice = close
vrsi = rsi(RSIprice, RSIlength)


///////////// Double strategy: RSI strategy + Stochastic strategy

if (not na(k) and not na(d))
    if (crossover(k,d) and k < StochOverSold)
        if (not na(vrsi)) and (crossover(vrsi, RSIOverSold))
            strategy.entry("LONG", strategy.long, comment="StochLE + RsiLE")
 
 
if (crossunder(k,d) and k > StochOverBought)
    if (crossunder(vrsi, RSIOverBought))
        strategy.entry("SHORT", strategy.short, comment="StochSE + RsiSE")
 
 
//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)WQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQ
```

> Detail

https://www.fmz.com/strategy/436762

> Last Modified

2023-12-27 15:18:40
