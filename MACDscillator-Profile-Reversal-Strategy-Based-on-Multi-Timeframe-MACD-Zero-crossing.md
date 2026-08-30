
> Name

Multi-timeframe MACD Zero-axis Crossing Reversal Strategy scillator-Profile-Reversal-Strategy-Based-on-Multi-Timeframe-MACD-Zero-crossing
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/7a422427830a290110.png)
[trans]
## Overview
The multi-time period MACD zero-axis cross reversal strategy calculates MACD indicators of different periods, identifies signals of possible price reversals, and adopts trend following stop loss methods to pursue higher capital utilization efficiency.
## Strategy Principle
This strategy simultaneously calculates the 3-period and 10-period SMA moving averages, constructs fast and slow lines, and then calculates the MACD indicator and signal line. When the fast line and the signal line cross the upward or downward zero axis, it means that the price has reached a critical point and a reversal may occur. In addition, this strategy also combines the long and short situation judgment of trading volume, RSI indicators, etc. to identify the reliability of reversal signals. When the reversal signal reaches certain reliability requirements, go long or short.
Specifically, the strategy determines price reversals by:
1. MACD zero axis crosses, indicating that the price has reached a critical point
2. Judgment of long and short situation based on trading volume and buying and selling pressure
3. The RSI indicator is bullish on the bullish and bearish forces, and combined with changes in the MACD slope, determines the strength of the reversal signal.
4. The fast line and the signal line cross in opposite directions to form a reversal signal
When the reliability of the reversal signal is high, the strategy adopts the trend following stop loss method to enter the market and pursue higher returns.
## Advantage Analysis
This strategy has several advantages:
1. Multi-indicator judgment makes reversal signals more reliable
2. Use MACD zero axis cross to determine the reversal point with high accuracy.
3. RSI indicator and trading volume assist judgment, with high reliability
4. Trend following stop loss method to pursue higher capital utilization efficiency
## Risk Analysis
There are also some risks with this strategy:
1. The MACD indicator has a high probability of sending out false signals, and it is easy to be trapped.
2. During the alternation between long and short, the probability of stop loss being penetrated is high.
3. Improper parameter settings may lead to too frequent transactions, increased transaction costs and slippage losses.
Risks can be reduced by:
1. Appropriately relax the stop loss range to avoid being trapped
2. Optimize parameters and reduce transaction frequency
3. Only consider entering near key support and resistance levels
## Optimization direction
Directions in which this strategy can be further optimized include:
1. Add machine learning algorithm to assist in judging the reliability of reversal signals
2. Add sentiment indicators to judge the psychological aspects of long and short
3. Combine key support and resistance levels to improve entry accuracy
4. Optimize stop loss methods to further improve capital utilization efficiency
5. Test the optimal parameter combination to reduce transaction frequency
## Summary
The multi-time period MACD zero-axis cross reversal strategy comprehensively considers information from multiple dimensions such as price, trading volume and volatility indicators, determines the timing of reversal entry through multi-indicator judgment, and stops losses in time after sufficient profits are made, so that better returns can be obtained in reversal markets. This strategy is expected to be further improved through machine learning and key position optimization to reduce transaction frequency and risks and increase profit margins.
||

## Overview  
The 3 10.0 Oscillator Profile Reversal strategy identifies potential price reversals by calculating MACD indicators across different timeframes. It adopts a trend-following stop loss approach to pursue higher capital efficiency.  

## Strategy Logic
The strategy calculates SMA moving averages of 3 and 10 periods to construct fast and slow lines and the MACD indicator and signal line. When the fast line and signal line cross the zero line upward or downward, it indicates the price has reached a critical point and a reversal may occur. In addition, it also incorporates volume pressure judgment, RSI index etc. to identify reliability of reversal signals. It goes long or short when reversal signals meet certain reliability requirements.  

Specifically, the strategy judges price reversals through:  
1. MACD zero-crossing indicates price reaches critical point
2. Volume pressure judges bullish or bearish sentiment  
3. RSI index with MACD slope change determines strength of reversal signals  
4. Fast line and signal line crossing in reverse direction forms reversal signal  

When reversal signal reliability is high, the strategy adopts trend-following stop loss to pursue higher profit.  

## Advantage Analysis  
The strategy has the following advantages:   

1. Multiple indicators make reversal signals more reliable
2. MACD zero-crossing accurately locates reversal points  
3. RSI and volume assist judgment to improve reliability   
4. Trend-following stop loss improves capital efficiency   

## Risk Analysis
There are also some risks:   

1. High probability of MACD false signals and being trapped  
2. High chance of stop loss being hit during alternating trends   
3. Improper parameter setting may increase trading frequency and cost  

Risks can be reduced through:  
1. Allow wider stop loss to avoid being trapped  
2. Optimize parameters to lower trading frequency  
3. Only consider entry near key support/resistance levels  

## Optimization Directions
The strategy can be further optimized through:   

1. Add machine learning algorithms to assist reversal signal reliability  
2. Add sentiment indices to determine bull/bear mentality  
3. Combine key support/resistance levels to improve entry precision   
4. Optimize stop loss for higher capital efficiency   
5. Test optimal parameter combinations to lower trading frequency   

## Conclusion
The multi timeframe MACD zero-crossing reversal strategy comprehensively considers price, volume and volatility indicators to determine entry timing through multi-indicator evaluation. It sets timely stop loss upon sufficient profitability. It can achieve good returns during reversal markets. Further improvements on machine learning and key level integration may lower risks and trading frequencies while improving profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.26|Signal Bias|
|v_input_2|0.8|MACD Bias|
|v_input_3|3|Short LookBack|
|v_input_4|10|Long LookBack|
|v_input_5|0.8|Take Profit|
|v_input_6|0.75|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-11 00:00:00
end: 2024-02-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("3 10.0 Oscillator Profile Flagging", shorttitle="3 10.0 Oscillator Profile Flagging", overlay=false)

