
> Name

Oscillating-Channel-Breakout-Strategy Oscillating-Channel-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/de1c4a7d48795a06a7654446f3c9c1a350914ad4706d865fe51eb312fa70fc87.png)
[trans]


## Overview
This strategy is a breakout trading strategy based on the channel indicator. It uses the oscillation characteristics of the upper and lower rails of the channel to go long when the price breaks through the upper rail of the channel and short when it breaks through the lower rail of the channel. It is a trend following type strategy.
## Strategy Principle
This strategy first uses SMA to calculate the central axis of the channel, adds a parameter value to the central axis as the upper track, and subtracts a parameter value as the lower track to form a price channel. Then judge whether the price breaks through the upper and lower rails, and combine it with the surge in trading volume as a signal to open a position. When the price falls back into the channel, it is used as a signal to close the position.
Specifically, the trading logic of the strategy is as follows:
1. Calculate the central axis of the channel: SMA (closing price, N)
2. Channel upper trajectory: central axis + parameter value
3. Channel lower trajectory: central axis - parameter value
4. When breaking through the upper rail line, if the conditions for trading volume to be greater than twice the previous period are met, enter the market long.
5. When it falls back into the channel, close the long position
6. When breaking through the lower trajectory, if the conditions for trading volume to be greater than twice the previous period are met, enter the market short.
7. When it falls back into the channel, close the short position
## Advantage Analysis
This strategy has the following advantages:
1. Use channel indicators to effectively track price trends.
2. Combined with the conditions of surge in trading volume, false breakthroughs can be effectively filtered.
3. Falling back into the channel serves as a stop-loss exit mechanism, which can limit the loss of a single transaction.
4. The oscillatory characteristics are suitable for capturing short- and medium-term trends.
5. The implementation logic is simple and easy to understand and implement.
## Risk Analysis
There are also some risks with this strategy:
1. When the price is on one side of the channel for a long time, it will continuously trigger the opening of positions in the same direction and face the risk of loss.
2. Improper channel parameter settings may result in excessive error signals.
3. Improper judgment criteria for a surge in trading volume may also miss the real breakthrough signal.
4. The stop-loss exit mechanism may be too conservative and miss larger market trends.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize channel parameters to make them more suitable for the characteristics of different markets.
2. Optimize or increase the opening conditions, such as considering long and short moving averages, or Kline patterns, etc. to avoid false breakthroughs.
3. Optimize the stop-loss exit mechanism, appropriately relax the stop-loss range, and avoid premature exit.
4. Add a position management mechanism to adjust positions and capital utilization according to market conditions.
5. Combine more indicators to determine the direction of large-level trends and avoid going against the general trend.
## Summarize
Overall, this strategy is a relatively simple and practical trend following strategy. It takes advantage of the oscillating characteristics of the price channel and can effectively capture short- and medium-term trends. However, you also need to pay attention to optimizing parameter settings and guarding against the risks involved, so as to obtain better strategic effects. If optimized with more indicators and technical means, the stability and profitability of the strategy can be further enhanced.
||


## Overview

This is a breakout trading strategy based on channel indicators. It utilizes the oscillation characteristic of the channel bands to go long when price breaks out above the upper band and go short when breaking out below the lower band. It belongs to the trend following strategy category.

## Strategy Logic

The strategy first uses SMA to calculate the midline of the channel. The upper band is set as midline plus a parameter value, and the lower band is midline minus the parameter value, forming a price channel. It then judges if price breaks out of the upper or lower bands, combined with a surge in trading volume as the opening signal. When price falls back into the channel, it serves as the closing signal.

Specifically, the trading logic is as follows:

1. Calculate midline: SMA(close, N) 

2. Upper band: midline + parameter value

3. Lower band: midline - parameter value

4. When price breaks out above upper band, if trading volume is greater than 2x of previous period, go long.

5. When price falls back into channel, close long position.

6. When price breaks out below lower band, if trading volume is greater than 2x of previous period, go short. 

7. When price falls back into channel, close short position.

## Advantage Analysis 

The advantages of this strategy are:

1. Using channel indicator can effectively track price trends.

2. Combining with surge in trading volume filters false breakouts well. 

