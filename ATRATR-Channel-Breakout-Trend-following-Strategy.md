
> Name

Breakout trend strategy based on ATR channel ATR-Channel-Breakout-Trend-following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/02c67d8b8256f02b25ee7ba55efdc9782a87c500b3c471209f3c3a4b6cabca42.png)
[trans]

## Overview
This strategy uses the ATR channel and break theory to step into the trend when it breaks through the channel, which is a trend following strategy. The strategy is simple and easy to understand, using the moving average channel and ATR indicator to determine the trend direction and send trading signals at key points.
## Strategy Principle
This strategy uses high, low, closing prices and ATR indicators to construct upper and lower rails to form an ATR channel. The channel width is determined by the size of the ATR parameter. When the price breaks through the channel, it is judged that the trend has begun, and at this time it enters the long or short direction. The strategy is divided into two levels of trading signals. If the price breaks through one ATR width, it is regarded as the beginning of the trend, and the first buying and selling point is triggered; when the price breaks through two ATR widths, it is regarded as the trend is accelerating, and the second buying and selling point is triggered.
## Advantage Analysis
The main advantages of this strategy are as follows:
1. Use the ATR indicator to construct a channel and consider market volatility, which is better than a simple moving average.
2. Two levels of buying and selling points are set, entry is in batches, and risks are controllable.
3. Break through theory to judge trends and accurately locate key points.
4. The code is streamlined and easy to understand and implement.
## Risk Analysis
The main risks of this strategy are as follows:
1. Judging by a single indicator, when ATR fails, the probability of strategy failure is high.
2. Failure to set up stop loss limits and position management, and insufficient risk control.
3. The effectiveness needs to be verified, and the effect may not be good under real offer conditions.
4. Improper parameters may lead to crossover or over-trading.
## Optimization direction
The directions in which this strategy can be optimized are as follows:
1. Add multiple indicators for filtering and confirmation to prevent misjudgment.
2. Add a stop loss module to strengthen risk control.
3. Increase position control and position management.
4. Add parameter optimization and adjust parameters for different varieties.
5. Reduce transaction frequency and position size, and consider firm offer conditions.
## Summary
The overall framework of this strategy is clear and can be understood and used as a proof-of-concept strategy. However, there is still a certain gap between the real offer and there is a lot of room for optimization. If risk control and transaction frequency control can be further improved, the application prospects of this strategy are better.
||

## Overview
This strategy utilizes the ATR channel and breakout theory to follow trends by entering when the channel is broken. It belongs to trend-following strategies. The strategy is simple and easy to understand, using moving average channels and ATR indicators to determine trend direction and issuing trading signals at key points.  

## Principle  
This strategy constructs upper and lower bands with high, low, close prices and ATR indicator to form an ATR channel. The channel width is determined by the ATR parameter size. When the price breaks through the channel, it is judged as the beginning of a trend, at which points long or short positions are entered. The strategy has two tiers of trading signals. When the price breaks through one ATR width, it is considered as an emerging trend, triggering the first tier of buy/sell points. When the price breaks through two ATR widths, it is considered an accelerating trend, triggering the second tier of buy/sell points.

## Advantage Analysis
The main advantages of this strategy are:
1. Using ATR indicators to construct channels considers market volatility better than simple moving averages. 
2. The two-tier buy/sell points allow staged entry with controllable risks.
3. Breakout theory accurately locates key trend points.  
4. The concise code is easy to understand and implement.

## Risk Analysis
The main risks of this strategy are:  
1. Reliance on a single indicator means high failure probability if ATR fails.
2. Lack of stop loss and position management leads to insufficient risk control.
3. Utility needs verification and may underperform in live trading conditions.
4. Improper parameters may cause whipsaws or overtrading.  

## Optimization Directions
The optimization directions for this strategy include:
1. Adding filters with multiple indicators to prevent misjudgments.
2. Adding stop loss modules to enhance risk control.
3. Adding position control and money management.  
4. Parameter tuning for different products.
5. Reducing trading frequency and position sizing for live trading.

## Summary
The overall framework of this strategy is clear and usable as a proof of concept. But there are gaps from live trading that allow substantial optimizations. If risk controls and trading frequencies can be further improved, the application prospects would be good.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_timeframe_1|60|TimeFrame|
|v_input_int_1|60|ATR length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-03 00:00:00
end: 2024-01-02 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Myhaj_Lito

//@version=5
strategy("Renko Trend Strategy",shorttitle = "RENKO-Trend str.",overlay = true)
TF = input.timeframe(title='TimeFrame', defval="60")
ATRlength = input.int(title="ATR length", defval=60, minval=2, maxval=1000)

HIGH = request.security(syminfo.tickerid, TF, high)
LOW = request.security(syminfo.tickerid, TF, low)
CLOSE = request.security(syminfo.tickerid, TF, close)
ATR = request.security(syminfo.tickerid, TF, ta.atr(ATRlength))


RENKOUP = float(na)
RENKODN = float(na)
H = float(na)
COLOR = color(na)
BUY = int(na)
SELL = int(na)
UP = bool(na)
DN = bool(na)
CHANGE = bool(na)

RENKOUP := na(RENKOUP[1]) ? (HIGH + LOW) / 2 + ATR / 2 : RENKOUP[1]
RENKODN := na(RENKOUP[1]) ? (HIGH + LOW) / 2 - ATR / 2 : RENKODN[1]
H := na(RENKOUP[1]) or na(RENKODN[1]) ? RENKOUP - RENKODN : RENKOUP[1] - RENKODN[1]
COLOR := na(COLOR[1]) ? color.white : COLOR[1]
BUY := na(BUY[1]) ? 0 : BUY[1]
SELL := na(SELL[1]) ? 0 : SELL[1]
UP := false
DN := false
CHANGE := false

// calculating 
if not CHANGE and close >= RENKOUP[1] + H * 2
    CHANGE := true
    UP := true
    RENKOUP := RENKOUP[1] + ATR * 2
    RENKODN := RENKOUP[1] + ATR
    COLOR := color.rgb(0, 255, 170,60)
    SELL := 0
    BUY += 2
    BUY


if not CHANGE and close >= RENKOUP[1] + H
    CHANGE := true
    UP := true
    RENKOUP := RENKOUP[1] + ATR
    RENKODN := RENKOUP[1]
    COLOR := color.rgb(0, 230, 38,60)
    SELL := 0
    BUY += 1
    BUY

if not CHANGE and close <= RENKODN[1] - H * 2
    CHANGE := true
    DN := true
    RENKODN := RENKODN[1] - ATR * 2
    RENKOUP := RENKODN[1] - ATR
    COLOR := color.rgb(255, 92, 43,60)
    BUY := 0
    SELL += 2
    SELL
if not CHANGE and close <= RENKODN[1] - H
    CHANGE := true
    DN := true
    RENKODN := RENKODN[1] - ATR
    RENKOUP := RENKODN[1]
    COLOR := color.rgb(245, 69, 69,60)
    BUY := 0
    SELL += 1
    SELL
//// STRATEGY 
if(UP)
    strategy.entry("Long",strategy.long)
if(DN)
    strategy.entry("Short",strategy.short)


// ploting 

bgcolor(COLOR)

```

> Detail

https://www.fmz.com/strategy/437503

> Last Modified

2024-01-03 11:53:52
