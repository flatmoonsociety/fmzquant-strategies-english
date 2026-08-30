
> Name

Williams-Alligator-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ac69f44667ed580f1b.png)

[trans]

## Overview
The Williams Alligator strategy is a trend following strategy that uses the "crocodile mouth" shape formed by three moving averages of different periods to determine the direction of the trend. When the fast line is higher than the middle line and the middle line is higher than the slow line, an alligator's mouth with an upward trend is formed, go long; when the fast line is lower than the middle line, and the middle line is lower than the slow line, an alligator's mouth with a downward trend is formed, go short. This strategy is based on the Alligator indicator invented by Bill Williams and combines the trend judgment ability of the moving average to effectively capture market trends.
## Strategy Principle
This strategy uses three SMA moving averages with different period lengths, namely fast line sma1, midline sma2 and slow line sma3. Among them, sma1 has the shortest period and sma3 has the longest period.
When sma1 crosses sma2, and sma2 crosses sma3, it indicates that the market is in an upward trend, forming an upward crocodile mouth. According to trend trading theory, you should enter the market at this time and do long.
On the contrary, when sma1 crosses sma2 and sma2 crosses sma3, it indicates that the market is in a downward trend, forming a downward crocodile mouth. At this time, you should enter the market to go short.
The exit conditions for long and short positions are that the three moving averages are rearranged, and the fast line is lower than the middle line or the middle line is lower than the slow line. At this time, the position should be closed.
The strategy also draws background colors to identify trend direction, with green representing an uptrend and red representing a downtrend.
Generally speaking, this strategy takes advantage of the moving average, uses the "crocodile's mouth" shape to determine the direction of the trend, and enters the market with the trend. It is a relatively typical trend following strategy.
## Advantage Analysis
- Use crocodile mouth judgment to effectively identify the trend direction.
- Using different combinations of periodic lines can improve the accuracy of morphological judgment. 
- Entering trades following the trend, in line with the trend trading theory.
- Set the background color to assist judgment and make it intuitively visible.
- The transaction logic is simple, clear and easy to implement.
## Risk Analysis
- In the large-cycle turbulent market, there is the risk of multiple adjustments.
- When the order of the three lines changes, the risk of closing the position is greater.
- It is impossible to judge the strength of the trend, and there are situations where trend entry is not suitable.
- Stop loss is not considered, and the risk of large retracements is greater.
- Fixed cycles cannot adapt to market changes, so adaptive cycles should be used.
In response to the above risks, the following measures can be taken to further optimize:
1. Add trend filter conditions to avoid frequent opening of positions in volatile markets.
2. Optimize exit conditions and determine the timing of closing positions based on trend indicators.
3. Add a stop-loss strategy to control single losses.
4. Use adaptive moving averages to dynamically adjust the period.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Increase the judgment of trend strength and avoid premature entry into stable or oscillating trends. MACD, KDJ and other auxiliary judgments can be introduced.
2. Optimize the moving average period parameters and find the best combination. The optimal parameters can be found by backtesting multiple sets of parameters.
3. Use adaptive moving averages to enable the cycle to change adaptively according to market momentum.
4. Add stop loss strategies, such as trailing stop loss, balance stop loss, etc., to control risks.
5. To optimize entry conditions, you can consider trading volume, Bollinger Bands and other indicators for filtering to improve entry accuracy.
6. Optimize exit conditions, combine trend indicators to determine the probability of trend reversal when the three lines cross, and reduce exit risks.
## Summarize
The Williams Alligator strategy is a typical trend following strategy. It uses three moving averages of fast, medium and slow to form an alligator's mouth to judge the direction of the trend and enter the market with the trend. The advantage of this strategy is that the trading logic is simple and clear, and it is easy to operate; the disadvantage is that the accuracy of trend judgment and risk control ability are weak. In the future, it can be improved by introducing auxiliary indicators, optimization parameters, stop losses, etc. to make the strategy more adaptable to complex market environments.
||


## Overview

Williams' Alligator Strategy is a trend following strategy that uses three moving average lines of different periods to form "alligator jaws" to determine the trend direction. When the fast line is above the middle line and the middle line is above the slow line, an upward trend alligator mouth is formed to go long. When the fast line is below the middle line and the middle line is below the slow line, a downward trend alligator mouth is formed to go short. It was invented by Bill Williams and combines the trend judging ability of moving averages to effectively capture market trends.

