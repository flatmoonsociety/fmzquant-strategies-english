
> Name

Donchain-Channel-Based-Trading-Strategy based on multi-scale Donchain step-by-step channel
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/91010e376227ee5268.png)
[trans]
## Overview
This is a trading strategy that uses the Tangqi Channel on multiple time scales to determine entry and exit points. The main idea of ​​the strategy is: judge the trend direction on a longer time scale and find the entry opportunity; judge the trend reversal on a shorter time scale and find the exit opportunity.
## Strategy Principle
This strategy mainly utilizes the concept of Tangqi channel. Tangqi Channel consists of the upper edge, lower edge and middle line of the channel. Channel width varies with time scale. Here we use different time scales to construct the Tangqi channel, specifically:
1. Use 52 cycles to construct the Tangqi channel on a longer time scale, and obtain the upper edge, lower edge and center line of the channel.
2. Use 12 periods to construct the Tangqi channel on a shorter time scale, and obtain the upper edge, lower edge and center line of the channel.
Entry logic: When the price breaks through the upper edge of the longer time scale channel, it is judged as the opportunity for long entry. In order to avoid false breakthroughs, we require that the closing price of at least one K line among the recent three K lines is higher than the upper edge of the channel of the K line. This can avoid false breakthroughs caused by short-term excessive expansion.
Exit logic: When the price falls below the lower edge of the shorter time scale channel, it is judged as the time to close the position and exit. We also require that the closing price of at least one K line among the recent three K lines is lower than the lower edge of the channel of the K line. This can confirm the effectiveness of the breakthrough and avoid being trapped.
## Strategic Advantages
1. This strategy combines the advantages of trend following and reversal trading. The longer time scale determines the direction of the trend, and the shorter time scale determines the local reversal. The combination of the two can capture local fluctuations in the trend.
2. The use of multi-time scale analysis can better deal with the problem of false breakthroughs, making entry and exit more clear and effective.
3. Through parameter optimization, it can adapt to different varieties and market environments.
## Risks and Solutions
1. This strategy is sensitive to parameters, and different parameters may produce completely different results. Optimization needs to be fully tested to find the best combination of parameters.
2. In volatile market conditions, the strategy may generate a large number of trading signals, leading to over-trading. You can control a single loss by configuring a stop loss.
3. The strategy does not consider the large-level trend judgment logic and may fail at the bull-bear transition point. It can be combined with other indicators to determine large-level trends.
## Optimization direction
1. Carry out parameter optimization and find the best parameter combination. Optimize parameters such as cycle length and channel type.
2. Add stop loss logic. Configure a reasonable trailing stop to control single losses.
3. Combine with other indicators to determine large-level trends. For example, EMA, K-line channel, Mike indicator, etc. Avoid failure at critical turning points.
## Summarize
This strategy is generally a typical multi-time scale channel breakthrough strategy. It well integrates the advantages of trend following and reversal trading, and achieves the effect of capturing local fluctuations in the trend through channel judgment on different time scales. If the parameters are optimized in place, the effect will be excellent in markets with obvious trends. However, the strategy itself is relatively fragile and is sensitive to parameters and judgments on grasping the overall trend. It is recommended to use it in combination with other large-level trading strategies or indicators to achieve better results.
||

## Overview

This is a trading strategy that utilizes Donchain channels over multiple timeframes to determine entry and exit points. The core idea is to judge the trend direction on a longer timeframe for entry signals, and look for trend reversals on a shorter timeframe for exit signals.  

## Strategy Logic

The strategy mainly leverages the concept of Donchain channels, which consists of the channel tops, bottoms and midlines. The channel width varies over different timeframes. Specifically, we construct Donchain channels over two timescales:

1. Use 52 periods to construct a longer-term Donchain channel and obtain its top, bottom and midline.  

2. Use 12 periods to construct a shorter-term Donchain channel and obtain its top, bottom and midline.

Entry logic: When price breaks above the longer-term channel top, we determine it as a long entry signal. To avoid false breakouts, we require at least 1 candle in the recent 3 closed above its channel top.  

Exit logic: When price breaks below the shorter-term channel bottom, we determine it as an exit signal to close long positions. Similarly, we require at least 1 candle in the recent 3 closed below its channel bottom to confirm the validity of the breakdown.

## Advantages

1. The strategy combines the merits of both trend following and mean reversion trading. The longer timeframe judges the trend while the shorter timeframe captures local reversals within the trend.  

2. Using multi-timeframe analysis helps address issues with false breakouts and makes entries/exits more valid. 

3. Parameters can be optimized for different products and market regimes.

## Risks & Solutions

1. The strategy is sensitive to parameters. Different parameters may lead to drastically different results. Adequate testing and optimization is needed to find the optimal parameter set.  

2. It may trigger excessive trades in ranging markets. A stop loss should be used to control single trade loss.

3. It does not consider the overall market regime. May fail at major trend reversal points. Other indicators should be used to gauge the major trend.

## Optimization Directions 

1. Conduct parameter optimization to find the best parameters, including channel periods, channel types etc.  

2. Incorporate stop loss logic with reasonable trailing stops to control loss.

3. Combine other indicators to determine major trend, such as EMA, Keltner Channels, MACD etc, avoiding failures at key turning points.


## Conclusion

In summary, this is a typical multi-timeframe Donchain channel breakout strategy. It integrates both trend following and mean reversion nicely to capture local reversals within trends. With optimized parameters, it can perform very well in trending markets. However, the strategy itself is fragile, sensitive to parameters and overall market regime. It is recommended to combine with other strategies or indicators to achieve more robust results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|21|Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-20 00:00:00
end: 2024-02-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © venkyrocker7777

