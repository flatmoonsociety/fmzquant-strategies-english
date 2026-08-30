
> Name

Multi-Timeframe-RSI-and-Stochastics-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/145698e35e7d08fe7b4.png)
[trans]
## Overview
The multi-time frame RSI and stochastic indicator strategy is a strategy that uses a combination of RSI and stochastic indicators to determine whether the market is overbought or oversold in multiple time frames. This strategy combines the RSI and stochastic indicators of 4 time frames at the same time, and uses its average value to determine the overall market trend and overbought and oversold conditions to take advantage of each time frame indicator.
## Strategy Principle
### 1. RSI indicator
The RSI indicator is a powerful overbought and oversold indicator that is calculated based on the rise and fall of a stock over a certain period of time. The RSI value fluctuates between 0 and 100. Generally speaking, an RSI greater than 70 indicates overbought, and an RSI less than 30 indicates oversold.
This strategy uses the RSI indicator with a length of 14 and obtains RSI values ​​for 4 time frames: 1 month, 1 day, 4 hours and 1 hour.
### 2. Stochastic indicator %K
The stochastic indicator %K is an indicator that shows whether the market is overbought or oversold. The value fluctuates between 0 and 100. Generally speaking, a stochastic indicator greater than 80 indicates overbought, and a stochastic indicator less than 20 indicates oversold.
In this strategy, the length of the stochastic indicator %K is 14, the smoothing is 3, and the values ​​of the above four time frames are also obtained.
### 3. Average combination
The key to the strategy is to calculate the average of the above two indicators in the four time frames to take advantage of each time frame and judge the overall market trend. The specific calculation formula is as follows:
RSI average = (RSI monthly + RSI daily + RSI4 hours + RSI1 hours) / 4
Stochastic indicator average = (Stochastic indicator monthly line + Stochastic indicator daily line + Stochastic indicator 4 hours + Stochastic indicator 1 hour) / 4

### 4. Trading signals
When the average RSI is less than 30 and the average stochastic is less than 20, go long; when the average RSI is greater than 70 and the average stochastic is greater than 80, go short.
After going long, close the position when the average stochastic indicator is greater than 70 and the average RSI is greater than 50; after going short, close the position when the average stochastic indicator is less than 30 and the average RSI is less than 50.
## Advantage Analysis
The biggest advantage of this strategy is to combine two indicators and multiple time frames at the same time, which can greatly improve the reliability of trading signals and avoid false signals to the greatest extent. The specific advantages are as follows:
1. The RSI indicator and the stochastic indicator verify each other. Relying solely on a single indicator can easily produce false signals, but this strategy can improve the accuracy of the signal by combining two indicators.
2. Multi-time frame analysis can improve the accuracy of judgment. For example, the monthly and daily lines show overbought, but the 4-hour and 1-hour lines are not completely overbought, indicating that the trend may continue. The signal is more reliable if all time frames are consistent.
3. Determine structural turning points more clearly. Seeing key Support/Resistance breakthroughs simultaneously on multiple time frames can indicate a turning point in the current trend.
4. Automatically calculate indicator averages to simplify operations. No manual calculation is required, the code automatically completes data extraction, indicator calculation and averaging, reducing workload.
## Risk Analysis
The main risk of this strategy is that, like all technical analysis strategies, the probability of being trapped and generating false signals cannot be completely avoided. The main risks are:
1. Short-term trend reversal leads to trapping. For example, during a long position, the price breaks through the support level in the short term and then rebounds again. At this time, the loss needs to be stopped immediately according to the closing logic of the strategy, but it may cause short-term losses.
2. The failure of key support/resistance levels leads to the failure of trailing stop loss. If a key support or resistance level falls, the original stop loss price may be directly breached, resulting in greater losses.
3. Improper time frame setting leads to incorrect judgment. If the time frame is set too long or too short, it may lead to deviations in indicator interpretation.
4. Indicator divergence leads to Dunkirk effect. That is, if indicators on higher time frames indicate overbought and indicators on lower time frames indicate oversold, the average indicator cannot reflect the true situation.
Solutions to corresponding risks include: optimizing stop loss strategies, tracking dynamic support/resistance levels, adjusting time frame parameters and adding screening mechanisms, etc.
## Optimization direction
Taking into account the above-mentioned risks, this strategy can also be optimized from the following directions:
1. Optimize the stop loss mechanism and implement trailing stop loss and batch stop loss. This can control the risk of single loss while ensuring profits.
2. Add higher time frames such as quarterly lines. This can take advantage of larger-level trends to filter out misleading signals. When indicators diverge, priority is given to higher time frames.
3. Increase long and short verification of trading volume. Combine the changes in trading volume to determine the bottom divergence and top divergence to avoid being misled by zombie trends.
4. Optimize entry timing. You can wait for a breakthrough to enter near important historical support/resistance, or wait for the best callback buying point.
5. Add adaptive stop loss. Dynamic stops can be calculated and adjusted based on recent volatility and ATR.
## Summarize
The multi-time frame RSI and stochastic indicator strategy is a clear and reliable trading strategy that uses a combination of RSI indicators and stochastic indicators to determine the overbought and oversold ranges of the market on multiple time frames. Its biggest advantage is that the combination of indicators and time frames verifies each other, which can greatly avoid the risk of being trapped and false signals. Of course, this strategy also has common risks similar to technical analysis strategies, and it needs to be continuously improved and optimized from aspects such as optimizing stop loss and time frame selection to make it a stable and profitable algorithmic trading strategy.
||

