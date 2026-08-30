
> Name

Trading-Strategy-Based-on-MACD-and-RSI-Crossover-Signals
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ee7f751190112e14fe4f2c07570b05bf76a223197e4d5cff9bb112a49d17505b.png)

[trans]

## Overview
This strategy uses the MACD indicator to determine market trends and find potential buying and selling points, and combines it with the RSI indicator to confirm overbought and oversold phenomena. When the MACD indicator sends out a buy/sell signal, only when the RSI also confirms that the market is in an oversold/overbought state will a trading signal be generated for buying or selling. This strategy can effectively filter false signals and improve the stability of the strategy.
## Strategy Principle
### MACD indicator calculation
The MACD indicator is composed of the difference between the fast moving average (EMA) and the slow moving average, reflecting the difference in short-term and long-term average price movement trends. In this strategy, the period of the fast line is 12 days and the period of the slow line is 26 days.
When the fast line crosses the slow line, it is a golden cross signal, indicating that the market has entered an upward trend; when the fast line crosses the slow line, it is a dead cross signal, indicating that the market has entered a downward trend.
### RSI indicator calculation
The RSI indicator reflects overbought and oversold conditions in the market. In this strategy, the parameter period of RSI is set to 14.
RSI BELOW 30 when buyers outpaced sellers for an extended period suggests ASSET was OVERSOLD. 

RSI ABOVE 70 when selling pressure outpaced buying pressure over the tracked timeline suggests ASSET was OVERBOUGHT.

When the RSI is below 30, it means the market is oversold; when the RSI is above 70, it means the market is overbought.
### Strategy signals
When relying solely on the MACD indicator to generate trading signals, certain false signals will appear. This strategy uses the RSI indicator to filter signals. Only when MACD sends a signal and RSI also confirms that the market is overbought and oversold, will an actual trading signal be generated.
Specifically, when MACD forms a golden cross signal, if RSI <= 34, it is confirmed that the market is oversold, and a buy signal is generated; when MACD forms a dead cross signal, if RSI >= 75, it is confirmed that the market is overbought, and a sell signal is generated.
This double confirmation mechanism can filter out many unreliable trading signals, thereby improving the stability and reliability of the strategy.
## Advantage Analysis
### Dual indicator filtering to improve signal reliability
This strategy uses two indicators, MACD and RSI, to perform double confirmation. This can effectively reduce the interference of false signals and filter out some unreliable trading signals, thereby improving the reliability and stability of the signals.
### Clear trend judgment
As a volume and price indicator, MACD can clearly judge the rising and falling trends of the market. Combined with the overbought and oversold judgment of the RSI indicator, we can accurately grasp the important reversal points of the market and provide clear signals for entering and exiting positions.
### There is a lot of room for parameter optimization
The parameters of MACD and RSI of this strategy can be optimized and adjusted to adapt to different cycles and varieties, and the optimization space is large. Through parameter adjustment, we can tailor measures to local conditions and obtain better strategic effects.
### Easy to understand and implement
The indicators such as MACD and RSI used by this strategy are very typical and commonly used technical indicators, which are easy to understand, and the code implementation is also very simple and intuitive. This brings convenience to parameter adjustment and optimization.
## Risk Analysis
### You may miss some trading opportunities
This strategy uses a more cautious double confirmation strategy. In order to filter out false signals, you may miss some trading opportunities that can make profits under a single indicator condition.
* Solution: Appropriately relax the threshold range of RSI, reduce the strictness of confirmation, and allow the strategy to obtain more trading opportunities.
### Loss occurs when the market changes drastically
When the market changes drastically, both MACD and RSI indicators may delay judgment, causing the strategy to generate wrong trading signals and cause losses.
* Solution: Add a stop-loss mechanism to avoid excessive single losses; adjust parameters to make the indicator sensitive to drastic changes.
### The effect is highly related to the quality of parameter settings
The effect of this strategy depends largely on the settings of parameters such as MACD and RSI. If the parameters are set improperly, it is easy to obtain reverse trading signals.
* Solution: Optimize the parameter combination through backtesting to find the best parameter settings.
## Optimization direction
### Add a stop-loss mechanism to manage risks
You can set price stop loss or indicator stop loss rules to stop loss and exit when the loss expands to a certain extent, effectively controlling single losses.
### Adjust parameters to adapt to market characteristics
You can optimize parameter settings by adjusting MACD's fast and slow line cycles, RSI's overbought and oversold thresholds and other parameters to make them more suitable for the market characteristics of different cycles and varieties.
### Test different varieties to find the best fit
You can conduct backtests on different varieties such as stock indexes, digital currencies, foreign exchange, commodities, etc. to find the varieties with the best strategy effects.
### Add other indicators for multi-dimensional confirmation
On the basis of the existing MACD and RSI, other indicators such as stoch, OBV, and CCI can be introduced to achieve multi-indicator confirmation and further improve signal quality.
## Summarize
This strategy is based on the MACD indicator to determine the market trend direction and trading signals. In order to filter out false signals, the RSI indicator is added to confirm the phenomenon of overbought and oversold. Only when both conditions are met at the same time will a trading signal be generated. This dual indicator confirmation mechanism can effectively improve the quality and stability of signals.
Through parameter optimization, application of stop-loss mechanisms, multi-indicator confirmation and other improvements, the effect of the strategy can be further improved. This strategy is simple to operate and has good stability. It is a quantitative trading strategy suitable for beginners to practice and optimize.
|| 

