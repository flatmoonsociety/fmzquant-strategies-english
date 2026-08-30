
> Name

Oscillation-Positioning-Breakthrough-Strategy-with-Multiple-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/aa7e688f935244a704.png)
[trans]


## Overview
This strategy achieves precise positioning of market fluctuations by combining multiple indicators such as STOCH.RSI, RSI, dual strategy, CM Williams indicator and money flow index (MFI), looking for opportunities to long/short. Trading signals can be issued when a stock's price approaches a support or pressure level. This strategy comprehensively utilizes the advantages of multiple indicators, and through mutual verification of indicators, it can effectively reduce the false alarm rate and enhance the reliability of the signal.
## Strategy Principle
1. The STOCH.RSI indicator combines the advantages of the stochastic indicator Stochastic and the relative strength index RSI. It can display overbought and oversold areas and find reversal opportunities.
2. The RSI indicator determines overbought and oversold and serves as an auxiliary verification signal.
3. The dual strategy determines the intersection of Stoch and RSI and sends trading signals.
4. The CM Williams indicator calculates percentile ranges. The pop-up of this range represents the reversal of the market, and serves as a basis for assisting Stoch.RSI and RSI in judging market fluctuations and reversals.
5. The Money Flow Index (MFI) determines the inflow and outflow of funds and verifies each other with Stoch.RSI and RSI to improve signal quality.

In summary, this strategy can effectively determine the overbought and oversold areas of the market, locate reversal opportunities, and issue trading signals through the combination of multiple indicators such as Stoch.RSI, RSI, dual strategy, CM Williams indicator, and MFI. Combination verification of multiple indicators can improve signal quality and reduce false alarms.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Multiple indicator combinations and mutual verification can reduce false alarms and improve signal quality.
2. Use STOCH.RSI, RSI and MFI to determine overbought and oversold areas, which can effectively locate market reversal points.
3. The CM Williams indicator calculates the percentile range, which can assist in judging market fluctuations and reversals.
4. The dual strategy sends trading signals, which is simple to operate and easy to track.
5. There is a large space for parameter optimization, parameters can be adjusted according to different markets, and the adaptability is strong.
## Risk Analysis
There are also some risks with this strategy:
1. The calculation of multi-indicator combination is relatively complex and requires high computing power, so it is not suitable for high-frequency trading.
2. Improper parameter settings may lead to a decrease in signal quality. You should choose parameters that suit you.
3. The reversal signal may lag, and more indicators need to be combined to judge the trend.
4. The number of transactions may be large, and the efficiency of capital utilization needs to be controlled.
Corresponding solutions:
1. Choose a terminal with strong computing power and optimize the parameters.
2. Do a good job of backtesting and choose a parameter combination that suits you.
3. Use it in combination with more indicators to judge trends in advance.
4. Optimize the stop loss mechanism and control the risk of a single transaction.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize indicator parameters and select the best parameter combination.
2. Add volume, profit factor and other indicators to improve trading and stock selection capabilities.
3. Combine with more convergence lines, Bollinger Bands and other indicators to determine support and resistance in advance.
4. Add stop loss and market entry screening conditions to control risks.
5. Different varieties and cycle parameters are different. The best parameters can be selected according to the characteristics of the variety.
## Summarize
This strategy uses the precise combination of STOCH.RSI, RSI, dual strategy, CM Williams indicator and MFI multi-indicator to locate the overbought and oversold areas of the market and discover reversal opportunities. Mutual verification of signals can reduce false alarms and improve signal quality. By further improving it through parameter optimization and adding other judgment conditions, it can become a stable and practical trading strategy.
||
## Overview

This strategy combines multiple indicators including STOCH.RSI, RSI, Dual Strategy, CM Williams Indicator and Money Flow Index (MFI) to accurately locate market fluctuations and looking for opportunities to long/short. It can generate trading signals when stock prices approach support or resistance levels. By integrating the advantages of multiple indicators and cross validation, this strategy can effectively reduce false signals and enhance reliability.

## Strategy Logic   

1. STOCH.RSI combines the strengths of Stochastic Oscillator and Relative Strength Index (RSI), displaying overbought/oversold levels to detect reversal opportunities.

2. RSI judges overbought/oversold conditions as an auxiliary confirmation.

3. Dual Strategy determines crossovers between Stoch and RSI to generate trading signals.  

