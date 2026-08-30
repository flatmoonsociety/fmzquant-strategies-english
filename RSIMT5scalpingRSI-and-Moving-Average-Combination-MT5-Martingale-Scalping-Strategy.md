
> Name

MT5 Martingale scaling strategy RSI-and-Moving-Average-Combination-MT5-Martinale-Scalping-Strategy combined with double moving average and RSI
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/edfdf8b89946b147b8d47896dd1b56ce81242c6f903d415366981e86afbc28bd.png)
[trans]

## Overview
This strategy comprehensively uses a combination of double moving average indicators and relative strength index (RSI) indicators to achieve high-frequency scalping transactions, and combines the Martingale principle of adding positions to control the overall risk level of the strategy.
## Strategy Principle
1. This strategy first uses the stoch indicator to draw a custom oscillator, set the parameter oscillatorPeriod to 5, and set the upper and lower thresholds k1 and k2 to build a buying and selling consolidation area. When the stochastic indicator value enters the consolidation area, it indicates that a reversal opportunity may exist.
2. Secondly, combine the RSI indicator to determine overbought and oversold conditions. The RSI indicator can effectively identify when the market breaks through upper and lower limits. This strategy sets the overbought line of RSI to 70 and the oversold line to 30.
3. Furthermore, this strategy also introduces the trendActivity factor as the main trend filter. When the stochastic indicator and RSI meet the reversal conditions at the same time, it will also be checked whether the main trend is still active enough to avoid losses due to false breakthroughs that shock the market.
4. Finally, this strategy uses the classic Martingale adding principle to control the overall risk. By dynamically adjusting the number of trading lots, you can add positions when you first open a position with a loss to achieve breakeven and control the maximum drawdown.
## Strategic advantage analysis
1. The introduction of RSI indicator can effectively identify overbought and oversold phenomena and assist in judging the timing of reversal.
2. Set the oscillator to determine the buying and selling consolidation area, which can filter out some false breakthrough signals.
3. Set up the main trend filter to avoid losses in volatile market conditions.
4. Martingale's position increase effectively controls the maximum retracement of the strategy, which is the key to sustainable profitability of the strategy. 
## Risk Analysis
1. Under abnormal market conditions, the RSI indicator may fail, leading to errors in overbought and oversold judgments. Special attention should be paid to this risk.
2. Improper oscillator parameter settings may also lead to excessive filtering of signals or identification of false breakthroughs. This requires parameter optimization based on historical market data.
3. Martingale’s increased position will lead to cascading losses under certain circumstances. If the number of steps to add a position is too large, it will lead to a significant risk of account failure.
4. This strategy has only been verified on the 15-minute period GBPUSD currency pair data. There may be data fitting risks in other markets and other cycles.

## Optimization direction
1. Optimize RSI parameters and find parameters more suitable for the current market environment.
2. Test and optimize the parameters of the oscillator so that the buying and selling consolidation area can be determined more accurately. 
3. Add stop loss logic. You can proactively stop losses after the losses reach a certain level, effectively controlling single losses.
4. Optimize the setting rules of the main trend filter to prevent missing reversal opportunities. 
5. Test different position increase range settings. It is necessary to ensure that the increase in position will not be too large and lead to rapid losses.
## Summarize
This strategy comprehensively uses the dual moving average indicator, RSI indicator and custom oscillator to judge the phenomenon of short-term breakthroughs in the upper and lower limits, and supplements it with the main trend filter to avoid false breakthroughs, thereby conducting efficient scalping transactions. At the same time, the classic Martingale adding principle is introduced to control the overall risk level. After parameter optimization and strict risk management, this strategy is expected to obtain stable returns.

|| 

## Overview  

The strategy is named "RSI and Moving Average Combination MT5 Martingale Scalping Strategy". It combines the double moving average indicator and the Relative Strength Index (RSI) indicator to implement high-frequency scalping trading, while incorporating the Martingale position averaging principle to control the overall risk level of the strategy.  

## Strategy Logic   

1. The strategy first uses the stoch indicator to draw a custom oscillator with the parameter oscillatorPeriod set to 5, and sets upper and lower thresholds k1 and k2 to build the consolidation area. When the stochastic indicator value enters the consolidation area, it indicates that there may be reversal opportunities.  

2. Next, the RSI indicator is incorporated to identify overbought and oversold phenomena. The RSI indicator can effectively identify the timing of market penetration of upper and lower limits. This strategy sets the overbought line of RSI at 70 and the oversold line at 30.   

3. In addition, the strategy also introduces the trendActivity factor as the main trend filter. When the stochastic indicator and RSI meet the reversal conditions at the same time, it also checks whether the main trend is still active enough to avoid losses due to false breakouts in the shock market.   

4. Finally, the strategy uses the classic Martingale position averaging principle to control overall risk. By dynamically adjusting the trading volume, additional positions are placed when the initial position is at a loss in order to achieve breakeven and thereby control maximum drawdown.  

