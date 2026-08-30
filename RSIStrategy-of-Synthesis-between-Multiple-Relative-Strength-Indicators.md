
> Name

Strategy-of-Synthesis-between-Multiple-Relative-Strength-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1f706e0a3d0ff14f1b06cf2c9ca6507fe18255ffcd6b43304bf4c416198649d3.png)

[trans]

## Overview
The multiple RSI indicator aggregation strategy is a strategy that uses multiple relative strength index (RSI) indicators for stock timing trading. This strategy uses RSI indicators of 1, 2, 3, 4, and 5 different periods at the same time. When any RSI indicator is lower than the set limit value, a buy signal is generated. When all RSI indicators are higher than their respective limit values, a sell signal is generated to realize the timing entries and exits of the stock.
## Strategy Principle
The core logic of this strategy is to simultaneously track the RSI indicators of 1, 2, 3, 4, and 5 different periods, including 4-period, 7-period, 14-period, 21-period, and 28-period RSI. These five RSI indicators have different limit values ​​set respectively. As long as any RSI indicator is lower than the corresponding limit value, a buy signal will be generated.
For example, the limit value of the 4-period RSI indicator is set to 15. When the 4-period RSI is lower than 15, a buy signal will be generated. The strategy will also detect whether the RSI indicators of other periods are also lower than the corresponding limit value. If so, a buy signal will also be generated.
When all five RSI indicators are higher than their respective limit values, a sell signal will be generated to achieve profit taking. In this way, the accuracy of Entries can be improved by aggregating the signals of multiple period indicators.
## Strategic Advantages
1. Use multiple RSI indicators to improve Entries accuracy   
This strategy uses 5 RSI indicators with different periods at the same time, and generates a buy signal when any RSI is below the extreme value. This can improve the reliability of the signal and avoid false signals caused by a single indicator. The aggregation of multiple indicators can improve the accuracy of Entries.
2. Different cycle indicators adapt to various market conditions
Using the 1, 2, 3, 4, and 5 period RSI indicators can adapt to stock fluctuations in different periods. For example, a 28-period RSI is suitable for long-term trading, and a 4-period RSI is suitable for short-term trading. This guarantees that the strategy will work properly in a variety of market conditions.
3. The code structure is clear and easy to understand.
The variable naming and code structure of the strategy are very clear, and the calculation process of different indicators and signals is clear at a glance. This makes the strategy easy to understand, modify, and optimize. This is a very important advantage of quantitative strategies.
## Strategy Risk
1. Unilateral market is invalid
This strategy mainly relies on the generation of overbought and oversold signals. In a unilateral upward or downward trend market, its effect will be compromised. This is a common problem with strategies using reversal indicators.
2. Parameter optimization is difficult
The strategy contains multiple indicators and parameters, which makes parameter optimization very difficult. Unreasonable parameter combinations may significantly reduce the strategy effect. This requires using optimization tools to find the best parameters.
3. Frequent switching between long and short positions
Due to the use of multiple period indicators, the long-short switching of the strategy may be more frequent, which will bring higher transaction costs and slippage risks.
## Strategy optimization direction
1. Combined with trend indicators
Trend indicators such as MA or BOLL can be added to avoid discounting under unilateral market conditions. For example, only enter when the trend indicator also agrees with the reversal.
2. Reduce the number of indicators
Try to reduce the number of RSI indicators used and reduce the difficulty of parameter optimization. Experiments show that a combination of 2-3 indicators can achieve good results.
3. Optimize parameter range
Use methods such as step optimization and stochastic optimization to find the best range and combination of each RSI parameter to maximize the strategy performance.  

## Summarize
The multiple RSI indicator aggregation strategy improves the accuracy of entries and enables timing trading of stocks by congregating RSI signals of multiple periods. It has the advantage of using a variety of indicators, but it also has problems such as unilateral market failure and difficulty in optimization. The robustness of the strategy can be further improved by adding trend indicators, reducing the number of indicators, optimizing parameters, etc.
||


## Overview

The strategy of synthesis between multiple relative strength indicators (RSI) is a timing trading strategy that utilizes multiple RSIs with different periods to trade stocks. It tracks 1-, 2-, 3-, 4-, and 5-period RSI indicators simultaneously. Buying signals are generated when any of the RSI goes below a threshold. Selling signals are generated when all RSIs exceed their own thresholds, in order to earn profits. Thus, timing entries and exits can be achieved in stocks.

## Strategy Logic  

The key rationale behind this strategy is to track 1-, 2-, 3-, 4-, and 5-period RSI indicators simultaneously, including 4-, 7-, 14-, 21-, and 28-period RSIs. Separate threshold values are set for each of the 5 RSI indicators. A buying signal is triggered when any of the RSI drops below its own threshold.  

For example, the threshold of the 4-period RSI is set as 15.  A buying signal is generated when the 4-period RSI falls below 15. The strategy checks other RSIs to see whether they also drop below their own thresholds. If yes, more buying signals will be produced.

When all the 5 RSI indicators rally and exceed their own thresholds, a selling signal is generated in order to gain profits. By congregation signals of the multiple-period indicators, accuracy of entries can be improved.

## Strategy Strengths 

1. Improve accuracy of entries with multiple RSIs  
   
The strategy utilizes 5 RSIs of different periods to generate buy and sell signals. One single indicator may generate false signal at times. However, with the congregation of multiple ones, accuracy of signal can be improved, hence enhancing accuracy of entries.  

2. RSIs of different periods suitable for various market conditions

   The 1-, 2-, 3-, 4-, 5-period RSIs used in this strategy can adapt to stock fluctuations of different frequencies. For instance, 28-period RSI suits long-term trading while 4-period RSI suits short-term trading. This guarantees the strategy works under different market situations.  

