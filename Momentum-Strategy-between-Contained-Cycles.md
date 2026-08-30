
> Name

Momentum-Strategy-between-Contained-Cycles Momentum-Strategy-between-Contained-Cycles
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
The core idea of ​​this strategy is to use the K-line pattern "included between cycles" to determine the trend direction and use it as an entry signal. When an inter-cycle pattern appears that includes the previous K-line, we can infer that the current trend is a transition point. At this time, we can choose to go long when it breaks through the previous high point, or go short when it breaks through the previous low point, and set stop loss and take profit.
### Strategy Principles
1. Determine whether there is a K-line pattern contained between cycles. The specific judgment logic is: the high point of the current K line is lower than the high point of the previous K line, and the low point of the current K line is higher than the low point of the previous K line.
2. Determine the rise and fall of the previous K-line. If the closing price is higher than the opening price, it is an increase; if the closing price is lower than the opening price, it is a decrease.
3. If the previous K-line is an uptrend and a pattern contained between cycles appears, we set a buy stop order within 10% of the previous K-line high point.
4. If the previous K-line is in a downtrend and there is a pattern contained between cycles, we set a sell stop order within 10% of the low of the previous K-line.
5. Once the stop order is triggered to form a position, we will set up a stop loss order and a take profit order. The specific stop loss distance and take profit distance are both a certain proportion of the amplitude of the previous K line.
6. If the pattern contained between cycles appears again, we will give priority to closing the position and then reset the new pending order.
### Analysis of strategic advantages
The advantages of this strategy are:
1. Use the internal logic of K-line to accurately grasp the timing of entry. The patterns contained between cycles often mean that a trend reversal or acceleration is about to occur, which provides us with a better entry opportunity.
2. The policy rules are clear and easy to understand and easy to operate.
3. Use the high and low points of the previous period to set stop-loss and take-profit positions to control risks.
4. Every time a matching pattern reappears, a new pending order will be reset, allowing you to follow the new trend.
### Strategy Risk Analysis
There are also some risks with this strategy:
1. The patterns contained between cycles may not necessarily lead to trend reversal or acceleration, and there is a certain risk of false signals.
2. The stop loss distance may be set too small and cannot withstand large fluctuations in the market.
3. The take-profit distance may be set too large, preventing timely profits.
4. This strategy relies more on trending market conditions and has limited profit potential in consolidation market conditions.
5. The number of transactions may be too frequent and the transaction costs will be high.
Countermeasures:
1. It can be combined with other indicators to filter the confirmation signals contained in the form between cycles to reduce the false signal rate.
2. The stop loss distance can be appropriately relaxed, but it should not exceed 50% of the previous K-line amplitude.
3. The take-profit distance can be shortened to about 50% of the previous K-line amplitude.
4. Optimize fund management, reduce single positions, and cope with market consolidation.
5. Relax entry conditions appropriately and reduce the number of transactions.
### Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Use trend indicators to determine the trend direction and avoid frequent trading during consolidation. For example, adding MACD to determine the trend will only consider entering the market when MACD is in the same direction.
2. Optimize the stop-loss and take-profit strategy, and use methods such as trailing stop-loss or profit-protecting stop-loss to make the stop-loss more flexible.
3. Test different stop-loss and take-profit ratio settings to find the optimal parameter combination.
4. Add a re-entry mechanism to capture the trend again after exiting with stop loss.
5. Optimize position management and adjust individual positions according to market fluctuations.
6. Optimize fund management, such as fixed fund utilization, etc.
7. Test the effectiveness of the strategy on different varieties and time periods.
### Summarize
To sum up, this is a strategy that uses the patterns contained in the cycles to determine the turning point of the trend and set pending orders to capture the reversal trend. It has the advantages of clear entry timing, simple strategy rules, and controllable risks, but there is also a certain risk of false signals and room for optimization. We can further improve the stability and profitability of the strategy by combining trend indicators, optimizing stop loss and profit, and adjusting positions. This strategy is more suitable for trending market conditions. In specific applications, it needs to be optimized and tested according to the characteristics of different markets to maximize its effectiveness.
|| 

