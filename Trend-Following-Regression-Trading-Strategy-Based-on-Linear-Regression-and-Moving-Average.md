
> Name

Trend-Following-Regression-Trading-Strategy-Based-on-Linear-Regression-and-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/5bf2eccd8d49da0c76461b774adcead03871ac60a7308fe4a14c559aa1cf902c.png)
[trans]

## Overview
This strategy designs a simple trend following trading system based on linear regression lines and moving averages. Go long when the linear regression line crosses the moving average, and go short when the linear regression line crosses below the moving average. At the same time, the slope of the linear regression line is combined to filter some trading signals, and only enter the market when the trend direction is consistent.
## Strategy name
Trend Following Regression Trading Strategy
## Strategy Principle
The strategy contains the following key components:
1. Calculate the N-day simple moving average (SMA)
2. Calculate the linear regression line for the last N days
3. When the closing price crosses the SMA line and is higher than the regression line, go long
4. When the closing price crosses the SMA line and is lower than the regression line, go short
5. Set stop loss price and take profit price
A linear regression line provides a good fit to the direction of the trend over a recent period of time. This can be used to help determine the direction of the overall trend. When the price breaks through the SMA line, we need to further determine whether the direction of the linear regression line is consistent with this breakthrough. Only when the two directions are consistent, a trading signal is generated. This can filter out some false breakthroughs.
In addition, the strategy also sets a stop-loss mechanism. When the price hits the stop loss line, close the position and stop the loss. A take-profit line is also set up to lock in some profits.
## Strategic Advantages
This strategy has the following advantages:
1. Combine trend indicators and breakthrough indicators to avoid false breakthroughs and improve signal quality
2. Use linear regression to determine the trend direction, perform trend filtering, and only go long when the trend is upward and short when the trend is downward.
3. Set up stop-loss and take-profit mechanisms to control risks
4. The rules are clear and easy to understand and implement.
5. Only a few parameters need to be adjusted, no need to be too complicated
## Risk Analysis
There are also some risks with this strategy:
1. More false trading signals will be generated in volatile market conditions
2. The settings of moving averages and regression periods require repeated testing and optimization. Improper settings may affect the performance of the strategy.
3. In extreme market conditions, stop loss may be breached and cause large losses.
4. Based only on technical indicators without combining fundamental factors
In response to these risks, we can optimize from the following aspects:
1. In volatile markets, consider pausing the strategy or using other indicator filters.
2. Repeated backtesting of parameters to find optimal parameters
3. Optimize and dynamically adjust stop loss positions
4. Combined with economic data and other fundamental factors
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Add other auxiliary indicators to judge market conditions and avoid trading in volatile market conditions
2. Optimize moving average types, such as double moving average, three moving average and other combinations
3. Conduct further analysis on the slope of the regression line and add slope judgment rules
4. Combined with volatility indicators, set dynamic stop-loss and take-profit positions
5. Use machine learning methods to automatically optimize various parameters
## Summarize
This strategy integrates the trend tracking function of moving averages and the trend judgment function of linear regression to form a relatively simple and easy trend tracking trading system. In markets with obvious trends, this strategy can achieve better results. We also need to conduct a lot of backtesting and optimization of parameters and rules, and do a good job in risk control, then this strategy should be able to obtain a stable return on investment.
|| 


## Overview

This strategy designs a simple trend following trading system based on linear regression line and moving average line. It goes long when the linear regression line crosses above the moving average and goes short when the linear regression line crosses below. Meanwhile, it uses the slope of the regression line to filter some trading signals and only enters when the trend direction matches.  

## Strategy Name  

Trend Following Regression Trading Strategy

## Strategy Principle  

The key components of this strategy include:

1. Calculate N-day simple moving average (SMA)  
2. Calculate linear regression line of recent N days
3. Go long when close price crosses above SMA and is higher than regression line
4. Go short when close price crosses below SMA and is lower than regression line
5. Set stop loss price and take profit price

The linear regression line can fit the trend direction well in recent periods. It can help judge the overall trend direction. When price breaks through the SMA line, we need to further determine whether the direction of the linear regression line is consistent with this breakout. Only when the two directions are consistent, a trading signal is generated. This can filter out some false breakouts.

