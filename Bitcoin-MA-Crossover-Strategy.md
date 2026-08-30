
> Name

Bitcoin-Moving Average Crossover Strategy-Bitcoin-MA-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1a5f8bfffa2b339bb85.png)
[trans]


## Overview
This strategy is a trend following trading strategy designed based on Bitcoin’s moving average crossover principle. The strategy uses the crossover of the fast and slow moving averages as buy and sell signals. When the fast moving average crosses the slow moving average, it is regarded as a golden cross and goes long; when the fast moving average crosses below the slow moving average, it is regarded as a dead cross and goes short. At the same time, the strategy also combines the RSI indicator to avoid reckless entry.
## Strategy Principle
This strategy is mainly based on two indicators:
1. Moving Average (MA): Calculates the average closing price within a certain period and is used to determine price trends and signals of turning points.
2. Relative Strength Index (RSI): Calculate the rise and fall speed of stock prices within a certain period and determine the overbought and oversold areas.
Specifically, the strategy uses shorter MAs as fast lines and longer MAs as slow lines. When the fast line crosses the slow line, it means that the short-term price rise is accelerating, generating a buy signal; when the fast line crosses the slow line, it means that the short-term price decline is accelerating, generating a sell signal.
At the same time, the strategy also sets the RSI threshold, which only generates a buy signal when the RSI is higher than 50, and a sell signal when the RSI is lower than 50, to avoid reckless entry when the price fluctuates violently.
## Strategic Advantages
This strategy has the following advantages:
1. The principle is simple, easy to understand and implement.
2. Reliable trading signals avoid irrational entry.
3. Few parameters and easy to optimize.
4. Moving average technology is mature and widely used.
5. The RSI indicator can effectively indentify overbought and oversold phenomena.
## Risk Analysis
There are also some risks with this strategy:
1. Following the trend strategy can easily cause large losses when the price reverses.
2. The moving average lags behind and cannot capture price turns in time.
3. Wrong parameter selection can lead to a decrease in the quality of trading signals.
4. The strategy is only based on technical indicators and does not take into account fundamental factors.
In order to reduce risks, it is recommended to optimize the moving average cycle parameters, adjust the stop loss position, and appropriately reduce the position size. This strategy should be suspended when fundamentals change significantly.
## Optimization direction
This strategy has the following main optimization directions:
1. Optimize the moving average period parameters and find the best parameter combination. It can be optimized through stepwise search, genetic algorithm and other methods.
2. Add other technical indicator filters, such as KDJ, MACD, etc., to improve the quality of trading signals.
3. Increase monitoring of price fluctuations and adjust positions and stop losses based on volatility.
4. Combine trading volume to avoid false breakthroughs. Only send signals when volume increases.
5. Develop parameter adaptation mechanism. Allows the strategy to automatically adjust parameter values ​​according to different market environments.
## Summarize
Generally speaking, this strategy is a more typical trend following strategy. Based on the moving average crossover principle, the trading logic is simple and clear, easy to understand and implement. At the same time, incorporating the RSI indicator can avoid irrational trading. This strategy can be said to have both risks and returns, and is suitable for investors with certain quantitative trading experience, but they need to pay attention to guarding against potential loss risks. If developers can add more filtering conditions and optimize parameter adaptability, the stable profitability of the strategy can be further improved.
||

## Overview

This strategy is a trend following trading strategy designed based on the crossover principle of Bitcoin's moving average lines. The strategy uses the crossover of the fast moving average line and the slow moving average line as the buy and sell signals. When the fast moving average line crosses above the slow moving average line, it is considered a golden cross and goes long; when the fast moving average line crosses below the slow moving average line, it is considered a death cross and goes short. At the same time, the strategy also incorporates the RSI indicator to avoid reckless entry.

## Strategy Principle 

The strategy is mainly based on two indicators:

1. Moving Average (MA): Calculates the average closing price over a certain period to determine price trends and reversal signals.

2. Relative Strength Index (RSI): Calculates the speed of price rises and falls over a certain period to judge overbought and oversold areas.

Specifically, the strategy uses a shorter MA as the fast line and a longer MA as the slow line. When the fast line crosses above the slow line, it indicates that the short-term price rise is accelerating and a buy signal is generated; when the fast line crosses below the slow line, it indicates that the short-term price decline is accelerating and a sell signal is generated.

