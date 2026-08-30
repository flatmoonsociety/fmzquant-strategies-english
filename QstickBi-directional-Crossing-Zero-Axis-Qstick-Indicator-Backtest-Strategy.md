
> Name

Bi-directional-Crossing-Zero-Axis-Qstick-Indicator-Backtest-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2659be4faeefcf4f70238eb3546f67708d3831700522450f8036a0b0cdb17620.png)

[trans]

## Overview
The two-way cross zero-axis Qstick indicator backtesting strategy is a trend following and trading signal generation strategy based on the Qstick technical indicator developed by Tushar Chande. This strategy determines the market's buying and selling pressure by calculating the moving average difference between the stock's opening price and closing price, and generates trading signals when the difference indicator crosses the zero axis.
## Strategy Principle
The core indicator of the two-way crossing zero-axis Qstick strategy is Qstick. The Qstick indicator is obtained by calculating the moving average of the difference between the closing price and the opening price within a certain period. When Qstick is greater than 0, it means that the closing price in the period is generally higher than the opening price, and the bullish power is dominant; when Qstick is less than 0, it means that the opening price in the period is generally higher than the closing price, and the short force is dominant.
The trading signals for this strategy come from when the Qstick indicator crosses the zero line. When Qstick crosses the zero axis from below, a buy signal is generated, which means that the buying pressure begins to be higher than the selling pressure, and a long position can be established; on the contrary, when Qstick crosses the zero axis from above, a sell signal is generated, which means that the selling pressure begins to increase, and the selling position needs to be cleared. In addition, this strategy can also draw the moving average of the Qstick value as a signal line. When the Qstick indicator crosses the signal line, a trading signal will also be generated.
This strategy allows the option of reversal trades. That is, when a buy signal should have been generated, a selling operation was actually taken; when a sell signal was supposed to be generated, a buying operation was actually taken. This can be used to reverse mainstream investors who follow market ideology.
## Advantage Analysis
The two-way crossing zero-axis Qstick strategy has the following advantages:
1. Use simple and intuitive indicators to judge market buying and selling pressure, and generate clear signals
2. Using the moving average difference indicator can effectively filter out market noise
3. Signal lines can be drawn to avoid false signals
4. Supports reversal trading and can be used to track mainstream investors
5. Customizable parameters to adapt to different stocks and market environments
## Risk Analysis
The two-way crossing zero-axis Qstick strategy also has some risks:
1. The Qstick indicator delays identifying trend turning points and may miss the best entry point.
2. Frequent signals and high transaction costs
3. Reversal trading is risky and needs to be used with caution
Risks can be reduced by:
1. Optimize Qstick cycle parameters and reduce indicator latency
2. Increase signal line period parameters and reduce false signals
3. Only take reversal trades at specific stages and control the position size
## Optimization direction
The two-way crossing zero-axis Qstick strategy can be optimized from the following aspects:
1. Combine with other indicators to filter signals, such as trading volume indicators, volatility indicators, etc., to avoid generating false signals in non-trend environments
2. Add a stop-loss strategy to stop the loss when the loss reaches a certain proportion.
3. Further research to determine the best combination of Qstick and signal line period parameters
4. Automatically determine optimal parameters through machine learning methods
5. Test the strategy in specific industries or individual stocks
## Summarize
The two-way zero-axis crossing Qstick strategy uses simple indicators to judge changes in buying and selling pressure, and generates trading signals when the Qstick indicator crosses the zero-axis, which can effectively capture price trends. This strategy is intuitive and easy to understand, suitable for beginners, and can also be optimized through various means to meet the needs of advanced traders. However, this strategy also has certain flaws and needs to be used with caution. Overall, this is a very practical trend following and signal generation strategy.
||

## Overview  

The bi-directional crossing zero axis Qstick indicator backtest strategy is a trend tracking and signal generation strategy based on the Qstick technical indicator developed by Tushar Chande. This strategy calculates the moving average difference between the open and close prices of a stock to judge the buying and selling pressure in the market, and generates trading signals when this difference indicator crosses the zero axis.  

## Strategy Principle  

