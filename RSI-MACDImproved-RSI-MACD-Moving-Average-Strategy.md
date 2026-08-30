
> Name

Moving Average Golden Cross RSI-MACD Strategy Improved-RSI-MACD-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d659072572f1536b55.png)
[trans]

## Overview
This strategy is a combination strategy that utilizes RSI, MACD, and moving averages. It combines the overbought and oversold signals of RSI, the sensitivity of MACD and the indicator effect of the moving average when judging the time to enter the market.
## Strategy Principle
This strategy mainly judges the following four conditions to decide to enter the market long:
1. The MACD bar is greater than the set long entry parameter;
2. RSI is greater than 50, indicating that it is overbought;
3. The short-term EMA crosses the long-term EMA, forming a golden cross;
4. The closing price crosses the long-term EMA and is higher than the long-term EMA plus the ATR stop loss range.
When the following two exit conditions are met, the strategy will close the position and stop the loss:
1. The MACD bar is smaller than the set stop loss parameter;
2. The short-term EMA breaks below the long-term EMA and forms a dead cross.
In this way, the strategy can stop losses promptly when profits retrace to avoid larger losses.
## Advantage Analysis
The biggest advantage of this strategy lies in the combined use of indicators, which gives full play to the advantages of each indicator, specifically:
1. The application of RSI avoids the loss of transaction costs caused by repeated opening of positions in volatile market conditions.
2. The sensitivity of the MACD bar indicator ensures timely capture of market turning points.
3. The moving average filters out short-term market noise and exerts its indicator effect.
## Risks and Solutions
This strategy mainly has the following two risks:
1. The risk of retracement is high. The biggest risk of trend-based strategies such as moving averages is the large retracement caused by market reversal. Drawbacks can be actively controlled by reducing position size and setting stop losses.
2. Parameter optimization is difficult. Multi-index combination strategy parameter setting and optimization are difficult. Parameter optimization methods such as step method and genetic algorithm can be used to determine the optimal parameters.
## Optimization ideas
This strategy can continue to be optimized from the following aspects:
1. Add additional conditions to further filter out false signals. For example, combine trading volume indicators, volatility indicators, etc.
2. Test the differences in parameter settings of different varieties. Adjust parameters to accommodate more varieties.
3. Optimize the moving average parameter settings. Test the difference in different length parameters.
4. Research using adaptive moving averages. Switch different parameter combinations according to the market environment.

## Summarize
Generally speaking, this strategy is a typical optimized version of the moving average and trend following strategy. It absorbs the advantages of many mainstream indicators such as MACD and RSI, and is unique in judging the timing of market entry and stop loss. In the next step, improvements can be made from parameter optimization, risk control and other aspects to make the strategy parameters more robust and compatible with more varieties, thereby achieving higher stability.
||

# Overview

This is a combination strategy utilizing RSI, MACD and Moving Averages. It incorporates the overbought/oversold signals from RSI, the sensitivity of MACD and the indicator effect of moving averages when determining entry points.  

# Strategy Logic

The strategy mainly judges the following four conditions to decide long entry:

1. MACD histogram is greater than the set long entry level;
2. RSI is above 50, indicating overbought state; 
3. Short period EMA crosses above long period EMA, forming golden cross;
4. Close price breaks through long period EMA and is higher than long period EMA plus ATR stop loss range.

When the following two exit conditions are met, the strategy will close positions to stop loss:

1. MACD histogram is less than the set stop loss level; 
2. Short period EMA crosses below long period EMA, forming dead cross.

Thus the strategy timely stops loss and avoids huge losses when profit taking or retracement.

# Advantage Analysis 

The biggest advantage of this strategy lies in the combination use of indicators, giving full play to the merits of each indicator:

1. The application of RSI avoids the transaction fee loss caused by repeatedly opening positions in range-bound markets.

2. The sensitivity of MACD histogram indicator ensures timely capture of inflection points.

3. Moving averages filter out short-term market noise and give full play to indicator effect.

# Risks & Solutions

The main risks of this strategy include:

