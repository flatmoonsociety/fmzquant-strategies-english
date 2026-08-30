
> Name

MACD-and-RSI-Based-Trend-Following-Reversal-Strategy MACD-and-RSI-Based-Trend-Following-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16057189a7397864fe1.png)
 [trans]

### Overview
This strategy comprehensively uses three indicators, MACD, EMA and RSI, to achieve trend following and reversal trading. When MACD crosses the signal line upwards and the closing price is higher than the EMA moving average, a buy signal is generated; when MACD falls below the signal line and the closing price is lower than the EMA moving average, a sell signal is generated to capture the trend; at the same time, when the RSI reaches the overbought and oversold area, a reversal trade is performed.
### Strategy Principles
1. Calculate MACDdiffs and EMA.
    
```
    fastMA = ema(close, fast)  
    slowMA = ema(close, slow)
    macd = fastMA - slowMA
    signal = sma(macd, 9)
    ema = ema(close, input(200))
    
```

2. Generate a buy signal: MACD difference (macd-signal) crosses the 0 axis and the closing price is higher than the EMA moving average.
    
```
    delta = macd - signal 
    buy_entry= close>ema and delta > 0
    
```

3. Generate a sell signal: the MACD difference falls below the 0 axis and the closing price is below the EMA moving average.   
    
```
    sell_entry = close<ema and delta<0 
    
```

4. When RSI enters the overbought and oversold zone, perform a reversal trade.
    
```
    if (rsi > 70 or rsi < 30)
        reversal := true
    
```

### Advantage Analysis
1. Combining trend following and reversal trading, you can not only track the main trend, but also make profits at reversal points.
2. Use MACD to determine the main trend direction and avoid false breakthroughs. 
3. Use EMA to filter out some noise.
4. The RSI indicator determines the reversal point and enhances the profit margin of the strategy.
### Risk Analysis
1. In a trending market, reversal trading may result in losses.
2. Improper parameter settings will increase transaction frequency and slippage costs.
3. The reversal signal may be delayed and the best entry opportunity may be missed.
Solution:
1. Optimize parameters and find the best parameter combination.
2. Appropriately adjust the RSI threshold for reversal trading.
3. Consider adding a stop loss to limit losses.
### Optimization direction
1. Test EMA moving average parameters of different lengths.
2. Optimize MACD parameters and find the best parameter combination.  
3. Test different reversal RSI thresholds.
4. Consider adding other indicators for combination.
### Summarize
This strategy comprehensively uses MACD, EMA and RSI indicators to achieve an organic combination of trend following and reversal trading. MACD determines the main trend direction, EMA filters out noise, and the RSI indicator captures reversal points. This multi-indicator combination can more accurately judge market trends, while reducing false trades and increasing the probability of profit. Of course, parameter optimization and stop loss management need to be further improved to reduce unnecessary losses and make the strategy more robust. In general, the strategy framework is reasonable and is expected to achieve stable returns.
||


### Overview

This strategy combines MACD, EMA and RSI indicators to implement trend following and reversal trading. It generates buy signals when MACD goes up through signal line and close price is above EMA; and sell signals when MACD falls below signal line and close price is below EMA to capture trends. Meanwhile, it trades reversals when RSI reaches overbought or oversold levels.

### Strategy Logic

1. Calculate MACD diffs and EMA.

    
```
    fastMA = ema(close, fast)
    slowMA = ema(close, slow) 
    macd = fastMA - slowMA
    signal = sma(macd, 9)
    ema = ema(close, input(200))
    
```

2. Generate buy signal: MACD diff (macd - signal) goes above 0 and close price is above EMA.

    
```
    delta = macd - signal
    buy_entry= close>ema and delta > 0 
    
```

3. Generate sell signal: MACD diff goes below 0 and close price is below EMA.

    
```
    sell_entry = close<ema and delta<0
    
```

4. Trade reversals when RSI reaches overbought or oversold levels.

    
```
    if (rsi > 70 or rsi < 30)
        reversal := true
    
```

### Advantage Analysis

1. Combine trend following and reversal trading to profit from both trends and reversals.  
2. Use MACD to judge trend directions and avoid false breakouts.
3. Filter noise with EMA.  
4. Enhance profitability with RSI for reversal trades.

### Risk Analysis

1. Reversal trades may incur losses in strong trending markets.  
2. Improper parameter tuning may increase trading frequency and slippage costs.
3. Reversal signals may have some lag, missing best entry prices.

Solutions:

1. Optimize parameters to find best combination.
2. Adjust reversal RSI thresholds properly.  
3. Consider adding stop loss to control losses.

### Optimization Directions 

1. Test EMA lengths.  
2. Optimize MACD parameters.
3. Test different RSI reversal thresholds.  
4. Consider combining with other indicators.

### Summary

This strategy combines MACD, EMA and RSI to organically implement trend following and reversal trading. MACD judges trend directions, EMA filters noise, and RSI captures reversal points. Such multi-indicator combination can better determine market movements, improving profitability while reducing false signals. Parameter optimization and stop loss management could be further improved to reduce unnecessary losses. Overall, this is a solid strategy framework with potential for steady profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|v_input_1|
|v_input_2|14|v_input_2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-17 00:00:00
end: 2023-12-17 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mbuthiacharles4

//Good with trending markets
//@version=4
strategy("CHARL MACD EMA RSI")

fast = 12, slow = 26
fastMA = ema(close, fast)
slowMA = ema(close, slow)
macd = fastMA - slowMA
signal = sma(macd, 9)

ema = ema(close, input(200))

rsi = rsi(close, input(14))
//when delta > 0  and close above ema buy

delta = macd - signal

buy_entry= close>ema and delta > 0
sell_entry = close<ema and delta<0 
var bought = false
var sold = false
var reversal = false
if (buy_entry and bought == false and rsi <= 70) 
    strategy.entry("Buy",true , when=buy_entry)
    bought := true
    
strategy.close("Buy",when= delta<0 or rsi > 70)
if (delta<0 and bought==true)
    bought := false

//handle sells

if (sell_entry and sold == false and rsi >= 30)
    strategy.entry("Sell",false , when=sell_entry)
    sold := true

strategy.close("Sell",when= delta>0 or rsi < 30)
if (delta>0 and sold==true)
    sold := false
    
if (rsi > 70 or rsi < 30)
    reversal := true
    placing = rsi > 70 ? high :low
    label.new(bar_index, placing, style=label.style_flag, color=color.blue, size=size.tiny)
if (reversal == true)
    if (rsi < 70 and sold == false and delta < 0)
        strategy.entry("Sell",false , when= delta < 0)
        sold := true
        reversal := false
    else if (rsi > 30 and bought == false and delta > 0)
        strategy.entry("Buy",true , when= delta > 0)
        bought := true
        reversal := false


```

> Detail

https://www.fmz.com/strategy/435775

> Last Modified

2023-12-18 17:53:38
