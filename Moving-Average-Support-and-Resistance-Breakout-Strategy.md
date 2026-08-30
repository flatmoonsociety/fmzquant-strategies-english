
> Name

Moving-Average-Support-and-Resistance-Breakout-Strategy Based on Moving Average
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy identifies key support and resistance price areas based on moving averages and trades when these areas break out. The strategy is simple and effective, easy to understand and implement.
## Strategy Principle
This strategy uses a 50-period simple moving average SMA to identify key areas of support and resistance. Specifically:
- When the closing price breaks through the SMA from below, take the highest price in the past 50 periods as the resistance level R
- When the closing price falls below the SMA from above, the lowest price in the past 50 periods is taken as the support level S
- When the closing price exceeds the resistance R, go long
- When the closing price falls below the support S, go short
That is, this strategy uses SMAs of 50-period length to divide price zones and trade in the opposite direction when price breaks out of these zones. Go long when resistance is broken, go short when support is broken. The strategy is simple, clear and easy to operate.
## Advantage Analysis
This strategy has the following advantages:
1. Using moving averages to identify support and resistance has certain reliability and can effectively filter out false breakthroughs.
2. The length of the 50 cycle is neither long nor short, and more important mid-term support and resistance can be identified.
3. Using only one SMA indicator, the system overhead is small and easy to implement.
4. The breakthrough trading strategy is simple, effective and easy to operate.
5. There are few configurable parameters and it is not easy to over-optimize.
## Risk Analysis
This strategy also has the following risks:
1. There is still a certain risk of false breakthroughs, and the moving average cannot completely filter it.
2. The fixed cycle cannot adapt to various market cycles and may miss opportunities in shorter cycles.
3. After the breakthrough, there may be a callback to test the previous high and low, which requires certain stop loss skills.
4. When holding a long-term position, you need to pay attention to the trend direction of a larger level.
To address these risks, optimization can be achieved by appropriately adjusting the moving average cycle or adding trend filter indicators. At the same time, it is very important to do a good job in stop loss management.
## Optimization direction
This strategy can be optimized from the following directions:
1. Add indicators such as MACD to assist in judging the direction and strength of the trend.
2. Add adaptive optimization of MA cycle so that the cycle can be dynamically adjusted.
3. Optimize breakthrough identification, such as requiring simultaneous breakthrough of MA and Bollinger Band upper and lower rails, etc.
4. Add a stop-loss mechanism to control single losses.
5. Try different MA cycle parameters to find the optimal parameter combination.
Through these optimizations, the strategy can be made more flexible and effective in different market cycles.
## Summarize
Overall, this strategy uses simple moving averages to identify support and resistance areas and conduct price breakthrough operations, which is simple and efficient. The optimization space is also large and can be improved from multiple dimensions. Although there is a certain risk of false breakthroughs, reasonable stop loss configuration can effectively control it. The strategy is clear and easy to understand, and is very suitable for beginners to practice as an introductory strategy.
||


## Overview

This strategy identifies key support and resistance levels based on moving averages, and takes trades when price breaks through these levels. The strategy is simple and effective, easy to understand and implement.

## Strategy Logic

The strategy uses a Simple Moving Average (SMA) with a period of 50 to identify support and resistance zones. Specifically:

- When close price crosses above SMA from below, the highest high over the past 50 periods is taken as resistance R
- When close price crosses below SMA from above, the lowest low over the past 50 periods is taken as support S
- Go long when close exceeds resistance R
- Go short when close breaks support S

In other words, the strategy uses the 50-period SMA to divide price zones, and takes trades when price breaks out of these zones. It goes long on breakouts above resistance, and goes short on breakdowns below support. The strategy is straightforward and easy to execute.

## Advantage Analysis 

The strategy has the following advantages:

1. Using moving averages to identify support/resistance is reasonably reliable and can effectively filter false breakouts.
2. A period of 50 is neither too long nor too short, and can detect meaningful medium-term levels.
3. It uses only a single SMA indicator, resulting in low system overhead and easy implementation.
4. Breakout trading strategies are simple and effective. 
5. There are few tunable parameters, avoiding excessive optimization.

## Risk Analysis

The strategy also has the following risks:

1. There is still some risk of false breakouts that SMAs cannot completely filter out.
2. The fixed period cannot adapt to different market cycles, potentially missing shorter-term opportunities.  
3. There may be pullbacks and retests after initial breakouts, requiring prudent stop loss techniques.
4. Larger trend direction needs to be monitored for longer-term trades.

These risks can be addressed through optimizations like adjusting the SMA period, adding trend filter indicators, etc. Proper stop loss management is also very important.

## Optimization Directions

Some ways the strategy can be enhanced:

1. Add indicators like MACD to help gauge trend direction and momentum.  
2. Implement adaptive optimization of MA periods for dynamic adjustment.
3. Improve breakout detection, e.g. requiring concurrent break of MA and Bollinger Bands.
4. Incorporate stop loss mechanisms to control single trade loss.
5. Test different MA period parameters to find optimal combinations.

These improvements can make the strategy more robust across different market cycles.

## Summary

Overall, the strategy identifies support/resistance with SMAs and trades breakouts, keeping things simple and effective. There is also significant room for optimization across multiple dimensions. While false breakouts remain a risk, prudent stop loss usage can effectively control this. The strategy is easy to understand for beginners and great for gaining practical experience.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Number of lookback periods|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//--------------------------*
//-- This source code is subject to the terms of the Mozilla Public License 2.0
//-- 開源代碼受Mozilla公眾授權條款2.0版規範, 網址是https://mozilla.org/MPL/2.0/
//
//@version=4
//
//  作品: [LunaOwl] 支撐壓力策略第4版
//  英文: [LunaOwl] Support Resistance Strategy V4
//
////////////////////////////////
//     ~~!!*(๑╹◡╹๑) **       //
//  製作:  @LunaOwl 彭彭      //
//  日期:  2019年03月05日     //
//  修改:  2019年04月22日     //
//  四版:  2020年06月16日     //
//  發表:  2020年06月17日     //
////////////////////////////////

//==設定策略==//

strategy("[LunaOwl] 支撐壓力策略 [回測]",
     shorttitle          = "支撐壓力策略 [回測]",
     overlay             = true,
     calc_on_order_fills = false,
     calc_on_every_tick  = false,
     pyramiding          = 0,
     currency            = currency.NONE,
     initial_capital     = 10000,
     slippage            = 5,
     default_qty_value   = 100,
     default_qty_type    = strategy.percent_of_equity,
     commission_type     = strategy.commission.percent,
     commission_value    = 0.05
     )

LB = input(50, title = "回溯期數", type = input.integer)
R = valuewhen(cross(sma(close, LB),close), highest(high, LB), 1)
S = valuewhen(cross(close,sma(close, LB)),  lowest( low, LB), 1)

plot(R, title = "壓力", color = color.green)
plot(S, title = "支撐", color = color.red)

//==定義輸出結果==//

Trend_up = crossover(close, R) ? 1 : 0
Trend_dn = crossunder(close, S) ? -1 : 0

//==設定出場規則==//

Enter = Trend_up ==  1 and Trend_up[1] == 0 ? Trend_up : na
Exit  = Trend_dn == -1 and Trend_dn[1] == 0 ? Trend_dn : na
strategy.entry("多", strategy.long, when = Enter)
strategy.entry("空", strategy.short, when = Exit)
```

> Detail

https://www.fmz.com/strategy/428086

> Last Modified

2023-09-28 15:20:47
