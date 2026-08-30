
> Name

MACD Trend Following Strategy-MACD-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/e339b6dc204ec1405c7caa483c277460986b518092006f31c6f1aa1ed73705c2.png)

[trans]

#### Overview
The MACD trend following strategy is a quantitative trading strategy based on the MACD indicator. The main idea of ​​this strategy is to use the golden cross and dead cross signals of the MACD indicator to determine the direction of the trend, and establish long or short positions at the appropriate time. When the MACD line crosses the signal line and goes above the 0 axis, a long position is opened; when the MACD line crosses below the signal line and goes below the 0 axis, a short position is opened. This strategy uses the most recent low as a long stop and the most recent high as a short stop. The condition for closing the position is that the MACD line crosses the signal line in the opposite direction.
#### Strategy Principle
The core principle of the MACD trend following strategy is to use the MACD indicator to capture the formation and reversal of trends. The MACD indicator is composed of the difference between two moving averages (fast moving average and slow moving average), and is used in conjunction with the signal line to generate trading signals. When the MACD line crosses the signal line and crosses the 0 axis, it indicates that an upward trend has formed, and a long position is opened at this time. When the MACD line crosses below the signal line and below the 0 axis, it indicates that a downward trend has formed, and a short position is opened at this time. The strategy uses the most recent significant low as a long stop and the most recent significant high as a short stop to control risk. When the MACD line crosses the signal line in the opposite direction, close the current position.
#### Strategic Advantages
1. The MACD trend following strategy can effectively capture trend opportunities, build positions at the early stage of the trend, and make full use of the momentum of the trend.
2. This strategy uses both the MACD Golden Cross and the 0 axis as filter conditions, which can better filter out false signals in the volatile market.
3. The strategy uses recent significant highs and lows as stop loss levels to control the risk exposure of a single transaction.
4. The strategy logic is clear, easy to understand and implement, and is suitable for beginners to learn.
#### Strategy Risk
1. The MACD indicator is essentially a lagging indicator, and there may be a large retracement in the early stages of a trend reversal.
2. The strategy may result in frequent transactions in volatile markets, resulting in higher transaction costs.
3. The setting of the stop loss position depends on the recent significant high and low points. In some cases, the stop loss may be too early or too late.
4. This strategy does not consider position management and fund management, and it needs to be optimized based on specific circumstances in actual application.
#### Strategy optimization direction
1. You can consider introducing other technical indicators or price action patterns as filter conditions to improve the reliability and accuracy of signals.
2. Optimize the method of setting stop loss levels, such as using ATR or percentage stop loss, to better control risks.
3. Introduce position management and fund management mechanisms to dynamically adjust position sizes based on market volatility and account equity.
4. Optimize and adjust parameters for different markets and trading targets to find the most suitable parameter combination.
#### Summary
The MACD trend following strategy is a simple and effective quantitative trading strategy that captures trend opportunities by utilizing the characteristics of the MACD indicator. The strategy has clear logic, is easy to understand and implement, and is suitable for beginners to learn. However, in practical applications, it is necessary to pay attention to risk control and combine other methods for optimization and improvement to obtain more robust trading performance.
||

#### Overview
The MACD Trend Following Strategy is a quantitative trading strategy based on the MACD indicator. The main idea of this strategy is to use the golden cross and death cross signals of the MACD indicator to determine the direction of the trend and establish long or short positions at appropriate times. When the MACD line crosses above the signal line and above the zero axis, a long position is opened; when the MACD line crosses below the signal line and below the zero axis, a short position is opened. The strategy uses the most recent low point as the stop loss for long positions and the most recent high point as the stop loss for short positions. The closing condition is when the MACD line crosses the signal line in the opposite direction.

#### Strategy Principle
The core principle of the MACD Trend Following Strategy is to use the MACD indicator to capture the formation and reversal of trends. The MACD indicator consists of the difference between two moving averages (fast and slow) and is used in conjunction with a signal line to generate trading signals. When the MACD line crosses above the signal line and above the zero axis, it indicates an upward trend is forming, and a long position is opened. When the MACD line crosses below the signal line and below the zero axis, it indicates a downward trend is forming, and a short position is opened. The strategy uses the most recent significant low point as the stop loss for long positions and the most recent significant high point as the stop loss for short positions to control risk. When the MACD line crosses the signal line in the opposite direction, the current position is closed.

#### Strategy Advantages
1. The MACD Trend Following Strategy can effectively capture trending opportunities by establishing positions at the beginning of trend formation, fully utilizing the momentum of the trend.

2. The strategy uses both the MACD golden/death cross and the zero axis as filtering conditions, which can better filter out false signals in a oscillating market.

