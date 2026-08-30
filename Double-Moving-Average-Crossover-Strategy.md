
> Name

Double-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](assets/images/7ab368f2007ca4db90cfdf0105513783c3c6f1818e73bc655f19fdca03ae9afd.png)
[trans]

## Overview
The double moving average breakout strategy is a trend following strategy based on the crossover of two moving averages with different periods as buy and sell signals. This strategy uses the intersection of the fast average and the slow average as the trading entry point. After the intersection, the trend direction is determined and the corresponding long or short position is established. It can not only capture the intermediate-level trend, but also reduce the problem of excessive trading frequency caused by unnecessary jitter.
## Strategy Principle
This strategy uses two moving averages: a fast MA and a slow MA. The fast MA cycle is generally set to a shorter period (such as 15 periods) to capture short-term price changes; the slow MA cycle is generally set to a longer period (such as 21 periods) to determine the main trend direction. The trading signal of the strategy comes from the intersection of two MAs: when the fast MA crosses above the slow MA, it is a buy signal; when the fast MA crosses below the slow MA, it is a sell signal.
By setting different MA cycle combinations, you can adjust the length of time for the strategy to capture the trend. A shorter MA combination can capture short-term, small-cycle price change opportunities; a longer MA combination can filter out shocks and only capture longer-term trends.
The strategy also includes risk management modules: take profit, stop loss, and trailing stop. This can limit the maximum profit or loss of a single transaction and help protect overall profits.
## Strategic Advantages
The double moving average strategy has the following advantages:
1. The concept is simple, easy to understand and implement;
2. You can adjust the MA cycle to adapt to different market environments and capture trends of different lengths of time;
3. Relatively stable and avoid too frequent transactions;
4. Combined with stop loss and stop profit, risks can be effectively controlled;
5. Easy to optimize, MA cycle, risk management parameters, etc. can be adjusted to further improve the effect.
## Risk Analysis
There are also certain risks in the double moving average strategy, which are mainly concentrated in the following aspects:
1. During the shock and consolidation stage, MA cross signals may be too frequent, causing the problem of excessive trading frequency;
2. There is a lag between the two moving averages, and the price reversal point may be missed and the loss cannot be stopped in time;
3. It cannot effectively filter out false breakthroughs, which may cause unnecessary losses;
4. MA itself is slow to respond to price and cannot fully track price changes.
These risks can be improved and optimized by adjusting MA parameters, adding filter conditions, optimizing stop loss logic, etc.
## Optimization direction
The double moving average strategy can be optimized from the following aspects:
1. Add filters such as trading volume or volatility indicators to avoid frequent opening of positions during shocks and false breakthroughs;
2. MA cycles and combinations can be diversified and adjusted to adapt to the characteristics of different cycles and varieties;
3. You can test different types of MA, such as EMA, LWMA, etc., and select the MA form that is most responsive to price;
4. Add a machine learning algorithm to automatically optimize hyper-parameters such as MA parameters and stop loss amplitude;
5. You can test different stop loss methods, such as gap stop loss, trailing stop loss, average stop loss, etc.
Through these optimizations and improvements, the winning rate, rate of return, and risk-return rate of the strategy can be greatly improved.
## Summarize
The Double Moving Average Breakout Strategy is overall a trend following strategy that is easy to implement and optimize. It has the advantages of simple operation, flexibility and controllable risks, and is very suitable as an entry-level strategy for quantitative trading. Through continuous testing and optimization, this strategy can continue to improve and has the potential to become a quality quantitative strategy.
|| 

## Overview  

The double moving average crossover strategy is a trend-following strategy that uses the crossover of two moving averages of different periods as trading signals. It enters long or short positions when the fast MA crosses above or below the slow MA and determines trend direction after the crossover. It can capture intermediate-term trends while reducing unnecessary trading frequency from excessive fluctuations.   

## Strategy Logic

The strategy employs two moving averages: a fast MA with a shorter period (e.g. 15 periods) to capture short-term price moves, and a slow MA with a longer period (e.g. 21 periods) to identify major trend direction. Trading signals are generated from the crossover between the two MAs: the fast MA crossing above the slow MA gives buy signals, while the fast MA crossing below gives sell signals.

By tuning the MA period combinations, the strategy can adjust the timeframe of trends to capture. Shorter MA combos target short-term oscillations while longer MA combos filter out noise and focus on longer-term trends only.

The strategy also incorporates risk management modules including take profit, stop loss and trailing stop loss. These help limit the max profit/loss of individual trades and contain overall risk.

## Advantages

The double MA strategy has the following edges:

1. Simple logic and easy to understand/implement;  
2. Flexibility to adapt to market conditions by tuning MA periods;
3. Stability from fewer trade signals;
4. Effective risk control via stop losses;
5. Ease of optimization on MA, risk parameters etc.

## Risks

There are also some risks to consider:

1. Excessive crossovers and trading frequency during range-bound markets;
2. Lagging MAs may miss price reversal points and fail to stop loss in time;
3. Vulnerability to false breakouts resulting in unnecessary losses; 
4. General price tracking inaccuracy due to lag of MAs.

These weaknesses can be alleviated via optimizations like filtering signals, trailing stop loss etc.

## Enhancement Opportunities

The strategy can be enhanced in aspects like:

1. Adding filters on volume or volatility to avoid whipsaws;
2. Testing more MA types and fine-tuning periods/formulas to fit different products and timeframes; 
3. Examining MA types like EMA, LWMA for fastest price tracking;
4. Automating MA tuning and stop loss sizing with machine learning;
5. Alternate stop loss techniques e.g. gap, average price, chandelier.
 
Significant lift in win rate, risk-adjusted returns is expected from these augmentations.

## Conclusion  

Overall, the dual moving average crossover strategy offers simplicity, flexibility and controllable risks. Its ease of implementation and optimization makes it an ideal initial quant strategy. With recurrent testing and tuning, it has the credentials to evolve into a robust system over time.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_ohlc4|0|Fast MA Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_2|15|Fast MA Period|
|v_input_3_ohlc4|0|Slow MA Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_4|21|Slow MA Period|
|v_input_5|false|Invert Trade Direction?|
|v_input_6|100|Take Profit percentage(0.1%)|
|v_input_7|100|Stop Loss|
|v_input_8|false|Trailing Stop Loss|
|v_input_9|false|Trailing Stop Loss Offset|
|v_input_10|true|Use Start Time Limiter?|
|v_input_11|2018|Start From Year|
|v_input_12|5|Start From Month|
|v_input_13|true|Start From Day|
|v_input_14|false|Start From Hour|
|v_input_15|false|Start From Minute|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-10 00:00:00
end: 2023-06-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title = "Silent Trader Strategy", shorttitle = "Silent Trader", overlay = true, pyramiding = 0, default_qty_type = strategy.cash, default_qty_value = 1000, commission_value = 0.0675, initial_capital = 1000, currency = currency.USD, calc_on_order_fills = true, calc_on_every_tick = true)

maFastSource   = input(defval = ohlc4, title = "Fast MA Source")
maFastLength   = input(defval = 15, title = "Fast MA Period", minval = 1)
maSlowSource   = input(defval = ohlc4, title = "Slow MA Source")
maSlowLength   = input(defval = 21, title = "Slow MA Period", minval = 1)

tradeInvert     = input(defval = false, title = "Invert Trade Direction?")
inpTakeProfit   = input(defval = 100, title = "Take Profit percentage(0.1%)", minval = 0)
inpStopLoss     = input(defval = 100, title = "Stop Loss", minval = 0)
inpTrailStop    = input(defval = 0, title = "Trailing Stop Loss", minval = 0)
inpTrailOffset  = input(defval = 0, title = "Trailing Stop Loss Offset", minval = 0)

useTakeProfit   = inpTakeProfit  >= 1 ? inpTakeProfit  : na
useStopLoss     = inpStopLoss    >= 1 ? inpStopLoss    : na
useTrailStop    = inpTrailStop   >= 1 ? inpTrailStop   : na
useTrailOffset  = inpTrailOffset >= 1 ? inpTrailOffset : na

useTimeLimit    = input(defval = true, title = "Use Start Time Limiter?")
startYear       = input(defval = 2018, title = "Start From Year",  minval = 0, step = 1)
startMonth      = input(defval = 05, title = "Start From Month",  minval = 0,step = 1)
startDay        = input(defval = 01, title = "Start From Day",  minval = 0,step = 1)
startHour       = input(defval = 00, title = "Start From Hour",  minval = 0,step = 1)
startMinute     = input(defval = 00, title = "Start From Minute",  minval = 0,step = 1)

startTimeOk() =>
    inputTime = timestamp(syminfo.timezone, startYear, startMonth, startDay, startHour, startMinute)
    timeOk = time > inputTime ? true : false
    r = (useTimeLimit and timeOk) or not useTimeLimit

maFast = ema(maFastSource, maFastLength)
maSlow = sma(maSlowSource, maSlowLength)

fast = plot(maFast, title = "Fast MA", color = #26A69A, linewidth = 1, style = line, transp = 50)
slow = plot(maSlow, title = "Slow MA", color = #EF5350, linewidth = 1, style = line, transp = 50)

aboveBelow = maFast >= maSlow ? true : false
tradeDirection = tradeInvert ? aboveBelow ? false : true : aboveBelow ? true : false

if( startTimeOk() )
    enterLong = not tradeDirection[1] and tradeDirection
    exitLong = tradeDirection[1] and not tradeDirection
    strategy.entry( id = "Long", long = true, when = enterLong )
    //strategy.close( id = "Long", when = exitLong )
    
    enterShort = tradeDirection[1] and not tradeDirection
    exitShort = not tradeDirection[1] and tradeDirection
    strategy.entry( id = "Short", long = false, when = enterShort )
    //strategy.close( id = "Short", when = exitShort )
    
    strategy.exit("Exit Long", from_entry = "Long",  profit = close * useTakeProfit / 1000 / syminfo.mintick, loss = close * useStopLoss / 1000 / syminfo.mintick, trail_points = close * useTrailStop / 1000 / syminfo.mintick, trail_offset = close * useTrailOffset / 1000 / syminfo.mintick)
    strategy.exit("Exit Short", from_entry = "Short", profit = close * useTakeProfit / 1000 / syminfo.mintick, loss = close * useStopLoss / 1000 / syminfo.mintick, trail_points = close * useTrailStop / 1000 / syminfo.mintick, trail_offset = close * useTrailOffset / 1000 / syminfo.mintick)
```

> Detail

https://www.fmz.com/strategy/434991

> Last Modified

2023-12-11 15:21:58
