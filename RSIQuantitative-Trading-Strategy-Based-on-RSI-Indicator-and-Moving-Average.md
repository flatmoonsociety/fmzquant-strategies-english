
> Name

Quantitative-Trading-Strategy-Based-on-RSI-Indicator-and-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/149f60210b0e0304f2b.png)
[trans]

## Overview
The name of this strategy is "Quantitative trading strategy of RSI indicator combined with moving average". This strategy uses RSI indicators and moving averages as trading signals to implement a quantitative trading strategy for reversal operations under the trend background. The core idea is to open a position when a reversal signal appears in the stock price and take profit when it is overbought or oversold.
## Strategy Principle
This strategy mainly uses the RSI indicator and fast and slow moving averages to determine stock price trends and reversal opportunities. Specifically, the strategy first calculates the fast moving average (SMA) and the slow moving average. When the fast moving average crosses the slow moving average, a buy signal is generated; when the fast moving average crosses below the slow moving average, a sell signal is generated. This is a sign of a shift in share price trends.
At the same time, this strategy calculates the RSI indicator to determine whether the stock price is overbought or oversold. Before opening a position, it will be judged whether the RSI indicator is normal. If the RSI exceeds the set threshold, the position will be suspended and wait for the RSI to fall back before opening a position. This avoids opening positions at unfavorable times when overbought or oversold conditions occur. On the other hand, when a position is already held, if the RSI exceeds the set take-profit threshold, the position will be closed and the take-profit will be taken. This locks in a profitable trade.
Through the cooperation of the RSI indicator and the moving average, you can open a position when the stock price generates a reversal signal, and take profits when it is overbought or oversold, thereby realizing a quantitative trading strategy that makes profits from reversal operations against the background of the stock price trend.
## Strategic Advantages
This strategy has the following advantages:
1. Positions can be opened accurately when the stock price reverses. By using the golden cross of the moving average as a buy signal and the dead cross as a sell signal, you can accurately seize the opportunity of stock price trend reversal.
2. It can avoid opening positions at unfavorable times. Using the RSI indicator to determine overbought and oversold conditions can effectively prevent the establishment of positions when the stock price fluctuates excessively in the short term and avoid unnecessary floating losses.
3. Risks can be well controlled. RSI stop profit can control the position within a reasonable profit range and effectively control transaction risks.
4. Easy parameter tuning. SMA cycles, RSI parameters, etc. can be flexibly adjusted to adapt to different market environments.
5. High capital utilization efficiency. Frequent trading can be carried out during the trend consolidation and shock phase to effectively utilize funds.
## Risk Analysis
This strategy also has the following risks:
1. Tracking error risk. As a trend judgment indicator, the moving average has a certain lag, which may lead to inaccurate position opening timing.
2. Frequent trading risks. In volatile market conditions, it may lead to opening and closing positions too frequently.
3. Risks of parameter tuning. The SMA cycle and RSI parameters require repeated testing and adjustment to adapt to the market. Improper settings may affect the performance of the strategy.
4. Take profit risk. Improper RSI take-profit setting may also cause the position to exit prematurely or continue to rise after taking profit.
## Optimization direction
The optimization direction of this strategy is as follows:
1. Try to use other indicators such as MACD and Bollinger Bands in combination with RSI to make the signal more accurate and reliable.
2. Add a machine learning algorithm so that parameters can be automatically adjusted based on historical data and reduce parameter tuning risks.
3. Add a profit-taking strategy optimization mechanism to make profit-taking more intelligent and adapt to market changes.
4. Optimize the position management strategy and reduce the risk of a single transaction by dynamically adjusting the position size.
5. Combined with high-frequency data, use tick-level real-time data for high-frequency trading to increase the frequency of strategies.
## Summarize
In general, this strategy uses RSI indicators and moving averages to generate trading signals, and implements a quantitative strategy that performs reversal operations during the trend. Compared with using the moving average alone, this strategy adds RSI indicator judgment to effectively prevent opening positions at unfavorable times, and controls trading risks through RSI take-profit, which improves the stability of the strategy to a certain extent. Of course, there is some room for improvement in this strategy. In the future, more indicator combinations, automatic parameter optimization, position management, etc. can be optimized to make the strategy perform even better.
||

## Overview

