
> Name

Golden Channel Reversal Strategy Fibonacci-Retracement-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7dab7124fd10109c08a8a658558d73441e06996d0bf30d5928ee86030a283f89.png)
[trans]


## Overview
The Golden Channel Reversal Strategy is a quantitative trading strategy based on the Golden Section and the Relative Strength Index (RSI). This strategy combines the golden channel theory and overbought and oversold indicators to perform reversal operations under the general cycle trend in order to make profits in a short cycle.
## Strategy Principle
The strategy first calculates two important price areas of the golden section, namely 0.618 times the high and 0.618 times the low. When price approaches these two areas, we believe a price reversal is likely.
In addition, the strategy also calculates the RSI indicator to determine overbought and oversold conditions. When the RSI is below 30, it is oversold, and when it is above 70, it is overbought. These two states also mean that price may reverse.
Combining these two conditions, the strategy determines that the buying conditions are: the closing price goes above 0.618 times the low and the RSI index is lower than 30; the selling conditions are: the closing price goes below 0.618 times the high and the RSI index is higher than 70.
When the buy signal is triggered, the strategy will open a long position at the market price at that point; when the sell signal is triggered, the strategy will open a short position at the market price at that point. In addition, the strategy will also set take-profit and stop-loss levels. When the price moves in a favorable direction to a certain proportion, the profit will be taken. When the price moves in an unfavorable direction to a certain proportion, the loss will be stopped.
## Strategic advantage analysis
This strategy combines trend and reversal factors, taking into account large-cycle trends and taking advantage of short-cycle reversals to make profits. Has the following advantages:
1. The golden section has natural support and resistance attributes and is an effective tool for judging key price areas.
2. The RSI indicator determines overbought and oversold conditions and indicates possible reversal points.
3. The long and short signals are clear and the reversal opportunity will not be missed.
4. Set up a stop-profit and stop-loss strategy to control risks.
## Strategy risk analysis
This strategy also has some risks that need to be guarded against:
1. If the big cycle does not reverse, a short-cycle rebound will cause the risk of loss. It can be avoided by amplifying the cycle to determine the trend of the large cycle.
2. When the reversal does not occur, the stop loss may be triggered, resulting in losses. The stop loss range can be appropriately relaxed.
3. The reversal time may take a long time and requires sufficient financial support.
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Collect more historical data, test and optimize key parameters such as the range of the golden section and the overbought and oversold lines of RSI to make it more consistent with the real market.
2. Add other indicator judgments to form stronger trading signals. Such as K-line shape, trading volume changes, etc.
3. Adjust parameters or optimize rules according to the characteristics of different trading varieties.
4. Add an automatic stop loss strategy and track real-time price changes to determine the stop loss position.
## Summarize
The golden channel reversal strategy combines trend factors and reversal factors to make short-term profits while controlling risks. It is a quantitative strategy worth recommending. Optimization can lead to better returns.
||  


## Overview  

The Fibonacci Retracement Reversal strategy is a quantitative trading strategy based on Fibonacci retracement levels and the Relative Strength Index (RSI) indicator. This strategy combines the Fibonacci channel theory and overbought/oversold indicator to make reversal trades against the major trend in order to profit in the short-term cycles.  

## Strategy Logic  

The strategy first calculates two important price zones based on the 0.618 Fibonacci levels - the 0.618 times high point and 0.618 times low point. When prices approach these areas, we believe a reversal may occur.

In addition, the strategy also uses the RSI indicator to determine overbought/oversold conditions. RSI below 30 indicates oversold status while RSI above 70 suggests overbought condition. These also imply potential price reversals.

Combining the two conditions, the buy signal is triggered when: close breaks above the 0.618 times low point AND RSI is below 30; the sell signal triggers when: close breaks below the 0.618 times high point AND RSI goes over 70. 

Upon buy signal, the strategy will long at market price. Upon sell signal, it will short at market price. Also, take profit and stop loss levels are set so that the position will be closed when price moves favorably by certain percentage (take profit) or moves adversely by certain percentage (stop loss).

## Pros  

The strategy combines both trend and reversal scenarios, taking into account major trend while profiting from short-term retracement. The main advantages are:

1. Fibonacci levels have inherent support/resistance attributes, serving as effective price zone indicator.  
2. RSI overbought/oversold status suggests potential turning points.
3. Long/short signals are clear, catching reversal chances.  
4. Take profit/stop loss controls risk.

## Risks 

There are some risks to be awared of:

1. Losses may occur if no major trend reversal happens despite short-term bounces. Larger timeframe analysis can help avoid this.  
2. Stop loss may be triggered before reversal happens. Wider stop loss zone could help.
3. Reversals may sustain for long time, requiring sufficient capital support.