3. The strategy uses the most recent significant high and low points as stop loss levels, which can control the risk exposure of a single trade.

4. The strategy logic is clear, easy to understand and implement, making it suitable for beginners to learn.

#### Strategy Risks
1. The MACD indicator is essentially a lagging indicator, which may experience significant drawdowns at the beginning of trend reversals.

2. The strategy may generate frequent trades in a oscillating market, leading to high transaction costs.

3. The setting of stop loss levels depends on the most recent significant high and low points, which may result in premature or delayed stop losses in certain situations.

4. The strategy does not consider position sizing and money management, which need to be optimized based on specific circumstances in practical applications.

#### Strategy Optimization Directions
1. Consider introducing other technical indicators or price behavior patterns as filtering conditions to improve the reliability and accuracy of signals.

2. Optimize the method of setting stop loss levels, such as using ATR or percentage-based stop losses, to better control risk.

3. Introduce position sizing and money management mechanisms to dynamically adjust position sizes based on market volatility and account equity.

4. Optimize and adjust parameters for different markets and trading instruments to find the most suitable parameter combinations.

#### Summary
The MACD Trend Following Strategy is a simple and effective quantitative trading strategy that captures trending opportunities by leveraging the characteristics of the MACD indicator. The strategy has a clear logic, is easy to understand and implement, making it suitable for beginners to learn. However, in practical applications, attention needs to be paid to risk control, and it should be combined with other methods for optimization and improvement to achieve more robust trading performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|MACD fast moving average|
|v_input_2|9|MACD slow moving average|
|v_input_3|5|MACD signal line moving average|
|v_input_4|true|length|
|v_input_5|true|From Month|
|v_input_6|true|From Day|
|v_input_7|2002|From Year|
|v_input_8|3|To Month|
|v_input_9|true|To Day|
|v_input_10|2029|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-23 00:00:00
end: 2024-03-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("MACD trendfollow", shorttitle="MACD TF", overlay=true)
// switch = input(true, title="Enable MACD Bar Color")
// X001TK MACD trendfollow Strategy
//
// 
// This strategy combines the non standart approach in MACD strategy to buy once to buy when the MACD value goes above Signal line and a zero line, to sell on the opposite condition.
//
//
// This strategy goes long if the MACD (3,9,5) goes above its Signal and above zero
//
// You can set Stop loss on the recent lowest low when long position is opened and recent highest hugh in short
// 
//
// Exit rule is simple. We close the LONG position once MACD goes below Signal line and close SHORT on the opposite condition 
//
// 
// 
//
// Input
fastMAlen = input(3, minval=1, title="MACD fast moving average")
slowMAlen = input(9,minval=1, title="MACD slow moving average")
signalMACDlen = input(5,minval=1, title="MACD signal line moving average")
// switch = input(true, title="Enable MACD Bar Color")
length = input(1, minval=1)



// === INPUT BACKTEST RANGE ===
FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
FromYear  = input(defval = 2002, title = "From Year", minval = 2000)
ToMonth   = input(defval = 3, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
ToYear    = input(defval = 2029, title = "To Year", minval = 2017)



// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 00, 00)        // backtest finish window
window()  => true // create function "within window of time"

// MACD Calculation
MACD = ema(close, fastMAlen) - ema(close, slowMAlen)
signalMACD = ema(MACD, signalMACDlen)
delta = MACD - signalMACD
fastMA = ema(close,fastMAlen)
slowMA = ema(close,slowMAlen)


// Colors
//bartrendcolor = MACD > signalMACD and MACD > 0? green : MACD < signalMACD and MACD < 0? red : MACD < signalMACD? gray :  gray 
//barcolor(switch?bartrendcolor:na)

barcolour=(MACD > signalMACD and MACD > 0)?#53B987:(MACD < signalMACD and MACD < 0)?#EB4D5C:na
barcolor(color=barcolour)


// === STRATEGY ===
// conditions

longCond =  MACD > signalMACD and MACD > 0 
XlongCond = MACD < signalMACD 
ShortCond = MACD < signalMACD and MACD < 0 
XShortCond = MACD > signalMACD 





strategy.entry("long", strategy.long, when=longCond==true and window()==true )
//strategy.exit(id="Close Long", stop=longStop)//, limit=longTake)
strategy.close("long", when=XlongCond==true and window()==true)
strategy.entry("short", strategy.short,  when=ShortCond==true and window()==true )
//strategy.exit(id="Close Short", stop=shortStop)//, limit=shortTake)
strategy.close("short", when=XShortCond==true and window()==true)

// === /STRATEGY ===
```

> Detail

https://www.fmz.com/strategy/446542

> Last Modified

2024-03-29 15:14:18
