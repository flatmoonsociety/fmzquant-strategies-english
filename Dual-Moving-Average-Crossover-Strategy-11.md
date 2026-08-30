
> Name

Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/7d375b3b01892cbe1e.png)
[trans]


## Overview
The double moving average crossover strategy calculates moving averages of different periods to determine the direction of the price trend and achieve trend tracking. When the short-period moving average crosses the long-period moving average, go long, and when the short-period moving average crosses below the long-period moving average, go short, which is a typical trend following strategy.
## Strategy Principle
The strategy is based on 9-, 21-, and 50-period exponential moving averages (EMA). Among them, the 9-period EMA represents the short-term trend, the 21-period EMA represents the mid-term trend, and the 50-period EMA represents the long-term trend.
When the 9-period EMA crosses above the 21-period EMA, it means that the short-term trend has turned upward, so go long; when the 9-period EMA crosses below the 21-period EMA, it means the short-term trend has turned downward, so go short. The crossover function crossover() is used here to determine the crossover of the moving average.
The code sets the logic for opening, taking profit, and stopping losses of long and short positions. The condition for opening a position is that the moving average crosses above or below. The long take profit is the entry price × (1 + the entered take profit ratio), and the short take profit is the entry price × (1 - the entered take profit ratio). The long stop loss is the entry price × (1 - the entered stop loss ratio), and the short stop loss is the entry price × (1 + the entered stop loss ratio).
In addition, the code also adds some filtering conditions, such as trend filtering, which requires that the K-line before the moving average crosses up and down cannot fluctuate, and capital utilization filtering, which requires that the strategic equity cannot be lower than the N-day moving average to avoid still trading when the loss is excessive. These filters can avoid false signals to a certain extent.
In general, this strategy uses double EMA crossover to determine the price trend direction, as well as reasonable stop-profit and stop-loss logic, which can capture the medium and long-term trend. However, as a single-factor strategy, its signal may not be stable enough and can be further optimized.
## Advantage Analysis
- Use the intersection of double moving averages to determine the trend direction. The principle is simple and easy to understand and implement.
- Using EMA of different periods, you can judge long-term and short-term trends.
- Set up stop-profit and stop-loss logic to lock in profits and control risks.
- Add filter conditions to filter out false signals to a certain extent.
- You can freely set parameters, optimize cycle combinations, and adapt to different market environments.
## Risk Analysis
- As a single-factor strategy, trading signals may not be stable enough. When prices fluctuate, multiple unnecessary transactions may occur.
- When the EMA crosses, the price may have moved for a certain distance, and there is a risk of chasing highs and selling lows.
- Transaction costs are not taken into account, and profits may be reduced during the actual offer.
- Without setting up a stop loss, losses under extreme market conditions cannot be controlled.
How to deal with it:
1. Optimize MA cycle parameters to make the signal more stable.
2. Filter signals in combination with other indicators.
3. Increase the number of transactions and reduce cost impact. 
4. Set a stop loss point to limit the maximum loss.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the period parameters of the moving average and find the best period combination. Adaptive optimization technology can be introduced to dynamically optimize the cycle.
2. Add other technical indicators to filter signals, such as MACD, KD, etc., to improve signal quality. Or introduce machine learning to score signals and automatically filter out false signals.
3. Combined with transaction volume analysis. If the moving average is exceeded but the trading volume is insufficient, the signal will not be accepted.
4. When a breakthrough occurs, examine the previous fluctuations. If the breakthrough occurs in the shock range, it may be a false breakthrough.
5. Establish a dynamic stop loss mechanism, such as trailing stop loss, Chandelier Exit, etc., to reduce the stop loss distance but ensure that the stop loss is effective.
6. Optimize position management, such as fixed positions, dynamic positions, leveraged positions, etc., to make the profit and loss ratio more reasonable.
7. Comprehensively consider the impact of transaction costs and slippage. Optimize the take-profit and stop-loss ratio to ensure that the strategy is still profitable in the real market.
## Summarize
The overall structure of this strategy is reasonable and the principle is simple. The trend direction is judged by the cross of double EMA and the stop-profit and stop-loss logic is set to capture the trend. However, as a single-factor strategy, parameter settings, signal filtering, etc. can be further optimized to make the strategy more robust. By adding mechanisms such as stop loss and position management, risks can be further reduced. Overall, this strategy provides a reliable trend following strategy framework, which can achieve stable investment returns after optimization and adjustment.
||


