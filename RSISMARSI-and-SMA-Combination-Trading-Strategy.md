
> Name

RSI and SMA Combination Trading StrategyRSI-and-SMA-Combination-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The core idea of ​​this strategy is to combine the RSI indicator and the SMA moving average to achieve position trading in the trend. When the RSI indicator shows overbought or oversold, combined with the long and short cross signals of the SMA moving average, long or short positions are opened and closed. This strategy is designed to identify short-term reversal opportunities for profit.
## Strategy Principle
This strategy uses the RSI indicator to determine the timing of reversal of overbought and oversold trends. An RSI value above 70 is considered overbought, and a value below 30 is considered oversold. At the same time, the intersection of the SMA fast line and the slow line is used to determine the trend direction. The fast line crossing the slow line is a bullish signal, and the fast line crossing the slow line below is a bearish signal.
When the RSI is above 50 and the fast line crosses the slow line, open a long order. When the RSI is below 50 and the fast line crosses the slow line, open a short order. When a long order has been opened, if the RSI is lower than 50 and the fast line crosses the slow line, the long order will be closed and a short order will be opened. When a short order has been opened, if the RSI is higher than 50 and the fast line crosses the slow line, the short order will be closed and a long order will be opened.
The trading logic of this strategy mainly includes:
1. Calculate the RSI indicator, the length is 14
2. Calculate the SMA fast line, the length is 100
3. Calculate the SMA slow line, the length is 150
4. RSI > 50 and the fast line crosses the slow line, which is a long signal
5. RSI < 50 and the fast line crosses the slow line, which is a short signal
6. Open long and short orders based on signals
## Advantage Analysis
This strategy has the following advantages:
1. Combine trend and reversal indicators to capture short-term reversal opportunities
2. The RSI indicator can effectively identify overbought and oversold phenomena.
3. The intersection of SMA fast and slow lines is more reliable in judging the trend direction.
4. The strategy logic is simple and clear, easy to understand and implement
5. Backtest results show that good returns can be obtained even in a bear market
6. Adopt fixed position management, no need to adjust positions frequently
## Risk Analysis
This strategy also has certain risks:
1. Reverse the risk of failure. RSI reversal signals are not always reliable, and false rebounds may occur leading to losses.
2. The trend is unclear. The trading signal sent by the fast and slow line crossover may be destroyed by the trend reversal midway.
3. Impact of handling fees. Frequent transactions will be greatly affected by handling fees and may erode profits.
4. Parameter optimization. Parameters such as RSI length and SMA period need to be continuously tested and optimized, otherwise the effect will be compromised.
5. Risk of large fluctuations. The strategic retracement may be relatively large, so you need to be mentally prepared.
In response to the above risks, the following measures can be taken:
1. Combine with other indicators to filter signals and improve signal quality
2. Adjust the position size according to the general cycle trend to reduce the risk of reversal failure
3. Optimize parameters and reduce transaction frequency to reduce the impact of handling fees
4. Use stop loss to control single losses
## Strategy optimization
This strategy can also be optimized from the following aspects:
1. Test different RSI parameter combinations and find the best parameters
2. Test different SMA cycle parameters and determine the optimal parameters
3. Reduce the position size when the trend is unclear
4. Combine with other indicators such as MACD, KD, etc. for signal filtering
5. Test different stop loss methods and find the best stop loss point
6. Optimize position management strategies and dynamically adjust positions according to market conditions
7. Combined with advanced order types to achieve smarter stop loss and entry
## Summarize
Overall, this strategy is a typical short-term reversal strategy. Through the combined use of RSI indicator and SMA moving average, it can seize the reversal opportunities brought by short-term overbought and oversold phenomena to make profits. This strategy has the advantages of simple trading logic and few parameters, but it also has certain risks of reversal failure and trend destruction. By continuously testing and optimizing parameters and assisting other indicators in signal filtering, the strategy winning rate can be improved. In addition, the rational use of stop loss and position management is also very important. In general, this strategy is quite practical as a short-term strategy and is worth a try.
||

## Overview

The core idea of this strategy is to combine the RSI indicator and SMA moving averages to implement position trading in trends. When the RSI indicator shows overbought or oversold conditions, it opens or closes long or short positions according to the crossover signals of the SMA moving averages. The strategy aims to discover short-term reversal opportunities to make profits.

