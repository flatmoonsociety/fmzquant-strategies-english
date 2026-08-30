
> Name

Bollinger-Band-Dynamic-Take-Profit-and-Dynamic-Position-Adding-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/09745a44e9277fb82a6bbcc504ecdf6ecc5a7b67b4ef858883cb3f7edebfa6c3.png)
[trans]
## Strategy Overview
This strategy is based on the Bollinger Band indicator, opening a position when the price touches the upper and lower rails of the Bollinger Band, and setting up dynamic take-profit and dynamic position-adding logic. When the price rebounds from the lower track and breaks through the middle track of the Bollinger Bands, the strategy believes that an upward trend has formed. At this time, the strategy will increase the position when the price retraces to a certain proportion of the middle track; when the price finally breaks through the upper track of the Bollinger Bands, the strategy closes the position and takes profits. In a downtrend, the strategy adopts the opposite operating logic. Through Bollinger Bands' dynamic take-profit and dynamic position-adding, this strategy can gain more profits in trending markets.
## Strategy Principle
The main principles of this strategy are as follows:
1. Calculate the upper, middle and lower Bollinger Bands. The calculation formula of the upper rail and the lower rail is the middle rail plus or minus N times the standard deviation, where N can be customized.
2. When the closing price falls below the lower Bollinger Band and no position has been opened before, the strategy opens a long position; when the closing price breaks through the upper Bollinger Band and no position has been opened before, the strategy opens a short position. The position opening logic here is similar to the traditional Bollinger Bands breakout system.
3. After opening a long position, if the closing price breaks upward above the middle track of the Bollinger Bands, an upward trend is considered to be formed, and the mark variable basisCrossed is true. After opening a short position, if the closing price breaks through the middle track of the Bollinger Band downwards, basisCrossed will also be marked as true.
4. In the long case, if the closing price falls below the lower track and basisCrossed is true, and the current price drops by more than 2% from the original opening price, the strategy will increase the position and reset basisCrossed to false. The opposite is true for shorts. The logic of adding positions here can enable the strategy to add positions at low positions during trend retracements, increasing profit margins.
5. If the closing price breaks the upper Bollinger Band when holding a long position, or the closing price falls below the lower Bollinger Band when holding a short position, the strategy will close all positions, take profits, and reset each marker variable to prepare for the next opening of a position.
Through the above dynamic logic of opening, adding, and taking profits, this strategy can operate flexibly in trending markets and gain higher profits. At the same time, capturing the trend through the classic technical indicator Bollinger Bands also makes the strategy have certain adaptability and stability.
## Advantage Analysis
1. Dynamic take-profit: This strategy dynamically adjusts the take-profit level through the upper and lower rails of Bollinger Bands. Compared with fixed-point take-profit, it can better adapt to market fluctuations and flexibly protect profits.
2. Dynamic position increase: During the retracement stage after the trend is formed, the strategy will gradually increase the position, so as to gain higher profits in the trending market. Dynamic position addition makes this strategy more advantageous in trend trading.
3. Flexible parameters: Bollinger Band parameters such as N, P value, etc. can be flexibly adjusted to adapt to different market characteristics and trading styles.
4. Strong adaptability: Bollinger Bands is a classic technical indicator with good trend capturing ability. Combining it with dynamic position management can play a stable role in various financial markets.
5. Clear logic: The opening and closing conditions and position addition and subtraction logic of this strategy are very clear and easy for traders to understand and control. Clear logic also means it is easier to do secondary development and strategy optimization.
## Risk Analysis
1. Shocking markets: The Bollinger Band strategy often performs poorly in volatile markets. Frequent opening and closing of positions at this time will lead to more transaction costs, thus affecting overall returns.
2. Trend turning: At the critical moment of trend turning, this strategy may lag in judgment, resulting in adding positions in the wrong direction, resulting in a large retracement.
3. Extreme market conditions: In extreme market conditions (such as sharp rises and plummets), the trend of Bollinger Bands may be abnormal, causing the strategy to fail.
4. Parameter settings: Improper parameter settings will seriously affect the performance of the strategy. For example, if the N value is set too small, it will lead to frequent transactions, and if the N value is set too large, it will cause signal lag.
5. Black swan events: In the event of major political and economic events, this strategy may face greater risk exposure.
In view of the above risks, we can control them from two aspects: 1) Set parameters reasonably and optimize parameters according to different targets and market conditions; 2) Add more filtering conditions to the strategy, such as trend judgment, volatility filtering, etc., to improve the quality of signals. In addition, in actual application, it is also necessary to do a good job in position control and risk management, and strictly control the risk exposure of a single transaction.
## Optimization direction
1. Trend filtering: Add the logic of trend judgment when opening a position, such as MA long arrangement as the filtering condition for long, MA short arrangement as the filtering condition for shorting, which can improve the success rate of trend grasping.
2. Volatility filtering: Bollinger Bands is actually a volatility indicator. The volatility state of the market can be identified by introducing indicators such as ATR and historical volatility. Positions can be appropriately reduced in high-volume states and increased in low-volatility states, thereby better controlling risks.
3. Dynamic parameter optimization: Bollinger Bands parameters can be dynamically adjusted according to market conditions. For example, the N value can be increased in a trending market and reduced in a volatile market. This requires the help of machine learning and other technologies to find optimal parameters through training on historical data.
4. Combination strategy: This strategy can be combined with other classic strategies such as MACD, RSI, etc. to form a combination strategy to improve the robustness and profitability of the system.
5. Add stop-loss logic: Currently, this strategy lacks clear stop-loss logic. You can consider adding mechanisms such as trailing stop-loss or fixed percentage stop-loss to control the maximum loss in a single transaction.
6. Position management optimization: In the process of adding and reducing positions, you can learn from classic position management methods such as Kelly's formula and optimal F value, in order to maximize profits under controllable risks.
Through the above optimization, the risk-return ratio of this strategy can be further improved, allowing it to better adapt to the changing market environment and bring stable returns to traders.
## Summarize
The Bollinger Bands dynamic take-profit and dynamic position-adding strategy is a classic trend following strategy. It is based on Bollinger Bands and uses dynamic position adjustments to gain higher trend profits. This strategy has clear logic, flexible parameters and strong adaptability. It is a quantitative trading strategy worthy of in-depth study and application. But at the same time, we must also see that this strategy performs poorly in volatile markets and lacks the ability to respond to extreme market conditions and black swan events. This requires us to focus on parameter optimization, risk control and strategy combination in practical applications, and regularly test the effectiveness of the strategy under different market conditions. Through in-depth understanding of the internal logic of this strategy and continuous optimization and improvement, we believe that this strategy can become an important tool for quantitative traders and bring long-term and stable returns to investors.
|| 