3. Falling back into channel serves as stop loss mechanism and limits loss per trade.

4. Oscillation characteristic fits capturing medium-term trends. 

5. Simple logic makes it easy to understand and implement.

## Risk Analysis

There are also some risks:

1. Consecutive same direction trades when price sticks on one side of channel for long, increasing loss risk.

2. Improper channel parameter setting may cause excessive false signals. 

3. Wrong criteria for trading volume surge may miss true breakout signals.

4. The stop loss mechanism may be too conservative, missing bigger moves.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize channel parameters to fit different market characteristics.

2. Enhance open position criteria, like considering MA crossover or candlestick patterns, to avoid false breakouts.

3. Optimize stop loss mechanism, allow wider stop loss range to avoid premature exit. 

4. Add position sizing rules to adjust position size and capital utilization based on market conditions.

5. Incorporate more indicators to determine overall trend direction, avoiding trading against major trend.

## Summary 

In summary, this is a simple and practical trend following strategy. By utilizing the channel oscillation, it can effectively capture medium-term trends. But parameter tuning is needed to fit different markets, and risks should be monitored. Further optimizations with more indicators and techniques can enhance its stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|Period|
|v_input_2|25|Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-08 00:00:00
end: 2023-11-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Copyright, 2022, Cache_that_pass.  You are free to use this script however you see fit and reproduce it in any manner.

//@version=5

            //////  Name the strategy between the 2 quotation marks.  Consider setting commission type and value in strategy header to match exchanges rates. //////

strategy("Oscillating SSL Channel Strategy", "O-SSL Strat", overlay=true, pyramiding=1, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, initial_capital = 100, calc_on_order_fills=true)



            //////  Inputs and calculations used by script  //////

period = input(title='Period', defval=25)
len = input(title='Period', defval=25)
smaHigh = ta.sma(high, len)
smaLow = ta.sma(low, len)
Hlv = int(na)
Hlv := close > smaHigh ? 1 : close < smaLow ? -1 : Hlv[1]
sslDown = Hlv < 0 ? smaHigh : smaLow
sslUp = Hlv < 0 ? smaLow : smaHigh

            //////  Show me the money  //////

plot(sslDown, linewidth=2, color=color.new(color.red, 0))
plot(sslUp, linewidth=2, color=color.new(color.lime, 0))


            //////  Trade execution logic  //////  
            
//pseudo-code//
        //Go long when high (or maybe close) breaks above the sslUp and volume is 2x or > Volume[1] and sslUp > sslDown
        //Close the above longs when sslUp crosses under sslDown (or set takeprofit and stop loss exits)
        //
        //Go short when low is lower than the sslUp and volume is 2x or > Volume[1] and sslDown > sslUp
        //Close shorts when sslDown crosses under sslUp

longCondition1 = (sslUp > sslDown)
longCondition2 = ta.crossover(high, sslUp)
//longCondition3 = (volume >= (volume[1]*1.89))
longCondition = ((longCondition1) and (longCondition2))// and (longCondition3))

longExit = ta.crossunder(sslUp, sslDown)

            //////  Bring It  //////
if (longCondition)
    strategy.entry("Bring It", strategy.long)

            //////  Sling It  //////
if (longExit)
    strategy.close("Bring It", comment="Sling It")


shortCondition1 = (sslDown) > (sslUp)
shortCondition2 = ta.crossunder(low, sslUp)
//shortCondition3 = (volume >= (volume[1]*1.89))
shortCondition = ((shortCondition1) and (shortCondition2))// and (shortCondition3))

shortExit = ta.crossunder(sslDown, sslUp)

            //////  Bring It  //////
if (shortCondition)
    strategy.entry("Bring It", strategy.long)

            //////  Sling It  //////
if (shortExit)
    strategy.close("Bring It", comment="Sling It")

            //////  Sling It  //////
if (shortCondition)
    strategy.entry("Sling It", strategy.short)

            //////  Bling It  //////
if (shortExit)
    strategy.close("Sling It", comment="Bring It")


```

> Detail

https://www.fmz.com/strategy/432214

> Last Modified

2023-11-15 16:01:09
