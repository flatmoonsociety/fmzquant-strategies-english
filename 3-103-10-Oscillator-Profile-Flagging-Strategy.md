
> Name

3-10 Oscillator Profile Flagging Strategy 3-10-Oscillator-Profile-Flagging-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/34755f835a61f2c2a797ad3d786590cf49eb3fb9048fdd990853f5d762f41422.png)
[trans]
### Overview
The 3-10 oscillator contour marking strategy calculates the difference between the 3-day and 10-day simple moving averages as the MACD indicator, and combines the analysis of trading volume to determine the strength of market buying and selling orders, thereby generating trading signals. The strategy also combines key price areas, volume characteristics, and MACD reversals to identify entry and exit opportunities.
### Strategy Principles
The core indicator of this strategy is MACD, which consists of a fast moving average and a slow moving average. The fast line is the 3-day simple moving average, and the slow line is the 10-day simple moving average. The difference between them forms the MACD histogram. When the fast line breaks through the slow line from below, it means that the buying power is strengthened and a buy signal is generated; conversely, when the fast line falls from above and breaks through the slow line, the selling power is strengthened and a sell signal is generated.
In addition, this strategy combines the relationship between the buying volume and selling volume of each K line to determine the relative strength of the market's buying and selling orders. The specific method is: buying volume = trading volume x (closing price - lowest price) ÷ (highest price - lowest price); selling volume = trading volume x (highest price - closing price) ÷ (highest price - lowest price). If the buying volume is significantly greater than the selling volume, it means that the K-line ended with a strong buying order, which is a buying signal.
By combining the MACD indicator and trading volume analysis, this strategy can effectively determine the market's supply and demand relationship and the pending direction. At the same time, the strategy will also verify whether the price is in a key area, whether MACD is effectively reversed, and whether the difference in buying and selling volume is large enough, etc., thereby filtering out some noise from impulsive operations and ensuring high probability and efficient entry.
### Advantage Analysis
- Use MACD indicator to determine the direction of market momentum
- Analysis of trading volume differences to determine the strength of buying and selling orders
-Multiple condition screening to ensure high probability operation
- Use stop-profit and stop-loss strategies to control risks
The biggest advantage of this strategy is that it fully combines the judgment of market supply and demand. The MACD columnar line can effectively determine the balance of buying and selling orders and the direction of market momentum; the analysis of trading volume differences can clearly identify the dominant force of buying and selling orders. At the same time, the strategy sets multiple conditions for review to avoid chasing ups and downs and ensuring a higher probability of profit. In addition, the strategy's built-in stop-profit and stop-loss mechanism can also limit single losses.
### Risk Analysis
- Risk of MACD failure. When the market is choppy or trading flat, MACD may generate false signals.
- Volume invalidation risk. There may be a phenomenon of increasing trading volume in the market, in which case the accuracy of trading volume analysis will be reduced.  
- Parameter optimization is difficult. This strategy contains multiple parameters, which is difficult to optimize and is not suitable for investors with weak parameter adjustment capabilities.
The above risks can be avoided by the following methods: accurately judge the main market trends and avoid using this strategy in volatile trading; pay attention to market information and identify situations where trading volume has been artificially boosted; adjust parameters carefully and learn from the advice of professional institutions.
### Optimization direction
This strategy can be optimized from the following aspects:
- Use indicators such as KD and Bollinger Bands to replace or cooperate with MACD to improve the accuracy of judgment.
- Add a position management mechanism to allow dynamic adjustment of strategy parameters
- Optimize take profit and stop loss points to achieve higher single profit
- Run in multiple time periods to improve stability
In summary, it can be seen that this strategy has a large room for optimization, and investors can make appropriate adjustments and improvements according to their own circumstances and market environment to make the strategy more effective.
### Summarize
The 3 10 oscillator contour marking strategy successfully integrates the ideas of MACD analysis, volume comparison and multiple condition filtering verification. It has a strong ability to judge the relationship between supply and demand and the direction of market momentum, and has a built-in stop-profit and stop-loss mechanism to control risks. This strategy has a large space for optimization and broad application prospects, and is worthy of investors' focus and in-depth study.
||

### Overview

The 3 10 Oscillator Profile Flagging strategy generates trading signals by calculating the difference between 3-day and 10-day simple moving averages as the MACD indicator and combining volume analysis to determine the strength of buyers and sellers in the market. The strategy also incorporates confirmation of entry and exit opportunities using key price areas, volume characteristics, and MACD indicator reversals.

### Strategy Principle 

The core indicator of this strategy is MACD, which consists of a fast moving average line and a slow moving average line. The fast line is a 3-day simple moving average and the slow line is a 10-day simple moving average. The difference between them forms the MACD histogram. When the fast line crosses above the slow line from below, it represents strengthening buying power and generates a buy signal. Conversely, when the fast line crosses below the slow line from above, selling power is strengthening and a sell signal is generated.

In addition, the strategy incorporates analysis of the relative strength of buying and selling volume based on the size relationship between buying volume and selling volume of each candlestick. The specific method is: Buying volume = Volume x (Close - Low) ÷ (High - Low); Selling volume = Volume x (High - Close) ÷ (High - Low). If the buying volume is significantly greater than the selling volume, it means the candlestick closes with relatively strong buying power, which is a buy signal. 

By combining the MACD indicator and volume analysis, the strategy can effectively determine the supply and demand relationship and the pending direction in the market. At the same time, the strategy also verifies conditions such as whether the price is in a key area, whether the MACD has an effective reversal, and whether the difference between buying and selling volume is large enough, so as to filter out some impulsive noise and ensure high-probability and high-efficiency entry.

### Advantage Analysis

