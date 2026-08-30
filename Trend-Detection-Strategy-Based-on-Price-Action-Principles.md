
> Name

Trend-Detection-Strategy-Based-on-Price-Action-Principles
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
The core idea of ​​this strategy is to determine the current trend direction based on the relationship between the high point and closing price of the K line, and smooth the results with a moving average. When there are more highs closing, it is judged as an upward trend, and when there are more lows closing, it is judged as a downtrend. This strategy is suitable for any digital assets with certain liquidity, and better results can be obtained through parameter optimization.
### Strategy Principles
This strategy uses the M-minute line, and based on the positional relationship between the closing price and the high and low points, it determines whether the M-minute K-line is a high closing type (closing price close to the high point), low closing type (closing price close to the low point), or ordinary type (closing price close to the middle).
Specifically, first calculate delt = high - close, which is the difference between the high point and the closing price, and height = high - low, which is the difference between high and low. If delt > height \* 2/3, it is judged to be a high closing type. If delt < height/3, it is judged to be a low closing type. Otherwise, it is a normal type.
Then count the number of high closing types, low closing types and ordinary types in the recent N K lines, calculate their proportions, and use EMA to smooth the three curves of rise, fall and middle. The rise curve represents the proportion of high-closing K-lines, the fall curve represents the proportion of low-closing K-lines, and the middle curve represents the proportion of ordinary K-lines.
When the rise curve crosses the fall curve, it means that the number of high-closing K-lines begins to increase. It is believed that the market has entered an upward trend and a long signal is issued. When the fall curve crosses the rise curve, it means that the number of low-closing K-lines begins to increase. It is believed that the market has entered a downward trend and a short signal is issued.
### Strategic Advantages
This strategy of judging trends based on price action has the following advantages:
1. The principle is clear, easy to understand and easy to master.
2. Do not rely on any indicators and judge the trend direction purely based on the characteristics of the price itself.
3. There are few configurable parameters, mainly N and EMA smoothing parameters, which are easy to optimize.
4. Can be widely applied to any digital assets with certain liquidity, including stocks, foreign exchange, cryptocurrency, etc.
5. The backtesting effect is good and risks can be strictly controlled.
6. It can be further optimized by combining trend lines, support and resistance and other technical methods.
7. Configurable stop loss strategy to control single loss.
### Strategy Risk
Although this strategy has certain advantages, it also has the following risks:
1. When the market is in a state of shock, K-line types switch frequently, which may produce false signals.
2. Improper setting of N and EMA parameters may lead to missing the trend or generating too many invalid signals.
3. When judging the trend direction purely based on the K-line type, there is a certain lag.
4. Unable to effectively filter common time-sharing graphics such as triangle convergence, flag shapes, etc., which may lead to the risk of reverse breakthroughs.
5. This strategy is a trend following strategy and cannot effectively capture reversal opportunities.
6. It is necessary to cooperate with stop loss to control the risk of loss, otherwise the single loss may be larger.
### Strategy optimization direction
In order to reduce risks and improve profit factors, this strategy can be optimized from the following aspects:
1. Combined with volatility indicators such as ATR, adjust parameter N and EMA smoothing parameters according to market volatility to avoid too many invalid signals in a volatile market.
2. Add Volume indicator judgment to filter out false breakthroughs when there is a large amount of volume.
3. Combine the trend line and key support and resistance levels to determine the trend direction and the authenticity of the breakthrough.
4. Add multiple time period judgments to avoid misjudgments in a single period.
5. Add a reversal pattern recognition module to promptly open positions in reverse when a significant reversal signal appears.
6. Optimize the stop loss strategy and set the stop loss range according to market volatility and risk appetite.
7. Add functions such as trailing stop loss and trailing stop loss to lock in profits and prevent profit taking.
### Summarize
This strategy is based on price action to determine the trend direction. The principle is clear, the backtesting effect is good, and it can be widely applied to digital asset transactions. However, there are certain limitations, and it is necessary to cooperate with stop loss and optimization to reduce risks. Overall, this strategy provides a simple and practical idea for quantitative trading, which is worth learning from. Through continuous optimization and combination, it is expected to obtain stable excess returns.
||


### Overview

The core idea of this strategy is to determine the current trend direction based on the relationship between the high point and closing price of K-line bars, and smooth the results using moving average lines. When there are more high closing bars, it is determined as an upward trend. When there are more low closing bars, it is determined as a downward trend. This strategy is suitable for any digital asset with certain liquidity, and better results can be obtained through parameter optimization.

