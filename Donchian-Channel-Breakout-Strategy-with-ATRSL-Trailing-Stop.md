
> Name

Donchian-Channel-Breakout-Strategy-with-ATRSL-Trailing-Stop
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/35ee2cee7a71b8a8f2a94fa80809b89a4d38a1d119c130ff5e0d319166bd123f.png)
[trans]

## Strategy Overview
The Donchian Channel Breakout Strategy is a trend-following quantitative trading strategy. This strategy utilizes Donchian Channels to capture market trends while using ATRSL Trailing Stops to control risk. When the price breaks through the upper track of the Donchian Channel, the strategy opens a long position; when the price falls below the ATRSL moving stop loss line, the strategy closes the position.
## Strategy Principle
1. Calculate the Tang Qian Channel: Calculate the highest price and lowest price in the past `donLength` periods based on the `donLength` parameters input by the user, and use them as the upper rail `donUpper` and lower rail `donLower` of the Tang Qian Channel respectively. The channel midline `donBasis` is the average of the upper and lower rails.
2. Calculate ATRSL trailing stop loss: Calculate the ATR value `SL2` based on the `AP2` and `AF2` parameters entered by the user, and then dynamically adjust the trailing stop price `Trail2` based on the relationship between the current closing price `SC` and the previous trailing stop price `Trail2[1]`.
3. Conditions for opening a position: When the current closing price crosses the upper track of the Tang Qian Channel, open a long position.
4. Position closing conditions: When the current closing price falls below the ATRSL moving stop loss line, the position will be closed.
## Strategic Advantages
1. Trend following: Judging the trend direction through the Tang Qian channel can effectively capture the market trend.
2. Dynamic stop loss: Using ATRSL moving stop loss, you can dynamically adjust the stop loss position according to market fluctuations and control risks.
3. Flexible parameters: Users can adjust parameters such as `donLength`, `AP2` and `AF2` ​​according to their own needs to optimize strategy performance.
## Strategy Risk
1. Parameter risk: Different parameter settings will lead to large differences in strategy performance, and sufficient backtesting and parameter optimization are required.
2. Market risk: In a volatile market or when the trend reverses, this strategy may experience a large retracement.
3. Slippage and transaction costs: Frequent transactions may lead to higher slippage and transaction costs, affecting strategy returns.
## Optimization direction
1. Add trend filtering: In the opening conditions, you can add indicators such as ADX to judge the strength of the trend, and only open positions when the trend is obvious to improve the quality of opening positions.
2. Optimize stop loss: You can try to use other stop loss methods, such as percentage stop loss, ATR stop loss, etc., or combine multiple stop loss methods to improve stop loss flexibility.
3. Add position management: dynamically adjust position size and control risk exposure according to market fluctuations and account risks.
## Summary
The Donchian Channel Breakout Strategy is a classic trend following strategy that captures trends through the Donchian Channel and uses ATRSL trailing stops to control risk. The advantage of this strategy is that the logic is simple and clear, easy to implement and optimize; the disadvantage is that it performs poorly during market shocks and trend reversals, and the parameter settings have a greater impact on the performance of the strategy. In practical applications, modules such as trend filtering, optimized stop loss and position management can be added to the original strategy to improve the stability and profitability of the strategy. At the same time, you need to pay attention to controlling transaction frequency and costs, and flexibly adjust strategy parameters according to market characteristics and your own risk preferences.
|| 

## Strategy Overview
The Donchian Channel Breakout Strategy is a trend-following quantitative trading strategy. It utilizes Donchian Channels to capture market trends while using an ATRSL trailing stop to manage risk. When the price breaks above the upper band of the Donchian Channel, the strategy enters a long position; when the price falls below the ATRSL trailing stop line, the strategy closes the position.

