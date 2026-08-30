
> Name

Strategy-of-Support-Resistance-with-MACD-LONG
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/bebfe3dd108edb4186be9a34cd40b77ff4d056ff12a1c57294625073ffb799ce.png)
[trans]

## Overview
This strategy combines the support and resistance analysis of price trends and the trend analysis of the MACD indicator, and realizes low-risk long-term operations in key support and resistance areas on the premise that the trend direction is determined, aiming to obtain greater profits that exceed the stop-loss price.
## Strategy Principle
1. Identify key support and resistance levels with the “Price Action - Support & Resistance by DGT” indicator. This indicator determines support and resistance based on price action. These levels are often potential areas for price reversal or consolidation.
2. After the indicator identifies support and resistance levels, it is necessary to confirm the strength of the support and resistance by analyzing historical price behavior near these levels. A level that touches or rebounds multiple times indicates that the support or resistance effect of that level is stronger.
3. Add the MACD indicator, which consists of the MACD line, the Signal line and the Histogram of the difference between the two. MACD identifies trends and potential trend reversals. When the MACD line crosses the Signal line and the Histogram is positive, it indicates that a bull trend is expected.
4. Combining the support level identified by the "Price Action - Support & Resistance by DGT" indicator and the trend direction identified by the MACD indicator, trading opportunities can be found:
- Long trading: When the price is close to a strong support level, if the MACD line crosses the Signal line and the Histogram is positive, it means that a long trend is expected to form. Go long near the support level and set a stop loss line below the support level.
5. After entering a trade, you can set a profit target based on the distance between the entry point and the nearest important support or resistance; at the same time, use a trailing stop loss or other risk management techniques to lock in profits and control risks.
## Advantage Analysis
- Use support and resistance to identify key reversal areas, which are lower risk trading areas
- Use MACD to determine the direction of the trend, only trade when the trend is confirmed, and avoid trading against the trend.
- Go long near the support level, stop loss and exit, the risk is controllable
- The target profit is large and it is expected to achieve a larger profit than the stop loss.
- Support, resistance and MACD can verify each other's signals and increase the success rate
## Risk Analysis
- Support and resistance may be breached, and you need to pay attention to the price trend after the breakthrough.
- MACD has hysteresis and misjudgments may occur
- There is a probability that the stop loss will be triggered, and the risk of a single stop loss needs to be controlled.
- It is necessary to pay attention to whether the profit target is set reasonably. If it is too aggressive, it may not be achieved.
- Need to pay attention to and verify each signal to avoid false signals
Solutions corresponding to risks:
- Breakthrough of support and resistance requires timely stop loss or reverse trade
- MACD needs to be cautious when judging signals. Use it in conjunction with price to verify the signal.
- Single stop loss risk is controlled at 1-2% to avoid excessive losses
- Don’t set profit targets too aggressively; adjust them appropriately.
- You must wait for confirmation of each signal before entering the market, and do not blindly follow orders.
## Optimization direction
- Can test the effect of support and resistance indicators under different parameters
- You can optimize MACD parameters and obtain more accurate MACD signals
- You can add other indicators for signal verification, such as RSI, etc.
- You can study indicators such as Bollinger Bands to set stop loss and take profit
- Automatic trailing stop can be added to better lock in profits
- Parameter optimization can be performed for different varieties
- Specific stop loss and take profit parameters can be optimized through backtesting
## Summarize
This strategy integrates trend judgment and key area trading methods. After obtaining the determined trend direction, select a risk-controllable support area to perform low-risk operations in order to obtain greater profits that exceed the stop loss. This long-term operation model only requires a smaller number of transactions to achieve stable returns. Of course, no strategy can completely avoid losses, and strict risk management measures need to be taken to control losses. By continuously optimizing parameters and signal verification methods, this strategy can achieve a higher winning rate. Generally speaking, this strategy provides a relatively stable long-term trading idea.
|| 


## Overview

This strategy combines the support & resistance analysis of price action and the trend analysis of the MACD indicator. It aims to make low-risk long trades at key support & resistance levels when the trend direction is determined, in order to gain profits exceeding the stop loss.

## Strategy Logic

1. Identify key support and resistance levels using the "Price Action - Support & Resistance by DGT" indicator. This indicator determines support and resistance based on price action. These levels are often potential areas where price may reverse or consolidate.

2. After the indicator identifies support and resistance levels, confirm the strength of these levels by analyzing historical price behavior around them. Multiple touches or bounces from the same level indicates stronger support or resistance.

