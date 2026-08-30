
> Name

Momentum-Breakout-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is based on a combination of moving averages and momentum indicators and is a trend following strategy. It determines the market trend direction by calculating the moving average within a certain period. When the price breaks through the moving average, it is considered that the trend has turned and trading can be carried out. At the same time, it introduces the number of days of continuous rise or fall within a certain period as a confirmation signal to avoid being deceived by false breakthroughs.
## Strategy Principle
This strategy is mainly based on two indicators:
1. Simple Moving Average (SMA): Calculate the average closing price within a certain period to determine the general trend direction.
2. Number of days of continuous rise/fall: counting the number of days that the price continues to rise or fall, as a confirmation signal of a trend turning point.
Specifically, the strategy first calculates the SMA with a length of 520 days, which represents the general trend direction. If the price rises and breaks through the SMA, the counting of rising days begins; if the price falls and breaks the SMA, the counting of falling days begins. When the number of rising or falling days reaches 27 days, trade in the corresponding direction.
For example, if the price rises above the SMA and continues to rise for 27 days, a long trade is made; if the price falls below the SMA and continues to fall for 27 days, a short trade is made.
## Advantage Analysis
This strategy combines moving averages and momentum indicators to effectively track trends while avoiding short-term market noise. Its main advantages are:
1. Using long-period SMA to determine the general trend can effectively filter out the noise of short-term fluctuations.
2. Adding confirmation signals for the number of days of continuous rise/fall can avoid being deceived by short-term false breakthroughs and reduce unnecessary transactions.
3. Only trade when the trend turns, so that you can capture the direction and strength of the trend to the greatest extent.
4. The rules are clear and easy to implement, do not require complicated parameter optimization, and are suitable for ordinary investors.
## Risk Analysis
There are also some risks with this strategy:
1. In a long-term trending bull market, early entry opportunities may be missed.
2. In a volatile market, it is easy to be deceived by frequent false breakthroughs and produce too many invalid transactions.
3. Improper setting of SMA parameters may cause the strategy to be unresponsive to trend changes.
4. Improper setting of perfusion parameters may result in too frequent or sparse trading signals.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Add multi-time period SMA and conduct multi-period verification to avoid the limitations caused by a single period.
2. Add other trend indicators, such as MACD, etc., to make comprehensive judgments and improve accuracy.
3. Optimize the perfusion parameters and find the balance point. Avoid trading signals that are too frequent or sparse.
4. Add a stop loss strategy to control single losses.
5. Combine quantity and energy indicators to avoid risks caused by deviations in quantity and energy.
## Summarize
Overall, this strategy is a simple and practical trend following strategy. It uses long-period SMA to determine the general trend, and uses perfusion to confirm trend turning signals, which can effectively track the trend while avoiding being deceived by noise. With certain optimization, it can become a reliable trend strategy. However, caution still needs to be taken to guard against limitations in specific market situations. Generally speaking, this strategy is suitable for investors with certain trading experience and can be used as part of a portfolio strategy.
|| 

## Overview

This strategy combines moving average and momentum indicators, belonging to trend following strategies. It judges the market trend direction by calculating the moving average over a certain period. When the price breaks through the moving average, it is considered that the trend has reversed, and trading can be carried out. At the same time, it introduces the number of consecutive up or down days within a certain period as a confirmation signal to avoid being deceived by false breakouts.

## Strategy Principle  

This strategy is mainly based on two indicators:

1. Simple Moving Average (SMA): Calculates the average closing price over a certain period to determine the general trend direction. 

2. Consecutive up/down days: Counts the number of days the price has been in a persistent uptrend or downtrend as a confirmation signal for trend reversal.

Specifically, the strategy first calculates the 520-day SMA, representing the general trend direction. If the price rises and breaks through the SMA, it starts counting the number of up days; if the price falls and breaks through the SMA, it starts counting the number of down days. When the number of up days or down days reaches 27 days, a corresponding directional trade is made. 

For example, if the price rises and breaks through the SMA, and continues to rise for 27 days, a long trade is made; if the price falls and breaks through the SMA, and continues to fall for 27 days, a short trade is made.

## Advantage Analysis

This strategy combines moving averages and momentum indicators to effectively track trends while avoiding short-term market noise interference. Its main advantages are:

1. Using long-period SMA to judge the major trend can effectively filter out short-term fluctuations and noise.

2. Increasing confirmation signals of consecutive up/down days can avoid being deceived by short-term false breakouts and reduce unnecessary trading.

3. Trading only when trend reverses can maximize capturing the direction and momentum of the trend. 

4. The rules are clear and easy to implement, no complex parameter optimization is needed, suitable for ordinary investors.

## Risk Analysis

This strategy also has some risks:

1. It may miss early entry opportunities in long-term bull market trends.

2. It is prone to be deceived by frequent false breakouts in range-bound markets, resulting in excessive invalid trading.

3. If SMA parameters are set improperly, the strategy may respond sluggishly to trend changes. 

4. If perfusion parameters are set improperly, trading signals may be too frequent or too sparse.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Add SMA of multiple timeframes for multi-cycle verification to avoid limitations of a single cycle.

2. Add other trend indicators such as MACD for comprehensive judgment to improve accuracy.

3. Optimize perfusion parameters to find a balance point, avoiding too frequent or too sparse trading signals.

4. Add stop loss strategies to control single loss.

5. Incorporate volume indicators to avoid risks of volume divergence.

## Summary

Overall, this strategy is a simple and practical trend following strategy. It judges the major trend with long-period SMA and uses perfusion to confirm trend reversal signals, which can effectively track trends while avoiding noise deception. With some optimization, it can become a reliable trend strategy. But still need to be aware of limitations under certain market conditions. In general, this strategy is suitable for investors with some trading experience, to be used as part of a portfolio strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|520|length|
|v_input_2|27|confirmBars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-09-18 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


strategy(title="Mbit Moving Average",overlay=true)

length = input(520)
confirmBars = input(27)
price = close
ma = ta.sma(price, length)

bcond = price > ma

bcount = bcond ? nz(bcount[1]) + 1 : 0

scond = price < ma

scount = scond ? nz(scount[1]) + 1 : 0

long =  scount == confirmBars

short = bcount == confirmBars


//Strategy

strategy.entry("long", strategy.long, when=long)

strategy.entry("short",strategy.short, when=short)

```

> Detail

https://www.fmz.com/strategy/427269

> Last Modified

2023-09-19 16:33:13
