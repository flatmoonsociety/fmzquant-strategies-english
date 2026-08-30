
> Name

Momentum-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/e8b1d084702b9fa50f.png)

[trans]

## Overview
This strategy uses the VIDYA (Variable Exponential Moving Average) indicator to identify the trend direction of the cryptocurrency market and trade based on the trend. It is a quantitative technical trading strategy.
## Strategy Principle
The strategy first calculates the VIDYA indicator. The VIDYA indicator is based on the momentum of price changes and can respond more quickly to trend changes. Specifically, it combines the Chande Momentum Oscillator (CMO) and the Simple Moving Average (SMA). CMO measures the difference between upward and downward price momentum to determine the strength of a trend. SMA smoothes prices. VIDYA dynamically adjusts the weight of SMA based on the value of CMO, giving greater weight to CMO in the early stages of trend changes, and giving greater weight to SMA after the trend is formed. In this way, VIDYA can quickly respond to trend changes while also maintaining smooth tracking of trends.
After calculating VIDYA, the strategy determines the direction of the trend based on the direction of the curve. When VIDYA rises, go long; when VIDYA falls, close the position.
## Advantage Analysis
- The VIDYA indicator responds quickly and can capture trend changes early, which has more advantages than traditional indicators such as SMA.
- Combined with the judgment of trend strength and trend direction, it can effectively distinguish strong and weak trends and avoid being misled by false trends that shock the market.
- Judging only based on a single VIDYA indicator realizes the simplicity of the strategy. There will be no conflict or misleading indicators.
- Using long-term VIDYA settings can track long-term trends and help grasp the main trend direction.
- The strategy backtest performed well and had positive expected returns.
## Risk Analysis
- VIDYA may lag behind in responding to market emergencies and cannot immediately seize short-term trading opportunities.
- Long-term VIDYA settings are not sensitive to short-term trend changes, and there may be large retracements in the middle.
- Pure trend following strategies perform poorly in volatile market conditions. Can be combined with additional filters to improve performance.
- There is insufficient backtest data to fully verify the robustness of the strategy. In actual transactions, parameters need to be optimized and tested repeatedly.
- The cryptocurrency market is highly volatile, so position size and stop loss conditions must be carefully controlled, and risk management must be strict.
## Optimization direction
- Test adding volume price indicators or volatility indicators to improve the sensitivity of identifying trend changes.
- Test the combination of VIDYA and other trend indicators to form an indicator aggregation effect.
- Optimize the stop loss strategy and stop the loss as early as possible when the trend reverses.
- Optimize position management strategies and dynamically adjust positions according to market conditions.
- Test robustness under different cryptocurrencies and cycle parameters.
## Summarize
The strategy as a whole is a quantitative trend following strategy. It uses the VIDYA indicator to determine the trend direction and grasp the long-term trend of cryptocurrency simply and effectively. However, there are also some limitations, and further optimization of stop loss, position management, etc. is required to make the strategy more robust and feasible. Overall, it provides a basic framework and ideas for building cryptocurrency trend strategies, but actual application requires careful evaluation.
||


## Overview

This strategy uses the VIDYA (Variable Index Dynamic Average) indicator to identify the trend direction in cryptocurrency markets and trades based on the trend. It is a quantitative technical trading strategy.

## Strategy Logic

The strategy first calculates the VIDYA indicator. The VIDYA indicator is based on price momentum and can respond to trend changes faster. Specifically, it combines the Chande Momentum Oscillator (CMO) and Simple Moving Average (SMA). CMO measures the difference between upward and downward momentum to gauge trend strength. SMA smoothes price data. VIDYA dynamically adjusts the weighting of SMA based on CMO values, giving more weight to CMO early in trend changes and more weight to SMA once the trend is established. Thus, VIDYA can quickly respond to trend changes while also maintaining a smooth tracking of the trend.

After calculating VIDYA, the strategy judges the trend direction based on the curve of VIDYA. It goes long when VIDYA rises and closes position when VIDYA falls.

## Advantage Analysis 

