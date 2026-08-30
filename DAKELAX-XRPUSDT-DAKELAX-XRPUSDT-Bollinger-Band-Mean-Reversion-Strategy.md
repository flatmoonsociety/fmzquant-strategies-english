
> Name

DAKELAX-XRPUSDT-Bollinger-Band-Mean-Reversion-StrategyDAKELAX-XRPUSDT-Bollinger-Band-Mean-Reversion-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f54e9433bd162d887f.png)
[trans]


## Overview
DAKELAX -
## Strategy Principle
This strategy first calculates the 20-period SMA moving average and the upper and lower rail fluctuation bands. The upper track is the SMA moving average plus 1.5 times the standard deviation, and the lower track is the SMA moving average minus 2.2 times the standard deviation. Then calculate the shrinkage rate of the wave band, fill it with black if the shrinkage rate is greater than 1.3, fill it with yellow if it is less than 0.1, otherwise fill it with red.
When the closing price is lower than the lower track, go long with 20 coins; when the closing price is higher than the upper track, close all positions.
This strategy also calculates the 7-day EMA fast line and the 18-day EMA slow line. When the fast line crosses the slow line, it is judged as a buy signal. When the fast line crosses below the slow line, it is judged as a sell signal.
## Advantage Analysis
- Use the fluctuation band and its shrinkage rate to judge trends and fluctuations, which is very intuitive
- Combined with the moving average golden cross and dead cross for judgment, the signal can be enhanced
- The backtest performance is better and the real offer is relatively stable.
## Risk Analysis
- After the fluctuation band shrinks, the probability of breakthrough failure is high, and it is easy to stop losses.
- Fixed quantity buying without considering position management, there is a risk of overbought and oversold
- In a volatile market, there are more golden crosses and dead crosses, which can easily lead to losses.
- Only considering daily factors without combining higher time periods, the larger direction may be missed
You can consider dynamically adjusting the buying amount or setting a stop loss to control risks. Optimize the golden cross and dead cross strategy to avoid being trapped in volatile market conditions. Combine with higher level trend indicators to determine the general direction.
## Optimization direction
- Adjust the buying amount according to the width of the fluctuation band. When the fluctuation band narrows, buy less, and when the fluctuation band expands, you can increase it appropriately.
- When the fluctuation band shrinks but the signal has not yet been triggered, you can consider accumulating short positions to establish a position.
- Combine the long-term INDICATOR indicator to determine the trend direction. When the general trend is unclear, the strategy can be suspended.
- Risk can be controlled by combining stop loss, and the stop loss point can be set to the low point of the recent fluctuation zone
- Optimize the golden cross and dead cross strategy parameters, adjust the moving average period, and avoid being trapped
## Summarize
DAKELAX-XRPUSDT is a trading robot program that uses fluctuation band contraction combined with moving average strategies. This strategy is intuitive and easy to understand, and the backtest effect is good, but there are certain risks. Risks can be reduced by adjusting the purchase quantity, stopping strategies, setting stop losses and optimizing moving average strategies. Overall, the strategy is clear and easy to operate, and it is a reference example of the Bollinger Band strategy. However, it needs to be optimized and adjusted for different currencies and market environments to achieve stable profits in the real market.
||


## Overview

DAKELAX-XRPUSDT is a trading bot strategy for XRPUSDT on Binance. It is a simple reverse to mean strategy using Bollinger Bands, and performs well in backtest on H1 timeframe from May to Aug 2019, as well as running live.

## Strategy Logic

The strategy first calculates the 20-period SMA and upper/lower Bollinger Bands. The upper band is SMA + 1.5 standard deviation, and the lower band is SMA - 2.2 standard deviation. It then calculates the contraction rate of the bands. Bands are filled black if contraction > 1.3, yellow if < 0.1, else red.

When close price is below the lower band, it goes long with 20 coins. When close is above upper band, it closes all positions. 

