
> Name

Level-by-Level-Build-Up-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The step-by-step moving average strategy is a trading strategy based on the RENKO chart. This strategy uses the moving average indicaotr to smooth the price, and uses the intersection of moving averages in different time periods as buying and selling signals. At the same time, this strategy will also determine the stop loss level based on the ATR indicator, making the stop loss more reasonable.
## Strategy Principle
This strategy is mainly implemented through the following parts:
1. Use input to select the RENKO time period and ATR period
2. Calculate the RENKO price and color. When the price exceeds the previous RENKO price plus the current ATR, it will turn up. When the price is lower than the previous RENKO price minus the current ATR, it will turn short.
3. Use two integers BUY and SELL to record the current number of long and short orders.
4. When the price breaks through, if there is no short order, open a long position and close the short position.
When the decline breaks through, if there are no long orders, short positions will be opened, and long orders will be closed.
5. Use plot to draw RENKO diagram
With this logic, the strategy can open long or short positions when the price breaks through the previous level, and close the current position when the price reverses. At the same time, using ATR to determine the breakthrough range can determine a reasonable stop loss position based on the current volatility.
## Advantage Analysis
This strategy has several advantages:
1. Use RENKO to eliminate noise and identify trends
The RENKO chart can effectively eliminate the noise of price shocks and identify the more obvious trend direction. This is a great combination for spotting trends and following them.
2. Moving average crossovers send trading signals
Moving average crossovers in different time periods can be used as more reliable trading signal indicators to avoid being deceived by noise.
3. ATR dynamic stop loss
Using ATR to dynamically set the stop loss level can set the stop loss reasonably according to the current volatility to avoid the stop loss being too large or too small.
4. Consider both trends and moving averages
Combining trend and moving average indicators, you can take advantage of both to capture the trend while ensuring more reliable trading signals.
## Risk Analysis
There are also some risks with this strategy:
1. Wrong trend judgment
There may be errors in the way RENKO determines price trends, resulting in unnecessary buy and sell openings. Parameters need to be optimized to reduce misjudgments.
2. False signal of moving average crossover
Moving average crossover signals may contain false signals, which may lead to unnecessary buying and selling actions. The moving average cycle parameters can be appropriately optimized.
3. Improper ATR parameters
Improper setting of the ATR period can also cause the stop loss to be too large or too small. Different markets need to be tested to determine optimal parameters.
4. Sharp market fluctuations
In sideways and sharp market fluctuations, there will be many unnecessary opening and closing operations on the RENKO chart, which will occupy funds. This needs to be filtered through other indicators to avoid this kind of market trading.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize RENKO and ATR parameters
Adjusting these two parameters can minimize RENKO's misjudgments and make RENKO capture trends more accurately.
2. Add moving average cross filtering
Adding more moving averages and requiring most of the moving averages to cross in the same direction to generate signals can filter out false signals.
3. Add other indicator filters
For example, adding a volume energy indicator will only generate a trading signal when the volume energy is confirmed in the same direction, thus avoiding being trapped.
4. Optimize stop loss strategy
You can study how to stop loss only when the trend reverses, instead of simply tracking ATR, to make stop loss more reasonable.
5. Optimize fund management
Study how to optimize fund management under this strategy to increase profitability while controlling risks.
## Summarize
Overall, this strategy is a strategy worthy of optimization and real-time verification. The core idea is to use RENKO to identify trends and use moving average crossovers as filtered trading signals. Combined with ATR dynamic stop loss, it can become an advantageous trend following strategy. The next step is to continue optimization testing based on known risks to make the strategy parameters more perfect and achieve better real-time performance.

||


## Overview

The Level by Level Build Up Moving Average Strategy is a trading strategy based on RENKO charts. It uses moving average indicators to smooth price and crossovers between moving averages of different timeframes as trading signals. Meanwhile, it also uses the ATR indicator to determine stop loss levels for more reasonable stops.

## Strategy Logic

The core logic of this strategy includes:

1. Use input to select RENKO timeframe and ATR period

2. Calculate RENKO price and color. Turn to up when price breaks above previous RENKO price plus current ATR. Turn to down when price falls below previous RENKO price minus current ATR.

3. Use two integers BUY and SELL to record current long and short positions. 

