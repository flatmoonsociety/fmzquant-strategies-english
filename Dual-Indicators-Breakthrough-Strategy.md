
> Name

Dual-Indicators-Breakthrough-Strategy Based on Dual-Indicators-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/84c1fa19835d64072f3acab2d08fe93cd9750e2ab4491ed06611b55755c70baa.png)
[trans]

## Overview
The dual indicator breakout strategy trades by combining the RSI indicator and the closing price indicator to buy low and sell high. This strategy is simple and practical, has low retracement risk, and is suitable for medium and long-term positions.
## Strategy Principle
This strategy is mainly judged based on the following two indicators:
1. RSI indicator: When RSI2 is less than 15, enter the market long.
2. Previous day's closing price: When today's closing price is higher than the previous day's highest price, close the position and exit.
The entry condition is that the RSI is overbought, indicating that the stock is highly undervalued and has a strong possibility of reversal. The exit condition is that the closing price exceeds the previous day's highest price, indicating that the stock is entering a long market and profit should be taken appropriately.
## Advantage Analysis
The dual indicator breakout strategy has the following advantages:
1. The strategy is simple to operate and easy to implement.
2. Based on dual indicators, false signals can be effectively controlled.
3. The RSI indicator parameters have a large space for optimization and can be adjusted to the best state.
4. Track the mid- to long-term trend with less risk of retracement.
5. It can be widely applied to large and mid-cap stocks and has good practical results.
## Risk Analysis
There are also some risks with this strategy:
1. Individual stocks fluctuate too much, and the RSI parameters need to be adjusted.
2. It is easy to expect a short-term correction in the bullish market.
3. The rationality of the previous day's highest price breakthrough needs to be evaluated.
The above risks can be avoided by optimizing RSI parameters, evaluating market types, and combining judgment with other indicators.
## Optimization direction
The optimization direction of this strategy mainly focuses on the following aspects:
1. Evaluate the effects of the RSI indicator in different periods.
2. Test closing price combinations with other price indicators.
3. Add a stop-loss mechanism, such as re-entering after a period of time after leaving the market.
4. Evaluate the reliability of entry signals based on changes in trading volume.
5. Use machine learning algorithms to automatically optimize parameters.
## Summarize
The dual indicator breakout strategy is overall a very practical quantitative strategy. This strategy is simple to operate and has low retracement risk. Through parameter optimization and rule improvement, it can become a smart and stable quantitative program. If implemented effectively, it can provide us with good medium and long-term trading opportunities.
||

## Overview

The dual indicators breakthrough strategy combines the RSI indicator and the closing price indicator to achieve low buying and high selling for trading. This strategy is simple and practical with low pullback risk and is suitable for medium and long term holds.  

## Strategy Principle  

The strategy is mainly based on the following two indicators for judgment:  

1. RSI indicator: go long when RSI2 is less than 15.  
2. Previous day's closing price: close the position when today's closing price is higher than yesterday's highest price.  

The entry condition is oversold RSI, indicating that the stock is highly undervalued and has a strong reversal potential. The exit condition is that the closing price breaks through the highest price of the previous day, indicating that the stock is entering a bullish trend and profits should be taken appropriately.  

## Advantage Analysis   

The dual indicator breakthrough strategy has the following advantages:  

1. The strategy operation is simple and easy to implement.  
2. False signals can be effectively controlled based on dual indicators.   
3. RSI indicator has large parameter optimization space for adjustment to optimal state.
4. Track medium and long term trends with low pullback risk.  
5. Widely applicable to large and medium caps with good practical results.   

## Risk Analysis   

The strategy also has some risks:  

1. Excessive fluctuations in individual stocks require RSI parameter adjustments. 
2. Expect short-term pullbacks in uptrends.  
3. Breakthrough amplitude of previous day's highest price needs evaluation of reasonableness.   

The above risks can be avoided through optimization of RSI parameters, evaluation of market conditions, and use of other indicators for judgment.   

## Optimization Directions   

The main optimization directions of this strategy are focused on the following aspects:  

1. Evaluate the effect of RSI indicators of different cycles. 
2. Test combinations of closing prices with other price indicators.  
3. Increase stop loss mechanisms, such as re-entry after a period of exit.  
4. Evaluate the reliability of entry signals in combination with trading volume changes.   
5. Automatically optimize parameters using machine learning algorithms.   

## Summary  

In general, the dual indicator breakthrough strategy is a very useful quantitative strategy. The strategy is simple to operate with low pullback risks. Through parameter optimization and rule refinement, it can become an intelligent and stable quantitative program. If implemented effectively, it can provide us with good medium and long term trading opportunities.  

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © hobbiecode

// If RSI(2) is less than 15, then enter at the close.
// Exit on close if today’s close is higher than yesterday’s high.

//@version=5
strategy("Hobbiecode - RSI + Close previous day", overlay=true)

// RSI parameters
rsi_period = 2
rsi_lower = 15

// Calculate RSI
rsi_val = ta.rsi(close, rsi_period)

// Check if RSI is lower than the defined threshold
if (rsi_val < rsi_lower)
    strategy.entry("Buy", strategy.long)

// Check if today's close is higher than yesterday's high
if (strategy.position_size > 0 and close > ta.highest(high[1], 1))
    strategy.close("Buy")

// Plot RSI on chart
plot(rsi_val, title="RSI", color=color.red)
hline(rsi_lower, title="Oversold Level", color=color.blue)


```

> Detail

https://www.fmz.com/strategy/439989

> Last Modified

2024-01-25 15:39:06
