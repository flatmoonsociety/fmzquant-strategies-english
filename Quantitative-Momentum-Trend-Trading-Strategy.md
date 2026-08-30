
> Name

Quantitative-Momentum-Trend-Trading-Strategy based on trend momentum
> Author

ChaoZhang

> Strategy Description


[trans]  

This article will introduce in detail a quantitative trading strategy based on trend momentum judgment. This strategy comprehensively uses moving averages, MACD, RSI and other indicators to judge price momentum to capture medium and long-term trend opportunities.
1. Strategy Principle
The main judgment indicators of this strategy include:
1. EMA moving average to determine the price trend in different periods;
2. MACD, to determine whether short-term momentum has changed;
3. RSI, determine whether it is overbought or oversold;
4. ATR, calculate stop loss and take profit positions.
It combines these indicators to judge that when the price has a sustained and powerful breakthrough, it determines that the trend has started and forms a trading signal.
When the short-term EMA has multiple reversals, it is judged to be consolidation, and the market will only enter the market when it breaks through the long-term EMA.
MACDImplement momentum change determines strength, and RSI avoids chasing tops and bottoms. ATR sets stop loss and take profit to control single risk.
2. Strategic advantages
The biggest advantage of this strategy is that the indicators are complementary and can effectively determine the start of the mid- to long-term trend.
Another advantage is the stop-loss and take-profit settings, which can lock in trend profits and control risks.
Finally, the EMA cycle is layered and can enter trends of different strengths.
3. Potential risks
But this strategy also has the following risks:
First of all, there may be a lag in trend judgment and there is a possibility of missed orders.
Secondly, if the stop loss is too aggressive, there is a risk of being trapped.
Finally, retracement pressure requires mental preparation.
4. Content summary
This article details a quantitative strategy based on trend momentum judgment. It comprehensively uses moving averages, MACD, RSI and other indicators to determine the trend direction. Through parameter optimization, risks can be controlled and stable returns can be obtained. But we also need to be wary of problems such as lagging indicators.
||

This article explains in detail a quantitative trading strategy based on momentum trend analysis. It synthesizes indicators like moving averages, MACD, and RSI to identify price momentum and capture mid-long term trend opportunities.

I. Strategy Logic

The main judgment indicators include:

1. EMAs to gauge trends across different periods. 

2. MACD to detect short-term momentum changes.

3. RSI to check overbought/oversold levels. 

4. ATR for stop loss and take profit calculation.

It combines these indicators to identify persistent, strong breakouts that signal the start of a trend for trade entry. 

When the short-term EMA fluctuates frequently, it judges the market as ranging. Trades are only taken when the long-term EMA is broken.

MACD judges momentum strength, RSI avoids chasing tops and bottoms. ATR sets stop loss and take profit controlling risk per trade.

II. Advantages of the Strategy

The biggest advantage is the complementarity of indicators, which can effectively identify the start of mid-long term trends.

Another advantage is the stop loss and take profit, which locks in trend profits and manages risk.

Lastly, the staged EMA periods allow smooth trend entries at different momentum levels.

III. Potential Risks 

However, the strategy also has the following risks:

Firstly, trend detection may lag, causing missed opportunities.

Secondly, stops set too tightly risk being stopped out prematurely.  

Finally, drawdown pressure needs psychological preparation.

IV. Summary

In summary, this article has explained a quantitative strategy based on momentum trend analysis. It synthesizes indicators like moving averages, MACD and RSI to determine trend direction. With proper parameter tuning, it can control risks and achieve steady profits. But risks like indicator lag need to be watched out for.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|ATR Stop Period|
|v_input_2|D|ATR Resolution|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-08-30 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("QuantCat Mom Finder Strateg (1H)", overlay=true)

//Series to sum the amount of crosses in EMA for sideways trend/noise filtering
//can change EMA lengths, can change to SMA's/WMA's e.t.c

lookback_value = 60
minMA = 20
midMA = 40
maxMA = 60

ema25_crossover = (crossover(close, ema(close, minMA))) == true ? 1 : 0
ema25_crossover_sum = sum(ema25_crossover, lookback_value) ///potentially change lookback value to alter results

ema50_crossover = (crossover(close, ema(close, midMA))) == true ? 1 : 0
ema50_crossover_sum = sum(ema50_crossover, lookback_value) ///potentially change lookback value to alter results

ema75_crossover = (crossover(close, ema(close, maxMA))) == true ? 1 : 0
ema75_crossover_sum = sum(ema75_crossover, lookback_value) ///potentially change lookback value to alter results

ema25_crossunder = (crossunder(close, ema(close, minMA))) == true ? 1 : 0
ema25_crossunder_sum = sum(ema25_crossunder, lookback_value) ///potentially change lookback value to alter results

ema50_crossunder = (crossunder(close, ema(close, midMA))) == true ? 1 : 0
ema50_crossunder_sum = sum(ema50_crossunder, lookback_value) ///potentially change lookback value to alter results

ema75_crossunder = (crossunder(close, ema(close, maxMA))) == true ? 1 : 0
ema75_crossunder_sum = sum(ema75_crossunder, lookback_value) ///potentially change lookback value to alter results4


//Boolean series declaration
//can change amount of times crossed over the EMA verification to stop sideways trend filtering (3)

maxNoCross=2

macdmidlinebull=-0.5
macdmidlinebear=0.5
[macdLine, signalLine, histLine] = macd(close, 12, 26, 9)

//---------------
//Series Creation

bullishMacd = (macdLine > signalLine) and (macdLine > macdmidlinebull) ? true : false

