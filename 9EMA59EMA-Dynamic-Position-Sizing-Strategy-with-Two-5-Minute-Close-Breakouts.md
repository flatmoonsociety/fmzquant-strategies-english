
> Name

5-minute double close price strong breakout strategy based on 9EMA dynamic position 9EMA-Dynamic-Position-Sizing-Strategy-with-Two-5-Minute-Close-Breakouts
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/139295c4430e34e3fe8.png)
[trans]

## Strategy Overview
This strategy uses the 9-period exponential moving average (9EMA) as the basis for trend judgment. Within 10 minutes of the opening of the trading day, if the closing prices of two consecutive 5-minute K-lines are very close to the highest price (greater than or equal to 99% of the highest price), and the closing price is above the 9EMA, then it is considered that a strong breakthrough signal has occurred. At this time, the position size is calculated based on the current closing price, and a long position is opened. The position will be closed until the first 5-minute K-line whose closing price falls below the 9EMA appears.
## Strategy Principle
This strategy is based on the following principles:
1. During the opening stage of the trading day, if the market has a strong breakthrough trend, it usually means that the market outlook is expected to continue its strong rise.
2. 9EMA is a relatively sensitive trend judgment indicator. Prices above 9EMA often mean that bulls have the advantage.
3. The closing prices of two consecutive K lines are very close to the highest price, indicating that the bulls are strong and have high buying enthusiasm.
4. After the emergence of a strong trend, using a fixed amount of funds to determine the position size can not only control risks but also make full use of the trend market.
5. When the price falls below the 9EMA, it often means that the trend has turned. At this time, closing the position in time can protect profits to the maximum extent.
This strategy captures the strong breakthrough market at the opening stage of the trading day and participates in the form of dynamic positions, striving to gain greater returns with less risk. At the same time, this strategy also adopts strict stop-loss conditions. Once the trend reverses, it will decisively close the position and control the retracement.
## Strategic Advantages
1. The trading time is concentrated 10 minutes before the opening, so as to grasp the early trading market, the trading frequency is low and the operability is strong.
2. Use two consecutive K-line breakthroughs to confirm the trend, which can effectively filter out false breakthroughs and improve signal reliability.
3. The position size is dynamically adjusted according to the price level of the breakthrough point, which can automatically adapt to the market characteristics of different periods, and the risk is controllable.
4. The stop loss conditions are clear and strictly implemented, which can effectively control the maximum loss of a single transaction.
5. The strategy logic is simple, easy to understand and execute, and is suitable for most traders.
## Strategy Risk
1. Although trend opportunities often appear during the opening stage, large fluctuations and recurrences sometimes occur, and there is a certain risk of false breakthroughs.
2. The strategy opens a position when two consecutive K lines meet the conditions. If the market reverses quickly after opening a position, you may still face a certain loss.
3. Although the position control method of fixed capital amount is simple, when the market fluctuates violently, the rate of return of the strategy may fluctuate greatly.
4. This strategy can only capture unilateral rising markets, and is not applicable to volatile markets and downward trend markets.
In response to the above risks, you can consider optimizing and improving from the following aspects:
1. Add the relationship between the opening price and the closing price of the previous day as a filtering condition to improve the accuracy of trend judgment.
2. Optimize stop loss conditions, such as adding trailing stop loss or conditional stop loss, to further reduce the risk exposure of a single transaction.
3. During the continuation stage of the trend, you can consider using the pyramid method of adding positions to increase the overall rate of return.
4. Try to combine this strategy with other strategies suitable for volatile markets or downward trends to improve the adaptability of the strategy.
## Optimization direction
1. Introduce more effective trend judgment indicators, such as MACD, Bollinger Bands, etc., and integrate multiple indicators to confirm trend signals, improve the reliability of position opening signals, and reduce the risk of false breakthroughs.
2. To optimize the position opening time window, you can consider shortening the 10-minute time window to 5 minutes or extending it to 15 minutes, and find the best position opening time through backtesting and comparison. In this way, the impact of initial fluctuations can be minimized while grasping the trend.
3. In terms of position control, you can consider introducing volatility factors, such as dynamically adjusting the proportion of funds for each opening of a position based on ATR (average true fluctuation range), reducing positions when fluctuations are large, and increasing positions when fluctuations are small, so that the strategy can better adapt to different market rhythms.
4. Optimize the stop loss conditions. On the basis of maintaining the original 9EMA stop loss logic, you can add a trailing stop loss strategy, that is, after the price moves a certain proportion in a favorable direction, the stop loss position will be moved up to the cost price or near the opening price, thereby reducing the retracement and locking in part of the profit.
5. Consider adding some filtering conditions, such as trading volume, volatility, etc., and when a position opening signal appears, determine whether these indicators are improving simultaneously to further confirm the validity of the trend. This can help the strategy avoid some traps and false signals.   
Through the above optimization, this strategy is expected to better control risks while capturing trends, and improve the stability and sustainability of strategy returns. Of course, any optimization needs to be verified through rigorous backtesting to verify its effectiveness and dynamically adjusted according to the actual situation.
## Summarize
This strategy takes 9EMA as the core, and uses the closing price of two consecutive 5-minute K lines to strongly break through 9EMA, capture the strong rising market within 10 minutes of the opening of the trading day, and use a fixed amount of funds to dynamically adjust positions for trading. The logic of this strategy is simple and clear, easy to understand and execute, and is suitable for most traders. At the same time, this strategy also has certain limitations and risks, such as insufficient adaptability to volatile market conditions and downward trend markets, and the risk of rapid reversal after opening a position. In response to these problems, improvements and optimizations can be made in terms of trend judgment, position control, stop loss optimization, filtering conditions, etc., so that the strategy can better grasp market opportunities and control risks. In general, this strategy has clear ideas and strong plasticity, and is worthy of further exploration and practice.
|| 

