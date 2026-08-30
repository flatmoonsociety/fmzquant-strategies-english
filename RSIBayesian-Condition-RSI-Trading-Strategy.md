
> Name

RSI trading strategy using Bayesian conditional judgment Bayesian-Condition-RSI-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9e75fbc8a1b5e34401.png)

[trans]

## Overview
This article mainly analyzes a quantitative trading strategy called "RSI trading strategy using Bayesian conditional judgment". This strategy calculates the probability distribution of the RSI indicator and applies Bayes' rule to calculate the probability that the RSI indicator will continue to rise or fall, in order to determine the future price trend and achieve profits.
## Strategy Principle
The core logic of this strategy is:
1. Calculate the probability distribution A of whether the closing price rises within a certain period
2. Calculate the probability distribution B of whether the RSI indicator continues to rise during the corresponding period
3. Apply Bayes’ rule to calculate the probability that A and B occur at the same time.
4. When the probability is higher than the threshold, it is judged that the trend will continue and a trading signal is taken.
Specifically, the strategy first defines parameter p as the period parameter for calculating the RSI indicator, and r as the time range for predicting future price changes. Then in period p, count the number of times whether the closing price rises, and calculate the probability distribution A. At the same time, in the p period, count the number of times whether the RSI continues to rise in the r period after the end of the period, and calculate the probability distribution B.
After that, the Bayes' rule formula is applied to calculate the probability of meeting the two conditions of "the closing price rises" and "the RSI continues to rise" at the same time, as the final probability judgment indicator. When the probability is higher than the given threshold, it is judged that the trend will continue to rise, and a long transaction is taken; when the probability is lower than the threshold, the trend is judged to be reversed, and the position is closed.
In this way, the strategy comprehensively considers price information and technical indicator information, applies probability statistics and Bayes' rule, makes judgments on future trends, and generates trading signals.
## Strategic Advantages
This strategy mainly has the following advantages:
1. **Combining a variety of information**: The strategy not only considers price information, but also combines technical indicator information such as RSI to comprehensively judge future trends and improve judgment accuracy.
2. **Probability Forecast**: Make probability predictions on the change direction of price and RSI through statistical probability distribution, instead of simple numerical comparison, making the judgment more scientific.
3. **Bayesian Optimization**: Use Bayes' rule to calculate relevant probabilities and optimize the original statistical probabilities to make the judgment more accurate.
4. **Flexible parameters**: Provides a variety of parameters for adjustment and optimization, and can perform parameter fitting for different markets and assets to improve strategy adaptability.
5. **Simple and effective**: The strategy idea is clear, and the trading signal judgment is realized through simple statistics and probability operations. It is easy to understand and optimize, and the effect is obvious.
## Strategy Risk
This strategy also has the following main risks:
1. **Parameter dependence**: The strategy effect depends on parameter settings. Different markets require a large number of parameters to be adjusted to achieve the best results, which increases the difficulty of strategy operation and maintenance.
2. **Probability Error**: Due to limited statistical time and samples, the calculated probability may not be consistent with the real trend, resulting in biased judgment.
3. **Special events**: Major emergencies may affect the correlation between market prices and RSI indicators, making the strategy ineffective.
4. **Technical indicator failure**: Under certain market conditions, technical indicators such as RSI may produce failure signals, leading to failure in strategic judgment.
Solutions to corresponding risks include: optimizing the parameter setting process, adjusting statistical time and sample size, combining more auxiliary information, manual intervention in abnormal situations, etc.
## Strategy optimization
The main optimization directions of this strategy are:
1. **Multiple time frames**: You can run strategies on multiple time periods (daily, weekly, etc.), make comprehensive judgments, and improve stability.
2. **More indicators**: Add more technical indicator signals, such as K-line patterns, moving averages, etc., to enrich the basis for judgment.
3. **Model Optimization**: Apply methods such as machine learning to optimize the Bayesian model to make calculations more accurate.
4. **Dynamic parameters**: Add a dynamic optimization module for parameters so that parameters can be adjusted according to real-time market changes.
5. **Risk control mechanism**: Set risk control indicators such as maximum drawdown and order frequency to avoid huge losses in extreme markets.
6. **Integration Improvement**: Integrate with other types of strategies or models to form a voting mechanism and improve the stability of judgment.
## Summarize
This strategy first counts the probability distribution of price and RSI indicators, then uses Bayes' rule to calculate the composite probability, and generates trading signals when the probability is higher than a given threshold to achieve profits. This strategy integrates multi-source information, applies probability prediction and Bayesian optimization, and has better judgment results. The main optimization directions include time frame expansion, indicator increase, parameter dynamization, etc. Overall, this strategy has unique ideas and significant effects, and is worth exploring and applying.
||

