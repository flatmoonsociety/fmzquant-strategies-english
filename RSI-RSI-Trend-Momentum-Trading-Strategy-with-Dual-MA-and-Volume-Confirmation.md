
> Name

RSI-Trend-Momentum-Trading-Strategy-with-Dual-MA-and-Volume-Confirmation
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11f03a3366467bafaf4.png)

[trans]
#### Overview
This strategy is a trend following strategy based on RSI oversold signals, long and short-term moving average trends, and volume confirmation. It mainly establishes long positions by identifying short-term oversold opportunities in long-term uptrends, while using volume amplification to confirm the validity of trading signals. The strategy uses the 10-period RSI indicator, the 250- and 500-period dual moving average system, and the 20-period volume moving average as the core indicator combination.
#### Strategy Principle
The core logic of the strategy is based on the synergy of three key conditions:
1. RSI oversold signal (RSI<=30): used to capture oversold market rebound opportunities
2. Double moving average bull arrangement (SMA250>SMA500): confirming the long-term upward trend
3. Trading volume confirmation (current trading volume > 20-period trading volume moving average * 2.5): Verify the validity of price changes
When the above three conditions are met at the same time, the strategy enters a long position. The closing signal is triggered by the short-term moving average crossing below the long-term moving average (die cross). At the same time, the strategy sets a 5% stop loss to control risk.
#### Strategic Advantages
1. Multiple confirmation mechanism reduces false signals: combined with triple filtering of RSI, moving average and trading volume, it significantly improves the reliability of trading signals.
2. Trend following characteristics: judge the general trend through long-term moving averages and avoid counter-trend transactions
3. Improved risk control: Set fixed stop loss levels to effectively control single transaction risks
4. Strong adaptability: strategy parameters can be flexibly adjusted according to different market characteristics
5. Strict screening of trading opportunities: multiple conditional filters ensure only entering the market at the best time
#### Strategy Risk
1. Lagging risk: There is a significant lag in the long-term moving average, and early trends may be missed.
2. Risk of excessive filtering: Strict multiple conditions may miss some effective trading opportunities
3. Volatile market risk: False signals may be frequently triggered in a volatile market.
4. Stop loss setting risk: fixed ratio stop loss may not be suitable for all market environments
5. Parameter optimization risk: Over-optimization may lead to poor performance of the strategy in real trading
#### Strategy optimization direction
1. Dynamic stop loss optimization: consider a dynamic stop loss mechanism based on ATR or volatility
2. Quantify trend strength: Introduce trend strength indicators such as ADX to improve the accuracy of trend judgment.
3. Position management optimization: dynamically adjust the position ratio based on signal strength and market volatility
4. Improved exit mechanism: flexible exit mechanisms such as increased profit target and trailing stop loss
5. Time filtering: Add transaction time filtering to avoid inefficient trading periods
#### Summary
This is a well-designed and logically rigorous trend tracking strategy that effectively balances returns and risks through the combined use of multiple technical indicators. The core advantage of the strategy lies in its complete signal confirmation mechanism and risk control system, but it also faces challenges such as excessive filtering and hysteresis. Through the suggested optimization directions, the strategy is expected to achieve better performance in practical applications. ||
#### Overview
This strategy is a trend-following system that combines RSI oversold signals, long-term moving averages, and volume confirmation. It aims to capture long positions during oversold conditions within established uptrends, validated by volume expansion. The strategy utilizes a 10-period RSI, dual SMAs of 250 and 500 periods, and a 20-period volume moving average as core indicators.

#### Strategy Principles
The core logic is based on three key conditions working in harmony:
1. RSI oversold signal (RSI<=30): Captures market rebound opportunities
2. Dual MA bullish alignment (SMA250>SMA500): Confirms long-term uptrend
3. Volume confirmation (Current volume>20-period volume MA*2.5): Validates price movements

A long position is initiated when all three conditions are met simultaneously. The exit signal is triggered by a death cross (shorter MA crossing below longer MA). Additionally, a 5% stop-loss is implemented for risk management.

#### Strategy Advantages
1. Multiple confirmation reduces false signals: Integration of RSI, MAs, and volume provides robust signal filtering
2. Trend-following characteristics: Long-term MAs prevent counter-trend trading
3. Comprehensive risk control: Fixed stop-loss effectively manages per-trade risk
4. High adaptability: Parameters can be adjusted for different market conditions
5. Strict trade selection: Multiple conditions ensure optimal entry timing

