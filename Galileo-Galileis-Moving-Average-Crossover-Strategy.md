
> Name

Galileo-Galileis-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1206dde7851f7e1f48b.png)
[trans]

## Overview
The Galilean Moving Average Crossover Strategy is a trading strategy based on moving averages. This strategy generates trading signals by calculating an exponential moving average for a certain period and cross-comparing it with the price. When the price falls below the moving average, a sell signal is generated; when the price breaks above the moving average, a buy signal is generated. The strategy takes its name from Galileo Galilei
## Strategy Principle
The core of the Galilean Moving Average crossover strategy is the exponential moving average (EMA). EMA is a moving average algorithm that tends to give more weight to recent prices. Its calculation formula is:
EMA today = (Closing price today × smoothing constant) + (EMA yesterday × (1-smoothing constant))
Among them, the smoothing constant α=(2/(number of periods + 1)).
This strategy calculates the EMA value in real time based on the period length entered by the user. The price is then compared to the EMA to determine the intersection between the two as buy and sell signals:
1. When the price falls below the EMA from above, a sell signal is generated for short-term operations.
2. When the price breaks through the EMA from bottom to top, a buy signal is generated and a long operation is performed.
This strategy simultaneously plots EMA lines and arrows that mark buy and sell signals.
## Advantage Analysis
The Galileo moving average crossover strategy has the following advantages:
1. The idea is simple, easy to understand and implement, and suitable for beginners.
2. Through the use of EMA, you can respond to price changes more quickly.
3. The cross signal is clear and there will be no frequent buying and selling.
4. You can adjust EMA parameters to adapt to different market environments.
5. Clear entry and exit signals and control risks.
## Risk Analysis
The Galileo moving average crossover strategy also has the following risks:
1. When prices fluctuate violently, more false signals will appear, affecting the effect. Stop loss strategies can be set for optimization.
2. A single indicator is susceptible to fraud and signal failure. Additional indicators can be added for optimization.
3. There is a certain degree of lag, especially after emergencies occur. Shortening moving average parameters can be tested.
4. Unable to adapt to long-term and sustained unilateral price trends. This is a common shortcoming of moving average strategies.
## Optimization direction
The Galilean moving average crossover strategy can be optimized in the following directions:
1. Combine with other indicators to build a composite strategy to avoid false signals and improve stability. For example, add trading volume, trend indicators, etc.
2. Add stop loss strategy, set trailing stop loss or percentage stop loss to control single loss.
3. Test the effects of different parameters of EMA and choose the best parameter combination. Other types of moving averages can also be tested.
4. Evaluate adding a re-entry mechanism to re-enter the market after price reversal to increase profitability.
## Summarize
The Galilean moving average crossover strategy is a simple and practical trading strategy with clear ideas and easy operation. It is suitable for beginners in quantitative trading. With continuous optimization and improvement, I believe its effect will become better and better, and it is worth recommending.
||

## Overview

Galileo Galilei's moving average crossover strategy is a trading strategy based on moving averages. It generates trading signals by calculating the exponential moving average (EMA) over a specified period and comparing crossovers between the EMA and price. Sell signals are generated when the price drops below the EMA from the top down, while buy signals occur when the price breaks above the EMA from the bottom up.

## Strategy Logic

The core of Galileo Galilei's strategy lies in the exponential moving average (EMA). EMA is a type of moving average that places more weight on recent prices. Its calculation formula is:

EMA today = (Closing price today × Smoothing factor) + (EMA yesterday × (1 − Smoothing factor))

Where the smoothing factor α = (2/(number of periods + 1))

The strategy dynamically calculates the EMA based on user input period parameters. It then compares the crossovers between price and EMA to determine trading signals:  

1. When price drops below the EMA from the top down, a sell signal is generated for short trading.

2. When price breaks above the EMA from below, a buy signal is triggered for long trading.

The strategy also plots the EMA line on the chart, along with arrow markers indicating buy and sell signals.

## Advantage Analysis 

