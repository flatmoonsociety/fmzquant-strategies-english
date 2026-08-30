
> Name

Williams-R-Indicator-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
The Williams %R indicator trading strategy is based on the Williams %R indicator to generate trading signals. This indicator measures market momentum by comparing the magnitude of the current closing price to the highest and lowest prices over a certain period.
When the Williams %R indicator line breaks through the overbought line, a sell signal is generated; when the indicator line breaks through the oversold area, a buy signal is generated. The specific trading logic of the strategy is:
1. Calculate the Williams %R value for a certain period (such as the 14th)
2. Set overbought line (eg -20) and oversold area (eg -80)
3. When the indicator line breaks through the oversold area from bottom to top, go long
4. When the indicator line breaks through the overbought line from top to bottom, close the position
In this way, the strategy can open long and short positions at points where prices may reverse, and capture short-term opportunities.
## Strategic Advantages
- Simple parameter setting and clear rules
- Ability to identify overbought and oversold conditions early
- Break through the systematic trading and not be affected by personal emotions
## Strategy Risk
- Williams %R lags behind and may miss opportunities
- Requires repeated testing of optimization parameters
- Overbought and oversold only have a certain reference value
## Summarize
The Williams %R indicator strategy captures reversal opportunities by determining overbought and oversold areas. Configuring reasonable position management and stop-loss strategies can control risks. However, traders need to pay attention to the problem of indicator lag, need to assist other technical tools for verification, and use this strategy with caution.

||

## Strategy Logic

The Williams %R trading strategy generates signals based on the Williams Percent Range indicator, which measures market momentum by comparing the current close to the high-low range over a period. 

The strategy goes long when the %R line crosses above oversold, and sells when the line crosses below overbought. The logic is:

1. Calculate Williams %R over a timeframe (e.g. 14 periods)

2. Set overbought (e.g. -20) and oversold (e.g. -80) levels

3. Go long when the %R line crosses up through oversold 

4. Close longs when the %R line crosses down through overbought

This allows entries around potential reversal points to capitalize on short-term moves.

## Advantages

- Simple parameters and rules

- Early identification of overbought/oversold  

- Systematic breakout trading

## Risks

- Lagging %R may miss opportunities 

- Requires optimization of inputs

- Oversold/bought levels are rough guides

## Summary

The Williams %R strategy aims to capture reversals by trading overbought/oversold regions. With proper position sizing and stops, risk can be controlled. But lag is a key limitation requiring additional tools for validation and caution in use.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|-20|Overbought Level|
|v_input_3|-80|Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-13 00:00:00
period: 12h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © Julien_Eche

//@version=5
strategy("Williams %R Strategy", overlay=true, initial_capital=100000, shorttitle="W%R Strategy")

// Paramètres
length = input(14, "Length")
overboughtLevel = input(-20, "Overbought Level")
oversoldLevel = input(-80, "Oversold Level")

// Calcul du Williams %R
williamsR = -100 * (ta.highest(high, length) - close) / (ta.highest(high, length) - ta.lowest(low, length))

// Conditions d'achat et de vente
buySignal = ta.crossover(williamsR, oversoldLevel)
sellSignal = ta.crossunder(williamsR, overboughtLevel)

// Entrée en position longue
if buySignal
    strategy.entry("Buy", strategy.long)

// Sortie de la position longue
if sellSignal
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/426783

> Last Modified

2023-09-14 15:38:51
