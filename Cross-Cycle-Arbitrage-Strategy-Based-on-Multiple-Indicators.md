
> Name

Cross-Cycle-Arbitrage-Strategy-Based-on-Multiple-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/135d93e3523629b7234.png)
[trans]
### Overview
This strategy uses a combination of three different technical indicators to build a multi-time frame arbitrage strategy to achieve low-risk excess returns by capturing price trends in different time periods.
### Strategy Principles
The three technical indicators used in this strategy are the Celtic Channel (KC), Volatility Stop (Vstop), and the William Gathering Indicator (WAE). The Celtic Channel is used to determine if the price is outside the range of the channel, thus issuing a trading signal. Volatility stop loss is used to dynamically adjust the stop loss position to ensure stop loss while reducing unnecessary stop loss. The William indicator is used to determine whether the price is in a strong direction. Specifically:
1. When the price is above the upper line of the Celtic Channel, it is considered a bullish signal. When the price falls below the lower edge of the Celtic Channel, it is considered a bearish signal.
2. Volatility stop loss sets the stop loss position based on price volatility and channel width. It can be adjusted dynamically to avoid overly conservative stop loss positions while ensuring stop loss.
3. The William indicator determines whether the price is in a strong upward or downward trend by calculating the MACD and Bollinger Bands channel width.
By combining these three indicators, signals on different time periods can verify each other. This reduces the probability of misjudgment and builds a stable and optimized strategy logic.
### Advantage Analysis
The biggest advantage of this strategy is the precise trading signals brought by the combination of multiple indicators. The three indicators act on different time periods and verify each other, which can effectively reduce the probability of misjudgment and enhance the accuracy of the signal. In addition, the volatility stop loss setting is dynamic and can adjust the stop loss position according to real-time fluctuations to further control risks.
Compared with a single indicator strategy, this combination strategy can provide more accurate and efficient trading signals. At the same time, the three indicators cooperate with each other to form trading judgments in multiple time frames. This logical design is very scientific and reasonable and is worth learning from.
### Risk Analysis
The main risk of this strategy is that improper parameter settings may lead to overfitting. The three indicators have a total of 8 parameters, and improper settings may have an adverse impact on the strategy. In addition, the weight relationship between indicators also needs to be reasonably configured, otherwise the signals may cancel each other out, resulting in ineffectiveness.
In order to reduce these risks, the adaptability to different market environments needs to be fully considered during the parameter setting process, and the optimal parameter combination needs to be adjusted through backtest analysis. In addition, the weight relationship between indicators should be appropriately adjusted to ensure that trading signals can be effectively triggered. When continuous losses occur, you also need to consider reducing the position size and controlling losses.
### Optimization direction
The optimization space of this strategy mainly focuses on two aspects: parameter tuning and stop-loss strategy improvement. Specifically, you can start from the following aspects:
1. Select indicator parameters more scientifically and rationally, and optimize parameter combinations. Algorithms can be used to find optimal parameters according to goals such as revenue maximization and risk minimization.
2. Improve the stop loss strategy, further reduce unnecessary stop losses and improve the winning rate while ensuring the stop loss. For example, combine more indicators as stop loss signals, or set a gradual retracement of the stop loss position.
3. Optimize the weight relationship of indicators and the judgment logic of trading signals to reduce the misjudgment rate. More price behavior characteristics can be introduced to build more stable and reliable judgment rules.
4. Try to introduce a machine learning model to achieve automatic parameter optimization. Or use deep reinforcement learning programming for policy evaluation and improvement.
### Summarize
This strategy uses the combination of Celtic Channel, volatility stop loss and William indicator to build an arbitrage system across time frames. Multi-indicator combination improves the accuracy of trading signals, and dynamic stop loss controls risks. However, there is still room for improvement in parameter setting and optimization. Overall, this strategy is scientific and worthy of further research and application.
||

### Overview  

This strategy uses a combination of three different technical indicators to build a cross-cycle arbitrage strategy that captures price trends across different time frames to achieve low-risk excess returns.

### Strategy Logic  