The core indicator of the bi-directional crossing zero axis Qstick strategy is Qstick. The Qstick indicator is obtained by calculating the moving average of the difference between closing price and opening price over a certain period. When Qstick is greater than 0, it means that the closing price was generally higher than the opening price during this period, and the bullish power prevailed; when Qstick is less than 0, it means that the opening price was generally higher than the closing price during this period, and the bearish power prevailed.

The trading signals of this strategy come from when the Qstick indicator crosses the zero axis. A buy signal is generated when Qstick crosses above zero from below, indicating that the buying pressure starts to exceed the selling pressure and a long position can be established; conversely, a sell signal is generated when Qstick crosses below zero from above, indicating that selling pressure starts to increase and existing positions should be closed out. In addition, a moving average of Qstick values can be plotted as a signal line, and trading signals can also be generated when the Qstick indicator crosses this signal line.  

This strategy allows for reversal trading. That is, when a buy signal is originally supposed to be generated, an actual sell operation is taken; when a sell signal is originally supposed to be generated, an actual buy operation is taken. This can be used to reverse follow mainstream investors in the market.

## Advantage Analysis   

The bi-directional crossing zero axis Qstick strategy has the following advantages:

1. Use simple and intuitive indicators to determine market buying and selling pressure, with clear signal generation  
2. Adopt moving average difference indicator, which can effectively filter out market noise
3. Signal lines can be drawn to avoid wrong signals  
4. Support reversal trading, which can be used to track mainstream investors
5. Customizable parameters suit different stocks and market environments   

## Risk Analysis

The bi-directional crossing zero axis Qstick strategy also has some risks:  

1. Qstick indicator has a lag in recognizing turning points, possibly missing the best entry point  
2. Frequent signals lead to relatively high transaction costs
3. Reversal trading has higher risks and needs to be used cautiously  

The following methods can be used to reduce risks:

1. Optimize the Qstick cycle parameters to reduce indicator delay  
2. Increase signal line cycle parameters to reduce wrong signals  
3. Only adopt reversal trading during specific stages, and control position sizing

## Optimization Directions   

The bi-directional crossing zero axis Qstick strategy can be optimized in the following aspects:

1. Incorporate other indicators to filter signals, such as volume indicators, volatility indicators, etc., to avoid generating wrong signals in non-trending environments  
2. Add stop loss strategies to stop loss when losses reach a certain percentage  
3. Further research to determine the optimal combination of Qstick and signal line cycle parameters  
4. Use machine learning methods to automatically determine optimal parameters
5. Test the efficacy of this strategy in specific industries or individual stocks  

## Conclusion  

The bi-directional crossing zero axis Qstick strategy utilizes simple indicators to determine changes in buying and selling pressure, and generates trading signals when the Qstick indicator crosses the zero axis, which can effectively capture price trends. This strategy is intuitive and easy to understand, suitable for beginners, and can also be optimized in many ways to meet the needs of advanced traders. However, this strategy also has certain flaws and needs to be used cautiously. In general, this is a very practical trend tracking and signal generation strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 16/04/2018
// A technical indicator developed by Tushar Chande to numerically identify 
// trends in candlestick charting. It is calculated by taking an 'n' period 
// moving average of the difference between the open and closing prices. A 
// Qstick value greater than zero means that the majority of the last 'n' days 
// have been up, indicating that buying pressure has been increasing. 
//
// Transaction signals come from when the Qstick indicator crosses through the 
// zero line. Crossing above zero is used as the entry signal because it is indicating 
// that buying pressure is increasing, while sell signals come from the indicator 
// crossing down through zero. In addition, an 'n' period moving average of the Qstick 
// values can be drawn to act as a signal line. Transaction signals are then generated 
// when the Qstick value crosses through the trigger line.
//
// You can change long to short in the Input Settings
// WARNING:
//  - For purpose educate only
//  - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Qstick Indicator Backtest")
Length = input(14, minval=1)
reverse = input(false, title="Trade reverse")
xR = close - open
xQstick = sma(xR, Length)
clr = iff(xQstick >= 0, green, red)
pos = iff(xQstick > 0, 1,
       iff(xQstick < 0, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
p1 = plot(0, color=black, title="0")
p2 = plot(xQstick, color=blue, title="Qstick")
fill(p1, p2, color=clr)
```

> Detail

https://www.fmz.com/strategy/439854

> Last Modified

2024-01-24 14:14:07
