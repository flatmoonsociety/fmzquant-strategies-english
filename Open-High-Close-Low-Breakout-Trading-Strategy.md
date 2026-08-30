
> Name

Open-High-Close-Low-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/cc444d6881c2c2649c858c22dc2611b68ba1a9b692e3a5eb78e48758e8403300.png)
[trans]
## Overview
The open high close buy low trading strategy is a trend following trading strategy. This strategy determines the relationship between the opening price and closing price of the K-line, identifies the short-term trend direction of the price, and builds long and short positions when the trend starts, so as to quickly enter the market and track the trend.
## Strategy Principle
This strategy mainly determines the relationship between the opening price and closing price of the K-line. When the opening price is equal to the lowest price, a long signal is generated; when the opening price is equal to the highest price, a short signal is generated. This can capture short-term price breakthroughs and track trends.
After entering the signal, a fixed amount will be used to open a position immediately. The stop loss level will be set with reference to the ATR indicator to track market fluctuations. The take profit target is the RR proportional part of the distance from the stop loss level to the entry price. When the price touches the stop loss level or the take profit target, the loss or take profit will be stopped in time.
This strategy will also close all positions at a time point set by the user, such as half an hour before the US market closes, to prevent the risk of large overnight fluctuations.
## Advantage Analysis
This strategy has the following advantages:
1. Use the relationship between the opening price and the closing price to determine the trend direction and quickly identify short-term price breakthroughs.
2. The entry signal is simple, clear and easy to implement.
3. Stop loss and profit in time to lock in profits and avoid losses from expanding.
4. Forced liquidation within a specific time period can avoid the risk of overnight fluctuations.
5. There is no need to select specific trading products, and it is suitable for foreign exchange, stocks, cryptocurrency and other markets.
## Risk Analysis
There are also some risks with this strategy:
1. Use ATR to stop loss. Stop loss may occur frequently in volatile market conditions.
2. The characteristics of transaction types and time periods are not considered, and there is a possibility of over-fitting.
3. The fixed take-profit target may not match the market conditions, making it impossible to sustain profits.
4. Improper forced liquidation may miss trend opportunities or incur additional losses.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the stop loss method, use stay stop loss in trending market, use pending stop loss in volatile market, etc.
2. Add filter conditions and combine trend indicators to determine the entry point to avoid false breakthroughs.
3. Dynamically adjust the take-profit position and determine a reasonable take-profit distance based on the degree of market fluctuations.
4. Optimize the closing time and choose the appropriate closing time for different trading types and regions.
## Summarize
The open high close low take trading strategy quickly establishes a position by simply determining the short-term price trend. It has the advantages of simple entry and clear take-profit and stop-loss. But there are also some aspects that can be optimized, such as stop loss methods, signal filtering, etc. Through continuous testing and optimization, the strategy Parameters can be adapted to more market environments and have strong adaptability and profitability.
||

## Overview

The Open High Close Low breakout trading strategy is a trend-following strategy. It identifies the short-term trend direction by checking the relationship between the open and close prices on candlestick charts. When a trend starts, it enters long or short positions to catch the momentum quickly.

## Strategy Logic

The core logic is to check if the open price equals the lowest or highest price of the candlestick. A long signal is triggered when the open price equals the low. A short signal is triggered when the open price equals the high. This aims to catch breakouts that suggest a short-term trend.

Once a signal is triggered, a fixed size position will be opened immediately. The stop loss is set based on the ATR indicator to trail the market volatility. The take profit level is a fixed RR multiple of the stop loss distance from the entry price. When the price hits either the stop loss or take profit, the position will be closed accordingly.

The strategy also flattens all positions at a user-defined daily cutoff time, such as 30 minutes before the US market close. This avoids overnight gap risk. 

## Advantage Analysis 

The main advantages are:

1. Using open/close prices to identify breakout signals fast. 

2. Clear entry signals that are easy to implement.  

3. Timely stop loss and take profit to lock in profits and limit losses.

4. Flatten positions at the daily cutoff to avoid overnight gap risk.

5. Market-neutral, applies to forex, stocks, crypto etc.

## Risk Analysis

Some risks to consider:

1. Frequent stop loss with ATR in choppy markets. 

2. Overfit to specific instruments and sessions without additional filters.

3. Fixed take profit level may underperform in strong trends.

4. Bad timing on flattening positions could miss trends or cause unnecessary losses.

## Improvement Areas

Some ways to further optimize it:

1. Experiment with various stop loss techniques for different market conditions.  

