
> Name

RSI moving average crossover strategy RSI-EMA-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1487e94972b79236da2.png)

[trans]

## Overview
This strategy uses the principle of moving average crossover, combined with the RSI indicator, to determine the trend direction and perform buying and selling operations.
## Strategy Principle
This strategy uses three EMA moving averages with different periods, namely fast line, middle line and slow line. When the fast line crosses the middle line, it is judged as a buy signal; when the fast line crosses below the middle line, it is judged as a sell signal.
At the same time, this strategy also uses the RSI indicator to determine overbought and oversold conditions. RSI shows the relative strength of an asset through the ratio of the average increase and the average decrease within a period. When the RSI exceeds the set overbought line, it is considered to be in an overbought state; when the RSI is below the set oversold line, it is considered to be in an oversold state.
The buying conditions for this strategy are:
1. The price crosses the fast line, middle line, and slow line
2. RSI crosses the oversold line set above
The selling conditions are:
1. The fast line crosses the middle line
2. RSI crosses below the midline of the setting
Use the moving average to determine the direction of the general trend, and combine it with RSI to find short-term overbought and oversold opportunities. This strategy comprehensively uses trend trading and reversal trading strategies.
## Advantage Analysis
This strategy combines moving average crossover and RSI indicators to simultaneously determine trends and overbought and oversold conditions, which can filter out noise trading caused by false breakthroughs. Using three moving averages, you can judge the trend status more clearly.
The setting of the RSI indicator also allows this strategy to capture better entry and exit opportunities in overbought and oversold areas.
This strategy also takes into account transaction costs and can avoid being trapped by entering the market only when the price breaks through the three moving averages.
## Risk Analysis
This strategy still has the risk of overfitting in backtesting. Changes in the market environment during real trading will cause the parameters to no longer adapt to the new market conditions.
In volatile market conditions, this strategy can easily generate false signals, which may result in losses.
The setting of RSI parameters needs to be adjusted according to different markets. If the parameters are set improperly, it is easy to miss opportunities or generate false signals.
## Optimization direction
1. You can consider verifying the signal again on a longer-term chart to avoid being disturbed by short-term market noise.
2. You can experiment before entering the market by waiting for a breakthrough or retracement of the moving average before entering the market to further verify the signal.
3. It can be combined with other indicators, such as MACD, Bollinger Bands, etc., to combine the signals of multiple indicators to improve the Entry hit rate.
4. Machine learning algorithms can be used to assist in optimizing parameters to make the strategy more adaptable.
5. You can consider adding a stop loss strategy to stop losses in time when the trend is uncertain.
## Summarize
This strategy integrates moving average crossover and RSI indicators to identify short-term trend reversal opportunities while judging trends. It effectively utilizes the advantages of trend trading and reversal trading, and can capture short-term opportunities while holding in a long-term bullish direction. This strategy has certain room for optimization. By further verifying signals, optimizing parameters, adding stop losses, etc., the strategy can be made more stable and reliable. However, we need to pay attention to the problem of over-fitting in backtesting. The real market environment will test the flexibility of the strategy. Generally speaking, this strategy has certain reference value as a learning strategy, but the actual effect needs further verification.
|| 

## Overview

This strategy utilizes the principle of exponential moving average (EMA) crossovers, combined with the RSI indicator, to determine trend direction for entries and exits. 

## Strategy Logic

The strategy uses 3 EMA lines with different periods - fast, medium and slow lines. A buy signal is generated when the fast EMA crosses above the medium EMA, and a sell signal is generated when the fast EMA crosses below the medium EMA.

The strategy also incorporates the RSI indicator to gauge overbought and oversold conditions. The RSI calculates a ratio of average up days to average down days over a period to show the relative strength of an asset. Values above the overbought threshold signal overbought conditions, while values below the oversold threshold signal oversold conditions.

The buy conditions for the strategy are:

1. Price crossing above fast, medium and slow EMA lines 
2. RSI crossing above the oversold threshold

The sell conditions are:

1. Fast EMA crossing below medium EMA
2. RSI crossing below the medium line

Using EMA crossovers to determine trend direction combined with RSI to identify short-term reversal opportunities, this strategy makes use of both trend following and mean reversion concepts.

## Advantage Analysis 

This strategy combines EMA crossovers and RSI to gauge both trend and overbought/oversold levels, filtering out false breakouts and noisy trades. Using 3 EMA lines gives a clear trend bias. 

The RSI settings allow the strategy to time entries and exits at advantageous overbought/oversold areas.

The requirement for price to break all 3 EMA lines before entering trades helps avoid being whipsawed.

## Risk Analysis

Like all backtested strategies, this strategy faces the risk of backtest overfitting. Changing market conditions in live trading may render the optimized parameters unsuitable.

In ranging markets, the strategy may generate false signals and suffer losses.

Poor RSI parameter tuning may lead to missed opportunities or false signals.

## Enhancement Opportunities

1. Consider adding validation on higher timeframes to avoid noise. 

2. Wait for retest of EMA lines before entering trades to validate signal.

3. Incorporate other indicators like MACD, Bollinger Bands for combined signal confirmation.

