
> Name

Renko reversal tracking strategy Renko-Reversal-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

### Strategy Overview
The Renko reversal tracking strategy is a short-term strategy that uses Renko graphics to determine market reversals. It captures short-term reversal opportunities by monitoring changes in adjacent Renko colors. A trading signal is generated when the next Renko changes color after consecutive Renkos of the same color.
### Strategy Principles
1. Use traditional unfixed Renko.
2. Monitor the color changes of two adjacent Renkos.
3. When the color of the previous Renko and the previous two Renko are the same, and the color of the current Renko is reversed, a signal is generated.
4. Long signal: a positive brick appears after two negative bricks, which is bullish;
5. Short selling signal: A negative brick appears after two positive bricks, which is bearish.
6. The entry method can be market order or stop loss order.
7. Set the take-profit and stop-loss points to be a certain multiple of the Renko size.
The core of this strategy is to seize the short-term callback opportunity caused by the Renko color reversal. Continuous Renko of the same color represents the formation of a trend, and the next Renko color change indicates a possible reversal.
Renko size and take-profit and stop-loss coefficients can be adjusted to optimize strategy effects.
### Strategic Advantages
- Renko displays reversal information directly
- The rules are simple and clear, easy to operate
- Symmetry of long and short opportunities
- Flexible adjustment of Renko size
- Take profit and stop loss to strictly control risks
### Risk warning
- A certain number of consecutive Renkos are required to form a signal
- Renko size directly affects returns and drawdowns
- Unable to determine trend duration
- Continuous stop losses may occur
### Summarize
The Renko reversal tracking strategy innovatively uses traditional technical indicators to determine short-term reversal opportunities through direct Renko color changes. This strategy is simple and practical, and can obtain stable returns through parameter adjustment. It is worthy of backtest verification and real-time optimization before application.

||

### Strategy Overview

The Renko reversal tracking strategy is a short-term trading strategy that uses Renko bricks to identify market reversals. It captures short-term reversal opportunities by monitoring color changes between adjacent bricks. Trading signals are generated when the current brick color flips after consecutive same-colored bricks.

### Strategy Logic

1. Use traditional non-repainting Renko bricks. 

2. Monitor color changes between neighboring bricks.

3. Signals emerge when current brick color flips while previous two bricks share the same color.

4. Long signal: Bullish brick appears after two bearish bricks.

5. Short signal: Bearish brick appears after two bullish bricks.

6. Entry options: market order or stop order.

7. Set stop loss/take profit at brick size multiplied by a coefficient. 

The core is capitalizing on pullback opportunities caused by brick color flips. Consecutive same-colored bricks represent trend formation, and next brick flipping color indicates potential reversals.

Brick size and stop loss/take profit coefficients can be tuned for optimization.

### Advantages of the Strategy

- Bricks directly display reversal information 

- Simple and clear logic, easy to implement

- Symmetrical long and short opportunities 

- Flexible brick size adjustment

- Strict risk control with stop loss/take profit

### Risk Warnings

- Requires a certain number of consecutive bricks to form signals

- Brick size directly impacts profit/drawdown

- Hard to determine trend duration

- Consecutive stop loss may occur

### Conclusion

The Renko reversal tracking strategy innovatively applies traditional technical indicators by directly using brick color flips to identify short-term reversals. Simple and practical, this strategy can achieve steady returns through parameter tuning, and is worth backtesting, live optimization, and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Brick size multiplier: use high value to avoid SL and TP|
|v_input_2|true|Use stop orders instead of market orders|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-07 00:00:00
end: 2023-09-08 18:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Simple Renko strategy, very profitable. Thanks to vacalo69 for the idea.
//Rules when the strategy opens order at market as follows:
//- Buy when previous brick (-1) was bearish and previous brick (-2) was bearish too and actual brick close is bullish
//- Sell when previous brick (-1) was bullish and previous brick (-2) was bullish too and actual brick close is bearish
//Rules when the strategy send stop order are the same but this time a stop buy or stop sell is placed (better overall results).
//Note that strategy open an order only after that condition is met, at the beginning of next candle, so the actual close is not the actual price.
//Only input is the brick size multiplier for stop loss and take profit: SL and TP are placed at (brick size)x(multiplier) Or put it very high if you want startegy to close order on opposite signal.
//Adjust brick size considering: 
//- Strategy works well if there are three or more consecutive bricks of same "color"
//- Expected Profit
//- Drawdown
//- Time on trade
//
//Study with alerts, MT4 expert advisor and jforex automatic strategy are available at request.
//

strategy("Renko Strategy Open_Close", overlay=true, calc_on_every_tick=true, pyramiding=0,default_qty_type=strategy.percent_of_equity,default_qty_value=100,currency=currency.USD)

//INPUTS
Multiplier=input(1,minval=0, title='Brick size multiplier: use high value to avoid SL and TP')
UseStopOrders=input(true,title='Use stop orders instead of market orders')

//CALCULATIONS
BrickSize=abs(open[1]-close[1])
targetProfit = 0
targetSL = 0

//STRATEGY CONDITIONS
longCondition = open[1]>close[1] and close>open and open[1]<open[2]
shortCondition = open[1]<close[1] and close<open and open[1]>open[2]

//STRATEGY
if (longCondition and not UseStopOrders)
    strategy.entry("LongBrick", strategy.long)
    targetProfit=close+BrickSize*Multiplier
    targetSL=close-BrickSize
    strategy.exit("CloseLong","LongBrick", limit=targetProfit, stop=targetSL)
    
if (shortCondition and not UseStopOrders)
    strategy.entry("ShortBrick", strategy.short)
    targetProfit = close-BrickSize*Multiplier
    targetSL = close+BrickSize
    strategy.exit("CloseShort","ShortBrick", limit=targetProfit, stop=targetSL)

if (longCondition and UseStopOrders)
    strategy.entry("LongBrick_Stop", strategy.long, stop=open[2])
    targetProfit=close+BrickSize*Multiplier
    targetSL=close-BrickSize
    strategy.exit("CloseLong","LongBrick_Stop", limit=targetProfit, stop=targetSL)
    
if (shortCondition and UseStopOrders)
    strategy.entry("ShortBrick_Stop", strategy.short, stop=open[2])
    targetProfit = close-BrickSize*Multiplier
    targetSL = close+BrickSize
    strategy.exit("CloseShort","ShortBrick_Stop", limit=targetProfit, stop=targetSL)
```

> Detail

https://www.fmz.com/strategy/426927

> Last Modified

2023-09-15 16:28:21