1. High retracement risk. The biggest risk of moving average like trend following strategies is large pullback caused by trend reversal. This can be actively controlled by means of position sizing, stop loss etc.

2. Difficulty in parameter optimization. Multi-indicator combined strategies have higher difficulty in parameter setting and optimization. Methods like walk forward, genetic algorithm can be adopted for optimized parameters.


# Enhancement Orientations 

The strategy can be further optimized in the following aspects:

1. Increase additional filters to further avoid false signals, e.g. combine with volume, volatility indicators etc.

2. Test parameter differences fitting more products. Adjust parameters to adapt more varieties. 

3. Optimize moving average parameter settings. Test the differences of various length parameters.

4. Research adaptive moving averages. Switch different parameter sets based on market regimes.


# Conclusion

In conclusion, this strategy is a typical optimized version of moving average and trend following strategy. It absorbs the strengths of mainstream indicators like MACD and RSI in aspects of timing entry and stopping loss. Next steps could be improving from perspectives like parameter optimization and risk control to make the strategy more robust and adaptable to more products, thereby resulting in higher stability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|14|lengthRSI|
|v_input_float_1|0.09|Stop Loss Percentage|
|v_input_float_2|0.15|Take Profit Percentage|
|v_input_2|12|fastlen|
|v_input_3|26|slowlen|
|v_input_4|9|siglen|
|v_input_5|false|Long Entry Level|
|v_input_6|false|Exit Level|
|v_input_7|8|Short EMA Length|
|v_input_8|21|Long EMA Length|
|v_input_float_3|2|atrMultiplier|
|v_input_int_2|20|atrLength|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-29 00:00:00
end: 2024-01-04 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Improved RSI MACD Strategy with Moving Averages", overlay=true)

// Inputs
src = input(close, title="RSI Source")

// RSI Settings
lengthRSI = input.int(14, minval=1)

// Stop Loss Settings
stopLossPct = input.float(0.09, title="Stop Loss Percentage")
takeProfitPct = input.float(0.15, title="Take Profit Percentage")

// MACD Settings
fastlen = input(12)
slowlen = input(26)
siglen = input(9)

// Strategy Settings
longEntry = input(0, title="Long Entry Level")
exitLevel = input(0, title="Exit Level")

// EMA Settings
emaShortLength = input(8, title="Short EMA Length")
emaLongLength = input(21, title="Long EMA Length")

atrMultiplier = input.float(2, title="atrMultiplier")
atrLength = input.int(20, title="atrLength")

// Indicators
rsi1 = ta.rsi(src, lengthRSI)
[macd, signal, hist] = ta.macd(src, fastlen, slowlen, siglen)

// Calculate EMAs
emaShort = ta.ema(src, emaShortLength)
emaLong = ta.ema(src, emaLongLength)

// Calculate ATR
atr = ta.atr(atrLength)

// Variables
var bool canEnterLong = na

// Strategy conditions
longCondition = hist > longEntry and rsi1 > 50 and emaShort > emaLong and close > emaLong + atrMultiplier * atr

// Entries and Exits
if hist < exitLevel and emaShort < emaLong
    canEnterLong := true
    strategy.close("Long")
    
// Store last entry price
var lastEntryPrice = float(na)
var lastEntryPrice2 = float(na)
if longCondition
    strategy.entry("Long", strategy.long)
    canEnterLong := false
    lastEntryPrice := close
if lastEntryPrice < close
    lastEntryPrice := close
// Calculate Stop Loss and Take Profit Levels based on last entry price
stopLossLevel = lastEntryPrice * (1 - stopLossPct)

// Check for stop loss and take profit levels and close position if triggered
if (strategy.position_size > 0)
    last_buy = strategy.opentrades[0]
    if (close < stopLossLevel)
        strategy.close("Long", comment="Stop Loss Triggered")
    if (close * (1 - takeProfitPct) > strategy.opentrades.entry_price(strategy.opentrades - 1) )
        strategy.close("Long", comment="Take Profit Triggered")
```

> Detail

https://www.fmz.com/strategy/437795

> Last Modified

2024-01-05 16:11:23
