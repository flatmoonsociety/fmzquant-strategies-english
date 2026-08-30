
> Name

RSI indicator combined with CCI indicator quantitative trading strategy RSI-amp-CCI-Combination-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d16ca004eae218543d.png)
 [trans]

## Overview
This strategy is called a quantitative trading strategy that combines the RSI indicator with the CCI indicator. This strategy mainly uses the combination of RSI indicator and CCI indicator to judge the overbought and oversold phenomenon of the market to capture reversal opportunities. Specifically, the strategy sets the opening rules for long and short positions by calculating the long and short lines of RSI and combining the long and short signals of the CCI indicator. When the rules for opening a position are met, the corresponding long and short operations are performed.
## Strategy Principle
The core logic of this strategy is to use the statistical characteristics of the RSI indicator and the CCI indicator at the same time to determine whether the market is currently overbought or oversold.
First, the RSI part. The RSI indicator can reflect overbought and oversold conditions in the market. When the RSI is greater than 70, it is an overbought zone, and when it is less than 30, it is an oversold zone. This strategy sets two RSI indicators, long-term and short-term. The long-term parameter is the default period of 14, and the short-term parameter is 12 periods. The long-term can determine the core trend, and the short-term can track more sensitive turning points. When the long-term and short-term RSI indicators are in the same direction (such as double overbought or double oversold), it means that the market is in a clear disequilibrium state, and this is the best opportunity for reversal.
Secondly, the CCI part. The CCI indicator can also be used to determine overbought and oversold, with a 14-period parameter. A CCI above 100 is overbought, and a CCI below -100 is oversold. This strategy uses this characteristic of the CCI indicator to set the opening rules: when the long and short signals given by the CCI indicator and the RSI indicator are consistent, the opening direction determined by the RSI indicator is executed.
Specifically, the opening rules of the strategy are:
1. Open a long position: When the RSI indicator shows the oversold zone (both long-term and short-term RSI are less than 30 during this period), and the CCI indicator is less than -100, go long;
2. Open a short position: When the RSI indicator shows the overbought zone (both long-term and short-term RSI are greater than 70 during this cycle), and the CCI indicator is above 100, go short.
Through the joint judgment of RSI indicator and CCI indicator, the true overbought and oversold range can be effectively confirmed, thereby improving the stability and profit probability of the strategy.
## Advantage Analysis
The biggest advantage of this strategy is that it uses the statistical laws of the two indicators RSI and CCI at the same time, making it more accurate to identify overbought and oversold phenomena, thus providing an ideal entry point for capturing reversals. The specific advantages are as follows:
1. The combination of RSI's long and short lines can simultaneously determine trends and sensitive reversal points, and flexibly capture opportunities.
2. CCI indicator assists judgment to avoid being misled by false market reversals.
3. Through the combined judgment of RSI and CCI, false signals can be effectively filtered, making the entry time selection more accurate.
4. Using the overbought and oversold range for reversal trading is a trading strategy idea with a high probability.
5. The strategy method is simple, easy to understand and implement, and is suitable for quantitative beginners to learn.
## Risk Analysis
The main risk of this strategy is that the overbought and oversold signals determined by RSI and CCI may not fully reflect the true reversal point. Specific risks include:
1. The signal sent by the indicator may be a false reversal. If the price shows a shock adjustment rather than a trend reversal.
2. Even if the judgment is correct, there will be a time lag. Parameter changes during the calculation period cannot fully reflect the latest price changes simultaneously.
3. During the reversal process, the stop loss point may be breached, causing losses to expand.
4. The strategy does not consider the impact of large-level trends, and needs to be combined with trend analysis in specific implementation. 

