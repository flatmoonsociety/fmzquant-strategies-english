
> Name

Price-Momentum-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1646bdd6510619422d1.png)

[trans]

### Overview
This strategy uses the price momentum indicator to determine trade direction. Specifically, the moving average and average price are calculated separately, and a buy signal is generated when the price crosses the moving average and average price. In order to filter out false signals, it is required that there are no similar signals before. Then save the signal status and combine it with the moving average judgment to generate the final opening signal. The strategy includes both stop loss and take profit settings.
### Strategy Principles
This strategy is primarily based on the price momentum indicator to determine trend direction. First calculate the moving average and average price of the price:
```pine
swmaClose = swma(close)  
vwapClose = vwap(close)
```

Among them, `swma` is the moving average, and `vwap` is the volume-weighted average price. Both reflect price averages.
Then compare the relationship between the price and the mean to determine whether it crosses the moving average and the average price, thereby determining whether it is a bullish signal:
```pine 
swmaLong = close > swmaClose
vwapLong = close > vwapClose 
```

In order to filter out false signals, it is required that these two indicators have not given signals before:
```pine
triggerLong = vwapLong and not vwapLong[1] and not swmaLong and not swmaLong[1]
```

Next save the bullish signal:
```pine 
saveLong = false, saveLong := triggerLong ? true : not vwapLong ? false : saveLong[1]
```

Finally, when the upward crossing signal is saved and the price crosses above the moving average again, an opening signal is generated:
```pine
startLong = saveLong and swmaLong
```

This can filter out some false signals and make the signal more reliable.
The strategy also includes stop loss and take profit settings. The stop loss distance is configurable, and the take profit is set to a certain multiple of the stop loss.
### Advantage Analysis
This strategy has the following advantages:
1. Use the price momentum indicator to better judge the trend direction
2. Combining dual indicators and multi-step judgment can filter out false signals and make the strategy more reliable
3. The stop-loss and stop-profit settings are reasonable and can control the risk of a single transaction.
4. Strategy parameters can be configured to adapt to different market environments
5. The strategy logic is simple and direct, easy to understand and implement
### Risk Analysis
There are also some risks with this strategy:
1. The moving average indicator lags behind and may miss some price fluctuations.
2. The effect depends on parameter settings, and the effects of different parameter combinations vary greatly.
3. There are few buying signals and there is a certain risk of missing orders.
4. Multi-step judgment will filter out some opportunities and may affect profitability.
Countermeasures:
1. Can test different moving average parameters and optimize parameter settings
2. Appropriately simplify the judgment logic and increase buying signals
3. Adjust the stop-loss and take-profit ratios to control single losses
### Optimization direction
This strategy can also be optimized in the following directions:
1. Test more price momentum indicators, such as MACD, DMI, etc.
2. Increase the judgment of selling signals and realize two-way trading
3. Combine with trading volume indicators to avoid potential false breakthroughs
4. Optimize parameter settings based on backtest results
5. Consider automatically adjusting parameters based on market conditions
6. Add machine learning algorithms to achieve parameter adaptive optimization
These optimizations can improve strategy flexibility, robustness and profitability.
### Summarize
Overall, this price momentum tracking strategy is a simple, direct, and logical trend following strategy. The strategy uses price moving averages and average prices to determine the direction of price momentum, and designs a multi-step verification mechanism to improve signal quality. The strategy also includes reasonable stop loss and take profit settings. Judging from the amount of code, the strategy logic is very simple and only requires more than 20 lines of pine script to implement. Overall, this strategy is a very good learning case and can be used as a good starting point for beginners to understand quantitative trading strategies. Of course, the strategy itself also has actual trading value. Through parameter optimization and function expansion, it can become a practical trading system that avoids noise and tracks trends.
||

### Overview

This strategy uses price momentum indicators to determine the trading direction. Specifically, it calculates the moving average and mean price respectively. When the price crosses above the moving average and mean price, a buy signal is generated. To filter out false signals, it requires no similar previous signals. Then it saves the signal status and generates the final opening position signal in combination with the moving average. The strategy also contains stop loss and take profit settings.

### Strategy Principle

The strategy mainly relies on price momentum indicators to judge the trend direction. First it calculates the moving average and mean price of the price:  

```pine
swmaClose = swma(close)
vwapClose = vwap(close) 
```

Where `swma` is the smoothed moving average and `vwap` is volume weighted average price. Both can reflect the average price level.  

Then compare the price with the average to see if the price crosses above the moving average and mean price, to judge if it is a bullish signal:

