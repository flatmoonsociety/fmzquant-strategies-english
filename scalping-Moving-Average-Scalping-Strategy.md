
> Name

Moving average short-term-scalping-strategy Moving-Average-Scalping-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy belongs to the short-term scalping strategy type. Its goal is to frequently open and close positions, achieve stable returns through small profits and control downside risks. The strategy uses moving average indicators to determine possible reversal points and enter long positions, and sets quick profit-taking targets to lock in small profits.
## Strategy Principle
This strategy uses 4 moving averages, namely 9-period, 50-period, 100-period and 200-period moving averages.
The specific trading rules are:
- Enter long when the 9-period moving average crosses the 50-period moving average
- The 50-period MA is below the 100-period MA
- The 100-period MA is below the 200-period MA
This kind of combination judgment can find the time when the price is falling in the short term but may reverse and go long.
The closing rule is to close long positions when the 9-period moving average crosses the 200-period moving average. A relatively recent take-profit target is set here to achieve stable income through frequent small profits.
## Strategic Advantages
- Frequently open and close positions to effectively control single losses
- Use moving averages to determine reversal points and find potential buying points
- Set a profit stop point closer to lock in a small amount of guaranteed profit
- Reduce the holding time and reduce the impact of the general trend
- High capital utilization rate, suitable for small capital growth
## Strategy Risk
- The moving average judgment lags behind and the best entry point may be missed.
- Small profit margin and easily affected by transaction fees
- Many invalid transactions, frequent transactions cause time and energy costs
- The take-profit point is too conservative and fails to fully follow the trend
- Difficulty making profits in a consolidating market
Risks can be reduced by:
- Optimize moving average parameters to improve the accuracy of buying point judgments
- Appropriately relax the profit limit EXIT to pursue more trend profits
- Add other technical indicators for confirmation to reduce invalid transactions
- Optimize capital utilization and position management
- consider usch
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the combination of moving average parameters
Test more moving average cycle parameters to find a combination that more accurately determines reversal.
2. Relax the profit stop point
Appropriately relax the take-profit distance and pursue more trend profits.
3. Add other technical indicators
For example, KDJ, MACD, etc., to confirm and reduce invalid transactions.
4. Optimize warehouse management
The set position size is dynamically adjusted according to the specific take-profit and stop-loss points.
5. Add re-entry mechanism
After exiting with a profit stop, if the trend continues, you can consider re-entering through conditions.
## Summarize
This strategy belongs to the short-term scalping strategy type. It forms trading signals by judging short-term reversal moving average combinations, and sets a closer take profit to make frequent profits. This can effectively control single losses and risks, and is suitable for the growth of small capital amounts. However, there are problems such as small profit margin and frequent transactions. We can improve it through parameter optimization, profit-taking adjustment, and indicator filtering. On the basis of maintaining its advantages, we can further expand the profit space and make the strategy more stable and efficient. At the same time, we should pay attention to continuous learning of other more diversified strategic ideas.
|| 

## Overview 

This strategy belongs to the scalping strategy type, aiming to open and close positions frequently to profit from small gains while limiting downside risks. It identifies potential reversal points with moving averages to go long, and sets tight take profit targets to lock in small profits.

## Strategy Logic

The strategy uses 4 moving averages - 9, 50, 100, and 200 periods. 

The specific trading rules are:

- Go long when 9 MA crosses above 50 MA
- 50 MA is below 100 MA 
- 100 MA is below 200 MA

This combination identifies situations when price is in short-term downtrend but a reversal may occur.

Exit rule is when 9 MA crosses above 200 MA. A near profit target is used to lock in frequent small gains for steady profits.

## Advantages

- Frequent opening and closing controls single loss
- MA crossover catches potential bottoms  
- Near profit target locks in small certain wins
- Reduced holding time minimizes trend influence
- High capital utilization suitable for small accounts

## Risks

- MA lag may miss best entry points
- Small profit range vulnerable to fees
- More invalid trades increase time and energy costs
- Excessively conservative TP fails to ride trends  
- Hard to profit in range-bound markets

