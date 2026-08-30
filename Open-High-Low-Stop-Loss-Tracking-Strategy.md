
> Name

Open-High-Low-Stop-Loss-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/110de81942aa476240a.png)
[trans]
### Overview
This strategy is based on the K-line's opening high and low data to design Entries to find the reversal point of the trend. After Entries, the stop loss line will be set based on the ATR indicator and the stop loss will be tracked. The strategy will also calculate the Target level based on the risk-return ratio, and close the position after reaching the Target or being stopped.
### Strategy Principles
The Entries signal for this strategy comes from opening highs and lows. When the opening price of a certain K line is equal to the lowest price, a buy signal is generated, and when the opening price is equal to the highest price, a sell signal is generated, indicating that there may be a trend reversal opportunity.
After Entries, dynamic trailing stop loss will be calculated based on the ATR indicator. The stop-loss line after buying is the lowest price within the recent N K lines minus 1 times ATR; the stop-loss line after selling is the highest price within the recent N K lines plus 1 times ATR. The stop loss line will be dynamically updated to track the price movement.
The target profit is calculated based on the set risk-reward ratio. The buying target price is the Entry price plus (the risk-reward ratio multiple of the difference between the Entry price and the stop-loss price); the selling target price is the Entry price minus (the risk-reward ratio multiple of the difference between the stop-loss price and the Entry price).
When the price reaches the stop loss price or target price, a closing order is issued.
### Advantage Analysis
This strategy has the following advantages:
1. The Entries signal is simple and clear, easy to judge, and avoids multiple shocks.
2. Dynamic ATR stop loss, lock in profits to the greatest extent, and avoid chasing highs and killing lows.
3. Risk-return control to avoid profit legacy and ultra-short-term operations.
4. Suitable for different varieties and easy to optimize.
### Risk Analysis
This strategy also has certain risks:
1. The Entries signal may lag to a certain extent and miss the best point of the market.
2. If the stop loss price is too close or too loose, you may be trapped or lose profits.
3. There is no trend judgment module and it is easy to be trapped in the volatile market.
4. Unable to handle the situation of opening a position overnight.
Corresponding optimization direction:
1. Combine with other indicators to determine trends and avoid arbitrage in volatile market conditions.
2. Adjust ATR parameters or add volatility control to optimize the stop loss level.
3. Add trend judgment or filtering module to reduce the error of Entries signal.
4. Add the overnight processing module to process overnight positions of specific varieties.
### Summarize
Generally speaking, this strategy is relatively simple and direct, with clear Entries signals, reasonable stop loss ideas, and adequate risk control. However, there are also certain limitations, such as insufficient trend judgment and signal lag. These issues also provide directions for future optimization. By combining more indicator judgments and risk control modules, the strategy can further enhance its effect and become more versatile.
||

### Overview

This strategy is designed based on the open, high and low data of candlestick charts to identify trend reversal points for entries. After entries, stop loss lines will be set based on the ATR indicator and tracked. Targets will also be calculated based on the risk-reward ratio. When price hits either the stop loss or profit target, orders will be sent to close positions.

### Strategy Logic

The entry signals of this strategy come from the open, high and low prices. A buy signal is generated when the opening price equals the low of the candlestick, and a sell signal is generated when the opening price equals the high, indicating potential trend reversal opportunities.

After entry, dynamic trailing stop loss is calculated based on the ATR indicator. The long stop loss is set at the lowest low of recent N bars minus 1 ATR; the short stop loss is set at the highest high of recent N bars plus 1 ATR. The stop loss line will update dynamically to trail price moves.

Profit targets are calculated based on the risk-reward ratio setting. The long target is set at the entry price plus (the risk difference between entry price and stop loss multiplied by the risk-reward ratio); the short target is set at the entry price minus (the risk difference between stop loss and entry price multiplied by the risk-reward ratio).

When price hits either the stop loss or profit target, orders will be sent to flatten positions.

### Advantage Analysis 

The advantages of this strategy include:

1. Simple and clear entry signals, avoiding multiple whipsaws. 

2. Dynamic ATR trailing stop locks in profits and prevents chasing highs and lows.

3. Risk-reward ratio control avoids leaving profits on table and over-trading.

4. Applicable to different products, easy to optimize.

### Risk Analysis

There are also some risks of this strategy:

1. Entry signals may lag to some extent, missing best market entry.

2. Stop loss too tight or too loose, causing unnecessary stop loss or missing profits. 

3. No trend determination, prone to being trapped in ranging markets.

4. Unable to handle overnight positions.

The optimization directions are:

1. Incorporate other indicators for trend bias to avoid whipsaws.  

2. Fine tune ATR parameters or add volatility control for better stop loss.

3. Add trend filtering to reduce signal noise.

4. Add overnight position handling for certain products. 

### Conclusion

In conclusion, this is a simple and straightforward strategy with clear entry logic, reasonable stop loss methodology and good risk control. But there are some limitations like insufficient trend bias, signal lagging etc. These flaws also point out directions for future optimization. By incorporating more indicators filters and risk management modules, this strategy can be further enhanced and made more robust.
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

strategy('Strategy: OLH', shorttitle="OLH", overlay=true )

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

https://www.fmz.com/strategy/441989

> Last Modified

2024-02-18 14:30:08