## Overview 

The Multi Timeframe RSI and Stochastics Strategy is a strategy that combines RSI and Stochastics indicators across multiple timeframes to determine overbought and oversold conditions in the market. It utilizes the average values of RSI and Stochastics from 4 different timeframes to gauge overall market momentum and overextension. This allows it to harness the strengths of indicators across different timeframes.  

## Strategy Logic

### 1. RSI Indicator

The RSI indicator is a powerful oscillator that measures overbought and oversold levels based on the magnitude of recent price movements. RSI values fluctuate between 0 to 100, where values over 70 are considered overbought and under 30 oversold.

This strategy uses a 14-period RSI and obtains RSI values from the monthly, daily, 4-hour and 1-hour timeframes.

### 2. Stochastics %K 

Stochastics %K is an indicator that shows overbought/oversold levels in the market on a scale of 0 to 100. Generally, values above 80 indicate an overbought market while values below 20 signal an oversold market.

The strategy uses a 14,3 Stochastics configuration and likewise obtains %K values from the aforementioned timeframes.

### 3. Average Value Combination

The crux of the strategy lies in taking an average of the two indicators across the multiple timeframes. This allows it to tap on the strengths of each timeframe when gauging overall market conditions. The exact formulas are:

RSI Average = (Monthly RSI + Daily RSI + 4H RSI + 1H RSI) / 4

Stochastics Average = (Monthly Stochastics + Daily Stochastics + 4H Stochastics + 1H Stochastics) / 4

### 4. Trade Signals 

The strategy triggers a long when the RSI average falls below 30 and Stochastics average goes below 20. It triggers a short when the RSI average rises above 70 and Stochastics average breaches 80. 

The long position is closed when Stochastics average rises above 70 and RSI average climbs over 50. The short position is closed when Stochastics average dips below 30 and RSI average drops under 50.

## Advantage Analysis

The key advantage of this strategy lies in the combination of two indicators across multiple timeframes. This greatly enhances the reliability of trade signals and minimizes false signals. Specific advantages include:

1. RSI and Stochastics verify each other as signals. Relying solely on one indicator tends to generate false signals more frequently. The dual indicator approach promotes accuracy.

2. Multiple timeframes lead to more robust analysis. For instance, the monthly and daily timeframes show an overbought market but the smaller timeframes have yet to reach overextension levels. This suggests an uptrend is likely to continue. Signals are more reliable when all timeframes agree.  

