
> Name

Pivot-Points-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/161eec6574e30bf6e4b.png)

[trans]

## Overview
Pivot Points Breakout Strategy is a quantitative trading strategy that determines market trends and conducts trading operations based on the pivot points calculated from the previous day's highest price, lowest price, and closing price, as well as the upper and lower rails. The main idea of ​​this strategy is that if the price breaks through the upper band, go long; if the price breaks through the lower band, go short.
## Strategy Principle
The calculation formula for the pivot point breakout strategy is as follows:
Pivot Price (PP) = (previous day’s highest price + previous day’s lowest price + previous day’s closing price)/3
First Resistance (R1) = (pivot point price * 2) - the lowest price of the previous day
Lower track support line (First Support, S1) = (pivot point price * 2) - the highest price of the previous day
The judgment logic of trading signals is:
If the closing price > the upper resistance line R1, go long
If the closing price < the lower support line S1, go short
The main advantages of this strategy are:
1. Use the data of the previous day to calculate the pivot point, which is responsive
2. The probability of breaking through the upper and lower rails to form a strong trend is high
3. The policy rules are simple, clear and easy to implement
## Advantage Analysis
The pivot point breakout strategy has several advantages:
1. The calculation formula is simple and easy to implement. Pivot points and upper and lower rails can be calculated using only the previous day's high, low and closing prices.
2. Respond quickly. Pivot points and upper and lower rails are updated daily, allowing you to quickly capture price changes.
3. Capture trends early. The price breaking through the upper and lower rails represents a major change and may form a new trend.
4. The retracement is small. Setting a stop loss can limit the risk of loss.
5. Easy to optimize. Parameters can be adjusted, such as calculating pivot points using different periodic data.
## Risk Analysis
There are also some risks associated with the pivot point breakout strategy:
1. Risk of false breakthroughs. There may be temporary false breakthroughs in price, resulting in trading losses.
2. Risk of market shock. When the market fluctuates for a long time, the price may touch the upper and lower rails multiple times, causing losses.
3. param risk. If the parameters are set improperly, such as the trading cycle is too short, losses may also increase.
Countermeasures:
1. Set stop loss and stop profit to strictly control risks.
2. Optimize parameters and adjust cycle length.
3. Filter signals in combination with other indicators.
## Optimization direction
The pivot point breakout strategy can also be optimized from the following aspects:
1. Cycle optimization. You can test calculating pivot points using longer periods such as weekly or monthly data.
2. Parameter optimization. You can test and adjust the values ​​of the upper and lower rail parameters, such as 1.5 or 2.5, etc.
3. Filter optimization. Filter error signals using indicators such as moving averages.
4. Optimize risk control. Set up a dynamic stop-loss and stop-profit mechanism and adjust the stop-loss position according to market changes.
## Summarize
The pivot point breakout strategy is generally a relatively simple and practical trend following strategy. It responds quickly to market changes and can effectively capture the formation of new trends. But there is also a certain risk of false signals. Through parameter optimization, signal filtering and risk control methods, potential risks can be controlled while maintaining its advantages, and the stability of the strategy and profitability can be improved.
||


## Overview

The Pivot Points Breakout Strategy is a quantitative trading strategy that uses pivot points calculated based on the previous day's high, low and close prices, as well as upper and lower rails, to determine market trends and make trading decisions. The main idea of this strategy is to go long when prices break through the upper rail and go short when prices break through the lower rail.

## Strategy Principle

The calculation formulas for the Pivot Points Breakout Strategy are as follows:

Pivot Price (PP) = (Previous day's high + Previous day's low + Previous day's close) / 3

First Resistance (R1) = (Pivot Price * 2) - Previous day's low  

First Support (S1) = (Pivot Price * 2) - Previous day's high

The logic for trade signals is: 

If close > First Resistance (R1), go long

If close < First Support (S1), go short

The main advantages of this strategy are:

1. Uses previous day's data to calculate pivot points, responsive
2. High probability of forming strong trends after breaking through upper/lower rails 
3. Simple and clear strategy rules, easy to implement

## Advantage Analysis   

The Pivot Points Breakout Strategy has the following advantages:

1. The calculation formula is simple and easy to implement. It only requires the previous day's high, low and close prices to calculate the pivot points and upper/lower rails.  

2. It responds quickly. The pivot points and upper/lower rails update daily and can quickly capture price changes.

3. It captures trends early. Prices breaking through the upper/lower rails represent significant changes that may form new trends.  

4. It has small drawdowns. Setting stop loss can limit downside risk.

5. It is easy to optimize. Parameters can be adjusted such as using different period data to calculate the pivot points.

## Risk Analysis

The Pivot Points Breakout Strategy also has some risks:

1. Wrong breakout risk. Prices may temporarily break out incorrectly, leading to trading losses.

2. Market fluctuation risk. When the market fluctuates for an extended time, prices may touch the upper/lower rails multiple times leading to losses.  

3. Parameter risk. If parameters are set inappropriately, such as the trading period is too short, it may also increase losses.

Countermeasures:

1. Set stop loss/take profit to strictly control risks.

2. Optimize parameters, adjust cycle length.  

3. Combine with other indicators to filter signals.

## Optimization Directions   

The Pivot Points Breakout Strategy can also be optimized in the following aspects:

1. Cycle optimization. Test using longer cycle data such as weekly or monthly to calculate the pivot points.

2. Parameter optimization. Test adjusting the parameter values for the upper/lower rails, such as 1.5 or 2.5 etc.

3. Filter optimization. Combine with moving averages and other indicators to filter erroneous signals.   

4. Risk control optimization. Set dynamic stop loss/take profit mechanisms, adjust stop loss price based on market changes.

## Conclusion

Overall, the Pivot Points Breakout Strategy is a relatively simple and practical trend following strategy. It responds quickly to market changes and can effectively capture new trend formations. But there are also certain risks of wrong signals. By optimizing parameters, filtering signals and implementing risk control measures, the advantages can be maintained while controlling potential risks to improve the stability and profitability of the strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-05 00:00:00
end: 2023-12-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 27/06/2018
// The name ‘Floor-Trader Pivot,’ came from the fact that Pivot points can 
// be calculated quickly, on the fly using price data from the previous day 
// as an input. Although time-frames of less than a day can be used, Pivots are 
// commonly plotted on the Daily Chart; using price data from the previous day’s 
// trading activity. 
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Floor Pivot Points Backtest", shorttitle="FPP", overlay = true)
xHigh  = request.security(syminfo.tickerid,"D", high[1])
xLow   = request.security(syminfo.tickerid,"D", low[1])
xClose = request.security(syminfo.tickerid,"D", close[1])
reverse = input(false, title="Trade reverse")
vPP = (xHigh+xLow+xClose) / 3
vR1 = (vPP * 2) - xLow
vS1 = (vPP * 2) - xHigh
pos = iff(close > vR1, 1,
       iff(close < vS1, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
```

> Detail

https://www.fmz.com/strategy/435151

> Last Modified

2023-12-12 16:47:17
