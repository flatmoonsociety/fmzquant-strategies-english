
> Name

Donchian-Channel-Breakout-Strategy Donchian-Channel-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is based on the Donshian Channel indicator and uses the price breakthrough of the upper and lower rails of the channel as a trading signal to implement trend tracking operations for stocks/futures/crypto/forex and other varieties. It is a trend breakthrough strategy for medium and long-term positions.
## Strategy Principle
1. Calculate the highest and lowest prices in a given period (such as the 20th) to obtain the upper and lower tracks of the Donshian Channel.
2. The channel midline is the average of the upper and lower rails. A breakthrough on the upper track is a signal that the trend is turning to bullish, and a breakthrough on the lower track is a signal that the trend is turning to bearish.
3. When the price closes and breaks through the upper track, it is judged that the trend has started, and you enter the market long.
4. When the price falls below the midline, it is deemed to be a stop-profit exit.
5. You can refer to the backtesting time period to generate actual trading signals.
6. Optionally, you can also use the price breaking through the lower track as a short selling signal.
This strategy determines the start of the trend by breaking through the channel, uses the midline to take profit as the entry point, and captures the medium and long-term trend market. Channel parameters can be adjusted to suit the market.
## Advantage Analysis
1. The Donshian channel is simple to calculate and the indicators are easy to implement.
2. The price breaks through the channel to determine trend changes.
3. The midline of the channel serves as the take-profit level and should be set appropriately.
4. The trading signal rules are clear and easy to execute.
5. Channel parameters can be flexibly adjusted to adapt to various varieties and cycles.
6. Can evaluate long-term or short-term trading effects.
7. Large expansion space, other technical indicators can be introduced.
## Risk Analysis
1. There is a lag in the channel breakthrough and the risk of missing early opportunities.
2. Failure to consider the divergence before the breakthrough may produce false signals.
3. The midline stop loss range is fixed and is sensitive to market shocks.
4. Improper selection of the backtest period may lead to overfitting.
5. If a stop-loss strategy is not set up, attention should be paid to the risk of loss expansion.
## Optimization direction
1. Test and optimize channel cycle parameters.
2. Evaluate other types of moving averages as take profit lines.
3. Add filtering conditions for indicators such as trading volume.
4. Set up a trailing stop or trailing stop strategy.
5. Introduce machine learning to predict price breakthroughs.
6. Optimize fund management strategies and establish profit-loss ratios.
7. Consider long and short-term mixed operations or multi-variety combinations.
## Summarize
This strategy is based on the Donshian Channel, determines the trend direction, and operates with breakthroughs. It is a typical medium and long-term trend following strategy. Optimizing channel parameters and supplementing them with other technical indicators can form a more stable breakthrough system. This strategy is simple and clear, has a lot of room for expansion, can be used as a basic strategy module for quantitative trading, and has good practicality.
|| 

## Overview

This strategy uses the Donchian Channel indicator to trade breakouts of the upper and lower bands, enabling trend following operations across stocks/futures/crypto/forex etc, belonging to medium-to-long-term trend breakout strategies.

## Strategy Logic

1. Calculate the highest high and lowest low over a given period (e.g. 20 days) to get the upper and lower bands.

2. The midline is the average of the upper and lower bands. Breaking upper band signals uptrend, breaking lower band signals downtrend.

3. When price closes above upper band, determine uptrend has started, go long to enter. 

4. When price breaks below midline, take profit to exit.

5. Can reference backtest timeframe to generate actual trading signals.

6. Optionally, breaking lower band can also act as short signal.

The strategy determines trend start by channel breakouts, uses midline as profit taking exit, capturing mid-to-long term trends. Channel parameters can be adjusted to fit the market. 

## Advantage Analysis

1. Donchian Channel is simple to calculate and implement.

2. Price breaking channel signals trend change.

3. Midline as profit taking level is reasonably set. 

4. Clear signal rules, easy to execute.

5. Can flexibly adjust channel parameters for different products and timeframes.

6. Can evaluate long term or short term trading performance.

7. Large expansion space, can introduce other technical indicators.

## Risk Analysis

1. Channel breakout may lag, risking missed early opportunities. 

2. Does not consider divergence before breakout, may generate false signals.

3. Fixed midline stop loss sensitive to market volatility.

4. Improper backtest period risks over-fitting. 

5. Lacks stop loss, need to watch out for enlarged losses.

## Optimization Directions

1. Test and optimize channel period parameters.

2. Evaluate other MA types as stop loss lines.

3. Add filters like volume indicators.

4. Add moving or trailing stop loss mechanisms. 

5. Introduce machine learning to predict price breakouts.

6. Optimize money management, set profit ratio etc.

7. Consider combining long/short term operations or multiple products.

## Summary

This strategy uses Donchian Channel to determine trend direction, trading breakouts, a typical mid-to-long term trend following approach. Optimizing channel parameters and adding other technical indicators can form a more robust breakout system. The clear and concise logic allows expansions, making it a foundational quant strategy module with great practical utility.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2000|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2018|Backtest Start Year|
|v_input_5|12|Backtest Start Month|
|v_input_6|true|Backtest Start Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-09-15 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//future strategy
//strategy(title = "stub", default_qty_type = strategy.fixed, default_qty_value = 1,  overlay = true, commission_type=strategy.commission.cash_per_contract,commission_value=2)
//stock strategy
strategy(title = "dc", default_qty_type = strategy.percent_of_equity, default_qty_value = 100,  overlay = true, commission_type=strategy.commission.cash_per_contract,commission_value=.005)
//forex strategy
//strategy(title = "stub", default_qty_type = strategy.percent_of_equity, default_qty_value = 100,  overlay = true)
//crypto strategy
//strategy(title = "stub", default_qty_type = strategy.percent_of_equity, default_qty_value = 100,  overlay = true, commission_type=strategy.commission.percent,commission_value=.25,default_qty_value=10000)


testStartYear = input(2000, "Backtest Start Year")
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

testEndYear = input(2018, "Backtest Start Year")
testEndMonth = input(12, "Backtest Start Month")
testEndDay = input(1, "Backtest Start Day")
testPeriodEnd = timestamp(testStartYear,testStartMonth,testStartDay,0,0)


testPeriod() =>
    true
    //time >= testPeriodStart  ? true : false

dcPeriod = 20

dcUpper = highest(close, dcPeriod)[1]
dcLower = lowest(close, dcPeriod)[1]
dcAverage = (dcUpper + dcLower) / 2

plot(dcLower, style=line, linewidth=3, color=red, offset=1)
plot(dcUpper, style=line, linewidth=3, color=aqua, offset=1)

plot(dcAverage, color=yellow, style=line, linewidth=1, title="Mid-Line Average")

strategy.entry("simpleBuy", strategy.long, when=close >= dcUpper)
strategy.close("simpleBuy",when=close < dcAverage)
    
//strategy.entry("simpleSell", strategy.short,when=close <= dcLower)
//strategy.close("simpleSell",when=close > dcAverage)
    


```

> Detail

https://www.fmz.com/strategy/427308

> Last Modified

2023-09-19 21:47:41