## Overview

The Dual Moving Average Crossover strategy judges the price trend direction by calculating moving averages of different periods, and realizes trend following. It goes long when the short period MA crosses over the long period MA, and goes short when the short period MA crosses below the long period MA. It is a typical trend following strategy.

## Strategy Logic

This strategy is based on 9, 21 and 50 period Exponential Moving Averages (EMA). The 9 period EMA represents the short term trend, 21 period EMA represents the medium term trend, and 50 period EMA represents the long term trend. 

When the 9 period EMA crosses over the 21 period EMA, it signals an uptrend in the short term, thus going long. When the 9 period EMA crosses below the 21 period EMA, it signals a downtrend in the short term, thus going short. The crossover() function is used here to determine the crossover between the MAs.

The logic for long/short entry, take profit and stop loss is configured. The entry condition is the crossover of the MAs. Long take profit is entry price * (1 + input take profit ratio), short take profit is entry price * (1 - input take profit ratio). Long stop loss is entry price * (1 - input stop loss ratio), short stop loss is entry price * (1 + input stop loss ratio).

Some filters are also added, like trend filter to avoid sideways, and equity filter to avoid trading when strategy equity is too low. These filters can help avoid some false signals.

In summary, this strategy uses dual EMA crossovers to determine price trend direction, with proper take profit and stop loss logic, which can capture mid to long term trends. But as a single factor strategy, the signals may not be stable enough and can be further optimized.

## Advantage Analysis  

- Using dual MA crossovers to determine trend direction, the logic is simple and easy to understand.

- Adopting EMAs of different periods can judge short and long term trends.

- Take profit and stop loss logic locks in profit and controls risk.

- Filters help avoid some false signals to some extent.

- Parameters can be freely configured, periods can be optimized for different market environments.

## Risk Analysis

- As a single factor strategy, trading signals may not be stable enough. Whipsaws may occur during price consolidations.

- When crossover happens, price may have already run up/down a stretch, with risk of buying high and selling low.

- Trading costs are not considered, actual returns could be lower.

- No stop loss in place, risks unlimited loss in extreme market conditions.

Solutions:

1. Optimize MA periods for more stable signals.

2. Add other indicators to filter signals. 

3. Increase trade size to lower cost impact.

4. Set proper stop loss to limit maximum loss.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize MA periods to find best combinations, or use adaptive optimization to dynamically select best periods.

2. Add other technical indicators like MACD, KD etc to filter signals and improve quality, or use machine learning to score signals and filter false ones.

3. Incorporate volume analysis. Do not take signal if volume is insufficient on MA crossover.

4. Check price fluctuations before crossover happens. Crossover in ranging market may be false signal.

5. Build dynamic stop loss mechanisms like trailing stop loss, Chandelier Exit etc, to reduce stop loss distance but keep it effective.

6. Optimize position sizing like fixed/dynamic/leveraged, to achieve more reasonable profit/loss ratios. 

7. Comprehensively consider trading costs, slippage. Optimize take profit/stop loss ratios to ensure profitability in live trading.

## Conclusion

The overall structure of this strategy is sound, with simple logic of dual EMA crossover to determine trend direction, coupled with take profit and stop loss logic to capture trends. As a single factor strategy, it can be further optimized on parameters, signal filters etc to make it more robust. With proper stop loss and position sizing, risks can be further reduced. Overall, it provides a solid trend following strategy framework, which can achieve consistent profits after optimizations and adjustments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|include longs?|
|v_input_2|true|condition two?|
|v_input_3|true|condition three?|
|v_input_4|true|include shorts?|
|v_input_5|true|condition two?|
|v_input_6|true|condition three?|
|v_input_7|200|lookback for average range (bars)|
|v_input_8|true|filter trades if range is less than (%)|
|v_input_9|40|filter trades if equity is below ema()|
|v_input_10|true|sideways filter?|
|v_input_11|true|equity filter?|
|v_input_12|true|long TP %|
|v_input_13|0.4|long SL %|
|v_input_14|true|short TP %|
|v_input_15|0.4|short SL %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-16 00:00:00
end: 2023-11-15 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © TradingMentalist

