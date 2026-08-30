
> Name

Parabolic-Period-and-Bollinger-Band-Combined-Moving-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/20aebdfdb4a0d59f3f7.png)
[trans]
### Overview
This article will introduce a quantitative trading strategy that combines the Pablo Cycle indicator and the Bollinger Band indicator to set a moving stop loss strategy. This strategy determines the market trend direction by calculating the Pablo Bel cycle line, and then uses the upper and lower rails of Bollinger Bands to dynamically set stop loss levels, thereby achieving moving stop loss to lock in profits.
### Strategy Principles
First, this strategy uses the Parobe indicator to determine current market trends. When today's closing price crosses yesterday's Parobel cycle line, the market is considered bullish and you can go long; when today's closing price falls below yesterday's cycle line, the market is bearish and you can go short.
Secondly, this strategy combines the Bollinger Bands indicator to set dynamic stop loss levels. The upper track in Bollinger Bands can be regarded as the overbought zone, and the lower track is the oversold zone. After going long, if the price falls below the lower Bollinger Band again, stop loss and close the position; after going short, if the price rises below the upper track again, stop loss and exit. In this way, the upper and lower rails of the Bollinger Bands become moving stop loss lines.
Through the above principles, this strategy not only determines the market direction, but also sets up a dynamic stop-loss mechanism to track profits. This allows it to capture part of the rise and fall in the general trend, and at the same time, it can lock in profits and avoid risks through stop loss.
### Strategic Advantages
Compared with the traditional stop-loss strategy that only sets a fixed stop-loss level, this strategy uses the Bollinger Band indicator as the stop-loss line, so that the stop-loss line can move with price fluctuations. This allows it to lock in more profits in larger market conditions. In addition, compared to using the Parobel cycle line alone, this strategy adds the Bollinger Bands indicator to determine overbought and oversold areas, which can be more accurate.
### Risks and Solutions
The main risk of this strategy is that the trend judged by the Parobe indicator is not strong. In a volatile market, the price may cross the Parobel cycle line up and down multiple times, causing the strategy to produce frequent but low-profit transactions. At this time, transaction fees and slippage costs may account for a larger proportion, reducing the profitability of the strategy.
In order to deal with the above risks, you can consider adjusting parameters to increase the degree of change of the Parobel periodic line and reduce the probability of misjudgment; or combine other indicators to filter entry opportunities. For example, oscillators can be added to determine whether the market is trending or oscillating to reduce unnecessary transactions.
### Strategy optimization
This strategy can be optimized from the following aspects:
1. Optimize the Parobel indicator parameters, adjust the change speed of parameter indicators, and reduce the probability of misjudgment
2. Add other technical indicator filters, such as adding MACD, KD, etc. to determine the market type and avoid arbitrage that may shock the market.
3. Optimize Bollinger Band parameters and adjust bandwidth parameters to make Bollinger Bands closer to price changes
4. Increase volume energy indicators, such as trading volume, positions, etc. to assist judgment and avoid false breakthroughs
5. Combine with stock fundamental information to avoid problems that may affect the performance of strategic holdings
### Summarize
This strategy uses the Parobel indicator to determine the direction and strength of the market trend, and then uses the upper and lower Bollinger Bands as moving stop positions to set stop-loss strategies, achieving a combination of trend tracking and risk control. Compared with the traditional fixed stop loss strategy, this strategy can obtain higher returns in larger market conditions. By optimizing parameters and adding other auxiliary judgment indicators, the stability of the strategy can be further enhanced and unnecessary transactions can be reduced.
||

### Overview  

This article will introduce a quantitative trading strategy that combines the parabolic period indicator and the Bollinger band indicator to set a moving stop loss strategy. By calculating the parabolic period line to judge the market trend direction, and then using the upper and lower rails of the Bollinger bands to dynamically set the stop loss position, the strategy realizes moving stop loss to lock in profits.

### Strategy Principle

Firstly, this strategy uses the parabolic indicator to judge the current market trend. When today's closing price crosses above yesterday's parabolic period line, it is considered that the market has reversed to bullish and can go long; when today's closing price crosses below the period line, the market outlook is bearish and can go short.

Secondly, this strategy combines the Bollinger Band indicator to set a dynamic stop loss position. The upper rail of the Bollinger Band can be seen as an overbought zone, and the lower rail is an oversold zone. After going long, if the price falls back below the lower rail of the Bollinger Band, stop loss to close position; after going short, if the price rises above the upper rail again, stop loss to exit. Thus, the upper and lower rails of Bollinger Bands become moving stop loss lines.  

Through the above principles, this strategy realizes judging the market direction while setting a dynamic stop loss mechanism to track profits. This allows it to capture some ups and downs in major trends, while also being able to lock in profits through stop losses to avoid risks.


### Advantages of the Strategy  

Compared with traditional stop loss strategies that only set one fixed stop loss position, this strategy uses the Bollinger band indicator as the stop loss line, so that the stop loss line can move with price fluctuations. This allows it to lock in more profits in relatively large moves. In addition, compared to using the parabolic period line alone, this strategy adds the Bollinger band indicator to determine overbought and oversold areas, which can be more accurate.

### Risks and Solutions   

The main risk of this strategy is that the trending of the parabolic indicator is not strong. In oscillating markets, prices may cross parabolic period lines several times, causing frequent but small profitable trades for the strategy. At this point, transaction fees and slippage costs may account for a large proportion and reduce the profitability of the strategy.   

