
> Name

Golden-Cross-Death-Cross-Long-term-Multi-factor-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11ecc5ba515ff6dfe2a.png)
[trans]
## Overview
This strategy is a long-term multi-factor strategy. It combines the three indicators of moving average, RSI and ATR to determine when the market enters the undervalued area and generates a buy signal. It is a long-term holding strategy that mainly pursues stable returns.
## Strategy Principle
When the fast-cycle moving average crosses the slow-cycle moving average, forming a golden cross signal, and at the same time, when the RSI indicator is below the overbought zone, it is considered that the market is undervalued and a buy signal is generated. Then set the stop loss and take profit levels according to the ATR indicator, and use fixed take profit and stop loss.
Specifically, the strategy uses the 10-day moving average and the 50-day moving average to form trading signals. A buy signal is generated when the 10-day moving average crosses the 50-day moving average. At the same time, the RSI (14) indicator needs to be below the overbought zone of 70 to avoid buying highs.
After entering the market, set the stop loss and take profit level according to the size of ATR (14). The stop-loss position is when the stock price is lower than the entry price by 1.5 times the ATR; the take-profit position is when the stock price is higher than the entry price by 2 times the ATR.
## Advantage Analysis
This is a long-term multi-factor strategy that combines multiple indicators to judge the market, which can effectively avoid losses caused by false breakthroughs. Specific advantages include:
1. Multi-factor judgment to avoid false breakthroughs and ensure the reliability of buying signals
2. Track the long-term trend and don’t stop losses following short-term fluctuations.
3. Fixed take-profit and stop-loss points to prevent huge losses
4. The indicator parameters are adjustable and can be optimized for different varieties.
5. Simple to implement, easy to understand and operate
## Risk Analysis
As a long-term holding strategy, this strategy also has some risks that need to be noted. The main risk points include:
1. The risk of substantial losses caused by long-term holding. Large losses may occur when encountering long-term market adjustments. A trailing stop can be set to mitigate this.
2. Stop trailing stop loss risk. Fixed stop loss is only set once after entering the market and will not be adjusted subsequently, which may cause the stop loss to be breached. Optimization can be done using dynamic stop loss or trailing stop loss.    
3. The indicator is set too slowly and short-term trading opportunities are missed. The indicator parameters can be appropriately shortened to pursue faster trading frequency.
4. The risk of adding positions along the trend is magnified. You can set the frequency and proportion upper limit of adding positions to control risks.
## Optimization direction
This strategy can be optimized from the following directions:
1. Add a dynamic stop loss mechanism and adjust the stop loss position according to price and volatility
2. Add a mobile take-profit function so that profits can be better locked in
3. Combine with trading volume indicators to avoid low-volume false breakthroughs
4. Optimize indicator parameters to adapt to more varieties
5. Increase the position increase mechanism and increase positions appropriately at advantageous positions
## Summarize
As a long-term multi-factor Golden Cross and Dead Cross strategy, this strategy combines moving averages, RSI and ATR indicators to generate trading signals based on multi-factor judgments in order to pursue stable returns brought by the long-term trend. It has the characteristics of accurate judgment, clear stop loss and simple implementation. It is a recommended long-term strategy. At the same time, we also need to pay attention to guarding against long-term holding risks and dynamically adjust stop-loss and take-profit strategies. In general, after parameter optimization, this strategy can become one of the effective long-term strategies that generate stable returns.
||

## Overview   

This is a long-term multi-factor strategy that combines moving average, RSI and ATR indicators to identify undervalued market conditions and generate buy signals. It is a long-term holding strategy focused on pursuing steady returns.  

## Strategy Logic

When the fast moving average crosses above the slow moving average, forming a golden cross signal, while the RSI indicator is below the overbought area, the market is considered undervalued and a buy signal is generated. Stop loss and take profit are then set based on the ATR indicator for fixed stop loss/take profit.   

Specifically, the strategy uses 10-day and 50-day moving averages to form trading signals. A buy signal is generated when the 10-day MA crosses above the 50-day MA. At the same time, RSI (14) needs to be below the 70 overbought area to avoid buying at high points.   

