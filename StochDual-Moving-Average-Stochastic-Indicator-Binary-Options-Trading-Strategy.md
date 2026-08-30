
> Name

Dual-Moving-Average-Stochastic-Indicator-Binary-Options-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/5b9e6d833e1744946693634dcabc3330ab25c289159c479066a8d73bf9302444.png)
[trans]


## Overview
This strategy combines double moving averages and the Stoch indicator to implement a simple and effective binary options trading strategy. This strategy simultaneously uses the price's high EMA, low EMA and closing price EMA to build a dual moving average system, and combines it with the Stoch indicator to send trading signals to capture short-term price fluctuations in binary options.
## Principle
This strategy is mainly based on the following principles:
1. Use the high EMA and low EMA of the price to construct the upper and lower rails, and hesesEMA lines as support and resistance levels.
2. Calculate the closing price EMA to determine the position of the price relative to the double moving average. If the closing price goes above the upper track or breaks below the lower track, it indicates a trend reversal.
3. Stoch indicator determines overbought and oversold conditions. Both the K value and the D value are below 50, indicating an oversold zone, and above 50, indicating an overbought zone.
4. According to the overbought and oversold zone of the Stoch indicator and the reversal signal of the price breaking through the upper and lower rails, short-term buying and selling operations can be carried out.
The specific trading rules are as follows:
- If the closing price is lower than the lower track and the opening price is lower than the midpoint of the double moving average, and the Stoch indicator shows the oversold zone (K<50, D<50), go long;
- If the closing price is above the upper track and the opening price is above the midpoint of the double moving average, and the Stoch indicator shows the overbought zone (K>50, D>50), go short.
## Advantage Analysis
This strategy combines double moving averages and Stoch indicators, which can effectively capture the short-term trend reversal of binary option prices and has the following advantages:
1. The moving average system filters out shocks, and the Stoch indicator determines overbought and oversold to improve accuracy.
2. The trading rules are simple, clear and easy to implement.
3. High capital utilization efficiency, only holding positions in one direction at a time.
4. The retracement is controllable to avoid unnecessary losses.
5. Easy to optimize, the moving average parameters and Stoch input values ​​can be adjusted.
## Risk Analysis
Although this strategy has certain advantages, it also has the following risks:
1. The probability of false breakthroughs of double moving averages may lead to missing a strong trend or reversal.
2. There is a lag in the Stoch indicator, and the trend may have reversed when the signal is sent.
3. Unable to adapt to sharp market fluctuations and should avoid major events.
4. Improper parameter settings may lead to excessive trading frequency or insufficient signals.
5. It is impossible to accurately predict the price trend of binary options, and there is a certain risk of loss.
Corresponding risks can be reduced by adjusting parameters, optimizing rules, and strictly stopping losses. In addition, it is necessary to consider the matching relationship between the account fund size and the stop loss point, and control the single loss and maximum drawdown.
## Optimization direction
This strategy also has the potential for further optimization. The main directions are as follows:
1. Add other indicator filters, such as MACD, RSI, etc., to improve signal accuracy.
2. Add trend indicators to judge and avoid trading against the trend.
3. Optimize the parameters of the moving average system and find the best length combination.
4. Adjust the overbought and oversold judgment conditions to reduce the Stoch lag problem.
5. Set dynamic stop loss or trailing stop loss.
6. Combine with relevant technical analysis tools to find the best entry opportunity.
7. Test the feasibility of arbitrage of different varieties.
Through the above optimization methods, the stability and profitability of the strategy can be further improved.
## Summarize
This strategy integrates the advantages of dual moving averages and Stoch indicators to form a simple and reliable short-term binary options trading strategy. It standardizes trading rules and helps with risk control. Although there is still some room for improvement, the idea is clear and easy to operate, making it an option worth considering. By optimizing parameter settings and rules, more ideal strategic effects can be achieved.

||


## Overview

This strategy combines dual moving averages and the Stochastic indicator to implement a simple and effective binary options trading strategy. It uses the EMA of high prices, EMA of low prices and EMA of closing prices to build a dual moving average system, and incorporates the Stochastic indicator to generate trading signals, in order to capture short-term price fluctuations in binary options.

## Principles 

The strategy is mainly based on the following principles:

1. Use the EMA of high prices and EMA of low prices to build upper and lower bands as support and resistance levels.

