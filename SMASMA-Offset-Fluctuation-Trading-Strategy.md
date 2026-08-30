
> Name

SMA Fluctuation Offset Trading Strategy SMA-Offset-Fluctuation-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7f33f0e1d4aecaac0af05d99e7842921843b7a0fd68344dbace6de18129243bf.png)
 [trans]

## SMA Swing Offset Trading Strategy
### Strategy Overview
This strategy utilizes a simple moving average and some math to determine buy/sell points. We use the 100-day SMA as the baseline. If the closing price is below this line, we select the opening point based on the degree below this line, this value (low offset) is a configurable percentage. For closing a position, if the close is above our 100-day SMA, we determine when to sell the previous offset. If we try to sell too early (price is still rising), the trailing stop will be triggered.
### Strategy Principles
This strategy uses three SMA lines: fast line (default 14 days), slow line (default 100 days) and reference line (default 30 days).
When the closing price is lower than the reference line and the low offset relative to the slow line is greater than the configured low offset, and the fast line rises and the slow line falls, enter the long position. When these conditions are met, the fast and slow lines are very likely to cross, so it is a better entry point.
When the closing price is higher than the reference line, and the high offset relative to the slow line is greater than the configured high offset, and the closing price has risen for three consecutive K lines, profits have been realized, and when the fast line is higher than the slow line, close the long position. If the price continues to rise sharply, the trailing stop will be activated.
The position of each transaction is entered according to a certain proportion of equity, and the position is controlled in this way.
### Analysis of strategic advantages
1. Take advantage of the advantages of SMA, which is to smooth the price curve and filter out market noise.
2. SMA crossover has a certain ability to predict trends.
3. Set the offset relative to the SMA line to avoid false breakthroughs.
4. Combine trends and cross indicators to improve the accuracy of decision-making.
5. Use trailing stop loss to lock in profits and avoid retracements.
### Strategy Risk Analysis
1. SMA itself has a strong hysteresis and may miss the price turning point.
2. Improper offset setting may lead to being too aggressive or too cautious.
3. Improper setting of trailing stop loss parameters may result in premature stop loss or excessive stop loss range.
4. Unable to cope with markets with violent price fluctuations.
Corresponding optimization measures:
1. Combine with other leading indicators to filter entry.  
2. Repeated testing and optimization of the offset.
3. Repeatedly backtest the stop loss parameters to find the optimal parameters.
4. Reduce positions during periods of high volatility.
### Strategy optimization direction
1. Test SMAs of different periods to find optimal parameters
2. Add other indicators to determine market structure and trends
3. Optimize trailing stop loss parameters to lock in more profits
4. Adjust positions according to market volatility
5. Apply to multiple varieties at the same time and combine them
### Summarize
The SMA volatility offset trading strategy sets the offset to refer to different SMA moving averages to find the best entry opportunity. At the same time, the exit mechanism sets a trailing stop loss to lock in profits. The strategy is simple to understand and easy to implement. By optimizing SMA parameters, offset settings, stop loss levels, etc., you can get better results. This strategy is suitable for investors who pursue stable profits in medium and long-term cycles.
||

### Strategy Overview  

This strategy uses simple moving averages (SMA) and some math calculations to determine buy/sell points. We keep a 100-day SMA line as our basis. If the closing price is below this line, we determine the opening position based on the percentage the price is below the line (low offset), which is configurable. Similarly, we set a high offset percentage above the 100-day SMA before closing long positions. If we try to close too early while price is still rising, the trailing stop loss will be triggered.  

### Strategy Logic  

The strategy uses three SMA lines: fast line (default 14 days), slow line (default 100 days), and reference line (default 30 days).  

It goes long when closing price is below reference line, percentage below slow line (low offset) is greater than configured value, fast line is rising and slow line is falling. When this condition satisfies, fast and slow line are very likely to cross soon, so it's a good entry point.

It closes long when closing price is above reference line, percentage above slow line (high offset) is greater than configured value, closing price rose for 3 consecutive candles, we have open profits, and fast line is above slow line. If price keeps rising after closing long, trailing stop loss will be triggered.  

The order size is based on a percentage of total equity, this controls our position size.  

### Advantage Analysis  

1. Utilize the advantage of SMA being able to smooth price fluctuations and filter out market noise.  
2. SMA crossovers have some ability to predict trend changes. 
3. Setting offsets avoids false breakouts of SMA lines.  
4. Combining trend and crossover indicators improves accuracy of trading signals.
5. Trailing stop loss locks in profits and prevents drawdowns.

### Risk Analysis

1. SMA itself has lag and may miss price turning points.  
2. Improper offset setting can make strategy too aggressive or too conservative.  
3. Improper stop loss parameter may stop out too early or stop loss percentage too large.  
4. Unable to cope with violent price swings.

