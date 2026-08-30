
> Name

Adaptive-Moving-Average-and-Weighted-Moving-Average-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/924407fb2b24d0f126.png)
[trans]
### Overview
This strategy implements trading signals based on the Adaptive Moving Average indicator (AIOMA) and the Weighted Moving Average indicator (WMA). It generates buy and sell signals through the crossover of AIOMA and WMA.
### Policy name
AIOMA-WMA adaptive crossover strategy
### Strategy Principles
The strategy mainly includes the following parts:
1. AIOMA indicator calculation
- Specify the length parameter to calculate a series of exponential moving averages (EMA)
   - Smoothly connect these EMAs to form a smooth sequence
   - The final AIOMA is the EMA of the last smoothed value
2. WMA indicator calculation
- Specify length parameters and calculate WMA
3. Trading signal generation
- When WMA crosses AIOMA, a buy signal is generated
   - When WMA crosses below AIOMA, a sell signal is generated
4. Transaction logic
- On buy signal, enter a long position
   - On a sell signal, enter a short position
   - When closing a position signal, close the position in the corresponding direction
### Strategic Advantages
1. Using two different types of moving averages can improve the accuracy of trading signals
2. AIOMA can reduce false signals through multiple exponential smoothing
3. As the main indicator, WMA is more sensitive to price changes and can capture trends early.
4. Simple transaction logic, easy to understand and implement
### Strategy Risk
1. Multiple EMA smoothing can cause excessive lag
2. WMA is susceptible to short-term price fluctuations and produces false signals.
3. Failure to consider stop loss logic may lead to larger losses
Risks can be reduced by appropriately optimizing parameters, setting stop loss points, or combining filtering with other indicators.
### Strategy optimization direction
1. Test combinations of different length parameters to find the best parameters
2. Trigger stop loss orders simultaneously with buy/sell signals
3. Combine with market volatility indicators to filter out false signals
4. Add position management strategies
### Summarize
This strategy integrates the advantages of AIOMA and WMA and generates trading signals through crossover. Compared with a single moving average, the signal quality can be improved. Through further improvements such as parameter optimization, stop loss strategies and volatility filtering, it can become a stable and reliable trading system.
||

## Overview

This strategy generates trading signals based on the Adaptive Indicator for Moving Averages (AIOMA) and the Weighted Moving Average (WMA) indicators. It produces buy and sell signals based on the crossovers between AIOMA and WMA.  

### Strategy Name

AIOMA-WMA Adaptive Crossover Strategy

### Strategy Logic

The strategy includes the following main components:

1. AIOMA Indicator Calculation

   - Calculate a series of Exponential Moving Averages (EMA) with specified length 
   - Chain these EMAs to create smoothed values  
   - The final AIOMA is an EMA of the last smoothed value

2. WMA Indicator Calculation

   - Calculate WMA with specified length

3. Signal Generation

   - Buy signal when WMA crosses above AIOMA
   - Sell signal when WMA crosses below AIOMA

4. Trading Logic

   - Enter long position on buy signal
   - Enter short position on sell signal  
   - Close position on reverse crossover signals

### Advantages

1. Using two different types of moving averages improves signal accuracy 
2. AIOMA reduces false signals through multiple exponential smoothings
3. WMA as the main indicator reacts faster to price changes to capture trends early  
4. Simple trading logic, easy to understand and implement

### Risks

1. Excessive lagging due to multiple EMA smoothings  
2. WMA prone to wrong signals from short-term price fluctuations
3. No stop loss logic, can lead to large losses

Can reduce risks through parameter optimization, adding stop loss, filtering with other indicators etc.

### Enhancement Areas

1. Test different parameter combinations to find optimal values
2. Trigger stop loss orders together with entry signals 
3. Filter signals using volatility indicators 
4. Incorporate position sizing strategies

### Conclusion

This strategy combines the strengths of AIOMA and WMA by using crossovers to generate trading signals. Compared to single moving averages, it improves signal quality. Further refinements like parameter optimization, stop loss strategies, volatility filtering etc. can make it a robust trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|AIOMA Length|
|v_input_2|21|WMA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SDTA

//@version=5
strategy("AIOMA-WMA Strategy", overlay=true)

// Parametreler
aioma_length = input(14, "AIOMA Length")
wma_length = input(21, "WMA Length")

// AIOMA hesaplama
length1 = aioma_length
ema1 = ta.ema(close, length1)
length2 = aioma_length
ema2 = ta.ema(ema1, length2)
length3 = aioma_length
ema3 = ta.ema(ema2, length3)
length4 = aioma_length
ema4 = ta.ema(ema3, length4)
aioma = ta.ema(ema4, aioma_length)

// WMA hesaplama
wma = ta.wma(close, wma_length)

// Kesişim kontrolü
cross_up = ta.crossover(wma, aioma)
cross_down = ta.crossunder(wma, aioma)

// İşlem fonksiyonu
enterTrade(dir, price, signalText, color) =>
    if dir
        strategy.entry("Enter", strategy.long)
        label.new(x = bar_index, y = price, text = signalText, color = color, textcolor = color, style = label.style_label_up, size = size.small, tooltip = "Entry Signal")
    else if not dir
        strategy.entry("Exit", strategy.short)
        label.new(x = bar_index, y = price, text = signalText, color = color, textcolor = color, style = label.style_label_down, size = size.small, tooltip = "Exit Signal")

// Long pozisyon girişi
if cross_up
    enterTrade(true, low, "Buy Signal", color.green)

// Short pozisyon girişi
if cross_down
    enterTrade(false, high, "Sell Signal", color.red)

// Pozisyon kapatma
if cross_up and strategy.position_size > 0
    strategy.close("Enter")
if cross_down and strategy.position_size < 0
    strategy.close("Exit")

// Grafiğe plot
plot(aioma, color=color.blue, linewidth=2, title="AIOMA")
plot(wma, color=color.red, linewidth=2, title="WMA")

```

> Detail

https://www.fmz.com/strategy/439735

> Last Modified

2024-01-23 14:13:55
