
> Name

Classic-Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b70c5ce3c6f1c36d83.png)
[trans]

## Overview
The double moving average crossover strategy is a very classic and commonly used technical analysis strategy. This strategy utilizes the crossover of the fast and slow moving averages as buy and sell signals. When the fast moving average breaks above the slow moving average, a buy signal is generated; when the fast moving average falls below the slow moving average, a sell signal is generated.
## Strategy Principle
The code of this strategy mainly includes the following parts:
1. Define the length and type of fast and slow moving averages: the length of the fast line is 5 periods, and the length of the slow line is 21 periods, both using simple moving averages.
2. Calculate fast and slow lines: Calculate the 5-period and 21-period simple moving averages through the sma function.
3. Drawing: Draw trend charts of fast and slow lines.
4. Define the buying and selling conditions: buy when the fast line crosses the slow line, sell when the fast line crosses below the slow line.
5. Execute transactions: Automatically execute buy and sell operations when conditions are met through the long and short functions of the strategy.
The key to this strategy is to use a combination of moving averages with periods of different lengths to form fast and slow moving averages, and use their crossover as a trading signal. The fast line can capture price changes faster, while the slow line can better reflect the long-term trend. When the fast line crosses the slow line, it means that the market reverses from bottom to top, which is a buy signal; when the fast line crosses below the slow line, it means that the market reverses from top to bottom, which is a sell signal. The principle of this strategy is simple, clear and easy to implement.
## Advantage Analysis
The double moving average crossover strategy has the following advantages:
1. The principle is simple, easy to master, and suitable for beginners.
2. Operate with the trend, follow the price trend, and have a small retracement.
3. The trading frequency is moderate and not too frequent.
4. Customizable parameters to flexibly respond to market changes.
5. It is easy to find the parameter combination that suits you through optimization.
6. Stop loss points can be set to control risks.
7. Can be used in a variety of markets and has strong applicability.
8. Can be used in combination with other indicators to improve the effect.
## Risk Analysis
The double moving average crossover strategy also has some risks:
1. When the market trend is strong, the moving average is delayed in following the trend, which may cause sluggishness and miss the best entry opportunity. The moving average period can be appropriately shortened and sensitivity improved.
2. In volatile market conditions, there may be many false signals. Filter conditions can be added appropriately to avoid erroneous transactions.
3. The number of transactions may be too high, affecting profits. The distance between moving averages can be appropriately widened to reduce crossovers.
4. It is impossible to judge the trend type and there is a risk of trading against the trend. It can assist in judging trend indicators.
5. Parameter optimization requires certain historical data support, and new varieties may be overfitted. Parameter robustness should be tested using various combinations.
6. A single indicator is easily affected by the external environment and its performance may be unstable. Can be combined with other indicators for verification.
## Optimization direction
The double moving average crossover strategy can also be optimized from the following aspects:
1. Test fast and slow moving averages of different lengths to find the best parameters suitable for specific trading varieties.
2. Add filtering conditions, such as transaction volume, ATR stop loss, etc., to reduce the chance of suboptimal results.
3. Use momentum indicators and other indicators to confirm buying and selling signals to avoid false breakthroughs.
4. Optimize the stop loss strategy to avoid premature or late exit of some stop losses.
5. Combine trend and wave indicators to achieve trend following and counter-trend trading.
6. Use adaptive moving averages to adjust moving average parameters according to the market instead of fixed periods.
7. Use multiple time periods in combination and use different parameter combinations according to market time characteristics.
8. Real-time optimization, using machine learning and other technologies to continuously optimize parameters.
## Summarize
The double moving average crossover strategy has become one of the most core and commonly used trading strategies in technical analysis due to its simple principle, easy to master and implement. This strategy follows the price trend, has controllable drawdowns, and acceptable risks. However, there is also a large space for optimization. Through parameter optimization, combined with other indicators and automated algorithms, the applicability and effect of this strategy can be further expanded. Generally speaking, the double moving average crossover strategy deserves investors' focused research and long-term application.
||

## Overview

The dual moving average crossover strategy is a very classic and commonly used technical analysis strategy. This strategy utilizes the crossover of a faster moving average and a slower moving average as the trading signals for buying and selling. When the faster moving average crosses above the slower moving average from below, a buy signal is generated. When the faster moving average crosses below the slower moving average from above, a sell signal is generated.

## Strategy Logic

The key parts of the strategy code include:

1. Define the length and type of fast and slow moving averages: the fast MA has a period of 5, the slow MA has a period of 21, both using simple moving average. 

2. Calculate the fast and slow MAs: using the sma function to compute the 5-period and 21-period simple moving averages.

3. Plot the chart: plot the trend lines of the fast and slow MAs.  

4. Define the entry and exit rules: buy when the fast MA crosses above the slow MA, sell when the fast MA crosses below the slow MA.

5. Execute trades: use the strategy's long and short functions to automatically execute trades when conditions are met.

The key of this strategy is using moving averages of different periods to form the fast and slow MAs, and using their crossovers as trading signals. The fast MA captures price changes faster while the slow MA reflects long term trend better. The crossover of the fast MA above the slow MA indicates an upside breakout, which is a buy signal. And the crossover below is a sell signal. The logic of this strategy is simple and easy to implement.

