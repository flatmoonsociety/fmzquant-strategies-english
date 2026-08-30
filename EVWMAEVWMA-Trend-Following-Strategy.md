
> Name

Trend following strategy based on EVWMA indicatorEVWMA-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1bca646f3b9703973ee.png)
[trans]

## Overview
This strategy designs a simple trend following strategy based on the EVWMA indicator. This strategy uses the fast line and the slow line to construct the EVWMA indicator, going long when the fast line crosses the slow line, and going short when the fast line crosses below the slow line to achieve trend tracking.
## Strategy Principle
The core indicator of this strategy is EVWMA, which is the elastic weighted moving average. It dynamically reflects market trends by calculating its own cycle length and combining price and trading volume information.
Specifically, the calculation period length of the fast line is the sum of the trading volume of the last 10 K lines, and the calculation period length of the slow line is the sum of the trading volume of the last 20 K lines. The EVWMA of each K-line is calculated according to the formula of "(previous day's EVWMA × (cycle length - current K-line volume) + current K-line closing price × current K-line volume) / cycle length". This combines both price and volume information.
When the fast line crosses the slow line, it means that the buying power is strengthened, so go long; when the fast line crosses the slow line, it means the selling power is strengthened, and you go short. Through such a combination of fast and slow lines, market trends can be dynamically captured and trend following strategies can be implemented.
## Advantage Analysis
The biggest advantage of this strategy is that it uses the dynamic cycle design of the EVWMA indicator to respond more quickly to changes in price and trading volume and capture market trends in real time, which is very suitable for trend following strategies. In addition, compared with indicators such as traditional moving averages, it combines price and trading volume information and can filter out false breakthroughs.
## Risks and Solutions
The main risk of this strategy lies in the setting of EVWMA indicator parameters. If the fast and slow line periods are set improperly, a large number of false signals may be generated. Furthermore, the trend-following strategy itself is just as trendyțile as it is consecințe.
In order to solve these problems, the best parameter combination can be found by optimizing parameters and adjusting the calculation cycles of fast and slow lines. At the same time, you can set a stop loss to control the risk of loss. At a time when the market may undergo a major turning point, such as the release of important data, you can consider suspending the strategy to avoid this time period.
## Optimization direction
This strategy also has room for further optimization. For example, you can consider adding other indicators, such as trading volume breakthroughs, Bollinger Bands, etc., to confirm signals to improve the stability of the strategy. In addition, the optimal values ​​of parameter combinations for different varieties and different time periods may be different. A parameter adaptive optimization mechanism can be established to adjust parameters based on real-time data.
From a trading perspective, methods such as dynamic stop loss and trailing stop loss can also be designed to control risks. In addition, the optimal values ​​of parameter combinations for different varieties and different time periods may be different. A parameter adaptive optimization mechanism can be established to adjust parameters based on real-time data.
## Summarize
This strategy uses the dynamic cycle design of the EVWMA indicator and the consideration of trading volume information to build a simple and effective trend following strategy. It can quickly respond to price changes and capture market trends. Through parameter optimization, risk control and other means, the stability of the strategy can be further improved. This strategy is novel and worthy of further exploration and application.
||


## Overview  

This strategy is designed as a simple trend following strategy based on the EVWMA indicator. It uses fast line and slow line to construct the EVWMA indicator. A long position will be opened when the fast line crosses over the slow line, and a short position will be opened when the fast line crosses below the slow line, to follow the trend.  

## Strategy Logic

The core indicator of this strategy is EVWMA, namely Elastic Volume Weighted Moving Average. It incorporates both price and volume information to reflect the market trend dynamically by calculating its own period.

Specifically, the period of the fast line is calculated as the sum of volume of recent 10 bars, and 20 bars for the slow line. The EVWMA of each bar is calculated as "(Previous bar's EVWMA × (Period length - Current bar's volume) + Current bar's close price × Current bar's volume) / Period length". In this way, it combines both price and volume information.  

When the fast line crosses over the slow line, it indicates that the buying power is strengthening to go long. When the fast line crosses below the slow line, it indicates that the selling power is strengthening to go short. With such a combination of fast and slow lines, the strategy can capture the market trend dynamically to follow the trend.

## Advantage Analysis   

The biggest advantage of this strategy lies in the dynamic period design of the EVWMA indicator to respond faster to the changes in price and volume, thereby capturing the market trend in real time, which is very suitable for trend following strategies. Also, compared to traditional moving averages, it incorporates both price and volume information, which can filter false breakouts.  

## Risks and Solutions

The main risk of this strategy is the inappropriate parameter settings of the EVWMA indicator. If the periods of the fast and slow lines are not set properly, it may generate excessive false signals. Besides, trend following strategies themselves have some drawbacks when the market trend reverses sharply.

To solve these problems, we can optimize the parameters and adjust the calculation periods of fast and slow lines to find the best combination. Also, a stop loss can be set to control the risk of loss. Around time points when significant market reversal is likely to occur such as important data releases, we may consider temporarily suspending the strategy to avoid trades during this period.

## Optimization Directions 

There is room for further optimization of this strategy. For example, other indicators like breakout of trading volume, Bollinger Bands etc. can be incorporated to confirm the signals, thereby enhancing the stability of the strategy. Also, the optimal parameter values might differ across different products and time periods. An adaptive parameter optimization mechanism can be established to adjust parameters based on real-time data.  

On the trading aspects, dynamic stop loss, trailing stop loss and other means can also be designed to control risks. In addition, an adaptive parameter mechanism may help obtaining optimal parameters across different products and time periods.

## Summary

This strategy leverages the dynamic period design of the EVWMA indicator and incorporates volume information to construct an effective trend following strategy. It can respond quickly to price changes and capture market trends. With parameter optimization, risk control measures etc., the stability of the strategy can be further improved. The logic behind this strategy is innovative and worth further exploration and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Fast Sum Length|
|v_input_2|20|Slow Sum Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-05 00:00:00
end: 2023-12-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("QuantNomad - EVWMA Cross Strategy", shorttitle="EVWMA Cross", overlay=true)

// Inputs
fast_sum_length = input(10, title = "Fast Sum Length", type = input.integer)
slow_sum_length = input(20, title = "Slow Sum Length", type = input.integer)

// Calculate Volume Period
fast_vol_period = sum(volume, fast_sum_length)
slow_vol_period = sum(volume, slow_sum_length)

// Calculate EVWMA
fast_evwma = 0.0
fast_evwma := ((fast_vol_period - volume) * nz(fast_evwma[1], close) + volume * close) / (fast_vol_period)

// Calculate EVWMA
slow_evwma = 0.0
slow_evwma := ((slow_vol_period - volume) * nz(slow_evwma[1], close) + volume * close) / (slow_vol_period)

// Plot 
plot(fast_evwma, title = "EVWMA Fast", linewidth = 2, color = color.red)
plot(slow_evwma, title = "EVWMA Slow", linewidth = 2, color = color.green)

// Strategy
strategy.entry("Long",   true, when = crossover(fast_evwma, slow_evwma))
strategy.entry("Short", false, when = crossunder(fast_evwma, slow_evwma))
```

> Detail

https://www.fmz.com/strategy/435137

> Last Modified

2023-12-12 16:00:37
