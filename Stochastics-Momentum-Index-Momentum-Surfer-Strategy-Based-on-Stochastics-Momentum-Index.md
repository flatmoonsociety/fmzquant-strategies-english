
> Name

Momentum-Surfer-Strategy-Based-on-Stochastics-Momentum-Index-
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/150ec8c0936224d3b3c.png)
[trans]
## Overview
This article introduces a strategy for tracking stock trends based on the Stochastics Momentum Index (SMI) indicator. The strategy is called "Momentum Surfer Strategy". It uses the SMI indicator to identify overbought and oversold areas of a stock and buy and sell at trend reversal points to make a profit.
## Strategy Principle
The SMI indicator is used to identify overbought and oversold areas in a stock. When the SMI indicator enters the red zone, it indicates that the stock is oversold, and when it enters the green zone, it indicates that the stock is overbought. The trading signals for this strategy are derived from the crossover of the SMI indicator and its EMA.

Specifically, a buy signal is generated when the SMI indicator crosses above its EMA line and at this point the SMI value is in the oversold zone below -40. A sell signal is generated when the SMI indicator crosses below its EMA line and the SMI value is above 40 in the overbought zone.

In this way, this strategy can catch the signal in time when the stock price reverses, and achieve the purpose of buying low and selling high. This way you can track the rising and falling trends of stocks.
## Strategic advantage analysis
The biggest advantage of this strategy is that it can follow the trend of the stock. Because it uses the SMI indicator to identify entry and exit opportunities, it can capture signals when stock prices reverse.

In addition, the SMI indicator itself has the characteristics of smoothing prices. It responds more smoothly to price changes than indicators such as a simple moving average. This also makes the trading signals generated more reliable and less susceptible to short-term market noise.

Overall, this strategy successfully utilizes the advantages of the SMI indicator to achieve effective tracking of stock trends. It can help investors make profits and is also very suitable for automated trading.
## Risk Analysis
This strategy relies heavily on the SMI indicator, so it has some SMI-related risks.

First, the SMI indicator is sensitive to parameter settings. If the parameters are set improperly, the effect of the trading signals generated will be greatly reduced. This requires repeated testing by investors to determine the best combination of parameters.

In addition, SMI itself cannot completely avoid the occurrence of false trading signals. When the market fluctuates violently, it may generate false signals leading to unnecessary losses. This needs to be used in combination with other indicators to confirm trading signals and reduce the probability of wrong trading.

Finally, this strategy cannot change overall stock market risk. When the entire market enters a bear market, this strategy is still difficult to avoid large losses. This is a systemic risk that cannot be completely avoided by any technical analysis strategy.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Combine other indicators and use the advantages of indicator combination to reduce the probability of wrong trading signals and increase the probability of profit. For example, you can add fundamental factors, volatility indicators, etc.
2. Use machine learning methods to automatically optimize SMI parameters. Through a large amount of historical data training, find the optimal parameter combination.
3. Add a stop loss strategy. Reasonable stop loss can greatly reduce the impact of a single loss and reduce risks.
4. Combine with quantitative stock selection strategies to improve the overall quality of the stock pool. Good stock pool quality will directly improve the stability of the strategy.
## Summarize
This article details the Momentum Surfer strategy for trend following based on the SMI indicator. The biggest advantage of this strategy is that it can capture price reversals and track changes in stock trends. It also has some risks such as parameter setting sensitivity and signal reliability. We have given some optimization suggestions to further improve the effectiveness of the strategy. Overall, this strategy is very attractive for automated trading and deserves real-world verification.
||

## Overview

This article introduces a strategy to track stock trends based on the Stochastics Momentum Index (SMI) indicator. The strategy is called "Momentum Surfer Strategy". It identifies overbought and oversold areas with SMI and enters long/short to profit from trend reversals.

## Strategy Logic

The SMI indicator is used to identify overbought and oversold zones. Values in the red area indicate the stock is oversold while the green area means overbought conditions. The trading signals are generated from the crossover between SMI and its EMA line.


Specifically, a long signal is triggered when SMI crosses above its EMA and SMI is below -40 oversold level. A short signal is triggered when SMI crosses below its EMA and SMI is above 40 overbought level.  


