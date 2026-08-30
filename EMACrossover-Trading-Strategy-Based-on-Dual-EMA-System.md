
> Name

Crossover-Trading-Strategy-Based-on-Dual-EMA-System
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy calculates two EMA indicators, one fast and one slow, and generates buy and sell signals based on their intersections. It is a typical trend following strategy. When the fast line crosses the slow line, go long, and when it crosses below, it will close the long position; when the fast line crosses below the slow line, it will go short, and when it crosses above, it will close the short position.
### Strategy Principles
The strategy calculates two EMA moving averages, one fast and one slow, with periods of 13 and 50 respectively. When the fast line breaks through the slow line from bottom to top, a buy signal is generated to go long; when the fast line breaks through the slow line from top to bottom, a sell signal is generated to go short.
After going long, if the fast line falls below the slow line again, a signal to close the long position will be generated; after going short, if the fast line breaks below the slow line again, a signal to close the short position will be generated.
### Advantage Analysis
This strategy uses the common double EMA system to determine the market trend and entry point based on the intersection of EMAs of different periods. The combined use of double EMA can effectively filter noise and identify trends.
The operation is simple and intuitive, and it is easy to realize automation. And it can be achieved only based on price information, without considering other complex factors. The EMA cycle can be freely adjusted to adapt to different market environments.
### Risk Analysis
The double EMA crossover system has a general effect on identifying zigzag trends. In a volatile market, EMA cross signals are frequent and it is easy to get stuck. Only the price factor is considered, without taking other factors into consideration comprehensively.
The EMA period interval can be appropriately expanded to reduce the crossover frequency. Indicators such as trading volume or volatility can also be added to assist judgment. In addition, optimizing the stop loss strategy can also reduce the risk of being trapped.
### Optimization direction
1. Test and optimize the EMA cycle parameters and find the optimal parameters.
2. Add judgment rules such as volume energy indicators or volatility indicators.
3. Combine with breakthrough signals, etc., to set stricter entry conditions.
4. Apply machine learning to predict price trends and assist EMA in determining signal quality.
5. Optimize stop loss strategies, such as trailing stop loss, average stop loss, etc.
6. Dynamically adjust positions and optimize fund management.
### Summarize
This strategy is a typical double EMA crossover system, which determines the trend through a simple combination of indicators. The advantage is that it is easy to implement, but it is also easy to produce false signals. Combining more indicators and parameter optimization can improve the stability of the strategy. Overall, it provides a concise trend following strategy template.
||

### Overview

This strategy computes one fast and one slow EMA indicators, generating buy and sell signals based on their crossover situation, belonging to a typical trend following strategy. It goes long when the fast line crosses above the slow line, and flattens longs when the fast line crosses below the slow line. Conversely, it goes short when the fast line crosses below the slow line, and flattens shorts when the fast line crosses above the slow line.

### Strategy Logic 

The strategy computes one fast and one slow EMA lines, with periods of 13 and 50 respectively. When the fast line breaks out upwards crossing the slow line, a buy signal is generated to go long. When the fast line breaks downwards crossing below the slow line, a sell signal is generated to go short.

After going long, if the fast line recrosses below the slow line, a flatten long signal is generated. After going short, if the fast line recrosses above the slow line, a flatten short signal is generated.

### Advantage Analysis

The strategy adopts the common dual EMA system, judging trend and entry points based on crossover situations between different timeframe EMAs. The dual EMAs can effectively filter noise and identify trends when used together.

The operations are simple and intuitive, easy to automate. It only needs price information, without considering other complex factors. The EMA periods can be freely adjusted to adapt to different market environments.

### Risk Analysis

The dual EMA crossover system has mediocre performance in identifying intricate trends. In ranging markets, EMA crossover signals may be frequent, risking whipsaws. Only price factors are considered without incorporating other elements.

Increasing the interval between the EMA periods could reduce crossover frequency. Volume or volatility indicators could also help provide additional insight. Optimizing stop loss strategies may also lower whipsaw risks.

### Optimization Directions

1. Test and optimize EMA period parameters to find the optimal settings.

2. Add volume, volatility or other judgement rules. 

3. Incorporate breakout signals etc to set more stringent entry conditions.

4. Apply machine learning to predict trends and aid EMA signal quality determination.

5. Optimize stop loss strategies such as trailing stops, average stops etc.

6. Dynamically adjust position sizing to optimize capital management.

### Summary

The strategy belongs to the typical dual EMA crossover system, gauging trends by simple indicator combinations. It is easy to implement but also prone to false signals. Combining more indicators and parameter optimization can improve robustness. Overall it provides a concise trend following strategy template.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|13|LSEMA|
|v_input_2|50|LLEMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-12 00:00:00
end: 2023-09-12 22:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © himanshumahalle

//@version=4
strategy("CROSS_ALGO SYSTEM")


// INPUT CONTROLS

lengthSEMA= input(title="LSEMA", type = input.integer, defval=13,minval=1,maxval=100,step=1)
lengthLEMA= input(title="LLEMA", type = input.integer, defval=50,minval=1,maxval=100,step=1)

//INDICATOR

SEMA= ema(close,lengthSEMA)
LEMA= ema(close,lengthLEMA)

// BUY AND SELL

buy = crossover(SEMA,LEMA)
sell = crossunder(SEMA,LEMA)

//EXITS

buyexit = crossunder(SEMA,LEMA)
sellexit = crossover(SEMA,LEMA)


//EXECUTION

strategy.entry("long",strategy.long,when=buy,comment = "Buy")
strategy.entry("short",strategy.short,when=sell,comment = "Sell")

strategy.close("long",when= buyexit , comment= "Sell")
strategy.close("short",when= sellexit , comment= "Buy")



```

> Detail

https://www.fmz.com/strategy/427348

> Last Modified

2023-09-20 11:39:40
