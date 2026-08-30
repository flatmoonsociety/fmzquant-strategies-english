
> Name

multiple-technical-indicators-Momentum-Breakout-Strategy multiple-technical-indicators-Momentum-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/837b5734fab0b8a987ed89d35c157abb4b3758c472afdfc358d93492923358bf.png)

[trans]

## Overview
This strategy comprehensively considers a variety of technical indicators and conducts buying operations when it is judged that the market has strong bull momentum. Specifically, the strategy will consider the five indicators of MACD, RSI, ADX, Stochastic and Bollinger Bands at the same time, and generate a buy signal when these indicators meet the long conditions at the same time.
## Strategy Principle
The core logic of this strategy is to buy after judging that the market has strong bull momentum. The specific judgment rules are as follows:
1. The current bars of the 5-minute, 15-minute and 60-minute MACD are all rising
2. RSI is greater than 60
3. ADX is greater than 12
4. Stochastic %K line wears %D line
5. Bollinger Bands rise on track
When the above five conditions are met at the same time, it is believed that the market has strong bull momentum, and it is time to carry out buying operations.
The trading exit rule is to exit the current position when the 5-minute closing price falls below the 5-minute EMA.
## Advantage Analysis
This strategy has several advantages:
1. Combine multiple indicators to determine the overall bullish trend of the market and avoid being misled by a single indicator.
2. Use a combination of high and low timeline indicators to determine the sustainability of market bull momentum
3. Strict exit mechanism to avoid loss expansion
4. The transaction frequency is moderate and will not be too intensive.
In general, this strategy has accurate judgment and proper risk control, and is suitable for capturing short-term long market conditions.
## Risk Analysis
There are also some risks with this strategy:
1. Judgment based on a combination of multiple indicators increases the probability of entry errors.
2. The exit mechanism may be too strict and correct trades may be exited prematurely
3. The transaction frequency is high. Too frequent transactions will increase the handling fee burden.
Generally speaking, the risks of this strategy mainly lie in entry errors and premature exit, which need to be mitigated through parameter optimization and rule adjustment.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize MACD parameters and find parameter combinations that are more in line with market rules.
2. Adjust RSI parameters to find better overbought and oversold ranges
3. Optimize the parameters of Stochastic and find better cross combinations
4. Adjust Bollinger Band parameters to make Bollinger Bands better reflect market volatility
5. Optimize or replace exit mechanism rules to reduce the probability of incorrect exits
Through parameter and rule optimization, the profitability and risk control capabilities of this strategy can be further improved.
## Summarize
This strategy comprehensively considers multiple indicators to determine the bullish trend of the market, and the exit mechanism is relatively strict. The strategic judgment is accurate, the short-term market can be captured, and the risk control is also good. By continuously optimizing parameters and trading rules, the effectiveness of the strategy can be further enhanced. Overall, this strategy has strong practicality.
||


## Overview  

This strategy considers multiple technical indicators comprehensively and takes long position when the market is judged to have strong bullish momentum. Specifically, this strategy takes into account MACD, RSI, ADX, Stochastic and Bollinger Band these 5 indicators. It generates buy signals when all these indicators meet bullish criteria simultaneously.   

## Strategy Logic   

The core logic of this strategy is to buy when the market is determined to have strong bullish momentum. The specific judging rules are as follows:   

1. The current MACD bars of 5-minute, 15-minute and 60-minute charts are rising.   
2. RSI is greater than 60   
3. ADX is greater than 12   
4. Stochastic %K crosses over %D    
5. Bollinger Band upper band rises  

When all the 5 conditions above are met, the market is considered to have strong bullish momentum. At this time, a long position will be taken.   

The exit rule is to close current position when 5-minute closing price breaks below 5-minute EMA.  

## Advantage Analysis  

The advantages of this strategy include:   

1. Combining multiple indicators prevents being misguided by a single one  
2. Using indicators across timeframes judges sustainability of bullish momentum   
3. Strict exit mechanism prevents enlarged losses
4. Appropriate trading frequency without over-trading  

In general, this strategy has accurate judgement, proper risk control and is suitable to capture short-term bullish trends.   

## Risk Analysis   

This strategy also has some risks:   

1. Combining multiple indicators increases probability of wrong entry   
2. Exit mechanism may be too strict, causing premature exit from right trades  
3. High trading frequency increases burden of commission fees  