Risks can be reduced by:

- Optimizing MA parameters for better signal accuracy
- Relaxing TP to capture more trend profits 
- Adding other indicators for confirmation, reducing invalid trades
- Optimizing capital utilization and position sizing
- Considering re-entries

## Optimization Directions

The strategy can be improved by:

1. Optimizing MA combinations

   Testing more MA periods for better reversal detection.

2. Widening take profit levels

   Allow wider TP distance for more trend profits.

3. Adding other indicators 

   Such as KDJ, MACD for confirmation to reduce invalid trades.

4. Position sizing optimization

   Dynamically size positions based on specific TP and SL.

5. Adding re-entry rules

   Consider re-entering after TP if trend continues.

## Summary

This scalping strategy identifies potential short-term reversals with MA combinations for frequent small profits. This effectively controls single loss and risks, making it suitable for small accounts growth. However limitations exist like small profit range and excessive trades. Improvements can be made via parameter tuning, TP adjusting, adding filters etc, to expand profits while retaining its strengths, making the strategy more robust and efficient. Also continuously learning other more advanced strategies is important.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|10|From Day|
|v_input_3|2019|From Year|
|v_input_4|true|Thru Month|
|v_input_5|true|Thru Day|
|v_input_6|2112|Thru Year|
|v_input_7|true|Show Date Range|
|v_input_8|9|v_input_8|
|v_input_9|50|v_input_9|
|v_input_10|200|v_input_10|
|v_input_11|100|v_input_11|
|v_input_12|2|v_input_12|
|v_input_13|8|v_input_13|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//strategy(shorttitle='Moving Average Scalper (by Coinrule)',title='Moving Average Scalper', overlay=true, initial_capital = 1000, default_qty_type = strategy.percent_of_equity, default_qty_type = strategy.percent_of_equity, default_qty_value = 30, commission_type=strategy.commission.percent, commission_value=0.1)

//Backtest dates
fromMonth = input(defval = 1,    title = "From Month",      type = input.integer, minval = 1, maxval = 12)
fromDay   = input(defval = 10,    title = "From Day",        type = input.integer, minval = 1, maxval = 31)
fromYear  = input(defval = 2019, title = "From Year",       type = input.integer, minval = 1970)
thruMonth = input(defval = 1,    title = "Thru Month",      type = input.integer, minval = 1, maxval = 12)
thruDay   = input(defval = 1,    title = "Thru Day",        type = input.integer, minval = 1, maxval = 31)
thruYear  = input(defval = 2112, title = "Thru Year",       type = input.integer, minval = 1970)

showDate  = input(defval = true, title = "Show Date Range", type = input.bool)

start     = timestamp(fromYear, fromMonth, fromDay, 00, 00)        // backtest start window
finish    = timestamp(thruYear, thruMonth, thruDay, 23, 59)        // backtest finish window
window()  => true       // create function "within window of time"

//MA inputs and calculations
movingaverage_signal = sma(close, input(9))
movingaverage_fast = sma(close, input(50))
movingaverage_slow = sma(close, input(200))
movingaverage_mid= sma(close, input(100))

//Entry 
bullish = crossover(movingaverage_signal, movingaverage_fast)

strategy.entry(id="long", long = true, when = bullish and movingaverage_fast < movingaverage_mid and movingaverage_mid < movingaverage_slow and window())

//Exit

bearish = crossover(movingaverage_signal, movingaverage_slow)


Stop_loss= ((input (2))/100)
Take_profit= ((input (8))/100)

longStopPrice  = strategy.position_avg_price * (1 - Stop_loss)
longTakeProfit = strategy.position_avg_price * (1 + Take_profit)

strategy.close("long", when = bearish)

// close < longStopPrice or close > longTakeProfit and window())

//PLOT
plot(movingaverage_signal, color=color.black, linewidth=2 )
plot(movingaverage_fast, color=color.orange, linewidth=2)
plot(movingaverage_slow, color=color.purple, linewidth=2)
plot(movingaverage_mid, color=color.blue, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/427508

> Last Modified

2023-09-21 20:41:15
