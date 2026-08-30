
> Name

Trix Simple Trend Following Strategy Trix-Simple-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
Trix Simple Trend Following Strategy is a simple trend following strategy based on the Trix indicator. It uses the Trix indicator to determine price trends and combines it with moving averages for buying and selling. This strategy is suitable for medium and long-term trading and can gain profits in larger trends.
## Strategy Principle
This strategy is mainly based on the Trix indicator. The Trix indicator is a technical analysis tool capable of identifying price trends. It calculates its velocity changes by taking a triple smoothed moving average of the price. When the Trix crosses its moving average above, it is a buy signal, and when it crosses below its moving average, it is a sell signal.
Specifically, the strategy first calculates two sets of Trix indicators with different parameters, named Trix and Trix1 respectively. The Trix parameters are (7,4,4), and the Trix1 parameters are (4,4,4). Then calculate the 20-day simple moving average of Trix to obtain the middle band.
When the fast moving average EMA13 crosses the slow moving average SMA68, and Trix is ​​below the middle band, it is a buy signal; when Trix1 crosses Trix, a buy is triggered. The position is closed when Trix returns to the middle band.
When EMA13 goes below SMA68 and Trix is ​​above the middle band, it is a sell signal; when Trix1 goes below Trix, a sell is triggered. The position is closed when the Trix goes back through the middle band.
## Strategic Advantages
This is a very simple trend following strategy with the following advantages:
1. Use the Trix indicator to effectively identify price trends and reduce false signals.
2. Combining the fast and slow moving average systems can help determine the trend direction.
3. Combining two sets of different parameter Trix indicators can improve signal quality.
4. The middle band filter increases the filtering effect and avoids frequent opening of positions in volatile market conditions.
5. Suitable for medium and long-term trend trading and will not be disturbed by short-term fluctuations.
6. Easy to understand and implement, suitable for novices to learn.
## Strategy Risk
There are also some risks to be aware of with this strategy:
1. In a stable trend, you cannot follow the trend in time and miss some profits.
2. In sharply volatile market conditions, the Trix indicator may produce false signals.
3. Improper management of fast and slow moving average positions may lead to increased losses.
4. Lack of stop-loss strategy and inability to effectively control single losses.
5. Improper parameter settings may lead to excessive trading frequency or poor signal quality.
6. Transaction fees may account for part of the profit.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Add stop loss strategies, such as trailing stop loss or ATR stop loss, to control single losses.
2. Optimize Trix parameters, find a more suitable parameter combination, and improve signal quality.
3. Add other indicator filters, such as MACD, KDJ, etc., to avoid false signals.
4. Dynamically adjust fast and slow moving average parameters according to market conditions to improve flexibility.
5. Add trend judgment indicators, such as ADX, to avoid counter-trend trading.
6. To distinguish between bull and bear markets, use different parameter combinations.
7. Optimize the timing of entry and enter the market after the trend is confirmed.
## Summarize
Trix Simple Trend Following Strategy Overall, this is an easy to implement trend following strategy. It uses the Trix indicator to determine the trend direction and combines it with the moving average to generate trading signals. The advantage of this strategy is that it is simple and easy to use, can effectively track medium and long-term trends, and is suitable for novices to learn. But there are also some risks that need to be taken care of. Through appropriate optimization, the effectiveness of the strategy can be improved. Overall, this strategy provides a simple and practical trend trading idea for beginners.
||

## Overview

The Trix simple trend following strategy is a simple trend following strategy based on the Trix indicator. It uses the Trix indicator to judge price trends and combines moving averages to generate buy and sell signals. This strategy is suitable for medium-to-long term trading and can profit from larger trends.

## Strategy Logic 

This strategy is mainly based on the Trix indicator. The Trix indicator is a technical analysis tool that can identify price trend changes. It calculates the rate of change of prices through triple smoothed moving averages. When the Trix crosses above its moving average, it is a buy signal. When the Trix crosses below its moving average, it is a sell signal.