//@version=5

strategy('Donchain channel based investment strategy', shorttitle='Donchain channel strategy', overlay=true)

Length = input.int(21, minval=1)
xPrice = close
xvnoise = math.abs(xPrice - xPrice[1])
nAMA = 0.0
nfastend = 0.666
nslowend = 0.0645
nsignal = math.abs(xPrice - xPrice[Length])
nnoise = math.sum(xvnoise, Length)
nefratio = nnoise != 0 ? nsignal / nnoise : 0
nsmooth = math.pow(nefratio * (nfastend - nslowend) + nslowend, 2)
nAMA := nz(nAMA[1]) + nsmooth * (xPrice - nz(nAMA[1]))
plot(nAMA, color=color.new(color.blue, 0), title='KAMA')

// Function to get Lower Channel, Upper Channel, Middle Channel for a period length
getLCUCMC(PeriodLength) =>
    lowestValueInThePeriod = ta.lowest(PeriodLength)  // LC
    highestValueInThePeriod = ta.highest(PeriodLength)  // UC
    middleChannelInTheperiod = math.avg(highestValueInThePeriod, lowestValueInThePeriod)  // MC
    // Returns Lower Channel, Upper Channel, Middle Channel for a period length
    [lowestValueInThePeriod, highestValueInThePeriod, middleChannelInTheperiod]

// Longer time frame for entry
longerPeriod = 52

// Shorter time frame for exit
shorterPeriod = 12

if timeframe.period == 'D'
    // Longer time frame for entry
    longerPeriod := 52 * 5

    // Shorter time frame for exit
    shorterPeriod := 12 * 5
    shorterPeriod

if timeframe.period == 'M'
    // Longer time frame for entry
    longerPeriod := 12

    // Shorter time frame for exit
    shorterPeriod := 3
    shorterPeriod

// Get Lower Channel, Upper Channel, Middle Channel for longerPeriod, shorterPeriod
[lowestValueInTheLongerPeriodLength, highestValueInTheLongerPeriodLength, middleChannelInLongerperiod] = getLCUCMC(longerPeriod)
[lowestValueInTheShorterPeriodLength, highestValueInTheShorterPeriodLength, middleChannelInShorterperiod] = getLCUCMC(shorterPeriod)


// Plot Upper Channel of longerPeriod in dark green
plot(highestValueInTheLongerPeriodLength, 'highestValueInTheLongerPeriodLength', color=color.new(color.green, 0))

// Plot Lower Channel of shorterPeriod in dark red
plot(lowestValueInTheShorterPeriodLength, 'lowestValueInTheShorterPeriodLength', color=color.new(color.red, 0))

// Entry Plan
// Will start to see if we can enter when high crosses up longer period high (high >= highestValueInTheLongerPeriodLength)
// Check if any of the three past candles and enter when any of the 3 past candles satisfy
// 1) high of that candle >= highestValueInTheLongerPeriodLength of that candle (high[i] >= highestValueInTheLongerPeriodLength[i])
// 2) close of entry point consideration candle is above close of that candle (close > close[i])
isThisPointAnEntry() =>
// Check last 3 bars
    isThisPointAnEntry = false
    offset = 0
    for i = 1 to 3 by 1
        isCurrentCandleALongerPeriodHigh = high >= highestValueInTheLongerPeriodLength
        isCurrentCandleCloseGreaterThanPreiousIthOne = close > close[i]
        isPreviousIthCandleAlsoALongerPeriodHigh = high[i] >= highestValueInTheLongerPeriodLength[i]
        isThisPointAnEntry := isCurrentCandleALongerPeriodHigh and isCurrentCandleCloseGreaterThanPreiousIthOne and isPreviousIthCandleAlsoALongerPeriodHigh
        if isThisPointAnEntry
            offset := -i
            break
    [isThisPointAnEntry, offset]

// Exit Plan - same as entry plan, with things reversed and also on a shorter time frame
// Will start to see if we should exit when low crosses down longer period low (low <= lowestValueInTheShorterPeriodLength)
// Check if any of the three past candles and exit when any of the 3 past candles satisfy
// 1) low of that candle <= highestValueInTheLongerPeriodLength of that candle (low[i] <= lowestValueInTheShorterPeriodLength[i])
// 2) close of exit point consideration candle is below close of that candle (close < close[i])
isThisPointAnExit() =>
// Check last 3 bars
    isThisPointAnExit = false
    for i = 1 to 3 by 1
        isCurrentCandleAShorterPeriodLow = low <= lowestValueInTheShorterPeriodLength
        isCurrentCandleCloseLesserThanPreiousIthOne = close < close[i]
        isPreviousIthCandleAlsoAShorterPeriodLow = low[i] <= lowestValueInTheShorterPeriodLength[i]
        isThisPointAnExit := isCurrentCandleAShorterPeriodLow and isCurrentCandleCloseLesserThanPreiousIthOne and isPreviousIthCandleAlsoAShorterPeriodLow
        break
    isThisPointAnExit

[isEntry, offset] = isThisPointAnEntry()


if isEntry
    strategy.entry('Buy', strategy.long)

strategy.close_all(when=isThisPointAnExit() == true)

if year(timenow) == year(time) and month(timenow) == month(time) and dayofmonth(timenow) - 2 == dayofmonth(time)
    strategy.close_all()


```

> Detail

https://www.fmz.com/strategy/442936

> Last Modified

2024-02-27 14:57:37
