
> Name

Bull-Market-Chasing-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The main idea of ​​this strategy is to use the simple moving average indicator EMA to achieve trend following. Go long when the short-term EMA crosses above the long-term EMA, and close when the short-term EMA crosses below the long-term EMA. This strategy is suitable for varieties with large fluctuations in the bull market and can obtain larger trend profits.
## Strategy Principle
This strategy is mainly based on the golden cross and dead cross of the EMA indicator to determine the timing of buying and selling. Two EMA periods are defined in the code, a short-term EMA period of 10 and a long-term EMA period of 60. Calculate these two EMA values ​​separately. When the short-term EMA crosses above the long-term EMA, it means that the price upward momentum is strong, and you will go long at this time; when the short-term EMA crosses below the long-term EMA, it means that the price upward momentum is weak, and you will close your position at this time.
The core logic of this strategy is to use the golden cross and dead cross of EMA to judge the trend, which is a typical trend following strategy. As a trend index smoothed moving average, EMA can better indicate the direction of the price trend. The short-term EMA represents the trend and intensity of recent price changes, and the long-term EMA represents the overall trend direction. If the short-term EMA crosses above the long-term EMA, it means that the recent rise is stronger than the long-term rise, and going long can track the trend; if the short-term EMA crosses below the long-term EMA, it is just the opposite, indicating that the recent rise is not as good as the long-term rise, and the position should be closed.
The entire strategy only uses a simple EMA indicator to judge and track the trend, which is very simple and effective. This is also the biggest advantage of this strategy.
## Advantage Analysis
- The strategy idea is simple and clear. It only uses the EMA indicator to judge the trend, which is very easy to understand and implement.
- High capital utilization efficiency. Only go long and short when the trend is obvious, and will not occupy funds for a long time.
- Using a combination of short-period and long-period EMA, you can smooth out noise and capture the trend over a longer period of time.
- The drawdown of this strategy is relatively small, the maximum drawdown is controlled at around 20%, and it can withstand higher leverage levels.
- Configurable short trading, you can conduct counter-trend trading in a downward trend and obtain additional income.
## Risk Analysis
- As a trend following strategy, it performs poorly in volatile and consolidating markets and is prone to the risk of missing opportunities.
- Unable to determine the logical basis behind the trend, there is a risk of divorce from the trend.
- Improper parameter settings may lead to over-trading or missed trading opportunities.
- Short trading is risky and requires careful allocation.
- This strategy is sensitive to the characteristics of trading varieties, and parameters need to be adjusted for different varieties.
- Slippage control and handling fee issues in the implementation of the trading system will have a certain impact on the actual results.
## Optimization direction
- You can introduce stop-loss strategies, set reasonable stop-loss points, and control the maximum loss in a single transaction.
- Can be combined with other indicators to determine the factors behind the trend to avoid trend divorce. For example, add trading volume analysis.
- Optimal parameter combinations for different varieties can be obtained through parameter optimization.
- You can study different exit strategies and consider exiting with a stop loss when the retracement is too large.
- It can be combined with the position control strategy to dynamically adjust the position size according to the performance of the strategy.
- You can use the step-by-step method to enter the market and establish positions in batches to reduce the risk of a single entry.
## Summarize
This strategy is overall a very simple and straightforward trend following strategy. It uses the EMA indicator to determine the direction of the trend, and uses the EMA's golden cross to go long and the dead cross to close positions, thereby achieving effective tracking of the trend. This strategy has a controlled retracement and is suitable for the trading style of chasing ups and killing downs. However, there is also a certain amount of room for monitoring and optimization, and parameters and exit strategies need to be tested and optimized to adapt to wider market conditions. If it can be improved by combining strategies such as stop loss and position management, the actual effectiveness of this strategy still has a lot of room for improvement.
||


## Overview

The main idea of this strategy is to use the simple moving average indicator EMA to implement trend chasing. It goes long when the short period EMA crosses over the long period EMA and closes position when the short period EMA crosses below the long period EMA. This strategy is suitable for highly volatile assets during a bull market and can capture significant trend profits.

## Strategy Logic

This strategy mainly uses the golden cross and death cross of the EMA indicator to determine entries and exits. The code defines two EMA periods, a short period EMA of 10 and a long period EMA of 60. The values of the two EMAs are calculated respectively. When the short period EMA crosses over the long period EMA, it indicates the upward momentum is strong and should go long. When the short period EMA crosses below the long period EMA, it indicates the upward momentum is weakening and should close position.

