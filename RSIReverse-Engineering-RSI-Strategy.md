
> Name

Reverse-Engineering-RSI-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/169f3667150e464014e.png)
[trans]

## Overview
The Reverse Engineering RSI strategy is a trading strategy based on the RSI indicator. This strategy simulates the calculation process of the RSI indicator and reversely derives the price to generate trading signals.
## Strategy Principle
The core idea of ​​​​this strategy is:
1. Calculate the K value, ExpPer period, AUC rising sequence and ADC falling sequence in the RSI indicator.
2. Calculate nVal in reverse according to RSI parameter settings, ADC, AUC sequence values, etc.
3. Add nVal to the price and calculate nRes in reverse.
4. Compare nRes and the current close price to generate long and short position signals.
Specifically, the strategy first calculates some key parameters in RSI, including K value, ExpPer period, AUC rising sequence and ADC falling sequence. Among them, the K value is the smoothing factor, and ExpPer is twice the RSI parameter setting minus 1.
Then based on these parameters, the strategy works backwards to derive the price. First calculate a key variable nVal, which is equal to (WildPer - 1) * (ADC_ Value / (100 - Value) - AUC).  This formula reverses the calculation process of RSI.
Then nVal is added to the current close price to obtain the reverse engineering price nRes. Finally, if nRes is higher than the current close price, a short position signal is generated, and if nRes is lower than the current close price, a long position signal is generated.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Using the calculation process of the RSI indicator for reverse derivation, the idea is novel and innovative.
2. Reverse engineer prices to generate trading signals that are opposite to the market, which can achieve the effect of short selling and expand the application scope of the strategy.
3. RSI is a mature and commonly used trading indicator with reasonable parameter settings, high reliability and low risk.
4. The strategy idea is clear and easy to understand, has fewer parameters, is easy to implement, and is suitable for the requirements of quantitative trading.
## Risk Analysis
There are also some risks with this strategy:
1. The reverse engineering price is calculated only based on RSI. If RSI sends an incorrect signal, the strategy signal will also be invalid.
2. Reverse signals may be inconsistent with the overall market trend, and you need to pay attention to the general market environment.
3. RSI parameter setting requires experience. If improperly set, it may lead to too frequent transactions or the sending of wrong signals.
4. The risk of reverse short selling is high and strict fund management is required to prevent liquidation.
Risks can be controlled by optimizing RSI parameters, combining with other indicators, and strict fund management.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize RSI parameters WildPer and Value to better adapt to market conditions.
2. Add a stop-loss strategy to lock in profits and reduce losses.
3. Combine with other indicators such as MACD for optimization to make the signal more accurate and reliable.
4. Add position opening filter conditions to avoid unnecessary mistakes in transactions.
5. Optimize the fund management strategy, strictly control the amount of funds in a single transaction, and prevent excessive losses.
## Summarize
The reverse engineering RSI strategy generates trading signals that are opposite to the market by deriving the calculation process of the RSI indicator backwards. This strategy has unique ideas and is innovative. It can realize short selling and expand the scope of strategy application. However, there is also the risk of reverse operation, which requires appropriate optimization and risk control. Overall, this strategy provides new ideas and tools for quantitative trading.
||


## Overview

The Reverse Engineering RSI strategy is a trading strategy based on the RSI indicator. This strategy deduces the price inversely by simulating the calculation process of the RSI indicator to generate trading signals.

## Strategy Logic

The core idea of this strategy is:  

1. Calculate the K value, ExpPer period, AUC rising sequence and ADC falling sequence in the RSI indicator.

2. Inversely calculate nVal based on RSI parameter settings, ADC, AUC sequence values, etc.  

3. Add nVal to the price to inversely deduce nRes.

4. Compare nRes with the current close price to generate long and short signals.

Specifically, the strategy first calculates some key parameters in RSI, including the K value, ExpPer period, AUC rising sequence and ADC falling sequence. Among them, the K value is the smoothing factor, and ExpPer is twice the RSI parameter setting minus 1.

Then, according to these parameters, the strategy deduces the price inversely. First, a key variable nVal is calculated, which equals (WildPer - 1) * (ADC_Value / (100 - Value) - AUC). This formula deduces the RSI calculation process inversely.  

Then add nVal to the current close price to get the reverse engineered price nRes. Finally, if nRes is higher than the current close price, a short signal is generated. If nRes is lower than the current close price, a long signal is generated.

## Advantage Analysis 

The main advantages of this strategy are:

1. It innovatively deduces the RSI calculation process inversely. The logic is novel and innovative to some extent. 

2. The reverse engineered price generates trading signals opposite to the market, which enables short selling to expand the application scope of the strategy.

3. RSI is a mature and commonly used trading indicator with reasonable parameter settings and high reliability and low risk.  

4. The strategy logic is clear and easy to understand. The few parameters make it easy to implement and meet the requirements of quantitative trading.

## Risk Analysis

There are also some risks to this strategy:

1. The reverse engineered price relies solely on RSI calculations. If RSI sends wrong signals, the strategy signals will also fail.

2. The reverse signals may not be consistent with the overall market trend. The overall environment needs attention.

3. RSI parameter setting requires experience. Improper settings may lead to over-frequent trading or wrong signals. 

4. Short selling with reverse operations has high risks. Strict money management is required to prevent account blowups.

The risks can be controlled by optimizing RSI parameters, combining other indicators, and strict money management.

## Optimization Directions

The strategy can be optimized in the following aspects:  

1. Optimize the RSI parameters WildPer and Value to better adapt to market conditions.

2. Add stop loss strategies to lock in profits and reduce losses.  

3. Combine with other indicators like MACD to generate more accurate and reliable signals.

4. Add open position filters to avoid unnecessary losing trades.  

5. Optimize money management strategies to strictly control the capital per trade to prevent losses beyond affordable range.

## Conclusion  

The Reverse Engineering RSI strategy generates trading signals opposite to the market by deducing the RSI calculation process inversely. The strategy has unique logic and certain innovation, enabling short selling to expand its application scope. But there are also risks of reverse operations that need proper optimization and risk control. Overall, the strategy provides new ideas and tools for quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Value|
|v_input_2|14|WildPer|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-21 00:00:00
end: 2023-11-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 25/10/2017
// The related article is copyrighted material from
// Stocks & Commodities.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Reverse Engineering RSI, by Giorgos Siligardos", overlay = true)
Value = input(50, minval=1)
WildPer = input(14,minval=1)
reverse = input(false, title="Trade reverse")
ExpPer = 2 * WildPer - 1
K = 2 / (ExpPer + 1)
AUC = iff(close > close[1], K * (close - close[1]) + (1 - K) * nz(AUC[1], 1), (1-K) * nz(AUC[1], 1))
ADC = iff(close > close[1], (1-K) * nz(ADC[1], 1), K * (close[1] - close) + (1 - K) * nz(ADC[1], 1))
nVal = (WildPer - 1) * (ADC * Value / (100 - Value) - AUC)
nRes = iff(nVal >= 0, close + nVal, close + nVal * (100 - Value) / Value)
pos = iff(nRes > close, -1,
	   iff(nRes < close, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=blue, title="Reverse Engineering RSI")
```

> Detail

https://www.fmz.com/strategy/433569

> Last Modified

2023-11-28 15:50:07
