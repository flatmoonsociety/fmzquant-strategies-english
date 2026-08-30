
> Name

Bandpass-Filtering-Trend-Extraction-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1657295340f3d80b6cb.png)
[trans]

## Overview
The band-pass filter trend extraction strategy is a stock trend following strategy based on a band-pass filter. This strategy uses exponentially weighted moving averages and band-pass filtering to process price sequences, extract the trend components in prices, and use certain parameters as signals for opening and closing positions.
## Strategy Principle
This strategy first constructs a double exponential weighted moving average, and controls the time length and smoothness of the moving average by adjusting the parameters Length and Delta. Then a set of mathematical transformations are used to extract the trend component in the price series and stored in the xBandpassFilter variable. Finally, the simple moving average xMean of xBandpassFilter is calculated as an indicator for opening and closing positions.
Go long when xMean goes above the level set by parameter Trigger, go short when it goes below. The sensitivity of opening and closing positions can be controlled by adjusting the Trigger level.
## Advantage Analysis
1. Using the double exponentially weighted moving average can effectively filter out some noise in the price sequence, making the strategy more stable.
2. The band-pass filter only extracts the trend components in the price sequence to avoid being misled by the volatile market, making the strategy more stable and reliable.
3. The strategy has fewer parameters and is easy to tune and control risks.
## Risk Analysis
1. The strategy has a time lag and may miss the opportunity for rapid price reversal. 
2. Both the double exponentially weighted moving average and the band-pass filter have a low-pass filtering effect, which will filter out high-frequency signals and reduce the sensitivity of the strategy.
3. If the parameters are set improperly and the filtering effect is too strong, strong trend opportunities may be missed.
The lag problem can be improved by appropriately shortening the Length parameter, and the sensitivity of the Trigger level control strategy can be adjusted.
## Optimization direction
1. You can consider adding a stop-loss strategy to control single losses.
2. The stability of the strategy can be improved through short-term and long-term double moving average systems.
3. The reversal signal can be judged in combination with other indicators such as market trading volume to avoid being trapped in volatile market conditions.
4. Machine learning or genetic algorithms can be used to optimize parameters to make the strategy more stable and reliable.
## Summarize
This strategy is relatively stable overall and performs better in strong trending markets. It can be further optimized in a variety of ways to maintain stable profitability in more market environments. This strategy deserves further research and application.
||


## Overview

The Bandpass Filtering Trend Extraction Strategy is a stock trend tracking strategy based on bandpass filters. It uses an exponentially weighted moving average and bandpass filtering to process the price series and extract the trend component in prices as the signal for entries and exits. 

## Principles

The strategy first constructs a double exponential moving average by tuning the Length and Delta parameters to control the length of the moving average and smoothness. Then it uses a set of mathematical transformations to extract the trend component from the price series and stores it in the xBandpassFilter variable. Finally, it calculates the simple moving average of xBandpassFilter, xMean, as the indicator for entries and exits.

It goes long when xMean crosses above the Trigger level, and goes short when crossing below. The sensitivity of entries and exits can be controlled by tuning the Trigger level.

## Advantages

1. The double EMA effectively filters out some noise in prices for more stable strategies.
2. Bandpass filtering only extracts the trend component in prices, avoiding whipsaws.
3. Fewer parameters make optimization and risk control easier.

## Risks 

1. Time lag causes missed opportunities from quick reversals.
2. Double EMA and bandpass filtering have low pass effects, reducing sensitivity. 
3. Overfiltering can cause missing strong trends if parameters poorly tuned.

Shortening Length can improve lag issues. Tuning Trigger controls sensitivity.

## Enhancements

1. Add stop loss to control single trade loss.
2. Dual moving averages system can improve stability. 
3. Combine with volume or other reversal signals to avoid whipsaws.
4. Use machine learning or genetic algorithms to optimize parameters.

## Conclusion

The strategy is relatively stable with good performance in strong trending markets. Further optimizations in multiple market environments can make it more reliably profitable. It warrants further research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Length|
|v_input_2|0.5|Delta|
|v_input_3|false|Trigger|
|v_input_4|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-27 00:00:00
end: 2024-01-02 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version = 2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 14/12/2016
// The related article is copyrighted material from Stocks & Commodities Mar 2010
//
// You can use in the xPrice any series: Open, High, Low, Close, HL2, HLC3, OHLC4 and ect...
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="Extracting The Trend Strategy Backtest")
Length = input(20, minval=1)
Delta = input(0.5)
Trigger = input(0)
reverse = input(false, title="Trade reverse")
hline(Trigger, color=blue, linestyle=line)
xPrice = hl2
beta = cos(3.1415 * (360 / Length) / 180)
gamma = 1 / cos(3.1415 * (720 * Delta / Length) / 180)
alpha = gamma - sqrt(gamma * gamma - 1)
xBandpassFilter = 0.5 * (1 - alpha) * (xPrice - xPrice[2]) + beta * (1 + alpha) * nz(xBandpassFilter[1]) - alpha * nz(xBandpassFilter[2])
xMean = sma(xBandpassFilter, 2 * Length)
pos = iff(xMean > Trigger, 1,
	   iff(xMean < Trigger, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(xMean, color=red, title="ExTrend")
```

> Detail

https://www.fmz.com/strategy/437527

> Last Modified

2024-01-03 15:22:49
