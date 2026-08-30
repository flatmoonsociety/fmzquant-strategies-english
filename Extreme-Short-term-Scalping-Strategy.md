
> Name

Extreme-Short-term-Scalping-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12584ecdfa212284b79.png)
 [trans]

## Overview
The short-term extreme short strategy is a high-frequency trading strategy that attempts to establish short positions when the price approaches or breaks through the support line and sets minimal stop loss and take profit levels. This strategy uses short-term price breakthroughs to capture market fluctuations and achieve profits.
## Strategy Principle
The strategy starts by calculating a linear regression line of prices. A long position is established if the actual closing price is lower than the predicted closing price; a short position is established if the actual closing price is higher than the predicted closing price. Stop loss and take profit are set to a very small number of pips. This strategy allows you to choose to trade in only long, only short, or all directions.
Key parameters include:
- Source price: closing price
- Linear regression line length: 14
- Offset: 1
- Trading direction: All/Buy only/Sell only
- Stop loss and take profit points: extremely small fixed points or points for the minimum trading unit
The main idea of ​​this strategy is to capture short-term price breakthroughs against the moving average. When the price approaches or breaks through the support or resistance line, establish a position in time; set a very small stop loss and take profit, close the position immediately after realizing a profit, and repeat the process.
## Advantage Analysis
This strategy has the following advantages:
1. High transaction frequency, suitable for high-frequency trading, and can capture more short-term price fluctuation opportunities
2. The stop loss and take profit settings are extremely small, which is helpful for controlling single losses.
3. Can flexibly choose trading directions and adapt to different market environments
4. Simple calculation and implementation, easy to operate
## Risk Analysis
There are also some risks with this strategy:
1. Night trading and short gaps may lead to expanded losses
2. Higher transaction costs
3. The signal may be wrong and requires timely attention and optimization.
4. The market needs to be continuously monitored and you cannot leave the market.
Corresponding risk response measures include:
1. Night trading is prohibited
2. Optimize stop loss and take profit levels to reduce the impact of transaction costs
3. Test and optimize parameters to reduce error signals
4. Pay close attention to the market and do not trade away from the market
## Optimization direction
Directions where this strategy can be further optimized include:
1. Combine with other indicators to filter signals and reduce erroneous transactions
2. Dynamically adjust stop loss and take profit levels
3. Optimize parameters to reduce the risk of overfitting
4. Consider the impact of transaction costs and set reasonable stop loss and take profit
5. Test the stability of parameters of different varieties and time periods
## Summarize
The short-term extreme short strategy is a typical high-frequency trading strategy. It captures short-term price fluctuations by promptly opening positions near key price points and setting minimal stop-loss and take-profit. Although you can get higher returns, you also face certain risks. Through continuous testing and optimization, the strategy can further enhance stability and profitability.
||

## Overview

The extreme short-term scalping strategy attempts to establish short positions when prices approach or break support lines and sets very small stop loss and take profit levels for high frequency trading. The strategy exploits short-term price breakthroughs to capture market fluctuations for profits.

## Strategy Logic

The strategy first calculates the linear regression line of prices. If the actual closing price is lower than the forecast closing price, long positions are established. If the actual closing price is higher than the forecast closing price, short positions are established. Stop loss and take profit are set to very small number of pips. The strategy allows choosing only long, only short or all direction trading.  

Key parameters include:

- Source price: closing price 
- Length of linear regression line: 14
- Offset: 1
- Trading direction: all/only buy/only sell
- Stop loss and take profit in pips: very small fixed pips or minimum tick pips

The main idea of the strategy is to capture short-term price breakthroughs of moving averages. When prices approach or break through support or resistance lines, timely establish positions. And set very small stop loss and take profit to realise profit then close positions immediately, repeating the process.

## Advantage Analysis 

The strategy has the following advantages:

1. High trading frequency, suitable for high frequency trading, can capture more short-term price fluctuations
2. Very small stop loss and take profit helps control single loss  
3. Can flexibly choose trading direction to adapt to different market environments
4. Easy to implement with simple logic

## Risk Analysis

There are also some risks:

1. Price gaps may lead to expanded losses
2. High transaction costs
3. Signal errors may happen and need timely attention and optimisation  
4. Requires continuous market monitoring 

Corresponding risk management measures include:

1. Disable overnight trading
2. Optimise stop loss and take profit to reduce transaction cost impacts
3. Test and optimise parameters to reduce wrong signals
4. Pay close attention to the market

## Optimisation Directions

Further optimisation directions include:

1. Add other indicators to filter signals and reduce wrong trades
2. Dynamically adjust stop loss and take profit  
3. Optimise parameters to reduce overfitting
4. Consider transaction cost impacts for reasonable stop loss and take profit configuration   
5. Test stability across products and timeframes

## Summary  

The extreme short-term scalping strategy is a typical high frequency trading strategy. By establishing positions around key price levels and setting very small stop loss and take profit, it captures short-term price fluctuations. Although it can achieve high returns, there are also certain risks. With continuous testing and optimisation, the strategy can be further enhanced for stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|14|Length|
|v_input_3|true|offset|
|v_input_4|100|gap_tick|
|v_input_5|300|fixedTP|
|v_input_6|100|fixedSL|
|v_input_7|true|useFixedSLTP|
|v_input_8|0|Direction of order: ALL|BUY ONLY|SELL ONLY|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-09 00:00:00
end: 2024-01-16 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Extreme Scalping", overlay=true )
src = input(close,title="Source")
len = input(defval=14, minval=1, title="Length")
offset = input(1)
out = linreg(src, len, offset)
plot(out)

gap_tick=input(100)
fixedTP=input(300)
fixedSL=input(100)
useFixedSLTP=input(true)
direction=input(defval="ALL",title="Direction of order",options=["ALL","BUY ONLY","SELL ONLY"])
gap=gap_tick*syminfo.mintick
plot(out+gap,color=color.red)
plot(out-gap,color=color.green)

tp=useFixedSLTP?fixedTP:gap_tick
sl=useFixedSLTP?fixedSL:gap_tick

longCondition = close<(out-gap) and (direction=="ALL" or direction=="BUY ONLY")
shortCondition = close>(out+gap) and (direction=="ALL" or direction=="SELL ONLY")

if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit("exit long","Long",profit = tp,loss = sl)
    

if (shortCondition)
    strategy.entry("Short", strategy.short)
    strategy.exit("exit short","Short",profit =tp,loss=sl)
    
// === Backtesting Dates === thanks to Trost

// testPeriodSwitch = input(true, "Custom Backtesting Dates")
// testStartYear = input(2019, "Backtest Start Year")
// testStartMonth = input(10, "Backtest Start Month")
// testStartDay = input(3, "Backtest Start Day")
// testStartHour = input(0, "Backtest Start Hour")
// testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,testStartHour,0)
// testStopYear = input(2019, "Backtest Stop Year")
// testStopMonth = input(12, "Backtest Stop Month")
// testStopDay = input(31, "Backtest Stop Day")
// testStopHour = input(23, "Backtest Stop Hour")
// testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,testStopHour,0)
// testPeriod() =>
//     time >= testPeriodStart and time <= testPeriodStop ? true : false
// isPeriod = testPeriodSwitch == true ? testPeriod() : true
// // === /END

// if not isPeriod
//     strategy.cancel_all()
//     strategy.close_all()
        
```

> Detail

https://www.fmz.com/strategy/439053

> Last Modified

2024-01-17 12:06:39