The strategy is named "Quantitative Trading Strategy Based on RSI Indicator and Moving Average". It utilizes RSI indicator and moving averages as trading signals to implement a quantitative trading strategy that makes reversal operations under trend background. Its core idea is to open positions when price reversal signals occur and take profit when overbought or oversold.

## Strategy Principle  

The strategy mainly uses RSI indicator and fast/slow moving averages to determine price trends and reversal timing. Specifically, it firstly calculates the fast moving average (SMA) and slow moving average. When the fast SMA crosses over the slow SMA, a buy signal is generated. When the fast SMA crosses below the slow SMA, a sell signal is generated. This indicates the trend of the price is changing.

At the same time, this strategy calculates the RSI indicator to determine whether the price is in an overbought or oversold state. Before opening positions, it will judge whether the RSI indicator is normal. If the RSI exceeds the set threshold, it will suspend opening positions and wait for the RSI to fall back before opening positions. This can avoid establishing positions at unfavorable overbought and oversold timing. On the other hand, after taking positions, if the RSI exceeds the set take profit threshold, it will close positions to take profits. This can lock trading gains.


By collaborating RSI indicator with moving averages, positions can be opened when price reversal signals occur. And by taking profit when overbought or oversold, a quantitative trading strategy that makes reversal operations for profits under price trend background can be implemented.  

## Advantages

The strategy has the following advantages:

1. Accurately open positions when price reversal occurs. Using moving average golden cross as buy signal and death cross as sell signal can accurately capture price trend reversal opportunities.

2. Avoid unfavorable opening positions timing. By judging overbought and oversold conditions through RSI indicator, it can effectively prevent establishing positions when price fluctuates excessively in the short term, avoiding unnecessary floating losses.

3. Risks can be well controlled. RSI take profit can keep positions within reasonable profit range and effectively control trading risks.

4. Easy to optimize parameters. SMA periods, RSI parameters etc. can be flexibly adjusted to adapt to different market environments.

5. High capital utilization efficiency. Frequent trading can be carried out during trend consolidation and shock stages, making efficient use of capital.

## Risk Analysis

The strategy also has the following risks:  

1. Tracking error risk. Moving averages as trend judgment indicators have certain lags, which may lead to inaccurate timing of opening positions.

2. Frequent trading risk. In oscillating markets, it may lead to excessively frequent openings and closings of positions.

3. Parameter tuning risk. SMA periods and RSI parameters need repeated testing and adjustment to adapt to markets. Improper settings may affect strategy performance.  

4. Take profit risk. Improper RSI take profit settings may also lead to premature exit of positions or continued rise after take profit exit.

## Optimization Directions

The optimization directions are as follows:

1. Try using MACD, Bollinger Bands and other indicators combined with RSI to make signals more accurate and reliable. 

2. Increase machine learning algorithms to automatically adjust parameters based on historical data, reducing parameter tuning risks.

3. Increase optimization mechanisms for take profit strategies to make take profit more intelligent and adaptable to market changes.

4. Optimize position management strategies by dynamically adjusting position sizes to reduce risks of single trades.

5. Combine high-frequency data and use tick-level real-time data for high-frequency trading to improve strategy frequency.   

## Conclusion  

In summary, this strategy uses trading signals generated by RSI indicator and moving averages to implement a quantitative strategy that makes reversal operations during trend runs. Compared to using moving averages alone, by adding RSI indicator judgments, this strategy can effectively prevent unfavorable opening positions timing and control trading risks through RSI take profit. To some extent, it improves the stability of the strategy. Of course, there are still room for improvements for this strategy. In the future, it can be optimized in aspects like more indicator combinations, automatic parameter optimization, position management, etc. to make strategy performance even better.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|11|fastLength|
|v_input_2|82|slowLength|
|v_input_3|14|Length|
|v_input_4|80|rsi exceeds the upper track and more profits are made|
|v_input_5|20|rsi exceeds the lower track and makes profit|
|v_input_6|75|Open long only when rsi is lower than this threshold|
|v_input_7|25|Open a short position only when rsi is higher than this threshold|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-17 00:00:00
end: 2023-12-18 19:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//1. 做多
//    a. RSI在超买区间时不开单，直到RSI回落一点再开单
//    b. 已经有多仓，如果RSI超买，则平多获利，当RSI回落一点之后，再次开多，直到有交叉信号反转做空

//2. 做空
//    a. RSI在超卖区间时不开单，直到RSI回落一点之后再开多单
//    b. 已经有空仓，如果RSI超卖，则平空获利，当RSI回落一点之后，再开空单，直到有交叉信号反转做多