## How it Works

The strategy uses three SMAs of different period lengths - fast line sma1, middle line sma2, and slow line sma3, where sma1 has the shortest period and sma3 has the longest. 

When sma1 crosses above sma2, and sma2 crosses above sma3, it indicates the market is in an upward trend and forms an upward alligator mouth. According to trend trading theory, a long position should be entered.

Conversely, when sma1 crosses below sma2, and sma2 crosses below sma3, it indicates the market is in a downward trend and forms a downward alligator mouth. A short position should be entered.

The exit condition is when the three lines re-align, with the fast line below the middle line or the middle line below the slow line. Positions should be closed out.

The strategy also draws background colors to identify the trend direction - green for uptrend and red for downtrend.

In summary, the strategy utilizes the strengths of moving averages and "alligator mouth" patterns to determine trend direction and trade accordingly. It is a typical trend following strategy.

## Advantage Analysis

- Alligator mouth effectively identifies trend direction.
- Combination of different period lines improves pattern accuracy.
- Trading with the trend aligns with trend trading theory.  
- Background colors assist visual judgement.
- Simple and clear logic, easy to implement.

## Risk Analysis

- Multiple whipsaw risks in ranging markets.
- High risk when lines re-align to close out positions.
- Unable to determine trend strength, may incorrectly enter trends.
- No stop loss, high drawdown risk.  
- Fixed periods cannot adapt to market changes.

To address the risks, the following improvements can be made:

1. Add trend filter to avoid whipsaws in ranging markets.

2. Optimize exit conditions using trend indicators.

3. Add stop loss strategy to control single trade loss.  

4. Use adaptive moving averages so periods adjust dynamically.

## Improvement Directions

The strategy can be further optimized in the following aspects:

1. Add trend strength filter to avoid premature entry in weak trends. Indicators like MACD, KDJ can help.

2. Optimize moving average periods to find best combinations through backtesting.

3. Use adaptive moving averages so periods adapt based on market momentum. 

4. Add stop loss strategies like trailing stop loss, account balance stop loss to control risks.

5. Improve entry conditions using volume, Bollinger Bands etc to increase accuracy.

6. Improve exit conditions by judging trend reversal probability with indicators when lines cross.

## Conclusion

Williams' Alligator Strategy is a typical trend following strategy. It uses the alligator mouth formed by three moving averages to determine trend and trade accordingly. The advantages are its simple and clear logic. The disadvantages are weaker trend accuracy and risk control. Future improvements can be made by incorporating additional indicators, optimizing parameters, adding stop loss to make it more robust for complex market conditions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Lot|
|v_input_4|50|MA 1 Length|
|v_input_5|100|MA 2 Length|
|v_input_6|200|MA 3 Length|
|v_input_7_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_8|false|Show Background|
|v_input_9|1900|From Year|
|v_input_10|2100|To Year|
|v_input_11|true|From Month|
|v_input_12|12|To Month|
|v_input_13|true|From day|
|v_input_14|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-13 00:00:00
end: 2023-11-12 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2019

//@version=3
strategy(title = "Noro's Alligator Strategy by Bill Williams", shorttitle = "Alligator", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot")
len1 = input(50, defval = 50, minval = 1, title = "MA 1 Length")
len2 = input(100, defval = 100, minval = 1, title = "MA 2 Length")
len3 = input(200, defval = 200, minval = 1, title = "MA 3 Length")
src = input(close, title = "Source")
showbg = input(false, title = "Show Background")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//MAs
sma1 = sma(src, len1)
sma2 = sma(src, len2)
sma3 = sma(src, len3)
plot(sma1, color = lime, linewidth = 2)
plot(sma2, color = blue, linewidth = 2)
plot(sma3, color = red, linewidth = 2)

//Signals
up = sma1 > sma2 and sma2 > sma3
dn = sma1 < sma2 and sma2 < sma3

//Background
trend = 0
trend := up ? 1 : dn ? -1 : trend[1]
col = showbg == false ? na : trend == 1 ? lime : red
bgcolor(col)

//Trading
size = strategy.position_size
lot = 0.0
lot := size != size[1] ? strategy.equity / close * capital / 100 : lot[1]
if up
    strategy.entry("Long", strategy.long, needlong ? lot : 0, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
if dn
    strategy.entry("Short", strategy.short, needshort ? lot : 0, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/431911

> Last Modified

2023-11-13 10:58:22