bearishMacd = (macdLine < signalLine) and (macdLine < macdmidlinebear) ? true : false

bullRsiMin = 50 //53 initial values
bullRsiMax = 60 //61
bearRsiMin = 40 //39
bearRsiMax = 50 //47

basicBullCross25bool = ((ema25_crossover_sum < ema50_crossover_sum) 
     and (ema25_crossover_sum < ema75_crossover_sum) 
     and (ema25_crossover_sum < maxNoCross) 
     and crossover(close, ema(close, minMA)) and (rsi(close, 14) > bullRsiMin)
     and (rsi(close, 14) < bullRsiMax) and (bullishMacd == true)) ? true : false
  
basicBullCross50bool = ((ema50_crossover_sum < ema25_crossover_sum) 
     and (ema50_crossover_sum < ema75_crossover_sum) 
     and (ema50_crossover_sum < maxNoCross) 
     and crossover(close, ema(close, midMA)) and (rsi(close, 14) > bullRsiMin)
     and (basicBullCross25bool == false) 
     and (rsi(close, 14) < bullRsiMax) and (bullishMacd == true)) ? true : false
  
basicBullCross75bool = ((ema75_crossover_sum < ema25_crossover_sum) 
     and (ema75_crossover_sum < ema50_crossover_sum) 
     and (ema75_crossover_sum < maxNoCross) 
     and crossover(close, ema(close, maxMA)) and (rsi(close, 14) > bullRsiMin)
     and (basicBullCross25bool == false) and (basicBullCross50bool == false)
     and (rsi(close, 14) < bullRsiMax) and (bullishMacd == true)) ? true : false
     
basicBearCross25bool = ((ema25_crossunder_sum < ema50_crossunder_sum) 
     and (ema25_crossunder_sum < ema75_crossunder_sum) 
     and (ema25_crossunder_sum < maxNoCross) 
     and crossunder(close, ema(close, minMA)) and (rsi(close, 14) <bearRsiMax)
     and (rsi(close, 14) > bearRsiMin) and (bearishMacd == true)) ? true : false
  
basicBearCross50bool = ((ema50_crossunder_sum < ema25_crossunder_sum) 
     and (ema50_crossunder_sum < ema75_crossover_sum) 
     and (ema50_crossunder_sum < maxNoCross) 
     and crossunder(close, ema(close, midMA)) and (rsi(close, 14) < bearRsiMax)
     and (basicBearCross25bool == false) 
     and (rsi(close, 14) > bearRsiMin) and (bearishMacd == true)) ? true : false
  
basicBearCross75bool = ((ema75_crossunder_sum < ema25_crossunder_sum) 
     and (ema75_crossunder_sum < ema50_crossunder_sum) 
     and (ema75_crossunder_sum < maxNoCross) 
     and crossunder(close, ema(close, maxMA)) and (rsi(close, 14) < bearRsiMax)
     and (basicBearCross25bool == false) and (basicBearCross50bool == false)
     and (rsi(close, 14) > bearRsiMin) and (bearishMacd == true)) ? true : false

//STRATEGY
//can change lookback input on ATR

atrLkb = input(14, minval=1, title='ATR Stop Period')
atrRes = input("D",  title='ATR Resolution')
atr = security(syminfo.tickerid, atrRes, atr(atrLkb))


longCondition = (basicBullCross25bool or basicBullCross50bool or basicBullCross75bool) == true
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = (basicBearCross25bool or basicBearCross50bool or basicBearCross75bool) == true
if (shortCondition)
    strategy.entry("Short", strategy.short)
    
   
// Calc ATR Stops
// can change atr multiplier to affect stop distance/tp distance, and change "close" to ema values- could try ema 50

stopMult = 0.6 //0.6 is optimal

longStop = na
longStop :=  shortCondition ? na : longCondition and strategy.position_size <=0 ? close - (atr * stopMult) : longStop[1] 
shortStop = na
shortStop := longCondition ? na : shortCondition and strategy.position_size >=0 ? close + (atr * stopMult) : shortStop[1]

//Calc ATR Target

targetMult = 2.2 //2.2 is optimal for crypto x/btc pairs

longTarget = na
longTarget :=  shortCondition ? na : longCondition and strategy.position_size <=0 ? close + (atr*targetMult) : longTarget[1]
shortTarget = na
shortTarget := longCondition ? na : shortCondition and strategy.position_size >=0 ? close - (atr*targetMult) : shortTarget[1]

// Place the exits

strategy.exit("Long ATR Stop", "Long", stop=longStop, limit=longTarget)
strategy.exit("Short ATR Stop", "Short", stop=shortStop, limit=shortTarget)

//Bar color series

longColour = longCondition ? lime : na
shortColour = shortCondition ? red : na
    
// Plot the stoplosses and targets

plot(longStop, style=linebr, color=red, linewidth=2,     title='Long ATR Stop')
plot(shortStop, style=linebr, color=red, linewidth=2,  title='Short ATR Stop')
plot(longTarget, style=linebr, linewidth=2, color=lime,  title='Long ATR Target')
plot(shortTarget, linewidth=2, style=linebr, color=lime,  title='Long ATR Target')

barcolor(color=longColour)
barcolor(color=shortColour)

alertcondition(((basicBullCross25bool or basicBullCross50bool or basicBullCross75bool)==true), title='Long Entry', message='Bullish Momentum Change!')
alertcondition(((basicBearCross25bool or basicBearCross50bool or basicBearCross75bool)==true), title='Short Entry', message='Bearish Momentum Change!')
```

> Detail

https://www.fmz.com/strategy/426854

> Last Modified

2023-09-14 20:38:49