- Use MACD indicator to judge market pending direction  
- Volume difference analysis to determine the strength of buyers and sellers
- Multi-condition screening ensures high-probability operation 
- Adopt stop profit and stop loss strategy to control risks

The biggest advantage of this strategy is that it fully incorporates judgment of market supply and demand relationship. The MACD histogram can effectively determine the contrast between buying and selling power and the pending direction in the market; volume difference analysis can clearly identify the dominant power between buyers and sellers. At the same time, the strategy sets multiple conditions for review to avoid chasing rises and beating declines, ensuring a relatively high probability of profit. In addition, the built-in stop profit and stop loss mechanism of the strategy can also limit single losses.

### Risk Analysis

- MACD failure risk. When the market fluctuates or consolidates in a flat pattern, the MACD may generate false signals.
- Volume failure risk. There may be market manipulation to drive up trading volume, which would reduce the accuracy of volume analysis.
- Difficulty of parameter optimization. The strategy contains multiple parameters that are difficult to optimize, making it unsuitable for investors with relatively weak parameter tuning capabilities.

The above risks can be avoided by: accurately determining the main trend of the market to avoid using this strategy during market fluctuation; paying attention to market information to identify artificially inflated trading volumes; adjusting parameters carefully, or seeking advice from professionals.  

### Optimization Directions

The strategy can be optimized in the following aspects:

- Use indicators like KD, Bollinger Bands etc. to replace or assist MACD and improve judgment accuracy  
- Add position management mechanisms for dynamic parameter adjustment  
- Optimize stop profit and stop loss points for higher single profit  
- Run on multiple timeframes to improve stability  

In summary, it can be seen that there is ample room for optimizing this strategy. Investors can make appropriate adjustments and improvements according to their own situation and market conditions to achieve better strategy effectiveness.  

### Summary  

The 3 10 Oscillator Profile Flagging strategy successfully integrates the ideas of MACD analysis, volume comparison, and multi-condition filtering verification. It has strong capabilities in determining supply-demand relationships and market pending directions, while controlling risks through built-in stop profit and stop loss mechanisms. The strategy has large optimization space and broad application prospects that are worth key consideration and in-depth research for investors.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.26|Signal Bias|
|v_input_2|0.8|MACD Bias|
|v_input_3|3|Short LookBack|
|v_input_4|10|Long LookBack|
|v_input_5|0.75|Take Profit|
|v_input_6|0.5|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("3 10 Oscillator Profile Flagging", shorttitle="3 10 Oscillator Profile Flagging", overlay=true)

signalBiasValue = input(title="Signal Bias", defval=0.26)
macdBiasValue = input(title="MACD Bias", defval=0.8)
shortLookBack = input( title="Short LookBack", defval=3)
longLookBack = input( title="Long LookBack", defval=10)
takeProfit = input( title="Take Profit", defval=0.75)
stopLoss = input( title="Stop Loss", defval=0.5)

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
//plot(macdSlope, color=color.red, title="Total Volume")
//plot(signalSlope, color=color.green, title="Total Volume")
intrabarRange = high - low

getLookBackSlope(lookBack) => signal - signal[lookBack]
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
    float b = 0
    float s = 0
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
        if signal[i] < ( 0 - signalBiasValue )
            j += 1
    j

getSignalNoBias(lookBack) =>
    j = 0
    for i = 1 to lookBack
        if signal[i] < signalBiasValue and signal[i] > ( 0 - signalBiasValue )
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

bool isNegativeSignalReversal = signalSlope < 0 and signalSlope[1] > 0
bool isNegativeMacdReversal = macdSlope < 0 and macdSlope[1] > 0

bool isPositiveSignalReversal = signalSlope > 0 and signalSlope[1] < 0
bool isPositiveMacdReversal = macdSlope > 0 and macdSlope[1] < 0

bool hasBearInversion = signalSlope > 0 and macdSlope < 0
bool hasBullInversion = signalSlope < 0 and macdSlope > 0

bool hasSignalBias = math.abs(signal) >= signalBiasValue
bool hasNoSignalBias = signal < signalBiasValue and signal > ( 0 - signalBiasValue )

bool hasSignalBuyerBias = hasSignalBias and signal > 0
bool hasSignalSellerBias = hasSignalBias and signal < 0

bool hasPositiveMACDBias = macd > macdBiasValue
bool hasNegativeMACDBias = macd < ( 0 - macdBiasValue )

bool hasBullAntiPattern = ta.crossunder(macd, signal)
bool hasBearAntiPattern = ta.crossover(macd, signal)

bool hasSignificantBuyerVolBias = buyVolume > ( sellVolume * 1.5 )
bool hasSignificantSellerVolBias = sellVolume > ( buyVolume * 1.5 )

// 7.48 Profit 52.5% 
if ( hasSignificantBuyerVolBias and getPriceRising(shortLookBack) == shortLookBack  and getBuyerVolBias(shortLookBack) == shortLookBack and hasPositiveMACDBias and hasBullInversion)
    strategy.entry("Short1", strategy.short, qty=10)
strategy.exit("TPS", "Short1", limit=strategy.position_avg_price - takeProfit, stop=strategy.position_avg_price + stopLoss)

// 32.53 Profit 47.91%
if ( getPriceFalling(shortLookBack) and (getVolBias(shortLookBack) == false) and signalSlope < 0 and hasSignalSellerBias)
    strategy.entry("Long1", strategy.long, qty=10)
strategy.exit("TPS", "Long1", limit=strategy.position_avg_price + takeProfit, stop=strategy.position_avg_price - stopLoss)
```

> Detail

https://www.fmz.com/strategy/442016

> Last Modified

2024-02-18 16:17:26
