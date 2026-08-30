
> Name

Beyond Indicator Momentum System Trading Strategy SMI-Ergodic-Oscillator-Momentum-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/99148773e9ce335da302ca495f0e16e13dc4268bbbb2298180b726ba697b3883.png)

[trans]

## Overview
This strategy builds a trend tracking system based on the Transcendence Index (SMI) and the Ergotic Line, and combines the fast moving average and the slow moving average to form buy and sell signals. It is a momentum system strategy for frequent trading.
## Strategy Principle
This strategy is mainly based on the Transcendence Index (SMI) and the Ergotic Line (Ergotic Line) to construct trading signals.
The Transcendence Index (SMI) is calculated based on the speed of price movement, calculated by dividing the difference between the exponential moving averages of two different periods by the absolute difference. The calculation formula is:
SMI = (Fast EMA - Slow EMA) / Abs(Fast EMA - Slow EMA)

Among them, Fast EMA is a short-period exponential moving average, and Slow EMA is a long-period exponential moving average.
By calculating the speed of price changes, SMI can determine changes in market trends. When the SMI crosses 0, it is a bullish signal, and vice versa, it is a bearish signal.
The Ergotic Line is the exponential moving average of SMI and can be used to generate trading signals. When the SMI crosses the Wudao line above, it is a buy signal, and when the SMI crosses the Wudao line below, it is a sell signal.
This strategy forms a trend tracking system without lag through the combination of SMI and Enlightenment Line, which is a momentum system strategy for frequent trading.
## Strategic Advantages
1. Trend judgment based on price change speed and sensitive to trend changes;
2. The enlightenment line filters out the false signals of the SMI indicator and forms a more reliable trading signal;
3. Adopting a dual-track structure, the buying and selling signals are clear;
4. Frequent transactions and the ability to capture rapid price changes within trends.
5. No lag, able to capture turning points in time.
## Strategy Risk
1. As a momentum system, there is a large risk of stop loss in volatile market conditions;
2. Improper setting of dual tracks may lead to frequent signals and excessive trading;
3. Improper setting of short-period parameters may produce a large number of false signals;
4. Failure to consider the direction of the large-level trend and may operate against the trend.
5. Stop loss rules must be strictly followed, otherwise losses may increase.
For risks, you can consider optimizing the following aspects:
1. Optimize dual-track parameters to reduce the probability of false signals;
2. Combine with trend filtering to avoid going against the trend;
3. Add a stop loss strategy to control single losses.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the fast and slow moving average parameters and find the optimal parameter combination;
2. Test different price inputs, such as opening price, highest price, lowest price, etc.;
3. Add machine learning algorithms to automatically optimize parameters;
4. Filter based on trend indicators to avoid counter-trend trading;
5. Add stop-loss strategies and strictly control single losses;
6. Consider factors such as the number of transactions or profit-loss ratio to avoid over-trading;
7. Test the suitability of different varieties to find the best variety.
8. Explore combinations with other indicators to form a more complete trading system.
## Summarize
This strategy builds a trend tracking system without lag based on the Transcendence Indicator and Enlightenment Line, forming clear trading signals through dual tracks, and is a momentum strategy for frequent trading. The advantage is that it can capture rapid changes in trends, but the disadvantage is that it can easily lead to over-trading and counter-trend trading. We can improve it through parameter optimization, stop loss strategies, trend filtering, etc. to build it into a more complete quantitative trading system.
||

## Overview

This strategy builds a trend following system based on the Superior Momentum Index (SMI) and Ergodic Line, generating trading signals through the combination of fast and slow moving averages. It belongs to a high-frequency momentum trading system.

## Strategy Logic

The strategy mainly utilizes the Superior Momentum Index (SMI) and Ergodic Line to construct trading signals.

The SMI measures the speed of price changes by calculating the difference between two exponential moving averages of different periods divided by the absolute difference. Its formula is:

SMI = (Fast EMA - Slow EMA) / Abs(Fast EMA - Slow EMA)

Where Fast EMA is the short-period EMA and Slow EMA is the long-period EMA. 

By gauging the speed of price movements, SMI can determine the trend changes in the market. A cross above 0 suggests an uptrend while a cross below 0 signals a downtrend.

