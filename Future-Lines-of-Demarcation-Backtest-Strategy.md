
> Name

Future-Lines-of-Demarcation-Backtest-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1addd7806136f18c9a8.png)
[trans]

### Overview
The main idea of ​​this strategy is to determine the direction of future prices by drawing a future price extension line and combining the relationship between the current price and this line. When the price is above or below the extension line, you can go long or short accordingly.
### Strategy Principles
Future Lines of Demarcation (FLD) represent the median price, highest price or lowest price in a specific period in the future. This strategy uses FLD to determine the future price trend. Its principle is:
1. Based on the period length, calculate the displacement period Period of FLD, which is the future price of Price.
2. Compare the current Close price with the price after the FLD displacement period.
    - When the Close price is lower than the future price of FLD, it is judged as a bullish signal.
    - When the Close price is higher than the future price of FLD, it is judged as a bearish signal.
3. Carry out corresponding long and short operations based on bullish and bearish signals.
### Advantage Analysis
The main advantages of this strategy are:
1. Use FLD to determine future price trends with high accuracy.
2. The cycle parameters can be customized and suitable for different market environments.
3. You can choose the median price, the highest price or the lowest price as the FLD drawing source, which is highly adaptable.
### Risk Analysis
The main risks of this strategy are:
1. The FLD itself may fail, resulting in missed opportunities or false signals. It can be judged in combination with other indicators.
2. Improper setting of period parameters may result in too many false signals. Cycle length needs to be optimized.
3. Unexpected events cause sharp price fluctuations, and FLD predictions become invalid. Stop losses can be set to control risk.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Combine with other indicators to filter signals to improve strategy accuracy. Such as MACD, KDJ, etc.  
2. Optimize cycle parameters and find the best parameter combination.
3. Add a stop-loss and stop-profit mechanism to control single losses and profits.
4. Based on the backtest results, adjust the long and short rules to reduce false signals.
### Summarize
This strategy determines the future price trend direction by comparing the price with the future price extension line after the displacement. It is a typical trend following strategy. Generally speaking, the logic is clear and easy to understand, and the implementation risk is small. Through parameter optimization and indicator combination, better strategy effects can be obtained.
||

### Overview

The main idea of this strategy is to predict the future price trend by drawing future price extension lines and comparing the current price with the lines. It can make long or short positions accordingly when the price is higher or lower than the extension line.  

### Strategy Principle

The Future Lines of Demarcation (FLD) represents the median, highest or lowest price in a certain future period. The strategy uses FLD to determine the future price movement. The principle is:

1. Calculate the displacement period Period of FLD based on cycle length, which is the future price of Price.  
2. Compare current Close price with FLD's future price at displacement period.
    - When Close price is lower than future FLD price, it is a bullish signal.
    - When Close price is higher than future FLD price, it is a bearish signal.
3. Make corresponding long or short positions based on bullish and bearish signals.

### Advantage Analysis 

The main advantages of this strategy:

1. Using FLD to determine future trend has high accuracy. 
2. Customizable cycle parameter, adaptable to different market environments.  
3. Can choose median, highest or lowest price as FLD source, high adaptability.

### Risk Analysis

The main risks of this strategy:  

1. FLD itself may fail, resulting in missing opportunities or wrong signals. Can combine other indicators.
2. Improper cycle parameter settings may cause excessive wrong signals. Need cycle length optimization.  
3. Sudden price fluctuations causing FLD prediction failure. Can set stop loss to control risk.

### Optimization Directions   

The strategy can be optimized in the following aspects:

1. Combine with other indicators to filter signals and improve accuracy, e.g. MACD, KDJ etc.
2. Optimize cycle parameters to find best combination. 
3. Add stop loss and take profit mechanisms to control single trade loss and profit.
4. Adjust long and short rules based on backtest results to reduce wrong signals.  

### Summary   

The strategy judges future price trend by comparing price with displaced future price extension line. It's a typical trend following strategy. The logic is clear and easy to understand, with relatively small implementation risk. By parameter optimization and indicator combination, good strategy results can be obtained.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|40|Period|
|v_input_2_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-29 00:00:00
end: 2024-02-04 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 15/02/2017
//  An FLD is a line that is plotted on the same scale as the price and is in fact the 
//  price itself displaced to the right (into the future) by (approximately) half the 
//  wavelength of the cycle for which the FLD is plotted. There are three FLD's that can be 
//  plotted for each cycle:
//    An FLD based on the median price.
//    An FLD based on the high price.
//    An FLD based on the low price.
///////////////////////////////////////////////////////////////////
strategy(title="FLD's - Future Lines of Demarcation", overlay=true)
Period = input(title="Period", defval=40)
src = input(title="Source", defval=hl2)
reverse = input(false, title="Trade reverse")
FLD = src
pos = iff(FLD[Period] < close , 1,
       iff(FLD[Period] > close, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
         iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue)
plot(FLD, title="FLD", style=line, linewidth=1, color=black, offset = Period)
```

> Detail

https://www.fmz.com/strategy/441077

> Last Modified

2024-02-05 14:00:01
