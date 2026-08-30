
> Name

Low-Volatility-Directional-Buy-with-Profit-Taking-and-Stop-Loss
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18ef8c3c3cbc7688a6e.png)
[trans]

### Overview
This strategy is called "Low Volatility Directional Buying Take Profit and Stop Loss Strategy". It uses the crossing of the moving average as a buy signal, combined with stop-profit and stop-loss to lock in profits, and is suitable for currencies in the low volatility range.
### Strategy Principles
This strategy uses 3 moving averages with different periods: 50 period, 100 period and 200 period. The buying logic is: when the 50-period line crosses the 100-period line, and the 100-period line crosses the 200-period line, enter the market long.
This signal indicates that the market is breaking out of a low volatility range and entering a trend. The rapid rise of the 50-period represents a sudden increase in short-term internal power, which begins to drive the medium and long-term upwards; the 100-period line also begins to rise, indicating that medium-term forces have joined in, stabilizing the upward trend.
After entering the market, the strategy uses stop-profit and stop-loss methods to lock in profits. The take-profit target is 8% of the entry price, and the stop-loss line is 4% of the entry price. Setting the stop profit to be greater than the stop loss will help profits exceed losses and ensure the overall profitability of the strategy.
### Advantage Analysis
This strategy has the following advantages:
1. Able to accurately seize trend opportunities brought by breakthroughs in low-volatility ranges.
2. The moving average is easy to calculate and backtest, and the logic is simple and clear.  
3. The stop-profit and stop-loss settings are reasonable, which is conducive to obtaining stable income.
4. The configurable parameters are flexible and easy to optimize.
### Risk Analysis
There are also some risks with this strategy:
1. False breakout signals may lead to losses.
2. It is difficult to stop losses when the market reverses.
3. Improper setting of stop-profit and stop-loss parameters will affect profits.
Countermeasures:
1. Combine with other indicators to filter signals to ensure the effectiveness of breakthroughs.
2. Appropriately shorten the stop loss period to reduce losses caused by reversal. 
3. Test different take-profit and stop-loss ratios to find the optimal parameters.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Test different moving average cycle parameters and find the best combination.
2. Add indicators such as trading volume to confirm trend breakthroughs. 
3. Dynamically adjust the stop-profit and stop-loss ranges.
4. Use machine learning and other methods to predict the success rate of breakthroughs.
5. Adjust parameters according to different market conditions and currencies.
In summary, the overall operation logic of this strategy is clear. Low-risk returns can be obtained by configuring the moving average cycle and stop-profit and stop-loss ranges, and can be flexibly applied to quantitative transactions. Subsequent optimization can be carried out in terms of entry signals, stop loss methods, etc., and parameters can be adjusted to find the best results.
||

### Overview  

The strategy is named "Low Volatility Directional Buy with Profit Taking and Stop Loss". It utilizes moving average crossover as buy signals and combines profit taking and stop loss to lock in profit. It is suitable for low volatility coins.  

### Strategy Logic  

The strategy uses 3 moving averages with different periods: 50-period, 100-period and 200-period. The buy logic is: when 50-period MA crosses over 100-period MA and 100-period MA crosses over 200-period MA, go long.  

This signals a breakout from low volatility range and the start of a trend. 50-period MA's fast rise represents strengthening of short term momentum; 100-period MA also turning up indicates mid term force joining in to stabilize the up trend.

After entry, the strategy uses profit taking and stop loss to lock in gains. Take profit is set at 8% of entry price. Stop loss is set at 4% of entry price. With higher take profit over stop loss, it ensures the strategy stays profitable overall.  

### Advantage Analysis

The advantages of this strategy:

1. Accurately capture trend opportunity from low volatility breakouts.  
2. Simple and clear logic with moving averages that are easy to calculate and backtest.
3. Reasonable profit taking and stop loss settings ensure stable gains. 
4. Flexible configurable parameters make optimizations easy.

### Risk Analysis  

There are also some risks:

1. Wrong breakout signals may cause losses.  
2. Hard to stop loss when markets reverse.
3. Improper profit taking and stop loss parameter settings affect profitability.

Solutions:  

1. Add other indicators to filter signals and ensure breakout validity.
2. Shorten stop loss period to reduce losses from reversals.
3. Test different profit taking and stop loss ratios to find optimum.

### Optimization Directions

Optimizations can be made in below areas:  

1. Test different moving average periods to find best combination.  
2. Add volume etc. to confirm trend breakouts.
3. Dynamically adjust profit taking and stop loss percentage.  
4. Incorporate machine learning etc. to predict breakout success rate. 
5. Adjust parameters based on different market conditions and coins.

In summary, the strategy has clear logic overall, obtains low risk profit through configuring moving average periods and profit taking/stop loss percentage. It can be flexibly applied in quantitative trading. Further optimizations can be made in areas like entry signals and stop loss methods, combined with parameter tuning to achieve best results.

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
|v_input_8|50|v_input_8|
|v_input_9|200|v_input_9|
|v_input_10|100|v_input_10|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-10 00:00:00
end: 2023-12-17 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(shorttitle='Low volatility Buy w/ TP & SL (by Coinrule)',title='Low volatility Buy w/ TP & SL', overlay=true, initial_capital = 1000, process_orders_on_close=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)

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
window()  => time >= start and time <= finish ? true : false       // create function "within window of time"

//MA inputs and calculations
movingaverage_fast = sma(close, input(50))
movingaverage_slow = sma(close, input(200))
movingaverage_normal= sma(close, input(100))



//Entry 
strategy.entry(id="long", long = true, when = movingaverage_slow > movingaverage_normal and movingaverage_fast > movingaverage_normal)

//Exit
longStopPrice  = strategy.position_avg_price * (1 - 0.04)
longTakeProfit = strategy.position_avg_price * (1 + 0.08)

strategy.close("long", when = close < longStopPrice or close > longTakeProfit and window())

//PLOT

plot(movingaverage_fast, color=color.orange, linewidth=2)
plot(movingaverage_slow, color=color.purple, linewidth=3)
plot(movingaverage_normal, color=color.blue, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/435715

> Last Modified

2023-12-18 12:00:07