3. Clearer identification of structural turning points when multiple timeframes concurrently show a break of key S/R levels, signaling a trend reversal.

4. Auto-computation of averages simplifies the workflow. No manual calculation needed as the code handles data retrieval, indicator computation and averaging automatically.

## Risk Analysis

As with all technical analysis strategies, the core risk lies in whipsaws and false signals. Key risks include:

1. Trend reversals leading to being stopped out. For instance, prices make a short term breach below support before rebounding while long. Such cases may incur short term losses due to the exit logic.

2. Invalidation of key S/R leading to failed trailing stops. A break of major S/R levels can directly trigger stops designed below them, resulting in above average losses.

3. Incorrect judgments from suboptimal timeframe configurations. Overssmoothed or undersmoothed timeframes may provide misleading oscillator values. 

4. Divergence across timeframes causing a Dunkirk effect. Where higher timeframes show an overbought market but lower timeframes signal oversold conditions, rendering averages ineffective.

Solutions involve optimizing stop loss strategies, tracking dynamic S/R levels, adjusting timeframe parameters and adding additional filters.

## Enhancement Opportunities

In view of the discussed risks, enhancement opportunities include:

1. Optimizing the stop loss mechanism to incorporate trailing stops and partial exits. This locks in profits while controlling single trade risks.

2. Adding higher timeframes like the quarterly chart. This allows larger trend guidance to filter false signals. Prioritize readings from higher timeframes when divergence occurs.  

3. Incorporating volume for additional trend validation via bull/bear divergences to avoid zombie trends.

4. Fine-tuning entry signals by awaiting breakouts around key historic S/R or allowing for optimal pullback entries.

5. Implementing adaptive stops based on recent volatility and ATR values for dynamic stop positioning.

## Conclusion  

The Multi Timeframe RSI and Stochastics Strategy is a clear, reliable approach that uses a combination of RSI and Stochastics across multiple timeframes to identify overbought/oversold levels. Its biggest strength lies in the mutual verification of indicators and timeframes to minimize whipsaw and false signal risks. Nonetheless like all technical strategies, it faces inherent risks that need to be addressed via stop loss optimization, timeframe selections etc to refine it into a stable automated trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|80|(?══════════    General    ══════════)Overbought Level|
|v_input_int_2|20|Oversold Level|
|v_input_timeframe_1|W|(?══════════   Timeframes   ══════════)Timeframe 1|
|v_input_timeframe_2|D|Timeframe 2|
|v_input_timeframe_3|240|Timeframe 3|
|v_input_timeframe_4|60|Timeframe 4|
|v_input_int_3|14|(?══════════   RSI settings   ══════════)RSI length|
|v_input_1_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_4|70|RSI Overbought Level|
|v_input_int_5|30|RSI Oversold Level|
|v_input_int_6|14|(?══════════   Stochastic settings   ══════════)%K length|
|v_input_int_7|3|Smooth K|
|v_input_2_close|0|Stochastic Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_8|70|Stochastic Overbought Level|
|v_input_int_9|30|Stochastic Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

////////////////////////////////////////// MTF Stochastic & RSI Strategy ? ©️ bykzis /////////////////////////////////////////
//

// *** Inspired by "Binance CHOP Dashboard" from @Cazimiro and "RSI MTF Table" from @mobester16 *** and LOT OF COPY of Indicator-Jones MTF Scanner
// 
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

//@version=5
strategy('MTF RSI & STOCH Strategy? by kzi', overlay=false,initial_capital=100, currency=currency.USD, commission_value=0.01, commission_type=strategy.commission.percent)


// Pair list
var string GRP1       = '══════════    General    ══════════'
overbought = input.int(80, 'Overbought Level', minval=1, group=GRP1)
oversold = input.int(20, 'Oversold Level', minval=1, group=GRP1)