The core logic of this strategy is to use the golden cross and death cross of EMA to judge the trend, which is a typical trend chasing strategy. EMA, as a trending exponential smoothing moving average, can indicate the price trend well. The short period EMA represents recent price change trends and momentum, while the long period EMA represents the overall trend direction. When the short period EMA crosses over the long period EMA, it means the short term rising momentum is stronger than the long term momentum, so going long can chase the trend. When the short period EMA crosses below the long period EMA, it indicates the opposite and the position should be closed.

The whole strategy implements trend identification and chasing with simple EMA indicators, which is very concise and effective. This is the biggest strength of this strategy.

## Advantage Analysis

- The strategy idea is simple and clear. It uses EMA indicators to judge the trend, which is easy to understand and implement.

- The capital usage efficiency is high. It only goes long or short when the trend is obvious, without occupying capital for long periods. 

- The combination of short period and long period EMA can smooth noise and capture longer term trends.

- This strategy has relatively small drawdowns, maximum drawdown controlled within 20%, allowing high leverage levels.

- Short selling can be enabled to trade counter trend during down trends for additional profits.

## Risk Analysis

- As a trend chasing strategy, it underperforms during range-bound markets, with the risk of missing opportunities.

- It cannot ascertain the logical basis behind the trend, risking trend divorce. 

- Improper parameter settings may lead to over trading or missing trades.

- Short selling has higher risks and needs to be carefully configured.

- This strategy is sensitive to the characteristics of different trading instruments and parameters need to be adjusted accordingly.

- Real world slippage control and commission fees will impact actual performance to some extent.

## Optimization Directions

- Stop loss strategies can be introduced to set reasonable stop loss points and control maximum loss per trade.

- Other indicators can be incorporated to analyze factors behind the trend to avoid trend divorce, for example trading volumes.

- Parameter optimization can find optimum parameter sets for different trading instruments. 

- Different exit strategies can be researched to consider stop loss exits when drawdown gets too high.

- Position sizing strategies can be used to dynamically adjust position sizes based on performance.

- Stepped entry can be adopted to establish positions in batches, reducing per entry risks. 

## Summary

In summary, this is a very simple and direct trend chasing strategy. It uses EMA indicators to determine trend direction, going long on golden crosses and closing on death crosses to effectively track the trend. This strategy has controlled drawdowns and suits aggressive trading styles. But there are also spaces for monitoring and optimization. Parameters and exit strategies need to be tested and optimized to adapt to more market conditions. Further improvements can be made by incorporating stop loss, position sizing and other strategies. This can greatly improve its practical performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|true|Attiva Short|
|v_input_int_1|10|Periodo Media veloce|
|v_input_int_2|60|Periodo Media lenta|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-20 00:00:00
end: 2023-09-27 00:00:00
period: 45m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © TheSocialCryptoClub

//@version=5
// strategy(title = "STB - Gianno Nano Strategy",
//          shorttitle= "STB - Gianno Nano Strategy",
//          overlay = true,
//          initial_capital = 1000,
//          default_qty_type = strategy.cash,
//          default_qty_value = 1000,
//          commission_type = strategy.commission.percent,
//          commission_value = 0.075)

short_yes = input.bool(true,"Attiva Short")
ema_fast = input.int(10, "Periodo Media veloce")
ema_slow = input.int(60, "Periodo Media lenta")

// Variable declarations

ema10 = ta.ema(close, ema_fast)
ema60 = ta.ema(close, ema_slow)

plot(ema10, "EMA 10", color.yellow, 2)
plot(ema60, "EMA 60", color.aqua, 2)

// Long Condition

long_cond = ta.crossover(ema10, ema60)
short_cond = ta.crossunder(ema10, ema60) and short_yes
close_cond = ta.crossunder(ema10, ema60) and not short_yes
// Engine strategy

if long_cond
    strategy.entry("EL", strategy.long)
if short_cond
    strategy.entry("ES", strategy.short)
if close_cond
    strategy.close("EL" )
    
```

> Detail

https://www.fmz.com/strategy/428106

> Last Modified

2023-09-28 16:23:41