## Strategy Principle
1. Calculate Donchian Channel: Based on the user-defined `donLength` parameter, calculate the highest high and lowest low of the past `donLength` periods as the upper band `donUpper` and lower band `donLower` of the Donchian Channel, respectively. The midline `donBasis` is the average of the upper and lower bands.
2. Calculate ATRSL Trailing Stop: Based on the user-defined `AP2` and `AF2` parameters, calculate the ATR value `SL2`. Then, dynamically adjust the trailing stop price `Trail2` according to the relationship between the current close price `SC` and the previous trailing stop price `Trail2[1]`.
3. Entry Condition: When the current close price crosses above the upper band of the Donchian Channel, enter a long position.
4. Exit Condition: When the current close price crosses below the ATRSL trailing stop line, close the position.

## Strategy Advantages
1. Trend Following: By using Donchian Channels to determine trend direction, the strategy can effectively capture market trends.
2. Dynamic Stop Loss: The ATRSL trailing stop allows for dynamic adjustment of the stop loss level based on market volatility, helping to manage risk.
3. Parameter Flexibility: Users can adjust parameters such as `donLength`, `AP2`, and `AF2` according to their needs to optimize strategy performance.

## Strategy Risks
1. Parameter Risk: Different parameter settings can lead to significant differences in strategy performance, requiring thorough backtesting and parameter optimization.
2. Market Risk: During choppy markets or trend reversals, the strategy may experience significant drawdowns.
3. Slippage and Trading Costs: Frequent trading may result in high slippage and trading costs, impacting strategy profitability.

## Optimization Directions
1. Add Trend Filters: In the entry condition, indicators such as ADX can be added to assess trend strength and only enter positions when the trend is strong, improving entry quality.
2. Optimize Stop Loss: Experiment with other stop loss methods, such as percentage-based stop loss or ATR stop loss, or combine multiple stop loss approaches to increase stop loss flexibility.
3. Incorporate Position Sizing: Dynamically adjust position size based on market volatility and account risk to manage risk exposure.

## Summary
The Donchian Channel Breakout Strategy is a classic trend-following strategy that captures trends using Donchian Channels and manages risk with an ATRSL trailing stop. The strategy's advantages include its simple and clear logic, ease of implementation, and potential for optimization. However, its drawbacks include poor performance during choppy markets and trend reversals, and significant impact of parameter settings on strategy performance. In practical application, the strategy can be enhanced by adding trend filters, optimizing stop loss, and incorporating position sizing modules to improve stability and profitability. At the same time, it is important to control trading frequency and costs, and flexibly adjust strategy parameters based on market characteristics and personal risk preferences.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|100|donLength|
|v_input_2|10|Slow ATR period|
|v_input_3|3|Slow ATR multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-16 00:00:00
end: 2024-03-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Stock Trend USE THIS", overlay = true)
donLength = input(100, minval=1)

//Donchian Long
donLower = lowest(donLength)
donUpper = highest(donLength)
donBasis = avg(donUpper,donLower)

// ATRSL
SC = close

// Slow Trail //
AP2 = input(10, title="Slow ATR period")  // ATR Period
AF2 = input(3, title="Slow ATR multiplier")  // ATR Factor
SL2 = AF2 * atr(AP2)  // Stop Loss
Trail2 = 0.0
iff_3 = SC > nz(Trail2[1], 0) ? SC - SL2 : SC + SL2
iff_4 = SC < nz(Trail2[1], 0) and SC[1] < nz(Trail2[1], 0) ? min(nz(Trail2[1], 0), SC + SL2) : iff_3
Trail2 := SC > nz(Trail2[1], 0) and SC[1] > nz(Trail2[1], 0) ? max(nz(Trail2[1], 0), SC - SL2) : iff_4



// Long and Short Conditions
longCondition = (crossover(close,donUpper[1])) 

// Close Conditions
closeLongCondition = crossunder(close,Trail2)

// Strategy logic
if (longCondition) 
    strategy.entry("Long", strategy.long)
    alert("Open Long position")

if (closeLongCondition)
    strategy.close("Long")
    alert("Close Long position")

// Plot Donchian
l = plot(donLower, color=color.blue)
u = plot(donUpper, color=color.blue)
plot(donBasis, color=color.orange)
fill(u, l, color=color.blue)
plot(Trail2, color=color.blue, title="ATRSL Trail")
```

> Detail

https://www.fmz.com/strategy/445840

> Last Modified

2024-03-22 16:13:58
