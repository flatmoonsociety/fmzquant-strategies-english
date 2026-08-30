
> Name

Highest-Lowest-Center-Lookback-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1a8831f1c93d21e8dfd.png)
[trans]

## Overview
The Maximum Minimum Center Lookback Strategy is a trend following strategy. Its main idea is to calculate the middle price between the highest price and the lowest price in a certain period in the past as the base price, and then calculate the opening and closing areas based on this base price combined with the volatility. When the price enters the opening zone, go long; when the price enters the closing zone, close the position.
## Strategy Principle
This strategy is mainly implemented through the following steps:
1. Calculate the highest price h and lowest price l in the past lookback_length period, and use EMA smoothing
2. Calculate the center price between the highest price and the lowest price as the base price
3. Calculate volatility vola based on ATR and ATR multiplier
4. Calculate the opening area upper and the closing area lower based on center and vola.
5. When price crosses upper, go long; when price crosses lower, close the position.
Through this method, the trend can be tracked in time when the price enters the trend state; at the same time, the risk can also be controlled through volatility.
## Advantage Analysis
This strategy has several advantages:
1. Can effectively track trends and capture price changes in a timely manner
2. Using the middle price of the highest and lowest prices as the base price can reduce the probability of false breakthroughs
3. Volatility can be automatically adjusted to control risk
4. The position holding time is short and you can obtain higher frequency trading opportunities.
5. Simple to implement, easy to understand and optimize
## Risk Analysis
There are also some risks with this strategy:
1. There may be more unnecessary transactions in volatile market conditions
2. The setting of ATR size and multiple will affect the strategy performance and requires careful testing and optimization.
3. A pullback may occur after breaking through the middle price, resulting in a stop loss
4. If the trend reverses too quickly, it will cause large losses
In order to control these risks, optimization can be done from the following aspects:
1. Adjust ATR parameters, reduce volatility, and filter shocks
2. Add filter conditions to avoid unnecessary transactions
3. Use a trailing stop to lock in profits
4. Use trend indicators to determine the beginning and end of the real trend
## Optimization direction
This strategy also has room for further optimization:
1. Can test the parameter effects of different markets and different cycles
2. Can be combined with machine learning algorithms to automatically optimize parameters
3. More indicators can be combined to determine the start and end of the trend.
4. You can consider dynamically adjusting the position ratio
5. You can combine sentiment indicators to avoid being biased by extreme emotions.
Through these optimizations, we can expect to further improve the stability and profitability of the strategy.
## Summarize
The High Low Center Lookback Strategy is a simple and practical trend following strategy. It can capture price changes in time, track trends, and control risks through volatility. This strategy is easy to implement and suitable for beginners of quantitative trading to learn and practice. Through parameter optimization and rule optimization, the effect of the strategy can be further improved. Overall, this is a quantitative strategy worth recommending.
|| 

## Overview

The Highest/Lowest Center Lookback strategy is a trend following strategy. Its main idea is to calculate the middle price of the highest and lowest prices over a certain period in the past as the benchmark price, and then calculate the entry zone and exit zone based on this benchmark price combined with volatility. When the price enters the entry zone, go long; when the price enters the exit zone, close the position.

## Strategy Logic

The strategy is mainly implemented through the following steps:

1. Calculate the highest price h and lowest price l over the past lookback_length periods, and smooth them with EMA
2. Calculate the middle price of h and l as the center price 
3. Calculate volatility vola based on ATR and ATR multiplier
4. Calculate entry zone upper and exit zone lower based on center and vola
5. When price price breaks above upper, go long; when price breaks below lower, close position

In this way, it can track the trend in time when price enters a trend state; at the same time, risk can be controlled through volatility.

## Advantage Analysis 

This strategy has the following advantages:

1. Can effectively track trends and capture price changes in time
2. Using the middle price of highest and lowest prices can reduce the probability of false breakouts  
3. Volatility can be automatically adjusted to control risk
4. Position holding time is short, allowing more frequent trading opportunities
5. Simple to implement and easy to understand and optimize

## Risk Analysis

The strategy also has some risks:  

1. More unnecessary trades may occur in range-bound markets
2. The settings of ATR size and multiplier will affect strategy performance, requiring careful testing and optimization
3. Pullback after breaking the middle price may cause stop loss
4. If the trend reversal speed is too fast, it will lead to greater losses

To control these risks, optimization can be done in the following aspects:

1. Adjust ATR parameters to reduce volatility and filter whipsaws
2. Add filters to avoid unnecessary trades 
3. Use moving stop loss to lock in profits
4. Combine trend indicators to judge real trend start and end  

## Optimization Directions

The strategy also has room for further optimization:

1. Test parameter effectiveness across different markets and timeframes
2. Automatically optimize parameters with machine learning algorithms
3. Incorporate more indicators to judge trend start and end
4. Consider dynamically adjusting position sizing
5. Incorporate sentiment indicators to avoid bias from extreme emotions

Through these optimizations, further improvements in strategy stability and profitability can be expected.  

## Conclusion

The Highest/Lowest Center Lookback strategy is a simple and practical trend following strategy. It can capture price changes in time, track trends, while controlling risk through volatility. The strategy is easy to implement, suitable for quantitative trading beginners to learn and practice. By optimizing parameters and rules, the strategy performance can be further improved. In general, this is a recommended quantitative strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|Lookback Length|
|v_input_2|5|Smoother Length|
|v_input_3|10|ATR Length|
|v_input_4|1.5|ATR Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-27 00:00:00
end: 2023-12-27 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Highest/Lowest Center Lookback Strategy", overlay=true)

lookback_length = input(200, type=input.integer, minval=1, title="Lookback Length")
smoother_length = input(5, type=input.integer, minval=1, title="Smoother Length")
atr_length = input(10, type=input.integer, minval=1, title="ATR Length")
atr_multiplier = input(1.5, type=input.float, minval=0.5, title="ATR Multiplier")

vola = atr(atr_length) * atr_multiplier
price = sma(close, 3)

l = ema(lowest(low, lookback_length), smoother_length)
h = ema(highest(high, lookback_length), smoother_length)
center = (h + l) * 0.5
upper = center + vola
lower = center - vola
trend = price > upper ? true : (price < lower ? false : na)

bull_cross = crossover(price, upper)
bear_cross = crossunder(price, lower)

strategy.entry("Buy", strategy.long, when=bull_cross)
strategy.close("Buy", when=bear_cross)

plot(h, title="High", color=color.red, transp=75, linewidth=2)
plot(l, title="Low", color=color.green, transp=75, linewidth=2)

pc = plot(center, title="Center", color=color.black, transp=25, linewidth=2)
pu = plot(upper, title="Upper", color=color.green, transp=75, linewidth=2)
pl = plot(lower, title="Lower", color=color.red, transp=75, linewidth=2)

fill(pu, pc, color=color.green, transp=85)
fill(pl, pc, color=color.red, transp=85)

bgcolor(trend == true ? color.green : (trend == false ? color.red : color.gray), transp=85)
```

> Detail

https://www.fmz.com/strategy/436878

> Last Modified

2023-12-28 15:42:10