2. Calculate the EMA of closing prices to determine the relationship between price and dual moving averages. If the closing price crosses above the upper band or breaks below the lower band, it indicates a possible trend reversal.

3. The Stochastic indicator determines overbought and oversold conditions. K and D values below 50 indicate oversold while above 50 overbought. 

4. According to the overbought/oversold signals from Stochastic combined with price breakouts of the upper/lower bands, short-term buy/sell operations can be executed.

The specific trading rules are:

- If the closing price is below the lower band and the opening price is below the midpoint of the dual moving averages, while Stochastic shows oversold (K<50, D<50), go long.

- If the closing price is above the upper band and the opening price is above the midpoint of the dual moving averages, while Stochastic shows overbought (K>50, D>50), go short.

## Advantage Analysis

By combining dual moving averages and the Stochastic oscillator, this strategy can effectively capture short-term trend reversals in binary options prices, with the following advantages:

1. The moving average system filters out consolidation while Stochastic increases accuracy by determining overbought/oversold levels.

2. The trading rules are simple and clear, easy to implement.

3. High capital utilization efficiency, only hold one direction at a time.

4. Controllable drawdowns, avoid unnecessary losses.

5. Easy to optimize by adjusting moving average parameters and Stochastic inputs.

## Risk Analysis

Although this strategy has some merits, it also has the following risks:

1. There is a probability of false breakouts with the dual moving averages, potentially missing strong trends or reversals.

2. Stochastic has lagging issues, signals may come after trend reversals have already begun.

3. Cannot adapt to highly volatile markets, should avoid major events.

4. Improper parameter settings may lead to excessive trading frequency or insufficient signals.

5. Unable to accurately predict binary option price movements, has inherent loss risks.

Corresponding risks can be reduced by adjusting parameters, optimizing rules and strict stop loss. In addition, account size and stop loss levels should match to control single trade loss amount and maximum drawdown. 

## Optimization Directions

There is further optimization potential for this strategy:

1. Add other indicators for filtration, like MACD, RSI etc, to improve signal accuracy.

2. Incorporate trend indicators to avoid counter-trend trading.

3. Optimize moving average parameters to find the best length combinations.

4. Adjust overbought/oversold criteria to reduce Stochastic lag.

5. Set dynamic or trailing stop loss.

6. Combine relevant technical analysis tools to find optimal entry timing.

7. Test spread trading feasibility across different products.

Through the above optimization means, strategy stability and profitability can be further enhanced.

## Conclusion

This strategy integrates the advantages of dual moving averages and Stochastic oscillator into a simple and reliable short-term binary options trading strategy. It standardizes trading rules for better risk control. Although there is still room for improvement, its logic is clear and easy to implement, making it a viable choice worth considering. By optimizing parameters and rules, better strategy performance may be achieved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|length1|
|v_input_2|true|smoothK|
|v_input_3|3|smoothD|
|v_input_4|4|Length|
|v_input_5_high|0|Source: high|close|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_6|4|Length|
|v_input_7_low|0|Source: low|high|close|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_8|21|Length|
|v_input_9_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-07 00:00:00
end: 2023-11-14 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Binary Option EMA/Stoch strategy Corrected", overlay=true)

//stoch

length1 = input(14, minval=1), smoothK = input(1, minval=1), smoothD = input(3, minval=1)
k = sma(stoch(close, high, low, length1), smoothK)
d = sma(k, smoothD)


len = input(4, minval=1, title="Length")
src = input(high, title="Source")
out = ema(src, len)
HIGH = out

len1 = input(4, minval=1, title="Length")
src1 = input(low, title="Source")
out1 = ema(src1, len1)
LOW = out1


HL2 = (HIGH+LOW)/2

len2 = input(21, minval=1, title="Length")
src2 = input(close, title="Source")
out2 = ema(src2, len2)
EMA = out2


x = close < LOW and open < HL2 and close < EMA  and d < 50 and k < 50 

y =   close > HIGH and open > HL2 and close > EMA and d > 50 and k > 50

if (x)
    strategy.entry("UP", strategy.long)

if (y)
    strategy.entry("DOWN", strategy.short)
```

> Detail

https://www.fmz.com/strategy/432228

> Last Modified

2023-11-15 16:56:47
