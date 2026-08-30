
> Name

RSI Moving Average Crossover Trend Strategy RSI-Moving-Average-Crossover-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/82e27a52e02841de9509bd3b388f887d95ebab9e7e1080cf9f03b8bf07c7fb3f.png)

[trans]

## Overview
RSI Moving Average Crossover Trend Strategy is a strategy that uses the moving average crossover signal of the RSI indicator to determine trends and issue trading signals. This strategy also combines the EMA of the price. Only when the price is higher than the EMA, a buy signal will be issued.
## Strategy Principle
The core indicator of this strategy is RSI, and the two moving averages of RSI, EMA and SMA, are calculated at the same time. Only when the EMA line of RSI is higher than the SMA line and the price is higher than the EMA, a buy signal will be issued; when the EMA line of RSI is lower than the SMA line, a sell signal will be issued to implement trend following.
The RSI indicator can effectively reflect the overbought and oversold conditions in the market. A break above 70 on the RSI indicator is considered an overbought market, while a break below 30 is considered oversold. This strategy uses two moving averages, EMA and SMA, to discover trends and turning points in the RSI indicator. The EMA line is more sensitive to the latest price changes, while the SMA line is more dependent on old data, and the two can cooperate.
When the EMA of the RSI begins to rise, it indicates that the market is showing signs of consolidation and stabilization. At this time, the SMA is used to verify its direction; when the SMA also begins to rise, it indicates that the RSI has clearly entered an upward trend. At this time, the strategy will issue a buy signal on the premise that the price is higher than the EMA to follow the trend.
## Advantage Analysis
This is a trend-tracking strategy that can effectively seize mid- to long-term directional opportunities. Compared with a single indicator, this strategy uses RSI's EMA and SMA to form cross-validation, which can reduce false signals and enhance stability.
This strategy also combines the EMA of price to ensure that you only buy when the price is rising, avoiding the risk of market shocks, thereby increasing the probability of profit.
## Risk Analysis
This strategy is mainly based on the RSI indicator. When RSI generates an error signal, the strategy will also send out an error signal. In addition, the RSI indicator is more suitable for judging overbought and oversold phenomena, and has a certain lag in judging medium and long-term trends.
This strategy also has a certain time lag, especially when the EMA and SMA of RSI are flat and consolidated, which will cause the signal to be delayed. There is also a certain risk of loss during this period.
## Optimization direction
1. You can consider optimizing RSI and selecting more appropriate parameters to enhance its judgment effect.
2. You can consider adding stop-loss logic to exit the position after the loss reaches a certain level to effectively control risks.
3. You can test the parameter settings of different time periods and optimize the parameters so that the strategy can run stably on more varieties and more periods.
## Summarize
The RSI moving average crossover trend strategy is a simple strategy that uses the RSI indicator to determine the trend direction and cross-validate it. Combined with price EMA, it can seize directional opportunities in upward trends. This strategy has high stability and is suitable for medium and long-term holdings, but attention must be paid to guarding against certain lag risks. Through further optimization, the performance of this strategy can be made even better.
||

## Overview  

The RSI Moving Average Crossover Trend Strategy is a strategy that uses the moving average crossover signals of the RSI indicator to determine the trend and issue trading signals. The strategy also incorporates the price EMA, issuing buy signals only when the price is above the EMA.  

## Strategy Logic  

The core indicator of this strategy is RSI. It calculates both the EMA and SMA of the RSI. Buy signals are only issued when the RSI EMA is above the SMA while the price is above the EMA. Sell signals are issued when the RSI EMA falls below the SMA to follow the trend.

The RSI indicator can effectively reflect overbought and oversold conditions in the market. Breaking above 70 on the RSI is regarded as overbought while breaking below 30 is oversold. This strategy utilizes the EMA and SMA to discover trends and turning points of the RSI indicator. The EMA reacts faster to recent price changes while the SMA relies more on older data. The two lines work together.  

When the RSI EMA starts picking up, it signals stabilization in the market. The SMA then verifies the direction. When the SMA also starts rising, it confirms the RSI is in an uptrend. The strategy will now issue a buy signal given that the price is above EMA to follow the trend.

