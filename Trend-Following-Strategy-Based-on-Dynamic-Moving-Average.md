
> Name

Trend-Following-Strategy-Based-on-Dynamic-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/6f9eaaf7fa17f42d62f0b325affe5fe3f0e91f87a5bc84c98d51fb0da7d85345.png)
[trans]

## Overview
This strategy is based on the dynamic moving average indicator, which enables real-time tracking of price trends and sends trading signals through the breakthrough of the moving average. The advantages of the strategy are simple parameter setting, clear signal judgment, and suitable for medium and long-term positions.
## Strategy Principle
This strategy uses dynamic moving average indicators, including ALMA, EMA, SMA and other types of moving averages. The basic principle is that when the price crosses above the moving average, go long; when the price crosses below the moving average, go short. That is, the moving average is used as a barometer of price trends, and trading signals can be issued when a direction change occurs.
Specifically, the strategy uses the moving average formed by high and low points, and then uses the low moving average as a long signal line and the high moving average as a short signal line. When the closing price is higher than the low moving average, go long; when the closing price is lower than the high moving average, go short.
In this way, moving average indicators are used to determine the price trend, and then combined with the breakthrough principle to send signals, a simple and practical trend following strategy is formed.
## Strategic Advantages
- Use moving average indicators to judge, simple parameter settings and easy operation
- The signal judgment rules are clear and no false signals will be generated
- You can freely choose the moving average algorithm to flexibly respond to market changes
- Adjustable moving average parameters to adapt to trends in different cycles
- Signals can be verified in multiple time frames to improve reliability
## Risks and Solutions
- The moving average indicator lags behind and some opportunities may be missed.
    - Shorten the moving average period appropriately, or use exponential moving average EMA
- Large fluctuations in the short term, risk of stop loss
    - Appropriately relax the stop loss range to ensure sufficient room for maneuver
- Long-term holding risk, you may not be able to stop profits in time
    - Combine judgment with other indicators to avoid chasing highs and selling lows
## Strategy optimization
- Adjust the moving average algorithm and parameters according to the characteristics of different varieties
- Add secondary indicator judgment to improve strategy effect
- Add stop loss and stop profit mechanism
- Evaluate signal reliability on multiple time frames
- Combined with machine learning technology to find better parameters
## Summarize
This strategy uses moving average indicators to determine the direction of price trends and sends trading signals based on breakout theory. The advantage is that it is simple and easy to use, suitable for medium and long-term positions, and can adapt to market changes through parameter adjustment. It is necessary to pay attention to prevent short-term fluctuations and risks caused by long-term holdings, which can be solved by stop-loss and stop-profit. There is room for optimization in using more indicators to improve strategy effects and using machine learning to find better parameters.
||

## Overview  

This strategy is based on the dynamic moving average indicator to track the price trend in real time and generate trading signals when the moving average is broken through. The advantage of this strategy lies in its simple parameter settings, clear signal rules, and suitability for medium-to-long-term holding.  

## Strategy Logic  

This strategy utilizes dynamic moving average indicators including ALMA, EMA, SMA and more. The principle is to go long when the price breaks above the moving average and go short when it breaks below. That is, the moving average serves as a barometer for the price trend, and signals can be generated when a trend reversal occurs.   

Specifically, the strategy uses moving averages formed by high and low prices. The low price MA serves as the signal line for long signals, while the high price MA serves as the line for shorts. When the closing price rises above the low price MA, go long. When the close drops below the high price MA, go short.   

By judging the price trend with MA and combining with the breakout principle to generate signals, a simple and practical trend following strategy is formed.  

## Advantages  

- Simple parameter settings with MA indicator, easy to operate  
- Clear signal rules without false signals  
- Flexible MA types to adapt to market changes
- Adjustable MA periods suit different trend cycles  
- Multi-timeframe signal validation improves reliability   

## Risks and Solutions   

- MA lag may miss some opportunities 
    - Shorten MA period or use EMA
- Large swing risks in short term  
    - Widen stop loss room for flexibility 
- Long holding risks, unable to lock profit in time
    - Combine other indicators, avoid chasing highs and killing lows  

## Optimization Directions   

