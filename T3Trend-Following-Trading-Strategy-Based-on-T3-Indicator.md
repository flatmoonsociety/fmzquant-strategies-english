
> Name

Trend-Following-Trading-Strategy-Based-on-T3-Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/107d015e0635530270f.png)
 [trans]
## Strategy Overview
This strategy designs a trend following trading system based on the T3 Moving Average indicator. The system can automatically identify the price trend direction and make long and short positions accordingly. Go long when prices rise and go short when prices fall. The system also has the ability to reverse trades.
## Strategy Principle
This strategy uses the T3 indicator to determine the price trend direction. The T3 indicator is an adaptive moving average that has higher sensitivity and can respond more quickly to price changes. The calculation formula of this indicator is:
T3(n) = GD(GD(GD(n)))

Among them, GD represents generalized DEMA (double exponential moving average), and the calculation formula is:
GD(n,v) = EMA(n) * (1+v)-EMA(EMA(n)) * v

v is the volume factor, which determines the response sensitivity of the moving average to the linear trend of price. When v=0, GD=EMA; when v=1, GD=DEMA. The author recommends setting v=0.7.
This strategy compares the T3 indicator with the price. When T3 goes above the price, it is judged that the price is on an upward trend, and you go long; when T3 goes below the price, it is judged that the price is on a downward trend, and you go short.
## Strategic Advantages
- Use the adaptive moving average T3 indicator to respond sensitively to changes in price trends
- Automatically determine the price trend direction without manual judgment
- Configurable reversal transactions to flexibly respond to market changes
## Strategy Risk
- The T3 indicator may be difficult to determine the direction of the trend during consolidation and shock.
- Adaptive Moving Average indicator is prone to error signals
- Risk control during reversal trading requires caution
You can reduce false trades by adjusting the parameters of the T3 indicator or adding other indicator filters. You can also set a stop loss to control a single loss.
## Strategy optimization direction
- Add other indicator filters, such as MACD, RSI and other indicators for combination
- Add trend judgment rules to avoid misoperations during market shocks
- Optimize parameters and adjust the value of v to obtain a better parameter combination
- Add stop loss logic
## Summarize
This strategy automatically determines the price trend direction through the T3 indicator, without manual judgment, and can automatically do long and short positions. At the same time, reversal trading logic can be configured to cope with more complex market conditions. There is room for optimization in indicator parameters, trading logic, etc., which can make the strategy perform better.
||

## Strategy Overview  

This strategy designs a trend following trading system based on the T3 moving average indicator. It can automatically identify the direction of price trends and take corresponding long or short positions. It goes long when prices rise and goes short when prices fall. The system also has the function of reversal trading.

## Strategy Logic

The strategy uses the T3 indicator to determine the direction of the price trend. The T3 indicator is an adaptive moving average with higher sensitivity that can respond to price changes faster. Its calculation formula is:  

T3(n) = GD(GD(GD(n)))

Where GD represents the generalized DEMA (double exponential moving average), which is calculated as:  

GD(n,v) = EMA(n) * (1+v)-EMA(EMA(n)) * v  

v is the volume factor, which determines the sensitivity of the moving average's response to linear price trends. When v=0, GD=EMA; when v=1, GD=DEMA. The author suggests setting v=0.7.  

The strategy compares the T3 indicator with the price. When T3 crosses above the price, it determines an upward price trend and goes long. When T3 crosses below the price, it determines a downward price trend and goes short.


## Advantages  

- Uses adaptive moving average T3 indicator, sensitive to price trend changes  
- Automatically determines price trend direction, no manual judgment needed
- Configurable reversal trading, flexible to cope with market changes


## Risks  

- T3 indicator may have difficulty determining trend direction during range-bound consolidation
- Adaptive moving average indicators tend to produce false signals  
- Risk control for reversal trading needs to be cautious  

This can be mitigated by adjusting T3 parameters or adding other indicators for filtration, as well as setting stop loss to control single loss.

## Optimization Directions

- Add other indicators for filtration, such as MACD, RSI etc for combination  
- Add trend judgment rules to avoid false operations during sideways markets  
- Optimize parameters, adjust v value for better parameter combination
- Add stop loss logic  

## Summary  

The strategy automatically determines the price trend direction through the T3 indicator, without the need for manual judgment, and can automatically go long or short. It can also be configured for reversal trading to cope with more complex market situations. There is room for optimizing parameters, trading logic etc. to make the strategy perform even better.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Length|
|v_input_2|0.7|b|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-18 00:00:00
end: 2024-01-17 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.00 29/11/2017
// This indicator plots the moving average described in the January, 1998 issue
// of S&C, p.57, "Smoothing Techniques for More Accurate Signals", by Tim Tillson.
// This indicator plots T3 moving average presented in Figure 4 in the article.
// T3 indicator is a moving average which is calculated according to formula:
//     T3(n) = GD(GD(GD(n))),
// where GD - generalized DEMA (Double EMA) and calculating according to this:
//     GD(n,v) = EMA(n) * (1+v)-EMA(EMA(n)) * v,
// where "v" is volume factor, which determines how hot the moving average’s response
// to linear trends will be. The author advises to use v=0.7.
// When v = 0, GD = EMA, and when v = 1, GD = DEMA. In between, GD is a less aggressive
// version of DEMA. By using a value for v less than1, trader cure the multiple DEMA
// overshoot problem but at the cost of accepting some additional phase delay.
// In filter theory terminology, T3 is a six-pole nonlinear Kalman filter. Kalman
// filters are ones that use the error — in this case, (time series - EMA(n)) — 
// to correct themselves. In the realm of technical analysis, these are called adaptive
// moving averages; they track the time series more aggres-sively when it is making large
// moves. Tim Tillson is a software project manager at Hewlett-Packard, with degrees in
// mathematics and computer science. He has privately traded options and equities for 15 years.   
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="T3 Averages", shorttitle="T3", overlay = true)
Length = input(5, minval=1)
b = input(0.7, minval=0.01,step=0.01) 
reverse = input(false, title="Trade reverse")
xPrice = close
xe1 = ema(xPrice, Length)
xe2 = ema(xe1, Length)
xe3 = ema(xe2, Length)
xe4 = ema(xe3, Length)
xe5 = ema(xe4, Length)
xe6 = ema(xe5, Length)
c1 = -b*b*b
c2 = 3*b*b+3*b*b*b
c3 = -6*b*b-3*b-3*b*b*b
c4 = 1+3*b+b*b*b+3*b*b
nT3Average = c1 * xe6 + c2 * xe5 + c3 * xe4 + c4 * xe3
pos = iff(nT3Average > close, -1,
       iff(nT3Average < close, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )  
plot(nT3Average, color=blue, title="T3")
```

> Detail

https://www.fmz.com/strategy/439268

> Last Modified

2024-01-18 16:21:40
