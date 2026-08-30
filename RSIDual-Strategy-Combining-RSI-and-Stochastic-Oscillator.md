
> Name

Dual-Strategy-Combining-RSI-and-Stochastic-Oscillator
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy combines the relative strength index (RSI) with the stochastic indicator to form a dual strategy to more accurately determine the overbought and oversold status of the market, thereby obtaining more reliable trading signals.
## Strategy Principle
In this strategy, the RSI length is 14 periods, the overbuy threshold is 70, and the oversell threshold is 30. The K value of the stochastic indicator is calculated using a 3-period moving average, and the D value is the 3-period moving average of the K value. When the K line breaks through the D line from bottom to top, it is determined to be an overbought signal, and vice versa, it is an oversold signal.
The strategy uses a combination of RSI indicators and stochastic indicators to send trading signals:
1. When the stochastic indicator crosses upward (the K line crosses the D line from below) and the RSI indicator is higher than 70, it is judged as an overbought signal and goes short.
2. When the stochastic indicator crosses downwards (the K line crosses the D line from above) and the RSI indicator is lower than 30, it is judged to be an oversold signal, so go long.
This dual combination strategy makes full use of the advantages of the RSI indicator to judge overbought and oversold, and combines the trendiness of the stochastic indicator to filter out false signals, thereby generating more reliable trading signals.
## Advantage Analysis
The biggest advantage of this dual strategy is that it can effectively reduce false signals and improve signal reliability.
When the RSI indicator is used alone, it will produce more false signals. This is because the RSI indicator itself only determines the overbought and oversold status of the price and cannot reflect the direction of the trend. Therefore, many RSI signals alone are unreliable.
The stochastic indicator can determine the direction of the price trend. The K line crossing the D line indicates that the upward trend of prices may continue. At this time, the RSI overbought signal is more reliable and is judged to be true overbought rather than false overbought.
On the contrary, if the K line crosses the D line, it indicates that the price trend may reverse. Even if the RSI shows an oversold signal, it may be false oversold and no transaction will be made.
Therefore, the combination of RSI and stochastic indicators can better grasp the overbought and oversold status of the price and the directionality of the trend, filter out a large number of unreliable signals, and obtain more accurate trading opportunities.
## Risk Analysis
This strategy also has certain risks that need to be noted:
1. Although the combination of dual indicators can filter out false signals, it may also miss some real signals, thereby missing trading opportunities.
2. The parameter settings of RSI and stochastic indicators need to have a good relationship. For example, the RSI period is too short, and the smoothness of the stochastic indicator K and D values ​​​​is improper, which will affect the accuracy of the signal.
3. When the indicator sends a signal, it needs to be confirmed based on price momentum, trading volume and other factors to avoid entering a false breakthrough.
4. Pay attention to systemic risks and avoid blind trading when the market fluctuates violently.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Optimize the parameters of RSI and stochastic indicators and find the best parameter combination. Parameter tuning can be performed through backtest data, or machine learning methods can be used to dynamically optimize parameters.
2. Increase confirmation indicators of trading volume, such as a sudden increase in trading volume to verify buying and selling signals.
3. Combine with trend confirmation indicators such as moving averages to avoid being pulled by the volatile market. For example, only consider buy signals when the trend is up.
4. Use machine learning methods to identify more complex buying and selling rules, such as combining Bollinger Bands, price patterns and other signals to improve strategy stability.
5. Use cutting-edge technologies such as deep learning to develop more intelligent diversified trading systems and optimize strategy rules in a larger sample space.
## Summarize
This dual combination strategy of RSI and stochastic indicators rationally utilizes the advantages of each indicator through the idea of ​​indicator integration to form a complementary effect. It has higher signal filtering accuracy than a single RSI indicator, thereby obtaining more accurate and reliable trading signals. However, we still need to pay attention to issues such as parameter optimization and risk management. This strategy idea can be extended to other indicator combinations to discover more effective quantitative trading strategies.
||


## Overview

This strategy combines the Relative Strength Index (RSI) with the Stochastic oscillator to form a dual strategy for more accurately identifying overbought and oversold market conditions, thus generating more reliable trading signals.

## How It Works

