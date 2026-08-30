
> Name

Quantitative-Trading-Dual-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f5be46db2dc9f1350f.png)
 [trans]

## Overview
The name of this strategy is "Quantitative Trading Dual Indicator Strategy". This strategy uses two indicators, the Bollinger Bands indicator and the relative strength indicator, as trading signals at the same time to implement a dual indicator filtering trading strategy.
## Strategy Principle
The core logic of this strategy is to use both Bollinger Bands and RSI indicators to determine the overbought and oversold conditions of the market and filter trading signals.
Specifically, the upper and lower rails of Bollinger Bands can determine whether the price is outside the fluctuation range, and thus whether the market is overbought or oversold. The Relative Strength Index (RSI) can determine the strength of market forces. When the RSI is above 55, it is an overbought signal, and when it is below 45, it is an oversold signal.
This strategy is set to perform corresponding buying or selling operations only when the Bollinger Bands indicator and the RSI indicator both display overbought or oversold signals. This can filter out some misleading signals and improve the stability of the strategy.
## Strategic Advantages
The biggest advantage of this strategy is that it uses dual indicators for filtering, which can reduce misleading transactions and improve the reliability of signals.
Compared with a single Bollinger Band indicator, the dual indicator strategy can greatly reduce the probability of false signals. Compared with a single RSI indicator, Bollinger Bands can be used to determine whether it is outside the shock range to prevent false signals from being generated in a volatile market.
Overall, the dual indicator strategy takes into account a variety of situations and has better adaptability and stability.
## Strategy risks and solutions
The main risk of this strategy is that both the Bollinger Bands parameter settings and the RSI parameter settings may be inappropriate. If the Bollinger Bands parameters are set too sensitively, redundant signals will easily be generated; if the RSI parameters are set too loosely, the effect will be weakened.
In addition, the dual indicator combination itself means that there will be fewer signals. If the market only meets the signal of one indicator and the other indicator does not reach the trigger level, then this strategy will not generate a signal. Therefore, compared to a single indicator strategy, the trading frequency of this strategy will be lower.
The main solutions include setting more appropriate parameters, modifying the trigger levels of RSI and Bollinger Bands, etc. If the trading frequency is too low, you can consider lowering the parameter requirements to increase entry opportunities.
## Strategy optimization direction
This strategy can be optimized from the following directions:
1. Test different combinations of Bollinger Bands parameters and RSI parameters to find a more matching combination. Existing parameters may not be fully suitable for all varieties and time periods.
2. Add stop-loss and take-profit strategies to improve profit results. Current strategies do not take these aspects into account.
3. Add a position management mechanism. Use dynamic positions to increase your position when the trend is good and reduce losses when the trend is bad.
4. Add parameter adaptation function based on historical data. Allow indicator parameters to be automatically optimized to adapt to the latest market conditions.
## Summarize
As a dual-index filtering strategy, this strategy has good overall stability and adaptability. While reducing the proportion of false signals, it also reduces the frequency of transactions. By optimizing indicator parameters and adding auxiliary functions, the profit margin of the strategy can be further enhanced.
||

## Overview

The strategy is named "Quantitative Trading Dual Indicator Strategy". It utilizes both Bollinger Bands and the Relative Strength Index (RSI) as trading signals to implement a dual indicator filtered trading strategy.

## Strategy Logic

The core logic of this strategy is to use both Bollinger Bands and RSI to judge overbought and oversold conditions in the market for trading signal filtering.  

Specifically, Bollinger Bands upper and lower bands can determine if prices are outside the volatility range, thereby judging if the market is overbought or oversold. The Relative Strength Index (RSI) can judge the strength of market forces. RSI above 55 is an overbought signal, and below 45 an oversold signal.

The strategy is set so that buy or sell operations are only carried out when Bollinger Bands and RSI both display overbought or oversold signals at the same time. This filters out some misleading signals and improves the stability of the strategy.

## Advantages of the Strategy

The biggest advantage of this strategy is the use of dual indicators for filtering, which can reduce misleading trades and improve signal reliability.

Compared to a single Bollinger Bands indicator, the dual indicator strategy can greatly reduce the probability of false signals. Compared to a single RSI indicator, Bollinger Bands can be used to determine if it is currently outside the oscillation range to prevent wrong signals in an oscillating market.

Overall, the dual indicator strategy comprehensively considers multiple situations and has better adaptability and stability.

## Risks of the Strategy and Solutions

The main risk of this strategy is that the parameter settings of both Bollinger Bands and RSI may be inappropriate. If Bollinger Bands parameters are set to be too sensitive, it is prone to generate redundant signals. If RSI parameters are set too loose, the effect will be weakened.