4. Use machine learning to optimize parameters for robustness. 

5. Consider adding stop loss to exit uncertain trends quickly.

## Conclusion

This strategy combines EMA crossovers and RSI to identify trend while taking advantage of short-term reversals. It utilizes both trend following and mean reversion concepts efficiently. There is scope for optimization via signal validation, parameter tuning, stop losses etc. But backtest overfitting needs to be considered, and live performance should be evaluated. Overall, this serves as a useful reference for learning, but requires further validation in live markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|26|Rsi Lenght|
|v_input_int_2|30|Rsi OVS line|
|v_input_int_3|70|Rsi OVB line|
|v_input_int_4|42|Rsi Medium line|
|v_input_int_5|17|EMA Fast|
|v_input_int_6|35|EMA Medium|
|v_input_int_7|142|EMA Slow|
|v_input_int_8|2011|Start Year|
|v_input_int_9|true|Start Month|
|v_input_int_10|true|Start Day|
|v_input_int_11|2025|End Year|
|v_input_int_12|true|End Month|
|v_input_int_13|true|End Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-24 00:00:00
end: 2023-10-24 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © chadsadachai

//@version=5
strategy("EMA Cross V1", overlay= true)

//rsi
length = input.int(title = "Rsi Lenght" , defval=26 , minval=1, maxval=50)
overS = input.int(title = "Rsi OVS line" , defval=30 , minval=1, maxval=40)
overB = input.int(title = "Rsi OVB line" , defval=70 , minval=1, maxval=100)
mLine = input.int(title = "Rsi Medium line" , defval=42 , minval=1, maxval=60)
price = close
vrsi = ta.rsi(price, length)
co = vrsi >= mLine and vrsi < overB 
cu = ta.crossunder(vrsi, overB)
//ema
F = input.int(title = "EMA Fast" , defval=17 , minval=1, maxval=50)
M = input.int(title = "EMA Medium" , defval=35, minval=1, maxval=100)
S = input.int(title = "EMA Slow" , defval=142, minval=1, maxval=200)
emaF = ta.ema(price , F)
emaM = ta.ema(price , M)
emaS = ta.ema(price , S)

//plot
plot(emaF , color = color.green , linewidth=1)
plot(emaM , color = color.yellow , linewidth=1)
plot(emaS , color = color.red , linewidth=1)

//Time Stamp
start = timestamp(input.int(title = "Start Year" , defval=2011 , minval=2011, maxval=2025), input.int(title = "Start Month" , defval=1 , minval=1, maxval=12), input.int(title = "Start Day" , defval=1 , minval=1, maxval=31), 0, 0)
end = timestamp(input.int(title = "End Year" , defval=2025 , minval=2011, maxval=2025), input.int(title = "End Month" , defval=1 , minval=1, maxval=12), input.int(title = "End Day" , defval=1 , minval=1, maxval=31), 0, 0)
// years = input.int(title = "Year" , defval=2018 , minval=2011, maxval=2025)
// months = input.int(title = "Month" , defval=1 , minval=1, maxval=12)
// days = input.int(title = "Day" , defval=1 , minval=1, maxval=31)

//longCondition Default
// longCondition1 = EMA_Fast >= EMA_Slow and EMA_Fast >= EMA_Medium//ta.crossover(EMA_Fast, EMA_Slow)  EMA_Fast > EMA_Slow and EMA_Medium > EMA_Slow
// longCondition3 = price >= EMA_Medium and price > EMA_Slow
// longCondition2 = vrsi >= overSold and vrsi <= overBought 

//longCondition & shortCondition ETHUSD
// 1.price > emaF > emaM > emaS
// 2.rsi overcross overS
longC1 = price > emaF and price > emaM and price > emaS 
// longC1 = ta.crossover(emaF, emaM)
longC2 = if longC1
    co
// shortC1 = EMA_Fast < EMA_Medium //and EMA_Fast < EMA_Slow and EMA_Medium < EMA_Slow //and cu
// shortC2 = overBought > vrsi //and vrsi < overBought //overSold < vrsi and vrsi < mediumLine

// exitLong Condition
// 1.price < emaF < emaM < emaS
// 2.rsi overcross mediumLine
exitLong1 = ta.crossunder(emaF, emaM) //or emaF < emaM//and price < emaM and price < emaF
exitLong2 = ta.crossunder(vrsi,mLine)
//exitLong3 = price < emaM
//strategy.entry
if time >=start and time <=end
    strategy.entry("Buy", strategy.long , when = longC1 and longC2)

// if(exitLong1 or exitLong2)
strategy.close("Buy" , when = exitLong1 or exitLong2)
    
// exitShort1 = EMA_Fast > EMA_Medium
// //exitShort2 = ta.crossover(vrsi , mediumLine) 
// exitShort2 = ta.crossunder (vrsi,mediumLine)
// strategy.close("Short" , when = exitShort1 or exitShort2)
// //shortCondition = cu


// //if (shortCondition1 and shortCondition2)
//     //strategy.entry("My Short Entry Id", strategy.short)

```

> Detail

https://www.fmz.com/strategy/430126

> Last Modified

2023-10-25 11:46:49
