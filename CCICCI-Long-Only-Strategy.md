
> Name

Long-term trading strategy CCI-Long-Only-Strategy based on CCI indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18f7b1a0954ba1563ec.png)
 [trans]

## Overview
This strategy is based on the CCI indicator and designs a long-term trading strategy that only goes long but does not go short. A buy signal is generated when the CCI indicator exceeds 100, and a sell signal is generated when the CCI indicator falls below -100. This strategy only allows closing positions and does not allow short selling, so it can effectively prevent the risk of short trading.
## Strategy Principle
The CCI indicator is a trend-type fluctuation indicator that determines whether the current price is overbought or oversold by measuring the deviation of the current price from the typical price within a certain period. When the CCI indicator exceeds 100, it indicates that it has entered the overbought area, and you can consider selling at this time; when the CCI indicator falls below -100, it indicates that it has entered the oversold area, and you can consider buying at this time.
The trading logic of this strategy is that when the CCI indicator crosses 100, a buy signal is generated, and a long position can be established at this time; when the CCI indicator subsequently breaks below -100, a sell signal is generated, and the previous long position is closed. In addition, the strategy prevents short positions and effectively controls risks by only allowing position closing.
## Strategic advantage analysis
- Use the CCI indicator to determine overbought and oversold areas, which is a relatively mature trading technique.
- Only long, not short, can effectively prevent the risk of short trading
- CCI parameters are adjustable and parameters can be optimized for different varieties
- The strategy logic is simple, easy to understand and easy to implement
## Strategy risk analysis
- The CCI indicator has the problem that different parameters have a greater impact on the results, and parameters need to be carefully optimized.
- When paying attention to the CCI indicator to make trading signals, you must consider more factors to avoid misjudgments.
- Only going long can easily miss short trading opportunities
- You need to pay attention to the impact of emergencies on prices to avoid being trapped
## Strategy optimization direction
- Optimize CCI parameters and select the best parameters for different varieties
- Combine more indicators to filter CCI signals to improve accuracy
- Add stop loss strategy and reduce single stop loss
- Added reopened signal to allow reopening of positions
- Allow short selling appropriately to increase the profit potential of the strategy
## Summarize
This strategy uses the CCI indicator to determine overbought and oversold areas, and only goes long but not short, which can effectively prevent short trading risks. The strategy concept is relatively mature, the logic is simple, and it is easy to implement. However, there are also certain risks, and you need to pay attention to issues such as parameter optimization, combining more indicators, and setting stop losses. Through continuous optimization and adjustment, this strategy can become a stable and reliable long-term trading strategy choice.
|| 


## Overview  

This strategy designs a long only trading strategy based on the CCI indicator. It generates buy signals when CCI is above 100 and closes long positions when CCI drops below -100. The strategy effectively prevents shorting by only allowing closing of long positions.

## Strategy Logic

The CCI indicator is a trending oscillator that measures the deviation of current price from the typical price over a period. CCI above 100 suggests overbought conditions while CCI below -100 suggests oversold conditions.

The trading logic is to go long when CCI crosses above 100 and close the long position when CCI subsequently drops below -100. Additionally, the strategy only allows position closing to prevent short positions, effectively controlling risks.

## Advantage Analysis  

- Utilizes mature CCI techniques to identify overbought/oversold areas
- Prevents short side risks by only going long  
- Customizable CCI parameters for optimization across products
- Simple logic easy to understand and implement

## Risk Analysis

- CCI results sensitive to different parameters
- Need to incorporate more factors when taking CCI signals to avoid false signals  
- Missing short side trading opportunities
- Vulnerable to price shocks from events

## Optimization Directions

- Optimize CCI parameters for different products
- Add filters with more indicators to improve accuracy 
- Incorporate stop loss strategy to limit losses
- Allow reopened signals for re-entry
- Allow measured short side trading to increase profits

## Summary

The strategy identifies overbought/oversold areas with CCI for long only trading. The concept is mature and easy to implement but has risks around parameter optimization, signal filters, stops etc. With continuous improvements, it can become a robust long term trading strategy choice.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|CCI Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-11 00:00:00
end: 2023-12-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("CCI Long Only Strategy", overlay=true)

// Input for CCI period
cciPeriod = input(14, title="CCI Period")

// Calculate CCI
cciValue = ta.cci(close, cciPeriod)

// Initialize variables to track last signals
var bool lastBuySignal = na
var bool lastSellSignal = na

// Buy condition
buyCondition = cciValue > 100 and na(lastBuySignal)

// Sell condition
sellCondition = cciValue < -100 and na(lastSellSignal)

// Update last signals
lastBuySignal := buyCondition ? true : na
lastSellSignal := sellCondition ? true : na

// Execute Buy and Sell orders
strategy.entry("Buy", strategy.long, when = buyCondition)
strategy.close("Buy", when = sellCondition)

// Plot CCI for reference
plot(cciValue, title="CCI", color=color.blue)
```

> Detail

https://www.fmz.com/strategy/435724

> Last Modified

2023-12-18 12:32:07
