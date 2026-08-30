
> Name

Breakthrough-Highs-and-Lows-Backtesting-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/6d3826a679658e5d0d.png)
[trans]

### Overview
This strategy is based on breaking through the high and low points of the cycle to determine the direction of the trend. It goes long when the price breaks through the high point of the cycle and goes short when it breaks through the low point of the cycle. It is a trend following strategy.
### Strategy Principles
This strategy first reads the period set by the user (daily line, weekly line, etc.) and the number of lookback periods. Then based on these parameters, the highest price and lowest price of the lookback period are obtained. For example, if it is set to a daily cycle and looks back 1 cycle, the highest price and lowest price of the previous day will be taken.
In actual trading, if the closing price is greater than or equal to the lowest price of the lookback period, it is judged to be an upward breakthrough and a long position is taken; if the closing price is less than or equal to the highest price of the lookback period, it is judged to be a downward breakthrough and a short position.
In this way, capturing the trend direction by breaking through the high and low points of the cycle is a type of trend following strategy.
### Advantage Analysis
This strategy mainly has the following advantages:
1. Determine the trend direction based on the breakthrough point, and it is easy to grasp the general trend after strong consolidation.
2. The operation is simple and easy to understand, which is very suitable for novices to learn and use.
3. The cycle parameters can be easily optimized and adjusted, suitable for different varieties.
4. Reverse operations can be set through reverse input to enrich the application of strategies.
5. Draw cycle high and low points to assist judgment and form multiple verifications.
### Risk Analysis
There are also some risks with this strategy:
1. Unable to effectively filter oscillations and consolidation, and multiple misoperations may occur.
2. Unable to control stop loss, there is a certain degree of risk of loss.
3. Sensitive to transaction costs, there is a certain deviation in actual profit and loss.
4. The position size cannot be limited, and there is an overage problem.
In response to the above risks, you can set up a stop-loss mechanism, optimize filtering conditions, control the number of positions, and other methods for optimization.
### Optimization direction
This strategy can be optimized mainly from the following directions:
1. Add a filtering mechanism to avoid frequent opening of positions during shock and consolidation. Filter conditions such as price channels and volatility can be set.
2. Set a trailing stop or time stop. Control the risk of single loss and ensure overall profitability.
3. Optimize position size and fund management to prevent over-capacity problems and ensure strategy stability.
4. Test the effects of different cycle parameters and select the optimal parameter combination.
5. Add an algorithmic trading module and use machine learning algorithms to improve decision-making efficiency.
### Summarize
In general, this backtesting strategy for breaking through high and low points is based on trend tracking to determine the direction. It is simple and easy to operate and suitable for novices to learn, but there is a risk of difficulty in arbitrage. By adding filtering conditions, stop loss mechanisms, position control and other optimization methods, these risks can be mitigated and the strategy can be more effective. This strategy can provide us with ideas and reference for further research and improvement.
||

### Overview

This strategy judges trend direction based on breaking through periodic highs and lows. It goes long when price breaks through the periodic high and goes short when price breaks below the periodic low. It belongs to the trend tracking strategy.

### Principle  

The strategy first reads the user-defined cycle (daily, weekly, etc.) and lookback periods. Then it gets the highest and lowest prices for the lookback period based on these parameters. For example, if it is set to daily cycle and lookback 1 period, it takes the highest and lowest prices for the previous day.

In actual trading, if the closing price is greater than or equal to the lowest price of the lookback period, it is judged as an upward breakthrough and it goes long. If the closing price is less than or equal to the highest price of the lookback period, it is judged as a downward breakthrough and it goes short.  

By capturing the trend direction through breaking through periodic highs and lows, this strategy belongs to a kind of trend tracking strategy.

### Advantage Analysis  

The main advantages of this strategy are:

1. Capturing the big trend after strong consolidation by judging direction based on breakthrough points.  

2. Simple and easy to understand, very suitable for beginners to learn and use.

3. Easy to optimize by adjusting periodic parameters, applicable to different varieties.  

4. Can set reverse input for reverse operation, enriching strategy use.

5. Drawing periodic highs and lows to assist judgement and form multi-validation.

### Risk Analysis

There are also some risks:

1. Cannot effectively filter sideways volatility, possible multiple mis-operations.

2. Cannot control stop loss, certain degree of loss risk exists.

3. Sensitive to trading costs, actual PnL may deviate.  

4. Cannot limit position size, over-trading risk exists.

To address these risks, methods like setting stop loss, optimizing filter conditions, controlling position size can be used.

### Optimization  

The main optimization directions are:  

1. Adding filter mechanisms to avoid frequent opening during sideways. Set price channel, volatility filters etc.

2. Set trailing stop loss or time stop loss to control single loss risk and ensure overall profitability.

3. Optimize position sizing and money management to prevent over-trading and ensure stability.  

4. Test effects of different periodic parameters and select optimal parameter combinations.

5. Increase algorithmic trading modules, use machine learning algorithms to improve decision efficiency.

### Summary  

In summary, this breakthrough high low backtest strategy is simple to operate based on trend tracking, suitable for beginners to learn, but risks being trapped exist. By adding optimizations like filters, stops, position control, these risks can be reduced and strategy results improved. It can provide ideas and references for our further research and improvements.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|D|SelectPeriod|
|v_input_2|true|LookBack|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2024-01-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 03/07/2018
// This script shows a high and low period value.
//    Width - width of lines
//    SelectPeriod - Day or Week or Month and etc.
//    LookBack - Shift levels 0 - current period, 1 - previous and etc.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="High and Low Levels Backtest", shorttitle="HL Levels", overlay = true)
SelectPeriod = input("D", defval="D")
LookBack = input(1,  minval=0)
reverse = input(false, title="Trade reverse")
xHigh  = request.security(syminfo.tickerid, SelectPeriod, high[LookBack])
xLow   = request.security(syminfo.tickerid, SelectPeriod, low[LookBack])
vS1 = xHigh
vR1 = xLow
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

https://www.fmz.com/strategy/438051

> Last Modified

2024-01-08 16:13:44