## Strategy Overview

This strategy is based on the Bollinger Band indicator. It opens positions when the price reaches the upper or lower band, and sets up dynamic take profit and dynamic position adding logic. When the price rebounds from the lower band and breaks through the middle band, the strategy considers an uptrend has formed. At this time, the strategy will add positions when the price pulls back to a certain percentage of the middle band. When the price finally breaks through the upper band, the strategy closes positions to take profits. In a downtrend, the strategy adopts the opposite operating logic. Through dynamic take profit and dynamic position adding based on Bollinger Bands, this strategy can obtain more profits in trending markets.

## Strategy Principle

The main principles of this strategy are as follows:

1. Calculate the upper, middle and lower bands of Bollinger Bands. The upper and lower bands are calculated by adding and subtracting N times the standard deviation from the middle band, where N can be customized.

2. When the closing price breaks down the lower band and no position has been opened before, the strategy opens a long position; when the closing price breaks up the upper band and no position has been opened before, the strategy opens a short position. The opening logic here is similar to the traditional Bollinger Band breakout system.

3. After opening a long position, if the closing price breaks upward through the middle band, it is considered that an uptrend has formed, and the variable basisCrossed is marked as true. After opening a short position, if the closing price breaks downward through the middle band, basisCrossed is also marked as true.

