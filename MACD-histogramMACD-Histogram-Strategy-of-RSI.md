
> Name

MACD-histogram strategy MACD-Histogram-Strategy-of-RSI
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11bdcbcb67f43715117.png)
[trans]

## Overview
This strategy generates trading signals based on the MACD of the RSI indicator. It combines the characteristics of the RSI indicator to judge overbought and oversold markets, and the advantages of MACD to judge market trends and momentum changes, and designs a strategy that comprehensively uses multiple indicators to provide trading signals.
## Strategy Principle
This strategy first calculates the RSI indicator, and then calculates the MACD indicator based on the RSI indicator. The RSI indicator can determine the overbought and oversold conditions of the market, and the MACD indicator can capture changes in market trends and momentum.
Specifically, the strategy first calculates the 14-period RSI indicator. Then calculate the MACD indicator based on the RSI indicator, including the 12-period and 26-period EMA moving averages, and the 9-period signal line. Calculate the MACD histogram.
A buy signal is generated when the MACD histogram crosses the 0 axis above; a sell signal is generated when the MACD histogram crosses the 0 axis below. In this way, RSI is used to determine whether the market is overbought or oversold, and MACD is used to determine changes in market trends and momentum to generate trading signals.
## Strategic Advantages
This strategy combines the advantages of the two indicators RSI and MACD, which can judge the state of the market more comprehensively, and the signal is more reliable.
1. Use RSI to determine overbought and oversold conditions, which is helpful for stock selection and preventing false breakthroughs.
2. The MACD indicator determines trends and momentum changes, making trading signals clearer.
3. RSI combined with MACD can filter out false signals based on multiple factors.
## Strategy Risk
1. The parameter settings of RSI and MACD will affect the strategy performance and need to be adjusted and optimized.
2. The combination of multiple indicators increases the complexity of the strategy and the probability of error.
3. MACD trading signals may lag behind and need to be combined with other indicators to assist judgment.
## Strategy optimization
1. Optimize the parameters of RSI and MACD and find the best parameter combination.
2. Add other indicator judgments, such as KDJ, Bollinger Bands, etc., to form indicator clusters and improve signal accuracy.
3. Add a stop-loss strategy to control single losses.
4. Optimize the logic of opening and closing positions to prevent conflicting signals.
## Summarize
This strategy comprehensively uses the advantages of two indicators, RSI and MACD, to form trading signals. It determines overbought and oversold while considering trend and momentum factors, which can effectively filter out false signals and have high signal quality. The next step is to further improve the strategy through parameter optimization, stop loss strategies, and adding other indicators to make the signal more accurate and reliable.
||


## Overview  

This strategy generates trading signals based on the MACD of RSI indicator. It combines the RSI indicator's ability to judge overbought and oversold levels in the market, as well as MACD's advantage in determining market trend and momentum changes, to design a strategy that utilizes multiple indicators to provide trading signals.

## Strategy Logic   

The strategy first calculates the RSI indicator, then computes the MACD based on the RSI indicator. The RSI indicator can determine the overbought and oversold conditions in the market, while the MACD captures changes in market trend and momentum.   

Specifically, the strategy first calculates the 14-period RSI indicator. Then based on the RSI, the MACD indicator is computed, including 12 and 26-period EMAs, as well as a 9-period signal line. The MACD histogram is then calculated.  

When the MACD histogram crosses above 0, a buy signal is generated. When the MACD histogram crosses below 0, a sell signal is triggered. This way, the strategy utilizes RSI to judge overbought/oversold levels, while also using MACD to determine trend and momentum changes, to generate trade signals.

## Advantages of the Strategy  

This strategy combines the strengths of both RSI and MACD indicators, allowing for a more comprehensive judgment of market conditions, resulting in more reliable signals.  

1. Using RSI to judge overbought/oversold levels helps with stock selection and preventing false breakouts.  

2. MACD's judgment of trend and momentum changes makes trade signals clearer.

3. The combination of RSI and MACD, with judgments based on multiple factors, helps filter out false signals.   

## Risks of the Strategy

1. Parameter settings for RSI and MACD affect strategy performance and require tuning and optimization.  

2. The combination of multiple indicators increases strategy complexity and the probability of errors.

3. MACD trade signals may lag and need to be complemented by other indicators.

## Optimization Directions  

1. Optimize RSI and MACD parameters to find best parameter combinations.  

2. Incorporate other indicators like KDJ, Bollinger Bands to form an indicator cluster and improve signal accuracy.   

3. Incorporate stop loss strategies to control per trade loss.

4. Optimize entry and exit logic to prevent conflicting signals.  

## Conclusion  

This strategy utilizes the combined strengths of RSI and MACD indicators to form trade signals, judging overbought/oversold levels while also considering trend and momentum factors, effectively filtering out false signals and providing quality signals. Next steps involve further enhancements like parameter optimization, stop loss, adding more indicators etc. to improve signal accuracy and reliability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|12|fastLength|
|v_input_3|26|slowLength|
|v_input_4|9|signalLength|
|v_input_5|6|monthfrom|
|v_input_6|12|monthuntil|
|v_input_7|true|dayfrom|
|v_input_8|31|dayuntil|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-18 00:00:00
end: 2023-12-24 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

strategy(title = "MACD of RSI", overlay = false)
//////////////////////// RSI ///////////////////////////

src = close, len = input(14, minval=1, title="Length")

up = sma(max(change(src), 0), len)

down = sma(-min(change(src), 0), len)

rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))

//////////////////////// RSI   //////////////////////////

//////////////// MACD  ////////////////////////////

sourcemacd = rsi

fastLength = input(12, minval=1), slowLength=input(26,minval=1)

signalLength=input(9,minval=1)


fastMA = ema(sourcemacd, fastLength)

slowMA = ema(sourcemacd, slowLength)

macd = fastMA - slowMA

signal = ema(macd, signalLength)

delta=macd-signal

swap1 = delta>0?green:red


plot(delta,color=swap1,style=columns,title='Histo',histbase=0,transp=20)

p1 = plot(macd,color=blue,title='MACD Line')

p2 = plot(signal,color=red,title='Signal')

fill(p1, p2, color=blue)

hline(0)

/////////////////////////MACD  //////////////////////////

// Conditions

longCond = na

sellCond = na

longCond :=  crossover(delta,0)

sellCond :=  crossunder(delta,0)

monthfrom =input(6)

monthuntil =input(12)

dayfrom=input(1)

dayuntil=input(31)

if (  longCond   )

    strategy.entry("BUY", strategy.long, stop=close, oca_name="TREND", comment="BUY")

else

    strategy.cancel(id="BUY")

if ( sellCond   )

    strategy.close("BUY")
```

> Detail

https://www.fmz.com/strategy/436487

> Last Modified

2023-12-25 11:45:10