By doing so, the strategy can capture the price reversal and implement buy low sell high. It surfs the uptrend and downtrend of stocks smoothly.

## Advantage Analysis  

The biggest advantage lies in its ability to follow trends. As it utilizes SMI to determine entry and exit points, the signals align perfectly with price reversals.


Also, SMI itself has the characteristic of smoothing prices. Compared to simple moving averages, it responds more steadily to price changes. The trading signals are more reliable without being easily affected by market noise.


In summary, the strategy successfully leverages the strength of SMI to effectively track stock trends. It generates profit while being suitable for algo trading.

## Risk Analysis

The strategy relies heavily on the SMI indicator, thus faces some associated risks.


Firstly, SMI is sensitive to parameter tuning. Incorrect parameters can significantly undermine the signal quality. Extensive testing is required to find the optimum.


Besides, no indicator is immune to false signals, including SMI. Whipsaws can happen during high volatility that causes unnecessary losses. Using SMI together with other indicators helps to confirm signals and reduce errors.


Finally, it does not mitigate systemic market risk. Severe losses are inevitable if the whole market plunges into a bear state. This limitation applies to all technical strategies. 

## Enhancement  

The strategy can be further improved from the following aspects:

1. Incorporate other indicators to form a syndicate system. It helps to increase signal reliability and profitability. Fundamental factors and volatility measures can be added.

2. Utilize machine learning to automatically optimize SMI parameters based on big historical data.

3. Add stop loss mechanisms. Reasonable stop loss enormously reduces single trade loss and avoids risks.  

4. Combine quantitative stock screening rules to improve the overall quality of the stock pool. Good stock selection lays the foundation of a robust strategy.

## Conclusion   

In this article, we introduce the Momentum Surfer strategy which tracks trends with the SMI indicator. Its biggest strength lies in capturing reversals and smoothly following the trends. Some risks like parameter sensitivity and signal quality are present. We suggest a few ways to enhance it. Overall speaking, the strategy is attractive for algo trading and worth real trading verification.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|10|Percent K Length|
|v_input_int_2|3|Percent D Length|
|v_input_int_3|40|Overbought|
|v_input_int_4|-40|Oversold|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Stochastics Momentum Index Strategy", shorttitle="Stoch_MTM_Doan", overlay=true)

// Input parameters
a = input.int(10, "Percent K Length")
b = input.int(3, "Percent D Length")
ob = input.int(40, "Overbought")
os = input.int(-40, "Oversold")

// Range Calculation
ll = ta.lowest(low, a)
hh = ta.highest(high, a)
diff = hh - ll
rdiff = close - (hh+ll)/2

avgrel = ta.ema(ta.ema(rdiff,b),b)
avgdiff = ta.ema(ta.ema(diff,b),b)

// SMI calculations
SMI = avgdiff != 0 ? (avgrel/(avgdiff/2)*100) : 0
SMIsignal = ta.ema(SMI,b)
emasignal = ta.ema(SMI, 10)

// Color Definition for Stochastic Line
col = SMI >= ob ? color.green : SMI <= os ? color.red : color.white

plot(SMIsignal, title="Stochastic", color=color.white)

plot(emasignal, title="EMA", color=color.yellow)

level_40 = ob
level_40smi = SMIsignal > level_40 ? SMIsignal : level_40

level_m40 = os
level_m40smi = SMIsignal < level_m40 ? SMIsignal : level_m40

plot(level_40, "Level ob", color=color.red)
plot(level_40smi, "Level ob SMI", color=color.red, style=plot.style_line)

plot(level_m40, "Level os", color=color.green)
plot(level_m40smi, "Level os SMI", color=color.green, style=plot.style_line)

//fill(level_40, level_40smi, color=color.red, transp=ob, title="OverSold")
//fill(level_m40, level_m40smi, color=color.green, transp=ob, title="OverBought")

// Strategy Tester
longCondition = ta.crossover(SMIsignal, emasignal) and (SMI < os)
if (longCondition)
    strategy.entry("Buy", strategy.long)

shortCondition = ta.crossunder(SMIsignal, emasignal) and (SMI > ob)
if (shortCondition)
    strategy.entry("Sell", strategy.short)

```

> Detail

https://www.fmz.com/strategy/442928

> Last Modified

2024-02-27 14:32:46