2. Add filters using momentum indicators etc to avoid false signals.

3. Dynamically adjust take profit levels based on market volatility. 

4. Optimize the daily cutoff time for various trading instruments and sessions. 

## Conclusion

The Open High Close Low breakout strategy offers a simple way to trade momentum. Clear entry and exit rules make it easy to implement and manage. But further optimizations on parameters like stop loss, take profit, filters would improve its robustness across more market conditions. Fine-tuned over time via rigorous testing, it has the potential to achieve strong risk-adjusted returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|(?StopLoss settings)ATR Period for placing SL|
|v_input_bool_1|false|(?Stolploss settings)Show SL lines in chart|
|v_input_float_1|2|(?Trade settings)Risk:Reward|
|v_input_int_2|1500|Close all trades, default is 3:00 PM, 1500 hours (integer)|
|v_input_bool_2|true|Markets that never closed (Crypto, Forex, Commodity)|
|v_input_int_3|true|Lot Size|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// Open-High-Low strategy

strategy('Strategy: OLH', shorttitle="OLH", overlay=true)

// Inputs
slAtrLen = input.int(defval=14, title="ATR Period for placing SL", group="StopLoss settings")
showSLLines = input.bool(defval=false, title="Show SL lines in chart", tooltip="Show SL lines also as dotted lines in chart. Note: chart may look untidy.", group="Stolploss settings")
// Trade related
rrRatio = input.float(title='Risk:Reward', step=0.1, defval=2.0, group="Trade settings")
endOfDay = input.int(defval=1500, title="Close all trades, default is 3:00 PM, 1500 hours (integer)", group="Trade settings")
mktAlwaysOn = input.bool(defval=true, title="Markets that never closed (Crypto, Forex, Commodity)", tooltip="Some markers never closes. For those cases, make this checked.", group="Trade settings")
lotSize = input.int(title='Lot Size', step=1, defval=1, group="Trade settings")


// Utils
green(open, close) => close > open ? true : false
red(open, close) => close < open ? true : false
body(open, close) => math.abs(open - close)
lowerwick = green(open, close) ? open - low : close - low
upperwick = green(open, close) ? high - close : high - open
crange = high - low
crangep = high[1] - low[1] // previous candle's candle-range
bullish = close > open ? true : false
bearish = close < open ? true : false


// Trade signals
longCond = barstate.isconfirmed and (open == low)
shortCond = barstate.isconfirmed and (open == high)

// For SL calculation
atr = ta.atr(slAtrLen)
highestHigh = ta.highest(high, 7)
lowestLow = ta.lowest(low, 7)
longStop = showSLLines ? lowestLow - (atr * 1) : na
shortStop = showSLLines ? highestHigh + (atr * 1) : na
plot(longStop, title="Buy SL", color=color.green, style=plot.style_cross)
plot(shortStop, title="Sell SL", color=color.red, style=plot.style_cross)

// Trade execute
h = hour(time('1'), syminfo.timezone)
m = minute(time('1'), syminfo.timezone)
hourVal = h * 100 + m
totalTrades = strategy.opentrades + strategy.closedtrades
if (mktAlwaysOn or (hourVal < endOfDay))
    // Entry
    var float sl = na
    var float target = na
    if (longCond)
        strategy.entry("enter long", strategy.long, lotSize, limit=na, stop=na, comment="Enter Long")
        sl := longStop
        target := close + ((close - longStop) * rrRatio)
        alert('Buy:' + syminfo.ticker + ' ,SL:' + str.tostring(math.floor(sl)) + ', Target:' + str.tostring(target), alert.freq_once_per_bar)
    if (shortCond)
        strategy.entry("enter short", strategy.short, lotSize, limit=na, stop=na, comment="Enter Short")
        sl := shortStop
        target := close - ((shortStop - close) * rrRatio)
        alert('Sell:' + syminfo.ticker + ' ,SL:' + str.tostring(math.floor(sl)) + ', Target:' + str.tostring(target), alert.freq_once_per_bar)

    // Exit: target or SL
    if ((close >= target) or (close <= sl))
        strategy.close("enter long", comment=close < sl ? "Long SL hit" : "Long target hit")
    if ((close <= target) or (close >= sl))
        strategy.close("enter short", comment=close > sl ? "Short SL hit" : "Short target hit")
else if (not mktAlwaysOn)
    // Close all open position at the end if Day
    strategy.close_all(comment = "Close all entries at end of day.")


```

> Detail

https://www.fmz.com/strategy/440817

> Last Modified

2024-02-02 12:03:45
