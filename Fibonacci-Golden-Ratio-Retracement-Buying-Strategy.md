
> Name

Fibonacci Golden Ratio Retracement Buying Strategy-Fibonacci-Golden-Ratio-Retracement-Buying-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ff579074dc08cffa80.png)

[trans]
#### Overview
The Fibonacci Golden Retracement Buy Strategy is a trading strategy based on Fibonacci retracement levels and trend following stops. This strategy utilizes Fibonacci retracement levels as potential support and resistance levels, combined with trend-following stops to determine buy and sell timing. The strategy will issue a buy signal when the price retraces to a certain Fibonacci level in an uptrend and is above the trend following stop; it will issue a sell signal when the price falls below the trend following stop or a certain Fibonacci level.
#### Strategy Principle
1. Calculate Fibonacci retracement levels: Calculate Fibonacci retracement levels of 0%, 23.6%, 38.2%, 50%, 61.8% and 78.6% based on the highest price and lowest price within the specified price range.
2. Identify swing highs and lows: Identify swing highs and lows in price over a specified number of trading periods.
3. Calculate the trend following stop loss: Calculate the trend following stop loss price based on whether the current closing price is higher than the previous swing high or lower than the previous swing low.
4. Define buy and sell conditions: when the closing price is higher than the trend following stop loss and higher than a certain Fibonacci retracement level, a buy signal is generated; when the closing price is lower than the trend following stop loss and lower than a certain Fibonacci retracement level, a sell signal is generated.
5. Execute the transaction: When the buying conditions are met, the strategy enters a long position; when the selling conditions are met, the strategy closes the position.
#### Strategic Advantages
1. Combining technical analysis and trend following: This strategy uses Fibonacci retracement levels as potential support and resistance levels, and combined with trend following stop loss, can effectively capture trend opportunities and control risks.
2. Adapt to different market conditions: Fibonacci retracement levels have certain applicability under different market conditions and can provide a reference for trading in uptrends and downtrends.
3. Clear entry and exit conditions: The strategy is based on clear buying and selling conditions, which helps traders make objective decisions and avoid the influence of subjective emotions.
#### Strategy Risk
1. Market fluctuation risk: In the case of severe market fluctuations, the price may quickly break through the Fibonacci retracement level and trend following stop loss, resulting in strategy errors or excessive stop loss.
2. Parameter setting risk: The performance of the strategy depends on the parameter settings of Fibonacci retracement levels and trend tracking stop loss. Inappropriate parameters may lead to poor performance of the strategy.
3. Trend identification risk: The strategy assumes that price movement follows the trend, but in the actual market, prices may fluctuate or reverse, leading to misjudgments in trend identification.
#### Strategy optimization direction
1. Combined with other technical indicators: You can consider using Fibonacci retracement levels in conjunction with other technical indicators (such as moving averages, relative strength index, etc.) to improve the reliability of the strategy.
2. Dynamically adjust parameters: According to changes in market conditions, dynamically adjust the parameters of Fibonacci retracement levels and trend tracking stop loss to adapt to different market environments.
3. Introduce risk management measures: Introduce risk management measures into the strategy, such as position management, stop loss management, etc., to control potential risk exposures.
#### Summary
The Fibonacci Golden Retracement Buy Strategy is a trading strategy that combines Fibonacci retracement levels with trend following stops. This strategy utilizes Fibonacci retracement levels as potential support and resistance levels, combined with trend-following stops to determine buy and sell timing. The advantage of the strategy is that it combines technical analysis and trend tracking, adapts to different market conditions, and provides clear entry and exit conditions. However, strategies also face market fluctuation risks, parameter setting risks and trend identification risks. In order to optimize strategy performance, you can consider combining other technical indicators, dynamically adjusting parameters, and introducing risk management measures.
|| 

#### Overview
The Fibonacci Golden Ratio Retracement Buying Strategy is a trading strategy based on Fibonacci retracement levels and trend-following stop-loss. The strategy utilizes Fibonacci retracement levels as potential support and resistance levels and combines them with a trailing stop loss to determine buying and selling opportunities. When the price retraces to a certain Fibonacci level during an uptrend and is above the trailing stop loss, the strategy generates a buy signal. When the price falls below the trailing stop loss or a certain Fibonacci level, the strategy generates a sell signal.

#### Strategy Principle
1. Calculation of Fibonacci Retracement Levels: Based on the highest high and lowest low within a specified price range, the strategy calculates Fibonacci retracement levels at 0%, 23.6%, 38.2%, 50%, 61.8%, and 78.6%.
2. Identification of Swing Highs and Lows: The strategy identifies swing highs and lows within a specified number of trading periods.
3. Calculation of Trailing Stop Loss: Based on whether the current close price is above the previous swing high or below the previous swing low, the strategy calculates the trailing stop loss price.
4. Definition of Buy and Sell Conditions: When the close price is above the trailing stop loss and above a certain Fibonacci retracement level, a buy signal is generated. When the close price is below the trailing stop loss and below a certain Fibonacci retracement level, a sell signal is generated.
5. Trade Execution: When the buy condition is met, the strategy enters a long position. When the sell condition is met, the strategy closes the position.