## Strategy Logic

This strategy uses the RSI indicator to determine the timing of trend reversal when overbought or oversold, with RSI values above 70 indicating overbought and below 30 indicating oversold conditions. It also uses the crossover of fast and slow SMA lines to determine the trend direction, with the fast line crossing above the slow line being a bullish signal and the fast line crossing below the slow line being a bearish signal.

When RSI is above 50 and the fast SMA crosses above the slow SMA, it opens a long position. When RSI is below 50 and the fast SMA crosses below the slow SMA, it opens a short position. When a long position is already open, if RSI falls below 50 and the fast SMA crosses below the slow SMA, it will close the long and open a short position. When a short position is already open, if RSI rises above 50 and the fast SMA crosses above the slow SMA, it will close the short and open a long position.

The main trading logic of this strategy includes:

1. Calculating the RSI indicator, with a length of 14

2. Calculating the fast SMA, with a length of 100 

3. Calculating the slow SMA, with a length of 150

4. RSI > 50 and fast SMA crossing above slow SMA gives long signal

5. RSI < 50 and fast SMA crossing below slow SMA gives short signal

6. Opening and closing long/short positions based on the signals

## Advantage Analysis 

This strategy has the following advantages:

1. Combining trend and reversal indicators can capture short-term reversal opportunities

2. RSI indicator can effectively identify overbought and oversold conditions

3. SMA crossover can reliably determine trend direction 

4. The strategy logic is simple and clear, easy to understand and implement

5. Backtest results show decent returns even in a bear market

6. Uses fixed position sizing, no need for frequent adjustment

## Risk Analysis

This strategy also has some risks:

1. Failed reversal risk. RSI reversal signals are not always reliable, false breakouts may cause losses.

2. Unclear trend. Trading signals from SMA crossover may be disrupted by mid-term trend reversals.

3. Fee impact. Frequent trading can be significantly affected by fees, eating into profits.

4. Parameter optimization. RSI length, SMA periods need continual testing and tuning.

5. Whipsaw risk. Strategy drawdown can be sizable, need psychological preparation.

To address these risks, the following measures can be taken:

1. Add other filters to improve signal quality 

2. Adjust position sizing according to major trend to reduce reversal failure risk

3. Optimize parameters to reduce trading frequency and fee impact

4. Use stop loss to control single trade loss

## Optimization Directions

This strategy can also be optimized in the following aspects:

1. Test different RSI parameter combinations to find the optimal

2. Test different SMA period parameters to determine the best

3. Reduce position sizing when trend is unclear

4. Add other indicators like MACD, KD for signal filtering

5. Test different stop loss methods to find the optimal stop loss points

6. Optimize position sizing strategy according to market conditions

7. Use advanced order types for smarter stop loss and entry

## Summary

Overall this is a typical short-term mean reversion strategy, utilizing the combination of RSI indicator and SMA moving averages, it can capture profit from short-term overbought and oversold reversals. The strategy has the advantage of simple logic and few parameters, but also has some reversal failure risks and trend disruption risks. Through continual testing and parameter optimization, and adding other filters, the win rate can be improved. In addition, proper use of stop loss and position sizing is also very important. In summary, this strategy is quite practical as a short-term system and is worth trying out.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_2|14|length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-02 00:00:00
end: 2023-10-08 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=5
strategy('RSI and SMA',
         overlay=true,
         initial_capital=1000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=30,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 1, 1, 0, 0)
notInTrade = strategy.position_size <= 0

//==================================Buy Conditions============================================
//RSI
length = input(14)
rsi = ta.rsi(close, length)

//SMA
fastEMA = ta.sma(close, 100)
slowEMA = ta.sma(close, 150)
plot(fastEMA, color = color.green)
plot(slowEMA, color = color.blue)


bullish = ta.crossover(fastEMA, slowEMA) and rsi > 50
bearish = ta.crossover(slowEMA, fastEMA) and rsi < 50

strategy.entry("Long", strategy.long, when=bullish and timePeriod)
strategy.close("Exit", when=bearish)

strategy.entry("Short", strategy.short, when=bearish and timePeriod)
strategy.close("Exit", when=bullish)





```

> Detail

https://www.fmz.com/strategy/428799

> Last Modified

2023-10-09 15:42:48
