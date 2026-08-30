
> Name

Bull-Power-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/8720436b76ac76473f.png)
[trans]

## Overview
The Bull Power Trading Strategy is a trend following strategy based on the "Bull Bear Balance Indicator". This strategy calculates the relationship between the current K line and the previous K line to determine whether the current market is in a long or short state, and then performs corresponding buying or selling operations.
## Strategy Principle
The core indicator of this strategy is value, which determines the long and short status of the market by comparing the closing price, opening price, highest price and lowest price of the current K line.
The specific calculation formula is as follows:
If closing price < opening price:
If the closing price of the previous K line < the opening price of the current K line:
        value = max (highest price - closing price of the previous K line, closing price - lowest price)
    Otherwise:
        value = max(highest price - opening price, closing price - lowest price)
If closing price > opening price:
If the closing price of the previous K line > the opening price of the current K line:
        value = highest price - lowest price
    Otherwise:
        value = max (opening price - closing price of the previous K line, highest price - lowest price)
If closing price == opening price:
If high price - closing price > closing price - low price:
        If the closing price of the previous K line < the opening price of the current K line:
            value = max (highest price - closing price of the previous K line, closing price - lowest price)
        Otherwise:
            value = highest price - opening price
If highest price - closing price < closing price - lowest price:
        If the closing price of the previous K line > the opening price of the current K line:
            value = highest price - lowest price
        Otherwise:
            value = max (opening price - closing price of the previous K line, highest price - lowest price)    
Otherwise:
        If the closing price of the previous K line > the opening price of the current K line:
            value = max(highest price - opening price, closing price - lowest price)
        Otherwise:
            value = max (opening price - closing price of the previous K line, highest price - lowest price)
The main idea of ​​this formula is to determine the long and short status of the current K line by comparing the size relationship of prices. If the closing price is lower than the opening price, it represents a short position; if the closing price is higher than the opening price, it represents a long position.
Compare the calculated value with the two input parameters SellLevel and BuyLevel. If value is greater than SellLevel, it means the market is short; if value is less than BuyLevel, it means the market is long.
Based on the comparison results, perform corresponding buying or selling operations.
## Strategic Advantages
1. This strategy responds quickly and can quickly capture the turning point of the trend and adjust positions in a timely manner.
2. By dynamically calculating the relationship between the current K line and the previous K line, we can judge the market long and short in real time without relying on fixed indicators.
3. The strategy has fewer parameters. SellLevel and BuyLevel directly affect the specific transaction logic and are easy to understand and adjust.
4. The reverse transaction and normal transaction logic can be flexibly adjusted to suit different market environments.
## Strategy Risk
1. This strategy is sensitive to emergencies and may produce too many invalid transactions.
2. The calculation of the value indicator is complex and may fail in some extreme cases, resulting in false signals.
3. Operating based only on one custom indicator has high systemic risks.
4. Failure to consider stop loss logic may result in larger losses.
These risks can be reduced by appropriately relaxing the buying and selling conditions, adding a stop-loss mechanism, or using it in combination with other indicators.
## Strategy optimization direction
1. Combine with other indicators to filter trading signals, such as MACD, KDJ, etc., to avoid wrong transactions.
2. Add liquidity indicators to avoid misplaced trading during periods of high volatility.
3. Optimize the settings of parameters SellLevel and BuyLevel to adapt to different cycles and varieties.
4. Add a stop loss strategy to control single losses.
5. Combine the VIX indicator to determine market volatility. Different parameters are used in different market environments.
## Summarize
The bull market power trading strategy is a real-time long and short judgment indicator based on the price relationship between the current K line and the previous K line. It can quickly respond to market changes and capture trend turning points. The strategy is simple and easy to understand and implement, but it is only based on a custom complex indicator and can be optimized in a variety of ways to make its parameters better adapt to the market environment, filter out false signals, and control risks. Generally speaking, this strategy is suitable for short-term operators who pursue high response speed.
||

## Overview

The Bull Power trading strategy is a trend following strategy based on the "Bull and Bear Balance Indicator". By calculating the relationship between the current K-line and previous K-line, the strategy judges whether the current market is bullish or bearish and makes corresponding buy or sell decisions.

## Strategy Logic

The core indicator of this strategy is value. By comparing the close price, open price, highest price and lowest price of the current K-line, it determines the bullish/bearish status of the market. 

The specific formula is as below:

