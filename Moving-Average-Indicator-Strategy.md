
> Name

A Moving Average Indicator Strategy-Moving-Average-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/dd1200efc6cef248a3.png)
[trans]
## Overview
The moving average indicator strategy is a quantitative trading strategy that determines the market trend based on the moving average and performs long or short positions. This strategy calculates the average closing price of a certain period to determine whether the market is overbought or oversold to capture price reversal opportunities.
## Strategy Principle
The core indicator of this strategy is the Stochastic Oscillator. The calculation method is:
```
低点 = 最近N天的最低价中的最低值 
高点 = 最近N天的最高价中的最高值
K值 = (当前close - 低点)/(高点 - 低点)* 100
```

Among them, the N value is the length Length. This indicator roughly reflects the position of the current closing price relative to the price range of the last N days.
When the K value is greater than the overbought line (BuyBand), it means that the stock price may be overbought and a correction will occur; when the K value is less than the oversold line (SellBand), it means that the stock price may be oversold and a rebound will occur.
According to this judgment rule, this strategy will open a position by selling in the overbought area and buying in the oversold area. The condition for closing the position is that the indicator line re-enters the middle area ((SellBand, BuyBand)).
## Advantage Analysis
This strategy has the following advantages:
1. Use the moving average indicator to judge market trends. The backtesting effect is better and it is easy to form trading signals.
2. By adjusting parameters, it can be flexibly adapted to different cycles and varieties.
3. The strategic ideas are simple and clear, easy to understand and optimize
## Risk Analysis
There are also some risks with this strategy:
1. The moving average is prone to mis-touching, and overbought and oversold signals may be "dumped".
2. Improper parameter settings may lead to frequent transactions or unclear signals.
3. Only considering a single indicator, the space for optimization is limited.
These risks can be reduced by appropriately optimizing indicator parameters or adding filter conditions.
## Optimization direction
This strategy can mainly be optimized from the following aspects:
1. Add indicator filtering such as volume or ATR to ensure more reliable trading signals
2. Add Stoch indicators of multiple periods and perform combined operations to generate signals
3. Add additional judgment indicators, such as MACD, KDJ, etc., to achieve multi-indicator aggregation
4. Traverse and optimize trading types, cycles, and parameters to find the best configuration
## Summarize
The overall idea of ​​the moving average indicator strategy is simple, widely used, and the backtesting effect is relatively stable. It is suitable as one of the introductory strategies for quantitative trading. However, this strategy considers a single factor and has limited room for optimization, so it is only suitable for short-term operations. In the future, it can be upgraded through multi-index aggregation, machine learning and other means.
||

## Overview  

The Moving Average Indicator strategy is a quantitative trading strategy that judges market trends based on moving averages and conducts long or short position operations. By calculating the average closing price over a period of time, this strategy determines whether the market is overbought or oversold in order to capture price reversal opportunities.  

## Strategy Principle  

The core indicator of this strategy is the Stochastic Oscillator. Its calculation method is:  

```
Low = the lowest low of the most recent N days  
High = the highest high of the most recent N days
K value = (Current close – Low)/(High – Low)*100
```

Where N is the length Length. This indicator roughly reflects the position of the current closing price relative to the price range over the most recent N days.  

When the K value is greater than the overbought line (BuyBand), it indicates that the stock may be overbought and a callback will occur. When the K value is less than the oversold line (SellBand), it indicates that the stock may be oversold and a rebound will occur.  

According to this judgment rule, the strategy will sell to open a position in the overbought zone and buy to open a position in the oversold zone. The closing condition is that the indicator line re-enters the intermediate zone ((SellBand, BuyBand)).  

## Advantage Analysis  

This strategy has the following advantages:  

1. Using moving average indicators to determine market trends, good backtesting results, easy to form trading signals  
2. Flexible to adapt to different cycles and varieties by adjusting parameters  
3. The strategy idea is simple and clear, easy to understand and optimize  

## Risk Analysis  

The strategy also poses some risks:   

1. Moving averages are prone to false touches, possibly being "whipsawed”  
2. Improper parameter settings can lead to frequent trading or unclear signals
3. Only one indicator is considered, limited optimization space  

These risks can be reduced by appropriately optimizing indicator parameters or adding filter conditions.  

## Optimization Directions   

The main aspects that this strategy can be optimized include:  

1. Add volume or ATR and other indicators to ensure more reliable trading signals  
2. Add Stoch indicators of multiple cycles, generate signals through composite operations  
3. Increase additional judgment indicators such as MACD and KDJ to achieve multi-indicator aggregation  
4. Traverse and optimize trading varieties, cycles, parameters to find the optimal configuration  

## Conclusion  

The overall idea of the Moving Average Indicator strategy is simple and widely used with relatively stable backtesting results, making it suitable as a beginner’s quantitative trading strategy. However, this strategy has limited optimization space as it considers limited factors and is only suitable for short-term operations. Future upgrades can be made through multi-indicator aggregation, machine learning, etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Length|
|v_input_2|0.92|BuyBand|
|v_input_3|0.5|SellBand|
|v_input_4|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 25/09/2017
// Simple Overbought/Oversold indicator
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Overbought/Oversold", shorttitle="OB/OS")
Length = input(10, minval=1)
BuyBand = input(0.92, step = 0.01)
SellBand = input(0.5, step = 0.01)
reverse = input(false, title="Trade reverse")
hline(BuyBand, color=green, linestyle=line)
hline(SellBand, color=red, linestyle=line)
xOBOS = stoch(close, high, low, Length)
nRes = iff(close > close[Length], xOBOS / 100, (100 - xOBOS) / 100)
pos = iff(nRes < SellBand, -1,
	   iff(nRes > BuyBand, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=blue, title="OB/OS")
```

> Detail

https://www.fmz.com/strategy/442815

> Last Modified

2024-02-26 11:10:23
