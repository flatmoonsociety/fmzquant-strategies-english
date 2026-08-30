
> Name

ATR-based trailing stop loss strategy is only long ATR-Trailing-Stop-Strategy-Long-Only
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b27c2ccb1840ef780e.png)
[trans]

## Overview
This strategy sets two dynamic stop-loss prices with different parameters based on the ATR indicator, a fast stop-loss and a slow stop-loss. Based on the price breaking through different stop-loss prices, a long position or a stop-loss exit position is established. The purpose of the strategy is to use the ATR indicator to set a reasonable stop loss position and try to track the rising price trend while ensuring the stop loss.
## Strategy Principle
This strategy uses the ATR indicator to calculate the stop loss position for two different parameters. The fast stop loss uses a 5-period ATR multiplied by 0.5 as the stop loss width; the slow stop loss uses a 10-period ATR multiplied by 3 as the stop loss width. When the price rises and breaks through the fast stop loss price, a long position is established; when the price continues to rise and breaks through the slow stop loss price, the stop loss position is adjusted to the slow stop loss price. If the price turns down, move the stop loss position based on the breakout relationship between the two.
The specific logic is:
1. Calculate the quick stop loss price Trail1:5 period ATR multiplied by 0.5
2. Calculate the slow stop loss price Trail2: 10-period ATR multiplied by 3
3. When the price rises above Trail1, establish a long position
4. When the price continues to rise and breaks through Trail2, adjust the stop loss position to Trail2
5. If the price turns down and breaks through Trail1, adjust the stop loss position back to Trail1
6. If the price continues to fall and breaks through Trail2, adjust the stop loss position to Trail2
7. Finally, if the price triggers the stop loss level, stop the loss and exit the position.
In this way, you can try to follow the trend and run profits when the price rises, and stop the loss in time when the price turns back to fall. At the same time, the two stop loss prices, fast and slow, can balance the relationship between stop loss and tracking.
## Strategic Advantages
1. Use the ATR indicator to dynamically set the stop loss position and reasonably set the stop loss range according to market volatility.
2. The double stop-loss mechanism can balance the relationship between stop-loss and tracking, and can both stop loss and chase increases.
3. The long direction is in line with the general trend and easy to make profits
4. The strategy logic is simple and clear, easy to understand and implement
5. The stop-loss rules are strict and effective, allowing you to stop losses in time and control losses.
## Strategy Risk
1. Improper setting of ATR indicator parameters may cause the stop loss to be too loose or too tight.
2. There is directional risk in the long direction, and it is easy to stop losses when the market tops.
3. The double stop loss rule is complicated and may fail if the parameters are set improperly.
4. Failure to consider filtering conditions such as breaking through EMA, and there is a risk of mistaken transactions
5. Without considering capital management and position management, there is a risk of overbought and oversold.
In response to the above risks, risks can be reduced by optimizing ATR parameters, adding filter conditions, and strengthening fund management.
## Strategy optimization direction
1. Optimize the ATR parameter combination and find the best parameters
2. Add EMA and other indicators to judge Filters in corresponding Barriers
3. Judgment based on Stoch RSI and other indicators again
4. Add re-entry mechanism to optimize position management
5. Optimize fund management rules and control single stop loss ratio
6. Combine btc10 wsb full network positions to avoid overall directional errors
7. Consider adding hourly strategies
8. Upgrade to a market-wide multi-variety strategy
9. Deploy high-performance trading engine
Through the above optimization points, the risk of mistaken transactions can be reduced and the stability of the strategy and winning rate can be improved.
## Summarize
The overall idea of ​​this strategy is clear, using the ATR indicator double stop loss method to establish a long position and trail the stop loss. The advantage of the strategy is that the stop loss rules are strict, the risk of loss can be controlled, and the logic is simple and easy to implement. There is a certain directional risk, and the risk can be reduced and the effect improved by optimizing parameter combinations, adding filter conditions, improving fund management, etc. If optimization and testing continue, this strategy can become a stable and reliable trend following strategy.
||


## Overview

This strategy uses two ATR stops with different parameters to set dynamic stop loss levels - one fast stop and one slow stop. It establishes long positions based on price breakouts of the different stop levels and exits positions using the trailing stops. The goal is to use ATR stops to set reasonable stop loss levels while maximizing the trend following ability.

## Strategy Logic

