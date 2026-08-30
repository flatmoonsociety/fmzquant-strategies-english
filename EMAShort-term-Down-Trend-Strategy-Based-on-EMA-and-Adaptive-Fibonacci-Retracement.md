
> Name

Short-term-Down-Trend-Strategy-Based-on-EMA-and-Adaptive-Fibonacci-Retracement
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the EMA indicator to determine the trend direction, and combines it with the adaptive Fibonacci retracement to automatically determine the reversal point, realize buying low and sell high, and capture the downward trend. The strategy operates frequently and is suitable for short-term trading.
## Strategy Principle
1. Use the 9-day EMA and the 21-day EMA to form a golden cross to determine the trend direction. The 21-day EMA crossing below the 55-day EMA is regarded as a signal to start the downward trend.
2. Set up an adaptive Fibonacci retracement indicator with a length of 100 periods, and automatically determine the key retracement ratio based on the recent price shock range.
3. When the price breaks through the 0.236 Fibonacci retracement, it is regarded as a reversal signal and the original position is closed.
4. When the 9-day EMA crosses below the 21-day EMA and the price is below the adaptive Fibonacci high, enter the market short.
5. The profit exit condition for longs is to break through the 200-day EMA. The short stop loss exit condition is a breakthrough of 0.236 Fibonacci retracement.
## Strategic Advantages
- Use EMA to determine the trend direction, and the operating signals are simple and clear
- Adaptive Fibonacci retracement, no need to manually determine parameters
- Frequent strategy operations can capture short-term changes and implement high-frequency strategies
- Use key retracement points to determine reversals and stop losses in a timely manner
- Configurable parameters to optimize strategies to suit different cycles
## Strategy Risk
- There is a lag in the EMA indicator, and other indicators need to be combined for confirmation.
- Adaptive Fibonacci may be over-optimized and the retracement points may be unstable
- High-frequency trading increases transaction costs and slippage costs
- Unable to effectively filter oscillatory trends, there are too many false signals
- Drawback management and profit-loss ratio control need to be improved
## Strategy optimization direction
- Add volume and energy indicators to avoid false signals caused by volume and price divergence
- Optimize EMA cycle parameters to make them more in line with the current market environment
- Set dynamic stop loss to better control risks
- Combined with trend strength indicators to avoid repeated trading during shock periods
- Consider the impact of actual transaction costs and set a minimum take-profit range
## Summarize
This strategy uses EMA to identify the trend direction and uses adaptive Fibonacci retracements to dynamically determine reversal points, which can automatically adapt to different market changes. However, this strategy relies more on indicator prompts, lacks trend segmentation and wave judgment logic, and has large room for optimization. Overall, as a high-frequency short-term trading strategy, it can capture faster price changes, but it requires traders to bear the risks of frequent stop losses and prevent over-trading.
|| 

## Overview

This strategy uses EMA to determine trend direction and adaptive Fibonacci retracement to automatically identify reversal points, aiming to sell high and buy low by catching down trends. It involves frequent trading suitable for short-term trading.

## Strategy Logic 

1. Use 9-day EMA and 21-day EMA golden cross and death cross to determine trend direction. 21-day EMA crossing below 55-day EMA signals a down trend start.

2. Implement adaptive Fibonacci retracement with 100 periods to automatically determine key retracement levels based on recent price swings. 

3. Price breaking 0.236 Fibonacci retracement indicates a reversal and closes existing position.

4. When 9-day EMA crosses below 21-day EMA, and price is lower than adaptive Fibonacci high, go short.

5. Long profit target is a crossover above 200-day EMA. Short stop loss is breaking 0.236 Fibonacci retracement.

## Advantages

- EMA gives clear trend signals, easy to implement

- Adaptive Fibonacci avoids manual parameter tuning

- Frequent trading catches short-term moves for high frequency strategies

- Key retracement levels for timely stop loss 

- Configurable parameters for optimization across cycles

## Risks

- EMA lagging requires confirmation from other indicators

- Adaptive Fibonacci risks overfitting with unstable levels

- High frequency trading increases costs from commissions and slippage

- Ineffective filtering of range-bound trends leads to false signals

- Needs improvement in drawdown management and risk-reward control

## Enhancement

