
> Name

Dual-Rate-of-Change-Momentum-Indicator-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/187762fb9492354ea1bfe1e6b388faa45d7379712c0ff7e49e2f7e307932b64b.png)

[trans]

## Overview
This strategy is a trading strategy based on the Dual Rate Volume Momentum indicator. The strategy constructs a comprehensive momentum indicator by calculating the changes in multiple different periods, and uses its fluctuations to determine market trends and generate trading signals.
## Strategy Principle
The core indicator of this strategy is the Dual Rate of Change Momentum Indicator, or DRCMI for short. It consists of a weighted average of changes in multiple different periods. Specifically, it includes changes in 6 cycles, 10 cycles, 15 cycles and 20 cycles. Among them, the weight of the 6-period and 10-period changes is 1; the weight of the 15-period change is 2; the weight of the 20-period change is 3. In this way, changes in longer periods have greater weight.
Combining the changes in multiple cycles can reflect both the short-term and longer-term momentum of the market. When the DRCMI is positive, it means that both the short-term and long-term trends are upward; when it is negative, it means that both the short-term and long-term trends are downward. The volatility of the DRCMI also reflects the strength of market momentum.
Based on the long and short cyclical characteristics of DRCMI, the strategy determines the market trend and generates trading signals. When the DRCMI crosses the 0 axis above, go long; when the DRCMI crosses the 0 axis below, go short.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Integrate multi-period momentum to judge market trends more accurately.
2. Captures cyclical characteristics better than a single variation indicator.
3. The weight design is reasonable, focusing on longer periods, and can filter noise.
4. Simple to implement, only one indicator can determine the market situation.
5. The cycle parameters can be customized to adapt to different varieties.
## Risk Analysis
There are also some risks with this strategy:
1. Multi-period comprehensive indicators, parameter settings are sensitive, and improper settings may fail.
2. Focus only on momentum indicators and may ignore other factors.
3. There is a certain lag, and market entry and exit should be appropriately optimized.
4. When the market fluctuates violently, stop-loss protection is still necessary.
In order to control risks, it is recommended to set stop loss, optimize indicator parameters, and assist other technical indicators.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the parameters of DRCMI and adjust the settings of cycle and weight.
2. Combine with trend indicators to determine the market stage and dynamically adjust parameters.
3. Set dynamic stop loss to protect profits.
4. Combined with correlation indicators, evaluate the relationship between varieties and set variety combinations.
## Summarize
This strategy builds the DRCMI indicator, integrates multi-period momentum characteristics, and determines market trends to make profits. The strategy is simple and practical, and the effect is obvious. However, PARAMETER settings and stop loss protection still need to be optimized, and the effect is better when used in conjunction with other technical indicators.
||

## Overview

This is a trading strategy based on the Dual Rate of Change Momentum Indicator (DRCMI). It generates trading signals by gauging market momentum across multiple timeframes.

## Strategy Logic

The core of this strategy is the DRCMI, which is a weighted average of multiple Rate of Change (ROC) indicators across different periods. Specifically, it incorporates 6-period, 10-period, 15-period, and 20-period ROC. The 6-period and 10-period ROC have a weight of 1, while the 15-period ROC has a weight of 2, and the 20-period ROC has a weight of 3. Thus, longer-term ROC is given greater emphasis.  

By combining ROC across timeframes, the DRCMI reflects both short-term and longer-term momentum. When it is positive, it indicates an uptrend in both the short and long run. When negative, it signals a downtrend. The intensity of the momentum is also captured in the amplitude of DRCMI fluctuations.

Trading signals are generated based on the cyclicality of DRCMI. A long position is initiated when DRCMI crosses above 0, while a short position is initiated when it crosses below 0.

## Advantage Analysis  

The main advantages of this strategy are:

1. Integrates momentum across periods for more accurate trend identification.  
2. Better captures cyclicality compared to single timeframe ROC.
3. Reasonable weighting methodology focuses on longer-term to filter noise.  
4. Simple to implement with just a single indicator for signals.
5. Customizable lookback periods suit different products.

## Risk Analysis

There are also some risks to consider:

1. Sensitivity to parameters with multiple integrated timeframes.
2. May overlook other factors by only considering momentum. 
3. Potential lag requires optimized entry and exit.
4. Stop loss still necessary during high volatility.  

To mitigate risks, stop losses should be utilized along with optimization of the DRCMI parameters and incorporation of additional technical indicators.

## Optimization Directions

Some ways to improve the strategy:

1. Optimize DRCMI parameters like periods and weights.  
2. Incorporate trend indicators to dynamically adjust parameters based on market regime.
3. Implement dynamic stops to lock in profits.
4. Consider intermarket relationships with correlation analysis to construct spreads. 

## Conclusion

This strategy generates trading signals by condensing momentum from multiple timeframes into the DRCMI indicator. It is simple yet effective in profiting from momentum swings. However, parameter tuning and stop loss implementation requires further optimization, and combining DRCMI with additional technical indicators can improve performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-23 00:00:00
end: 2023-11-22 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 20/09/2017
// This indicator really is the KST indicator presented by Martin Pring. 
// the KST indicator is a weighted summed rate of change oscillator that 
// is designed to identify meaningful turns. Various smoothed rate of change 
// indicators can be combined to form different measurements of cycles.
//
// You can change long to short in the Input Settings
// WARNING:
//  - For purpose educate only
//  - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="MovROC (KST indicator)", shorttitle="MovROC (KST indicator)")
reverse = input(false, title="Trade reverse")
hline(0, color=purple, linestyle=line)
xROC6 = sma(roc(close, 6), 10)
xROC10 = sma(roc(close, 10), 10)
xROC15 = sma(roc(close, 15), 9)
xROC20 = sma(roc(close, 20), 15)
nRes = xROC6 + (2 * xROC10) + (3 * xROC15) + (4 * xROC20)
pos = iff(nRes > 0, 1,
	   iff(nRes < 0, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=blue, title="MovROC (KST indicator)")
```

> Detail

https://www.fmz.com/strategy/432967

> Last Modified

2023-11-23 10:37:00
