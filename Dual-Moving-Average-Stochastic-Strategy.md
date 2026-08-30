
> Name

Dual-Moving-Average-Stochastic-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18bac4237d233e53ab7.png)
[trans]
### Overview
The dual moving average indicator stochastic strategy is a strategy that attempts to use a combination of moving average indicators and stochastic indicators to find trading opportunities. It generates trading signals when the fast EMA crosses the slow SMA, and uses the stochastic K value to determine whether it is overbought or oversold to filter out some signals.
### Strategy Principles
This strategy is mainly based on two technical indicators:
1. Moving average: Calculate three moving averages with different parameters: fast EMA, slow SMA, and slow VWMA. When the fast EMA crosses above or below the slow SMA, a trading signal is generated.
2. Stochastic indicator: Calculate the %K value. When it exceeds the set overbought zone or oversold zone threshold, it is considered that the market may reverse, and some moving average trading signals can be filtered out.
Specifically, the logic of strategy signals is:
1. When the fast EMA crosses above the slow SMA, and the %K value is lower than the oversold zone threshold, go long; when the fast EMA crosses below the slow SMA, and the %K value is above the overbought zone threshold, go short.
2. For an open long position, if the %K value re-enters the oversold area, or the price falls below the stop loss line, the position will be closed. For open short positions, if the %K value re-enters the overbought area, or the price rises below the stop loss line, the position will be closed.
By combining the moving average indicator and the stochastic indicator, this strategy attempts to issue entry signals at high-probability moving average signal points, while using the stochastic indicator to filter out some mistaken entry opportunities.
### Advantage Analysis
This strategy has the following main advantages:
1. Combine a variety of technical indicators to comprehensively judge the market, which is more comprehensive than a single indicator.
2. Using stochastic indicators to filter signals can avoid errors to a certain extent.
3. Using multiple sets of moving averages of mixed parameters makes the judgment more comprehensive and accurate.
4. Built-in stop loss mechanism to control single loss.
### Risk Analysis
There are also some risks with this strategy:
1. The moving average indicator is prone to produce more uncertain signals, has a greater probability of entering by mistake, and has limited stop loss capabilities.
2. The stochastic indicator itself may also produce false signals.
3. Parameter settings (such as overbought and oversold area size, moving average period, etc.) may need to be optimized. Improper settings will affect strategy performance.  
4. A purely technical strategy that pays insufficient attention to fundamental factors.
Corresponding method:
1. Optimize parameters and find the best combination of indicator parameters.  
2. Reduce the position size appropriately and open positions in batches.
3. Combine with fundamental analysis to avoid major events.
### Optimization direction
This strategy can be optimized mainly from the following aspects:
1. Test and optimize the moving average parameters to find the optimal parameter combination.
2. Test the parameters of the stochastic indicator, such as the size of the overbought and oversold areas, and find the optimal parameters.
3. Try to add other indicators, such as VOLUME to enhance judgment or volatility indicator to measure risk, and enrich the Entry logic.  
4. Add stop loss methods, such as trailing stop loss, to control risks.
5. Optimize fund management methods, such as dynamically adjusting positions based on ATR.
6. Use panic indicators such as VIX to avoid major risk-off events.
### Summarize
The dual moving average indicator stochastic strategy designs a more robust trend following strategy through the combination of fast and slow moving average indicators and stochastic indicators. But there is also some room for optimization, such as parameter selection, stop loss methods, etc. If more indicator judgments and optimizations are further introduced, this strategy is expected to obtain more stable excess returns.
||

### Overview

The Dual Moving Average Stochastic strategy attempts to identify trading opportunities using a combination of moving average indicators and the stochastic oscillator. It generates trade signals when the fast EMA crosses above or below the slow SMA, while also using the stochastic %K value to filter out signals when the market is overextended.   

### Strategy Logic

The strategy is primarily based on two technical indicators:

1. Moving Averages: It computes a fast EMA, slow SMA and slow VWMA using different parameters, and generates trade signals when the fast EMA crosses the slow SMA.

2. Stochastic Oscillator: It calculates the %K value and considers the market overbought or oversold when %K crosses preset upper or lower threshold levels, using this to filter some of the moving average signals.

Specifically, the logic for signal generation is:

1. When the fast EMA crosses above the slow SMA, and %K is below the oversold level, go long. When the fast EMA crosses below the slow SMA, and %K is above the overbought level, go short.  

2. For existing long positions, close when %K re-enters the overbought zone or price breaches the stop loss. For short positions, close when %K re-enters the oversold zone or price breaches the stop loss.

By combining moving averages and the stochastic oscillator, the strategy attempts to identify high probability moving average signal points to enter trades, while using the stochastic to filter out some of the false signals. 

### Advantage Analysis 

The main advantages of this strategy are:

1. Combining multiple technical indicators provides more comprehensive judgment versus using a single indicator.  
2. Filtering with the stochastic oscillator avoids some false signals. 
3. Using multiple moving averages with mixed parameters allows for more robust signals.  
4. Incorporates a stop loss mechanism to control single trade loss.

### Risk Analysis

There are also some risks:

1. Moving averages can generate many uncertain signals resulting in more false entries; limited stop loss capability.
2. Stochastic oscillator may also produce incorrect signals on its own.  
3. Parameter settings require optimization (e.g. overbought/oversold levels, moving average periods) otherwise performance impact.
4. Lack of fundamental analysis. 

Mitigations:
1. Optimize parameters to find best combination of indicator settings.
2. Use smaller position sizing, scale in.  
3. Incorporate fundamental analysis to avoid events.

### Enhancement Opportunities

The main optimization opportunities are:

1. Test and optimize moving average parameters to find optimum.
2. Test stochastic parameters like overbought/oversold zones for optimum settings.
3. Incorporate additional indicators like volume or volatility for richer entry logic.
4. Enhance stop loss methodology e.g. trailing stops to lower risk.
5. Improve money management such as dynamic position sizing based on ATR.  
6. Avoid risk-off events using VIX etc.

### Conclusion

The Dual Moving Average Stochastic Strategy utilizes a blend of moving averages and the stochastic oscillator to design a robust trend following system, but has some enhancement opportunities around parameters, stops etc. Further refinements like additional indicators and optimizations can potentially deliver more consistent alpha.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|16|length|
|v_input_2|80|OverBought|
|v_input_3|20|OverSold|
|v_input_4|true|TradeLong|
|v_input_5|true|TradeShort|
|v_input_6|80|OverBoughtClose|
|v_input_7|20|OverSoldClose|
|v_input_8|50|trail_points|
|v_input_9_close|0|Fast EMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_10|true|Fast EMA Period|
|v_input_11_close|0|Slow SMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_12|100|Slow SMA Period|
|v_input_13_close|0|Slower SMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_14|30|Slower SMA Period|
|v_input_15|7|ATR Days Lookback|
|v_input_16|5|ATR Modifier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-22 00:00:00
end: 2024-01-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("TVIX MEAN REV V2 TREND", overlay=true)
length = input(16, minval=1)
OverBought = input(80)
OverSold = input(20)
TradeLong = input (true)
TradeShort = input (true)

OverBoughtClose = input(80)
OverSoldClose = input(20)

smoothK = 3
smoothD = 3
trail_points = input(50)

k = sma(stoch(close, high, low, length), smoothK)
d = sma(k, smoothD)
k2 = sma(stoch(close, high, low, length), smoothK)
d2 = sma(k, smoothD)


// === GENERAL INPUTS ===
// short Ema
maFastSource = input(defval=close, title="Fast EMA Source")
maFastLength = input(defval=1, title="Fast EMA Period", minval=1)
// long Sma
maSlowSource = input(defval=close, title="Slow SMA Source")
maSlowLength = input(defval=100, title="Slow SMA Period", minval=1)
// longer Sma
maSlowerSource = input(defval=close, title="Slower SMA Source")
maSlowerLength = input(defval=30, title="Slower SMA Period", minval=1)

//ATR Stop Loss Indicator by Keith Larson
atrDays = input(7, "ATR Days Lookback")
theAtr = atr(atrDays)
atrModifier = input(5.0, "ATR Modifier")
//plot(atr * atrModifier, title="ATR")

LstopLoss = close - (theAtr * atrModifier)
SstopLoss = close + (theAtr * atrModifier)



// === SERIES SETUP ===
/// a couple of ma's..
maFast = ema(maFastSource, maFastLength)
maSlow = sma(maSlowSource, maSlowLength)
maSlower = vwma(maSlowerSource, maSlowerLength)
rsi = rsi(maSlowerSource, maSlowerLength)

// === PLOTTING ===
fast = plot(maFast, title="Fast MA", color=color.red, linewidth=2, style=plot.style_line, transp=30)
slow = plot(maSlow, title="Slow MA", color=color.green, linewidth=2, style=plot.style_line, transp=30)
slower = plot(maSlower, title="Slower MA", color=color.teal, linewidth=2, style=plot.style_line, transp=30)


// === LOGIC === Basic - simply switches from long to short and vice-versa with each fast-slow MA cross
LongFilter = maFast > maSlow
ShortFilter = maSlow > maFast




BUY=crossover(k, d) and k < OverSold
SELL=crossunder(k, d) and k > OverBought

SELLCLOSE=crossover(k, d) and k < OverSoldClose
BUYCLOSE=crossunder(k, d) and k > OverBoughtClose

Open = open


if not na(k) and not na(d)
    if crossover(k, d) and k < OverSold and LongFilter and TradeLong
        strategy.entry("$", strategy.long, limit = Open, comment="Long")
    
    strategy.close("$",when = crossunder(k, d) and k > OverBoughtClose or open < LstopLoss  )
    ///strategy.close("$",when = open < LstopLoss  )
    
if not na(k) and not na(d)
    if crossunder(k, d) and k > OverBought and ShortFilter and TradeShort
        strategy.entry("$1", strategy.short, limit = Open, comment="S")
        
    strategy.close ("$1", when = crossover(k, d) and k < OverSoldClose or open > SstopLoss  )
    ///strategy.close ("$1", when = open < SstopLoss) 
    
  
        




```

> Detail

https://www.fmz.com/strategy/440322

> Last Modified

2024-01-29 11:54:10
