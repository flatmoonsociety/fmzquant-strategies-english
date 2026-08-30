
> Name

Average-Highest-High-and-Lowest-Low-Swinger-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10d948d2cf189afcf51.png)
[trans]

## Overview
This strategy is a complete price action strategy specifically designed for markets with trending characteristics such as cryptocurrencies and stocks. It is formulated purely based on the calculation of the highest and lowest prices for two periods of different lengths. Multiple averages of these highest and lowest prices are calculated as entry and exit signals.
## Strategy Principle
This strategy uses the lowest and highest prices of two periods of different lengths and their average to determine entries and exits. Specifically, it calculates the lowest price average, the highest price average, and the average of these two averages for 9 and 26 periods respectively. Go long when the closing price is higher than the average price of two different periods at the same time, and go short when the closing price is lower than the average price of two different periods at the same time.
The specific logic of going long is: the closing price is higher than the 9-period average of the highest and lowest prices, higher than the 26-period average of the highest and lowest prices, and higher than the average of the two averages. Go long when these three conditions are met.
The specific logic of short selling is: the closing price is lower than the 9-period average of the highest and lowest prices, lower than the 26-period average of the highest and lowest prices, and lower than the average of the two averages. When these three conditions are met, go short.
Regardless of whether you are long or short, when a reverse signal appears, choose to stop loss and exit.
## Advantage Analysis
This strategy has several major advantages:
1. Using dual time frame analysis, you can judge trends more clearly and increase accuracy.
2. Calculation based on the highest price and lowest price can effectively seize breakthroughs.
3. Use multiple average filtering to increase the reliability of the signal and avoid being interfered by noise.
4. Pure price market strategy, suitable for most markets with trend characteristics.
5. Completely automated transactions without manual intervention, reducing the probability of human error.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. There is no integrated stop loss module, and there is a risk of loss expansion. Trailing stop loss or percentage stop loss can be added to control single losses.
2. Wrong signals and over-trading are prone to occur in volatile markets. You can adjust cycle parameters appropriately or add filter conditions.
3. Without taking into account the impact of the relationship between individual stocks and the market, systemic risks still exist. Multi-factor models can be considered to control this type of risk.
4. Insufficient backtest data may lead to overfitting. Robustness tests should be conducted over longer time scales and in more markets.
## Optimization direction
There is still some room for optimization in this strategy:
1. Periodic parameters can continue to be tested and optimized to find the best parameter combination.
2. You can consider adding trailing stop loss and trailing stop loss to control single losses.
3. You can test different markets and even different varieties to explore applicability.
4. Certain algorithmic trading modules, such as machine learning, can be added to assist decision-making.
5. Multi-factor models can be considered, adding more variable judgments to improve robustness.
## Summarize
In general, this dual time frame highest and lowest price average strategy has strong trend following capabilities and is suitable for highly volatile markets such as cryptocurrency. It effectively uses breakouts to determine entry timing, while using multiple layers of filtering to improve signal quality. This strategy can be further enhanced through parameter optimization, stop loss module addition, auxiliary algorithm and other means, making it an efficient and stable strategy worthy of long-term holding.
||


## Overview

This is a full price action strategy designed for trending markets such as crypto and stocks. It is purely made on calculations for the highest high and lowest low using 2 different length, a faster and a slower one.

## Strategy Logic  

This strategy uses two different cycle lengths of lowest low and highest high prices and their averages to determine entry and exit. Specifically, it calculates the average lowest price, the average highest price and the average of these two averages of the 9-cycle and 26-cycle respectively. It goes long when the closing price is higher than the two averages of different cycles at the same time, and goes short when the closing price is lower than the two averages of different cycles at the same time.  

The specific logic for long is: the closing price is higher than the average of the highest and lowest prices of the 9-cycle, higher than that of the 26-cycle, and higher than the average of the two averages, when all three conditions are met, it goes long.

The specific logic for short is: the closing price is lower than the average of the highest and lowest prices of the 9-cycle, lower than that of the 26-cycle, and lower than the average of the two averages, when all three conditions are met, it goes short.

Whether long or short, choose to cut losses when there is a reverse signal.

## Advantage Analysis

This strategy has the following main advantages:

1. Using dual time frame analysis can better judge the trend and increase accuracy. 

2. Building on the highest and lowest prices can effectively capture breakouts.

3. Using multiple moving averages to filter increases signal reliability and avoids noise interference.

4. A pure price action strategy that applies to most markets with trending characteristics.

5. Fully automated trading eliminates human error probabilities.

## Risk Analysis

The strategy also has some risks to note:

1. There is no integrated stop loss module, risk of expanding losses. Moving stop loss or percentage stop loss can be added to control single loss.

2. It is easy to generate wrong signals and overtrade in range-bound markets. Period parameters can be adjusted or filters can be added.

3. The impact of the relationship between individual stocks and the market is not considered, systemic risks still exist. Multi-factor models can be considered to control such risks.

4. Insufficient backtest data may lead to overfitting. Robustness testing should be carried out over longer time frames and more markets.

## Optimization Directions

There is still some room for optimization in this strategy:

1. Period parameters can continue to be test optimized to find the best combination.

2. Consider adding moving stop loss, trailing stop loss to control single loss.

3. Can test different markets or even different varieties to explore applicability. 

4. Certain algorithmic trading modules can be added, such as machine learning, to assist in decision making.

5. Multi-factor models can be considered to introduce more variables for judgment and improve robustness.

## Conclusion

In summary, this dual time frame highest high and lowest low average strategy has strong trend tracking capabilities and is suitable for high volatility markets like cryptocurrencies. It effectively uses breakout judgments for entry timing, while using multiple layers of filtering to improve signal quality. Parameters optimization, addition of stop loss module, auxiliary algorithms and other means can be used to further enhance the strategy, making it an efficient and stable strategy worth holding for the long term.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Fast Line|
|v_input_2|26|Slow  Line|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-27 00:00:00
end: 2023-12-04 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=4
strategy(title = "Avg HH/LL Crypto Swinger", overlay = true )

varLo = input(title="Fast Line", type=input.integer, defval=9, minval=1)
varHi = input(title="Slow  Line", type=input.integer, defval=26, minval=1)

a = lowest(varLo)
b = highest(varLo)
c = (a + b ) / 2

d = lowest(varHi)
e = highest(varHi)
f = (d + e) / 2

g = ((c + f) / 2)[varHi]
h = ((highest(varHi * 2) + lowest(varHi * 2)) / 2)[varHi]



long=close > c and close > f and close >g and close > h
short=close < c and close < f and close<g and close < h

strategy.entry("long",1,when=long)
strategy.entry('short',0,when=short)
```

> Detail

https://www.fmz.com/strategy/434336

> Last Modified

2023-12-05 16:34:01