To cope with the above risks, parameters can be adjusted to increase the degree of change in the parabolic period line to reduce misjudgment probability; or consider combining other indicators to filter entry timing. For example, volatility indicators can be added to determine if the market is trending or oscillating in order to reduce unnecessary trades.  

### Strategy Optimization

This strategy can be optimized in the following aspects:  

1. Optimize parabolic indicator parameters to adjust indicator change rate to reduce misjudgment probability  

2. Increase other technical indicators filtering, such as adding MACD, KD to determine market type, avoid arbitrage in oscillating market  

3. Optimize Bollinger Band parameters to adjust bandwidth parameters to make Bollinger Bands stick closer to price changes  

4. Increase volume indicators, such as trading volume, positions to assist in judging to avoid false breakouts  

5. Combine fundamentals of stocks to avoid problems with earnings of stocks strategy holding  

### Summary  

This strategy combines judging market trend direction and strength with parabolic indicator, and then uses the upper and lower rails of Bollinger Bands as the moving stop loss position to set a stop loss strategy, achieving a combination of trend tracking and risk control. Compared with traditional fixed stop loss strategies, this strategy can achieve higher returns in larger moves. By optimizing parameters and adding other auxiliary judgment indicators, the stability of the strategy can be further enhanced and unnecessary trades reduced.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|true|(?Backtest Time Period)Filter Date Range of Backtest|
|v_input_1|timestamp(5 June 2022)|Start Date|
|v_input_2|timestamp(5 July 2022)|End Date|
|v_input_int_1|10|(?number of past candles)Swing High|
|v_input_int_2|10|Swing Low|
|v_input_int_3|200|(?EMA)Ema Period|
|v_input_int_4|14|(?RSI)RSI Period|
|v_input_3|0.02|(?Parabolic SAR)start|
|v_input_4|0.02|increment|
|v_input_5|0.2|Max Value|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-02 00:00:00
end: 2024-02-01 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © maxencetajet

//@version=5
strategy("HA_RSI", overlay=true, initial_capital=1000, default_qty_type=strategy.fixed, default_qty_value=0.5, slippage=25)

closeHA = request.security(ticker.heikinashi(syminfo.tickerid), timeframe.period, close)

useDateFilter = input.bool(true, title="Filter Date Range of Backtest",
     group="Backtest Time Period")
backtestStartDate = input(timestamp("5 June 2022"), 
     title="Start Date", group="Backtest Time Period",
     tooltip="This start date is in the time zone of the exchange " + 
     "where the chart's instrument trades. It doesn't use the time " + 
     "zone of the chart or of your computer.")
backtestEndDate = input(timestamp("5 July 2022"),
     title="End Date", group="Backtest Time Period",
     tooltip="This end date is in the time zone of the exchange " + 
     "where the chart's instrument trades. It doesn't use the time " + 
     "zone of the chart or of your computer.")

inTradeWindow = true

swingHighV = input.int(10, title="Swing High", group="number of past candles")
swingLowV = input.int(10, title="Swing Low", group="number of past candles")

emaV = input.int(200, title="Ema Period", group="EMA")

rsiV = input.int(14, title="RSI Period", group="RSI")

start = input(0.02, group="Parabolic SAR")
increment = input(0.02, group="Parabolic SAR")
maximum = input(0.2, "Max Value", group="Parabolic SAR")

ema = ta.ema(closeHA, emaV)
rsi = ta.rsi(closeHA, rsiV)
SAR = ta.sar(start, increment, maximum)

myColor = SAR < low?color.green:color.red

longcondition = closeHA > ema and rsi > 50 and closeHA[1] > SAR and closeHA[1] < SAR[1] 
shortcondition = closeHA < ema and rsi < 50 and closeHA[1] < SAR and closeHA[1] > SAR[1]

float risk_long = na
float risk_short = na
float stopLoss = na
float entry_price = na
float takeProfit = na

risk_long := risk_long[1]
risk_short := risk_short[1]

swingHigh = ta.highest(closeHA, swingHighV)
swingLow = ta.lowest(closeHA, swingLowV)

if strategy.position_size == 0 and longcondition and inTradeWindow
    risk_long := (close - swingLow) / close
    strategy.entry("long", strategy.long, comment="Buy")
    
if strategy.position_size == 0 and shortcondition and inTradeWindow
    risk_short := (swingHigh - close) / close       
    strategy.entry("short", strategy.short, comment="Sell")
    
if strategy.position_size > 0

    stopLoss := strategy.position_avg_price * (1 - risk_long)
    entry_price := strategy.position_avg_price
    strategy.exit("long exit", "long", stop = stopLoss)
    
if strategy.position_size < 0 

    stopLoss := strategy.position_avg_price * (1 + risk_short)
    entry_price := strategy.position_avg_price
    strategy.exit("short exit", "short", stop = stopLoss)

if closeHA[1] < SAR and close > strategy.position_avg_price
    strategy.close("long", comment="Exit Long")
    
if closeHA[1] > SAR and close < strategy.position_avg_price
    strategy.close("short", comment="Exit Short")

p_ep = plot(entry_price, color=color.new(color.white, 0), linewidth=2, style=plot.style_linebr, title='entry price')
p_sl = plot(stopLoss, color=color.new(color.red, 0), linewidth=2, style=plot.style_linebr, title='stopLoss')
fill(p_sl, p_ep, color.new(color.red, transp=85))

plot(SAR, "ParabolicSAR", style=plot.style_circles, color=myColor, linewidth=1)
plot(ema, color=color.white, linewidth=2, title="EMA")
```

> Detail

https://www.fmz.com/strategy/440797

> Last Modified

2024-02-02 11:05:57