### Strategy Logic

This strategy uses M-minute bars. According to the position relationship between the closing price and the high and low points, it is determined whether the M-minute K-line bar belongs to a high closing type (closing price close to high point), low closing type (closing price close to low point) or normal type (closing price close to middle).

Specifically, first calculate delt = high - close, which is the difference between the high point and the closing price, and height = high - low, which is the difference between high and low. If delt > height * 2/3, it is determined as a high closing type. If delt < height/3, it is determined as a low closing type, otherwise it is a normal type. 

Then count the number of high closing, low closing and normal types in the most recent N K-line bars, calculate the percentage they account for, and use EMA to smooth them into rise, fall and middle curves. The rise curve represents the percentage of high closing bars, the fall curve represents the percentage of low closing bars, and the middle curve represents the percentage of normal bars.

When the rise curve crosses above the fall curve, it means that high closing bars begin to increase, indicating the market is entering an upward trend, and a long signal is issued. When the fall curve crosses below the rise curve, it means low closing bars begin to increase, indicating the market is entering a downward trend, and a short signal is issued.

### Advantages of the Strategy

This price action based trend judgment strategy has the following advantages:

1. The principle is clear and easy to understand and master.

2. It does not rely on any indicators, but purely judges the trend direction based on the characteristics of the price itself.

3. There are few configurable parameters, mainly N and EMA smoothing parameters, which are easy to optimize.

4. It can be widely applied to any digital asset with certain liquidity, including stocks, forex, cryptocurrencies, etc.

5. The backtest results are good, and risks can be strictly controlled. 

6. It can be further combined with trendlines, support/resistance levels and other technical methods for optimization.

7. Stop loss strategies can be configured to control single loss.

### Risks of the Strategy

Despite the advantages, the strategy also has the following risks:

1. When the market is in a shock state, the K-line type switches frequently, which may generate false signals.

2. Improper N and EMA parameter settings may lead to missing trends or too many invalid signals.

3. Judging the trend direction solely based on K-line types has some lag. 

4. It cannot effectively filter common chart patterns like triangle convergence, flags, etc., with the risk of reverse breakthroughs.

5. This strategy belongs to trend following, and cannot effectively capture reversal opportunities.

6. Stop loss should be used to control the risk of loss, otherwise single loss can be large.

### Directions for Strategy Optimization

To reduce risks and improve profitability, the strategy can be optimized in the following aspects:

1. Combine volatility indicators like ATR to adjust N and EMA parameters based on market volatility, avoiding excessive invalid signals in range-bound markets.

2. Add Volume analysis to filter false breakouts in high volume conditions.

3. Combine trendlines and key support/resistance levels to determine trend direction and breakthrough authenticity.

4. Add multiple timeframe analysis to avoid misjudgments on a single timeframe.

5. Add pattern recognition modules to reverse positions in a timely manner when significant reversal signals appear.

6. Optimize stop loss strategies based on market volatility and risk preference. 

7. Add trailing stop loss, moving stop loss etc. to lock in profits and prevent giving back.

### Summary

This strategy judges trend direction based on price action. The logic is clear and backtest results are good. It can be widely applied to crypto trading. But there are also some limitations. It needs to be combined with stop loss and optimizations to reduce risk. Overall, this strategy provides a simple and practical idea for quant trading and is worth learning from. With continuous optimizations and combinations, stable excess returns can be achieved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|34|lenght|
|v_input_2|5|ema_smooth|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-20 00:00:00
end: 2023-09-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("trend detect", overlay=false)


lenght = input(34)
ema_smooth = input(5)

delt = high - close
height = high - low

color_plot=black
state=0

if delt > height/3*2
    state := 1
    color_plot := red
else
    if delt > height/3
        state := 2
        color_plot := blue
    else 
        state := 3
        color_plot := green
//plot(state, color=color_plot, style=histogram)
percOfType(len, state_for_count) =>
    num = 0
    for i=1 to len
        if state[i]==state_for_count
            num := num+1
    num/len*100
    
rise = ema(percOfType(lenght, 3), ema_smooth)
fall = ema(percOfType(lenght, 1), ema_smooth)
plot(rise, color = green)
plot(ema(percOfType(lenght, 2), ema_smooth), color = blue)
plot(fall, color = red)
plot(10, color=black)
plot(60, color=black)

longCondition = crossover(rise, fall)
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = crossunder(rise, fall)
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)
```

> Detail

https://www.fmz.com/strategy/427342

> Last Modified

2023-09-20 11:11:46