3. Add the MACD indicator, consisting of the MACD line, signal line and histogram representing the difference between the two lines. MACD helps identify momentum and potential trend reversals. When the MACD line crosses above the signal line and the histogram turns positive, it suggests bullish momentum is likely to form.

4. Combine the support identified by the "Price Action - Support & Resistance by DGT" indicator and the trend direction by the MACD indicator to spot trading opportunities:

    - Bullish Trade: When price approaches a strong support level, if the MACD line crosses above the signal line and the histogram turns positive, it indicates potential bullish trend. Go long near the support with a stop loss below the support level.

5. After entering a trade, set the profit target based on the distance between entry price and the nearest significant support/resistance. Also use trailing stop loss or other risk management techniques to lock in profit and limit loss.

## Advantage Analysis 

- Trade at key reversal areas identified by support & resistance, which carries lower risk
- Only trade when the trend is determined by MACD, avoiding trading against the trend 
- Long near support with stop loss, risk is controlled
- Profit target is large, with potential to gain profit exceeding the stop loss
- Support & resistance and MACD can validate each other's signals, increasing success rate

## Risk Analysis

- Support & resistance levels may be broken, need to watch price action after breakout
- MACD has lagging effect, may generate false signals  
- Stop loss being triggered is probable, need to control loss per trade
- Need to ensure reasonable profit target, overly aggressive target may not be achieved
- Need to verify all signals to avoid false signals

Solutions to the risks:

- Breakout of support & resistance needs timely stop loss or reverse trade
- Be cautious when MACD signals, use price action to verify 
- Keep single stop loss at 1-2% to avoid large loss
- Don't set profit target too aggressively, can lower it appropriately
- Only enter trade after all signals are confirmed, avoid blindly following

## Optimization Directions

- Test support & resistance indicator with different parameters
- Optimize MACD parameters for more accurate signals
- Add other indicators like RSI for signal verification
- Study bands like Bollinger Bands for stop loss and take profit
- Add trailing stop loss to better lock in profits
- Optimize parameters for different products  
- Backtest to find optimal stop loss and take profit levels

## Summary

This strategy integrates trend determination and key zone trading. It makes low-risk trades at key support levels when the trend is determined, in order to gain profits exceeding the stop loss. With this long-term trading mode, stable profits can be achieved with relatively few trades. Of course, no strategy can completely avoid losses. Strict risk management is needed to control the downside. Through continuous optimization of parameters and signal verification methods, this strategy can achieve higher win rate. In conclusion, it provides a robust framework for long-term trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|100|Support Level Strength|
|v_input_2|100|Resistance Level Strength|
|v_input_3|5|Stop Loss Level (%)|
|v_input_4|7.5|Take Profit Level (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-23 00:00:00
end: 2023-10-29 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Price Action - Support & Resistance + MACD Strategy", overlay=true)

// Price Action - Support & Resistance
supportLevel = input(100, title="Support Level Strength", minval=1)
resistanceLevel = input(100, title="Resistance Level Strength", minval=1)

var supportPrice = 0.0
var resistancePrice = 0.0

if low <= supportPrice or barstate.islast
    supportPrice := low
if high >= resistancePrice or barstate.islast
    resistancePrice := high

plot(supportPrice, color=color.green, linewidth=1, title="Support")
plot(resistancePrice, color=color.red, linewidth=1, title="Resistance")

// MACD Indicator
[macdLine, signalLine, _] = macd(close, 26, 100, 9)
macdHistogram = macdLine - signalLine

// Bullish Trade Setup
bullishSetup = crossover(macdLine, signalLine) and macdHistogram > 0 and close > supportPrice
plotshape(bullishSetup, color=color.green, title="Bullish Setup", style=shape.triangleup, location=location.belowbar)

// Stop Loss and Take Profit Levels
stopLossLevel = input(5, title="Stop Loss Level (%)", minval=0.1, step=0.1)
takeProfitLevel = input(7.5, title="Take Profit Level (%)", minval=0.1, step=0.1)

// Execute Long Trades
if bullishSetup
    stopLossPrice = close * (1 - stopLossLevel / 100)
    takeProfitPrice = close * (1 + takeProfitLevel / 100)
    strategy.entry("Long", strategy.long)
    strategy.exit("Exit", "Long", stop=stopLossPrice, limit=takeProfitPrice)

```

> Detail

https://www.fmz.com/strategy/430589

> Last Modified

2023-10-30 16:18:34