Specifically, this strategy first calculates two groups of Trix indicators with different parameters, named Trix and Trix1. The parameters for Trix are (7,4,4) and for Trix1 are (4,4,4). Then it calculates the 20-day simple moving average of Trix to get the middle band.

When the faster EMA13 crosses above the slower SMA68, and Trix is below the middle band, it is a buy signal. When Trix1 crosses above Trix, it triggers the buy. When Trix crosses back above the middle band, it closes the position. 

When EMA13 crosses below SMA68, and Trix is above the middle band, it is a sell signal. When Trix1 crosses below Trix, it triggers the sell. When Trix crosses back below the middle band, it closes the position.

## Advantages

This is a very simple trend following strategy with these advantages:

1. Using the Trix indicator can effectively identify price trends and reduce false signals.

2. Combining fast and slow moving averages helps determine trend direction. 

3. Using two Trix indicators with different parameters improves signal quality.

4. The middle band filter increases the filtering effect and avoids frequent opening during market oscillation.

5. It is suitable for medium-to-long term trend trading and is not disturbed by short-term fluctuations.

6. It is easy to understand and implement, suitable for beginners to learn.

## Risks

There are also some risks to note for this strategy:

1. It cannot catch trends in time during stable trends, missing some profits.

2. The Trix indicator may generate incorrect signals during huge market swings.

3. Improper fast and slow moving average position management can lead to greater losses. 

4. It lacks a stop loss strategy and cannot effectively control single losses.

5. Improper parameter settings may lead to too high trading frequency or poor signal quality.

6. Transaction fees may take up some profits.

## Optimization

This strategy can be optimized in the following aspects:

1. Add stop loss strategies like trailing stop loss or ATR stop loss to control single losses.

2. Optimize Trix parameters to find more suitable combinations and improve signal quality.

3. Add other indicator filters like MACD, KDJ etc. to avoid false signals. 

4. Dynamically adjust fast and slow moving average parameters based on market conditions to improve flexibility.

5. Add trend judging indicators like ADX to avoid trading against the trend.

6. Use different parameter sets to distinguish bull and bear markets.

7. Optimize entry timing and enter after trend confirmation.

## Conclusion

In summary, this is an easy to implement trend following strategy. It uses the Trix indicator to determine trend direction and generates trading signals in combination with moving averages. The advantages are its simplicity and ability to effectively track medium-to-long term trends, making it suitable for beginners to learn. But risks exist and need to be prevented. With proper optimizations, the strategy's effectiveness can be improved. Overall, it provides beginners with a simple and practical trend trading idea.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|7|lengtha|
|v_input_2|4|lengtha1|
|v_input_3|20|bb|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-07 00:00:00
end: 2023-10-07 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Trix simple", overlay=true)

///_____________Made by Zan______//
// All thanks to Nmike's Chat, go visit there lol, you'll learn a lot.//

//Length setting
lengtha = input(7, minval=1)
lengtha1 = input(4, minval=1)
Trix = 10000 * change(ema(ema(ema(log(close), lengtha), lengtha), lengtha)) // TRIX 5
Trix1= 10000 * change(ema(ema(ema(log(close), lengtha1), lengtha1), lengtha1)) // TRIX 3
bb = input(20)
Middle_Band = sma(Trix, bb)
sma68 = sma(close,68)
ema13 = sma(close,13)



longCondition = ema13>sma68 and Middle_Band>0 and Trix<Middle_Band
if (longCondition)
    strategy.entry("Buy", strategy.long, when = crossover(Trix1,Trix))
    strategy.exit("Buy", when = cross(Trix,Middle_Band))
    
    
shortCondition = ema13<sma68 and Middle_Band<0 and Trix>Middle_Band
if (shortCondition)
    strategy.entry("Sell", strategy.short, when = crossunder(Trix1,Trix))
    strategy.exit("Sell",when = cross(Trix,Middle_Band))
```

> Detail

https://www.fmz.com/strategy/428683

> Last Modified

2023-10-08 12:17:21
