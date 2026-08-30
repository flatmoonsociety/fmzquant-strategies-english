
> Name

DiNapoli-Detrended-Oscillator-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy is based on the DiNapoli detrending oscillator to determine trading signals. This indicator uses the difference between the price and the moving average to reflect the overbought and oversold areas of the price, thereby identifying reversal opportunities. A strategy uses a breakthrough of a specific threshold as a trading signal.
### Strategy Principles
The strategy mainly includes the following elements:
1. Moving average: Calculate the moving average of a certain period to determine the price trend.
2. Difference indicator: The difference between the price and the moving average forms an oscillator.
3. Threshold line: When the difference indicator exceeds the threshold value, a trading signal is generated.
4. Buy signal: Buy when the difference crosses the threshold line.
5. Short signal: go short when the difference falls below the threshold line.
6. Reverse option: The long/short signal can be reversed as a trading signal.
This strategy determines the divergence between price and trend to capture short-term reversal opportunities. The implementation logic is simple and intuitive.
### Advantage Analysis
Compared with other reversal strategies, this strategy has the following advantages:
1. The principle is simple, intuitive and easy to understand, and the implementation difficulty is low.
2. Few parameters, convenient for backtest optimization.
3. Parameters can be adjusted by oneself, suitable for different cycles.
4. Provide reverse options, which can be flexibly used in different markets.
5. Clear stop-loss and stop-profit methods can control risks.
6. The retracement is relatively small, and the curve shock can be reduced through parameter adjustment.
7. Machine learning can be introduced for parameter optimization.
8. Overall, the risk-return balance is good and suitable for short-term trading.
### Risk Analysis
However, this strategy also has the following major risks:
1. Too much reliance on parameter optimization leads to the risk of over-fitting.
2. Both moving averages and indicators have hysteresis.
3. Lack of verification of auxiliary variables other than price.
4. The timing effect may be weakened due to changes in the market environment.
5. It is difficult to continuously obtain Alpha in the long term and requires frequent adjustments.
6. Pay attention to the return drawdown ratio to prevent the curve from being too jagged.
7. The transaction frequency is high, which affects transaction costs.
8. The robustness of the parameters in multiple markets needs to be verified.
### Optimization direction
Based on the above analysis, the optimization directions of this strategy include:
1. Test the effects of different moving average parameters.
2. Add trading volume indicators for verification.
3. Set stop loss and take profit to control risks.
4. Evaluate multi-species and multi-cycle robustness.
5. Continuously revalidate through rolling backtesting.
6. Adjust position management and reduce transaction frequency.
7. Introduce machine learning to generate better parameters.
8. Optimize the overall fund management strategy.
9. Continuously iterate strategies to adapt to market changes.
### Summarize
Overall, this strategy is a relatively simple reversal strategy idea and can achieve good results through parameter adjustment. However, any strategy needs to prevent overfitting and achieve long-term stable profitability. This requires continuous backtesting and optimization, and strategic improvement from more dimensions.
||


### Overview

This strategy generates trading signals based on the DiNapoli Detrended Oscillator. It reflects overbought/oversold levels by the difference between price and moving average, aiming to identify reversal opportunities. Signals are generated when the oscillator crosses a threshold.

### Strategy Logic 

The key components are:

1. Moving average: Calculates the trend baseline.

2. Difference indicator: Price minus moving average forms the oscillator.

3. Threshold line: Crossing this level triggers signals.

4. Long signal: Oscillator crossing above threshold.

5. Short signal: Oscillator crossing below threshold. 

6. Reverse option: Flips the long/short signals.

The strategy aims to capture short-term reversals by identifying divergences between price and trend. The logic is simple and intuitive.

### Advantages

Compared to other reversal strategies, the advantages are:

1. Simple and intuitive logic, easy to implement.

2. Minimal parameters, convenient backtesting. 

3. Flexibility in parameter tuning for different periods.

4. Reverse option adaptable to different markets.

5. Clear stops and exits control risk.

6. Relatively small drawdowns, tunable through parameters.

7. Potential to optimize with machine learning.

8. Overall good risk/reward profile for short-term trading.

### Risks

However, the main risks are:

1. Over-reliance on parameter optimization risks overfitting.

2. Lagging in moving average and oscillator. 

3. Lack of confirmation from other variables. 

4. Timing effect may degrade across changing markets.

5. Difficult to persistently generate alpha, requires frequent adjustments.

6. Need to monitor reward/risk ratios and curve smoothness. 

7. High trade frequency increases transaction costs.

8. Robustness across markets requires validation.

### Enhancements

Based on the analysis, enhancements may involve:

1. Testing different moving average parameters. 

2. Adding volume confirmation.

3. Implementing stops and exits to control risk.

4. Evaluating robustness across different markets and timeframes.

5. Rolling window backtesting for continual verification. 

6. Adjusting position sizing to lower frequency.

7. Incorporating machine learning for better parameters.

8. Optimizing overall risk management strategies.

9. Continual iterations to adapt to changing markets.

### Conclusion

In summary, this is a relatively simple mean-reversion strategy idea. Proper parameter tuning can yield decent results. But preventing overfitting and achieving persistent success require ongoing backtesting, optimization and enhancements from multiple dimensions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|false|Trigger|
|v_input_3|true|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-23 00:00:00
end: 2023-09-22 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version = 2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 05/12/2016
// DiNapoli Detrended Oscillator Strategy
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="DiNapoli Detrended Oscillator Strategy Backtest")
Length = input(14, minval=1)
Trigger = input(0)
reverse = input(true, title="Trade reverse")
hline(Trigger, color=gray, linestyle=line)
xSMA = sma(close, Length)
nRes = close - xSMA
pos = iff(nRes > Trigger, 1,
	   iff(nRes <= Trigger, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
         iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
plot(nRes, color=blue, title="DiNapoli")
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
```

> Detail

https://www.fmz.com/strategy/427679

> Last Modified

2023-09-23 15:48:40