## Advantage Analysis 

The dual moving average crossover strategy has the following advantages:

1. Simple principle, easy to grasp, suitable for beginners.

2. Follow the price trend, small pullback. 

3. Moderate trading frequency, avoids over-trading.

4. Customizable parameters, flexible to adapt to market changes.

5. Easy to optimize and find suitable personal parameter sets.

6. Can set stop loss to control risk.

7. Can be used in various markets, high applicability. 

8. Can be combined with other indicators to improve performance.

## Risk Analysis

There are also some risks with this strategy:

1. Delayed reaction when the trend is strong, could miss best entry timing. Can shorten the MA periods to improve sensitivity.

2. More false signals during range-bound markets. Can add filters to avoid wrong trades.

3. Too many trades can impact profitability. Can widen the MA distance to reduce crossovers.

4. Hard to determine trend, risk of counter-trend trading. Can add trend indictors.

5. Parameter optimization requires sufficient historical data, risk of overfitting with new products. Need to test robustness of parameters.

6. Single indicator susceptible to external factors, performance could be unstable. Can combine with other indicators for verification.

## Optimization Directions

There are some ways to optimize the dual MA strategy further:

1. Test different fast and slow MA lengths to find the optimal parameters for specific trading products.

2. Add filters like trading volumes, ATR stop loss to reduce inferior opportunities.

3. Combine momentum indicators to confirm trading signals and avoid false breakouts.

4. Optimize stop loss strategies to avoid premature or late exits.

5. Incorporate trend and wave indicators to enable trend following and counter-trend trading. 

6. Use adaptive MAs to adjust parameters based on market conditions rather than fixed periods.

7. Utilize combinations of parameters for different market sessions and characteristics.

8. Perform real-time optimization via machine learning algorithms to continuously improve parameters.

## Summary

With its simple logic and ease of implementation, the dual moving average crossover strategy has become one of the most essential and widely used technical analysis strategies. It follows the price trend with controlled pullback and acceptable risk. But there is also huge potential for optimization, by parameter tuning, incorporating other indicators and automated algorithms, its applicability and performance can be further enhanced. Overall, the dual MA crossover strategy deserves great attention and long-term application by investors.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2011|Start Year|
|v_input_2|true|Start Month|
|v_input_3|true|Start Day|
|v_input_4|2050|Finish Year|
|v_input_5|12|Finish Month|
|v_input_6|31|Finish Day|
|v_input_7|21|length1|
|v_input_8|3|smoothK1|
|v_input_9|3|smoothD1|
|v_input_10|14|Bottom Line|
|v_input_11|86|Upper Line|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-26 00:00:00
end: 2023-10-26 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
// strategy("Stochastic Strategy of BiznesFilosof", shorttitle="SS of BiznesFilosof", overlay=false, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=20, commission_type=strategy.commission.percent, commission_value=0.15, pyramiding=0)

//Period
startY = input(title="Start Year", defval = 2011)
startM = input(title="Start Month", defval = 1, minval = 1, maxval = 12)
startD = input(title="Start Day", defval = 1, minval = 1, maxval = 31)
finishY = input(title="Finish Year", defval = 2050)
finishM = input(title="Finish Month", defval = 12, minval = 1, maxval = 12)
finishD = input(title="Finish Day", defval = 31, minval = 1, maxval = 31)
//finish = input(2019, 02, 28, 00, 00)
timestart = timestamp(startY, startM, startD, 00, 00)
timefinish = timestamp(finishY, finishM, finishD, 23, 59)
window = true // Lenghth strategy

length1 = input(21, minval=1), smoothK1 = input(3, minval=1), smoothD1 = input(3, minval=1)
//length2 = input(5, minval=1), smoothK2 = input(1, minval=1), smoothD2 = input(1, minval=1)
inh0 = input(title="Bottom Line", defval = 14, minval=0), inh1 = input(title="Upper Line", defval = 86, minval=0)

k1 = sma(stoch(close, high, low, length1), smoothK1)
d1 = sma(k1, smoothD1)
plot(k1, color=blue)
plot(d1, color=red)
//k2 = sma(stoch(close, high, low, length2), smoothK2)
//d2 = sma(k2, smoothD2)
//plot(k2, color=orange)

h1 = hline(inh1)
h0 = hline(inh0)
fill(h0, h1, color = aqua, transp=90)

//open
strategy.entry("LongEntryID", strategy.long, comment="LONG", when = crossover(k1, d1) and crossover(k1, inh0) and window)
strategy.entry("ShortEntryID", strategy.short, comment="SHORT", when = crossunder(k1, d1) and crossunder(k1, inh1) and window)

if crossunder(k1, d1) and crossunder(k1, inh1) and strategy.position_size > 0
    strategy.close_all()
if crossover(k1, d1) and crossover(k1, inh0) and strategy.position_size < 0
    strategy.close_all()
  
    

```

> Detail

https://www.fmz.com/strategy/430380

> Last Modified

2023-10-27 16:47:30
