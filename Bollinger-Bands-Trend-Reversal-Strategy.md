
> Name

Bollinger-Bands-Trend-Reversal-Strategy Based on Bollinger Bands Trend Reversal Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/a86989d2b12be4e00ca52966266664fc8a8384a63a3a926a65e8ebf942945389.png)

[trans]


## Overview
This strategy is based on the Bollinger Band indicator and moving average, and determines whether the price is close to the upper and lower rails of the Bollinger Band by LONG or SHORT closing positions to make profits. When the price breaks through the upper Bollinger Band, you are bearish; when the price falls below the lower Bollinger Band, you are bullish. It combines the advantages of trend reversal and breakthrough trading strategies, and can obtain better returns when the trend fluctuates.
## Principle
This strategy mainly determines the following two entry signals:
1. Bull signal: When the closing price touches the lower track and the closing price is higher than the EMA moving average, the previous K-line entity is a negative line and the current K-line entity is a positive line, go long.
2. Short signal: When the closing price touches the upper rail and is lower than the EMA, the previous K-line entity is positive and the current K-line entity is negative.
Stop loss method: fixed stop loss. The stop loss point is the risk-reward coefficient times the entry price to the counterparty's track gauge.
Take-profit method: The target profit is the opponent's square track. That is to say, long take profit is the lower track, and short take profit is the upper track.
## Advantages
1. Combining the advantages of trend and reversal strategies, it performs better in trendy and volatile markets.
2. Use the Bollinger Bands indicator to determine overbought and oversold areas and accurately determine reversal opportunities.
3. Reasonable setting of fixed stop loss points helps to control risks.
4. The moving take-profit method maximizes profits.
## Risk
1. Breakthrough strategies are prone to arbitrage, so be wary of false breakthroughs.
2. When the market is too volatile, stop loss may be triggered frequently.
3. Fixed stop loss cannot be adjusted according to market fluctuations and may be too loose or too aggressive.
4. When the Bollinger Band parameters are set improperly, the effect may be unsatisfactory.
## Optimization ideas
1. You can consider combining the RSI indicator to filter entry signals. For example, if RSI is above 50, go long, and if RSI is below 50, go short, to avoid false signals.
2. Add the function of automatically adjusting the fixed stop loss distance to make the stop loss more flexible. For example, dynamically set the stop loss distance based on the ATR indicator.
3. Optimize Bollinger Band parameters and find the best parameter combination.
4. You can test different EMA moving average parameters and optimize the moat effect of the moving average.
## Summarize
This strategy comprehensively considers trends and reversals, uses Bollinger Bands to determine overbought and oversold points for entry, and maximizes profits through moving take-profits. It performs better in trendy and volatile markets. However, attention needs to be paid to preventing quilt traps, and at the same time, the effect of parameter optimization strategies must be adjusted. Overall, it is a relatively practical and efficient strategy.
||


## Overview

This strategy utilizes Bollinger Bands and Moving Average to go LONG or SHORT when price approaches the upper or lower bands. It goes short when price breaks above the upper band and goes long when price breaks below the lower band. The strategy combines the advantages of both trend following and mean reversion strategies, and performs well during range-bound markets.

## Logic

The strategy identifies two entry signals:

1. Long signal: when close price hits the lower band while above EMA line, previous candle was bearish and current candle is bullish. 

2. Short signal: when close price hits the upper band while below EMA line, previous candle was bullish and current candle is bearish.

The stop loss uses fixed stop loss. The stop loss level is set at the entry price plus/minus risk/reward ratio times the distance between entry price and take profit level. 

The take profit uses dynamic take profit. Long take profit is set at the lower band. Short take profit is set at the upper band.

## Advantages

1. Combines the strengths of both trend following and mean reversion strategies, performs well during range-bound markets.

2. Utilizes Bollinger Bands to identify overbought and oversold levels, improving accuracy of reversal signals.

3. Fixed stop loss facilitates risk management. 

4. Dynamic take profit allows maximization of profits.

## Risks

1. Breakout strategies are susceptible to stop runs. Need to beware of false breakouts.

2. Frequent stop loss triggers when market is too choppy.

3. Fixed stop loss is not adaptive to market volatility. Can be too wide or too tight.

4. Poor parameter tuning of Bollinger Bands can lead to mediocre results.

## Enhancement

1. Incorporate RSI indicator to filter entry signals. For example, only go long if RSI is above 50, and only go short if RSI is below 50. This avoids bad signals.

