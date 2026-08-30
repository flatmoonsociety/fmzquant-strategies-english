
> Name

Turtle-trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/f33195e5d324f7d83e468cd2d97afe793b268a063b98f5e6c45c2f98a452e9e5.png)
[trans]

## Overview
The trend-following turtle trading strategy is a quantitative strategy that determines the direction of the trend based on moving averages and trades at trend reversal points. This strategy also combines K-line shape judgment signals to enter and stop losses at potential reversal points.
## Strategy Principle
This strategy uses three EMA average lines with different periods to determine the trend direction. Specifically, calculate the EMA averages of the 15-day line, the 120-day line, and the 220-day line respectively. When the 15-day line is higher than the 220-day line, it is judged to be a bullish trend, and when the 15-day line is lower than the 220-day line, it is judged to be a bearish trend.
During a bullish trend, if the closing price is below the 220-day line, go short; during a bearish trend, if the closing price is above the 220-day line, go long.
At the same time, the strategy will also combine the K-line pattern to confirm the signal. When a bullish large gap K-line or a bearish large gap K-line appears, close the position and stop the loss.
## Advantage Analysis
The biggest advantage of this strategy is that it can operate in line with the trend and avoid doing reverse operations at will without a clear signal. Judging trends through multiple moving averages can effectively filter market noise and lock in the main trend direction.
At the same time, the strategy will also enter the market at potential trend reversal points, which has a good risk-reward ratio. And combined with the K-line stop loss, the stop loss point can be avoided from being too fragmented.
## Risk Analysis
The main risk of this strategy is that the trend judged by the moving average may lag behind the actual price trend. At this time, a reverse operation with the trend may occur.
In addition, the K-line pattern rules used in the strategy may also be invalid and cannot effectively stop losses. When the market experiences abnormal fluctuations, the stop loss point may be directly breached, resulting in larger losses.
In order to reduce the above risks, you can consider adjusting the period parameters of the moving average, or adjusting the proportion factor of K-line shape determination to make the rules more stringent. Of course, you also need to realize that technical analysis can never completely avoid market risks, and you need to control your positions.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the period parameters of the moving average and find a combination of period parameters that is more suitable for judging the trend.
2. Test different types of moving average indicators, such as SMA, LWMA, etc., to find indicators that better suit your style.
3. Adjust or add K-line shape determination rules to make reversal signals clearer and more reliable.
4. Add stop loss strategies, such as trailing stop loss, time stop loss, etc., to further control single losses
5. Combine with other indicators, such as oscillators, trading volume, etc., to enrich the trading signals of the system
## Summarize
The trend-following turtle trading strategy is generally a very typical trend-following strategy. Its method of judging trends is simple and easy, and it also has certain risk control measures. This strategy is suitable for investors who have a certain understanding of trend trading and hope to obtain stable returns. If it can be continuously optimized, it can also become a quantitative strategy with long-term competitive advantages.
||


## Overview

The turtle-trend following strategy is a quantitative strategy that determines the trend direction based on moving averages and trades at trend reversal points. The strategy also combines candlestick patterns to determine signals and enter and stop loss at potential reversal points.

## Strategy Principle  

The strategy uses three EMA lines of different cycles to determine the trend direction. Specifically, the 15-day, 120-day, and 220-day EMA lines are calculated. When the 15-day line is higher than the 220-day line, the uptrend is determined. When the 15-day line is lower than the 220-day line, the downtrend is determined.

When in an uptrend, if the closing price is below the 220-day line, go short; when in a downtrend, if the closing price is above the 220-day line, go long.

At the same time, the strategy also combines candlestick patterns to confirm signals. When there is a bullish big gap candlestick or a bearish big gap candlestick, the position is closed to stop loss.

## Advantage Analysis

The biggest advantage of this strategy is that it can follow the trend to operate, avoiding reverse operations without clear signals. By judging the trend with multiple moving averages, market noise can be effectively filtered to lock the main trend direction.