4. When up breakout, if no short position then go long. If already short then close short position.
   When down breakout, if no long position then go short. If already long then close long position.

5. Plot RENKO chart using plot.

With this logic, the strategy can open long or short when price breaks previous level, and close positions when price reverse. Using ATR to determine breakout range makes stop loss more reasonable based on current volatility.

## Advantage Analysis 

This strategy has the following advantages:

1. RENKO filters noise and identifies trends
RENKO can effectively filter price noise and identify significant trends. This combination is great for trend detection and following.

2. Moving average crossovers generate trading signals
Crossovers between moving averages of different timeframes can provide reliable trading signals and avoid false signals from noise.

3. Dynamic stops with ATR
Using ATR to dynamically set stop loss can make stops more reasonable based on current volatility, avoiding stops too wide or too tight.

4. Combination of trend and moving average
Combining trend and moving average indicators utilizes the strengths of both - catching trends with RENKO while ensuring reliable signals with moving averages.

## Risk Analysis

The strategy also has some risks:

1. Incorrect trend identification
The way RENKO determines trends may result in unnecessary longs or shorts. Parameters need to be optimized to reduce false signals.

2. False signals from moving average crossovers  
There can be false signals from moving average crossovers, causing unnecessary trades. Moving average periods could be optimized.

3. Improper ATR parameters
Improper ATR period setting can also lead to stops too wide or too tight. Different markets should be tested for optimal parameters.

4. Whipsaw markets
In sideways or strong whipsaw markets, RENKO may generate many unnecessary trades, occupying capital. Other filters are needed to avoid trading such markets.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize RENKO and ATR parameters  
Adjust these parameters to minimize RENKO false signals and better catch trends.

2. Add moving average crossover filters
Add more moving averages and require most of them to align before generating signals, to filter false signals. 

3. Add other indicator filters
For example, add volume to only take trades when volume confirms price, avoiding traps.

4. Improve stop loss strategy
Research how to use trend-based stops instead of simply tracking ATR, for more logical stops.

5. Optimize money management
Research optimal capital allocation under this strategy to maximize returns while controlling risks.

## Conclusion

Overall this is a strategy worth optimizing and testing in live markets. The core idea of using RENKO for trend and moving average crossovers as filtered signals is sound. With dynamic ATR stops it can become a solid trend following system. The next step is to continue optimizing it based on the known risks to improve parameters and performance.

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|D|TimeFrame|
|v_input_2|14|ATR length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-19 00:00:00
end: 2023-09-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Renko Level Strategy 2", shorttitle="RLS2", overlay=true, pyramiding=2, currency=currency.USD, default_qty_value=50, initial_capital=2000, default_qty_type=strategy.percent_of_equity) 

TF = input(title='TimeFrame', type=input.resolution, defval="D")
ATRlength = input(title="ATR length", type=input.integer, defval=14, minval=2, maxval=100)

HIGH = security(syminfo.tickerid, TF, high)
LOW = security(syminfo.tickerid, TF, low)
CLOSE = security(syminfo.tickerid, TF, close)
ATR = security(syminfo.tickerid, TF, atr(ATRlength))

float RENKO = na
color COLOR = na
int BUY = na
int SELL = na
bool UP = na
bool DN = na

RENKO := na(RENKO[1]) ? close : RENKO[1]
COLOR := na(COLOR[1]) ? color.white : COLOR[1]
BUY := na(BUY[1]) ? 0 : BUY[1]
SELL := na(SELL[1]) ? 0 : SELL[1]
UP := false
DN := false

if(close > RENKO[1]+ATR[1])
    UP := true
    RENKO := close
    COLOR := color.lime
    SELL := 0
    BUY := BUY+1

if(close < RENKO[1]-ATR[1])
    DN := true
    RENKO := close
    COLOR := color.red
    BUY := 0
    SELL := SELL+1
    

if(BUY[1]==1 and BUY==2)
    strategy.entry("long", strategy.long)//, limit = RENKODN)

if(DN)
    strategy.cancel_all()
    strategy.close_all(comment = "close")


plot(RENKO, style=plot.style_line, linewidth=2, color=COLOR)
```

> Detail

https://www.fmz.com/strategy/427886

> Last Modified

2023-09-26 16:00:20
