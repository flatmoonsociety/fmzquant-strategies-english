
> Name

Volume-Ratio-Reversal-Trading-Strategy based on quantitative indicators reversal trading strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1e8c9a422fb3b50d9f7.png)
[trans]

## Overview
Volume Ratio reversal trading strategy (VR reversal strategy) is a short-period reversal trading strategy based on volume indicator. It determines whether the main force of the market has entered by calculating the ratio of trading volume to average volume within a certain period of time, thereby generating trading signals. This strategy is mainly suitable for varieties with strong reversal in the short-term range.
## Strategy Principle
The core indicator of the VR reversal strategy is Volume Ratio (VR for short), which represents the ratio of the current period’s trading volume to the average trading volume over a period of time. The specific calculation method is:
VR = Current Volume / SMA(Volume, N)

Where N represents the parameter Length, the current period's trading volume is divided by the simple moving average of the trading volume within the Length period.
When VR > threshold, it is considered a signal for the main force to enter. At this time, combined with the upward or downward breakthrough of the price, buy and sell signals are generated.
This strategy also introduces the direction auxiliary judgment indicator dir. It compares the closing price of the current period with the closing price of N periods ago. If it is greater than 1, it is a long direction, and if it is less than 1, it is a short direction.
When VR is greater than the specified threshold, if dir=1, a buy signal is generated, and if dir=-1, a sell signal is generated.
## Advantages
The biggest advantage of the VR reversal strategy is to capture sudden price reversal opportunities. When there is a signal for the main force to intervene, the strategy can make quick judgments and seize the opportunity of rebound or pullback in time.
Other advantages include:
- Using trading volume indicators, the judgment of the main market forces is relatively reliable
- The algorithm is simple, easy to understand and implement
- Flexible configurable parameters and good adaptability
## Risk
Although the VR reversal strategy has certain advantages, there are also some risks that need to be noted:
- As a short-term strategy, there is a certain degree of randomness, and the income curve may be relatively ups and downs.
- The VR indicator may fail and the main force cannot be accurately judged.
- It is necessary to select varieties with appropriate parameters. If the fluctuations are gentle, the effect will not be good.
In addition, you also need to pay attention to preventing over-trading, setting stop losses to control single losses, etc.
## Optimization suggestions
There is room for further optimization of the VR reversal strategy. The main suggestions are as follows:
- Combine more indicators for judgment to avoid the failure of VR indicators
- Add stop loss logic, you can refer to the ATR indicator to set the stop loss range
- Optimize parameters, especially the Length cycle parameter, adjusted for different cycles and varieties
- Adjust the forward and reverse VR thresholds based on backtest results to ensure their robustness
## Summarize
VR reversal trading strategy is a short-term quantitative strategy that is simple, direct, and easy to implement. It seizes the reversal opportunity by capturing the signal of the main force. This strategy is particularly suitable for varieties with severe fluctuations and obvious reversals, but it also requires attention to risk control. Through further optimization, the strategy can be made more robust and more false signals can be filtered out.
||

## Overview

The Volume Ratio Reversal Trading Strategy (VR Reversal Strategy) is a short-term reversal trading strategy based on volume indicator. It judges the market participation of major players by calculating the ratio between volume and mean volume over a period of time to generate trading signals. This strategy is mainly suitable for short-term strongly mean-reverting assets.

## Strategy Logic

The core indicator of the VR reversal strategy is Volume Ratio (referred to as VR for short), which represents the ratio between the current period's trading volume and the average trading volume over a period of time. The specific calculation method is:

VR = Current Volume / SMA(Volume, N)

Where N stands for the parameter Length, the trading volume of the current cycle divided by the simple moving average of the trading volume over the Length cycle.  

When VR > threshold, it is considered as a signal of major players' participation. At this time, combined with the breakthrough of the price up or down, buy and sell signals are generated.

The strategy also introduces an auxiliary directional judgment indicator dir. It compares the closing price of the current cycle with that of N cycles ago. Greater than 1 is a bullish direction and less than 1 is a bearish direction.

When VR is greater than the specified threshold, if dir=1, a buy signal is generated. If dir=-1, a sell signal is generated.

## Advantages

The biggest advantage of VR reversal strategy is to capture the chance of sudden price reversal. When there is a signal of major players' intervention, the strategy can make judgments quickly and capture the opportunity of rebound or retracement in a timely manner. 

Other advantages include:

- Using volume indicator, the judgment on major players is relatively reliable  
- Simple algorithm, easy to understand and implement
- Flexible configurable parameters, better adaptability

## Risks

Although the VR reversal strategy has some advantages, there are still some risks to note:  

- As a short-term strategy, there is some randomness with fluctuating return curve  
- VR indicator may fail to accurately determine the major players
- Proper underlying products need to be selected. Less effective if fluctuation is mild

In addition, over trading should be avoided, stop loss should be set to control single loss, etc.

## Optimization Suggestions 

There is room for further optimization of the VR reversal strategy. The main suggestions are:

- Combine more indicators for judgment to avoid VR failure  
- Add stop loss logic, can refer to ATR indicator to set stop loss range
- Optimize parameters, especially the Length cycle parameter for different cycles and products
- Adjust the threshold of positive and negative VR based on backtest results to ensure robustness

## Conclusion

The VR reversal trading strategy is a simple, easy-to-implement short-term quantitative strategy. It captures reversal opportunities by catching major players' signals. The strategy is particularly suitable for volatile products with obvious reversal, but risk control is also needed. Further optimization can make the strategy more robust and filter out more false signals.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Length|
|v_input_2|3|Threshold value|
|v_input_3|true|direction picker # bars|
|v_input_4|2019|Start Year|
|v_input_5|true|Start Month|
|v_input_6|true|Start Day|
|v_input_7|9999|End Year|
|v_input_8|true|End Month|
|v_input_9|true|End Day|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

strategy(title="Volume Ratio_30min", shorttitle="VR_30min")//,initial_capital=1000)

// User Input ------------------------------------------------------------------
len = input(20, title="Length", minval=1)
threshold  = input(3,step=0.05, title="閾値")

// Volume Caliculetion ---------------------------------------------------------
vol = volume
sma=sma(volume,len)
vrs = vol / sma

// Direction -------------------------------------------------------------------
dirtime=input(1,"direction picker # bars")
dir=if close/close[dirtime] > 1
    1
else
    -1

// Plot ------------------------------------------------------------------------
plot(vrs, title="VRS",  color=color.green, transp=0)
hline(1, title="baseline")
plot(threshold, color=color.white)

// ️⚠️⚠️Logic　-----------------------------------------------------------------

long    = vrs > threshold  and dir == 1
short   = vrs > threshold  and dir ==-1

// Back Test Fnction -----------------------------------------------------------
start = timestamp(input(2019, "Start Year"), input(1, "Start Month"), input(1, "Start Day"), 0, 0)
end = timestamp(input(9999, "End Year"), input(1, "End Month"), input(1, "End Day"), 0, 0)
_testPeriod() => true

// Order -----------------------------------------------------------------------
if _testPeriod()
    if long
        strategy.entry("Long", strategy.long)
    if short
        strategy.entry("Short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/438469

> Last Modified

2024-01-12 12:08:05