4. In the case of a long position, if the closing price breaks down the lower band and basisCrossed is true, and the current price has fallen by more than 2% from the original opening price, the strategy adds positions at this time, and resets basisCrossed to false at the same time. The case of a short position is the opposite. The position adding logic here allows the strategy to add positions at a low level during a trend pullback, increasing the profit space.

5. If the closing price breaks through the upper band when holding a long position, or the closing price breaks down the lower band when holding a short position, the strategy closes all positions, takes profits, and resets various marker variables to prepare for the next opening.

Through the above dynamic opening, adding positions and taking profit logic, this strategy can flexibly operate in trending markets to gain higher profits. At the same time, using the classic technical indicator of Bollinger Bands to capture trends also gives the strategy a certain adaptability and stability.

## Advantage Analysis

1. Dynamic take profit: This strategy dynamically adjusts the take profit level through the upper and lower bands of Bollinger Bands. Compared with fixed point take profit, it can better adapt to market fluctuations and flexibly protect profits.

2. Dynamic position adding: In the pullback stage after the trend is formed, the strategy will gradually add positions, which can gain higher profits in trending markets. Dynamic position adding makes this strategy more advantageous in trend trading.

3. Flexible parameters: The parameters of Bollinger Bands, such as N and P values, can be flexibly adjusted to adapt to different market characteristics and trading styles.

4. Strong adaptability: Bollinger Band is a classic technical indicator with a good ability to capture trends. Combining it with dynamic position management, it can play a stable role in various financial markets.

5. Clear logic: The opening and closing conditions and the logic of adding and reducing positions of this strategy are very clear and easy to understand, which is convenient for traders to understand and control. Clear logic also means it is easier to do secondary development and strategy optimization.

## Risk Analysis

1. Oscillating market: Bollinger Band strategies often perform poorly in oscillating markets. At this time, frequent opening and closing of positions will lead to more transaction costs, which will affect the overall return.

2. Trend reversal: At the key moment of trend reversal, this strategy may experience lagging judgment, leading to adding positions in the wrong direction, resulting in a larger drawdown.

3. Extreme situations: In extreme situations (such as sharp rises and falls), the trend of Bollinger Bands may be abnormal, causing the strategy to fail.

4. Parameter settings: Inappropriate parameter settings will seriously affect the performance of this strategy. For example, setting the N value too small will lead to frequent transactions, and setting the N value too large will lead to signal lag.

5. Black swan events: If there are major political and economic events, this strategy may face greater risk exposure.

In order to control the above risks, we can start from two aspects: 1) Reasonably set parameters and optimize parameters for different targets and market conditions; 2) Add more filtering conditions to the strategy, such as trend judgment, volatility filtering, etc., to improve the quality of signals. In addition, in actual use, it is also necessary to do a good job in position control and risk management, and strictly control the risk exposure of a single transaction.

## Optimization Direction

1. Trend filtering: Add the logic of trend judgment when opening positions, such as using MA bullish arrangement as a filtering condition for going long, and MA bearish arrangement as a filtering condition for going short, which can improve the success rate of trend grasping.

2. Volatility filtering: Bollinger Bands are actually a kind of volatility indicator. Volatility indicators such as ATR and historical volatility can be introduced to identify the volatility state of the market. Positions can be appropriately reduced in high-volatility states and increased in low-volatility states, so as to better control risks.

3. Dynamic parameter optimization: The parameters of Bollinger Bands can be dynamically adjusted according to market conditions. For example, the N value can be increased in trending markets and decreased in oscillating markets. This requires the use of machine learning and other technologies to find the optimal parameters through training on historical data.