The strategy also calculates 7-period EMA fast line and 18-period EMA slow line. Crossover of fast line above slow line is buy signal, and crossover below is sell signal.

## Advantage Analysis

- Bollinger Bands and contraction rate intuitively identify trends and volatility
- Combine with EMA crossover adds strength to signals 
- Good backtest results and relatively stable in live trading

## Risk Analysis

- High probability of failure when breakout after band contraction
- Fixed amount buying without position sizing risks overtrading
- Too many crossovers in ranging markets risks losses
- Only considers daily factors, misses larger timeframe trends

Consider dynamic position sizing or stop loss to control risks. Optimize crossover strategy to avoid whipsaws in ranging markets. Add higher timeframe trend indicators to identify larger moves.

## Optimization Directions

- Adjust buy amount based on band width, less when contracted and more when expanded

- Consider accumulating positions when contraction seen but signal not triggered yet 

- Add longer timeframe trend INDICATOR to determine overall direction, pause strategy when unclear

- Incorporate stop loss to control risk, can set near recent lows of bands

- Optimize crossover parameters like EMA periods to avoid getting trapped

## Summary

DAKELAX-XRPUSDT is a trading bot strategy using Bollinger Band contraction with EMA crossover. It is intuitive and has good backtest results but contains some risks. These can be reduced through position sizing, stopping strategy, adding stop loss and optimizing crossover logic. Overall it provides a clear example of a Bollinger Band strategy, but requires pair-specific optimization for stable live profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|buyAmount|
|v_input_2|20|len2|
|v_input_3_close|0|src2: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-26 00:00:00
end: 2023-11-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//study(title="Tradebotler DAKELAX Binance:XRPUSDT Study-strategy", overlay=true)
strategy(title="Tradebotler DAKELAX Binance:XRPUSDT Strategy", overlay=true)

buyAmount = input(20, minval=1)

// SMA20
len2 = input(20, minval=1)
src2 = input(close)
out2 = sma(src2, len2)

// BB contraction value (medium tight)
contraction_value = 1.3
// BB contraction value (very tight)
contraction_value2 = 0.1

// 2xSTDEV BB calculation
dev = stdev(src2, len2)
upper_BB = out2  + 1.5*dev
lower_BB = out2  - 2.2*dev
x1 = plot(upper_BB, color=blue, linewidth = 2)
x2 = plot(lower_BB, color=blue, linewidth = 2)

contraction = (upper_BB-lower_BB)/out2

//fills the BBands according to the contraction value (threshold)

// Calculate values
fastMA  = ema(close, 7)
slowMA  = ema(close, 18)

// Determine alert setups
crossUp   = crossover(fastMA, slowMA)
crossDown = crossunder(fastMA, slowMA)

buySignal   = (crossUp or crossUp[1]) and (low > slowMA)
shortSignal = (crossDown or crossDown[1]) and (high < slowMA)

// Highlight alerts on the chart
bgColour =
     (buySignal and barstate.isrealtime) ? green :
     (shortSignal and barstate.isrealtime) ? red :
     na

signalBuy = (buySignal ) ? true : false
signalSell = (shortSignal ) ? true : false

test = true

test := not test[1]

closesBelowLowerBB = close < lower_BB
closesAboveUpperBB = close > upper_BB

tmptext = "blah"

// Plot values
plot(series=fastMA, color=teal)
plot(series=slowMA, color=orange)

plot(out2, color=black, linewidth = 1)
fill(x1, x2, color = contraction > contraction_value ? black : contraction < contraction_value2 ? yellow: red)

isInRed = contraction < contraction_value and contraction >= contraction_value2
isInYellow = contraction < contraction_value and contraction < contraction_value2

if ( closesBelowLowerBB )
    strategy.order('Buy', strategy.long, buyAmount)

if ( closesAboveUpperBB )
    strategy.close_all()


```

> Detail

https://www.fmz.com/strategy/430877

> Last Modified

2023-11-02 16:18:34