At the same time, the strategy also sets a threshold for RSI, generating buy signals only when the RSI is above 50 and sell signals only when the RSI is below 50, avoiding reckless entry when prices fluctuate violently.

## Advantage Analysis

The strategy has the following advantages:

1. The principle is simple and easy to understand and implement.
2. Reliable trading signals avoid irrational entry.  
3. Fewer parameters and easy to optimize.
4. Mature moving average technique with wide application.
5. RSI indicator can effectively identify overbought and oversold phenomena.

## Risk Analysis

The strategy also has some risks:  

1. Trend following strategies are prone to large losses when prices reverse.
2. Moving averages lag and fail to promptly capture price reversals.  
3. Incorrect parameter selection can lead to deteriorated trading signal quality.
4. The strategy only considers technical indicators without fundamental factors.

To mitigate risks, it is recommended to optimize the moving average period parameters, adjust stop loss positions, and appropriately scale down position sizes. The strategy should be suspended when major fundamental changes occur.

## Optimization Directions

The main optimization directions for this strategy include:

1. Optimize the moving average period parameters to find the optimal parameter combination, through incremental search, genetic algorithms, etc.

2. Increase other technical indicators for filtration, such as KDJ, MACD, etc. to improve trading signal quality.  

3. Monitor price fluctuations and adjust positions and stop losses accordingly.

4. Incorporate trading volume to avoid false breakouts, only issuing signals when trading volume expands.

5. Develop parameter self-adaptive mechanisms, allowing strategies to automatically adjust parameter values based on different market environments.

## Conclusion

In summary, this is a typical trend-following strategy. Based on the principle of moving average crossover, the trading logic is simple and clear, easy to understand and implement. Incorporating the RSI indicator can avoid irrational trading. The strategy carries both risks and rewards, suitable for investors with some quant trading experience, but the potential loss risks need to be guarded against. If developers can add more filters, optimize parameter adaptivity, it can further improve the steady profitability of the strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Equity Risk (%)|
|v_input_2|20|Fast MA (Period)|
|v_input_3|40|Slow MA (Period)|
|v_input_4|14|RSI (Period)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-03 00:00:00
end: 2023-12-03 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//Trading Strategy Warning - Past performance may not equal future performance
//Account Size Warning - Performance based upon default 10% risk per trade, of account size $100,000. Adjust before you trade to see your own drawdown.
//Time Frame - D1 and H4, warning H4 has a lower profit factor (fake-outs, and account drawdown), D1 recommended
//Trend Following System - Profitability of this system is dependent on a STRONG trend in Bitcoin, into the future
strategy("Bitcoin - MA Crossover Strategy", overlay=true)

// User Input
usr_risk = input(title="Equity Risk (%)",type=input.integer,minval=1,maxval=100,step=1,defval=10,confirm=false)
sma_fast = input(title="Fast MA (Period)",type=input.integer,minval=1,maxval=500,step=1,defval=20,confirm=false)
sma_slow = input(title="Slow MA (Period)",type=input.integer,minval=1,maxval=500,step=1,defval=40,confirm=false)
rsi_valu = input(title="RSI (Period)",type=input.integer,minval=1,maxval=500,step=1,defval=14,confirm=false)

// Create Indicator's
shortSMA = sma(close, sma_fast)
longSMA = sma(close, sma_slow)
rsi = rsi(close, rsi_valu)
strategy.initial_capital = 50000
// Units to buy
amount = usr_risk / 100 * (strategy.initial_capital + strategy.netprofit)
units = floor(amount / close)

// Specify entry conditions
longEntry = crossover(shortSMA, longSMA)
shortEntry = crossunder(shortSMA, longSMA)

// Specify exit conditions
longExit = crossunder(shortSMA, longSMA)
shortExit = crossover(shortSMA, longSMA)

// Execute long trade
if (longEntry)
    strategy.entry("long", strategy.long, units, when = rsi > 50)

// Exit long trade
if(longExit and strategy.position_size > 0)    
    strategy.order("exit long", strategy.short, abs(strategy.position_size))

// Execute short trade
if (shortEntry)
    strategy.entry("short", strategy.short, units, when = rsi < 50)
    
// Exit short trade
if(shortExit and strategy.position_size < 0)    
    strategy.order("exit short", strategy.long, abs(strategy.position_size))

// Plot Moving Average's to chart
plot(shortSMA)
plot(longSMA, color=color.black)
```

> Detail

https://www.fmz.com/strategy/434167

> Last Modified

2023-12-04 13:55:45
