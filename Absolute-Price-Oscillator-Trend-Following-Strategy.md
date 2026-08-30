
> Name

Absolute-Price-Oscillator-Trend-Following-Strategy Absolute-Price-Oscillator-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy utilizes the Absolute Price Oscillator (APO) indicator to generate trading signals and enable trend following trading. The APO indicator calculates the difference between two exponential moving averages of different periods to obtain the oscillator, and performs long and short positions based on its value crossing above or below.
## Strategy Principle
- The APO indicator consists of a short-term and long-term EMA, and the difference between the two is calculated.
- Go long when APO crosses the buying zone (default 3), go short when APO crosses the selling zone (default -3).
- You can choose reversal signals, go short when APO crosses up, and go long when it crosses down.
- The indicator curve represents price momentum and can be used to look for trend reversal signals formed by divergences.
This strategy is a trend following strategy that uses the APO indicator to determine the price trend direction and generate continuous long and short signals. After the indicator parameters are optimized, the mid-term trend of the general trend can be tracked.
## Strategic Advantages
- Easy to implement using a simple combination of moving average indicators.
- Use the APO indicator to determine price momentum and direction.
- Default parameters generate medium-term continuation signals to avoid over-trading.
- Can look for trend reversal opportunities when price deviates from APO.
## Strategy Risk
- False signals and whipsaws are prone to occur in consolidation markets.
- There is some lag and rapid reversals may be missed.
- There is no stop loss and position management, and risk control is incomplete.
Risk response measures:
- Optimize parameters and test suitable parameter combinations for different varieties.
- Added additional filters to avoid trading in volatile markets.
- Set stop loss strategies, such as trailing stop loss, etc.
## Strategy optimization direction
- Perform parameter optimization for each trading variety individually to find the best parameter pair.
- Add filter conditions such as price conditions or trading volume to reduce false signals.
- Dynamic position management based on volatility or balance ratio.
- Optimize the take-profit method and set trend-following take-profit.
- Apply machine learning algorithms to determine the success rate of indicator divergence signals.
## Summarize
This strategy is based on the APO indicator and implements trend following trading based on moving average crossovers. After optimizing parameters and risk control, it can become an effective quantitative trading system. The core idea is simple and reliable and deserves further development and improvement.
|| 

## Overview

This strategy uses the Absolute Price Oscillator (APO) indicator to generate trading signals and follow trends. The APO calculates the difference between two EMAs and trades crossovers above/below zero.

## Strategy Logic

- APO consists of a faster and slower EMA, taking the difference between them.

- When APO crosses above the buy zone (default 3), go long. When it crosses below the sell zone (default -3), go short.

- Option to reverse signals - cross above sells, cross below buys.

- Curve shows price momentum, can find reversals on divergence.

This is a trend following strategy, using APO to determine trend direction for sustained long/short signals. Optimized parameters can track medium-term trends.

## Advantages

- Simple implementation using basic moving average combination.

- APO gauges price momentum and direction. 

- Default parameters generate medium-term sustained signals, avoiding over-trading.

- Can detect trend reversals based on price/indicator divergence.

## Risks 

- Prone to false signals and whipsaws in ranging markets.

- Lagging signals may miss quick reversals. 

- No stop loss or position sizing, incomplete risk management.

Mitigations:

- Optimize parameters and test different combinations per instrument.

- Add filters to avoid trading in choppy conditions. 

- Implement stop loss, e.g. trailing stop.

## Enhancement Opportunities

- Parameter optimization for each instrument to find ideal pairs.

- Additional filters on price action or volume to reduce false signals.

- Dynamic position sizing based on volatility or account %. 

- Optimized take profit such as trailing stop to follow trends.

- ML to assess probability of successful divergence signals. 

## Conclusion

This EMA crossover system using APO provides a solid foundation for trend following. With optimizations in parameters, risk management and filters, it can become an effective quantitative strategy. The core concept is simple and robust for further development.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|LengthShortEMA|
|v_input_2|20|LengthLongEMA|
|v_input_3|3|BuyZone|
|v_input_4|-3|SellZone|
|v_input_5|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-14 00:00:00
end: 2023-09-20 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 20/09/2018
// The Absolute Price Oscillator displays the difference between two exponential 
// moving averages of a security's price and is expressed as an absolute value.
// How this indicator works
//    APO crossing above zero is considered bullish, while crossing below zero is bearish.
//    A positive indicator value indicates an upward movement, while negative readings 
//      signal a downward trend.
//    Divergences form when a new high or low in price is not confirmed by the Absolute Price 
//      Oscillator (APO). A bullish divergence forms when price make a lower low, but the APO 
//      forms a higher low. This indicates less downward momentum that could foreshadow a bullish 
//      reversal. A bearish divergence forms when price makes a higher high, but the APO forms a 
//      lower high. This shows less upward momentum that could foreshadow a bearish reversal.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Absolute Price Oscillator (APO) Backtest 2.0", shorttitle="APO")
LengthShortEMA = input(10, minval=1)
LengthLongEMA = input(20, minval=1)
BuyZone = input(3, step = 0.01)
SellZone = input(-3, step = 0.01)
reverse = input(false, title="Trade reverse")
hline(BuyZone, color=green, linestyle=line)
hline(SellZone, color=red, linestyle=line)
hline(0, color=gray, linestyle=line)
xPrice = close
xShortEMA = ema(xPrice, LengthShortEMA)
xLongEMA = ema(xPrice, LengthLongEMA)
xAPO = xShortEMA - xLongEMA
pos = iff(xAPO > BuyZone, 1,
       iff(xAPO < SellZone, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )  
plot(xAPO, color=blue, title="APO")
```

> Detail

https://www.fmz.com/strategy/427479

> Last Modified

2023-09-21 15:27:59
