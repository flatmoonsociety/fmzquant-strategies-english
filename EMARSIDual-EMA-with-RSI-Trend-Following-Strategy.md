
> Name

Dual-EMA-with-RSI-Trend-Following-Strategy Dual-EMA-with-RSI-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy combines the moving average indicator EMA and the overbought and oversold indicator RSI to determine the trend direction and discover potential trend opportunities. When the fast EMA crosses above the slow EMA, it is judged as a bullish opportunity; when the fast EMA crosses below the slow EMA, it is judged as a bearish opportunity. At the same time, the RSI indicator is used to filter out false breakthroughs, and only enter the market when RSI also confirms the trend direction.
## Principle
This strategy is mainly based on the following principles:
1. EMA can effectively smooth price data and show price trends. The combination of fast and slow EMA can form a moving average gap. An enlarging gap indicates the formation of a trend, and a narrowing gap indicates a trend reversal.
2. RSI can effectively identify overbought and oversold conditions. Combined with RSI, false signals of false EMA breakthroughs can be filtered out. Only when EMA and RSI confirm the trend at the same time can you enter the market with a high probability.
Specifically, the fast EMA period is set to 8 and the slow EMA period is set to 24. A bullish signal is generated when the fast EMA crosses above the slow EMA, and a bearish signal is generated when it crosses below. The RSI period is set to 7. When it goes above 70*(1-RSI threshold), it is an overbought zone, and when it goes below 30*(1+RSI threshold), it is an oversold zone. Only when the EMA and RSI are bullish at the same time can you enter the long position; only when the EMA and RSI are bearish at the same time can you enter the short position.
## Advantages
This strategy combines the advantages of EMA and RSI indicators to effectively identify the trend direction and filter out some false signals. The main advantages are:
1. EMA smoothes prices and identifies trend direction; RSI determines overbought and oversold and filters out false breakthroughs.
2. Parameter settings are flexible and can be optimized for different varieties.
3. A variety of indicators are used for confirmation, which can reduce false signals and improve the winning rate.
4. The strategy logic is simple and clear, easy to understand and implement, and suitable for trend tracking.
5. It can be applied to different time periods and can be used for intraday trading or long-term positions.
## Risk
There are also some risks to be aware of with this strategy:
1. When the trend reverses, EMA cannot respond in time and may cause losses.
2. If the RSI long and short judgment parameters are set inappropriately, trading opportunities may be missed.
3. Stock index varieties are prone to violent fluctuations, and strategies may face stop-loss risks.
4. Transaction costs will also affect strategy returns, and reasonable stop loss points need to be considered.
5. The strategy does not take into account fundamental factors and there is a risk of arbitrage.
Corresponding to the risk, single losses can be controlled through reasonable stop loss; RSI parameter settings can be optimized; take-profit and stop-loss levels can be improved by taking into account transaction costs and other methods.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize the parameters of EMA and RSI to better fit the characteristics of different varieties.
2. Add other indicator filters, such as Bollinger Bands, KDJ, etc., to improve signal quality.
3. Increase fundamental factors to avoid the risk of arbitrage.
4. Combine trend lines, support and resistance levels, etc. for entry.
5. optimize take profit and stop loss based on volatility and risk preference.

6. Backtest over longer timeframe and different assets to ensure robustness.

## Summarize
Overall, this strategy is a relatively simple and practical trend following strategy. It combines two indicators, EMA and RSI, to identify the trend direction and can filter out some noise to obtain higher-quality trading signals. Through parameter optimization and the appropriate use of other tools, the effectiveness of the strategy can be further enhanced. However, no strategy can completely avoid losses. Risk assessment needs to be controlled and used as a trend tracking tool.
|| 
 

## Overview

This strategy combines the moving average indicator EMA and the overbought-oversold indicator RSI to determine trend direction and identify potential trend opportunities. When the fast EMA crosses above the slow EMA, it signals a bullish opportunity. When the fast EMA crosses below the slow EMA, it signals a bearish opportunity. RSI is used to filter out false breaks, only taking positions when it confirms the trend direction indicated by EMA.

## Principle

The strategy is based on the following principles:

1. EMA can effectively smooth price data and identify trends. Crossovers between fast and slow EMA reveal trend formation and reversals.

2. RSI effectively identifies overbought and oversold levels. Combining RSI helps filter false signals from EMA crossovers. Only when EMA and RSI both confirm the trend will we enter a position.

Specifically, the fast EMA period is set to 8 and the slow EMA period is set to 24. A crossover of the fast EMA above the slow EMA generates a bullish signal, while a crossover below generates a bearish signal. The RSI period is set to 7. RSI above 70*(1-RSI threshold) indicates overbought levels and RSI below 30*(1+RSI threshold) indicates oversold levels. Only when both EMA and RSI signal bullish will we go long. Only when both signal bearish will we go short.

## Advantages

By combining the strengths of the EMA and RSI indicators, this strategy can effectively identify trend direction and filter out false signals. The main advantages are:

1. EMA smooths price and identifies trend while RSI determines overbought/oversold levels to filter false breaks.

2. Flexible parameter tuning for different assets. 

3. Multiple indicators confirm and reduce false signals, improving win rate.

4. Simple and clear logic, easy to understand and implement for trend following.

5. Applicable to different timeframes for day trading or long-term holding.

## Risks

There are also some risks to note for this strategy:

1. EMA may lag trend reversals and cause losses.

2. Improper RSI parameter setting may lead to missed trades. 

3. Index products can whipsaw, triggering stop loss.

4. Trading costs also impact profits, optimize stop loss carefully.

5. Fundamentals not considered, risks being gamed by arbitrageurs.

We can mitigate risks by reasonable stop loss, optimizing RSI parameters, considering costs when setting profit targets and stop loss, etc.

## Enhancement Opportunities

The strategy can be enhanced in the following aspects:

1. Optimize EMA and RSI parameters to better fit different assets.

2. Add other filters like Bollinger Bands, KDJ to improve signal quality. 

3. Incorporate fundamental factors to avoid arbitrage risks.

4. Combine with trendlines, supports/resistances for entry.

5. Optimize take profit and stop loss based on volatility and risk preference. 

6. Backtest over longer timeframe and different assets to ensure robustness.

## Conclusion

Overall this is a simple and practical trend following strategy. By combining EMA and RSI, it identifies trend direction effectively and filters out noise. With parameter tuning and integrating other tools, the strategy can be further improved. But no strategy eliminates losses entirely. Manage risks properly when using it for trend following.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|8|MACD Fast Length|
|v_input_3|24|MACD Slow Length|
|v_input_4|7|RSI Length|
|v_input_5|0.2|RSI Threshold|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-28 00:00:00
end: 2023-09-27 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("MACD + RSI", overlay=true)

src = input(close,"Source")

//MACD
len1 = input(8, title="MACD Fast Length")
len2 = input(24, title="MACD Slow Length")
ema1 = ema(src,len1)
ema2 = ema(src,len2)
div = ema1-ema2
long_macd = div>div[1]
short_macd = div<div[1]

//RSI
len = input(7, minval=1, title="RSI Length")
rsi_threshold = input(0.2,minval=0,maxval=0.5, title="RSI Threshold")
rsi = rsi(src,len)
long_rsi = rsi<30*(1+rsi_threshold)
short_rsi = rsi>70*(1-rsi_threshold)


//POSITIONING
if (long_macd)
    if(long_rsi)
        strategy.entry("Long", strategy.long)

if (short_macd)
    if(short_rsi)
        strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/428103

> Last Modified

2023-09-28 16:17:53