### Overview

The core idea of this strategy is to determine the trend direction using the "contained between cycles" candlestick pattern and use it as the entry signal. When a contained between cycles pattern appears that contains the previous candlestick, we can infer that this is a point where the trend is reversing, at which point we can go long on a breakout above the previous high or go short on a breakout below the previous low, with proper stop loss and take profit setup.

### Strategy Logic

1. Check if the contained between cycles pattern occurs. The specific logic is: the current candle's high is lower than the previous candle's high, and the current candle's low is higher than the previous candle's low.

2. Determine if the previous candle was bullish or bearish. If the close was higher than the open, it was bullish. If the close was lower than the open, it was bearish.

3. If the previous candle was bullish and the contained pattern occurs, place a buy stop order at the previous candle's high plus 10% of its range. 

4. If the previous candle was bearish and the contained pattern occurs, place a sell stop order at the previous candle's low minus 10% of its range.

5. Once the stop order is triggered and position is opened, set the stop loss and take profit. The stop loss and take profit distances are a certain percentage of the previous candle's range.

6. If another inside bar pattern forms, close existing positions first and then place new pending orders.

### Advantage Analysis

The advantages of this strategy include:

1. It utilizes the inherent logic of candlesticks and provides an accurate entry timing. The contained pattern often implies upcoming trend reversal or acceleration.

2. The rules are simple and easy to follow for actual trading.

3. The stop loss and take profit based on previous candle's range helps control risk.

4. New pending orders are placed each time a qualified pattern appears, allowing us to follow the new trend.

### Risk Analysis

There are also some risks:

1. The contained pattern does not always result in trend reversal or acceleration. There are some false signals.

2. The stop loss distance may be too small to withstand large fluctuations in the market.

3. The take profit target may be too wide, preventing timely profits.

4. The strategy relies more on trending markets. The profit potential is limited during consolidation.

5. The high trading frequency leads to large transaction costs.

Solutions:

1. Add other indicators to confirm the signals and reduce false signals.

2. Widen the stop loss slightly but not more than 50% of the previous candle's range.

3. Shorten the take profit target to around 50% of the previous candle's range.

4. Optimize capital management, reduce individual position size for ranging markets.

5. Loosen the entry criteria to reduce trading frequency.

### Optimization Directions

Some ways to optimize the strategy:

1. Add a trend indicator like MACD to determine trend direction, avoiding whipsaws during consolidation.

2. Use more advanced stop loss techniques like trailing stop or profit protection stop loss.

3. Test different stop loss and take profit ratios to find the optimal parameters.

4. Add re-entry logic to capture the trend again after stop loss.

5. Optimize the position sizing based on market volatility. 

6. Optimize capital management, such as fixed fractional position sizing.

7. Test the strategy on different products and timeframes.

### Conclusion

In summary, this is a strategy that uses the contained between cycles pattern to determine trend turning points and place pending orders to capture trend reversals. It has the advantages of clear entry signals, simple rules, and controllable risks, but also has some false signal risks and room for optimization. We can further improve its stability and profitability by combining trend filters, optimizing stops, adjusting position sizes etc. It is more suitable for trending markets, and needs to be optimized and tested for different market conditions before actual usage to maximize its effectiveness.

[/trans]


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2018|From Year|
|v_input_2|true|From Month|
|v_input_3|true|From Day|
|v_input_4|9999|To Year|
|v_input_5|true|To Month|
|v_input_6|true|To Day|
|v_input_7|10|Stop Buy Order Percentage From Previous Candle's Range|
|v_input_8|20|Stop Loss Distance from High/Low of Previous Candle|
|v_input_9|80|Take Profit Distance from High/Low of Previous Candle|
|v_input_10|2|Percentage Of EQUITY to risk per trade|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-03-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

// Inside Bar Momentum Strategy
// As defined on Babypips.com
// https://www.babypips.com/trading/forex-inside-bar-20170113

// strategy("Babypips: Inside Bar Momentum Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=5)