## Advantage Analysis

This is a trend following strategy, capable of effectively catching directional opportunities over the medium to long term. Compared to single indicators, this strategy uses RSI EMA and SMA crossover for verification, reducing false signals and increasing stability.  

The strategy also incorporates the price EMA to ensure buying only in a price uptrend, avoiding the risk of range-bound markets and improving profitability.  

## Risk Analysis

The strategy relies mainly on the RSI indicator. False RSI signals will lead to false strategy signals. Also, the RSI is more suitable for identifying overbought/oversold levels with some lag in catching mid-long term trends.

There can also be some time lag, especially when the RSI EMA and SMA are more range-bound. This period carries some loss risk before signals are triggered.  

## Optimization Directions 

1. The RSI can be optimized by selecting more appropriate parameters to enhance effectiveness.

2. Stop loss logic can be added to exit positions after losses reach certain levels to effectively manage risk.

3. Parameters can be tested and optimized across different timeframes so that the strategy can run stable on more products and periods.

## Summary  

The RSI Moving Average Crossover Trend Strategy is a simple trend following strategy using RSI to determine trend direction and crossovers for verification. It incorporates price EMA to buy on uptrends. The strategy has high stability for mid-long term holding but lag risk needs to be managed. Further optimizations can improve strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|From Month|
|v_input_2|true|From Day|
|v_input_3|2015|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|16|RSILength|
|v_input_8|12|RSI EMA Length|
|v_input_9|29|RSI SMA Length2|
|v_input_10|8|EMA price Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-21 00:00:00
end: 2023-11-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//Created by Sv3nla 5-Jan-2021
strategy(title="Sv3nla RSI EMA SMA Strat", shorttitle="Sv3nla RSI EMA SMA Strat", overlay=true, initial_capital=1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// === BACKTEST RANGE ===
FromMonth = input(defval = 5, title = "From Month", minval = 1)
FromDay   = input(defval = 1, title = "From Day", minval = 1)
FromYear  = input(defval = 2015, title = "From Year", minval = 2015)
ToMonth   = input(defval = 1, title = "To Month", minval = 1)
ToDay     = input(defval = 1, title = "To Day", minval = 1)
ToYear    = input(defval = 9999, title = "To Year", minval = 2022) 
// syminfo.mintick = 0.01$ for BTCUSDT

testPeriod() => true

//INPUTS
rsilen = input(defval = 16, minval=1, title="RSILength")
RSIemaLen = input(defval = 12, minval=1, title="RSI EMA Length")
RSIsmaLen2 = input(defval = 29, minval=1, title="RSI SMA Length2")
length = input(defval = 8, minval=1, title="EMA price Length")

// RSI
RSIsrc = close
RSIup = rma(max(change(RSIsrc), 0), rsilen)
RSIdown = rma(-min(change(RSIsrc), 0), rsilen)
rsi = RSIdown == 0 ? 100 : RSIup == 0 ? 0 : 100 - 100 / (1 + RSIup / RSIdown)
emavalue=ema(rsi,RSIemaLen)
smavalue=sma(rsi,RSIsmaLen2)

//EMA
ema=ema(close,length)

//PLOT
plot(ema(rsi, RSIemaLen), color=color.yellow, linewidth=2, title="EMA", transp=0)
plot(sma(rsi, RSIsmaLen2), color=color.aqua, linewidth=2, title="SMA", transp=0)

//ORDERS
if (testPeriod())
    strategy.entry("long",strategy.long, comment="RSIEMA", when=(emavalue > smavalue and close>ema))
    strategy.close(id="long", when=(emavalue < smavalue))

// Colour background when in a trade and 50 horizontal line
backgroundColour = (strategy.position_size > 0) ? color.green : na    
bgcolor(color=backgroundColour, transp=85)
hline(50, color=color.yellow)
```

> Detail

https://www.fmz.com/strategy/433590

> Last Modified

2023-11-28 17:03:56