2. Implement adaptive stop loss that adjusts stop distance based on volatility. E.g. use ATR to set dynamic stop loss.

3. Optimize Bollinger Bands parameters to find best parameter combinations. 

4. Test different EMA periods to enhance the EMA's support/resistance effect.

## Summary

The strategy combines trend and reversal, entering overbought/oversold levels identified by Bollinger Bands. It maximizes profits through dynamic take profit. Performs well during range-bound markets. Be wary of stop runs. Fine tune parameters to optimize performance. Overall a practical and effective strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|length|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|2|StdDev|
|v_input_4|200|EMA Input|
|v_input_5|1.5|Risk/Reward Ratio|
|v_input_6|false|Offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-24 00:00:00
end: 2023-10-31 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

// Welcome to yet another script. This script was a lot easier since I was stuck for so long on the Donchian Channels one and learned so much from that one that I could use in this one
// This code should be a lot cleaner compared to the Donchian Channels, but we'll leave that up to the pro's
// This strategy has two entry signals, long = when price hits lower band, while above EMA, previous candle was bearish and current candle is bullish
// Short = when price hits upper band, while below EMA, previous candle was bullish and current candle is bearish
// Take profits are the opposite side's band(lower band for long signals, upper band for short signals). This means our take profit price will change per bar
// Our stop loss doesn't change, it's the difference between entry price and the take profit target divided by the input risk reward
// At the time of writing this, I could probably calculate that much easier by simply multiplying the opposite band by the input risk reward ratio
// Since I want to get this script out and working on the next one, I won't clean that up, I'm sorry
// strategy(shorttitle="BB Trending Reverse Strategy", title="Bollinger Bands Trending Reverse Strategy", overlay=true, default_qty_type = strategy.cash, default_qty_value = 150, initial_capital = 1000, currency = currency.USD, commission_type = "percent", commission_value = 0.036)

// The built-in Bollinger Band indicator inputs and variables, added some inputs of my own and organised the code
length              = input(20, minval=1)
src                 = input(close, title="Source")
mult                = input(2.0, minval=0.001, maxval=50, title="StdDev")
emaInput            = input(title = "EMA Input", type = input.integer, defval = 200, minval = 10, maxval = 400, step = 1)
riskreward          = input(title = "Risk/Reward Ratio", type = input.float, defval = 1.50, minval = 0.01, maxval = 100, step = 0.01)
offset              = input(0, "Offset", type = input.integer, minval = -500, maxval = 500)
basis               = sma(src, length)
dev                 = mult * stdev(src, length)
upper               = basis + dev
lower               = basis - dev
ema                 = ema(close, emaInput)

// These are our conditions as explained above
entryLong           = low[1] <= lower[1] and low <= lower and low > ema
entryShort          = high[1] >= upper[1] and high >= upper and high < ema
reversecandleLong   = close > open and close[1] < open[1]
reversecandleShort  = close < open and close[1] > open[1]
var stopLong        = 0.0
var stopShort       = 0.0

// These are our entry signals, notice how the stop condition is within the if statement while the strategy.exit is outside of the if statement, this way the take profit targets trails up or down depending on what the price does
if reversecandleLong and entryLong and strategy.position_size == 0
    stopLong := (((close / upper - 1) * riskreward + 1) * close)
    strategy.entry("Long Entry", strategy.long, comment = "Long Entry")
    
strategy.exit("Exit Long", "Long Entry", limit = upper, stop = stopLong, comment = "Exit Long")

if reversecandleShort and entryShort and strategy.position_size == 0
    stopShort := (((close / lower - 1) / riskreward + 1) * close)
    strategy.entry("Short Entry", strategy.short, comment = "Short Entry")

strategy.exit("Exit Short", "Short Entry", limit = lower, stop = stopShort, comment = "Exit Short")


// The built-in Bollinger Band plots
plot(basis, "Basis", color=#872323, offset = offset)
p1 = plot(upper, "Upper", color=color.teal, offset = offset)
p2 = plot(lower, "Lower", color=color.teal, offset = offset)
fill(p1, p2, title = "Background", color=#198787, transp=95)
plot(ema, color=color.red)

// These plots are to check the stoplosses, they can  make a mess of your chart so only use these if you want to make sure these work
// plot(stopLong)
// plot(stopShort)
```

> Detail

https://www.fmz.com/strategy/430743

> Last Modified

2023-11-01 11:29:34
