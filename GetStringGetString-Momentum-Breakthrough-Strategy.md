
> Name

Momentum BreakthroughGetString StrategyGetString-Momentum-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/151ace47202424afa7d.png)

[trans]

## Overview
This strategy comprehensively uses multiple indicators such as moving averages, CCI indicators, PSAR indicators, and ADX trend index to achieve a typical breakthrough strategy. Go long when there is a clear long signal in the market, and go short when there is a clear short signal, which is very suitable for short- and medium-term operations.
## Principle
The entry conditions for this strategy include the following aspects:
1. Moving average: It is required that the 5-day line crosses the 10-day line, the 10-day line crosses the 20-day line, and the 20-day line crosses the 40-day line. This can effectively filter out most false breakthroughs. 
2. CCI indicator: When the CCI indicator is less than -100, it is a long entry signal, and when it is greater than 100, it is a short entry signal.
3. PSAR point direction indicator: The direction of the PSAR point indicator is required to be consistent with the direction of the price trend. 
4. In terms of ADX dynamic indicators: ADX is required to be greater than 20, which means that it is currently in a trending market and is suitable for using a breakthrough system.
At the same time, the exit conditions also take into account multiple indicators:
1. Moving average: Contrary to the entry conditions, if the 5-day line crosses below the 10-day line, it is a signal to close the position.
2. The CCI indicator and PSAR point indicator are also opposite to the entry conditions. If the CCI indicator is greater than 100, long positions will be closed.
In this way, the entry of the strategy is relatively strict and the exit is relatively loose, so that a relatively high profit rate can be obtained.
## Advantages
This is a typical multi-index combination breakthrough strategy, which has the following advantages:
1. Strict entry conditions and the use of multiple indicator filters can reduce the risk of false breakthroughs.
2. The indicator parameters have been optimized and have good adaptability to the market.
3. Use trend judgment indicators to avoid being trapped in volatile markets.
4. The moving average is used to determine the short- and medium-term trend, which is relatively stable.
5. The CCI indicator can capture short-term overbought and oversold phenomena.
6. The PSAR point indicator has a strong ability to judge the direction of market trends.
## Risk
This strategy also has the following risks:
1. In extreme market conditions, the effect of multiple indicator combinations will be compromised and risks cannot be comprehensively filtered.
2. When the trend is huge, using short- and medium-term indicators to judge the timing may be ineffective and the trend cannot be fully captured.
3. Improper setting of local indicator parameters such as CCI may lead to missed opportunities.
4. The PSAR indicator does not work well at trend turning points.
Countermeasures:
1. The entry conditions can be appropriately relaxed and more costs should be paid in exchange for lower risks.  
2. Add indicators for longer line segments, such as 60-day or even longer moving averages.
3. Dynamically optimize CCI and other parameters.
4. Combine with more indicators to judge the trend, such as Bollinger Bands.
## Optimization direction
This strategy also has the following optimization directions:
1. Add machine learning algorithms to optimize parameters in real time and improve the adaptability of parameters.
2. Add model combination technology and combine more non-correlated strategies to improve stability.
3. Introducing risk control mechanisms, such as stop-loss strategies, can effectively control single stop-loss.
4. Add a trend judgment module to avoid falling into volatile market conditions.
5. Optimize the weight of indicators so that the best indicators play a leading role in different market environments.
## Summarize
This strategy is generally a typical and classic multi-indicator breakthrough strategy. Its advantage is that the entry conditions are strict, the exit conditions are loose, and it includes a trend judgment module. However, there are also certain risks and need to be continuously optimized so that it can adapt to a more complex market environment. Model combination and parameter optimization are both its development directions.
||


## Overview  

This strategy combines moving average, CCI indicator, PSAR indicator and ADX trend index to implement a typical breakthrough strategy. It goes long when there is a clear bullish signal and goes short when there is a clear bearish signal, which is very suitable for medium and short-term operations.

## Principles

The entry conditions of the strategy include the following aspects:

1. Moving average: requiring 5-day line breaking through 10-day line, 10-day line breaking through 20-day line and 20-day line breaking through 40-day line, which can effectively filter out most false breakthroughs.

2. CCI indicator: requiring CCI indicator less than -100 as the long signal, and greater than 100 as the short signal.  

3. PSAR indicator: requiring the direction of PSAR indicator to be consistent with the trend direction determined by the price.  