The three technical indicators used in this strategy are Keltner Channel (KC), Volatility Stop (Vstop), and Williams Alligator (WAE). The Keltner Channel is used to determine if prices are outside the channel range and thus generate trading signals. Volatility Stop is used to dynamically adjust stop loss positions to ensure stop loss while reducing unnecessary stop loss. The Williams Alligator indicator is used to determine if prices are in a strong trend. Specifically:

1. When the price is higher than the Keltner Channel upper rail, it is considered a bullish signal. When the price is lower than the Keltner Channel lower rail, it is considered a bearish signal.  

2. Volatility Stop sets the stop loss position based on price volatility and channel width. It can adjust dynamically to ensure stop loss while avoiding excessively conservative stop loss positions.

3. The Williams Alligator indicator judges whether prices are in a strong uptrend or downtrend by calculating the MACD and Bollinger Band channel width.

By combining these three indicators, signals across different time frames are cross validated. This reduces the probability of misjudgment and builds an optimized strategy logic.  

### Advantage Analysis

The biggest advantage of this strategy is the precise trading signals brought by the combination of multiple indicators. The three indicators work in different time frames and cross validate each other, which can effectively reduce the probability of misjudgment and enhance the accuracy of signals. In addition, Volatility Stop setting is dynamic and can adjust the stop loss position according to real-time volatility to further control risks.

Compared with single indicator strategies, this combined strategy can provide more accurate and efficient trading signals. At the same time, the three indicators work together to form trading judgments within multiple time frames, which is a very scientific and reasonable logic design worth learning from.

### Risk Analysis  

The main risk of this strategy is that improper parameter settings may cause overfitting. The three indicators have 8 parameters in total. Improper settings may adversely affect the strategy. In addition, the weight relationship between indicators also needs to be properly configured, otherwise the signals may neutralize each other and become invalid.  

To reduce these risks, the adaptability to different market environments should be fully considered during parameter setting, and the optimal parameter combination should be adjusted through backtesting analysis. In addition, appropriately adjust the weights between indicators to ensure that trading signals can be effectively triggered. When consecutive losses occur, consider reducing the position size to control losses.

### Optimization Directions

The optimization space of this strategy mainly focuses on two aspects: parameter tuning and improvement of stop loss strategies. Specifically, the following aspects can be considered:

1. Choose indicator parameters more scientifically and optimize parameter combinations. Algorithms can be used to find the optimal parameters with the goals like return maximization and risk minimization.  

2. Improve the stop loss strategy to further reduce unnecessary stop loss while ensuring stop loss, thereby improving win rate. For example, incorporate more indicators as stop loss signals, or set progressive pullback of stop loss positions.  

3. Optimize weights between indicators and logic of trading signal judgments to reduce misjudgment rate. More price behavior features can be introduced to build more stable and reliable judgment rules.  

4. Try to introduce machine learning models to achieve automatic parameter optimization. Or use deep reinforcement learning programming for strategy evaluation and improvement.

### Summary   

This strategy builds a cross-cycle arbitrage system through the combination of Keltner Channel, Volatility Stop and Williams Alligator. Multi-indicator combination improves signal accuracy and dynamic stop loss controls risks. But there is room for improvement in parameters setting and optimization. Overall, this strategy has strong scientificity and is worth further research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|Keltner Period|
|v_input_2|5|Keltner Mult|
|v_input_3|3|Vstop length|
|v_input_4|150|Sensitivity|
|v_input_5|20|FastEMA Length|
|v_input_6|40|SlowEMA Length|
|v_input_7|20|BB Channel Length|
|v_input_8|2|BB Stdev Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("QuarryLake", overlay=true)  ///Ultilized modified full kelly for this strategy = 36%

///Keltner channel///
nPeriod = input(title="Keltner Period", type=input.integer, defval=200, minval=1)
Mult = input(title="Keltner Mult", type=input.integer, defval=5, minval=1)
xPrice = ema(hlc3, nPeriod)
xMove = ema(high - low, nPeriod)
xMoveMult = xMove * Mult
xUpper = xPrice + xMoveMult
xLower = xPrice - xMoveMult

