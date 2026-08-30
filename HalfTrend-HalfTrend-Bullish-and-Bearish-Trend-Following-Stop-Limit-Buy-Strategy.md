
> Name

HalfTrend Long and Short Trend Tracking Stop-Limit Buy Strategy-HalfTrend-Bullish-and-Bearish-Trend-Following-Stop-Limit-Buy-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/af540cf5634aa10733.png)

[trans]
####Overview
This strategy is based on the HalfTrend indicator and identifies buy signals by judging the long and short trends. When the HalfTrend indicator changes from idle to long, place a stop-loss limit buy order at the HalfTrend value of the previous short trend. This strategy uses the AmplitudeTrend indicator (ATR) to dynamically adjust the amplitude parameters of trend judgment.
####Strategy Principle
1. To calculate the HalfTrend indicator value, you need to set the lookback period length and amplitude parameter amplitude.
2. Compare the current closing price with the HalfTrend indicator value of the previous period to determine the long and short trend.
   - When the closing price crosses the HalfTrend indicator value amplitude point, the trend turns bullish.
   - When the closing price falls below the HalfTrend indicator value amplitude point, the trend turns bearish.
3. Record the HalfTrend indicator value when the trend turns bearish, as a potential buying position in the future.
4. When the HalfTrend indicator changes from idle to long again, place a stop-limit buy order at the position recorded in step 3.
####Strategic Advantages
1. Determine the investment direction based on the complete long-short trend and adapt to the current market situation to the greatest extent.
2. Use limit order to place an order, and you can buy at a preset position to obtain a better transaction price.
3. The buying position is determined based on the previous short HalfTrend trend, ensuring the low safety of the buying point.
4. Use the amplitude parameter to control the minimum amplitude required to distinguish between long and short trends, which can effectively filter noise signals.
####Strategic Risk
1. Trend reversal judgment relies on the amplitude parameter. Improper parameter values may lead to placing orders too early or too late.
2. Limit orders may not be able to be filled due to price fluctuations, and may miss out on the rising market.
3. If the stop loss setting position is too close to the buying position, you may suffer a large loss.
####Strategy optimization direction
1. Optimize the amplitude parameter and find the best trend judgment amplitude. Amplitude can be dynamically adjusted using the AmplitudeTrend indicator (ATR).
2. Set take profit to sell at the same time as stop loss buying to lock in profits in time.
3. The stop loss position can be set lower, giving greater room for losses and also increasing room for profit.
4. You can add trailing stop loss logic to increase the stop loss level when the price moves in a favorable direction to reduce risks.
####Summary
The HalfTrend long-short trend tracking stop-loss limit buying strategy determines the buying time by judging the changes in the long-short trend of the HalfTrend indicator, and uses the low point of the previous short trend as the buying position in order to enter the market at a relatively safe low level. This strategy includes common strategy elements such as trend judgment, limit orders, stop loss orders, etc., and can be further optimized to improve the risk-return ratio.
|| 

####Overview
This strategy is based on the HalfTrend indicator and identifies buy signals by determining bullish and bearish trends. When the HalfTrend indicator switches from bearish to bullish, a stop-limit buy order is placed at the HalfTrend value of the previous bearish trend. The strategy uses the AmplitudeTrend (ATR) indicator to dynamically adjust the amplitude parameter for trend determination.

####Strategy Principle
1. Calculate the HalfTrend indicator value, which requires setting the lookback period length and amplitude parameter.
2. Compare the current closing price with the previous period's HalfTrend indicator value to determine the bullish or bearish trend.
   - When the closing price crosses above the HalfTrend indicator value by amplitude points, the trend turns bullish.
   - When the closing price crosses below the HalfTrend indicator value by amplitude points, the trend turns bearish.
3. Record the HalfTrend indicator value when the trend turns bearish, which serves as a potential future buy position.
4. When the HalfTrend indicator switches from bearish to bullish again, place a stop-limit buy order at the position recorded in step 3.

####Strategy Advantages
1. Based on complete bullish and bearish trends to determine the investment direction, maximally adapting to the current market condition.
2. Using limit orders for buying, which can achieve better execution prices at predetermined positions.
3. The buy position is determined based on the previous bearish HalfTrend trend, ensuring the safety of buying at a low level.
4. The amplitude parameter is used to control the minimum amplitude required to distinguish between bullish and bearish trends, effectively filtering out noise signals.

####Strategy Risks
1. The trend reversal determination relies on the amplitude parameter, and inappropriate parameter values may lead to premature or delayed order placement.
2. Limit orders may fail to execute due to price fluctuations, missing out on upward movements.
3. The stop-loss setting position may be too close to the buy position, potentially incurring significant losses.

####Strategy Optimization Directions
1. Optimize the amplitude parameter to find the best amplitude for trend determination. The AmplitudeTrend (ATR) indicator can be used to dynamically adjust the amplitude.
2. Set a take profit sell order along with the stop-loss buy order to lock in profits in a timely manner.
3. The stop-loss position can be set lower to allow for a larger loss margin while also increasing the profit potential.
4. Incorporate a trailing stop-loss logic to raise the stop-loss position when the price moves in a favorable direction, reducing risk.

####Summary
The HalfTrend Bullish and Bearish Trend Following Stop-Limit Buy Strategy determines the timing of buying based on changes in the bullish and bearish trends of the HalfTrend indicator. It uses the low point of the previous bearish trend as the buy position, aiming to enter long positions at relatively safe low levels. This strategy incorporates common strategy elements such as trend determination, limit orders, and stop-loss orders, and it can be further optimized to improve the risk-reward ratio.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-11 00:00:00
end: 2024-05-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("HalfTrend Stop-Limit Buy", overlay=true)

// HalfTrend indicator parameters
length = 1
amplitude = 2.0

// HalfTrend calculation
float ph = na
float pl = na
var float dir = na
var float trend = na

if na(trend)
    trend := close
    ph := high
    pl := low
    dir := na
else
    if high > ph
        ph := high
    if low < pl
        pl := low
    if close > trend and na(dir)
        dir := 1
        trend := close
        ph := high
        pl := low
    if close < trend and na(dir)
        dir := -1
        trend := close
        ph := high
        pl := low
    if dir == 1 and close < trend - amplitude
        dir := -1
        trend := close
        ph := high
        pl := low
    if dir == -1 and close > trend + amplitude
        dir := 1
        trend := close
        ph := high
        pl := low

// Buy signal based on HalfTrend
buySignal = dir == 1 and ta.valuewhen(dir == -1, trend, 0)

// Plot HalfTrend
plot(dir == 1 ? trend : na, color=color.blue, linewidth=2, title="HalfTrend Bullish")
plot(dir == -1 ? trend : na, color=color.red, linewidth=2, title="HalfTrend Bearish")

// Place a stop-limit buy order
if (buySignal)
    stopPrice = ta.valuewhen(dir == -1, trend, 0)
    strategy.entry("HalfTrend Buy", strategy.long, stop=stopPrice, comment="HalfTrend Buy")


```

> Detail

https://www.fmz.com/strategy/451732

> Last Modified

2024-05-17 15:45:13
