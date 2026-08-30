
> Name

VRSI-EMA Crossover and VMACD Fusion Wave Finder StrategyVSTOCHASTIC-RSI-EMA-CROSSOVER-COMBINED-WITH-VMACD-WAVEFINDER-STRATEGY
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11eb833a57010f4073e.png)
[trans]

## Overview
This is a strategy that combines Stochastic RSI, EMA Crossover and VMACD to identify reversal points in the market and performs best when a downtrend is about to reverse. It generates a buy signal when conditions are met.
## Strategy Principle
This strategy is mainly based on a combination of the following indicators:
1. Stochastic RSI (Stochastic Exponential Smoothed Moving Average): used to identify overbought and oversold phenomena
2. Crossover of EMA (Exponential Moving Average) fast and slow lines: Determine trends and possible reversals
3. VMACD (volume-weighted MACD): used to confirm reversal signals
When the stochastic RSI rebounds from the oversold area, the EM fast line crosses the slow line, and VMACD also starts to rise, a buy signal will be generated. In addition, if the short-term price breaks through the 10-period SMA (simple moving average), it will also be used as an auxiliary signal to generate a buy.
This strategy will track changes in these indicators in real time and calculate SMA, EMA and other information after a certain length. When the buying condition is triggered, a fixed number of contracts will be used to open a buying position. Later, if the stop loss condition is triggered, such as a 5% retracement or below the SMA line, the stop loss will be closed.
## Advantage Analysis
This strategy combines multiple indicators to effectively identify market reversal opportunities. The main advantages are:
1. Stochastic RSI has a strong ability to identify overbought and oversold conditions.
2. EMA crossover judgment of reversal signals is highly accurate
3. VMACD effectively filters false signals
4. Multi-indicator combination to improve signal quality
5. It is reasonable to use short-term SMA as a stop loss method
To sum up, this strategy can effectively seize the reversal signal and establish a long position after falling to a certain extent, thereby making a profit.
## Risk Analysis
Although this strategy has certain advantages, there are also some risks that need to be noted, mainly including:
1. The market may not reverse and continue to fall, a systemic risk
2. When multiple indicators trigger the buy condition at the same time, the probability is low and fewer signals are generated.
3. SMA stop loss may be too subjective and the retracement control effect is average.
4. Failure to consider significant market shocks
In response to the above risks, further optimization can be done in the following ways:
1. Add a combination of other reversal indicators to improve the effect
2. Use a combination of time stop loss and amount stop loss
3. Judge the market status and avoid opening positions during volatile market conditions
4. Optimize stop loss logic to prevent overly aggressive stop loss traps
## Optimization direction
This strategy can be further optimized mainly in the following directions:
1. Add more combinations of indicators to form indicator clusters and improve signal quality
2. Select the best parameters according to the characteristics of major types of assets and optimize parameters.
3. Add a machine learning algorithm to determine the probability of reversal based on historical data training.
4. Add slippage during backtesting to make the results closer to actual transactions
5. Optimize the stop loss strategy to make it smoother and more reasonable
6. Detect trend status, distinguish between shocks and trending markets, and avoid blindly opening positions
## Summarize
The wave finder strategy that integrates the VRSI-EMA crossover and VMACD is generally a good strategy for identifying downward reversal opportunities. It combines multiple indicators to form a buy signal, which can effectively determine the timing of reversal. However, there are also some directions that need to be optimized. If further improved, the actual performance of this strategy will be even better. It represents a typical example of such quantitative strategies integrating multiple indicators.

||



## Overview

This is a strategy that incorporates Stochastic RSI, EMA crossovers and VMACD to identify market reversal points and performs best when a downtrend reversal is imminent. It will generate buy signals when conditions are met.

## Strategy Logic

The strategy mainly relies on the combination of the following indicators:  

1. Stochastic RSI: To identify overbought and oversold conditions  
2. EMA Crossover between Fast EMA and Slow EMA: To determine trend direction and potential reversals  
3. VMACD: To confirm reversal signals

When Stochastic RSI bounces off the oversold region, the fast EMA crosses above the slow EMA, and at the same time VMACD starts to rise, a buy signal is generated. In addition, if the short term price breaks above the 10 period SMA, it also serves as an auxiliary signal to buy.

The strategy tracks the changes of these indicators in real time, and calculates SMA, EMA and other information over a fixed lookback period. When the buy conditions are triggered, it will buy and open position with a fixed number of contracts. Afterwards if the stop loss conditions are triggered, such as 5% drawdown or price below SMA line, positions will be closed for stop loss.

## Advantage Analysis  