3. Clean and clear code structure  

   The variable naming and overall structure of the strategy code is neat and self-evident. The logic flow for different indicators and signals is clear. This makes the strategy easy to understand, modify and optimize, which is of great essence for quantitative strategies.  

## Risks of The Strategy

1. Invalid in trending market

   The strategy relies heavily on overbought and oversold signals. Its effectiveness would be compromised in persistent up- or downtrend market. This is a ubiquitous flaw of mean-reversion strategies using reverse indicators.   

2. Difficulty in parameter optimization

   A variety of indicators and input parameters exist in this strategy. This poses immense challenges for parameter optimization. Improper parameter combination may diminish the strategy efficacy drastically. Optimizing tools should be utilized to seek for the parameter set that maximizes strategy performance.   

3. Frequent reversals between long and short

   Due to the usage of multiple-period indicators, long and short position changes in the strategy could be rather frequent. This may lead to higher costs associated with trading and risks related to price slippage.  

## Directions for Optimization

1. Incorporate trend-following indicators 

   Trend tools such as MA and BOLL can be added. Signals are only taken when trend tools concur to the signals generated by reverse indicators. This helps avoid losses in persistent trend situations.  

2. Reduce the number of RSI indicators

   Try decreasing the number of RSI tools used. This mitigates the difficulty in parameter optimization. Experiments manifest 2 to 3 indicators can already create satisfying efficacy.  

3. Optimize parameter ranges

   Seek optimal ranges and combinations of RSI parameters and thresholds using optimization methods like gradient descent and random search. This maximizes strategy performance.  

## Conclusion  

The strategy of RSI synthesis generates trading signals by congregation signals from multiple RSIs with different periods. This improves accuracy of entries to realize timing trading in stocks. Despite advantages inherited from the usage of multiple indicators, flaws including ineffectiveness in trending markets and difficulty in optimization remain. Methods like adding trend tools, reducing indicator numbers, and parameter optimization can help further boost the strategy's robustness.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Lot, %|
|v_input_4|true|Use RSI 1|
|v_input_5|4|RSI 1 Period|
|v_input_6|15|RSI 1 Limit|
|v_input_7|true|Use RSI 2|
|v_input_8|7|RSI 2 Period|
|v_input_9|20|RSI 2 Limit|
|v_input_10|true|Use RSI 3|
|v_input_11|14|RSI 3 Period|
|v_input_12|25|RSI 3 Limit|
|v_input_13|true|Use RSI 4|
|v_input_14|21|RSI 4 Period|
|v_input_15|30|RSI 4 Limit|
|v_input_16|true|Use RSI 5|
|v_input_17|28|RSI 5 Period|
|v_input_18|35|RSI 5 Limit|
|v_input_19|false|Use color filter|
|v_input_20|1900|From Year|
|v_input_21|2100|To Year|
|v_input_22|true|From Month|
|v_input_23|12|To Month|
|v_input_24|true|From Day|
|v_input_25|31|To Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-26 00:00:00
end: 2024-01-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's Symphony v1.0", shorttitle = "Symphony 1.0", overlay = false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 20)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot, %")
usersi1 = input(true, defval = true, title = "Use RSI 1")
rsiperiod1 = input(4, defval = 4, minval = 2, maxval = 100, title = "RSI 1 Period")
rsilimit1 = input(15, defval = 15, minval = 2, maxval = 50, title = "RSI 1 Limit")
usersi2 = input(true, defval = true, title = "Use RSI 2")
rsiperiod2 = input(7, defval = 7, minval = 2, maxval = 100, title = "RSI 2 Period")
rsilimit2 = input(20, defval = 20, minval = 2, maxval = 50, title = "RSI 2 Limit")
usersi3 = input(true, defval = true, title = "Use RSI 3")
rsiperiod3 = input(14, defval = 14, minval = 2, maxval = 100, title = "RSI 3 Period")
rsilimit3 = input(25, defval = 25, minval = 2, maxval = 50, title = "RSI 3 Limit")
usersi4 = input(true, defval = true, title = "Use RSI 4")
rsiperiod4 = input(21, defval = 21, minval = 2, maxval = 100, title = "RSI 4 Period")
rsilimit4 = input(30, defval = 30, minval = 2, maxval = 50, title = "RSI 4 Limit")
usersi5 = input(true, defval = true, title = "Use RSI 5")
rsiperiod5 = input(28, defval = 28, minval = 2, maxval = 100, title = "RSI 5 Period")
rsilimit5 = input(35, defval = 35, minval = 2, maxval = 50, title = "RSI 5 Limit")
cf = input(false, defval = false, title = "Use color filter")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From Day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To Day")

//RSI
rsi1 = rsi(close, rsiperiod1)
rsi2 = rsi(close, rsiperiod2)
rsi3 = rsi(close, rsiperiod3)
rsi4 = rsi(close, rsiperiod4)
rsi5 = rsi(close, rsiperiod5)

//Signals
up1 = rsi1 < rsilimit1 and usersi1  
up2 = rsi2 < rsilimit2 and usersi2
up3 = rsi3 < rsilimit3 and usersi3
up4 = rsi4 < rsilimit4 and usersi4
up5 = rsi5 < rsilimit5 and usersi5

up = up1 or up2 or up3 or up4 or up5
exit = rsi1 > rsilimit1 and rsi2 > rsilimit2 and rsi3 > rsilimit3 and rsi4 > rsilimit4 and rsi5 > rsilimit5
lot = strategy.position_size == 0 ? strategy.equity / close * capital / 100 : lot[1]

//Background
col = up ? lime : na
bgcolor(col, transp = 0)

//Trading
if up and (close < open or cf == false)
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot)
 
if  exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/437399

> Last Modified

2024-01-02 12:06:14