## Overview

This strategy uses the MACD indicator to judge market trends and identify potential trading points, while combining the RSI indicator to confirm overbought/oversold conditions. Trading signals are only generated when the MACD gives a buy/sell signal and the RSI simultaneously confirms that the market is oversold/overbought. This can effectively filter out false signals and improve the stability of the strategy.

## Strategy Principles 

### MACD Indicator Calculation

The MACD indicator consists of the difference between fast EMA and slow EMA, reflecting the difference between short-term and long-term average price trends. In this strategy, the fast line period is 12 days and the slow line period is 26 days.

When the fast line crosses above the slow line, it is a golden cross signal indicating an uptrend. When the fast line crosses below the slow line, it is a death cross signal indicating a downtrend.

### RSI Indicator Calculation

The RSI indicator reflects the overbought/oversold conditions in the market. The RSI period parameter is set to 14 in this strategy. 

RSI BELOW 30 suggests the ASSET was OVERSOLD as buyers outpaced sellers for an extended period.

RSI ABOVE 70 suggests the ASSET was OVERBOUGHT as selling pressure outpaced buying pressure over the tracked timeline.

Readings below 30 indicate oversold conditions while readings above 70 indicate overbought conditions.

### Strategy Signals 

Relying solely on the MACD for trade signals can result in some false signals. This strategy uses the RSI to filter signals, only generating actual trading signals when the MACD gives a signal and the RSI simultaneously confirms overbought/oversold extremes.

Specifically, when the MACD generates a golden cross, if RSI<=34 at the same time, confirming an oversold market, a buy signal is generated. When the MACD forms a death cross, if RSI>=75, confirming an overbought market, a sell signal is generated.

This dual confirmation mechanism can filter out many unreliable trading signals, thereby improving the stability and reliability of the strategy.

## Advantage Analysis

### Dual Indicator Filtering Enhances Signal Reliability 

This strategy combines the MACD and RSI indicators for dual confirmation, which can effectively reduce interference from false signals and filter out some unreliable trade signals, thereby improving signal reliability and stability.

### Clear Trend Judgement

As a price & volume indicator, the MACD can clearly determine market uptrends and downtrends. Combined with the RSI's overbought/oversold judgement, it can accurately capture important reversal points in the market. Entry and exit signals are clear.

### Large Parameter Optimization Space

The parameters of this strategy's MACD and RSI components can be optimized and adjusted to suit different cycles and trading instruments. There is ample optimization room through parameter tuning for improved strategy performance in different markets.

### Easy to Understand and Implement

The MACD, RSI and other indicators used in this strategy are very typical and commonly used technical indicators that are easy to understand. The strategy code is also very simple and intuitive, which brings convenience for parameter adjustment and optimization.

## Risk Analysis

### May Miss Some Trading Opportunities 

This strategy adopts a relatively conservative dual confirmation approach which, in filtering out false signals, may cause some missed trading opportunities that could have resulted in profits based on a single indicator signal.

* Solution: Appropriately expand the RSI threshold range to reduce the confirmation strictness and allow the strategy to capture more trading opportunities.

### Loss Occurrence During Extreme Market Moves

In the event of extreme market volatility, both the MACD and RSI indicators may lag in making judgements, leading to incorrect trade signals generated by the strategy and losses incurred.

* Solution: Incorporate stop loss mechanisms to prevent excessive losses in single trades. Adjust parameters to build adequate sensitivity of the indicators to extreme market moves.

### Performance Depends Heavily on Parameter Settings

The performance of this strategy depends largely on the quality of the MACD, RSI and other parameter settings. Incorrect parameter configuration can easily lead to reversed trade signals. 