The strategy combines multiple indicators and is capable of effectively identifying market reversal opportunities. The main advantages are:

1. Stochastic RSI is strong at catching overbought and oversold conditions  
2. EMA crossover has high accuracy at determining reversal signals
3. VMACD helps filter fake signals effectively 
4. Combining multiple indicators improves signal quality
5. Using short term SMA as a stop loss method is reasonable

In summary, this strategy can effectively capture reversal signals, establish long positions after declines to a certain degree, and thus gain profits.

## Risk Analysis

Despite having some edge, there are also risks to note for this strategy:  

1. Market may not reverse and continues to decline - systematic risk
2. Probability of multiple indicators triggering buy together is not high - few signals  
3. SMA stop loss could be too subjective and result in mediocre drawdown control  
4. Does not take into account high volatility market environments

Some ways to mitigate the risks:

1. Add more reversal indicators for better combo effect  
2. Use timed stop loss combined with amount based stop loss 
3. Judge market conditions and avoid taking positions in choppy environments  
4. Optimize stop loss logic to prevent over-aggressive stop loss from being stopped out

## Optimization Directions

Main areas that could be optimized for the strategy:

1. Add more indicators to form an indicator cluster, improving signal quality  
2. Select optimal parameters based on characteristics of different asset classes  
3. Incorporate machine learning models to estimate reversal probability based on historical data   
4. Add slippage when backtesting to make results closer to live performance
5. Refine stop loss methodology to become more smooth and reasonable  
6. Detect trend conditions to distinguish ranging and trending environments before entering positions blindly  

## Conclusion  

Overall this VRSI-EMA Crossover with VMACD Wavefinder Strategy is quite capable of catching downtrend reversal opportunities. It generates buy signals effectively by combining multiple indicators to determine optimal timing for reversals. However, there remains some areas for improvements. If further optimized, the strategy's performance in live trading could be even better. It represents a typical example of a quantitative strategy based on the fusion of multiple indicators.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|length|
|v_input_2|2|confirmBars|
|v_input_3|12|Short period|
|v_input_4|26|Long period|
|v_input_5|9|Smoothing period|
|v_input_6|14|lengthRSI|
|v_input_7|14|lengthStoch|
|v_input_8|3|smoothK|
|v_input_9|3|smoothD|
|v_input_10|25|OverSold|
|v_input_11|75|OverBought|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-14 00:00:00
end: 2023-11-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Wavefinder+", overlay=true)
length = input(20)
confirmBars = input(2)
price = close

slow = input(12, "Short period")
fast = input(26, "Long period")
signal = input(9, "Smoothing period")


maFast = ema( volume * close, fast ) / ema( volume, fast ) 
maSlow = ema( volume * close, slow ) / ema( volume, slow ) 
da = maSlow - maFast 
maSignal = ema( da, signal ) 
dm=da-maSignal


source = close
lengthRSI = input(14, minval=8), lengthStoch = input(14, minval=5)
smoothK = input(3,minval=3), smoothD = input(3,minval=3)
OverSold = input(25), OverBought = input(75)
rsi1 = rsi(source, lengthRSI)
rsi2= rsi(low, 20)
k = sma(stoch(rsi1, rsi1, rsi1, lengthStoch), smoothK)
d = sma(k, smoothD)
k1= sma(stoch(rsi2, rsi2, rsi2, lengthStoch), smoothK)
d1= sma(k1, smoothD)
delta=k-d1
ma = ema(low, length)
ema5= ema(price,20)
sma= sma(price,10)
bcond = price < ma
lcond = price> ema5
bcount = 0
lcount= 0
bcount := bcond ? nz(bcount[1]) + 1 : 0
lcount := lcond ? nz(lcount[1]) + 1 : 0

if (lcount>1 and change(k)>3 and k>d and k<55 and rising(dm,1)) or ( k[1]-k[2]<-2 and k-k[1]>5 and k>35 and k<80) or (ma-sma>0.05*sma and rising(sma,3) and rising(dm,2)) 
    strategy.entry("Long", strategy.long, qty=10000/close)

if (bcount == confirmBars)
    strategy.close("Long")
if close<0.99*sma
    strategy.close("Long")

plot(0.99*sma)
plot(ma)

//hline(OverSold,color=blue)
//hline(OverBought,color=blue)

//plot(d, color=red)
//plot(k, color=green,title="k-line")
    
//(close-close[3]<-0.05*close[3]) or (close-close[2]<-0.05*close[2]) or (close-close[2]<-0.05*close[2]) or (close-close[4]<-0.05*close[4]) or
//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/432808

> Last Modified

2023-11-21 17:12:06