```pine
swmaLong = close > swmaClose 
vwapLong = close > vwapClose
```

To filter out false signals, it requires no previous signals from these two indicators:

```pine  
triggerLong = vwapLong and not vwapLong[1] and not swmaLong and not swmaLong[1] 
```

Next, save the bullish signal:  

```pine
saveLong = false, saveLong := triggerLong ? true : not vwapLong ? false : saveLong[1] 
```

Finally, when the saved crossing signal and the price crosses above the moving average again, generate the opening position signal:  

```pine 
startLong = saveLong and swmaLong
```

This can filter out some false signals and make the signals more reliable.  

The strategy also contains stop loss and take profit settings. The stop loss distance is configurable, and the take profit is set to a certain multiple of the stop loss.

### Advantage Analysis  

The strategy has the following advantages:

1. Using price momentum indicators can better judge the trend direction  
2. The combination of dual indicators and multi-step verification can filter false signals and make the strategy more reliable
3. The stop loss and take profit settings are reasonable to control single trade risk
4. The strategy parameters are configurable to adapt to different market environments 
5. The strategy logic is simple and straightforward, easy to understand and implement

### Risk Analysis   

The strategy also has some risks:

1. The moving average indicator has a lag and may miss some price fluctuations  
2. The effect relies on parameter settings, and different parameter combinations can make big differences
3. There are relatively few buy signals, with some missed trade risks
4. Multi-step verification will filter some opportunities, which may impact profit level  

Countermeasures:
1. Test different moving average parameters for parameter optimization
2. Slightly simplify the logical judgment to increase buy signals  
3. Adjust the stop loss and take profit ratio to control single loss

### Optimization Directions   

The strategy can also be optimized in the following directions:  

1. Test more price momentum indicators such as MACD, DMI, etc.  
2. Add sell signal judgments to implement dual-direction trading
3. Incorporate trading volume indicators to avoid potential false breakouts  
4. Optimize parameter settings based on backtest results  
5. Consider automatically adjusting parameters based on market conditions
6. Add machine learning algorithms to achieve parameter self-adaptive optimization  

These optimizations can improve strategy flexibility, robustness and profitability.  

### Summary   

Overall, this price momentum tracking strategy is a simple, straightforward and logical trend tracking strategy. The strategy uses price moving averages and mean prices to determine price momentum direction, and designs a multi-step verification mechanism to improve signal quality. The strategy also contains reasonable stop loss and take profit settings. In terms of code, the strategy logic is very concise, requiring only 20+ lines of Pine script to implement. In summary, this strategy is a very good learning example, beginners can use it as a very good starting point to understand quantitative trading strategies. Of course, the strategy itself also has practical trading value. Through parameter optimization and function expansion, it can become a practical trading system to avoid noise and track trends.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Consecutive Orders|
|v_input_2|250|Stop Loss|
|v_input_3|10|Reward/Risk|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-03 00:00:00
end: 2024-01-02 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title = "Simple Price Momentum", shorttitle = "SPM", overlay = true, initial_capital = 20000, default_qty_value = 100, default_qty_type = strategy.percent_of_equity, commission_value = 0.025)

// How To Create A Simple Trading Strategy With TradingView
// https://docs.google.com/document/d/1fXxCtPuGgTXb-RuBJNbwlfgkeiLTK5060LfTrzRlr5k/view

swmaClose = swma(close)
vwapClose = vwap(close)

swmaLong = close > swmaClose
vwapLong = close > vwapClose

triggerLong = vwapLong and not vwapLong[1] and not swmaLong and not swmaLong[1]
saveLong = false, saveLong := triggerLong ? true : not vwapLong ? false : saveLong[1]

startLong = saveLong and swmaLong
startLong := input(false, "Consecutive Orders") ? startLong : startLong and not startLong[1]

stopLoss = input(250, "Stop Loss", step = 50)
takeProfit = input(10, "Reward/Risk") * stopLoss

strategy.entry("Open Long", strategy.long, when = startLong)
strategy.exit("Exit Long", "Open Long", profit = stopLoss, loss = takeProfit)

// bgcolor(swmaLong ? color.blue : na)
// bgcolor(vwapLong ? color.orange : na)
// bgcolor(triggerLong ? color.purple : na)
// bgcolor(saveLong ? color.yellow : na)
bgcolor(startLong[1] ? color.green : na)

```

> Detail

https://www.fmz.com/strategy/437561

> Last Modified

2024-01-03 17:32:14
