
> Name

Closing Yang line strategy Harami-Closing-Price-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/8e2c835256eefbf33a.png)
[trans]

### Overview
The closed positive line strategy is a quantitative trading strategy based on the K-line pattern. This strategy looks for buy and sell signals by identifying "closed positive" patterns.
### Strategy Principles
The core principle of this strategy is: the current K line is a negative line, the previous K line is a positive line, and the lowest price of the current K line is higher than the lowest price of the previous K line, and when the highest price of the current K line is lower than the highest price of the previous K line, a "closed positive line" form is generated. This means that the price has formed a closed upward space, showing that the bulls are about to run out of power, which is a sell signal. On the contrary, when a "closed negative line" is formed, a buy signal is generated.
Here the average value of the K-line entity is used as the stop loss line. Stop loss when the real body is greater than half of the stop loss line.
### Advantage Analysis
The main advantages of the closed Yang line strategy are:
1. Based on simple and reasonable K-line shape judgment, easy to understand and implement.
2. Can identify range breakouts with less changing hands. When the increase narrows and a "closed positive line" appears, the bulls are about to run out of power, which is a suitable selling point.
3. Have a clear stop-loss mechanism to control risks.
### Risk Analysis
There are also some risks in the closed Yang line strategy:
1. The monitoring frequency is low and the best buying and selling points may be missed. The effect is not good for K-lines with shorter periods.
2. False positive lines and false negative lines may cause false signals. It is necessary to filter based on indicators such as trading volume.  
3. There is a certain degree of blindness in the comprehensive judgment based only on the K-line shape without considering other technical indicators and fundamental factors.
In order to reduce these risks, you can consider adding conditional judgments on trading volume, or use them in conjunction with other indicators such as moving averages to comprehensively judge market trends. The stop loss line can also be dynamically adjusted according to the degree of market volatility.
### Optimization direction
The closed Yang line strategy can also be optimized from the following aspects:
1. Add conditional judgment of trading volume. A sharp increase in trading volume often indicates a trend reversal.
2. Adjust stop loss conditions. Stop loss lines can be dynamically adjusted based on market volatility and risk appetite.
3. Multi-cycle combination. Identify the closing selling point of the bullish line near key support levels on multiple cycles.
4. Combined with other technical indicators. For example, adding a moving average system to determine the overall trend, or introducing some predictive indicators to determine buying and selling points in advance.
### Summarize
As a quantitative strategy based on the K-line pattern, the closed Yang line strategy has the advantage of being simple to understand and easy to implement, and it can effectively identify certain buying and selling signals. However, there are also some limitations, such as easy generation of false signals and strong blindness. These questions also provide optimization directions for the strategy. By using information such as trading volume, multi-period analysis, and other technical indicators for comprehensive judgment, the effect of this strategy can be further enhanced.
||
### Overview

The Harami Closing Price strategy is a quantitative trading strategy based on candlestick patterns. This strategy identifies "Harami" patterns to generate buy and sell signals.  

### Strategy Logic

The core logic is: When the current candlestick is a red candle and the previous one is a green candle, and the current candle's lowest price is higher than the previous candle's lowest price, the current candle's highest price is lower than the previous candle's highest price, the "Harami" pattern is formed. This means the uptrend momentum is losing strength and it is a signal for selling. On the contrary, a "Harami" pattern with two candles inverted constitutes a buy signal.

The average of the candle body is used as a stop loss line. When the body is larger than half the stop loss line, stop loss triggers.

### Advantage Analysis  

The main advantages of the Harami Closing Price strategy are:

1. Simple and reasonable judgment based on candlestick patterns, easy to understand and implement.  
2. Can identify breakouts with relatively small trading volumes. When the rising range narrows down to form a "Harami" pattern, the bullish momentum is losing strength and it's a good selling point.
3. There is a clear stop loss mechanism to control risks.

### Risk Analysis   

There are also some risks for this strategy:

1. Low monitoring frequency, may miss the best entry and exit points. Not effective for shorter cycle candlesticks.  
2. False bullish/bearish candles may generate wrong signals. Needs to be used with trading volume and other filters.
3. Judgments are solely based on candlestick patterns without considering other technical indicators and fundamentals, which leads to some blindness.  

To mitigate these risks, combining with trading volume, moving averages and other technical indicators is recommended, to make more comprehensive judgments on market trends. The stop loss line can also be dynamically adjusted based on market volatility.

### Optimization Directions  

The Harami Closing Price strategy can also be improved from the following aspects:  

1. Adding trading volume condition checks. Surges in trading volumes often imply trend reversals.  
2. Adjusting stop loss criteria dynamically based on market volatility and risk preference.
3. Multi-timeframe analysis. Identifying selling points near key support levels on higher timeframes when Harami patterns form.  
4. Combining other technical indicators like moving averages to determine overall market trends, or leading indicators to forecast entry and exit points.

### Summary   

The Harami Closing Price strategy is easy to understand and implement for generating certain buy and sell signals based on candlestick patterns. But it also has some limitations like generating false signals and blindness. These problems also point to directions for further optimizations, by applying more comprehensive judgments with trading volumes, multiple timeframes, and other technical indicators. This can greatly enhance the strategy's efficacy.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|false|Short|
|v_input_3|1900|From Year|
|v_input_4|2100|To Year|
|v_input_5|true|From Month|
|v_input_6|12|To Month|
|v_input_7|true|From day|
|v_input_8|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-20 00:00:00
end: 2023-11-27 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=3
strategy(title = "Noro's Harami Strategy v1.0", shorttitle = "Harami str 1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(false, defval = false, title = "Short")

fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Body
body = abs(close - open)
abody = sma(body, 10)

//MinMax Bars
min = min(close, open)
max = max(close, open)
bar = close > open ? 1 : close < open ? -1 : 0

//Signals
up = bar == 1 and bar[1] == -1 and min > min[1] and max < max[1]
dn = bar == -1 and bar[1] == 1 and min > min[1] and max < max[1]
exit = ((strategy.position_size > 0 and bar == 1) or (strategy.position_size < 0 and bar == -1)) and body > abody / 2

//Trading
if up
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if dn
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if time > timestamp(toyear, tomonth, today, 23, 59) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/433585

> Last Modified

2023-11-28 16:50:34