Corresponding improvements:
1. Add other leading indicators to filter entries.
2. Backtest and optimize offsets.  
3. Backtest and find optimal stop loss parameters.  
4. Reduce position size during high volatility periods.

### Optimization Directions  

1. Test SMAs of different periods to find optimal parameters.
2. Add other indicators to determine market structure and trend.  
3. Optimize trailing stop loss parameters to lock in more profits.
4. Adjust position sizing based on market volatility.  
5. Apply strategy to multiple products simultaneously for diversification.  

### Conclusion  

The SMA Offset Fluctuation Trading Strategy identifies optimal entry points by setting offsets based on different SMA lines. The exit mechanism sets a trailing stop loss to lock in gains. This strategy is simple to understand and implement. By optimizing parameters like SMA periods, offsets, stop loss levels, better results can be achieved. It suits medium-long term investors seeking steady profits.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|SMA Fast (days)|
|v_input_2|100|SMA Slow (days)|
|v_input_3|30|SMA Reference (days)|
|v_input_4|0.001|Low Offset (%)|
|v_input_5|0.0164|High Offset (%)|
|v_input_6|0.96|Order Stake (%)|
|v_input_7|1.35|Trailing Stoploss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-12-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// @version=4
// Author: Sonny Parlin (highschool dropout)
strategy(shorttitle="SMA+Strategy", title="SMA Offset Strategy",
                                      overlay=true,  currency=currency.USD,
                                      initial_capital=10000)

// Inputs and variables
ss = input(14, minval=10, maxval=50, title="SMA Fast (days)")
ff = input(100, minval=55, maxval=200, title="SMA Slow (days)")
ref = input(30, minval=20, maxval=50, title="SMA Reference (days)")
lowOffset = input(0.001, "Low Offset (%)", minval=0, step=0.001)
highOffset = input(0.0164, "High Offset (%)", minval=0, step=0.0001)
orderStake = input(0.96, "Order Stake (%)", minval=0, step=0.01)

// SMA
smaFast = sma(close, ss)
smaSlow = sma(close, ff)
smaRef = sma(close, ref)
distanceLow = (close - smaSlow) / close
distanceHigh = (close - smaSlow) / close

// Set up SMA plot but don't show by default
plot(smaFast, "smaFast", color=#00ff00, display = 0)
plot(smaSlow, "smaSlow", color=#ff0000, display = 0)
plot(smaRef, "smaRef", color=#ffffff, display = 0)

// The buy stratey:
// guard that the low is under our sma low reference line by our lowOffset %, 
// default is 0.001. (low < smaRef) and (distanceLow > lowOffset)
// SMA fast is on the rise and SMA slow is falling and they are very likely
// to cross. (rising(smaFast,1)) and (falling(smaSlow, 1)) 
enterLong = (low < smaRef) and (distanceLow > lowOffset) and (rising(smaFast,1)) and (falling(smaSlow, 1)) 

// The sell Strategy:
// Guard that close is higher than our sma high reference line by our 
// highOffset %, default is 0.0164. (close > smaRef) and (distanceHigh > highOffset)
// Guard that close has risen by 3 candles in a row (rising(close,3)) 
// Guard that we currently have profit (strategy.openprofit > 0)
// Guard that SMA fast is higher than smaSlow (smaFast > smaSlow)
// If it keeps going up past our close position the trailing stoploss will kick in!
enterShort = (close > smaRef) and (distanceHigh > highOffset) and (rising(close,3)) and (strategy.openprofit > 0) and (smaFast > smaSlow)

// Order size is based on total equity
// Example 1:
// startingEquity = 2000
// close = 47434.93
// orderStake = 0.45
// (2,000 × orderStake) / close = orderSize = 0.0189733599 = approx $900

// Example 2:
// startingEquity = 2000
// close = 1.272
// orderStake = 0.45
// (startingEquity × orderStake) / close = orderSize = 707.5471698113 = approx $900
orderSize = (strategy.equity * orderStake) / close

// Trailing Stoploss
// I'm using 1.35 as my default value, play with this for different results.
longTrailPerc = input(title="Trailing Stoploss (%)",
     type=input.float, minval=0.0, step=0.1, defval=1.35) * 0.01
     
longStopPrice = 0.0

longStopPrice := if (strategy.position_size > 0)
    stopValue = close * (1 - longTrailPerc)
    max(stopValue, longStopPrice[1])
else
    0

if (enterLong)
    strategy.entry("Open Long Position", strategy.long, orderSize, when=strategy.position_size <= 0)
    
if (enterShort)
    strategy.exit(id="Close Long Position", stop=longStopPrice)


//plot(strategy.equity)
```

> Detail

https://www.fmz.com/strategy/435831

> Last Modified

2023-12-19 10:52:10