## Strategy Overview

This strategy uses the 9-period Exponential Moving Average (9EMA) as the basis for trend determination. Within the first 10 minutes of the trading day, if there are two consecutive 5-minute candles with closing prices very close to the high (greater than or equal to 99% of the high) and above the 9EMA, it is considered a strong breakout signal. At this point, the position size is calculated based on the current closing price, and a long position is opened. The position is held until the first 5-minute candle with a close below the 9EMA, at which point the position is closed.

## Strategy Principles

This strategy is based on the following principles:

1. During the opening stage of a trading day, if the market shows a strong breakout trend, it usually indicates that the upward trend is likely to continue.
2. The 9EMA is a relatively sensitive indicator for trend determination, and prices above the 9EMA often indicate bullish dominance.
3. Two consecutive candles with closing prices very close to the high indicate strong bullish momentum and high buying enthusiasm.
4. After a strong trend emerges, using a fixed monetary amount to determine position size can both control risk and fully utilize the trend.
5. When the price falls below the 9EMA, it often indicates a reversal of the trend. Closing the position at this point can protect profits to the greatest extent.

This strategy aims to capture strong breakout moves during the opening period of a trading day and participates with dynamic position sizing, seeking to achieve high returns with low risk. At the same time, the strategy also employs strict stop-loss conditions, promptly closing positions once the trend reverses to control drawdowns.

## Strategy Advantages

1. Trading is concentrated within the first 10 minutes of the opening, capturing early market moves with low trading frequency and strong operability.
2. Using two consecutive candles to confirm the trend can effectively filter out false breakouts and improve signal reliability.
3. Position size is dynamically adjusted based on the price level at the breakout point, automatically adapting to the characteristics of different market periods with controllable risk.
4. Stop-loss conditions are clear and strictly executed, effectively controlling the maximum loss of a single trade.
5. The strategy logic is simple and easy to understand and execute, suitable for most traders to use.

## Strategy Risks

1. Although trending opportunities often emerge during the opening period, there can also be significant fluctuations and reversals at times, facing a certain risk of false breakouts.
2. The strategy enters a position when two consecutive candles meet the conditions. If the market quickly reverses after entry, there is still a possibility of facing certain losses.
3. Although the fixed monetary amount position sizing method is simple, the strategy's return volatility may also be relatively large when the market fluctuates dramatically.
4. This strategy can only capture unilateral upward trends and is not suitable for ranging markets or downward trending markets.