## Advantage Analysis  

1. The incorporation of the RSI indicator can effectively identify overbought and oversold phenomena to assist in judging reversal timing.  

2. Setting the oscillator to determine the consolidation area can filter out some false breakout signals.   

3. Setting the main trend filter avoids losses in volatile markets.   

4. Martingale position averaging effectively controls the maximum drawdown of the strategy and is key to sustainable profitability.    

## Risk Analysis   

1. Under abnormal market conditions, the RSI indicator may fail and cause misjudgment of overbought and oversold conditions. This risk should be especially noted.  

2. Improper parameter settings of the oscillator may also lead to excessive signal filtering or identification of false breakouts. This requires parameter optimization based on historical market data.   

3. Martingale position averaging will lead to cascading losses under certain environments. If the number of additional lots is too large, it will pose a major risk of account depletion.   

4. The strategy has only been verified on 15-minute GBPUSD currency pair data. There may be data fitting risks in other markets and other periods.  

## Optimization Directions  

1. Optimize the parameters of the RSI to find parameters more suitable for the current market environment.   

2. Test and optimize the parameters of the oscillator so that it can judge the consolidation area more accurately.     

3. Add stop loss logic. Actively stop losses when losses reach a certain level to effectively control single losses.   

4. Optimize the setting rules of the main trend filter to prevent missing reversal opportunities.   

5. Test different additional position sizing settings. Need to ensure that the additional amount is not too large to cause rapid loss.   

## Summary  

This strategy combines the double moving average indicator, RSI indicator and custom oscillator to judge the upper and lower limit breakthrough phenomena in the short term, and uses the main trend filter to avoid false breakouts for efficient scalping trading. At the same time, the classic Martingale position averaging principle is introduced to control the overall risk level. The strategy has the potential to generate stable returns after parameter optimization and rigorous risk management.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|70|RSI Overbought Threshold|
|v_input_int_2|30|RSI Oversold Threshold|
|v_input_int_3|5|Period for oscillator|
|v_input_float_1|0.2|K1 for oscillator's zone|
|v_input_float_2|0.5|K2 for oscillator's zone|
|v_input_float_3|true|Main Trend filter|
|v_input_float_4|0.1|Trend filter decrease per order|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-24 00:00:00
end: 2023-11-30 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © cloudofw

//@version=5
strategy("F2.2 Martingale Scalping Strategy", overlay=true)

// Input parameters
rsiOverbought = input.int(70, "RSI Overbought Threshold")
rsiOversold = input.int(30, "RSI Oversold Threshold")
oscillatorPeriod = input.int(5, "Period for oscillator")
k1 = input.float(0.2, "K1 for oscillator's zone")
k2 = input.float(0.5, "K2 for oscillator's zone")
trendActivity = input.float(1.0, "Main Trend filter", minval=0.1)
decreasePerOrder = input.float(0.1, "Trend filter decrease per order", minval=0.01)

// Calculate custom oscillator and RSI
oscillator = ta.stoch(close, high, low, oscillatorPeriod)
rsiValue = ta.rsi(close, 14)

zoneHigh = 100 - k1 * 100
zoneLow = k2 * 100

// Entry conditions
longCondition = oscillator < zoneLow and trendActivity > 0 and rsiValue < rsiOversold
shortCondition = oscillator > zoneHigh and trendActivity > 0 and rsiValue > rsiOverbought

// Martingale logic
var lot_multiplier = 1.0
var last_lot_size = strategy.equity * 0.01
var trade_1_profit = 0.0
if (strategy.position_size != 0)
    lot_multiplier := last_lot_size / strategy.position_size < 1.5 ? lot_multiplier * 1.5 : 1.0
    trade_1_profit := strategy.grossprofit
else
    lot_multiplier := 1.0
    trade_1_profit := 0.0
lot_size = strategy.equity * 0.01 * lot_multiplier + trade_1_profit
last_lot_size := lot_size

// Trading logic
if longCondition and strategy.position_size == 0
    strategy.entry("Long", strategy.long)
    
if shortCondition and strategy.position_size == 0
    strategy.entry("Short", strategy.short)

// Exit conditions
if longCondition == false and strategy.position_size > 0
    strategy.close("Long")

if shortCondition == false and strategy.position_size < 0
    strategy.close("Short")

// Indicators on chart
plotshape(series=longCondition, title="Buy Entry", location=location.belowbar, color=color.green, style=shape.labelup, text="Buy")
plotshape(series=shortCondition, title="Sell Entry", location=location.abovebar, color=color.red, style=shape.labeldown, text="Sell")

plot(oscillator, color=color.blue, title="Oscillator")
hline(zoneHigh, "Upper Zone", color=color.red)
hline(zoneLow, "Lower Zone", color=color.green)

```

> Detail

https://www.fmz.com/strategy/433960

> Last Modified

2023-12-01 17:56:56