After entering the market, stop loss and take profit are set based on the size of ATR (14). The stop loss is set at the price below entry price by 1.5 times ATR; the take profit is set at the price above entry price by 2 times ATR.

## Advantage Analysis

This is a long-term multi-factor strategy that combines multiple indicators to judge market conditions, which can effectively avoid losses caused by false breakouts. The main advantages are:

1. Multi-factor judgment avoids false breakouts and ensures reliability of buy signals  
2. Tracks long-term trends without being stopped out by short-term fluctuations
3. Fixed stop loss/take profit points prevent excessive losses
4. Adjustable indicator parameters allow optimization across different products  
5. Simple to implement, easy to understand and operate
   
## Risk Analysis   

As a long-term holding strategy, the strategy also has some risks to note. The main risk points include:  

1. Large loss risk from long-term holding. May see sizable loss in prolonged consolidation market. Can set up trailing stop loss to mitigate.
2. Stop tracking stop loss risk. Fixed stop loss is only set once after entry, no further adjustment, may get stop loss breached. Can optimize with dynamic stop loss or trailing stop loss.   
3. Indicators too slow, misses short-term trading opportunities. Can shorten indicator parameters appropriately to pursuit higher trading frequency.  
4. Risk magnification from trend following additions. Can set limits on frequency and size of additions to control risk.
   
## Optimization Directions
  
The strategy can be optimized in the following aspects:

1. Add dynamic stop loss mechanism, adjust stop loss based on price and volatility  
2. Add trailing take profit to better lock in profits 
3. Incorporate trading volume indicator to avoid low volume false breakout
4. Optimize indicator parameters to fit more products
5. Add trend following position addition mechanism to moderately add to winning positions  

## Conclusion

As a long-term multi-factor golden cross death cross strategy, it combines moving average, RSI and ATR indicators to generate trading signals based on multi-factor judgments, pursuing steady returns from long-term trends. With the characteristics of accurate judgment, clear stop loss, and simple execution, it is a recommended long-term strategy. At the same time, need to watch out for long holding risks, dynamically adjust stop loss and take profit. Overall, with parameter optimization, the strategy can become an effective long-term strategy to produce steady returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Fast MA Length|
|v_input_2|50|Slow MA Length|
|v_input_3|14|RSI Length|
|v_input_4|70|RSI Overbought Level|
|v_input_5|30|RSI Oversold Level|
|v_input_6|14|ATR Length|
|v_input_7|1.5|Risk Multiplier for SL and TP|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-16 00:00:00
end: 2024-01-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Long Only Multi-Indicator Strategy", shorttitle="LOMIS", overlay=true)

// Inputs
lengthMAFast = input(10, title="Fast MA Length")
lengthMASlow = input(50, title="Slow MA Length")
rsiLength = input(14, title="RSI Length")
rsiOverbought = input(70, title="RSI Overbought Level")
rsiOversold = input(30, title="RSI Oversold Level")
atrLength = input(14, title="ATR Length")
riskMultiplier = input(1.5, title="Risk Multiplier for SL and TP")

// Moving averages
maFast = sma(close, lengthMAFast)
maSlow = sma(close, lengthMASlow)

// RSI
rsi = rsi(close, rsiLength)

// ATR
atr = atr(atrLength)

// Long condition
longCondition = crossover(maFast, maSlow) and rsi < rsiOverbought

// Entering long trades
if (longCondition)
    strategy.entry("Long", strategy.long)
    slLong = close - atr * riskMultiplier
    tpLong = close + atr * riskMultiplier * 2
    strategy.exit("SL Long", "Long", stop=slLong)
    strategy.exit("TP Long", "Long", limit=tpLong)

// Plotting
plot(maFast, color=color.red)
plot(maSlow, color=color.blue)
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiOversold, "Oversold", color=color.blue)

```

> Detail

https://www.fmz.com/strategy/439704

> Last Modified

2024-01-23 11:11:40