The strategy uses ATR indicator to calculate two stop loss levels. The fast stop uses 5-period ATR multiplied by 0.5 as the stop distance. The slow stop uses 10-period ATR multiplied by 3 as the stop distance. When price breaks above the fast stop level, a long position is established. When price continues to break above the slow stop level, the stop is adjusted to the slow stop level. If price turns down, the stop level is adjusted based on the crossover relationships. 

The logic is:

1. Calculate fast stop Trail1: 5-period ATR * 0.5

2. Calculate slow stop Trail2: 10-period ATR * 3 

3. When price breaks above Trail1, establish long position

4. When price continues to break above Trail2, adjust stop to Trail2

5. If price turns down breaking Trail1, adjust stop back to Trail1

6. If price continues down breaking Trail2, adjust stop to Trail2

7. Finally, if price hits the stop level, exit the position with stop loss

This way, the strategy can maximize the profit during uptrends with the trailing stops while quickly stopping out losses when the trend reverses. The two stops also balance between capturing trends and limiting losses.

## Advantages

1. ATR stops set dynamic stop loss levels based on market volatility

2. Dual stop mechanism balances between stopping losses and trailing trends

3. Long direction aligns with overall uptrend, higher profitability

4. Simple and clear logic, easy to understand and implement

5. Strict stop loss rules limit losses effectively

## Risks

1. Improper ATR parameters may cause stops being too wide or too tight

2. Long direction has directional bias, prone to stops at market tops

3. Dual stop rules are complex, may fail if not set properly

4. No filters such as EMA crossovers, may cause bad trades

5. No position or risk management, risks of overtrading

These risks can be reduced by optimizing ATR parameters, adding filters, and enforcing risk management.

## Improvement Areas

1. Optimize ATR parameter combinations for best results

2. Add filters like EMA to qualify entry signals

3. Incorporate indicators like Stoch RSI for additional edge

4. Add re-entry logic to optimize position management 

5. Optimize risk management rules to limit per trade stop loss

6. Incorporate market-level analytics to avoid directional mistakes

7. Consider faster timeframe strategies like hourly

8. Expand to multi-market universal strategy

9. Deploy high performance trading engine

With these improvements, the strategy can be more robust, stable and profitable.

## Summary

The strategy uses clear ATR trailing stops for long entries and exits. The advantages lie in its strict stop loss rules to limit losses while trailing trends. It has directional bias risks that can be reduced through optimizations like better parameters, adding filters and enhancing risk management. With further testing and improvements, this can become a reliable trend following strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|5|Fast ATR period|
|v_input_3|0.5|Fast ATR multiplier|
|v_input_4|10|Slow ATR period|
|v_input_5|3|Slow ATR multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-25 00:00:00
end: 2023-11-01 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("ATR Trailing Stop Strategy (Long Position Only)", overlay=true)

SC = input(close, "Source", input.source)

// Fast Trail
AP1 = input(5, "Fast ATR period", input.integer)
AF1 = input(0.5, "Fast ATR multiplier", input.float)
SL1 = AF1 * atr(AP1)
Trail1 = 0.0
Trail1 := iff(SC > nz(Trail1[1], 0) and SC[1] > nz(Trail1[1], 0), max(nz(Trail1[1], 0), SC - SL1), iff(SC < nz(Trail1[1], 0), SC + SL1, na))

// Slow Trail
AP2 = input(10, "Slow ATR period", input.integer)
AF2 = input(3, "Slow ATR multiplier", input.float)
SL2 = AF2 * atr(AP2)
Trail2 = 0.0
Trail2 := iff(SC > nz(Trail2[1], 0) and SC[1] > nz(Trail2[1], 0), max(nz(Trail2[1], 0), SC - SL2), iff(SC < nz(Trail2[1], 0), SC + SL2, na))

Green = Trail1 > Trail2 and close > Trail2 and low > Trail2

Buy = crossover(Trail1, Trail2)

plotshape(Buy, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small)

strategy.entry("Buy", strategy.long, when = Buy)

var float trailingStopPrice = na
if (Trail2 > trailingStopPrice)
    trailingStopPrice := Trail2

if (crossover(Trail1, Trail2))
    trailingStopPrice := Trail2

strategy.exit("Exit", from_entry = "Buy", stop=trailingStopPrice)

```

> Detail

https://www.fmz.com/strategy/430836

> Last Modified

2023-11-02 14:05:22
