
> Name

Based on SuperTrend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/8cbe23f3675c325a61c2759d6a96ddd1a57e74029e99c45f6dc400936d7101bf.png)
[trans]
## Overview
This strategy uses super-trend indicators to determine price trends and enter long or short positions when the trend changes. This strategy allows adjusting the ATR period and ATR multiplier to optimize parameters. In addition, the strategy also provides the option to change the ATR calculation method, thus producing slightly different results.
The strategy also has built-in backtesting date range settings and the ability to only trade during certain time periods. This is especially useful for day trading stocks. When the time range option is enabled, you can choose to enter the current position immediately at the beginning of the time period, or wait for the trend to change before entering the first order.
The strategy can also set stop loss and take profit levels based on percentages. In most cases, there is no need to set an additional stop loss due to the ATR-based stop loss provided by the super trend itself. Therefore it is possible to optimize the exit mechanism by enabling only the take profit level.
Finally, the strategy features customized alert messages for trade entry and exit, which can be used for automated trading services.
## Strategy Principle
Supertrend strategies operate on the following main principles:
1. Calculate ATR value: You can choose to use SMA calculation or the built-in ATR indicator calculation. The SMA version of the formula is:    
```
    atr2 = sma(tr, Periods) 
    
```

2. Calculate the upper and lower rails: the upper rail is the price minus the product of the ATR multiplier and ATR, and the lower rail is the price plus the product of the ATR multiplier and ATR.    
```
    up = close - (Multiplier * atr)
    dn = close + (Multiplier * atr)
    
```

3. Determine the relationship between price and the upper and lower rails, and calculate the trend direction. When the price crosses the upper rail, the trend is long, and when the price crosses the upper rail, the trend is short.    
```
    trend := trend == -1 and close > dn ? 1 : trend == 1 and close < up ? -1 : trend 
    
```

4. Generate trading signals when the trend changes, such as generating a sell signal when switching from long to short:    
```
    sellSignal = trend == -1 and trend[1] == 1
    
```

5. Filter based on trading signals and other conditions, and choose whether to enter the market.
6. Set stop loss and take profit to lock in profits or avoid risks.
The above are the key points of the super-trend strategy. Combined with parameter optimization, better trading results can be obtained.
## Strategic Advantages
This super trend strategy has the following advantages:
1. The super trend indicator itself can effectively judge the price trend and is a commonly used trailing stop loss tool.
2. The ATR parameters are adjustable and can be optimized to obtain the best parameter combination for different varieties. The SMA calculation method also provides another option.
3. The time range for backtesting and real trading can be set to adapt to the needs of different trading periods.
4. Provide the option to enter the first order immediately or wait for the signal, which can be selected according to the characteristics of the variety.
5. The built-in stop loss and take profit settings can improve the strategy's risk resistance or lock in more profits.
6. Customized trading prompt information can be integrated into automatic or robot trading systems to achieve unattended trading.
## Strategy Risk
This strategy also has some risks:
1. Super trend indicators may produce more false signals and need to be filtered in combination with other indicators.
2. Improper ATR parameters may lead to frequent trading or missing trends. Parameter optimization is required to obtain the best balance.
3. If the stop-loss point is too close, you may exit a favorable position prematurely, and if the stop-loss point is too far, you may not be able to lock in enough profits.
4. If the time range is set improperly, the main trading period may be missed or the margin will be occupied unnecessarily.
The above risks can be solved by appropriately adjusting parameters or adding filtering conditions to improve the stability of the strategy.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Try different ATR cycle parameters to find a suitable balance point. Generally, between 10-20 is ideal.
2. Test different ATR multiplier parameters. Generally, 2-5 is more suitable. You can gradually adjust to find the best value.
3. Try to add other indicators to judge the long and short directions, such as MACD, KD, etc., to filter out false signals.
4. Optimize the stop-loss and take-profit parameters and find the optimal parameter combination. Dynamic stop-profit and stop-loss can be introduced.
5. Test different trading time frame settings. Intraday short-term varieties are suitable for shorter time periods.
6. Try to automatically select contracts and track targets with high liquidity or high volatility.
## Summarize
Overall, this super trend strategy is a relatively common and practical trend following strategy. It has the characteristics of adjustable parameters and efficient trend tracking, but there are also certain risks that need to be avoided. Through parameter optimization and CONDITIONS addition, this strategy can be optimized into a reliable quantitative trading system and obtain stable Alpha.
||

## Overview
This strategy uses the Supertrend indicator to determine price trends and enters long or short positions when the trends change. The strategy allows adjusting the ATR period and multiplier to optimize parameters. It also provides the option to change the ATR calculation method for slightly different results. 