* Solution: Optimize parameter combinations through backtesting to locate optimal parameter settings.

## Optimization Directions

### Incorporate Stop Loss Mechanisms To Control Risks

Price or indicator based stop loss rules can be implemented to exit positions with a pre-defined allowable loss threshold, effectively capping losses on individual trades.

### Adjust Parameters To Suit Market Characteristics 

Continuous optimization of key parameters like MACD fast/slow line periods and RSI overbought/oversold thresholds to align with evolving cycle structures and peculiarities of different trading instruments.

### Test Across Assets To Discover Best Fit

Perform backtests across equity indices, cryptocurrencies, forex pairs, commodities and other assets to discover which market best suits the characteristics of the strategy.

### Incorporate Additional Indicators For Multidimensional Confirmation

Indicators like Stochastics, OBV, CCI etc. can be added on top of the MACD and RSI components for greater confirmation precision via a multidimensional signal filtering approach.

## Conclusion

This strategy determines market trends and trade signals based on the MACD indicator, while the RSI confirms overbought/oversold conditions to filter false signals. This dual confirmation mechanism can effectively improve signal quality and stability. 

Performance can be further enhanced through optimization techniques, stop losses, multiprong confirmation etc. With simple logic and good stability, it serves as a good starting strategy for novice quants to practice and optimize.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|Fast moving average|
|v_input_2|26|Slow moving average|
|v_input_3|9|signalLength|
|v_input_4|34|RSIOverSold|
|v_input_5|75|RSIOverBought|
|v_input_6|14|Length|
|v_input_7|8|Start Date|
|v_input_8|3|Start Month|
|v_input_9|2021|Start Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-17 00:00:00
end: 2023-12-17 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(default_qty_type = strategy.percent_of_equity, default_qty_value = 25, pyramiding = 10, title="MACD crossover while RSI Oversold/Overbought", overlay=true, shorttitle="MACD Cross + RSI Oversold Overbought", initial_capital = 1000)

//MACD Settings
fastMA = input(title="Fast moving average",  defval = 12, minval = 7) //7 16
slowMA = input(title="Slow moving average",  defval = 26, minval = 7) //24 26 
signalLength = input(9,minval=1) //9 6

//RSI settings
RSIOverSold = input(34 ,minval=1) //26
RSIOverBought = input(75 ,minval=1) //77
src = close, len = input(14, minval=1, title="Length")
up = rma(max(change(src), 0), len)
down = rma(-min(change(src), 0), len)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
wasOversold = rsi[0] <= RSIOverSold or rsi[1] <= RSIOverSold or rsi[2] <= RSIOverSold or rsi[3] <= RSIOverSold or rsi[4] <= RSIOverSold or rsi[5] <= RSIOverSold
wasOverbought = rsi[0] >= RSIOverBought or rsi[1] >= RSIOverBought or rsi[2] >= RSIOverBought or rsi[3] >= RSIOverBought or rsi[4] >= RSIOverBought or rsi[5] >= RSIOverBought


[currMacd,_,_] = macd(close[0], fastMA, slowMA, signalLength)
[prevMacd,_,_] = macd(close[1], fastMA, slowMA, signalLength)
signal = ema(currMacd, signalLength)

crossoverBear = cross(currMacd, signal) and currMacd < signal ? avg(currMacd, signal) : na
crossoverBull = cross(currMacd, signal) and currMacd > signal ? avg(currMacd, signal) : na

plotshape(crossoverBear and wasOverbought , title='MACD-BEAR', style=shape.triangledown, text='overbought', location=location.abovebar, color=orange, textcolor=orange, size=size.tiny) 
plotshape(crossoverBull and wasOversold, title='MACD-BULL', style=shape.triangleup, text='oversold', location=location.belowbar, color=lime, textcolor=lime, size=size.tiny) 

// Configure backtest start date with inputs
startDate = input(title="Start Date",
     defval=8, minval=1, maxval=31)
startMonth = input(title="Start Month",
     defval=3, minval=1, maxval=12)
startYear = input(title="Start Year",
     defval=2021, minval=1800, maxval=2100)

afterStartDate = (time >= timestamp(syminfo.timezone,
     startYear, startMonth, startDate, 0, 0))
     
if (afterStartDate==true)
    posSize = abs(strategy.position_size)
    strategy.order("long", strategy.long, when = crossoverBull and wasOversold) 
    strategy.order("long", long=false, qty=posSize/3, when = crossoverBear and wasOverbought) 

```

> Detail

https://www.fmz.com/strategy/435766

> Last Modified

2023-12-18 17:19:03
