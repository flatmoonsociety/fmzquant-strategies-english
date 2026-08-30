
> Name

RSI Rising Crypto Trending Strategy RSI-Rising-Crypto-Trending-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1d6d8fd92bec27a72d6.png)

[trans]

## Overview
The RSI Rising Crypto Trend Strategy is a cryptocurrency and stock market trend strategy that works on longer time periods, such as 4 hours or more.
This strategy uses the RSI indicator to identify rising and falling trends, combined with the Bollinger Bands and Rate of Change indicators to avoid trading sideways. Based on testing, this strategy performs better in crypto-to-crypto trading, rather than trading against fiat currencies.
## Strategy Principle
This strategy uses the following indicators:
- RSI - identifies up and down trends
- Bollinger Bands - Identify consolidation trends
- Rate of change - identifies the direction of the trend
The specific trading rules are as follows:
**Opening Rules**
Open a long position: The RSI value rises and the Bollinger Bands and rate of change indicators indicate that it is no longer consolidating, go long
Open a short position: The RSI value drops and the Bollinger Bands and rate of change indicators indicate that it is no longer consolidating, go short
**Closing Rules**
Close a position when a reverse signal is received
## Advantage Analysis
- Use the RSI indicator to identify the trend direction and capture the turning point of the trend in time.
- Use Bollinger Bands to identify consolidation to avoid missing the trend or getting stuck
- The rate of change indicator assists in confirming the trend direction, making trading signals more reliable
- Suitable for longer period trading and beneficial to profits
- More suitable for cryptocurrency-to-cryptocurrency trading to avoid fiat currency exchange rate risks
## Risk Analysis
- This strategy has no stop loss rules and involves greater risks
- Improper setting of Bollinger Bands and Rate of Change parameters can lead to missed opportunities or false signals
- Relying solely on technical indicators cannot cope with major black swan events
It is necessary to pay attention to increasing the stop loss range, adjusting the combination of Bollinger Bands and change rate parameters, and combining it with fundamental analysis.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Add a stop-loss mechanism, set a reasonable stop-loss range, and control single losses.
2. Optimize the parameters of Bollinger Bands and rate of change indicators to find the best parameter combination. Can be optimized through backtesting.
3. Add other auxiliary indicators, such as MACD, KD, etc., to achieve multi-indicator combination and improve signal accuracy.
4. Develop a flow-stop model to suspend trading during abnormal fluctuations to avoid being trapped.
5. Use machine learning methods to automatically optimize parameter combinations and signal weights.
6. Combined with on-chain data, pay attention to parameters such as exchange liquidity and capital flow to improve the adaptability of the strategy.
## Summarize
The RSI rising crypto trend strategy uses the RSI indicator supplemented by Bollinger Bands and rate of change indicators to achieve the effect of capturing cryptocurrency market trends over a longer period of time. The advantage of this strategy is to capture trend turning points in time to avoid being trapped, and is suitable for tracking longer-term directional opportunities. However, this strategy also has problems such as no stop loss and over-reliance on parameters. In the future, improvements can be made through stop loss, parameter optimization, multi-index combination, machine learning and other methods to make the strategy more robust and reliable.
||

## Overview

The RSI Rising Crypto Trending Strategy is a trend trading strategy designed for longer timeframes (4h+) in crypto and stock markets. 

It utilizes RSI to identify rising and falling trends combined with Bollinger Bands and ROC to avoid trading in sideways markets. From tests, it appears to work better trading crypto against crypto rather than against fiat.

## Strategy Logic

The strategy uses the following indicators:

- RSI - To identify rising/falling trends
- Bollinger Bands - To identify sideways markets  
- ROC - To confirm trend direction

The specific trading rules are:

**Entry Rules**

Long entry: RSI rising AND not sideways market per BB and ROC
Short entry: RSI falling AND not sideways market per BB and ROC

**Exit Rules**

Exit when opposite signal is triggered

## Advantage Analysis 

- Captures trend turning points early using RSI 
- Avoids getting trapped in sideways markets using BB
- ROC confirms trend direction for more robust signals
- Good for longer timeframe trades and capturing trends
- Better for crypto/crypto pairs to avoid fiat exposure

## Risk Analysis

- No stop loss so high risk of large losses
- Poor BB and ROC parameters could lead to missed trades or bad signals
- Purely technical so misses major black swan events  

Increase stop loss, optimize BB/ROC parameters, and incorporate fundamental analysis.

## Enhancement Opportunities

Some ways this strategy could be improved:

1. Add stop loss for risk management and setting maximum loss per trade.

2. Optimize BB and ROC parameters through backtesting to find best settings.

3. Incorporate additional indicators like MACD, KD for multi-indicator signal reliability. 

4. Build a liquidity model to pause trading during volatility spikes to avoid traps.

5. Use machine learning to automatically optimize parameters and signal weighting.

6. Incorporate on-chain data like exchange liquidity and fund flows for greater adaptability.

## Summary

The RSI Rising Crypto Trend Strategy captures longer timeframe crypto trends using RSI plus BB and ROC. The advantage is quickly catching trend reversals and avoiding traps. The weaknesses are no stop loss and parameter dependency. Enhancements like stop loss, optimization, machine learning can make it more robust.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Day|
|v_input_2|true|From Month|
|v_input_3|2010|From Year|
|v_input_4|31|To Day|
|v_input_5|12|To Month|
|v_input_6|2021|To Year|
|v_input_7|19|periods|
|v_input_8|14|RSI Length|
|v_input_9_low|0|Source: low|high|close|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-16 00:00:00
end: 2023-10-16 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=4
strategy(title = "RSI Rising", overlay = true, initial_capital = 100, default_qty_type= strategy.percent_of_equity, default_qty_value = 100, slippage=0,commission_type=strategy.commission.percent,commission_value=0.03)

/////////////////////
source          = close
bb_length       = 20
bb_mult         = 1.0
basis           = sma(source, bb_length)
dev             = bb_mult * stdev(source, bb_length)
upperx           = basis + dev
lowerx           = basis - dev
bbr             = (source - lowerx)/(upperx - lowerx)
bbr_len         = 21
bbr_std         = stdev(bbr, bbr_len)
bbr_std_thresh  = 0.1
is_sideways     = (bbr > 0.0 and bbr < 1.0) and bbr_std <= bbr_std_thresh


////////////////
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2010, title = "From Year", minval = 1970)
 //monday and session 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2021, title = "To Year", minval = 1970)

startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true


sourcex = close
length = 2
pcntChange = 1

roc = 100 * (sourcex - sourcex[length])/sourcex[length]
emaroc = ema(roc, length/2)
isMoving() => emaroc > (pcntChange / 2) or emaroc < (0 - (pcntChange / 2))


periods = input(19)
smooth = input(14, title="RSI Length" )
src = input(low, title="Source" )


rsiClose = rsi(ema(src, periods), smooth)
long=rising(rsiClose,2) and not is_sideways and isMoving()
short=not rising(rsiClose,2) and not is_sideways and isMoving()


if(time_cond)
    strategy.entry('long',1,when=long)
    strategy.entry('short',0,when=short)

```

> Detail

https://www.fmz.com/strategy/429506

> Last Modified

2023-10-17 17:08:31