The RSI in this strategy has a period of 14, with overbought threshold at 70 and oversold threshold at 30. The %K line of the Stochastic oscillator uses a 3-period SMA, and its %D line is a 3-period SMA of %K. A bullish crossover happens when %K crosses above %D, while a bearish crossover occurs when %K crosses below %D.

The trading signals are generated based on the combined indicators:

1. When a bullish crossover happens on the Stochastic and RSI is above 70, an overbought signal is generated for going short. 

2. When a bearish crossover happens on the Stochastic and RSI is below 30, an oversold signal is generated for going long.

This dual strategy takes advantage of RSI's strength in identifying overbought/oversold levels, while using the Stochastic's trend-following feature to filter out false signals, resulting in more reliable trade entries.

## Advantages

The biggest advantage of this dual strategy is the significantly reduced false signals and improved reliability.

RSI alone can generate excessive false signals. This is because RSI only reflects price overextension levels without considering trend direction. Thus, standalone RSI signals tend to be unreliable.

On the other hand, the Stochastic oscillator can identify trend direction. An upward crossover suggests upside momentum may persist, making overbought RSI signals more reliable. 

Conversely, a downward crossover implies impending trend reversal. Oversold RSI signals may be false signals in this case.

Therefore, combining RSI and the Stochastic can better identify both overextension levels and trend directionality, filtering out unreliable signals and locating high-probability turning points.

## Risks

There are also risks to consider when using this strategy:

1. The dual indicator approach may filter out some valid signals, causing missed trading opportunities.

2. Fine tuning of parameters like RSI period and Stochastic smoothing is key, otherwise signal accuracy could be compromised. 

3. Price momentum and volume confirmation are still necessary when taking signals to avoid false breakouts.

4. Be aware of systemic risks and avoid blind trading during high market volatility.

## Enhancement

This strategy can be further enhanced from several aspects:

1. Optimize RSI and Stochastic parameters through backtesting to find ideal combinations. Machine learning techniques can also be applied for dynamic parameter optimization.

2. Incorporate volume indicators for signal confirmation, like volume spikes. 

3. Add trend-following overlays like moving averages to avoid market noise and whipsaws. Only consider buy signals when the trend is up.

4. Utilize machine learning to uncover more sophisticated signal combinations incorporating Bollinger Bands, price patterns, etc. to improve consistency. 

5. Leverage deep learning and big data analytics to develop more intelligent multipurpose trading systems with higher sample efficiency.

## Conclusion

In summary, the RSI-Stochastic dual strategy effectively utilizes the strengths of each through ensemble modeling. Compared to standalone RSI, it offers superior filtering capacity and signal precision. Caveats include parameter optimization and risk control. The methodology can be extended to combining other indicators for discovering novel effective trading strategies.

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
|v_input_9|22|LookBack Period Standard Deviation High|
|v_input_10|20|Bolinger Band Length|
|v_input_11|2|Bollinger Band Standard Devaition Up|
|v_input_12|50|Look Back Period Percentile High|
|v_input_13|0.85|Highest Percentile - 0.90=90%, 0.95=95%, 0.99=99%|
|v_input_14|false|-------Text Plots Below Use Original Criteria-------|
|v_input_15|false|Show Text Plot if WVF WAS True and IS Now False|
|v_input_16|false|Show Text Plot if WVF IS True|
|v_input_17|false|-------Text Plots Below Use FILTERED Criteria-------|
|v_input_18|true|Show Text Plot For Filtered Entry|
|v_input_19|true|Show Text Plot For AGGRESSIVE Filtered Entry|
|v_input_20|40|Long-Term Look Back Current Bar Has To Close Below This Value OR Medium Term--Default=40|
|v_input_21|14|Medium-Term Look Back Current Bar Has To Close Below This Value OR Long Term--Default=14|
|v_input_22|3|Entry Price Action Strength--Close > X Bars Back---Default=3|
|v_input_23|false|-------------------------Turn On/Off ALERTS Below---------------------|
|v_input_24|false|----To Activate Alerts You HAVE To Check The Boxes Below For Any Alert Criteria You Want----|
|v_input_25|false|Show Alert WVF = True?|
|v_input_26|false|Show Alert WVF Was True Now False?|
|v_input_27|false|Show Alert WVF Filtered?|
|v_input_28|false|Show Alert WVF AGGRESSIVE Filter?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-30 00:00:00
end: 2023-10-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
//Based on Divergences and Hidden Divergences
//Locates bottom market and reversals

