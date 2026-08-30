
> Name

Mean-Reversal-Breakout-Strategy in Buying
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
The core idea of ​​this strategy is to buy when the short-term moving average breaks upward during the session to capture the opportunity for short-term trend reversal.
### Strategy Principles
1. Define the buying condition: when the low price breaks the downward short-term SMA
2. Buy signal: When the buying conditions are established, enter the market long
3. Stop loss EXIT: By default, the position will be closed after 20 K lines
Specifically, this strategy calculates the intersection of a low price with a smoothness moving average as a buy signal. When the low price falls below the SMA moving average from above, a buy signal is generated. Then unconditionally close the position and stop the loss after 20 K lines.
This strategy attempts to capture short-term reversal opportunities. When the price falls to a certain level, the short-term SMA provides support, the bullish power may regain dominance, and the price may rebound. Buying at this time can make a rebound profit.
### Advantage Analysis
1. The strategy idea is simple and intuitive, easy to understand and implement, and suitable for beginners
2. Taking advantage of the support of short-term moving averages, there is a certain probability of capturing reversal opportunities.
3. No need to choose specific varieties, it can be widely applied to different markets
4. Moving average parameters can be flexibly adjusted to adapt to different cycles
5. Clear stop loss, single loss can be controlled
### Risk Analysis
1. Reverse the risk of failure. After the price breaks through the moving average, it may continue to fall rather than rebound.
2. Risk of frequent stop loss. High number of reversals leads to frequent stop losses
3. Parameter optimization risks. Parameters need to be adjusted for different varieties and cycles, otherwise the effect may be poor.
4. Transaction cost risk. Frequent transactions will increase transaction costs
The above risks can be reduced by optimizing stop-loss strategies, introducing trend filters, and appropriately easing positions.
### Optimization direction
1. Optimize the stop loss method to track real-time price changes and avoid being trapped by the default fixed stop loss.
2. Increase trend judgment, only buy when the trend turns, and avoid counter-trend transactions.
3. Consider increasing re-entry opportunities and adding positions multiple times during the rebound.
4. Test the impact of different moving average parameters on the effect and find the best parameter combination
5. Evaluate the parameter effects of different varieties and establish a parameter optimization system
6. Compare the impact of the number of stop loss bars and optimize the stop loss strategy
### Summarize
This strategy is a simple short-term reversal strategy, using the moving average breakthrough pattern as a buying opportunity. The advantage is that it is simple and easy to operate and can be widely used; the disadvantage is that it is easy to stop losses and there is a risk of reversal failure. Single losses can be controlled through strict stop loss, and then the strategy rules can be optimized to improve trend judgment and re-entry to reduce risks and improve results. This strategy is suitable for beginners who are familiar with basic trading strategy ideas to learn and optimize.
|| 

### Overview

The core idea of this strategy is to buy when there is an upward breakout of the short-term moving average during the session, in order to capture opportunities for short-term trend reversals.

### Strategy Logic

1. Define buy condition: When the low price breaks below the downward short-term SMA
2. Buy signal: Go long when the buy condition is met
3. Stop loss EXIT: Default exit after 20 bars 

Specifically, the strategy calculates the crossover between the low price and the SMA of length smoothness as the buy signal. When the low price breaks down from above across the SMA line, a buy signal is generated. Then it exits unconditionally after 20 bars.

The strategy attempts to capture short-term reversal opportunities. When the price falls to a certain level, the short-term SMA provides support, and the bullish forces could take over again, pushing the price to bounce back. Buying at this time could gain profits from the pullback.

### Advantage Analysis

1. The strategy idea is simple and intuitive, easy to understand and implement, suitable for beginners
2. Utilizes the support of short-term moving averages, has some probability of capturing reversal opportunities  
3. No need to select specific products, can be widely applied across different markets
4. Flexible adjustment of MA parameters to adapt to different cycles
5. Clear stop loss controls single trade loss

### Risk Analysis

1. Failed reversal risk. Price may continue to fall after breaking the MA instead of bouncing back
2. Frequent stop loss risk. High reversal frequency leads to frequent stop loss
3. Parameter optimization risk. Different products and cycles need parameter tuning, otherwise the results may be poor
4. Transaction cost risk. Frequent trading increases transaction costs

Risks can be reduced by optimizing stop loss strategy, adding trend filter, allowing loose holding position etc.

### Optimization Directions

1. Optimize stop loss methods to track price changes in real time, avoid fixed stop loss being trapped
2. Add trend judgment, only buy when the trend turns around, avoiding counter-trend trading
3. Consider adding re-entry opportunities, pyramiding during pullback
4. Test the impact of different MA parameters on results to find optimal parameter combinations
5. Evaluate parameter effectiveness across different products, build parameter optimization system
6. Compare impact of different stop loss bar quantities, optimize stop loss strategy

### Summary

This is a simple short-term mean reversal strategy, using MA breakout as entry timing. The advantages are being simple and widely applicable; the disadvantages are vulnerablility to stop loss and failed reversal risks. Risks can be managed through strict stop loss control, and the strategy can be improved by optimizing rules around trend filters, re-entry etc. It is suitable for beginners to learn and optimize such basic strategy ideas.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|Dipness|
|v_input_2|10|Smoothing|
|v_input_3|20|Exit After This Many Bars|


> Source (PineScript)

``` pinescript
//@version=3
strategy(title="Buy The Dip", shorttitle="BTFD", overlay=true)
dipness = input(title="Dipness",defval=2)
smoothness = input(title="Smoothing",defval=10,minval=0)
lookforward = input(title="Exit After This Many Bars", defval=20)

thedip = low - (atr(20) * dipness)
thedipsma = sma(thedip,smoothness)

buyCondition = crossunder(low,thedipsma)

if (buyCondition)
    strategy.entry("long", strategy.long)
    
strategy.close("long",when=buyCondition[20]) 

plot(thedipsma)
```

> Detail

https://www.fmz.com/strategy/427438

> Last Modified

2023-09-21 10:35:47