// plot(xPrice, color=red, title="KSmid")
p1 = plot(xUpper, color=color.white, title="KSup")
p2 = plot(xLower, color=color.white, title="KSdn")
fill(p1, p2, color=close > xUpper ? color.green : close < xLower ? color.red : color.white)

kclongcondition = close > xUpper
kcshortcondition = close < xLower
kccloselongcondition = crossunder(close, xUpper)
kccloseshortcondition = crossover(close, xLower)

///Volatility Stop///
length = input(title="Vstop length", type=input.integer, defval=3, minval=1)
mult1 = 1.5

atr_ = atr(length)
max1 = 0.0
min1 = 0.0
is_uptrend_prev = false
stop = 0.0
vstop_prev = 0.0
vstop1 = 0.0
is_uptrend = false
is_trend_changed = false
max_ = 0.0
min_ = 0.0
vstop = 0.0
max1 := max(nz(max_[1]), close)
min1 := min(nz(min_[1]), close)
is_uptrend_prev := nz(is_uptrend[1], true)
stop := is_uptrend_prev ? max1 - mult1 * atr_ : min1 + mult1 * atr_
vstop_prev := nz(vstop[1])
vstop1 := is_uptrend_prev ? max(vstop_prev, stop) : min(vstop_prev, stop)
is_uptrend := close - vstop1 >= 0
is_trend_changed := is_uptrend != is_uptrend_prev
max_ := is_trend_changed ? close : max1
min_ := is_trend_changed ? close : min1
vstop := is_trend_changed ? is_uptrend ? max_ - mult1 * atr_ : min_ + mult1 * atr_ : 
   vstop1

plot(vstop, color=is_uptrend ? color.green : color.red, style=plot.style_line, linewidth=1)

vstoplongcondition = close > vstop
vstoplongclosecondition = crossunder(close, vstop)
vstopshortcondition = close < vstop
vstopshortclosecondition = crossover(close, vstop)

///Waddah Attar Explosion///
sensitivity = input(150, title="Sensitivity")
fastLength = input(20, title="FastEMA Length")
slowLength = input(40, title="SlowEMA Length")
channelLength = input(20, title="BB Channel Length")
mult = input(2.0, title="BB Stdev Multiplier")
DEAD_ZONE = nz(rma(tr(true), 100)) * 3.7
calc_macd(source, fastLength, slowLength) =>
    fastMA = ema(source, fastLength)
    slowMA = ema(source, slowLength)
    fastMA - slowMA
calc_BBUpper(source, length, mult) =>
    basis = sma(source, length)
    dev = mult * stdev(source, length)
    basis + dev
calc_BBLower(source, length, mult) =>
    basis = sma(source, length)
    dev = mult * stdev(source, length)
    basis - dev
t1 = (calc_macd(close, fastLength, slowLength) - 
   calc_macd(close[1], fastLength, slowLength)) * sensitivity
t2 = (calc_macd(close[2], fastLength, slowLength) - 
   calc_macd(close[3], fastLength, slowLength)) * sensitivity
e1 = calc_BBUpper(close, channelLength, mult) - 
   calc_BBLower(close, channelLength, mult)
trendUp = t1 >= 0 ? t1 : 0
trendDown = t1 < 0 ? -1 * t1 : 0

waelongcondition = trendUp and trendUp > DEAD_ZONE and trendUp > e1
waeshortcondition = trendDown and trendDown > DEAD_ZONE and trendDown > e1

///Long Entry///
longcondition = kclongcondition and vstoplongcondition and waelongcondition
if longcondition
    strategy.entry("Long", strategy.long)

///Long exit///
closeconditionlong = kccloselongcondition or vstoplongclosecondition
if closeconditionlong
    strategy.close("Long")

///Short Entry///
shortcondition = kcshortcondition and vstopshortcondition and waeshortcondition
if shortcondition
    strategy.entry("Short", strategy.short)

///Short exit///
closeconditionshort = kccloseshortcondition or vstopshortclosecondition
if closeconditionshort
    strategy.close("Short")

///Free Hong Kong, the revolution of our time///

```

> Detail

https://www.fmz.com/strategy/440309

> Last Modified

2024-01-29 11:10:33