4. CM Williams Indicator calculates percentile bands. Bouncing off the bands represents market reversal, assisting judgement of fluctuations and reversals.

5. Money Flow Index (MFI) judges fund flows, validating signals together with Stoch.RSI and RSI to improve quality.

In summary, by combining Stoch.RSI, RSI, Dual Strategy, CM Williams and MFI, this strategy can effectively determine overbought/oversold levels, locate reversal points and generate quality signals. Cross validation by multiple indicators improves reliability and reduces false signals. 

## Advantage Analysis

The main advantages of this strategy include:

1. Multiple indicators combination improves signal quality by validation and reduces false signals.

2. STOCH.RSI, RSI and MFI effectively spot overbought/oversold zones and market turning points.

3. CM Williams calculates percentile bands to assist judging market fluctuations and reversals. 

4. Dual Strategy generates simple trading signals that are easy to follow.

5. Highly customizable with a wide range of optimizable parameters adaptable to different markets.

## Risk Analysis   

Some risks to note:

1. Complex multi-indicator computations demand high computing power, unsuitable for high frequency trading.

2. Improper parameter tuning could deteriorate signal quality. Parameters should suit personal style.

3. Reversal signals may lag. More indicators could assist trend judgment.

4. High trading frequency may lead to poor capital utilization. 

Solutions:

1. Use powerful terminals and optimize parameters.  

2. Backtest extensively to find optimal personal parameters.  

3. Add more indicators to determine trends in advance.

4. Optimize risk control mechanisms like stop loss to limit loss per trade.

## Optimization Directions

This strategy can be improved in the following aspects:

1. Optimize indicator parameters to find the optimal combination. 

2. Add indicators like volume and profit factor to enhance stock selection.

3. Incorporate more trend lines, Bollinger Bands etc. to forecast support/resistance levels.  

4. Add stop loss, market entry filters to control risk.

5. Parameters vary for different products and timeframes based on characteristics.

## Conclusion

This strategy locates market reversals by accurately combining multiple indicators including STOCH.RSI, RSI, Dual Strategy, CM Williams and MFI. Cross validation improves signal quality and reduces false signals. Further enhancements like parameter optimization and additional filters can make it a stable, practical trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|Stochastic %K Smoothing|
|v_input_2|3|Stochastic %K Moving Average|
|v_input_3|14|RSI Lenght|
|v_input_4|14|Stochastic Lenght|
|v_input_5|80|Stochastic RSI overbought|
|v_input_6|20|Stochastic RSI oversold|
|v_input_7|70|RSI overbought|
|v_input_8|30|RSI oversold|
|v_input_9|22|LookBack Period Standard Deviation High|
|v_input_10|20|Bollinger Band Length|
|v_input_11|2|Bollinger Band Standard Devaition Up|
|v_input_12|50|Look Back Period Percentile High|
|v_input_13|0.85|Highest Percentile - 0.90=90%, 0.95=95%, 0.99=99%|
|v_input_14|1.01|Lowest Percentile - 1.10=90%, 1.05=95%, 1.01=99%|
|v_input_15|false|Show High Range (Based on Percentile and LookBack Period)?|
|v_input_16|false|Show Standard Deviation Line?|
|v_input_17|14|MFI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-31 00:00:00
end: 2023-11-30 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


     //////////////////////////////////////////////////////////////////////////
    ////  STOCHASTIC_RSI+RSI+DOUBLE_STRATEGY+CM_WILLIAMS_VIX_FIX+MFI  ////////
   //////////////////////////////////////////////////////////////////////////


//  This is a simple combination of integrated and published scripts, useful 
//  if you don't have a PRO account and want to bypass the 3 indicators limit. 
//  It includes:
//  1) Stoch.RSI
//  2) Relative strenght index (RSI)
//  3) Stochastic + RSI, Double Strategy (by ChartArt)
//  4) CM_Williams_Vix_Fix Finds Market Bottoms (by ChrisMoody)
//  5) Monetary Flow Index (MFI)
//  For more details about 3) and 4) check the original scripts.


//@version=3
// @author GianlucaBezziccheri

strategy(title="Stoch.RSI+RSI+DoubleStrategy+CMWilliamsVixFix+MFI", shorttitle="Stoch.RSI+RSI+DoubleStrategy+CMWilliamsVixFix+MFI")