- VIDYA responds swiftly and can capture trend changes early compared to traditional indicators like SMA.

- Combining trend strength and direction, it can effectively distinguish strong and weak trends and avoid false trends in ranging markets.

- Relying solely on VIDYA makes the strategy simple. No conflicting or misleading signals from multiple indicators.

- Longer VIDYA settings allow tracking long-term trends and capturing the main trend direction.

- Good backtest results with positive expected returns.

## Risk Analysis

- VIDYA may lag in response to sudden market events and miss short-term trading opportunities.

- Long VIDYA settings make it less sensitive to short-term trend changes and can lead to larger drawdowns.

- Pure trend following performs poorly in choppy markets. Additional filters can improve performance.

- Limited backtest data cannot fully verify robustness. Parameters need iterative optimization and testing in live trading.

- High volatility in crypto markets. Position sizing and stop loss should be carefully controlled for strict risk management.

## Optimization Directions

- Test adding volume or volatility indicators to improve sensitivity to trend changes.

- Try combining VIDYA with other trend indicators for ensemble effect.

- Optimize stop loss strategy to exit early when trend reverses. 

- Optimize position sizing dynamically based on market conditions.

- Test robustness across different cryptocurrencies and timeframes.

## Conclusion

Overall this is a quantitative trend following strategy. It uses the VIDYA indicator to determine trend direction, capturing crypto trends simply and effectively. But it also has some limitations that require further optimizations in stop loss, position sizing etc. to make the strategy more robust and practically viable. In general, it provides a basic framework and approach for building crypto trend strategies, but prudent assessments are still needed for real-world applications.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(01 Jan 2000 08:00)|(?Date Range)Start Time|
|v_input_2|timestamp(01 Jan 2099 00:00)|End Time|
|v_input_int_1|50|(?Trend Settings)VIDYA Length|
|v_input_source_1_ohlc4|0|VIDYA Price Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-29 00:00:00
end: 2023-10-29 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// @version=5
// Author = TradeAutomation


strategy(title="VIDYA Trend Strategy", shorttitle="VIDYA Trend Strategy", process_orders_on_close=true, overlay=true, pyramiding=25,  commission_type=strategy.commission.percent, commission_value=.075, slippage = 1, initial_capital = 1000000, default_qty_type=strategy.percent_of_equity, default_qty_value=4)


// Backtest Date Range Inputs // 
StartTime = input(defval=timestamp('01 Jan 2000 08:00'), group="Date Range", title='Start Time')
EndTime = input(defval=timestamp('01 Jan 2099 00:00'), group="Date Range", title='End Time')
InDateRange = true

// Strategy Inputs //
len = input.int(title="VIDYA Length", defval=50, step=5,group="Trend Settings")
src = input.source(title="VIDYA Price Source",defval=ohlc4, group="Trend Settings")

// VIDYA Calculations //
valpha=2/(len+1)
vud1=src>src[1] ? src-src[1] : 0
vdd1=src<src[1] ? src[1]-src : 0
vUD=math.sum(vud1,9)
vDD=math.sum(vdd1,9)
vCMO=nz((vUD-vDD)/(vUD+vDD))
var VIDYA = 0.0
VIDYA := na(VIDYA[1]) ? ta.sma(src, len) : nz(valpha*math.abs(vCMO)*src)+(1-valpha*math.abs(vCMO))*nz(VIDYA[1])
plot(VIDYA, title="VIDYA",color=(VIDYA > VIDYA[1]) ? color.green : (VIDYA<VIDYA[1]) ? color.red : (VIDYA==VIDYA[1]) ? color.gray : color.black, linewidth=2)

// Entry & Exit Signals //
if (InDateRange)
    strategy.entry("Long", strategy.long, when = VIDYA>VIDYA[1])
    strategy.close("Long", when = VIDYA<VIDYA[1])
if (not InDateRange)
    strategy.close_all()
    
```

> Detail

https://www.fmz.com/strategy/430552

> Last Modified

2023-10-30 11:36:26