#### Strategy Risks
1. Lag risk: Long-period MAs introduce significant delay in trend identification
2. Over-filtering risk: Strict multiple conditions might miss valid trading opportunities
3. Ranging market risk: False signals may occur frequently in sideways markets
4. Stop-loss configuration risk: Fixed percentage stops may not suit all market conditions
5. Parameter optimization risk: Over-optimization may lead to poor live trading performance

#### Optimization Directions
1. Dynamic stop-loss: Consider implementing ATR or volatility-based dynamic stops
2. Trend strength quantification: Incorporate ADX or similar indicators for better trend assessment
3. Position sizing optimization: Adjust position size based on signal strength and market volatility
4. Exit mechanism enhancement: Add profit targets and trailing stops for flexible exits
5. Time filtering: Implement trading time filters to avoid inefficient periods

#### Summary
This is a well-designed trend-following strategy with rigorous logic, effectively balancing returns and risks through multiple technical indicators. Its core strengths lie in comprehensive signal confirmation and risk management systems, though it faces challenges in over-filtering and latency. Through the suggested optimization directions, the strategy shows potential for improved performance in practical applications.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


// This work is licensed under a Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0) https://creativecommons.org/licenses/by-nc-sa/4.0/
// © wielkieef

//@version=5
strategy(title=' Rsi Long-Term Strategy [15min]', overlay=true, pyramiding=1, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, calc_on_order_fills=false, slippage=0, commission_type=strategy.commission.percent, commission_value=0.03)

// Rsi
rsi_lenght = input.int(10, title='RSI lenght', minval=0)
rsi_up = ta.rma(math.max(ta.change(close), 0), rsi_lenght)
rsi_down = ta.rma(-math.min(ta.change(close), 0), rsi_lenght)
rsi_value = rsi_down == 0 ? 100 : rsi_up == 0 ? 0 : 100 - 100 / (1 + rsi_up / rsi_down)
rsi_overs = rsi_value <= 30
rsi_overb = rsi_value >= 70

// Volume
vol_sma_length = input.int(20, title='Volume lenght  ', minval=1)
Volume_condt = volume > ta.sma(volume, vol_sma_length) * 2.5

//SMA1
lengthSMA1 = input(250, title="Lenght SMA 1")
SMA1 = ta.sma(close, lengthSMA1)
//plot(SMA1, color=color.rgb(245, 108, 3), linewidth=1, title="SMA250")

//SMA2
lengthSMA2 = input(500, title="Lenght SMA 2")
SMA2 = ta.sma(close, lengthSMA2)
//plot(SMA2, color=#9803f5, linewidth=1, title="SMA500")


//Entry Logic
Long_cond = (rsi_overs and SMA1 > SMA2 and Volume_condt )  

if Long_cond
    strategy.entry('Long', strategy.long)

//Close Logic
Long_close = ta.crossunder(SMA1,SMA2)

if Long_close
    strategy.close("Long")

//Bar colors
Bar_color = Volume_condt ? #fc9802 : SMA1 > SMA2 ? color.rgb(84, 252, 0) : SMA1 < SMA2 ? color.maroon : color.gray
barcolor(color=Bar_color)

// Rsi value Plotshapes
plotshape(rsi_value < 30 and SMA1 > SMA2 and Volume_condt, title='Buy', color=color.new(color.green, 0), style=shape.circle, location=location.belowbar, size=size.tiny, textcolor=color.new(color.black, 0))
plotshape(rsi_value > 70 and SMA1 < SMA2 and Volume_condt, title='Sell', color=color.new(color.red, 0), style=shape.circle, location=location.abovebar, size=size.tiny, textcolor=color.new(color.black, 0))
plotshape(ta.crossunder(SMA1,SMA2) , title='DEATH CROSS', color=#000000, style=shape.xcross, location=location.abovebar, size=size.small, textcolor=color.new(color.black, 0))

//Stop-Loss// this code is from author RafaelZioni, modified by wielkieef
pera(pcnt) =>
    strategy.position_size != 0 ? math.round(pcnt / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)
stoploss = input.float(title=' stop loss', defval=5.0, minval=0.5)
los = pera(stoploss)
strategy.exit('SL', loss=los)




// by wielkieef
```

> Detail

https://www.fmz.com/strategy/473261

> Last Modified

2024-11-28 17:02:32