///STOCH.RSI///
smoothK = input(3, minval=1, title="Stochastic %K Smoothing")
smoothD = input(3, minval=1, title="Stochastic %K Moving Average")
lengthRSI = input(14, minval=1, title="RSI Lenght")
lengthStoch = input(14, minval=1, title="Stochastic Lenght")
RSIprice = close
rsi1 = rsi(RSIprice, lengthRSI)
k = sma(stoch(rsi1, rsi1, rsi1, lengthStoch), smoothK)
d = sma(k, smoothD)
plot(k, color=blue, linewidth=2)
plot(d, color=silver, linewidth=2)
h0 = hline(80)
h1 = hline(20)
fill(h0, h1, color=purple, transp=78)


///RSI///
up = rma(max(change(RSIprice), 0), lengthRSI)
down = rma(-min(change(RSIprice), 0), lengthRSI)
rsi2 = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
plot(rsi2, color=fuchsia, linewidth=2)
band0 = hline(70)
band1 = hline(30)
fill(band0, band1, color=purple, transp=100)


///OVERBOUGHT-OVERSOLD STRATEGY///
StochOverBought = input(80, title="Stochastic RSI overbought")
StochOverSold = input(20, title="Stochastic RSI oversold")
ks = sma(stoch(close, high, low, lengthStoch), smoothK)
ds = sma(k, smoothD)
RSIOverBought = input( 70  , title="RSI overbought")
RSIOverSold = input( 30  , title="RSI oversold")
vrsi = rsi(RSIprice, lengthRSI)
if (not na(ks) and not na(ds))
    if (crossover(ks,ds) and k < StochOverSold)
        if (not na(vrsi)) and (crossover(vrsi, RSIOverSold))
            strategy.entry("LONG", strategy.long, comment="LONG")
if (crossunder(ks,ds) and ks > StochOverBought)
    if (crossunder(vrsi, RSIOverBought))
        strategy.entry("SHORT", strategy.short, comment="SHORT")
 
 
///CM WILLIAMS VIX FIX///
pd = input(22, title="LookBack Period Standard Deviation High")
bbl = input(20, title="Bollinger Band Length")
mult = input(2.0    , minval=1, maxval=5, title="Bollinger Band Standard Devaition Up")
lb = input(50  , title="Look Back Period Percentile High")
ph = input(.85, title="Highest Percentile - 0.90=90%, 0.95=95%, 0.99=99%")
pl = input(1.01, title="Lowest Percentile - 1.10=90%, 1.05=95%, 1.01=99%")
hp = input(false, title="Show High Range (Based on Percentile and LookBack Period)?")
sd = input(false, title="Show Standard Deviation Line?")
wvf = ((highest(close, pd)-low)/(highest(close, pd)))*100
sDev = mult * stdev(wvf, bbl)
midLine = sma(wvf, bbl)
lowerBand = midLine - sDev
upperBand = midLine + sDev
rangeHigh = (highest(wvf, lb)) * ph
rangeLow = (lowest(wvf, lb)) * pl
col = wvf >= upperBand or wvf >= rangeHigh ? lime : gray
plot(hp and rangeHigh ? rangeHigh : na, title="Range High Percentile", style=line, linewidth=4, color=orange)
plot(hp and rangeLow ? rangeLow : na, title="Range High Percentile", style=line, linewidth=4, color=orange)
plot(wvf, title="Williams Vix Fix", style=columns, linewidth = 4, color=col, transp=85)
plot(sd and upperBand ? upperBand : na, title="Upper Band", style=line, linewidth = 3, color=aqua)


///MONETARY FLOW INDEX
length4 = input(title="MFI Length", defval=14, minval=1, maxval=2000)
src4 = hlc3
upper4 = sum(volume * (change(src4) <= 0 ? 0 : src4), length4)
lower4 = sum(volume * (change(src4) >= 0 ? 0 : src4), length4)
mf4 = rsi(upper4, lower4)
plot(mf4, color=yellow, style=line, linewidth=2, title="Monetary Flow Index")
overbought=hline(70, title="MFI Overbought", color=yellow)
oversold=hline(30, title="MFI Oversold", color=yellow)
fill(overbought, oversold, color=#9915ff, transp=100)
```

> Detail

https://www.fmz.com/strategy/433958

> Last Modified

2023-12-01 17:49:34