4. Combined strategies: This strategy can be combined with other classic strategies such as MACD and RSI to form combined strategies, improving the robustness and profitability of the system.

5. Add stop-loss logic: At present, this strategy lacks a clear stop-loss logic. We can consider adding mechanisms such as trailing stop or fixed percentage stop-loss to control the maximum loss of a single transaction.

6. Position management optimization: In the process of adding and reducing positions, classic position management methods such as the Kelly formula and optimal F value can be used to maximize profits under controllable risks.

Through the above optimizations, the risk-reward ratio of this strategy can be further improved, enabling it to better adapt to changing market environments and bring stable returns to traders.

## Summary

The Bollinger Band dynamic take profit and dynamic position adding strategy is a classic trend tracking strategy. Based on Bollinger Bands, it seeks higher trend profits by dynamically adjusting positions. This strategy has clear logic, flexible parameters, and strong adaptability. It is a quantitative trading strategy worthy of in-depth research and application. But at the same time, we must also see that this strategy performs poorly in oscillating markets and lacks the ability to deal with extreme situations and black swan events. This requires us to focus on parameter optimization, risk control and strategy combination in actual application, and regularly test the effectiveness of the strategy in different market conditions. By deeply understanding the internal logic of this strategy and continuously optimizing and improving it, I believe this strategy can become an important tool for quantitative traders and bring long-term and stable returns to investors.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|12|length|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|StdDev|
|v_input_int_2|false|Offset|
|v_input_float_2|0.98|add|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-01 00:00:00
end: 2024-03-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
//  Bollinger Bands 1Bb 상하한 크로스 롱숏 실행

strategy(shorttitle="BB", title="Bollinger Bands", overlay=true )
 // bb
length = input.int(12, minval=1)
src = input(close, title="Source")
mult = input.float(2.0, minval=0.001, maxval=50, title="StdDev")
basis = ta.sma(src, length)
dev = mult * ta.stdev(src, length)
upper = basis + dev
lower = basis - dev
offset = input.int(0, "Offset", minval = -500, maxval = 500)
plot(basis, "Basis", color=#FF6D00, offset = offset)
p1 = plot(upper, "Upper", color=#2962FF, offset = offset)
p2 = plot(lower, "Lower", color=#2962FF, offset = offset)
add = input.float(0.98, step = 0.001)
// plot(upper - lower, "Basis", color=color.red, offset = offset)
var bool entryMade = false
var bool basisCrossed = false
var bool upperCrossed = false
var bool lowerCrossed = false
strategy.initial_capital = 50000
if close < lower and not entryMade
    strategy.entry("롱", strategy.long, qty = strategy.initial_capital/10000)
    entryMade := true
if ta.crossover(close, basis) and entryMade and not upperCrossed
    basisCrossed := true
if close > upper
    upperCrossed := true
if close < lower and entryMade and basisCrossed and not upperCrossed and close < strategy.position_avg_price*add
    strategy.entry("추가롱", strategy.long, strategy.initial_capital/10000)
    basisCrossed := false
if close > upper
    strategy.close("롱")
    strategy.close("추가롱")
    entryMade := false
    basisCrossed := false
    upperCrossed := false
///////////반대 포지션
if close > upper and not entryMade
    strategy.entry("s", strategy.short, qty = strategy.initial_capital/10000)
    entryMade := true
if ta.crossunder(close, basis) and entryMade and not lowerCrossed
    basisCrossed := true
if close < lower
    lowerCrossed := true
if close > upper and entryMade and basisCrossed and not lowerCrossed and close > strategy.position_avg_price*add
    strategy.entry("추가s", strategy.short, strategy.initial_capital/10000)
    basisCrossed := false
if close < lower
    strategy.close("s")
    strategy.close("추가s")
    entryMade := false
    basisCrossed := false
    upperCrossed := false

```

> Detail

https://www.fmz.com/strategy/445836

> Last Modified

2024-03-22 15:49:28