If Close < Open:

    If Previous Close < Current Open:  
        value = max(Highest - Previous Close, Close - Lowest)
    Else:
        value = max(Highest - Open, Close - Lowest)

If Close > Open:

    If Previous Close > Current Open:
        value = Highest - Lowest
    Else: 
        value = max(Open - Previous Close, Highest - Lowest)

If Close == Open:

    If Highest - Close > Close - Lowest:
        If Previous Close < Current Open:
            value = max(Highest - Previous Close, Close - Lowest)
        Else:
            value = Highest - Open

    If Highest - Close < Close - Lowest:
        If Previous Close > Current Open:
            value = Highest - Lowest
        Else: 
            value = max(Open - Previous Close, Highest - Lowest)
    
    Else:
        If Previous Close > Current Open:
            value = max(Highest - Open, Close - Lowest)
        Else:
            value = max(Open - Previous Close, Highest - Lowest)

The main idea is to judge the current K-line's bull/bear status by comparing price relationships. If Close < Open, it indicates bearishness. If Close > Open, it indicates bullishness.

Compare the calculated value with input parameters SellLevel and BuyLevel. If value is greater than SellLevel, the market is bearish. If value is less than BuyLevel, the market is bullish. 

Make corresponding buy or sell decisions based on the comparison result.

## Advantages

1. The strategy responds quickly and captures trend turning points in a timely manner.

2. It calculates relationship between the current K-line and previous K-line in real time to determine the market condition instead of relying on fixed indicators.

3. The strategy has few parameters which directly affect the trading logic and are easy to understand.

4. It allows flexible configuration of reverse trade logic for different market environments.

## Risks

1. The strategy is sensitive to sudden events and may generate excessive invalid trades. 

2. The value calculation is complex. It may fail in extreme cases and cause wrong signals.

3. It relies solely on a custom complex indicator, resulting in higher systemic risks.

4. No stop loss logic may lead to huge losses.

These risks can be reduced by relaxing buy/sell criteria, adding stop loss mechanisms or combining with other indicators.

## Improvement Areas

1. Incorporate other indicators to filter trade signals, e.g. MACD, KDJ etc.

2. Add liquidity indicator to avoid misaligned trading during high volatility periods.

3. Optimize SellLevel and BuyLevel parameters for different cycles and products.  

4. Add stop loss strategy to control single trade loss.

5. Use VIX to determine market volatility and adopt adaptive parameters.

## Conclusion

The Bull Power trading strategy makes real-time judgment of market bullish/bearish status based on price relationships between the current K-line and previous K-line. It captures trend changes quickly. The strategy itself is simple to understand but relies solely on a complex custom indicator. It can be optimized in various ways to make parameters adaptive to market conditions, filter false signals and control risks. In summary, this strategy suits short-term traders pursuing high response speed.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|40|SellLevel|
|v_input_2|3|BuyLevel|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-12 00:00:00
end: 2024-01-11 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 30/01/2017
//  Bull Power Indicator
//  To get more information please see "Bull And Bear Balance Indicator" 
//  by Vadim Gimelfarb. 
////////////////////////////////////////////////////////////
strategy(title = "Bull Power Strategy")
SellLevel = input(40, step=0.01)
BuyLevel = input(3, step=0.01)
reverse = input(false, title="Trade reverse")
hline(SellLevel, color=red, linestyle=line)
hline(BuyLevel, color=green, linestyle=line)
value = iff (close < open ,  
         iff (close[1] < open ,  max(high - close[1], close - low), max(high - open, close - low)),
          iff (close > open, 
           iff(close[1] > open,  high - low, max(open - close[1], high - low)), 
             iff(high - close > close - low, 
              iff (close[1] < open, max(high - close[1], close - low), high - open), 
               iff (high - close < close - low, 
                 iff(close[1] > open,  high - low, max(open - close, high - low)), 
                  iff (close[1] > open, max(high - open, close - low),
                   iff(close[1] < open, max(open - close, high - low), high - low))))))
pos = iff(value > SellLevel, -1,
	     iff(value <= BuyLevel, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))
if (possig == -1) 
    strategy.entry("Short", strategy.short)
if (possig == 1)
    strategy.entry("Long", strategy.long)
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(value, style=line, linewidth=2, color=blue)
```

> Detail

https://www.fmz.com/strategy/438467

> Last Modified

2024-01-12 12:02:49