In addition, the dual indicator combination itself means fewer signals. If the market only meets the signals of one indicator while the other has not reached the trigger level, this strategy will not generate any signals. Therefore, compared to single indicator strategies, the trading frequency of this strategy will be lower.

The solutions mainly include setting more appropriate parameters, modifying RSI and Bollinger Bands trigger levels, etc. If the trading frequency is too low, consider reducing parameter requirements to increase entry opportunities.

## Optimization Directions  

This strategy can be optimized in the following aspects:

1. Test different combinations of Bollinger Bands and RSI parameters to find better matches. Existing parameters may not be suitable for all products and time periods.

2. Add stop loss and take profit strategies to improve profitability. Currently there are no considerations in these regards. 

3. Add position sizing mechanisms. Use dynamic position sizing to increase positions when the trend goes well, and reduce losses when the trend goes badly.

4. Add parameter self-adaptivity based on historical data. Allow indicator parameters to be automatically optimized to suit latest market conditions.

## Conclusion 
As a dual indicator filtered strategy, this strategy has good overall stability and adaptability. While reducing the proportion of false signals, it also reduces the trading frequency. By optimizing indicator parameters and adding auxiliary functions, the profit potential of the strategy can be further enhanced.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Bollinger Bands SMA Period Length|
|v_input_2|2|Bollinger Bands Standard Deviation|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|16|RSI Period Length|
|v_input_5|45|RSI Value Range|
|v_input_6|true|Enable Bar Color?|
|v_input_7|true|Enable Background Color?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-07 00:00:00
end: 2024-01-11 23:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Bollinger Bands + RSI, Double Strategy (by SlumdogTrader)", shorttitle="BolBand_RSI_Strat", overlay=true)

// SlumdogTrader's Bollinger Bands + RSI Double Strategy - Profit Trailer
//
// Version 1.0
// Script by SlumdogTrader on July Fri 13(!), 2018.
//
// This strategy uses a normalise Bollinger Bands + RSI.
//
// Bollinger Band triggers
// SELL - when the price is above the upper band.
// BUY - when the price is below the lower band.
//
// RSI triggers
// SELL - when the price is above 55.
// BUY - when the price is below 45.
//
// This simple strategy only triggers when
// both the BB and the RSI
// indicators, at the same time, are in
// a overbought or oversold condition.
//
// Visit my TradingView work at:
// https://www.tradingview.com/u/SlumdogTrader/
//
// Visit my website at:
// https://www.slumdogtrader.com
//

///////////// Bollinger Bands Settings
BBlength = input(20, minval=1,title="Bollinger Bands SMA Period Length")
BBmult = input(2.0, minval=0.001, maxval=50,title="Bollinger Bands Standard Deviation")
price = input(close, title="Source")
BBbasis = sma(price, BBlength)
BBdev = BBmult * stdev(price, BBlength)
BBupper = BBbasis + BBdev
BBlower = BBbasis - BBdev
source = close
buyEntry = crossover(source, BBlower)
sellEntry = crossunder(source, BBupper)
plot(BBbasis, color=aqua,title="BBs SMA Basis Line")
p1 = plot(BBupper, color=silver,title="BBs Upper Line")
p2 = plot(BBlower, color=silver,title="BBs Lower Line")
fill(p1, p2)

///////////// RSI Settings
RSIlength = input( 16 ,title="RSI Period Length")
RSIvalue = input( 45 ,title="RSI Value Range")
RSIoverSold = 0 + RSIvalue
RSIoverBought = 100 - RSIvalue
vrsi = rsi(price, RSIlength)


///////////// Colour Settings
switch1=input(true, title="Enable Bar Color?")
switch2=input(true, title="Enable Background Color?")
TrendColor = RSIoverBought and (price[1] > BBupper and price < BBupper) ? red : RSIoverSold and (price[1] < BBlower and price > BBlower)  ? green : na
barcolor(switch1?TrendColor:na)
bgcolor(switch2?TrendColor:na,transp=50)


///////////// RSI + Bollinger Bands Strategy
if (not na(vrsi))

    if (crossover(vrsi, RSIoverSold) and crossover(source, BBlower))
        strategy.entry("RSI_BB_L", strategy.long, stop=BBlower,  comment="RSI_BB_L")
    else
        strategy.cancel(id="RSI_BB_L")

    if (crossunder(vrsi, RSIoverBought) and crossunder(source, BBupper))
        strategy.entry("RSI_BB_S", strategy.short, stop=BBupper,  comment="RSI_BB_S")
    else
        strategy.cancel(id="RSI_BB_S")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)

```

> Detail

https://www.fmz.com/strategy/438780

> Last Modified

2024-01-15 12:18:53