- Adjust MA type and parameters based on symbol characteristics   
- Add auxiliary indicators to improve strategy 
- Add stop loss and take profit mechanisms  
- Evaluate signal reliability across timeframes   
- Utilize machine learning to find better parameters  

## Conclusion  

This strategy judges the trend direction with MA and generates signals based on the breakout principles. It is simple to use and suitable for medium-to-long-term holding. The parameters can also be adjusted to adapt to market changes. Risks from short-term fluctuations and long holding need to be managed with stop loss/profit taking. There is room for improvement by incorporating more indicators and finding optimal parameters through machine learning.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|MA Type: ALMA|EMA|WMA|HMA|VWMA|RMA|SMA|
|v_input_2|55|MA Length|
|v_input_3_ohlc4|0|Closing Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_4|0.85|Offset (alma only)|
|v_input_5|10|Sigma (alma only)|
|v_input_6|true|Use Current Resolution|
|v_input_7|1440|Timeframe|
|v_input_8|false|Show Signals ?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-02 00:00:00
end: 2024-01-01 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Baseline Strategy - evo", shorttitle="Baseline", overlay=true)

//INPUTS
mat =               input("ALMA", "MA Type", options=["SMA", "EMA", "WMA", "HMA", "VWMA", "RMA", "ALMA"])
baseline =          input(55, title="MA Length")
src =               input(ohlc4, title="Closing Source")

offset =            input(0.85, step=0.05, title="Offset (alma only)")
sigma =             input(10, title="Sigma (alma only)")

useCurrentRes =     input(true, title="Use Current Resolution")
resCustom =         input("1440", title="Timeframe")

showsignals =       input(false, title="Show Signals ?")

//BASELINE
baselinehigh = 

 mat=="SMA" ? sma(high,baseline) : 
 mat=="EMA" ? ema(high,baseline) : 
 mat=="WMA" ? wma(high,baseline) : 
 mat=="HMA" ? wma(2*wma(high, baseline/2)-wma(high, baseline), round(sqrt(baseline))) : 
 mat=="VWMA" ? vwma(high,baseline) : 
 mat=="RMA" ? rma(high,baseline) :
 mat=="ALMA" ? alma(high, baseline, offset, sigma) : na

baselinelow = 

 mat=="SMA" ? sma(low,baseline) : 
 mat=="EMA" ? ema(low,baseline) : 
 mat=="WMA" ? wma(low,baseline) : 
 mat=="HMA" ? wma(2*wma(low, baseline/2)-wma(low, baseline), round(sqrt(baseline))) : 
 mat=="VWMA" ? vwma(low,baseline) : 
 mat=="RMA" ? rma(low,baseline) : 
 mat=="ALMA" ? alma(low, baseline, offset, sigma) : na

//RESOLUTION
res =               useCurrentRes ? timeframe.period : resCustom

mtfhigh =           security(syminfo.tickerid, res, baselinehigh)
mtflow =            security(syminfo.tickerid, res, baselinelow)

//PLOTS
plot(mtfhigh, color=color.navy, linewidth=2, transp=0, title="Baseline High")
plot(mtflow, color=color.navy, linewidth=2, transp=0, title="Baseline Low")

long =              src > mtfhigh
short =             src < mtflow

barcolor(long ? #ffe0b2 : short ? #2a2e39 : not long and not short ? #b09e82 : na, title="BaseLine BarColor")

signal = 0
signal := long ? 1 : short ? 2 : nz(signal[1])

plotshape(showsignals ? (signal != signal[1] and long ? mtflow : na) : na, title="Long", location=location.absolute, size=size.small, style=shape.labelup, text="Long", textcolor=color.black, transp=40, color=#00ff00)
plotshape(showsignals ? (signal != signal[1] and short ? mtfhigh : na) : na, title="Short", location=location.absolute, size=size.small, style=shape.labeldown, text="Short", textcolor=color.white, transp=40, color=#ff0000)

alertcondition(signal != signal[1], title="Trend Change !", message="Trend Change !")

if (long)
    strategy.entry("Long", strategy.long)
if (short)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/437378

> Last Modified

2024-01-02 10:44:53
