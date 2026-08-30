
> Name

Price-Volatility-Mean-Reversion-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy determines whether there are abnormally large price fluctuations by calculating the standard deviation of the price. When the price fluctuates abnormally and significantly, it is judged as an opportunity for price reversal and reverse operations are taken.
## Principle
This strategy mainly uses two indicators:
1. VixFix indicator: Calculate the standard deviation of prices within a certain period to determine whether there are abnormal price fluctuations. The specific calculation method is:
```pine
wvf = ((highest(close, pd)-low)/(highest(close, pd)))*100 
sDev = mult * stdev(wvf, bbl)
midLine = sma(wvf, bbl)  
lowerBand = midLine - sDev
upperBand = midLine + sDev
```

Among them, wvf is the price volatility, sDev is the standard deviation, midLine is the average line, lowerBand and upperBand are the lower limit line and upper limit line respectively. When the price exceeds the upper limit line, it is considered that there is abnormal fluctuation.
2. RSI indicator: Calculate the relative strength index of prices and determine the timing of price reversal. The specific calculation method is:
```pine
fastup = rma(max(change(close), 0), 7)  
fastdown = rma(-min(change(close), 0), 7)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown)) 
```

When RSI is lower than a certain value, it means that the price is oversold and a rebound may occur. When RSI exceeds a certain value, it means that the price is overbought and may fall back.
## Entry and Exit
The entry and exit logic of this strategy is as follows:
Long position entry: When the price exceeds the upper limit line or the volatility exceeds the threshold, and the RSI is lower than a certain value, go long.
Short position entry: When the price exceeds the upper limit line or the volatility exceeds the threshold, and the RSI exceeds a certain value, go short.
Exit conditions: Close the position when the opening direction is opposite to the direction of the K-line entity.
## Advantages
- Utilize the statistical characteristics of abnormal price fluctuations to determine the timing of price reversal, with wide coverage.
- Combined with the RSI indicator to determine the overbought and oversold status, the accuracy of entry can be improved.
- Using the breakthrough of the lower limit of the standard deviation as an entry signal can reduce missed opportunities.
- Using physical reversal as a stop loss method can quickly stop losses and reduce losses.
## Risk
- The lower limit of the standard deviation may be adjusted and parameters need to be optimized.
- Breaking through the lower limit of the standard deviation may not necessarily result in a reversal, and there is a risk of being trapped.
- RSI parameters need to be optimized, if inappropriate it may lead to signal inaccuracy. 
- The stop loss determined by the entity direction may be too aggressive and the parameters need to be adjusted.
## Optimization ideas
- Optimize the period parameter for calculating standard deviation so that it can better capture abnormal price fluctuations.
- Optimize the parameters of RSI and find better overbought and oversold criteria.
- Try to combine with other indicators, such as KDJ, MACD, etc. to determine the timing of reversal.
- Optimize the stop loss method and set the price retracement range as the stop loss standard.
## Summarize
This strategy calculates the standard deviation of price volatility to determine whether there are abnormal price fluctuations, thereby capturing reversal opportunities. When choosing the timing of entry, the RSI indicator is used to determine the overbought and oversold status of the price to improve accuracy. Use a simple stop loss in the physical direction as the stop loss method. Overall, this strategy uses statistical data to determine abnormal fluctuations and has good results, but it needs to further optimize parameters and improve stability. If the stop loss mechanism can be reasonably optimized and losses reduced, the effect of this strategy will be better.
||


## Overview

This strategy detects price reversal opportunities by calculating the standard deviation of price volatility. When there is an anomalously large price fluctuation, it is considered as an opportunity for price reversal, and reverse trading positions are taken.

## Principle 

The strategy uses two main indicators:

1. VixFix indicator: Calculates the standard deviation of price over a certain period to determine if there is anomalous price volatility. The specific calculation is:

```pine
wvf = ((highest(close, pd)-low)/(highest(close, pd)))*100
sDev = mult * stdev(wvf, bbl) 
midLine = sma(wvf, bbl)
lowerBand = midLine - sDev 
upperBand = midLine + sDev
```

Where wvf is price volatility, sDev is standard deviation, midLine is the average line, lowerBand and upperBand are the lower and upper limit lines. When price exceeds the upper limit line, it is considered anomalous volatility.

2. RSI indicator: Calculates the Relative Strength Index of price to determine timing of price reversal. The calculation is:

``` pine
fastup = rma(max(change(close), 0), 7)
fastdown = rma(-min(change(close), 0), 7) 
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))
```

When RSI is below a threshold, it indicates oversold status and potential bounce back. When RSI exceeds a threshold, it indicates overbought status and potential pullback.

## Entry and Exit

The entry and exit logic is:

Long entry: When price exceeds upper limit or volatility exceeds threshold, and RSI is below a value, go long.

Short entry: When price exceeds upper limit or volatility exceeds threshold, and RSI exceeds a value, go short.

Exit: When candlestick body direction is opposite of position direction, close position.

## Advantages

- Uses statistical properties of anomalous price volatility to determine price reversal with wide coverage.
- Combining with RSI to judge overbought/oversold improves entry precision.  
- Breaking lower deviation band as entry signal reduces missing opportunities.
- Candlestick body reversal as stop loss realizes quick stop loss and reduces losses.

## Risks

- Lower deviation band may need adjustment for parameter optimization.
- Breaking lower band does not guarantee reversal, risks being trapped.
- RSI parameters need optimization, improper values lead to inaccurate signals.
- Candlestick body stop loss may be too aggressive, needs adjustment.

## Optimization Directions 

- Optimize calculation period of standard deviation to better capture anomalous volatility.
- Optimize RSI parameters to find better overbought/oversold criteria. 
- Try combining other indicators like KDJ, MACD to determine reversal timing.
- Optimize stop loss mechanism, set price retracement as stop loss benchmark.

## Conclusion

The strategy detects anomalous price volatility through calculating standard deviation of price volatility, to capture reversal opportunities. RSI is combined to judge overbought/oversold status for improving entry precision. Simple candlestick body direction stop loss is used. Overall, the strategy is effective in using statistical data to detect anomalous volatility, but needs further parameter optimization to improve stability. If the stop loss mechanism can be reasonably optimized to reduce losses, the strategy would perform even better.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|true|leverage|
|v_input_4|40|RSI Limit|
|v_input_5|22|LookBack Period Standard Deviation High|
|v_input_6|20|Bolinger Band Length|
|v_input_7|2|Bollinger Band Standard Devaition Up|
|v_input_8|50|Look Back Period Percentile High|
|v_input_9|0.85|Highest Percentile - 0.90=90%, 0.95=95%, 0.99=99%|
|v_input_10|1.01|Lowest Percentile - 1.10=90%, 1.05=95%, 1.01=99%|
|v_input_11|false|Show High Range - Based on Percentile and LookBack Period?|
|v_input_12|false|Show Standard Deviation Line?|
|v_input_13|1900|From Year|
|v_input_14|2100|To Year|
|v_input_15|true|From Month|
|v_input_16|12|To Month|
|v_input_17|true|From day|
|v_input_18|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-04 00:00:00
end: 2023-10-10 00:00:00
period: 2d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's VixFix + RSI Strategy v1.0", shorttitle = "VixFix + RSI str 1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 5)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
leverage = input(1, defval = 1, minval = 1, maxval = 100, title = "leverage")
limit = input(40, defval = 40, minval = 2, maxval = 50, title = "RSI Limit")

pd = input(22, title="LookBack Period Standard Deviation High")
bbl = input(20, title="Bolinger Band Length")
mult = input(2.0, minval = 1, maxval = 5, title = "Bollinger Band Standard Devaition Up")
lb = input(50, title="Look Back Period Percentile High")
ph = input(.85, title="Highest Percentile - 0.90=90%, 0.95=95%, 0.99=99%")
pl = input(1.01, title="Lowest Percentile - 1.10=90%, 1.05=95%, 1.01=99%")
hp = input(false, title="Show High Range - Based on Percentile and LookBack Period?")
sd = input(false, title="Show Standard Deviation Line?")

fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Vix Fix
wvf = ((highest(close, pd)-low)/(highest(close, pd)))*100
sDev = mult * stdev(wvf, bbl)
midLine = sma(wvf, bbl)
lowerBand = midLine - sDev
upperBand = midLine + sDev
rangeHigh = (highest(wvf, lb)) * ph
rangeLow = (lowest(wvf, lb)) * pl

col = wvf >= upperBand or wvf >= rangeHigh ? lime : gray

//RSI
fastup = rma(max(change(close), 0), 7)
fastdown = rma(-min(change(close), 0), 7)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//Body
body = abs(close - open)
abody = sma(body, 10)

//Signals
up = (wvf >= upperBand or wvf >= rangeHigh) and fastrsi < limit and close < open
dn = (wvf >= upperBand or wvf >= rangeHigh) and fastrsi > (100 - limit) and close > open
exit = ((strategy.position_size > 0 and close > open) or (strategy.position_size < 0 and close < open)) and body > abody / 3

//Trading
lot = strategy.position_size == 0 ? strategy.equity / close * leverage : lot[1]

if up
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Bottom", strategy.long, needlong == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if dn
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Top", strategy.short, needshort == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if time > timestamp(toyear, tomonth, today, 23, 59) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/428982

> Last Modified

2023-10-11 16:03:36