Risk-based solutions include:
1. It is better to confirm the reversal signal and achieve a large-volume breakthrough. If the price has a large volume increase when the indicator reversal signal appears, the reliability of the judgment can be increased. 
2. Appropriately adjust the parameters of RSI and CCI to reduce the probability of hysteresis.
3. Have a good idea of ​​stop loss and exit, and control single losses.
4. When implementing the strategy, it should be supplemented by trend and morphological analysis to avoid counter-trend operations.
## Optimization direction
This strategy can be further optimized in actual operation. The main optimization ideas include:
1. Test the parameter settings of RSI and CCI to find the optimal parameter combination. For example, test the long and short cycle parameters of RSI and the CCI cycle parameters.
2. Add other indicators to enrich the basis for long and short judgments, such as KD, MACD, etc. 
3. Add a stop loss strategy. Such as setting a trailing stop loss or a zigzag stop loss.
4. Combine with advanced winning strategies and use indicator differences to determine the entry direction with a higher winning rate, etc.  
5. Use machine learning algorithms to automatically optimize parameters and signal weights.
6. Test the strategy in combination with a trending system.
7. Add judgment rules for large-level trends and important price levels. Avoid going against the trend.
Through testing and optimization, you can expect the profitability and stability of this strategy to be further improved.
## Summarize
This strategy is a relatively typical reversal capture strategy. Through the combination of two commonly used indicators, RSI and CCI, we can determine the overbought and oversold ranges and design corresponding opening rules, forming a simple and practical short-term trading strategy. The main advantage of this strategy is that the combination of indicators makes the judgment more accurate, avoids the misleading of false reversals, and thus grasps the best opportunity for reversals. Of course, risks also exist, and it is necessary to optimize indicators, stop loss strategies, and use them in conjunction with trend judgment. Overall, this strategy provides beginners with a simple and reliable quantitative method that is worth learning and practicing.
||

## Overview  

This strategy is named RSI &amp; CCI Combination Quantitative Trading Strategy. It mainly uses the combination of RSI indicator and CCI indicator to judge the overbought/oversold status in the market and capture reversal opportunities. Specifically, the strategy calculates the buy and sell signals of RSI, combined with CCI indicator’s trading signals, to set up the long and short entry rules. When the entry rules are met, corresponding long or short positions will be opened.

## Strategy Logic

The core logic of this strategy is to utilize both the statistical properties of RSI indicator and CCI indicator to determine whether the market is currently in an overbought or oversold state.

Firstly, the RSI part. The RSI indicator can reflect the overbought/oversold phenomena in the market. RSI greater than 70 is typically considered overbought, while less than 30 is oversold. This strategy sets two RSI indicators, a long-term RSI with default 14 periods, and a short-term RSI with 12 periods. The long-term RSI judges overall trend, while the short-term RSI tracks more sensitive turning points. When both RSI lines indicate the same direction (such as double overbought or double oversold), it means the market is in a significant imbalanced state, which provides best reversal opportunities.  

Secondly, the CCI part. The CCI indicator can also be used to identify overbought/oversold levels. CCI higher than 100 is considered overbought, while lower than -100 is oversold. This strategy utilizes this characteristic of CCI to set up entry rules: when CCI signal is consistent with the RSI indicator, the entry signal indicated by RSI will be executed.

Specifically, the entry rules are:  

1. Long entry: when RSI shows oversold area (both long and short term RSI below 30), and CCI is lower than -100, go long.

2. Short entry: when RSI shows overbought area (both long and short term RSI above 70), and CCI is higher than 100, go short.  

By the joint judgment of RSI and CCI, overbought/oversold zones can be effectively confirmed, hence enhancing the stability and profitability of the strategy.

## Advantage Analysis   

The biggest advantage of this strategy lies in the simultaneous use of both RSI and CCI statistical patterns to identify overbought/oversold signals more precisely, which provides ideal turning points to capture reversals. The concrete advantages include:

1. The combination of long and short RSI judges both trend and sensitive inflection points, which helps capture opportunities flexibly.  
2. CCI’s confirmation avoids misleading by false reversals in the market.
3. Through RSI and CCI’s joint signals, false signals can be filtered effectively, making entries more accurate.  
4. Trading reversal in overbought/oversold zones itself is a strategy idea with relatively big winning odds.
5. The strategy is simple to understand and implement, suitable for quant beginners to learn.
   