/// Timeframes
var string GRP2       = '══════════   Timeframes   ══════════'
timeframe1 = input.timeframe(title="Timeframe 1", defval="W", group=GRP2)
timeframe2 = input.timeframe(title="Timeframe 2", defval="D", group=GRP2)
timeframe3 = input.timeframe(title="Timeframe 3", defval="240", group=GRP2)
timeframe4 = input.timeframe(title="Timeframe 4", defval="60", group=GRP2)

// RSI settings
var string GRP3       = '══════════   RSI settings   ══════════'
rsiLength = input.int(14, minval=1, title='RSI length', group=GRP3)
rsiSource = input(close, 'RSI Source', group=GRP3)
rsioverbought = input.int(70, 'RSI Overbought Level', minval=1, group=GRP3)
rsioversold = input.int(30, 'RSI Oversold Level', minval=1, group=GRP3)


/// Get RSI values of each timeframe /////////////////////////////////////////////////////
rsi = ta.rsi(rsiSource, rsiLength)
callRSI(id,timeframe) =>
    rsiValue = request.security(id, str.tostring(timeframe), rsi, gaps=barmerge.gaps_off)
    rsiValue

RSI_TF1 = callRSI(syminfo.tickerid, timeframe1)
RSI_TF2 = callRSI(syminfo.tickerid, timeframe2)
RSI_TF3 = callRSI(syminfo.tickerid, timeframe3)
RSI_TF4 = callRSI(syminfo.tickerid, timeframe4)




/////// Calculate Averages /////////////////////////////////////////////////////////////////
calcAVG(valueTF1, valueTF2, valueTF3, valueTF4) =>
    math.round((valueTF1 + valueTF2 + valueTF3 + valueTF4) / 4, 2)

AVG=calcAVG(RSI_TF1, RSI_TF2, RSI_TF3, RSI_TF4)



// Stochastic settings
var string GRP4       = '══════════   Stochastic settings   ══════════'
periodK = input.int(14, '%K length', minval=1, group=GRP4)
smoothK = input.int(3, 'Smooth K', minval=1, group=GRP4)
stochSource = input(close, 'Stochastic Source', group=GRP4)
stochoverbought = input.int(70, 'Stochastic Overbought Level', minval=1, group=GRP4)
stochoversold = input.int(30, 'Stochastic Oversold Level', minval=1, group=GRP4)


/// Get Stochastic values of each timeframe ////////////////////////////////////////////////
stoch = ta.sma(ta.stoch(stochSource, high, low, periodK), smoothK)
getStochastic(id,timeframe) =>
    stochValue = request.security(id, str.tostring(timeframe), stoch, gaps=barmerge.gaps_off)
    stochValue

Stoch_TF1 = getStochastic(syminfo.tickerid, timeframe1)
Stoch_TF2 = getStochastic(syminfo.tickerid, timeframe2)
Stoch_TF3 = getStochastic(syminfo.tickerid, timeframe3)
Stoch_TF4 = getStochastic(syminfo.tickerid, timeframe4)


AVG_STOCH=calcAVG(Stoch_TF1, Stoch_TF2, Stoch_TF3, Stoch_TF4)


plot(AVG, color = color.blue, title='RSI')
plot(AVG_STOCH, color = color.yellow,title='STOCH')
hline(rsioverbought,color=color.red)
hline(rsioversold, color=color.lime)
hline(50, color=color.white)

//============ signal Generator ==================================//

if AVG <= rsioversold and AVG_STOCH <=stochoversold 
    strategy.entry('Buy_Long', strategy.long)

    
strategy.close("Buy_Long",when=(AVG_STOCH >=70 and AVG >=50 and close >=strategy.position_avg_price),comment="Long_OK")

if AVG >=rsioverbought and AVG_STOCH >=stochoverbought
    strategy.entry('Buy_Short', strategy.short)


strategy.close("Buy_Short",when=(AVG_STOCH <=30 and AVG <=50 and close <=strategy.position_avg_price),comment="Short_OK")


///////////////////////////////////////////////////////////////////////////////////////////




```

> Detail

https://www.fmz.com/strategy/442396

> Last Modified

2024-02-21 15:56:37