Galileo Galilei's moving average crossover strategy has the following advantages:

1. Simple logic that is easy to understand and implement, suitable for beginners.  
2. Faster response to price changes through the use of EMA.
3. Clear crossover signals without excessive whipsaws.  
4. Flexibility to adapt to different market environments by adjusting EMA parameters.
5. Defined entry and exit signals provide risk control.

## Risk Analysis

Potential risks of this strategy include:

1. More false signals may occur during high price volatility. A stop loss strategy could help optimize.
2. Reliance on a single indicator makes it vulnerable to price manipulation. Additional indicators may improve robustness.   
3. Lagging effect, especially after sudden events. Shortening EMA periods could help.
4. Unable to adapt to prolonged one-sided price trends, a common limitation among moving average strategies.

## Optimization Directions

Some ways to optimize the strategy:

1. Incorporate other indicators to construct a composite strategy for increased robustness against false signals. Examples include volume, trend indicators etc.

2. Add stop loss mechanisms like trailing stop loss or percentage-based stop loss to control single-trade loss amount.

3. Test EMAs with different parameter combinations to find optimal settings. Other moving average types could also be evaluated.  

4. Assess re-entry logic to capture rebounds after initial price reversals, improving profitability.

## Conclusion

Galileo Galilei's moving average crossover is a simple yet practical strategy with clear logic and easy operability. It is suitable for novice quant traders. With continuous improvements, its performance could become increasingly superior over time.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|11|Length|
|v_input_2_open|0|Source: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|true|From Day|
|v_input_4|true|From Month|
|v_input_5|2020|From Year|
|v_input_6|true|To Day|
|v_input_7|12|To Month|
|v_input_8|2021|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-11 00:00:00
end: 2023-12-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © armigoldman

//@version=3
strategy(title="Galileo Galilei", shorttitle="Galileo Galilei", overlay=true, initial_capital = 100000, default_qty_type=strategy.cash, default_qty_value = 100000)
len = input(11, minval=1, title="Length")
src = input(open, title="Source")
out = ema(src, len)
plot(out, title="EMA", color=yellow)
//last8h = highest(close, 8)
//lastl8 = lowest(close, 8)

//plot(last8h, color=red, linewidth=2)
//plot(lastl8, color=green, linewidth=2)

////////////////////////////////////////////////////////////////////////////////
// BACKTESTING RANGE

// From Date Inputs
fromDay = input(defval=1, title="From Day", minval=1, maxval=31)
fromMonth = input(defval=1, title="From Month", minval=1, maxval=12)
fromYear = input(defval=2020, title="From Year", minval=1970)

// To Date Inputs
toDay = input(defval=1, title="To Day", minval=1, maxval=31)
toMonth = input(defval=12, title="To Month", minval=1, maxval=12)
toYear = input(defval=2021, title="To Year", minval=1970)

// Calculate start/end date and time condition
startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true


bearish = cross(close, out) == 1 and close[1] > close
bullish = cross(close, out) == 1 and close[1] < close

plotshape(bearish, color=white, style=shape.arrowdown, text="BEAR", location=location.abovebar)
plotshape(bullish, color=white, style=shape.arrowup, text="BULL", location=location.belowbar)

buy = if cross(close, out) == 1 and close[1] < close
    strategy.entry("BUY", strategy.long, when=time_cond)
        //strategy.close_all(when=bearish)
        // strategy.exit("exit", "Long", profit =, loss = 35)


sell = if cross(close, out) == 1 and close[1] > close
    strategy.entry("SELL", strategy.short, when=time_cond)
        //sell = if bearish
        //strategy.close_all(when=bullish)
        // strategy.exit("exit", "Long", profit = bullish, loss = 100)

profit = strategy.netprofit
if not time_cond
    strategy.close_all()

//plotshape(true, style=shape.triangleup, location=location.abovebar)

```

> Detail

https://www.fmz.com/strategy/435717

> Last Modified

2023-12-18 12:07:07
