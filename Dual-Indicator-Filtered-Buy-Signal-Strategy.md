
> Name

Dual-Indicator-Filtered-Buy-Signal-Strategy Dual-Indicator-Filtered-Buy-Signal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9131082e9ac43db238.png)

[trans]

## Overview
The Dual Indicator Buy Filter Buy Signal Strategy utilizes a combination of the Stochastic RSI and Bollinger Bands indicators to identify potential buying opportunities. This strategy uses multiple filters to distinguish the most profitable buy points. This enables it to identify high-probability buying opportunities in a volatile market environment.
## Strategy Principle
This strategy uses two sets of indicators to identify buying opportunities.
First, it uses a stochastic exponential smoothed moving average to determine whether the market is oversold. This indicator combines the stochastic index and its smooth moving average. When the %K line crosses its %D line from the low, it is considered an oversold signal. A threshold is set here. When the %K line is higher than 20, it is oversold.
Secondly, this strategy uses the Bollinger Bands indicator to identify price changes. Bollinger Bands calculate the upper and lower bands based on the standard deviation of prices. When the price is close to the lower track, it is oversold. The strategy here sets parameters of 2 times the standard deviation to make the Bollinger Bands range wider, thereby filtering out more false signals.
After obtaining oversold signals from the above two indicators, this strategy adds multiple filtering conditions to further identify buying opportunities:
1. The price has just broken through the Bollinger Bands and moved upward.
2. The current closing price is higher than the closing price before N K lines, indicating buying strength.
3. The current closing price is lower than the closing price in the long-term or medium-term lookback period, which is favorable for a correction.
If the buying opportunity is identified after comprehensive judgment, a buying signal will be issued.
## Advantage Analysis
This dual indicator filtering strategy has several advantages:
1. Use dual indicators to make buying signals more reliable and avoid false signals.
2. Multiple filtering conditions to avoid frequent buying in volatile market conditions.
3. Combined with the stochastic index indicator to determine oversold status, the Bollinger Bands indicator is used to determine price abnormalities.
4. Increase price strength judgment to ensure sufficient buying power.
5. Add callback judgment to further ensure the reliability of buying points.
In general, this strategy comprehensively uses a variety of technical indicators and filtering methods to make the identification of buying opportunities more accurate and reliable, thereby achieving better trading performance.
## Risk Analysis
Although this dual indicator filtering strategy has many advantages, there are also some risks that need to be guarded against:
1. Improper parameter settings may cause buy signals to be too frequent or conservative, requiring careful testing and optimization.
2. Multiple filtering conditions may miss some buying opportunities and make it impossible to track fast market trends.
3. When the indicator diverges, an error signal will be generated, so you need to pay attention to the consistency of the indicator.
4. Unable to judge the trend, in a bear market there may be false signals resulting in losses.
In response to the above risks, this strategy can be optimized as follows:
1. Adjust indicator parameters to balance the sensitivity of filtering conditions.  
2. With the help of trend judgment indicators, avoid generating false signals in a bear market.
3. Add stop loss means.
## Optimization direction
This dual indicator filtering strategy can be further optimized from the following dimensions:
1. Test more combinations of technical indicators to find better means of judging buying opportunities. For example VRSI, DMI, etc.
2. Add machine learning algorithm to automatically optimize parameters.
3. Add adaptive stop loss mechanism. When the profit reaches a certain level, gradually increase the stop loss line.
4. Combine with trading volume indicators to ensure there is sufficient buying power.
5. Optimize fund management strategies. Set dynamic transaction quantity to reduce single loss.
By introducing more advanced technologies and methods, this dual indicator filtering strategy can achieve more precise purchase timing selection and stronger risk control capabilities. In order to obtain more stable and reliable income in the real offer.
## Summarize
To sum up, the dual indicator buy filter buy signal strategy uses a variety of technical indicators such as Stochastic RSI and Bollinger Bands, and combines multiple filter conditions such as price strength and callback judgment to identify high-probability and reliable buying opportunities. With further improvements in parameter optimization, stop loss setting, etc., this strategy can become one of the quantitative trading strategies with stable returns.
Its core advantage lies in the effective combination of indicators and filtering conditions, making the judgment of buying timing more accurate. Risks and optimization directions are also controllable and solvable. Overall, this is an efficient quantitative strategy that can be implemented.
||
## Overview

The Dual Indicator Filtered Buy Signal strategy utilizes a combination of Stochastic RSI and Bollinger Bands to identify potential buy opportunities. It employs multiple filter conditions to distinguish the most favorable buy points. This allows it to identify high-probability buy entry timing in fluctuating market environments.

## Strategy Logic

The strategy leverages two sets of indicators to spot buy chances. 

Firstly, it uses Stochastic RSI to determine if the market is oversold. The indicator combines Stochastic and its moving average lines, treating a %K line crossover above its %D line from below as an oversold signal. A threshold is set here so that %K values above 20 are considered oversold.

Secondly, the strategy employs Bollinger Bands to identify price changes. Bollinger Bands are bands calculated from the standard deviation of prices. When prices approach the lower band, it signals an oversold condition. The strategy here sets the parameter to 2 times standard deviation for wider Bollinger Bands, filtering out more false signals.


With oversold signals obtained from both indicators, the strategy adds multiple filter conditions to further identify buy entry timing:

1. Price just bounced off the Bollinger lower band upwards  
2. Current close is higher than the close N bars ago, showing buying power
3. Current close is lower than longer-term or mid-term lookback period closes for pullback

Buy signals are triggered when the comprehensive criteria are met.

## Strength Analysis 

The dual indicator filtered strategy has several key strengths:

1. The dual indicator design makes buy signals more reliable by avoiding false signals.
2. Multiple filter conditions prevent excessive buys in range-bound markets. 
3. Combination of Stochastic RSI gauges oversold levels and Bollinger Bands detects price anomalies.
4. Buying power filter ensures adequate momentum behind buys. 
5. Pullback filters further validate reliability of buy zones.

In summary, the strategy combines various technical indicators and filtering techniques to pinpoint buy entry timing more precisely, leading to better trading performance.

## Risk Analysis

Despite its strengths, there are also risks to manage with the strategy:

1. Improper parameter tuning may result in too frequent or conservative signals. Careful optimization is required.  
2. Strict filtering logics may miss some opportunities in fast-moving markets.  
3. Diverging indicators may generate false signals. Cross-examination is necessary.
4. Lack of trend determination exposes the strategy during bear markets.

Suggested enhancements to mitigate the risks are:

1. Adjust indicator parameters to balance filter sensitivity.
2. Introduce trend-determining filters to avoid bull traps.  
3. Incorporate stop loss mechanisms.

## Enhancement Opportunities

The strategy can be further improved in aspects below:

1. Test more indicator combinations for better buy timing models, e.g. VRSI, DMI etc.
2. Introduce machine learning algorithms to auto-optimize parameters.  
3. Build adaptive stop loss mechanisms to trail stops at profit milestones.
4. Incorporate volume indicators to ensure sufficient momentum.   
5. Optimize money management models like dynamic position sizing to limit losses.

With more advanced techniques introduced, the strategy can achieve more precise signal generating capabilities and stronger risk control to deliver more reliable profits in live trading.

## Conclusion

In summary, the Dual Indicator Filtered Buy Signal Strategy leverages Stochastic RSI, Bollinger Bands and multiple filter conditions like price strength and pullback validation to identify high-probability buy entry points. With proper parameter tuning, risk controls etc., it has the potential to become a stable automated trading strategy. 

Its core strength lies in the effective combination of indicators and filters for accurate timing. The risks and enhancement paths are also identifiable and manageable. Overall, this is an implementable and effective quantitative strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1||Long_message|
|v_input_2||Close_message|
|v_input_3|14|lookback length of Stochastic|
|v_input_4|80|Stochastic overbought condition|
|v_input_5|20|Stochastic oversold condition|
|v_input_6|3|smoothing of Stochastic %K |
|v_input_7|3|moving average of Stochastic %K|
|v_input_8|14|lookback length of RSI|
|v_input_9|70|RSI overbought condition|
|v_input_10|30|RSI oversold condition|
|v_input_11|22|LookBack Period Standard Deviation High|
|v_input_12|20|Bolinger Band Length|
|v_input_13|2|Bollinger Band Standard Devaition Up|
|v_input_14|50|Look Back Period Percentile High|
|v_input_15|0.85|Highest Percentile - 0.90=90%, 0.95=95%, 0.99=99%|
|v_input_16|false|-------Text Plots Below Use Original Criteria-------|
|v_input_17|false|Show Text Plot if WVF WAS True and IS Now False|
|v_input_18|false|Show Text Plot if WVF IS True|
|v_input_19|false|-------Text Plots Below Use FILTERED Criteria-------|
|v_input_20|true|Show Text Plot For Filtered Entry|
|v_input_21|true|Show Text Plot For AGGRESSIVE Filtered Entry|
|v_input_22|40|Long-Term Look Back Current Bar Has To Close Below This Value OR Medium Term--Default=40|
|v_input_23|14|Medium-Term Look Back Current Bar Has To Close Below This Value OR Long Term--Default=14|
|v_input_24|3|Entry Price Action Strength--Close > X Bars Back---Default=3|
|v_input_25|false|-------------------------Turn On/Off ALERTS Below---------------------|
|v_input_26|false|----To Activate Alerts You HAVE To Check The Boxes Below For Any Alert Criteria You Want----|
|v_input_27|false|Show Alert WVF = True?|
|v_input_28|false|Show Alert WVF Was True Now False?|
|v_input_29|false|Show Alert WVF Filtered?|
|v_input_30|false|Show Alert WVF AGGRESSIVE Filter?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-30 00:00:00
end: 2023-12-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("SORAN Buy and Close Buy", pyramiding=1, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=10, overlay=false)

////Buy and Close-Buy messages
Long_message = input("")
Close_message = input("")

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
ltLB = input(40, minval=20, maxval=99, title="Long-Term Look Back Current Bar Has To Close Below This Value OR Medium Term--Default=40")
mtLB = input(14, minval=1, maxval=40, title="Medium-Term Look Back Current Bar Has To Close Below This Value OR Long Term--Default=14")
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
col = wvf >= upperBand or wvf >= rangeHigh ? #00E676 : #787B86

isOverBought = (crossover(k,d) and k > StochOverBought) ? 1 : 0
isOverBoughtv2 = k > StochOverBought ? 1 : 0
filteredAlert = alert3 ? 1 : 0
aggressiveAlert = alert4 ? 1 : 0

plot(isOverBought, "Overbought / Crossover", style=plot.style_line, color=#FF5252) 
plot(filteredAlert, "Filtered Alert", style=plot.style_line, color=#E040FB) 
plot(aggressiveAlert, "Aggressive Alert", style=plot.style_line, color=#FF9800)

if (filteredAlert or aggressiveAlert)
    strategy.entry("Buy", strategy.long, alert_message = Long_message)

if (filteredAlert or aggressiveAlert)
    alert("Buy Signal", alert.freq_once_per_bar)


if (isOverBought)
    strategy.close("Buy", alert_message = Close_message)

```

> Detail

https://www.fmz.com/strategy/434524

> Last Modified

2023-12-07 10:43:01