To address the above risks, the following aspects can be considered for optimization and improvement:

1. Incorporate the relationship between the opening price and the previous day's closing price as a filtering condition to improve the accuracy of trend determination.
2. Optimize stop-loss conditions, such as adding trailing stops or conditional stops, to further reduce the risk exposure of a single trade.
3. Consider using a pyramid approach to add positions during the trend continuation phase to increase overall returns.
4. Try combining this strategy with other strategies suitable for ranging or downward trending markets to improve the adaptability of the strategy.

## Optimization Directions

1. Introduce more effective trend determination indicators, such as MACD, Bollinger Bands, etc., to confirm trend signals based on multiple indicators, improving the reliability of entry signals and reducing the risk of false breakouts.
2. Optimize the entry time window. Consider shortening the time window from 10 minutes to 5 minutes or extending it to 15 minutes. Through backtesting comparisons, find the optimal entry time. This can capture trends while minimizing the impact of initial fluctuations.
3. In terms of position sizing, consider introducing a volatility factor. For example, dynamically adjust the percentage of funds for each entry based on the Average True Range (ATR). Decrease position size when volatility is high and increase position size when volatility is low, allowing the strategy to better adapt to different market rhythms.
4. Optimize stop-loss conditions. While maintaining the original 9EMA stop-loss logic, a trailing stop strategy can be added. That is, after the price moves in a favorable direction by a certain percentage, move the stop-loss level to near the cost price or entry price, thereby reducing drawdowns and locking in partial profits.
5. Consider adding some filtering conditions, such as trading volume, volatility, etc. When an entry signal appears, determine whether these indicators are simultaneously favorable to further confirm the validity of the trend. This can help the strategy avoid some traps and false signals.
   
Through the above optimizations, the strategy is expected to better control risks while capturing trends, improving the stability and sustainability of strategy returns. Of course, any optimization needs to be validated through rigorous backtesting and dynamically adjusted based on actual conditions.

## Summary

This strategy uses the 9EMA as the core and captures strong upward trends within the first 10 minutes of a trading day by having two consecutive 5-minute candles with closing prices strongly breaking above the 9EMA. It trades using a fixed monetary amount to dynamically adjust position size. The strategy logic is simple and straightforward, easy to understand and execute, and suitable for most traders to use. At the same time, the strategy also has certain limitations and risks, such as insufficient adaptability to ranging markets and downward trending markets, as well as the risk of rapid reversals after opening positions. To address these issues, improvements and optimizations can be made in terms of trend determination, position sizing, stop-loss optimization, filtering conditions, etc., to enable the strategy to better capture market opportunities and control risks. Overall, this strategy has a clear thought process and strong plasticity, and is worth further exploration and practice.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-13 00:00:00
end: 2024-03-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Two 5min Closes Above 9EMA Strategy with Dynamic Position Size", overlay=true)

// Define the fixed amount for position sizing
fixedAmount = 1000

// Calculate the 9-period EMA
ema9 = ta.ema(close, 9)

// Define time constraints (9:30 AM to 9:40 AM EST, adjust for your timezone)
sessionStart = 0930
sessionEnd = 0940
timeCondition = (hour * 100 + minute) >= sessionStart and (hour * 100 + minute) < sessionEnd

// Detect two consecutive 5-min bars where close is near 0.99 times the high and above 9 EMA
closeNearHighAndAboveEMA = close >= high * 0.99 and close > ema9
twoConsecutiveBars = closeNearHighAndAboveEMA and closeNearHighAndAboveEMA[1]

// Entry condition: Within the first 10 minutes of the day and two consecutive bars match criteria
entryCondition = twoConsecutiveBars

// Exit condition: First 5-min close below 9 EMA after entry
exitCondition = close < ema9

// Plot EMA for visualization
plot(ema9, color=color.blue, linewidth=2, title="9 EMA")

// Calculate position size
positionSize = fixedAmount / close

// Strategy execution
if (entryCondition)
    strategy.entry("Buy", strategy.long, qty=positionSize)

if (exitCondition)
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/445449

> Last Modified

2024-03-19 15:03:56