In summary, the main risks of this strategy lies in wrong entry and premature exit. These need to be alleviated through parameter tuning and rule adjustment.   

## Optimization Directions   

This strategy can be optimized in the following aspects:   

1. Optimize MACD parameters to find combinations better fitting the market  
2. Adjust RSI parameters to locate better overbought/oversold zones   
3. Optimize Stochastic parameters for better crossovers  
4. Tune Bollinger Band parameters for better reflection of market volatility  
5. Optimize or replace exit rules to reduce premature exits  

Through parameter and rule optimization, this strategy's profitability and risk control ability can be further improved.  

## Conclusion   

This strategy judges bullish trend by combining multiple indicators with relatively strict exits. It has accurate judgement, able to capture short-term trends and proper risk control. Continuous optimization over parameters and trading rules can further enhance the strategy. In summary, this is a practical strategy with strong usability.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Stochastic Length|
|v_input_2|3|%K Smoothing|
|v_input_3|3|%D Smoothing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-15 00:00:00
end: 2023-11-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © makarandpatil

// This strategy is for Bank Nifty instrument and for intraday purpose only
// It checks for various indicators and gives a buy signal when all conditions are met 
// Bank Nifty when in momentum gives 100-200 points in spot in 5-15 min which is how long the trade duration should be
// Issues - The custom script as per TradingView Pinescripting has an issue of repaint
// More information on repainting issue in this link - https://www.tradingview.com/pine-script-docs/en/v5/concepts/Repainting.html
// Use the script alert only to get notified, however check all the parameters individually before taking the trade
// Also, please perform a backtesting and deep backtesting of this strategy to see if the strategy gave correct buy signals in the past
// The script is made for testing purposes only and is in beta mode. Please use at own risk.

//@version=5
strategy("BankNifty_Bullish_Intraday", overlay=true, margin_long = 100, margin_short = 100)

// Variables
StochLength = input(14, title="Stochastic Length")
smoothK = input(3, title="%K Smoothing")
smoothD = input(3, title="%D Smoothing")
 
 
//INDICATOR CALCULATIONS
 
// 1. MACD
[macdLine, signalLine, histLine] = ta.macd(close[0],12,26,9)
 
macd5 = request.security(syminfo.tickerid, "5", macdLine)
macd15 = request.security(syminfo.tickerid,"15",macdLine)
macd60 = request.security(syminfo.tickerid,"60",macdLine)
 
// 2. RSI Calculation
xRSI = ta.rsi(close, 14)
 
// 3. ADX calculation
[diplus, diminus, adx] = ta.dmi(14,14)
// plot(adx,color = color.black)
 
// 4. Stochastic Calculation
k = ta.sma(ta.stoch(close, high, low, StochLength), smoothK)
d = ta.sma(k, smoothD)
 
// 5. Bollinger Band calculation
[middle, upper, lower] = ta.bb(close, 20, 2)
 
 
//CONDITIONS
 
// 1. Conditions for MACD
macd5Uptick = macd5[0] > macd5[1]
macd15Uptick = macd15[0] > macd15[1]
macd60Uptick = macd60[0] >= macd60[1]
 
// 2. Condition for xRSI
RSIStrong = xRSI > 60
 
// 3. Condition for ADX
ADXUngali = adx >= 12
 
// 4. Condition for Stochastic
StochPCO = k > d
 
// 5. Condition for Bollinger Band
BBCU = upper > upper [1]
 
//Evaluate the long condition
// longCondition = macd5Uptick and macd15Uptick and RSIStrong and ADXUngali and StochPCO and BBCU
longCondition = macd5Uptick and macd15Uptick and macd60Uptick and RSIStrong and ADXUngali and StochPCO and BBCU
// longCondition = macd5Uptick and macd15Uptick and RSIStrong and ADXUngali and StochPCO and BBCU

if (longCondition)
    strategy.entry("Buy", strategy.long,alert_message = "BankNifty_Buy_Momentum")

shortCondition = close < ta.ema(close,5)
if (shortCondition)
    strategy.entry("BuySquareoff", strategy.short, alert_message = "BankNifty_Closed_Below_5EMA")

```

> Detail

https://www.fmz.com/strategy/432900

> Last Modified

2023-11-22 15:56:43