#### Strategy Advantages
1. Combination of Technical Analysis and Trend Following: The strategy utilizes Fibonacci retracement levels as potential support and resistance levels while incorporating a trailing stop loss, effectively capturing trending opportunities and managing risk.
2. Adaptability to Different Market Conditions: Fibonacci retracement levels have applicability in various market conditions and can provide reference for trading in both uptrends and downtrends.
3. Clear Entry and Exit Rules: The strategy is based on well-defined buy and sell conditions, helping traders make objective decisions and avoid subjective emotional influences.

#### Strategy Risks
1. Market Volatility Risk: In highly volatile market conditions, prices may quickly break through Fibonacci retracement levels and the trailing stop loss, leading to strategy errors or excessive stop-outs.
2. Parameter Setting Risk: The performance of the strategy depends on the parameter settings for Fibonacci retracement levels and the trailing stop loss. Inappropriate parameters may result in suboptimal strategy performance.
3. Trend Identification Risk: The strategy assumes that price movements follow trends, but in real markets, prices may exhibit fluctuations or reversals, leading to misjudgments in trend identification.

#### Strategy Optimization Directions
1. Integration with Other Technical Indicators: Consider combining Fibonacci retracement levels with other technical indicators (such as moving averages, relative strength index, etc.) to enhance the reliability of the strategy.
2. Dynamic Parameter Adjustment: Dynamically adjust the parameters for Fibonacci retracement levels and the trailing stop loss based on changing market conditions to adapt to different market environments.
3. Introduction of Risk Management Measures: Incorporate risk management measures into the strategy, such as position sizing and stop-loss management, to control potential risk exposure.

#### Summary
The Fibonacci Golden Ratio Retracement Buying Strategy is a trading strategy that combines Fibonacci retracement levels with a trailing stop loss. The strategy utilizes Fibonacci retracement levels as potential support and resistance levels and incorporates a trailing stop loss to determine buying and selling opportunities. The advantages of the strategy lie in its combination of technical analysis and trend following, adaptability to different market conditions, and clear entry and exit rules. However, the strategy also faces risks such as market volatility risk, parameter setting risk, and trend identification risk. To optimize strategy performance, considerations include integrating other technical indicators, dynamically adjusting parameters, and introducing risk management measures.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Fibonacci 0% Level|
|v_input_2|true|Fibonacci 1% Level|
|v_input_3|0.236|Fibonacci 23.6% Level|
|v_input_4|0.382|Fibonacci 38.2% Level|
|v_input_5|0.5|Fibonacci 50% Level|
|v_input_6|0.618|Fibonacci 61.8% Level|
|v_input_7|0.786|Fibonacci 78.6% Level|
|v_input_8|50|Price|
|v_input_9|true|Swing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-04-23 00:00:00
end: 2024-04-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(title='Fibonacci BFSP', overlay=true)

// Define Fibonacci retracement levels
fib0 = input(0, title="Fibonacci 0% Level")
fib1 = input(1, title="Fibonacci 1% Level")
fib23 = input(0.236, title="Fibonacci 23.6% Level")
fib38 = input(0.382, title="Fibonacci 38.2% Level")
fib50 = input(0.5, title="Fibonacci 50% Level")
fib61 = input(0.618, title="Fibonacci 61.8% Level")
fib78 = input(0.786, title="Fibonacci 78.6% Level")
Price = input(50, title="Price")

// Calculate Fibonacci levels
priceHigh = ta.highest(high, Price)
priceLow = ta.lowest(low, Price)
priceRange = priceHigh - priceLow
fibRetracement0 = priceHigh - fib0 * priceRange
fibRetracement1 = priceHigh - fib1 * priceRange
fibRetracement23 = priceHigh - fib23 * priceRange
fibRetracement38 = priceHigh - fib38 * priceRange
fibRetracement50 = priceHigh - fib50 * priceRange
fibRetracement61 = priceHigh - fib61 * priceRange
fibRetracement78 = priceHigh - fib78 * priceRange

// Plot Fibonacci retracement levels
plot(fibRetracement0, color=color.gray, linewidth=2)
plot(fibRetracement1, color=color.gray, linewidth=2)
plot(fibRetracement23, color=color.green, linewidth=2)
plot(fibRetracement38, color=color.olive, linewidth=2)
plot(fibRetracement50, color=color.white, linewidth=2)
plot(fibRetracement61, color=color.orange, linewidth=2)
plot(fibRetracement78, color=color.red, linewidth=2)

// Inputs
no = input(1, title="Swing")

// Calculate swing highs and lows
res = ta.highest(high, no)
sup = ta.lowest(low, no)

// Calculate trailing stop loss
avd = close > res[1] ? 1 : close < sup[1] ? -1 : 0
avn = ta.valuewhen(avd != 0, avd, 0)
tsl = avn == 1 ? sup : res

// Define buy and sell conditions
buyCondition = (close > tsl) and (close > fibRetracement23 or close > fibRetracement38 or close > fibRetracement50 or close > fibRetracement61 or close > fibRetracement78)
sellCondition = (close < tsl) and (close < fibRetracement23 or close < fibRetracement38 or close < fibRetracement50 or close < fibRetracement61 or close < fibRetracement78)

// Entry strategy
if (buyCondition)
    strategy.entry("Buy", strategy.long)

// Exit strategy
if (sellCondition)
    strategy.close("Buy")

// Color bars based on buy and sell conditions
barColor = buyCondition ? color.green : sellCondition ? color.red : na
barcolor(barColor)

```

> Detail

https://www.fmz.com/strategy/449846

> Last Modified

2024-04-29 17:08:07