The strategy has built-in backtesting date ranges and the ability to trade only within certain times of the day and close all trades at the end of that timeframe. This is especially useful for day trading stocks. When the timeframe option is enabled, you can choose to enter the current position immediately when the timeframe starts, or wait for a trend change to enter the first position.

The strategy also allows you to specify percentage based stop loss and take profit levels. In most cases, the ATR based stop provided by Supertrend itself makes an additional stop loss unnecessary. So you could enable only take profit to optimize the exit mechanism.

Finally, there are custom alert fields for entry and exit messages to be used with automated trading services. 

## Strategy Logic

The Supertrend strategy is based on the following key principles:

1. Calculate the ATR value: Can choose between SMA calculation or built-in ATR indicator. SMA formula:
    
```
    atr2 = sma(tr, Periods)
    
```

2. Calculate upper and lower bands. Upper band is close minus ATR multiplier times ATR. Lower band is close plus multiplier times ATR.

    
```
    up = close - (Multiplier * atr) 
    dn = close + (Multiplier * atr)
    
```

3. Determine trend direction by comparing price to bands. Uptrend when price crosses above lower band. Downtrend when price crosses below upper band.
    
    
```
    trend := trend == -1 and close > dn ? 1 : trend == 1 and close < up ? -1 : trend
    
```

4. Generate trading signals on trend change, e.g. sell signal when changing from uptrend to downtrend:

    
```
    sellSignal = trend == -1 and trend[1] == 1 
    
```

5. Filter entry based on signals and additional conditions.

6. Use stop loss and take profit to lock in profits or limit risks.

These are the key working principles behind the Supertrend strategy. Combined with parameter optimization, it can produce good trading results.

## Advantages

The Supertrend strategy has several advantages:

1. Supertrend itself effectively identifies trends and is commonly used for trailing stops. 

2. Customizable ATR parameters can be optimized across products for best fit. SMA calculation provides another option.

3. Configurable backtest and live trading time ranges suit different trading sessions.

4. Option to enter first trade immediately or wait for signal caters to different products.

5. Built-in stop loss and take profit helps improve risk management or lock in more profits.

6. Customizable trade alerts for integration with automated trading systems and bots.

## Risks

There are also some risks to consider:

1. Supertrend can produce false signals which need to be filtered with additional conditions.

2. Improper ATR parameters may lead to over-trading or missing trends. Requires optimization for best balance.

3. Stop loss too close may prematurely exit profitable trades. Take profit too loose may leave money on the table. 

4. Poor timeframe configuration can miss trading sessions or tie up margin unnecessarily.

These risks can be addressed through appropriate adjustments to parameters or additional filters to improve robustness.

## Optimization Opportunities

Some ways the strategy can be further optimized:

1. Test different ATR periods to find the right balance, typically 10-20 works well. 

2. Try different ATR multiplier values, generally 2-5 is appropriate, adjust to find optimum.

3. Add filters like MACD, RSI etc. to reduce false signals. 

4. Optimize stop loss and take profit levels for best results. Consider dynamic trailing mechanisms.

5. Test different trading time ranges. Shorter durations suit intraday and high frequency strategies.  

6. Implement auto symbol selection to track high momentum or volatility.

## Conclusion
Overall this is a fairly common and practical trend following strategy. It efficiently tracks trends with customizable parameters, but also has inherent risks to manage. With optimization and additional conditions, it can be refined into a robust quant trading system with consistent alpha.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|ATR Period|
|v_input_2_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_3|3|ATR Multiplier|
|v_input_4|true|Change ATR Calculation Method ?|
|v_input_5|true|Enter First Trade ASAP|
|v_input_6|false|Wait To Enter First Trade|
|v_input_7|timestamp(2021-01-01T00:00:00)|Backtesting Start Date|
|v_input_8|timestamp(2021-12-31T00:00:00)|Backtesting End Date|
|v_input_9||Time Frame To Enter Trades|
|v_input_10|false|Enable Close Trade At End Of Time Frame|
|v_input_11|false|Enable Stop Loss|
|v_input_12|false|Enable Take Profit|
|v_input_13|5|Stop Loss %|
|v_input_14|10|Take Profit %|
|v_input_15||Long Entry message|
|v_input_16||Short Entry message|
|v_input_17||Close Long message|
|v_input_18||Close Short message|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © REV0LUTI0N

//@version=4

// Strategy
strategy("Supertrend Strategy", overlay=true, initial_capital = 10000, default_qty_value = 10000, default_qty_type = strategy.cash)
Periods = input(title="ATR Period", type=input.integer, defval=10)
src = input(hl2, title="Source")
Multiplier = input(title="ATR Multiplier", type=input.float, step=0.1, defval=3.0)
changeATR= input(title="Change ATR Calculation Method ?", type=input.bool, defval=true)
enableentry = input(true, title="Enter First Trade ASAP")
waitentry = input(false, title="Wait To Enter First Trade")

