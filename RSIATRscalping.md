
> Name

Super scaling strategy based on RSI and ATR channels
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11c8252bf57ef793872.png)
[trans]

## Overview
This strategy is based on the relative strength index (RSI) and the average true range (ATR) channel. It is suitable for 5-minute and 15-minute time periods and is a super scalping type strategy. The strategy uses the RSI indicator to determine the entry point in the long and short directions, and uses the ATR channel to set stop loss and take profit to achieve high-frequency trading.
## Strategy Principle
1. Use the 21-day exponential moving average (EMA) and the 65-day EMA to form a golden cross to determine the direction of the general trend.
2. RSI is bearish when it is below 50 and bullish when it is above 50, giving buy and sell signals.
3. The upper and lower rails of the ATR channel are: close+ATR and close-ATR respectively. Sell ​​when close breaks through the upper track of ATR, and buy when it breaks through the lower track of ATR.
4. Use 2 times of ATR to set stop loss and 5 times to set take profit.
## Advantage Analysis
1. Use golden cross and dead cross to judge the general trend and avoid operating against the trend.
2. RSI can determine better entry opportunities.
3. Setting stop-loss and stop-profit points on the ATR channel is effective and greatly improves the profit-loss ratio.
4. Suitable for high-frequency scalping transactions and quick profits.
## Risk Analysis
1. Pay close attention to the market. Missing the entry or stop loss point may cause large losses. 
2. Multiple positions may be added in the trending market, so the capital ratio needs to be controlled.
3. Sufficient funds are needed to support frequent transactions.
## Optimization direction
1. Optimize ATR parameters to make stop loss and profit more reasonable.
2. Add other indicator filters to improve the quality of admission. 
3. Add automatic stop loss and take profit functions.
4. Add fund management and position control modules.
## Summarize
This strategy belongs to the high-frequency scalping trading type. It uses the RSI indicator and ATR channel to set entry and exit points to achieve fast trading. The advantages are quick profits, good risk control, and suitable for short-term operations on highs and lows. However, it requires close monitoring of the market and sufficient funds to support frequent transactions. Overall, this strategy works well and can improve profitability through further optimization.
||

# Super Scalping Strategy Based on RSI and ATR Channel

## Overview

This strategy is based on Relative Strength Index (RSI) and Average True Range (ATR) channel, suitable for 5-min and 15-min timeframes, belonging to super scalping strategy type. It determines long/short direction entry points through RSI indicator and utilizes ATR channel to set stop loss and take profit, realizing high frequency trading.

## Strategy Principle 

1. Use 21-day Exponential Moving Average (EMA) and 65-day EMA to form golden cross and dead cross, judging the major trend direction.
2. When RSI is below 50, it is bearish; when above 50, it is bullish, sending out buy and sell signals.
3. The upper and lower bands of ATR channel are: close+ATR and close-ATR. Sell when close breaks through the upper band of ATR and buy when it breaks through the lower band.  
4. Set stop loss at 2 times ATR and take profit at 5 times ATR.

## Advantage Analysis

1. Using golden cross and dead cross to determine major trend, avoiding trading against the trend.
2. RSI can identify better entry timing.
3. ATR channel sets stop loss and take profit points effectively, greatly improving profit-loss ratio. 
4. Suitable for high frequency scalping trading with quick profits.

## Risk Analysis  

1. Need to watch the market closely, otherwise missing entry or stop loss points may lead to huge loss.
2. In trending market, multiple add-on positions may occur, needing good control of position sizing.
3. Enough capital is required to support frequent trading.  

## Optimization Direction

1. Optimize ATR parameters for more reasonable stop loss and take profit.
2. Add other indicator filters to improve entry quality.
3. Add auto stop loss and take profit functions. 
4. Include capital management and position sizing control modules.

## Summary

This strategy belongs to high frequency scalping trading type. It sets entry and exit points through RSI indicator and ATR channel for quick trades. The advantages are quick profit with good risk control, suitable for trading along the trend. However, close market watch is needed with enough capital supporting frequent trades. Overall speaking, this strategy performs well for trend trading and could be further improved on profitability through optimization.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-20 00:00:00
end: 2023-11-27 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Super Scalper - 5 Min 15 Min", overlay=true)

// Create Indicator's
shortSMA = ema(close, 21)
longSMA = ema(close, 65)
rsi = rsi(close, 14)
atr = atr(14)

// Specify  conditions
longCondition = open < close-atr
shortCondition = open > atr+close
GoldenLong = crossover(shortSMA,longSMA)
Goldenshort = crossover(longSMA,shortSMA)

plotshape(shortCondition, title="Sell Label", text="Sell", location=location.abovebar, style=shape.labeldown, size=size.tiny, color=color.red, textcolor=color.white, transp=0)
plotshape(longCondition, title="Buy Label", text="Buy", location=location.belowbar, style=shape.labelup, size=size.tiny, color=color.green, textcolor=color.white, transp=0)
plotshape(Goldenshort, title="Golden Sell Label", text="Golden Crossover Short", location=location.abovebar, style=shape.labeldown, size=size.tiny, color=color.blue, textcolor=color.white, transp=0)
plotshape(GoldenLong, title="Golden Buy Label", text="Golden Crossover Long", location=location.belowbar, style=shape.labelup, size=size.tiny, color=color.yellow, textcolor=color.white, transp=0)
// Execute trade if condition is True
if (longCondition)
    stopLoss = low - atr * 2
    takeProfit = high + atr * 5
    strategy.entry("long", strategy.long, 1, when = rsi > 50)


if (shortCondition)
    stopLoss = high + atr * 2
    takeProfit = low - atr * 5
    strategy.entry("short", strategy.short, 1, when = rsi < 50)


// Plot ATR bands to chart
plot(atr+close)
plot(close-atr)

// Plot Moving Averages
plot(shortSMA, color = color.red)
plot(longSMA, color = color.yellow)
```

> Detail

https://www.fmz.com/strategy/433562

> Last Modified

2023-11-28 15:15:14