## Risk Analysis   

The major risk of this strategy is that the overbought/oversold signals indicated by RSI and CCI may not completely reflect the real reversal timing. The concrete risks include:  

1. Indicator may give false reversal signals. E.g. price fluctuation instead of trend reversal.
2. Time lag would exist even if directional correctness. Parameters change within the computing cycle cannot fully synchronize the latest price moves.  
3. Stop loss may be touched during reversals hence enlarge loss.  
4. Major trend influence is not considered which should incorporate with trend analysis in actual trading.

Corresponding solutions include:

1. Reversals with huge volume tend to perform better in confirming signals.  
2. Try optimizing parameters of RSI and CCI to lower the probability of time lags.  
3. Set stop loss properly to control single trade loss.  
4. In actual trading, combine with trend and technical analysis to avoid trading against major trends.
  

## Optimization Directions   

The strategy can be further optimized in actual trading, mainly:  

1. Test and find the optimal parameter combinations for RSI and CCI, like the long/short cycle of RSI and CCI's cycle.
2. Add other indicators to enrich entry signals, like KD, MACD etc.  
3. Add stop loss strategies, like mobile stop loss or shark fin stop loss.
4. Combine advanced win rate models to determine higher probability entry directions judging from indicator divergences.
5. Utilize machine learning algorithms to auto optimize parameters and signal weights.  
6. Test the combination strategies with trend-following systems.  
7. Add rules considering higher time frame trends and key price levels, to avoid trading against major trends.
  
Through tests and optimizations, expectancy of the strategy's profitability and stability could be further improved.


## Conclusion   

The strategy belongs to a typical reversal capturing strategy. By combining two commonly used indicators, RSI and CCI, it judges overbought/oversold levels and sets up corresponding entry rules, forming a simple practical short term trading strategy. The biggest advantage is that the joint use of the two indicators makes signal judgment more accurate, avoiding fake reversals, and grasps the best timing for reversals. Of course risks exist, requiring optimizations in indicators themselves, stop loss strategies, and collaborating with trend analysis. Overall speaking, it provides beginners a simple reliable quant approach, worth learning and practicing.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|length|
|v_input_2|12|fastLength|
|v_input_3|26|slowLength|
|v_input_4|2|signalLength|
|v_input_5_close|0|CCI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-22 00:00:00
end: 2024-01-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Author: RvZ14
//Based on Joseph Nemeth MACD+CCI strategy
//Reference reading: https://sites.google.com/site/forexjosephnemeth/home/macd-cci

strategy(title="MACD+CCI Strategy", shorttitle="macd/cci")
length = input(14, minval=1)
fastLength = input(12, minval=1), slowLength=input(26,minval=1)
signalLength=input(2,minval=1)
src = input(close, title="CCI Source")

//cci
ma = sma(src, length)
cci = (src - ma) / (0.015 * dev(src, length))
plot(cci, title = "cci", color=#5DADE2,linewidth = 1,transp = 0)
band1 = hline(100, color=gray, linewidth = 1)
band0 = hline(-100, color=gray, linewidth = 1)
fill(band1, band0, color= #F9E79F)

//macd
source = close
fastMA = ema(source, fastLength)
slowMA = ema(source, slowLength)
macd = fastMA - slowMA
signal = ema(macd, signalLength)
hist = macd - signal
plot(hist, color=#EC7063, style=histogram)
plot(macd, title = "macd", color=#5DADE2, linewidth = 1,transp = 0)
plot(signal, title = "signal", color=#F5B041,linewidth = 1,transp = 0)

longCond = cci > 100 and macd > 0 or cci > -100 and macd < 0
shortCond = cci < -100 and macd < 0 or cci < 100 and macd > 0
strategy.entry("long",strategy.long,when = longCond == true)
strategy.entry("short",strategy.short,when=shortCond == true)
```

> Detail

https://www.fmz.com/strategy/439605

> Last Modified

2024-01-22 10:33:03
