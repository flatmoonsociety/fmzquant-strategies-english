
> Name

Trend-Following-Strategy-Based-on-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/c205b2173853721cbed389518b40d44697130de3eadaf826145e87b9508e9c71.png)
 [trans]
## Overview
This strategy uses fast moving averages and slow moving averages to construct trading signals to identify and track trends. When the fast line crosses the slow line, a buy signal is generated; when the fast line crosses below the slow line, a sell signal is generated. This strategy is suitable for tracking medium and long-term trends and can effectively filter market noise.
## Strategy Principle
This strategy uses two Exponential Moving Averages with different periods as the basis for trading decisions. The fast moving average parameter is set to 30 days, which is used to capture shorter-term price changes; the slow moving average parameter is set to 100 days, which is used to determine the direction of the long-term price trend.
When the fast line crosses the slow line from below, it means that the market has entered an upward trend, generating a buy signal; when the fast line crosses the slow line from above, it means that the market has entered a downward trend, generating a sell signal.
## Strategic Advantages
This strategy has the following advantages:
1. Based on the moving average construction, it can effectively filter out short-term market noise and follow the trend.
2. Using the double moving average strategy can clearly determine the trend direction.
3. To achieve parameter optimization, the fast and slow moving average periods can be customized.
4. It has the function of tracking medium and long-term trends and short-term adjustments.
5. The rules are simple and clear, easy to understand and implement, and suitable for beginners to learn.
## Risk Analysis
There are also some risks with this strategy:
1. When the price moves sideways, it is easy to generate false triggering trading signals. Risks can be reduced by optimizing moving average parameters.
2. Inability to effectively judge and handle abnormal situations of violent price fluctuations. Stop losses can be set to control risk. 
3. The moving average system itself has hysteresis and may miss the price turning point. Can be combined with other indicators for optimization.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the period parameters of the moving average to improve profitability.
2. Add other conditional judgment indicators, such as trading volume indicators, etc., to avoid false breakthroughs. 
3. Add a stop-loss strategy to control single losses.
4. Combine trend indicators to determine trend strength and avoid trend reversal.
5. Add parameter optimization function to make the strategy more versatile.

## Summarize
This strategy builds a trading decision-making system based on dual moving averages, and judges market trends through the price relationship between fast moving averages and slow moving averages. The signal generation is simple and clear. This strategy filters out some noise, can follow the trend, and is suitable for medium and long-term trend trading. However, there are also some flaws. Through multi-index optimization and risk control, this strategy can be optimized to be more versatile and efficient.
||

## Overview

This strategy uses fast and slow moving averages to identify and follow trends. It generates buy signals when the fast line crosses over the slow line and sell signals when the fast line crosses below the slow line. This strategy is suitable for tracking medium- and long-term trends and filtering out market noise effectively.

## Strategy Logic  

This strategy utilizes two Exponential Moving Averages (EMAs) with different periods as the basis for trade decisions. The fast EMA has a period set to 30 to capture short-term price fluctuations. The slow EMA has a period set to 100 to gauge the direction of the mid- to long-term trend.

When the fast EMA crosses the slow EMA from below, it indicates the market is entering an upward trend and generates a buy signal. When the fast EMA crosses below the slow EMA from above, it flags the start of a downward trend and produces a sell signal.   

## Advantage Analysis

The advantages of this strategy include:

1. Uses moving averages as the basis to filter out short-term market noise and follow trends. 
2. Adopts a dual-EMA approach to clearly determine trend directionality.  
3. Allows parameter optimization where fast and slow EMA periods can be customized.
4. Capable of tracking mid- to long-term trends and short-term adjustments.
5. Simple and clear logic, easy to understand and implement, suitable for beginners.  

## Risk Analysis   

Some risks also exist:

1. Prone to false signals when prices move sideways. Can be mitigated by EMA parameter tuning.
2. Ineffective in dealing with extreme price swings. Can set stop loss to control risk.
3. Lagging inherent in MA systems, may miss price reversal points. Can optimize with other indicators.  

## Optimization Directions

Some optimization directions:  

1. Optimize EMA periods to improve profitability. 
2. Add other indicators like trading volume to avoid false breakouts.  
3. Add stop loss strategies to limit downside on single trades. 
4. Incorporate trend strength indicators to avoid trend reversal whipsaws.
5. Introduce parameter optimization for wider adaptability.


## Conclusion  

This strategy builds a trading system based on double EMA crossovers, using fast and slow EMA relationships to determine market trend. Signal generation is simple and clear. It filters some noise and goes along with trends, suitable for medium- to long-term trend trading. There is room for improving universality and efficiency via multi-indicator optimization and risk control.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Fast MA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|30|Fast MA Period|
|v_input_3_close|0|Slow MA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|100|Slow MA Period|
|v_input_5|false|Invert Trade Direction?|
|v_input_6|true|Use Initial Stop Loss?|
|v_input_7|false|Initial Stop Loss Points|
|v_input_8|true|Use Trailing Stop?|
|v_input_9|false|Trail Points|
|v_input_10|false|Use Offset For Trailing Stop?|
|v_input_11|false|Trail Offset Points|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-21 00:00:00
end: 2024-01-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("EMA Strategy v2", shorttitle = "EMA Strategy v2", overlay=true, pyramiding = 3,default_qty_type = strategy.percent_of_equity, default_qty_value = 10)


// === Inputs ===
// short ma
maFastSource   = input(defval = close, title = "Fast MA Source")
maFastLength   = input(defval = 30, title = "Fast MA Period", minval = 1)

// long ma
maSlowSource   = input(defval = close, title = "Slow MA Source")
maSlowLength   = input(defval = 100, title = "Slow MA Period", minval = 1)

// invert trade direction
tradeInvert = input(defval = false, title = "Invert Trade Direction?")
// risk management
useStop     = input(defval = true, title = "Use Initial Stop Loss?")
slPoints    = input(defval = 0, title = "Initial Stop Loss Points", minval = 1)
useTS       = input(defval = true, title = "Use Trailing Stop?")
tslPoints   = input(defval = 0, title = "Trail Points", minval = 1)
useTSO      = input(defval = false, title = "Use Offset For Trailing Stop?")
tslOffset   = input(defval = 0, title = "Trail Offset Points", minval = 1)

// === Vars and Series ===
fastMA = ema(maFastSource, maFastLength)
slowMA = ema(maSlowSource, maSlowLength)

plot(fastMA, color=blue)
plot(slowMA, color=purple)

goLong() => crossover(fastMA, slowMA)
killLong() => crossunder(fastMA, slowMA)
strategy.entry("Buy", strategy.long, when = goLong())
strategy.close("Buy", when = killLong())

// Shorting if using
goShort() => crossunder (fastMA, slowMA)
killShort() => crossover(fastMA, slowMA)
//strategy.entry("Sell", strategy.short, when = goShort())
//strategy.close("Sell", when = killShort())

if (useStop)
    strategy.exit("XLS", from_entry ="Buy", stop = strategy.position_avg_price / 1.08 )
    strategy.exit("XSS", from_entry ="Sell", stop = strategy.position_avg_price * 1.58)
```

> Detail

https://www.fmz.com/strategy/439648

> Last Modified

2024-01-22 17:26:04