atr2 = sma(tr, Periods)
atr= changeATR ? atr(Periods) : atr2
up=src-(Multiplier*atr)
up1 = nz(up[1],up)
up := close[1] > up1 ? max(up,up1) : up
dn=src+(Multiplier*atr)
dn1 = nz(dn[1], dn)
dn := close[1] < dn1 ? min(dn, dn1) : dn
trend = 1
trend := nz(trend[1], trend)
trend := trend == -1 and close > dn1 ? 1 : trend == 1 and close < up1 ? -1 : trend

upPlot = plot(trend == 1 ? up : na, title="Up Trend", style=plot.style_linebr, linewidth=2, color=color.green)
Long = (trend == 1 ? up : na)
buySignal = trend == 1 and trend[1] == -1

dnPlot = plot(trend == 1 ? na : dn, title="Down Trend", style=plot.style_linebr, linewidth=2, color=color.red)
Short = (trend == 1 ? na : dn)
sellSignal = trend == -1 and trend[1] == 1

// Strategy Backtesting
startDate  = input(timestamp("2021-01-01T00:00:00"), type = input.time, title='Backtesting Start Date')
finishDate = input(timestamp("2021-12-31T00:00:00"), type = input.time, title='Backtesting End Date')

time_cond  = true

//Time Restriction Settings
startendtime = input("", title='Time Frame To Enter Trades')
enableclose = input(false, title='Enable Close Trade At End Of Time Frame')
timetobuy = (time(timeframe.period, startendtime))
timetoclose = na(time(timeframe.period, startendtime))

// Stop Loss & Take Profit % Based
enablesl = input(false, title='Enable Stop Loss')
enabletp = input(false, title='Enable Take Profit')
stopTick = input(5.0, title='Stop Loss %', type=input.float, step=0.1) / 100
takeTick = input(10.0, title='Take Profit %', type=input.float, step=0.1) / 100

longStop = strategy.position_avg_price * (1 - stopTick)
shortStop = strategy.position_avg_price * (1 + stopTick)
shortTake = strategy.position_avg_price * (1 - takeTick)
longTake = strategy.position_avg_price * (1 + takeTick)

plot(strategy.position_size > 0 and enablesl ? longStop : na, style=plot.style_linebr, color=color.red, linewidth=1, title="Long Fixed SL")
plot(strategy.position_size < 0 and enablesl ? shortStop : na, style=plot.style_linebr, color=color.red, linewidth=1, title="Short Fixed SL")
plot(strategy.position_size > 0 and enabletp ? longTake : na, style=plot.style_linebr, color=color.green, linewidth=1, title="Long Take Profit")
plot(strategy.position_size < 0 and enabletp ? shortTake : na, style=plot.style_linebr, color=color.green, linewidth=1, title="Short Take Profit")

// Alert messages
message_enterlong  = input("", title="Long Entry message")
message_entershort = input("", title="Short Entry message")
message_closelong = input("", title="Close Long message")
message_closeshort = input("", title="Close Short message")

// Strategy Execution
if Long and time_cond and timetobuy and enableentry
    strategy.entry("Long", strategy.long, alert_message = message_enterlong)
    
if Short and time_cond and timetobuy and enableentry
    strategy.entry("Short", strategy.short, alert_message = message_entershort)
    
if buySignal and time_cond and timetobuy and waitentry
    strategy.entry("Long", strategy.long, alert_message = message_enterlong)
    
if sellSignal and time_cond and timetobuy and waitentry
    strategy.entry("Short", strategy.short, alert_message = message_entershort)
    
if strategy.position_size > 0 and timetoclose and enableclose
    strategy.close_all(alert_message = message_closelong)
if strategy.position_size < 0 and timetoclose and enableclose
    strategy.close_all(alert_message = message_closeshort)
    
if strategy.position_size > 0 and enablesl and time_cond
    strategy.exit(id="Close Long", stop=longStop, limit=longTake, alert_message = message_closelong)
if strategy.position_size < 0 and enablesl and time_cond
    strategy.exit(id="Close Short", stop=shortStop, limit=shortTake, alert_message = message_closeshort)
    
if strategy.position_size > 0 and enabletp and time_cond
    strategy.exit(id="Close Long", stop=longStop, limit=longTake, alert_message = message_closelong)
if strategy.position_size < 0 and enabletp and time_cond
    strategy.exit(id="Close Short", stop=shortStop, limit=shortTake, alert_message = message_closeshort)





```

> Detail

https://www.fmz.com/strategy/440798

> Last Modified

2024-02-02 11:11:48
