
> Name

Quantitative trading strategy Fibonacci-Retracement-Quantitative-Trading-Strategy based on Fibonacci retracement
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/5ec37b50b669a9ca79ff7164b184d0ddecd14eb5f83b2d702461275a0ee6beed.png)

[trans]

## Overview
This strategy is designed based on the Fibonacci retracement principle. Buy or sell when prices rise or fall and approach key Fibonacci retracement levels. This strategy uses Fibonacci theory to determine the key points of price reversal, enter the market appropriately before the trend reverses, and aim to obtain excess returns that exceed the market.
## Principle
The strategy first calculates the highest price and lowest price in the last 50 days to obtain the price increase or decrease. Then based on the three key Fibonacci levels of 0.236, 0.382, and 0.618, the corresponding price retracement position is calculated. When the price rises and approaches the 0.618 level (the golden section), go long; when the price falls and approaches the 0.236 level, close the position.
This strategy is based on Fibonacci retracement theory. Any number in the Fibonacci sequence is approximately equal to the ratio of the previous two numbers, and this ratio is close to 0.618. Fibonacci retracement theory believes that when the price approaches the 0.382 or 0.618 level after rising or falling, a reversal is likely to occur. This strategy uses this rule to determine the timing of operations.
## Advantages
This is a more typical crossing trading strategy. Its biggest advantage is that it can judge the key point of price reversal in advance and enter the market appropriately before the trend turns. In addition, Fibonacci theory is widely used in technical analysis, which gives this strategy a certain academic basis.
## Risk
The main risk of this strategy is the risk that the price will continue to run after breaking through the Fibonacci retracement level, leading to the risk of expanding losses. In addition, any trading strategy based on empirical judgment cannot completely avoid losses caused by incorrect judgment.
In order to control risks, you can set a stop loss position and exit when the loss expands to a certain extent. In addition, the position of Fibonacci retracement can be appropriately adjusted according to market conditions to make trading signals more reliable.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Dynamically adjust Fibonacci retracement levels, and different parameters can be set at different market stages to make trading more flexible;
2. Combine with other indicators for filtering, such as increasing the judgment of trading volume, using moving averages, etc., to make the signal more reliable;
3. Optimize the stop loss strategy and better control risks through trailing stop loss, interval stop loss, etc.;
4. Test longer data periods to verify the stability of the strategy; adjust the holding time to maximize returns.
## Summarize
This strategy is based on Fibonacci theory to determine the price reversal point and is a typical crossover trading strategy. Have a certain basis for technical analysis and be able to seize price turning opportunities in advance. However, there is also a certain risk of loss. By dynamically adjusting parameters, setting stop losses, adding filter conditions, etc., it can be continuously optimized to make the strategy more stable and profitable.
||


## Overview

This strategy is designed based on the Fibonacci retracement principle. It enters long or short positions when prices rise or fall and approach key Fibonacci retracement levels. The strategy utilizes Fibonacci theory to identify critical reversal points in prices and appropriately enters positions ahead of trend reversals, aiming for excess returns over the broader market.  

## Principles

The strategy first calculates the highest and lowest prices over the past 50 days to determine price movement range. It then uses three key Fibonacci ratios - 0.236, 0.382 and 0.618 to calculate corresponding retracement levels. It goes long when prices rise and approach the 0.618 level (golden ratio), and closes long positions when prices fall to 0.236 level.

The strategy leverages the Fibonacci retracement theory, which observes that in a Fibonacci sequence, any number is approximately equal to the ratio of the preceding two numbers, and this ratio is close to 0.618. The theory suggests that prices tend to reverse when retracing to 0.382 or 0.618 levels after a rise or fall. This strategy hence utilizes this pattern to determine entry and exit signals.

## Advantages  

This is a typical breakout trading strategy. Its biggest edge is the ability to identify key reversal points beforehand and appropriately enter positions before trend reversals. Additionally, Fibonacci theory is widely applied in technical analysis, giving this strategy academic merits.

## Risks

The main risk is prices continuing to trend after penetrating Fibonacci retracement levels, thus amplifying losses. Moreover, empirical trading strategies cannot completely avoid losses due to misjudged signals.  

To mitigate risks, stop losses can be set to exit positions if losses exceed certain threshold. Fibonacci levels can also be dynamically adjusted based on changing market conditions to generate more reliable signals.

## Enhancement Areas

The strategy can be optimized in the following ways:

1. Dynamically adjust Fibonacci levels based on varying market stages, allowing for more flexibility.

2. Add other indicators for signal filtering, e.g. volume, moving averages etc, to make signals more reliable.  

3. Optimize stop loss mechanisms with trailing stops, zone stops etc to better control risks.

4. Test over longer time frames to verify stability; adjust holding period to maximize returns.


## Conclusion  

This strategy identifies price reversal points based on Fibonacci theory, belonging to the breakout trading category. It has academic merits in seizing turning point opportunities ahead of the market, but also bears certain probability of losses. Continual optimizations around adaptive parameters, stop losses, extra signal filtering etc can enhance its profitability and stability.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Fibonacci cycle length|
|v_input_2|0.236|Fibonacci Level 1|
|v_input_3|0.382|Fibonacci Level 2|
|v_input_4|0.618|Fibonacci Level 3|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-21 00:00:00
end: 2023-11-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("斐波那契回撤交易策略", overlay=true, initial_capital=10000)

// 参数
length = input(50, title="斐波那契周期长度")
fib1 = input(0.236, title="斐波那契水平1")
fib2 = input(0.382, title="斐波那契水平2")
fib3 = input(0.618, title="斐波那契水平3")

// 计算斐波那契水平
highLevel = ta.highest(high, length)
lowLevel = ta.lowest(low, length)
range1 = highLevel - lowLevel
fibLevel1 = highLevel - range1 * fib1
fibLevel2 = highLevel - range1 * fib2
fibLevel3 = highLevel - range1 * fib3

// 条件
longCondition = ta.crossover(close, fibLevel3)
shortCondition = ta.crossunder(close, fibLevel1)

// 下单
strategy.entry("Buy", strategy.long, when=longCondition)
strategy.close("Buy", when=shortCondition)

// 图表标记
plot(fibLevel1, title="Fib 0.236", color=color.red)
plot(fibLevel2, title="Fib 0.382", color=color.orange)
plot(fibLevel3, title="Fib 0.618", color=color.green)

```

> Detail

https://www.fmz.com/strategy/432798

> Last Modified

2023-11-21 15:57:11
