
> Name

Moving-Average-Displaced-Envelope-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/15e93b609a51ed804a3.png)
[trans]

This strategy generates trading signals based on the Moving Average Displacement Envelope indicator. Among them, the envelope is calculated by the percentage factor of the moving average. If the previous high point breaks through the upper track, a sell signal is generated; if the previous low point falls below the lower track, a buy signal is generated.
## Strategy Principle
This strategy uses the displaced exponential moving average (EMA) as the core indicator, and after a certain period, it expands the upper and lower rails through the percentage factor. This constitutes a complete moving average displacement envelope system. Specifically, the envelope system consists of:
* EMA(Price, Period) - Core Exponential Moving Average
* top = sEMA\[disp\] \* ((100 + perAb)/100) - top track
* bott = sEMA\[disp\] \* ((100 - perBl)/100) - lower track
Among them, Percent above and Percent below respectively control the percentage range of the upper and lower rails relative to the core exponential moving average. The Displacement parameter is used to control the periodic displacement between the upper and lower trajectories and the core exponential moving average.
In this way, we can form a suitable trading range by adjusting the above parameters. If the price breaks out of the range, a trading signal is generated. Specifically:
* If the closing price is lower than the lower track bott, a buy signal is generated
* If the closing price is higher than the upper track top, a sell signal is generated
It should be noted that this strategy also provides the reverse parameter. If set to true, the signal direction is opposite to the above.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Using the exponential moving average as a basic indicator can reduce the lag of the curve and improve the sensitivity to price changes.
2. There are many adjustable parameters, and better trading results can be obtained through parameter optimization.
3. Provide reverse mode, which can adapt to different types of markets
4. The rules are simple and clear, easy to understand and implement
## Risks and Prevention
This strategy also has some risks, mainly including:
1. False signals are easily generated in volatile market conditions
2. Improper parameter settings may lead to over-trading or missed signals
3. It cannot effectively filter market noise and may produce some worthless signals.
To prevent these risks, we can optimize from the following aspects:
1. Combine with other indicators to filter signals, such as trading volume, volatility, etc.
2. Add parameter optimization process to find the best parameter combination
3. Appropriately adjust stop loss strategies to control single losses
## Optimization ideas
This strategy still has a lot of room for optimization, and the following aspects can be considered:
1. Add machine learning models to realize automatic optimization and adjustment of parameters
2. Add functions such as stop loss, trailing stop, and trailing stop to effectively control risks
3. Combine sentiment indicators and investor sentiment to filter signals to improve signal quality
4. Increase model combinations and combine with other technical indicators to identify trends and improve overall accuracy.
5. Inherit this strategy template, develop other types of exponential moving average systems, and expand the scope of application
Through these optimizations, the stability, adaptability and effectiveness of the strategy can be further enhanced.
## Summarize
The moving average displacement envelope strategy uses a simple exponential moving average system and parameterized intervals to form clear trading rules that are easy to explain and implement. It is a relatively typical trend following strategy. Through parameter adjustment and optimization, this strategy can produce better results. However, it is also necessary to fully consider the impact of the market environment and guard against potential risks. This strategy is a basic template, and there is still a lot of room for expansion and optimization in the future.
||

This strategy generates trading signals based on the Moving Average Displaced Envelope indicator. The envelope bands are calculated by percentage factors of the moving average. If the previous high breaks above the upper band, a sell signal is generated. If the previous low breaks below the lower band, a buy signal is generated.

## Strategy Logic

This strategy uses the displaced exponential moving average (EMA) as the core indicator, and forms the upper and lower bands after a certain period by percentage factors. This constructs the complete moving average displaced envelope system. Specifically, the envelope system consists of:

* EMA(Price, Period) - The core moving average line  
* top = sEMA\[disp\] \* ((100 + perAb)/100) - Upper band
* bott = sEMA\[disp\] \* ((100 - perBl)/100) - Lower band

Here Percent above and Percent below control the percentage range of the bands relative to the core moving average line. The Displacement parameter controls the period displacement between the bands and the core moving average line.  

In this way, we can form appropriate trading ranges by adjusting the above parameters. Trading signals are generated when prices break through the bands. Specifically:

* If close is lower than the lower band bott, a buy signal is generated
* If close is higher than the upper band top, a sell signal is generated

Note that this strategy also provides a reverse parameter. If set to true, the signal direction is opposite to the above.

## Advantage Analysis

The main advantages of this strategy are:

1. Using exponential moving average as the base indicator can reduce curve lagging and improve sensitivity to price changes  
2. More adjustable parameters allow better optimization of trading performance through parameter tuning
3. The reverse mode adapts to different market types  
4. Simple and clear rules, easy to understand and implement

## Risks and Precautions 

There are also some risks with this strategy:

1. False signals can occur frequently in range-bound markets  
2. Improper parameter settings may cause over-trading or signal missing
3. Market noise cannot be filtered effectively, generating some worthless signals

To prevent these risks, some optimizations can be made:  

1. Filter signals with other indicators like volume, volatility etc. 
2. Add parameter optimization process to find optimum parameter sets
3. Adjust stop loss properly to limit losses

## Optimization Directions

There is still large room for optimizing this strategy:

1. Add machine learning models to realize automatic parameter optimization and adjustment
2. Incorporate features like stop loss, trailing stop to control risks
3. Filter signals with sentiment indicators to improve quality 
4. Increase model combinations with other technical indicators to identify trends and improve overall accuracy  
5. Inherit this strategy template to develop other types of moving average systems and expand applicability

With these optimizations, the stability, adaptability and performance of the strategy can be further improved.

## Summary  

The moving average displaced envelope strategy utilizes simple exponential moving average systems and parameterized bands to form clear trading rules that are easy to interpret and implement. It is a typical trend following system. Through parameter tuning and optimizations, good results can be achieved. But the impacts of market environments should also be fully considered and potential risks should be prevented. This strategy serves as a basic template and has much room for expansions and optimizations.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|9|Period|
|v_input_3|0.5|Percent above|
|v_input_4|0.5|Percent below|
|v_input_5|13|Displacement|
|v_input_6|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-25 00:00:00
end: 2024-02-01 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 14/08/2020
// Moving Average Displaced Envelope. These envelopes are calculated 
// by multiplying percentage factors with their displaced expotential 
// moving average (EMA) core.
// How To Trade Using:
// Adjust the envelopes percentage factors to control the quantity and 
// quality of the signals. If a previous high goes above the envelope 
// a sell signal is generated. Conversely, if the previous low goes below 
// the envelope a buy signal is given.
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Moving Average Displaced Envelope Backtest", shorttitle="MA DE", overlay = true)
Price = input(title="Source", type=input.source, defval=close)
Period =input(defval=9, minval=1)
perAb = input(title = "Percent above", defval=.5, minval=0.01, step = 0.1)
perBl = input(title = "Percent below", defval=.5, minval=0.01, step = 0.1)
disp = input(title = "Displacement", defval=13, minval=1) 
reverse = input(false, title="Trade reverse")
pos = 0
sEMA = ema(Price, Period)
top = sEMA[disp] * ((100 + perAb)/100)
bott = sEMA[disp]* ((100 - perBl)/100)
pos := iff(close < bott , 1,
	     iff(close > top, -1, pos[1])) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1 , 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	 
if (possig == 0) 
    strategy.close_all()
barcolor(possig == -1 ? #b50404: possig == 1 ? #079605 : #0536b3 )
```

> Detail

https://www.fmz.com/strategy/440851

> Last Modified

2024-02-02 17:02:18