At the same time, the strategy will also enter at potential trend reversal points, which has very good risk-reward characteristics at this time. And combining candlesticks to stop loss can avoid too fragmented stop loss points.

## Risk Analysis  

The main risk of this strategy is that the trend determined by the moving average may lag behind the actual price movement. At this time, reverse operations against the trend may occur.

In addition, the candlestick patterns used in the strategy may also fail and cannot stop loss effectively. When there is abnormal market fluctuation, the stop loss point may be directly penetrated, resulting in greater losses.

To reduce the above risks, consider adjusting the cycle parameters of the moving average, or adjusting the proportional factor for determining the candlestick pattern to make the rules stricter. Of course, it also needs to be aware that technical analysis can never completely avoid market risk, and position size needs to be controlled.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize the cycle parameters of the moving average to find a more suitable combination of parameters to judge the trend  

2. Test different types of moving average indicators, such as SMA, LWMA, etc., to find indicators that match your own style  

3. Adjust or add candlestick judgment rules to make reversal signals clearer and more reliable

4. Add stop loss strategies, such as trailing stop loss, time stop loss, etc., to further control single loss

5. Combine other indicators, such as volatility indicators, trading volume, etc., to enrich the trading signals of the system

## Summary  

The turtle-trend following strategy is a very typical trend following strategy overall. Its method of judging the trend is simple and easy to implement, while also having certain risk control measures. This strategy is suitable for investors who have some understanding of trend trading and hope to obtain stable returns. If continuously optimized, it can also become a quantitative strategy with long-term competitive advantages.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_3|50|Calculation period|
|v_input_bool_1|true|(?backtest range) enables backtest time range limitation|
|v_input_1|timestamp(1 Jan 2015)|Start time|
|v_input_2|timestamp(1 Jan 2040)|End time|
|v_input_int_1|15|(?market average cost) short-term market average cost|
|v_input_int_2|120|Medium-term market average cost|
|v_input_int_3|220|Long-term market average cost|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-14 00:00:00
end: 2023-12-21 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © Aayonga 
//@version=5
strategy('帆船探险寻找传说', overlay=true)

useDateFilter=input.bool(true,title = "启用回测时间范围限定", group = "回测范围")
backtesStarDate=input(timestamp("1 Jan 2015"),title = "开始时间", group = "回测范围")
backtestEndDate=input(timestamp("1 Jan 2040"),title = "结束时间",group = "回测范围")
inTradeWindow= true


A = input(50, '计算的周期')


shallowsea = ta.highest(A)
deepsea= ta.lowest(A)

//趋势形成条件
Length1 = input.int(15, title='短期市场平均成本', minval=1, group='市场平均成本')
Length2 = input.int(120, title='中期市场平均成本', minval=1, group='市场平均成本')
Length3 = input.int(220, title='长期市场平均成本', minval=1, group='市场平均成本')
SMA1 = ta.ema(close, Length1)
SMA2 = ta.sma(close, Length2)
SMA3 = ta.sma(close, Length3)


//趋势看多
longTrend=SMA1>SMA3 and open >SMA3 

shortTrend=SMA1<SMA3 

bullPinBar = ((close > open) and ((open - low) > 0.66* (high - low))) or ((close < open) and ((close - low) > 0.9 * (high - low)))
bearPinBar = ((close > open) and ((high - close) > 0.75 * (high - low))) or ((close < open) and ((high - open) >0.9 * (high - low)))



if close > shallowsea[5] and shortTrend and inTradeWindow
    strategy.entry('⛵?', strategy.short)

if close < deepsea[5] and longTrend and inTradeWindow
    strategy.entry('?', strategy.long)

if  bullPinBar and inTradeWindow
    strategy.close('⛵?',comment = '?')

if bearPinBar and inTradeWindow
    strategy.close('?',comment = '?')

plot(shallowsea,style=plot.style_area, color=color.new(#71bfef, 0))
plot(deepsea, style=plot.style_area,color=color.new(#298bd1, 0))



```

> Detail

https://www.fmz.com/strategy/436211

> Last Modified

2023-12-22 11:41:30