signalBiasValue = input(title="Signal Bias", defval=0.26)
macdBiasValue = input(title="MACD Bias", defval=0.8)
shortLookBack = input( title="Short LookBack", defval=3)
longLookBack = input( title="Long LookBack", defval=10.0)
takeProfit = input( title="Take Profit", defval=0.8)
stopLoss = input( title="Stop Loss", defval=0.75)

fast_ma = ta.sma(close, 3)
slow_ma = ta.sma(close, 10)
macd = fast_ma - slow_ma
signal = ta.sma(macd, 16)
hline(0, "Zero Line", color = color.black)

buyVolume = volume*((close-low)/(high-low))
sellVolume = volume*((high-close)/(high-low))
buyVolSlope = buyVolume - buyVolume[1]
sellVolSlope = sellVolume - sellVolume[1]
signalSlope = ( signal - signal[1] )
macdSlope = ( macd - macd[1] )
plot(macd, color=color.blue, title="Total Volume")
plot(signal, color=color.orange, title="Total Volume")
intrabarRange = high - low
rsi = ta.rsi(close, 14)
rsiSlope = rsi - rsi[1]

getRSISlopeChange(lookBack) =>
    j = 0
    for i = 0 to lookBack
        if ( rsi[i] - rsi[ i + 1 ] ) > -5
            j += 1
    j

getBuyerVolBias(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if buyVolume[i] > sellVolume[i]
            j += 1
    j

getSellerVolBias(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if sellVolume[i] > buyVolume[i]
            j += 1
    j

getVolBias(lookBack) =>
    float b = 0.0
    float s = 0.0
    for i = 1 to lookBack
        b += buyVolume[i]
        s += sellVolume[i]
    b > s

getSignalBuyerBias(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if signal[i] > signalBiasValue
            j += 1
    j

getSignalSellerBias(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if signal[i] < ( 0.0 - signalBiasValue )
            j += 1
    j

getSignalNoBias(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if signal[i] < signalBiasValue and signal[i] > ( 0.0 - signalBiasValue )
            j += 1
    j

getPriceRising(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if close[i] > close[i + 1]
            j += 1
    j


getPriceFalling(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if close[i] < close[i + 1] 
            j += 1
    j

getRangeNarrowing(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if intrabarRange[i] < intrabarRange[i + 1] 
            j+= 1
    j

getRangeBroadening(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if intrabarRange[i] > intrabarRange[i + 1] 
            j+= 1
    j

bool isNegativeSignalReversal = signalSlope < 0.0 and signalSlope[1] > 0.0
bool isNegativeMacdReversal = macdSlope < 0.0 and macdSlope[1] > 0.0

bool isPositiveSignalReversal = signalSlope > 0.0 and signalSlope[1] < 0.0
bool isPositiveMacdReversal = macdSlope > 0.0 and macdSlope[1] < 0.0

bool hasBearInversion = signalSlope > 0.0 and macdSlope < 0.0
bool hasBullInversion = signalSlope < 0.0 and macdSlope > 0.0

bool hasSignalBias = math.abs(signal) >= signalBiasValue
bool hasNoSignalBias = signal < signalBiasValue and signal > ( 0.0 - signalBiasValue )

bool hasSignalBuyerBias = hasSignalBias and signal > 0.0
bool hasSignalSellerBias = hasSignalBias and signal < 0.0

bool hasPositiveMACDBias = macd > macdBiasValue
bool hasNegativeMACDBias = macd < ( 0.0 - macdBiasValue )

bool hasBullAntiPattern = ta.crossunder(macd, signal)
bool hasBearAntiPattern = ta.crossover(macd, signal)

bool hasSignificantBuyerVolBias = buyVolume > ( sellVolume * 1.5 )
bool hasSignificantSellerVolBias = sellVolume > ( buyVolume * 1.5 )

// 393.60 Profit 52.26% 15m
if ( hasBullInversion and rsiSlope > 1.5 and volume > 300000.0 )
    strategy.entry("15C1", strategy.long, qty=10.0)
strategy.exit("TPS", "15C1", limit=strategy.position_avg_price + takeProfit, stop=strategy.position_avg_price - stopLoss)

// 356.10 Profit 51,45% 15m
if ( getVolBias(shortLookBack) == false and rsiSlope > 3.0 and signalSlope > 0)
    strategy.entry("15C2", strategy.long, qty=10.0)
strategy.exit("TPS", "15C2", limit=strategy.position_avg_price + takeProfit, stop=strategy.position_avg_price - stopLoss)

// 124 Profit 52% 15m
if ( rsiSlope < -11.25 and macdSlope < 0.0 and signalSlope < 0.0)
    strategy.entry("15P1", strategy.short, qty=10.0)
strategy.exit("TPS", "15P1", limit=strategy.position_avg_price - takeProfit, stop=strategy.position_avg_price + stopLoss)

// 455.40 Profit 49% 15m
if ( math.abs(math.abs(macd) - math.abs(signal)) < .1 and buyVolume > sellVolume and hasBullInversion)
    strategy.entry("15P2", strategy.short, qty=10.0)
strategy.exit("TPS", "15P2", limit=strategy.position_avg_price - takeProfit, stop=strategy.position_avg_price + stopLoss)
```

> Detail

https://www.fmz.com/strategy/442002

> Last Modified

2024-02-18 15:27:21