//@version=4
strategy("Initial template",initial_capital=1000, overlay=true, pyramiding=0, commission_type=strategy.commission.percent, commission_value=0.04, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, currency = currency.USD)

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////inputs
//turn on/off longs/shorts / extraneous conditions
longinc=input(true, title="include longs?")
lConSw2=input(true, title="condition two?")
lConSw3=input(true, title="condition three?")
shotinc=input(true, title="include shorts?")
sConSw2=input(true, title="condition two?")
sConSw3=input(true, title="condition three?")

//turn on/off / adjust trade filters (average range/average equity)
sidein2     = input(200, step=10, title='lookback for average range (bars)')
sidein      = input(1, title='filter trades if range is less than (%)')/100
equityIn    = input(40, title='filter trades if equity is below ema()')
sidewayssw  = input(true, title='sideways filter?')
equitysw    = input(true, title='equity filter?')
longtpin    = input(1,step=0.1, title='long TP %')/100
longslin    = input(0.4,step=0.1, title='long SL %')/100
shorttpin   = input(1,step=0.1, title='short TP %')/100
shortslin   = input(0.4,step=0.1, title='short SL %')/100

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////filters
//(leave as is)
side1       = (close[1] + close[sidein2]) / 2
side2       = close[1] - close[sidein2] 
side3       = side2 / side1
notsideways = side3 > sidein
equityMa    = equitysw ? ema(strategy.equity, equityIn) : 0
equityCon   = strategy.equity >= equityMa

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////indicators
ma1 = ema(close, 9)
ma2 = ema(close, 21)
ma3 = ema(close, 50)

plot(ma1, color=color.new(#E8B6B0,50))
plot(ma2, color=color.new(#B0E8BE,50))
plot(ma3, color=color.new(#00EEFF,50))

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////conditions
//adjust conditions
//-------------------------------------------
longCondition1  = crossover(ma2,ma3)
longCondition2  = close[5] > close[10]
longCondition3  = close[1] > close[2]

shortCondition1 = crossover(ma3,ma2)
shortCondition2 = close[5] < close[10]
shortCondition3 = close[1] < close[2]

closelong       = shortCondition1
closeshort      = longCondition1
//-------------------------------------------

//(leave as is)
longCondition1in  = longCondition1
longCondition2in  = lConSw2 ? longCondition2 : true
longCondition3in  = lConSw3 ? longCondition3 : true
shortCondition1in = shortCondition1
shortCondition2in = sConSw2 ? shortCondition2: true
shortCondition3in = sConSw3 ? shortCondition3: true
longConditions    = longCondition1in and longCondition2in and longCondition3in
shortConditions   = shortCondition1in and shortCondition2in and shortCondition3in

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////execution
//(leave as is)
long            = sidewayssw ? notsideways and equityCon and longConditions : equityCon and longConditions
short           = sidewayssw ? notsideways and equityCon and shortConditions : equityCon and shortConditions

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////risk
//(leave as is)
longtplevel     = strategy.position_avg_price * (1 + longtpin)
longsllevel     = strategy.position_avg_price * (1 - longslin)
shorttplevel    = strategy.position_avg_price * (1 - shorttpin)
shortsllevel    = strategy.position_avg_price * (1 + shortslin)

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////timeframe
//adjust timeframe
//-------------------------------------------
startyear   = 2000
startmonth  = 1
startday    = 1

stopyear    = 9999
stopmonth   = 12
stopday     = 31
//-------------------------------------------

//(leave as is)
startperiod = timestamp(startyear,startmonth,startday,0,0)
periodstop  = timestamp(stopyear,stopmonth,stopday,0,0)
timeframe()    =>
    time >= startperiod and time <= periodstop ? true : false

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////orders
//comments are empty characters for clear chart
if timeframe()
    if longinc
        if strategy.position_size == 0 or strategy.position_size > 0 
            strategy.entry(id="long", long=true, when=long, comment=" ")
            strategy.exit("stop","long", limit=longtplevel, stop=longsllevel,comment=" ")
            strategy.close(id="long", when=closelong, comment = " ")
    if shotinc
        if strategy.position_size == 0 or strategy.position_size < 0 
            strategy.entry(id="short", long=false, when=short, comment = " ")
            strategy.exit("stop","short", limit=shorttplevel, stop=shortsllevel,comment = " ")
            strategy.close(id="short", when=closeshort, comment = " ")
```

> Detail

https://www.fmz.com/strategy/432363

> Last Modified

2023-11-16 17:50:52