## Overview

This article mainly analyzes a quantitative trading strategy called "Bayesian Condition RSI Trading Strategy". This strategy calculates the probability distribution of the RSI indicator and applies Bayesian rule to infer the probability of the RSI indicator continuing to rise or fall to judge future price trends and make profits.

## Strategy Principle 

The core logic of this strategy is:

1. Calculate probability distribution A of whether the closing price has risen within a certain cycle
2. Calculate probability distribution B of whether the RSI indicator continues to rise within the corresponding cycle
3. Apply Bayesian rule to calculate the probability of A and B occurring simultaneously
4. When this probability is higher than the threshold, judge that the trend will continue and take trading signals

Specifically, the strategy first defines the parameter p as the cycle parameter for calculating the RSI indicator, and r as the time range for predicting future price changes. Then within the p cycle, count the number of times the closing price rises to calculate the probability distribution A. At the same time, within the p cycle, count the number of times the RSI continues to rise within the r cycle after this cycle ends, and calculate the probability distribution B.

After that, apply the Bayesian formula to calculate the probability that the two conditions of "closing price rise" and "RSI continue to rise" are satisfied at the same time, as the final probability judgment indicator. When this probability is higher than a given threshold, judge that the uptrend will continue and take long positions; when the probability is lower than the threshold, judge that the trend is reversed and close positions.

In this way, the strategy comprehensively considers price information and technical indicators, applies probability statistics and Bayesian rules to judge future trends and generate trading signals.

## Advantages of the Strategy

The main advantages of this strategy are:

1. **Combining multiple information**: The strategy considers not only price information, but also technical indicator information such as RSI to comprehensively judge future trends and improve judgment accuracy.

2. **Probability prediction**: Make probability predictions on the direction of price and RSI changes through statistical probability distribution, instead of simple numerical comparison, making the judgment more scientific.

3. **Bayesian optimization**: Use Bayesian rules to calculate relevant probabilities and optimize original statistical probabilities to make judgments more accurate.

4. **Flexible parameters**: Provide multiple parameters for adjustment and optimization to fit different markets and assets and improve adaptability of the strategy.

5. **Simple and effective**: The strategy idea is clear and simple statistical and probability operations are used to generate trading signal judgments, which is easy to understand and optimize, and the effect is significant.

## Risks of the Strategy  

The main risks of this strategy also include:

1. **Parameter dependence**: The performance relies heavily on parameter settings. Different markets need to adjust many parameters to achieve optimal results, increasing complexity of strategy operation.

2. **Probability error**: Due to limited statistical time and samples, the calculated probability may not match the real trend, leading to judgment deviation.  

3. **Special events**: Major emergencies may affect the correlation between market prices and RSI indicators, causing strategy failure.

4. **Technical indicator failure**: In some market situations, technical indicators like RSI may produce invalid signals, leading to strategy judgment failure.

Solutions include: optimizing parameter setting process, adjusting statistical time and sample size, combining more auxiliary information, manual intervention in abnormal situations, etc.

## Optimization Directions

The main optimization directions of this strategy include:

1. **Multiple timeframes**: Running strategies across multiple timeframes (daily, weekly etc) for integrated judgment to improve stability.  