4. ADX indicator: requiring ADX greater than 20, indicating the market is now in a trend, which is suitable for using breakthrough systems.

At the same time, the exit conditions also take multiple indicators into consideration: 

1. Moving average: the opposite of entry conditions. For example, 5-day line breaking down 10-day line is the signal of closing positions.

2. CCI and PSAR indicators have opposite meanings to entry conditions. For example, CCI greater than 100 is the signal for closing long positions.

So the entry is strict while the exit is loose for this strategy, which can obtain a relatively high rate of return.

## Advantages

This typical multi-indicator combined breakthrough strategy has the following advantages:

1. The strict entry conditions adopt multiple indicators for filtering, which can reduce the risk of false breakthroughs. 

2. The indicator parameters are optimized for good adaptability to the market.

3. The trend judgment indicator is adopted to avoid being trapped in the shock market.  

4. Moving averages are used to determine medium and short term trends stably.

5. CCI indicator can capture short-term overbought and oversold phenomena. 

6. PSAR indicator has strong ability to determine the direction of market trends.

## Risks

The strategy also has the following risks:

1. In extreme markets, the effects of multiple indicator combinations may be compromised and cannot fully filter out risks.

2. When the trend is huge, using medium and short-term indicators to determine the timing may fail and cannot fully capture the trend.  

3. Improper parameter settings of local indicators like CCI may lead to missing opportunities.  

4. The effect of PSAR indicator is poor at trend turning points.

Counter measures:

1. Appropriately relax entry conditions and pay more cost for lower risk.

2. Increase judgment of longer-term indicators, such as 60-day or even longer moving averages.  

3. Dynamically optimize parameters like CCI. 

4. Combine more indicators to judge trends, such as Bollinger Bands.

## Optimization Directions 

The strategy also has the following optimization directions:

1. Increase machine learning algorithms to realize real-time parameter optimization and improve adaptability.  

2. Increase model combination techniques, combine more non-correlated strategies to improve stability.

3. Introduce risk control mechanisms, such as stop loss strategies, to effectively control single stop loss.

4. Increase trend judgment module to avoid getting into shock markets.  

5. Optimize indicator weights so that the optimal indicators play a leading role under different market environments.

## Conclusion

In general, this strategy is a typical and classic multi-indicator breakthrough strategy. Its advantages are rigorous entry conditions, loose exit conditions, and it also contains a trend judgment module. But it also has some risks. It needs continuous optimization to adapt to more complex market environments. Model combination and parameter optimization are its development directions.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-14 00:00:00
end: 2023-11-21 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Bukan Kaleng Kaleng Li", shorttitle="BKKL", overlay=true)

psarDot = sar(0.01, 0.01, 0.2)
up = change(high)
down = -change(low)
plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
trur = rma(tr, 14)
plus = fixnan(100 * rma(plusDM, 14) / trur)
minus = fixnan(100 * rma(minusDM, 14) / trur)
sum = plus + minus
adx = 100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), 14)

longConditionSMA4020 = sma(close, 40) > sma(close, 20)
longConditionSMA2010 = sma(close, 20) > sma(close, 10)
longConditionSMA105 = sma(close, 10) > sma(close, 5)
longConditionSMA = longConditionSMA4020 and longConditionSMA2010 and longConditionSMA105
longConditionCCI = cci(close, 20) < -100
longConditionPSAR = psarDot > close
longConditionDMI = plus < 10
adxCondition = adx > 20

longCondition = longConditionSMA and longConditionCCI and longConditionPSAR and longConditionDMI
if (longCondition and adxCondition)
    strategy.order("Long Signal", true)

shortConditionSMA4020 = sma(close, 40) < sma(close, 20)
shortConditionSMA2010 = sma(close, 20) < sma(close, 10)
shortConditionSMA105 = sma(close, 10) < sma(close, 5)
shortConditionSMA = shortConditionSMA4020 and shortConditionSMA2010 and shortConditionSMA105
shortConditionCCI = cci(close, 20) > 100
shortConditionPSAR = psarDot < close
shortConditionDMI = minus < 10

shortCondition = shortConditionSMA and shortConditionCCI and shortConditionPSAR and shortConditionDMI
if (shortCondition and adxCondition)
    strategy.order("Short Signal", false)

```

> Detail

https://www.fmz.com/strategy/432894

> Last Modified

2023-11-22 15:31:26
