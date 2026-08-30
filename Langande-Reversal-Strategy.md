
> Name

Langande-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]
## Overview
The Langander reversal strategy uses the Langander indicator to identify potential turning points in the price, and combines the closing price to determine the trend reversal, so as to carry out buying and selling operations at the trend reversal point.
## Principle
This strategy uses two functions from the Langender indicator, pivothigh and pivotlow, to identify highs and lows.
The pivothigh function is used to find the maximum value of the highest price of the past n K lines, which is the potential resistance; the pivotlow function is used to find the minimum value of the lowest price of the past n K lines, that is, the potential support.
Afterwards, by judging the conditions of high points and low points, the K-line where the price reaches a new high or a new low is identified, indicating a potential trend reversal point. Buy at new highs and sell at new lows.
## Advantages
- Using the Langender indicator to identify key points can improve the reliability of trading signals.
- Make judgments based on the actual closing price to avoid being misled by false breakthroughs in the middle.
- The strategy logic is clear, easy to understand and easy to implement.
## Risk
- Improper parameter settings may lead to frequent transactions, increased transaction costs and slippage losses.
- Multiple false breakthroughs may occur in the short term, causing unnecessary trading losses.
- Deep pullbacks may occur in long-term trends, causing the strategy to generate false signals.
## Optimization direction
- Consider adding other indicator filters, such as moving averages, to improve signal accuracy.
- The value of parameter n can be optimized to balance trading frequency and signal quality.
- Stop loss logic can be added to control the maximum loss of a single transaction.
## Summarize
The Langander reversal strategy is relatively simple and straightforward overall. Because it only uses the Langander indicator, certain false signals may appear. You can reduce risks and improve strategy stability by adding auxiliary indicators, optimizing parameters, and setting stop losses. This strategy is suitable for counter-trend trading and market environments with clear trends.
 ||


## Overview

The Langande reversal strategy uses the Langande indicator to identify potential turning points in price and combines it with closing price to determine trend reversal, in order to buy and sell at trend reversal points.

## Principle 

The strategy uses the two functions pivothigh and pivotlow in the Langande indicator to identify high and low points. 

The pivothigh function is used to find the maximum value of the highest prices over the past n bars, i.e. the potential resistance. The pivotlow function is used to find the minimum value of the lowest prices over the past n bars, i.e. the potential support.

Then, through the condition judgement of high and low points, it identifies the bars when new highs or lows are made, indicating potential trend reversal points. It buys on the new high points and sells on the new low points.

## Advantages

- Using the Langande indicator to identify key points can improve the reliability of trading signals.

- Judging based on actual closing prices avoids being misled by intermediate false breakouts. 

- The strategy logic is clear and easy to implement.

## Risks

- Improper parameter settings may lead to frequent trading, increasing transaction costs and slippage loss.

- There could be multiple false breakouts in the short term, causing unnecessary trading losses.

- Deep pullbacks may occur in long term trends, causing the strategy to generate incorrect signals.

## Optimization Directions 

- Consider adding other filters like moving averages to improve signal accuracy.

- Optimize the value of n to balance trading frequency and signal quality.

- Add stop loss logic to control maximum loss per trade.

## Summary

The Langande reversal strategy is relatively simple and direct. Due to its sole reliance on the Langande indicator, some false signals may occur. Risks can be reduced and stability improved by adding auxiliary indicators, optimizing parameters, and setting stops. The strategy is suitable for counter-trend trading and markets where the trend is relatively clear.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|leftBars|
|v_input_2|2|rightBars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-17 00:00:00
end: 2023-09-16 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("lokendra Reversal Strategy", overlay=true)

leftBars = input(4)
rightBars = input(2)

swh = pivothigh(leftBars, rightBars)
swl = pivotlow(leftBars, rightBars)

swh_cond = not na(swh)

hprice = 0.0
hprice := swh_cond ? swh : hprice[1]

le = false
le := swh_cond ? true : (le[1] and high > hprice ? false : le[1])

if (le)
    strategy.entry("PivRevLE", strategy.long, comment="BUY**", stop=hprice + syminfo.mintick)

swl_cond = not na(swl)

lprice = 0.0
lprice := swl_cond ? swl : lprice[1]


se = false
se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])

if (se)
    strategy.entry("PivRevSE", strategy.short, comment="SELL**", stop=lprice - syminfo.mintick)

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/427062

> Last Modified

2023-09-17 18:10:02