The Ergodic Line is an EMA of SMI, which generates trade signals. A cross above the Ergodic Line is a buy signal while a cross below is a sell signal.

By combining SMI and the Ergodic Line, the strategy forms a lag-free trend following system, making it a high-frequency momentum trading strategy.

## Advantages

1. Sensitive to trend changes based on price velocity.

2. Ergodic Line filters fake signals from SMI, forming reliable trade signals. 

3. Clear buy/sell signals generated by the double rail structure. 

4. High trading frequency to capture fast price movements within trends.

5. No lagging, able to capture turning points in a timely manner.

## Risks

1. Prone to frequent stop loss in ranging markets as a momentum system.

2. Improper double rail settings may cause excessive trading due to frequent signals.

3. Bad short-term parameter tuning can lead to excessive false signals. 

4. No consideration of major trend direction may lead to counter-trend trades.

5. Strict stop loss rules must be followed, otherwise losses could mount.

To address the risks, the following aspects can be considered for optimization:

1. Optimize double rail parameters to reduce false signals.

2. Add trend filter to avoid counter-trend trades.  

3. Implement stop loss strategies to control single trade loss.

## Optimization Directions 

The strategy can be improved in the following aspects:

1. Optimize fast and slow EMA parameters to find the optimal parameter combination.

2. Test different price inputs like open, high, low prices etc.

3. Incorporate machine learning algorithms to auto-optimize parameters.

4. Add trend filters to avoid counter-trend trades.

5. Implement stop loss strategies to strictly control single trade loss. 

6. Consider trading frequency and profit factor to prevent over-trading.

7. Test applicability across different products to find the optimal asset.

8. Explore combinations with other indicators to build a more comprehensive system.

## Conclusion

The strategy constructs a lag-free trend following system using SMI and Ergodic Line, generating clear trade signals through the double rail structure. It belongs to a high-frequency momentum trading strategy. The advantage is quickly capturing trend changes while the disadvantages include over-trading and counter-trend trades. Improvements can be made through parameter optimization, stop loss, trend filters etc. to build a more robust quantitative trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|fastPeriod|
|v_input_2|8|slowPeriod|
|v_input_3|3|SmthLen|
|v_input_4|0.5|TopBand|
|v_input_5|-0.5|LowBand|
|v_input_6|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-01 00:00:00
end: 2023-10-31 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 03/11/2017
// The SMI Ergodic Indicator is the same as the True Strength Index (TSI) developed by 
// William Blau, except the SMI includes a signal line. The SMI uses double moving averages 
// of price minus previous price over 2 time frames. The signal line, which is an EMA of the 
// SMI, is plotted to help trigger trading signals. Adjustable guides are also given to fine 
// tune these signals. The user may change the input (close), method (EMA), period lengths 
// and guide values.
// You can use in the xPrice any series: Open, High, Low, Close, HL2, HLC3, OHLC4 and ect...
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="SMI Ergodic Oscillator")
fastPeriod = input(4, minval=1)
slowPeriod = input(8, minval=1)
SmthLen = input(3, minval=1)
TopBand = input(0.5, step=0.1)
LowBand = input(-0.5, step=0.1)
reverse = input(false, title="Trade reverse")
// hline(0, color=gray, linestyle=dashed)
// hline(TopBand, color=red, linestyle=line)
// hline(LowBand, color=green, linestyle=line)
xPrice = close
xPrice1 = xPrice - xPrice[1]
xPrice2 = abs(xPrice - xPrice[1])
xSMA_R = ema(ema(xPrice1,fastPeriod),slowPeriod)
xSMA_aR = ema(ema(xPrice2, fastPeriod),slowPeriod)
xSMI = xSMA_R / xSMA_aR
xEMA_SMI = ema(xSMI, SmthLen)
pos = iff(xEMA_SMI < LowBand, -1,
	   iff(xEMA_SMI > TopBand, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )  
plot(xSMI, color=green, title="Ergotic SMI")
plot(xEMA_SMI, color=red, title="SigLin")
```

> Detail

https://www.fmz.com/strategy/430740

> Last Modified

2023-11-01 11:19:18