In addition, the strategy also sets a stop loss mechanism. When the price hits the stop loss line, close positions to stop loss. It also sets a take profit line to lock in some profits.

## Advantages of the Strategy  

The strategy has the following advantages:

1. Combine trend indicator and breakout indicator to avoid false breakout and improve signal quality
2. Use linear regression to determine trend direction for trend filtering, only go long in uptrend and go short in downtrend
3. Set stop loss and take profit to control risk
4. Clear and easy to understand rules  
5. Only few parameters to tune without too much complexity

## Risk Analysis   

The strategy also has some risks:

1. More wrong trading signals may be generated in range-bound market
2. The settings of moving average and regression periods need extensive testing and optimization, improper settings may affect strategy performance  
3. Stop loss may be broken in extreme market conditions resulting in large losses
4. Based solely on technical indicators without combining fundamental factors

Regarding these risks, we can optimize from the following aspects:

1. Consider suspending the strategy or using other indicators for filtering in range-bound market
2. Backtest extensively to find the optimal parameters
3. Optimize and dynamically adjust stop loss position  
4. Combine economic data and other fundamental factors

## Optimization Directions  

The main aspects to optimize the strategy further include:

1. Add other auxiliary indicators to judge market conditions and avoid trading in range-bound periods
2. Optimize moving average type, such as dual moving average, triple moving averages etc. 
3. Further analyze the slope of the regression line and add slope judgment rules
4. Incorporate volatility indicators to set dynamic stop loss and take profit levels
5. Utilize machine learning methods to automatically optimize parameters

## Conclusion  

This strategy integrates the trend following function of moving averages and the trend judging capability of linear regression, forming a relatively simple trend following trading system. It can achieve good results in strong trending markets. We still need extensive backtesting and optimization on the parameters and rules, and proper risk control. Then this strategy should be able to obtain steady investment returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|SMA Period|
|v_input_2|2|Stop Loss Percentage|
|v_input_3|2|Take Profit Percentage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-17 00:00:00
end: 2023-12-05 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Regression Trading Strategy", shorttitle="RTS", overlay=true)

// Input parameters
n = input(14, title="SMA Period")
stop_loss_percentage = input(2, title="Stop Loss Percentage")
take_profit_percentage = input(2, title="Take Profit Percentage")

// Calculate the SMA
sma = sma(close, n)

// Linear regression function
linear_regression(src, length) =>
    sumX = 0.0
    sumY = 0.0
    sumXY = 0.0
    sumX2 = 0.0
    for i = 0 to length - 1
        sumX := sumX + i
        sumY := sumY + src[i]
        sumXY := sumXY + i * src[i]
        sumX2 := sumX2 + i * i
    slope = (length * sumXY - sumX * sumY) / (length * sumX2 - sumX * sumX)
    intercept = (sumY - slope * sumX) / length
    line = slope * length + intercept
    line

// Calculate the linear regression
regression_line = linear_regression(close, n)

// Plot the SMA and regression line
plot(sma, title="SMA", color=color.blue)
plot(regression_line, title="Regression Line", color=color.red)

// Trading strategy conditions
long_condition = crossover(close, sma) and close > regression_line
short_condition = crossunder(close, sma) and close < regression_line

// Exit conditions
stop_loss_price = close * (1 - stop_loss_percentage / 100)
take_profit_price = close * (1 + take_profit_percentage / 100)

// Plot entry and exit points on the chart
plotshape(series=long_condition, title="Long Entry", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=short_condition, title="Short Entry", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)
plotshape(series=crossunder(close, stop_loss_price), title="Stop Loss", location=location.abovebar, color=color.red, style=shape.labeldown, text="SL")
plotshape(series=crossover(close, take_profit_price), title="Take Profit", location=location.belowbar, color=color.green, style=shape.labelup, text="TP")

// Strategy orders
strategy.entry("Long", strategy.long, when = long_condition)
strategy.entry("Short", strategy.short, when = short_condition)
strategy.exit("Exit", from_entry = "Long", when = crossover(close, stop_loss_price) or crossover(close, take_profit_price))
strategy.exit("Exit", from_entry = "Short", when = crossunder(close, stop_loss_price) or crossunder(close, take_profit_price))


```

> Detail

https://www.fmz.com/strategy/435771

> Last Modified

2023-12-18 17:34:29