//@version=4
strategy("策略_RSI+移动揉搓线_", overlay=true)

// 输入
fastLength = input(11, minval=1)
slowLength = input(82,minval=1)
length = input(title="长度", type=input.integer, defval=14, minval=1, maxval=100)
hight_rsi = input(title="rsi超过上轨平多获利", type=input.integer, defval=80, minval=1, maxval=100)
low_rsi = input(title="rsi超过下轨平空获利", type=input.integer, defval=20, minval=1, maxval=100)

open_long_rsi_threshold = input(title="rsi低于该阈值时才开多", type=input.integer, defval=75, minval=1, maxval=100)
open_short_rsi_threshold = input(title="rsi高于该阈值时才开空仓", type=input.integer, defval=25, minval=1, maxval=100)

// 均线
sma_fast = sma(close, fastLength)
sma_slow = sma(close, slowLength)
// RSI
rsi = rsi(close, length)

//**********变量*start*******//
var long_f = false // 标记是否是均线交叉多头
var short_f = false // 标记是否是均线交叉空头
var long_open_pending = false // 标记开仓时rsi是否处于超买状态
var short_open_pending = false // 标记开仓时rsi是否处于超卖
var long_rsi_over_buy = false // 标记 多仓时 是否发生超买平多获利
var short_rsi_over_sell = false // 标记 空仓时 是否发生超卖平空获利

//**********逻辑*start*******//

// 买入
longCondition = crossover(sma_fast, sma_slow)
if (longCondition)
    short_rsi_over_sell := false // 清空该标记，防止再次开空仓
    long_f := true
	short_f := false
	if (rsi < hight_rsi)
	    // 并且没有超买
	    strategy.entry("多", long=strategy.long)
    if (rsi > hight_rsi)
        // 开仓时发生超买，等待rsi小于hight_rsi
	    long_open_pending := true

// 卖出
shortCondition = crossunder(sma_fast, sma_slow)
if (shortCondition)
    long_rsi_over_buy := false //清空该标记，防止再次开多仓
    long_f := false
    short_f := true
    if (rsi > low_rsi)
        strategy.entry("空", long=strategy.short)
	if (rsi < low_rsi)
	    // 开仓时发生超卖，等待rsi大于low_rsi
	    short_open_pending := true
	    

// 等待RSI合理，买入开仓
if (long_f and long_open_pending and strategy.position_size == 0 and rsi < open_long_rsi_threshold)
    strategy.entry("多", long=strategy.long)
	long_open_pending := false
// 等待RSI合理，卖出开仓
if (short_f and short_open_pending and strategy.position_size == 0 and rsi > open_short_rsi_threshold)
    strategy.entry("空", long=strategy.short)
	short_open_pending := false


	
//RSI止盈(RSI超买平多)
if (strategy.position_size > 0 and long_f and rsi > hight_rsi)
	strategy.close_all()
	long_rsi_over_buy := true
//RSI止盈(RSI超卖平空)
if (strategy.position_size < 0 and short_f and rsi < low_rsi)
	strategy.close_all()
	short_rsi_over_sell := true
	
	
//RSI止盈之后，再次开多
if (long_f and long_rsi_over_buy and strategy.position_size == 0 and rsi < hight_rsi)
    long_rsi_over_buy := false
    strategy.entry("多", long=strategy.long)
//RSI止盈之后，再次开空
if (short_f and short_rsi_over_sell and strategy.position_size == 0 and rsi > low_rsi)
    short_rsi_over_sell := false
    strategy.entry("空", long=strategy.short)


//**********绘图*start*******//

p1 = plot(sma_fast, linewidth=2, color=color.green)
p2 = plot(sma_slow, linewidth=2, color=color.red)
fill(p1, p2, color=color.green)
plot(cross(sma_fast, sma_slow) ? sma_fast : na, style = plot.style_circles, linewidth = 4)

// 绘制rsi线
//plot(rsi, color=color.green, editable=true, style=plot.style_circles, linewidth=2)

// 绘制上下轨
//high_ = hline(80, title="上轨")
//low_ = hline(20, title="下轨")
//fill(high_, low_, transp=80, editable=true, title="背景")
    
    
    
    
    
    
    
```

> Detail

https://www.fmz.com/strategy/436485

> Last Modified

2023-12-25 11:40:36