2. **More indicators**: Adding more technical indicator signals like candlestick patterns, moving averages etc to enrich basis for judgment.

3. **Model optimization**: Using machine learning etc to optimize the Bayesian model for more accurate calculations.  

4. **Dynamic parameters**: Adding dynamic optimization modules for parameters to adjust in real-time with market changes.

5. **Risk control mechanism**: Setting risk metrics like maximum drawdown and trade frequencies to prevent huge losses in extreme markets.

6. **Ensemble improvements**: Ensemble with other strategy types or models to form voting mechanisms and improve stability.

## Conclusion

This strategy first statistically calculates probability distributions of price and RSI, then uses Bayesian rules to compute combined probabilities, generating trading signals when probabilities exceed set thresholds, thus profiting. This strategy combines multi-source information, leverages probability prediction and Bayesian optimization for decent judgment performance. Main optimization directions include timeframe expansion, more indicators, dynamic parameters etc. In conclusion, this strategy has a unique idea and remarkable effect that is worth exploring and applying.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|Period|
|v_input_2|1.003|Movement Thresh|
|v_input_3|7|Look Range|
|v_input_4|8|Jump|
|v_input_5|3|SM|
|v_input_6|14|RSIP|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-11 00:00:00
end: 2023-03-15 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
// Stealthy7 trading scripts are radikal. You have entered the mystical realm of demonic profit.
// If you like this script, check out my bots at cryptotrader.org/?r=51
// Let me know if you find any improvements to this script. It is beta. 
// Please subscribe.
strategy("Stealthy7 Bayes Conditional RSI Trader Strategy", overlay=true)
p = input(title="Period",  defval=30, minval=5, maxval=500)
t = input(title="Movement Thresh", type=float, defval=1.003, minval=1.001, maxval=1.5, step=0.001)
r = input(title="Look Range",  defval=7, minval=1,maxval=500, step=1)
RSIT = input(title="Jump",  defval=8, minval=1,maxval=99, step=1)
BAYEST = input(title="SM",  defval=3, minval=1,maxval=99, step=1)
RSIP = input(title="RSIP",  defval=14, minval=2,maxval=100, step=1)
countup = 1
countdn = 1
countupS = 1
countdnS = 1
for i = p to 1
    if close[i]/close[i + r] > t
        countup := countup + 1
    else
        countdn := countdn + 1
    if close[i]/close[i + r] < 2 - t
        countupS := countupS + 1
    else
        countdnS := countdnS + 1

rsi = rsi(open,RSIP)

countup2 = 1
countup3 = 1
countup2S = 1
countup3S = 1
for i = p to 1
    if close[i]/close[i + r] > t and rsi[i + r + 1] > rsi[i + r + 2] + RSIT
        countup2 := countup2 + 1
    else
        countup3 := countup3 + 1
    if close[i]/close[i + r] < 2 - t and rsi[i + r + 1] < rsi[i + r + 2] - RSIT
        countup2S := countup2S + 1
    else
        countup3S := countup3S + 1

countup2b = countup2 / p
countup3b = countup3 / p
countupb = countup / p
countdnb = countdn / p

countup2bS = countup2S / p
countup3bS = countup3S / p
countupbS = countupS / p
countdnbS = countdnS / p
bayes = 0
bayes := ((countupb * countup2b) / ((countupb * countup2b) + (countdnb * countup3b))) * 100
bayesS = 0
bayesS := ((countupbS * countup2bS) / ((countupbS * countup2bS) + (countdnbS * countup3bS))) * 100
SN1 = sma(bayes,BAYEST)
SN2 = sma(bayesS,BAYEST)
shortCondition = crossunder(bayesS, SN2) //and rsi < 49
longCondition = crossover(bayes, SN1) //and rsi > 59
if (longCondition)
    strategy.entry("Long", strategy.long)
if (shortCondition)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/435763

> Last Modified

2023-12-18 17:09:00