From_Year  = input(defval = 2018, title = "From Year")
From_Month = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
From_Day   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
To_Year    = input(defval = 9999, title = "To Year")
To_Month   = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
To_Day     = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
Start  = timestamp(From_Year, From_Month, From_Day, 00, 00)  // backtest start window
Finish = timestamp(To_Year, To_Month, To_Day, 23, 59)        // backtest finish window
Window = true

Stop_Buy_Perc  = input(10, "Stop Buy Order Percentage From Previous Candle's Range")/100
Stop_Loss_Perc = input(20, "Stop Loss Distance from High/Low of Previous Candle")/100
Take_Prof_Perc = input(80, "Take Profit Distance from High/Low of Previous Candle")/100

Risk = input(2, "Percentage Of EQUITY to risk per trade", step=0.1, minval=0, maxval=100)/100

Inside_Bar = high[1] > high[0] and low[1] < low[0]
Prev_Range = high[1] - low[1]
Bullish = open[1] < close[1]
Bearish = open[1] > close[1]

// Get Key Levels 
Long_Stop_Buy_Level   = high[1] + (Prev_Range * Stop_Buy_Perc)
Short_Stop_Buy_Level  = low[1]  - (Prev_Range * Stop_Buy_Perc)
Long_Stop_Loss_Level  = high[1] - (Prev_Range * Stop_Loss_Perc)
Short_Stop_Loss_Level = low[1]  + (Prev_Range * Stop_Loss_Perc)
Long_Take_Prof_Level  = high[1] + (Prev_Range * Take_Prof_Perc)
Short_Take_Prof_Level = low[1]  - (Prev_Range * Take_Prof_Perc)

// Position Sizing
long_qty = floor((strategy.equity * Risk) / (Long_Stop_Buy_Level - Long_Stop_Loss_Level))
short_qty = floor((strategy.equity * Risk) / (Short_Stop_Loss_Level - Short_Stop_Buy_Level))

// -------------------------- LONG CONDITIONS --------------------------------//
// The first candlestick must be bullish (green or white) and if the second 
// candlestick is completely contained by the first, set a buy stop order at 
// the first candle’s high plus 10% of its range (high minus low).

// Place the stop loss at the first candle’s high minus 20% of its range 
// and set the target at the first candle’s high plus 80% of its range

// If another inside bar pattern forms, the current position should be closed 
// or the pending buy/sell order must be canceled and entry orders must be 
// updated to the latest candles.

Long_Condition = Window and Inside_Bar and Bullish
if (Long_Condition)
    // Incase we still have a buy stop order in the market
    strategy.cancel_all()
    // Close any existing positions according to the rules
    strategy.close_all()
    strategy.entry("Bullish IB", strategy.long, stop=Long_Stop_Buy_Level)
    strategy.exit("Bullish Exit","Bullish IB", stop=Long_Stop_Loss_Level, limit=Long_Take_Prof_Level)
    
// -------------------------- SHORT CONDITIONS -------------------------------//
// The first candlestick must be bearish (red or black) and if the second 
// candlestick is completely contained by the first, set a sell stop order at 
// the first candle’s low minus 10% of its range (high minus low).

// Place the stop loss at the first candle’s low plus 20% of its range and 
// set the target at the first candle’s low minus 80% of its range.

// If another inside bar pattern forms, the current position should be closed 
// or the pending buy/sell order must be canceled and entry orders must be 
// updated to the latest candles.

Short_Condition = Window and Inside_Bar and Bearish
if (Short_Condition)
    // Incase we still have a buy stop order in the market
    strategy.cancel_all()
    // Close any existing positions according to the rules
    strategy.close_all()
    strategy.entry("Bearish IB", strategy.short, stop=Short_Stop_Buy_Level)
    strategy.exit("Bearish Exit","Bearish IB", stop=Short_Stop_Loss_Level, limit=Short_Take_Prof_Level)
    
// ----------------------------- PLOTTING ------------------------------------//
plotshape(Inside_Bar, style=shape.arrowdown, location=location.abovebar, color=purple)

```

> Detail

https://www.fmz.com/strategy/427378

> Last Modified

2023-09-20 14:59:37