## Optimization  

The strategy can be further optimized by:

1. Collect more historical data to test and tune key parameters like Fibonacci zone range and RSI overbought/oversold lines for better fit to real market.

2. Incorporate more indicators to generate stronger signals, like candlestick patterns, volume changes etc.  

3. Adjust parameters or rules according to different trading instruments' characteristics.

4. Add dynamic stop loss mechanism to trail price real-time.

## Conclusion  

The Fibonacci Retracement Reversal strategy balances trend and reversal scenarios to profit in short-term while controlling risks. Further optimizations may lead to greater returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.618|Fibonacci Düzeltme Seviyesi|
|v_input_2|14|RSI Periyodu|
|v_input_3|70|RSI Satış Sinyali Seviyesi|
|v_input_4|30|RSI Alış Sinyali Seviyesi|
|v_input_5|true|Take Profit Yüzdesi|
|v_input_6|true|Stop Loss Yüzdesi|
|v_input_7|27|Fibonacci Destek Seviyesi|
|v_input_8|200|Direnç Seviyesi|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-06 00:00:00
end: 2023-12-06 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("FBS Trade", overlay=true)

// Fibonacci seviyeleri
fibonacciLevels = input(0.618, title="Fibonacci Düzeltme Seviyesi")

// RSI ayarları
rsiLength = input(14, title="RSI Periyodu")
overboughtLevel = input(70, title="RSI Satış Sinyali Seviyesi")
oversoldLevel = input(30, title="RSI Alış Sinyali Seviyesi")

// Take Profit ve Stop Loss yüzdesi
takeProfitPercent = input(1, title="Take Profit Yüzdesi") / 100
stopLossPercent = input(1, title="Stop Loss Yüzdesi") / 100

// Fibonacci seviyelerini hesapla
highFibo = high * (1 + fibonacciLevels)
lowFibo = low * (1 - fibonacciLevels)

// RSI hesaplama
rsiValue = ta.rsi(close, rsiLength)

// Alış ve satış koşulları
buyCondition = close > lowFibo and rsiValue < 30
sellCondition = close < highFibo and rsiValue > overboughtLevel

// Take Profit ve Stop Loss seviyeleri
takeProfitLong = strategy.position_avg_price * (1 + takeProfitPercent)
stopLossLong = strategy.position_avg_price * (1 - stopLossPercent)

takeProfitShort = strategy.position_avg_price * (1 - takeProfitPercent)
stopLossShort = strategy.position_avg_price * (1 + stopLossPercent)

// Alış ve satış işlemleri
if (buyCondition)
    strategy.entry("Buy", strategy.long)
if (sellCondition)
    strategy.entry("Sell", strategy.short)

// Take Profit ve Stop Loss seviyeleri
if (strategy.position_size > 0)
    strategy.exit("Take Profit/Close Buy", from_entry="Buy", limit=takeProfitLong, stop=stopLossLong)
if (strategy.position_size < 0)
    strategy.exit("Take Profit/Close Sell", from_entry="Sell", limit=takeProfitShort, stop=stopLossShort)

// Sadece mumları ve buy/sell işlemlerini göster
plot(close, color=color.black, title="Close")

// Destek ve direnç bölgeleri
supportLevel = input(27, title="Fibonacci Destek Seviyesi")
resistanceLevel = input(200, title="Direnç Seviyesi")

hline(supportLevel, "Fibonacci Destek Seviyesi", color=color.green)
hline(resistanceLevel, "Direnç Seviyesi", color=color.red)

// Trend çizgileri
var line trendLine = na
if (ta.crossover(close, highFibo))
    trendLine := line.new(bar_index[1], highFibo[1], bar_index, highFibo, color=color.green, width=2)
if (ta.crossunder(close, lowFibo))
    trendLine := line.new(bar_index[1], lowFibo[1], bar_index, lowFibo, color=color.red, width=2)

// RSI ve Fibo'yu grafiğe çizme
hline(overboughtLevel, "RSI Satış Sinyali", color=color.red, linestyle=hline.style_dashed)
hline(oversoldLevel, "RSI Alış Sinyali", color=color.green, linestyle=hline.style_dashed)
plot(rsiValue, color=color.purple, title="RSI")

// 15 dakikalıkta 3 mumda bir alarm
is15MinBar = ta.change(time('15'), 1)
if (is15MinBar % 3 == 0)
    alert("15 dakikalıkta 3 mum geçti.")

```

> Detail

https://www.fmz.com/strategy/434551

> Last Modified

2023-12-07 15:15:26