strategy("Vix FIX / StochRSI Strategy", pyramiding=9, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=3, overlay=false)

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

pd = input(22, title="LookBack Period Standard Deviation High")
bbl = input(20, title="Bolinger Band Length")
mult = input(2.0    , minval=1, maxval=5, title="Bollinger Band Standard Devaition Up")
lb = input(50  , title="Look Back Period Percentile High")
ph = input(.85, title="Highest Percentile - 0.90=90%, 0.95=95%, 0.99=99%")
new = input(false, title="-------Text Plots Below Use Original Criteria-------" )
sbc = input(false, title="Show Text Plot if WVF WAS True and IS Now False")
sbcc = input(false, title="Show Text Plot if WVF IS True")
new2 = input(false, title="-------Text Plots Below Use FILTERED Criteria-------" )
sbcFilt = input(true, title="Show Text Plot For Filtered Entry")
sbcAggr = input(true, title="Show Text Plot For AGGRESSIVE Filtered Entry")
ltLB = input(40, minval=25, maxval=99, title="Long-Term Look Back Current Bar Has To Close Below This Value OR Medium Term--Default=40")
mtLB = input(14, minval=10, maxval=20, title="Medium-Term Look Back Current Bar Has To Close Below This Value OR Long Term--Default=14")
str = input(3, minval=1, maxval=9, title="Entry Price Action Strength--Close > X Bars Back---Default=3")
//Alerts Instructions and Options Below...Inputs Tab
new4 = input(false, title="-------------------------Turn On/Off ALERTS Below---------------------" )
new5 = input(false, title="----To Activate Alerts You HAVE To Check The Boxes Below For Any Alert Criteria You Want----")
sa1 = input(false, title="Show Alert WVF = True?")
sa2 = input(false, title="Show Alert WVF Was True Now False?")
sa3 = input(false, title="Show Alert WVF Filtered?")
sa4 = input(false, title="Show Alert WVF AGGRESSIVE Filter?")

//Williams Vix Fix Formula
wvf = ((highest(close, pd)-low)/(highest(close, pd)))*100
sDev = mult * stdev(wvf, bbl)
midLine = sma(wvf, bbl)
lowerBand = midLine - sDev
upperBand = midLine + sDev
rangeHigh = (highest(wvf, lb)) * ph

//Filtered Bar Criteria
upRange = low > low[1] and close > high[1]
upRange_Aggr = close > close[1] and close > open[1]
//Filtered Criteria
filtered = ((wvf[1] >= upperBand[1] or wvf[1] >= rangeHigh[1]) and (wvf < upperBand and wvf < rangeHigh))
filtered_Aggr = (wvf[1] >= upperBand[1] or wvf[1] >= rangeHigh[1]) and not (wvf < upperBand and wvf < rangeHigh)

//Alerts Criteria
alert1 = wvf >= upperBand or wvf >= rangeHigh ? 1 : 0
alert2 = (wvf[1] >= upperBand[1] or wvf[1] >= rangeHigh[1]) and (wvf < upperBand and wvf < rangeHigh) ? 1 : 0
alert3 = upRange and close > close[str] and (close < close[ltLB] or close < close[mtLB]) and filtered ? 1 : 0
alert4 = upRange_Aggr and close > close[str] and (close < close[ltLB] or close < close[mtLB]) and filtered_Aggr ? 1 : 0

//Coloring Criteria of Williams Vix Fix
col = wvf >= upperBand or wvf >= rangeHigh ? lime : gray

isOverBought = (crossover(k,d) and k > StochOverBought) ? 1 : 0
isOverBoughtv2 = k > StochOverBought ? 1 : 0
filteredAlert = alert3 ? 1 : 0
aggressiveAlert = alert4 ? 1 : 0

plot(isOverBought, "Overbought / Crossover", style=line, color=red) 
plot(filteredAlert, "Filtered Alert", style=line, color=fuchsia) 
plot(aggressiveAlert, "Aggressive Alert", style=line, color=orange)

if (filteredAlert or aggressiveAlert)
    strategy.entry("Long", strategy.long)

if (isOverBought)
    strategy.close("Long")

    

```

> Detail

https://www.fmz.com/strategy/428627

> Last Modified

2023-10-07 16:19:30
