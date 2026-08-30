
> Name

Gold VWAP-MACD-SMO Trading StrategyGold-VWAP-MACD-SMO-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1b08c88cfd9448585fc.png)

[trans]


## Overview
The Gold VWAP MACD SMO trading strategy is a complete trading strategy designed on the 12-hour time period. It combines the VWAP monthly line, SMO oscillator and MACD indicators to identify trading opportunities in the gold market.
## Strategy Principle
This strategy uses the VWAP monthly line as the primary trend indicator. VWAP represents the average transaction price of the price, and the monthly line means that the time range for calculating VWAP is the past month. If the current closing price is higher than the VWAP monthly line, it means that the trend is currently rising; if the closing price is lower than the VWAP monthly line, it means that the trend is falling.
The SMO oscillator is used to determine the current overbought and oversold conditions. It consists of a long period component and a short period component. When the oscillator is above 0 it indicates an overbought condition, while when it is below 0 it indicates oversold conditions.
The MACD histogram can determine the direction of momentum. When the bar breaks upward, it means the momentum is getting stronger and you can go long; when the bar breaks down, it means the momentum is getting weaker and you should consider going short.
Based on these three indicators, specific rules for the trading strategy can be established:
Long entry: go long when the closing price is higher than the VWAP monthly line, the MACD histogram breaks through upward, and the SMO oscillator is above 0
Short entry: short when the closing price is below the VWAP monthly line, the MACD histogram breaks down, and the SMO oscillator is below 0
Take Profit and Stop Loss are set based on the entered percentage.
## Advantage Analysis
This strategy combines multiple time frames and indicators to effectively determine the direction and strength of the trend, and has the following advantages:
1. The VWAP monthly line can determine the main trend direction and avoid counter-trend operations.
2. MACD histogram can capture momentum changes in time
3. The SMO oscillator determines overbought and oversold conditions, helping to enter the market in areas that are prone to turning points.
4. Multiple indicator combinations can verify each other and improve signal reliability
5. Customizable take-profit and stop-loss ratios to control risks
## Risk Analysis
Although this strategy is well designed, there are still certain risks that need to be noted:
1. The VWAP indicator is sensitive to cross movements and may produce false signals.
2. Improper setting of MACD parameters, leading to increased probability of false breakthroughs
3. Improper SMO parameters may also lead to misjudgment of overbought and oversold areas.
4. The stop-profit and stop-loss settings are too loose and cannot effectively control a single loss.
In order to control the above risks, the parameters of VWAP and MACD should be reasonably optimized, and the range should not be too large. At the same time, the take-profit and stop-loss ratio should not be too large, and a single loss should be controlled to about 3%.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Increase volume and price confirmation, for example, trading volume breaks through the moving average
2. Combined with volatility indicators such as ATR, adjust positions according to market volatility
3. Add a batch lighten mechanism at a high level to prevent missed profits
4. Test different take profit and stop loss strategies, such as trailing stop loss, chain stop loss, etc.
5. Add model verification module to filter abnormal signals
## Summarize
The gold VWAP MACD SMO strategy combines multiple indicators to determine trends and overbought and oversold conditions, which can effectively seize gold's medium and long-term opportunities. Although there are certain risks, they can be controlled through parameter optimization and risk control methods. This strategy has very strong scalability and can be modularized and optimized according to actual needs. It is a trading system worthy of long-term tracking.
||


## Overview

The Gold VWAP MACD SMO trading strategy is a complete strategy designed for the gold market using a 12-hour timeframe chart. It combines VWAP monthly, SMO oscillator and MACD histogram to identify trading opportunities in the gold market. 

## Strategy Logic

The strategy uses VWAP monthly as the main trend indicator. VWAP represents the average transaction price, and monthly means the time range for calculating VWAP is the past month. If the current close is above the VWAP monthly, it indicates the current uptrend; if the close is below the VWAP monthly, it means the trend is down.

The SMO oscillator is used to determine the current overbought and oversold situation. It consists of a long cycle component and a short cycle component. When the oscillator is above 0, it indicates overbought conditions, and when below 0, it represents oversold.

The MACD histogram can determine the momentum direction. When the column breaks up, it represents the momentum is strengthening for going long; when the column breaks down, it means the momentum is weakening to consider going short.

According to these three indicators, the specific rules of the trading strategy can be established:

Long entry: when close is above VWAP monthly, MACD histogram breaks up, and SMO oscillator is above 0.
Short entry: when close is below VWAP monthly, MACD histogram breaks down, and SMO oscillator is below 0.

Take profit and stop loss are set based on the input percentages.

## Advantage Analysis 

The strategy combines multiple timeframes and indicators to effectively determine the trend direction and strength, with the following advantages:

1. VWAP monthly can determine the primary trend direction to avoid counter trend trading.
2. MACD histogram can capture momentum changes in a timely manner. 
3. SMO oscillator judges overbought and oversold conditions, which is helpful to enter at potential reversal points.
4. Multiple indicators combination can verify each other and improve signal reliability.
5. Customizable take profit and stop loss percentages to control risks.

## Risk Analysis

Although the strategy is designed reasonably, there are still some risks to note:

1. VWAP is sensitive to whipsaws, which may generate wrong signals.
2. Improper MACD parameters setting increases the probability of false breakouts.
3. Improper SMO parameters may also lead to misjudgement of overbought and oversold zones. 
4. Excessive wide take profit and stop loss settings cannot effectively control single loss.

To control the above risks, VWAP and MACD parameters should be optimized reasonably without too wide ranges. Also, take profit and stop loss percentages should not be too high, and single loss should be controlled around 3%.

## Optimization Directions

The strategy can also be optimized in the following aspects:

1. Add volume confirmation, such as volume breakout of MA.
2. Incorporate volatility indicators like ATR to adjust position sizing based on market volatility.
3. Add lighten mechanism at high levels to avoid missing profits.
4. Test different take profit and stop loss strategies, like trailing stop loss, adaptive stop loss etc.
5. Add model verification module to filter abnormal signals.

## Conclusion

The Gold VWAP MACD SMO strategy combines multiple indicators to determine the trend and overbought/oversold conditions, which can effectively capture medium-to-long term opportunities in gold. Although there are some risks, they can be controlled through parameter optimization and risk management. The strategy has very strong scalability and can be optimized modularly based on actual needs. It is a trading system worthy of long-term tracking.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_low|0|source: low|high|close|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|12|Fast Length|
|v_input_3|26|Slow Length|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|9|Signal Smoothing|
|v_input_6|22|Long Length SMO|
|v_input_7|6|Short Length SMO|
|v_input_8|5|Signal Line Length SMO|
|v_input_9|0.085|Take profit % for long|
|v_input_10|0.03|Stop loss % for long|
|v_input_11|0.05|Take profit % for short|
|v_input_12|0.025|Stop loss % for short|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-19 00:00:00
end: 2023-10-19 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=4
// strategy("VWAP Gold strategy", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 10000, calc_on_every_tick = true, commission_type = strategy.commission.percent, commission_value = 0.005)


source = input(low)


//vwap monthly
timeframeM = time("M")
beginningM = na(timeframeM[1]) or timeframeM > timeframeM[1]

sumsourceM = source * volume
sumVolM = volume
sumsourceM := beginningM ? sumsourceM : sumsourceM + sumsourceM[1]
sumVolM := beginningM ? sumVolM : sumVolM + sumVolM[1]
vwapMonthly= sumsourceM / sumVolM

//macd
fast_length = input(title="Fast Length", type=input.integer, defval=12)
slow_length = input(title="Slow Length", type=input.integer, defval=26)
src = input(title="Source", type=input.source, defval=close)
signal_length = input(title="Signal Smoothing", type=input.integer, minval = 1, maxval = 50, defval = 9)


fast_ma = ema(src, fast_length)
slow_ma = ema(src, slow_length)
macd = fast_ma - slow_ma
signal =  ema(macd, signal_length)
hist = macd - signal


//SMO
longlen = input(22, minval=1, title="Long Length SMO")
shortlen = input(6, minval=1, title="Short Length SMO")
siglen = input(5, minval=1, title="Signal Line Length SMO")
erg = tsi(close, shortlen, longlen)
sig = ema(erg, siglen)
osc = erg - sig


shortCondition =  close < vwapMonthly and hist < hist[1] and osc < 0
longCondition =  close > vwapMonthly and hist> hist[1] and osc > 0

tplong=input(0.085, step=0.005, title="Take profit % for long")
sllong=input(0.03, step=0.005, title="Stop loss % for long")
tpshort=input(0.05, step=0.005, title="Take profit % for short")
slshort=input(0.025, step=0.005, title="Stop loss % for short")

strategy.entry("long",1,when=longCondition)
strategy.entry("short",0,when=shortCondition)

strategy.exit("short_tp/sl", "long", profit=close * tplong / syminfo.mintick, loss=close * sllong / syminfo.mintick, comment='LONG EXIT',  alert_message = 'closeshort')
strategy.exit("short_tp/sl", "short", profit=close * tpshort / syminfo.mintick, loss=close * slshort / syminfo.mintick, comment='SHORT EXIT',  alert_message = 'closeshort')



```

> Detail

https://www.fmz.com/strategy/429773

> Last Modified

2023-10-20 16:23:33