- Add volume indicators to avoid false signals from price-volume divergence

- Optimize EMA periods to better fit current market conditions

- Implement dynamic stop loss for better risk control

- Incorporate trend strength index to avoid whipsaws

- Consider trading costs impact and set minimum profit target

## Conclusion

This strategy identifies trend direction with EMA and determines reversal levels dynamically using adaptive Fibonacci retracement, which automatically adapts to different market conditions. But it relies more on indicator cues without trend segmentation and Elliott Wave logic, leaving room for optimization. Overall, as a high frequency short-term trading strategy, it can capture fast price changes but involves risks of frequent stop loss and overtrading that traders need to manage.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|100|(?Automatic Fibonacci Retracement)Fibonacci Length|
|v_input_int_2|true|Show Last|
|v_input_int_3|5|Offset Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © CheatCode1

//@version=5
strategy("CC-Trend strategy 2", overlay=true, initial_capital = 10000, commission_type = strategy.commission.percent, commission_value = 0.01, default_qty_type =  strategy.percent_of_equity, default_qty_value = 100 )
ema9 = ta.ema(close, 9)
ema21 = ta.ema(close, 21)
ema55 = ta.ema(close, 55)
ema200 = ta.ema(close, 200)


plot(ema200, '22', color.blue, 2)

FibL = input.int(100, 'Fibonacci Length', 1, 500, group = 'Automatic Fibonacci Retracement')
len1 = input.int(1, 'Show Last', 0, 1000, group = 'Automatic Fibonacci Retracement')
len2 = input.int(5, 'Offset Length', 0, 1000, group = 'Automatic Fibonacci Retracement')

highF = ta.highest(ema55 >= ema9 ? ema55:ema9, FibL)
lowF = ta.lowest(ema55 >= ema9 ? ema9:ema55, FibL)
AvgFib = highF - lowF

//Fibonacci Executions
LL2 = highF + .618 * AvgFib
LL1 = highF + .272 * AvgFib
L1 = highF
L236 = highF - 0.236 * AvgFib
L382 = highF - 0.382 * AvgFib
Mid =  highF - 0.50 * AvgFib
S382 = lowF + 0.382 * AvgFib
S236 = lowF + 0.236 * AvgFib
S1 = lowF
SS1 = lowF - .272 * AvgFib
SS2 = lowF - .618 * AvgFib
//Fibonacci Plot's


high2FP = plot(LL2, 'Highe2', color.red,offset = len2, show_last = len1, trackprice = true)
high1FP = plot(LL1, 'Highe1', color.red,offset = len2, show_last = len1, trackprice = true)
highFP = plot(highF, 'High', color.red,offset = len2, show_last = len1, trackprice = true)
L236P = plot(L236, "0.764", #ED381C, offset = len2, show_last = len1, trackprice = true )
L382P = plot(L382, "0.618", color.white,offset = len2, show_last = len1, trackprice = true )
MidP = plot(Mid, "0.5", color.orange,offset = len2, show_last = len1, trackprice = true )
S382P = plot(S382, "0.382", color.yellow ,offset = len2, show_last = len1, trackprice = true)
S236P = plot(S236, "0.236", color.lime ,offset = len2, show_last = len1, trackprice = true)
lowFP = plot(lowF, 'Low', color.green,offset = len2, show_last = len1, trackprice = true)
low1FP = plot(SS1, 'Lowe1', color.green,offset = len2, show_last = len1, trackprice = true)
low2FP = plot(SS2, 'Lowe2', color.green,offset = len2, show_last = len1, trackprice = true)

plot(ema9, '22', color.yellow, 2)

plot(ema55, '55', color.aqua, 2)

plot(ema200, '200', color.maroon, 2)



shortCondition = close[1] < highF and ema21 < ema55
if (shortCondition)
    strategy.entry("Short", strategy.short)

shorttp = ta.crossover(close, ema200) and strategy.openprofit >= 0
if (shorttp)
    strategy.close('Short', 'Short TP', qty_percent = 100)

shortclose2 = close[1] > L236 and not (shortCondition) 
if(shortclose2)
    strategy.close('Short', 'Short RM', qty_percent = 100)
```

> Detail

https://www.fmz.com/strategy/427528

> Last Modified

2023-09-21 21:36:16
