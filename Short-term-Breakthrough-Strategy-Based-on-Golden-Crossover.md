
> Name

Short-term-Breakthrough-Strategy-Based-on-Golden-Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/722c472864b9dbf1dd446acabc9aaef67b23c532a7505d62efcb12385bacae0c.png)
[trans]

## Overview
This strategy is a short-term tracking strategy based on moving averages. It uses the golden cross of the long-term and short-term moving averages as a buy signal and the dead cross as a sell signal, and combines it with the RSI indicator to filter out false signals. This is a typical short-term trading strategy, suitable for high-frequency day trading.
## Strategy Principle
This strategy uses a 200-period long-term simple moving average malong and a 21-period short-term exponential moving average mashort. A buy signal is generated when the price crosses above the long-term moving average and the RSI indicator is less than 20; a sell signal is generated when the price crosses below the short-term moving average and the RSI indicator is greater than 80. In order to filter out false signals, it also sets additional conditions: long positions will be closed only when the price is lower than the short-term moving average and higher than the lowest price of the previous K line; short positions will be closed only when the price is higher than the short-term moving average and lower than the highest price of the previous K line.
This strategy has both a 1% stop loss and a 1% take profit. That is, the stop-loss price for long positions is 99% of the purchase price, and the take-profit price is 101% of the purchase price; the opposite is true for short positions, which ensures that each transaction has strict risk control.
## Strategic Advantages
The biggest advantage of this strategy is its short-term tracking nature. The moving average gold/die cross combination has proven to be an effective technical indicator for identifying short-term trend reversals. Combined with RSI extreme value filtering, short-term reversal opportunities can be effectively identified and positions adjusted in a timely manner. This high-frequency trading strategy can fully capture short-term price fluctuations and achieve profitability.
Another advantage is that this strategy has a strict stop loss mechanism. Regardless of whether you are long or short, the stop loss point is set to less than 1% of the buying/selling price, which can quickly stop the loss and prevent the loss from expanding. The take profit is similarly set to 1% to ensure that the profit is taken promptly after making a profit.
## Strategy Risk
The biggest risk with this strategy is the tendency to overtrade. When the price fluctuates near the moving average, the opening and closing of positions will be triggered frequently, which is not conducive to the control of position costs and handling fees. At this time, it is necessary to appropriately relax the indicator parameters and reduce unnecessary transactions.
Another risk is that moving averages tend to give off false signals. When prices fluctuate wildly, the actual trend has not changed, but the moving average may be sending false signals. At this time, you need to rely on RSI extreme value filtering to avoid chasing tops and withdrawing bottoms. RSI parameters can be tested and optimized to make filtering more stringent.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Add other indicator filters, such as KD, MACD, etc., and combine more indicators to judge the actual market trend to avoid false signals.
2. Optimize the moving average parameters and test the impact of different period parameters on the strategy effect.
3. Optimize the stop-loss and take-profit parameters and appropriately expand the stop-loss range to reduce the probability of the stop-loss being triggered.
4. Add trading time filtering and only open positions during active trading hours to avoid overnight risks.
5. Add intraday cycle and short position filtering logic to reduce the frequency of unnecessary transactions and reduce expenses.
## Summarize
This strategy is generally a typical short-term tracking strategy. It uses the golden/die cross combination of the moving average to determine the short-term trend, and supplements it with the RSI indicator to filter out false signals. The strategy has the advantage of high-frequency intraday trading and can fully capture short-term price fluctuations. But there is also a certain risk of false signals and over-trading risks. Through parameter optimization and adding other indicators, the strategy can be further improved and the strategy's ability to make stable profits can be improved.
||

## Overview

This is a short-term tracking strategy based on moving averages. It uses the golden crossover of long-term and short-term moving averages as buy signals, and the death cross as sell signals. Combined with the RSI indicator to filter false signals, this is a typical short-term trading strategy suitable for high-frequency intraday trading.

## Strategy Logic

The strategy uses a 200-period simple moving average malong as the long-term line and a 21-period exponential moving average mashort as the short-term line. It generates buy signals when the price crosses above the long-term line and the RSI is below 20. Sell signals are generated when the price crosses below the short-term line and the RSI exceeds 80. To filter false signals, additional criteria are set: long positions are closed only when the price is below the short-term line and above the lowest price of the previous bar; short positions are closed only when the price is above the short-term line and below the highest price of the previous bar. 

The strategy also sets a 1% stop loss and 1% take profit. That is, the stop loss for long positions is set at 99% of the entry price, and take profit is at 101% of the entry price. For short positions it is the opposite. This ensures strict risk control for every trade.

## Advantages

The biggest advantage of this strategy lies in its short-term tracking capability. The golden/death cross combinations of moving averages are proven effective technical indicators for identifying short-term trend changes. Combined with RSI extreme value filtering, they can effectively detect short-term reversal opportunities and promptly adjust positions. Such high frequency strategies can fully capture short-term price fluctuations and realize profits.

Another advantage is the strict stop loss mechanism set in the strategy. Whether long or short, the stop loss is set at 1% below the entry/exit price, which allows quick stop loss to prevent loss enlargement. Similarly take profit is set at 1% to lock in gains in a timely manner after profiting. 

## Risks

The biggest risk of this strategy is that it may result in excessive trading. When the price oscillates near the moving averages, it tends to frequently trigger openings and closings, which is not conducive to controlling carry costs and transaction fees. In this case, appropriate relaxation of indicator parameters is needed to reduce unnecessary trading.

Another risk lies in the false signals of the moving averages. When prices experience sharp fluctuations, the actual trend may not change, but the moving average can still give wrong signals. This is when RSI extreme value filtering needs to be relied on to avoid chasing tops and bottoms. The RSI parameters can be tested and optimized to make the filtering more strict.

## Optimization Directions 

The following aspects of the strategy can be further optimized:

1. Add other indicators for filtering, such as KD, MACD etc, to determine the actual market trend based on multiple indicators, avoiding false signals.  

2. Optimize moving average parameters by testing different cycle parameters for performance impact.

3. Optimize stop loss and take profit parameters to appropriately expand stop loss range to reduce the probability of being stopped out.  

4. Add trading session filters to take positions only during active trading hours to minimize overnight risks.

5. Add intraday cycle and empty warehouse filters to reduce unnecessary trading frequency and expense costs.

## Conclusion

In summary, this is a typical short-term tracking strategy. It utilizes the golden/death cross combinations of moving averages to determine short-term trends, supplemented by RSI indicators to filter false signals. The strategy has the advantage of high frequency intraday trading that can fully capture short-term price fluctuations. But it also has certain risks of false signals and excessive trading. Further improvements can be made through parameter optimization and integrating more indicators to enhance the steady profitability of the strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|200|(?Parameters)Long Term SMA Period|
|v_input_int_2|21|Short Term SMA Period|
|v_input_int_3|true|Take Profit Percentage|
|v_input_1|timestamp(01 Jan 2000 13:30 +0000)|(?Period)Start Trade Day|
|v_input_2|timestamp(1 Jan 2099 19:30 +0000)|End Trade Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-27 00:00:00
end: 2024-02-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("simple pull back", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// Input values
malongperiod = input.int(200, "Long Term SMA Period", group="Parameters")
mashortperiod = input.int(21, "Short Term SMA Period", group="Parameters")
stoprate = 1  // Set the stop loss percentage to 1%
profit = input.int(1, "Take Profit Percentage", group="Parameters") // Change the take profit percentage to 1%
startday = input(title="Start Trade Day", defval=timestamp("01 Jan 2000 13:30 +0000"), group="Period")
endday = input(title="End Trade Day", defval=timestamp("1 Jan 2099 19:30 +0000"), group="Period")

// Plotting indicators
malong = ta.sma(close, malongperiod)
mashort = ta.ema(close, mashortperiod)

plot(malong, color=color.aqua, linewidth=2)
plot(mashort, color=color.yellow, linewidth=2)

// Date range
datefilter = true

// Long entry condition
if close > malong and close < mashort and strategy.position_size == 0 and datefilter and ta.rsi(close, 3) < 20
    strategy.entry("Long", strategy.long)

// Short entry condition
if close < malong and close > mashort and strategy.position_size == 0 and datefilter and ta.rsi(close, 3) > 80
    strategy.entry("Short", strategy.short)

// Exit conditions with 1% stop loss and 1% take profit
strategy.exit("Cut", "Long", stop=(1 - 0.01 * stoprate) * strategy.position_avg_price, limit=(1 + 0.01 * profit) * strategy.position_avg_price)

if close > mashort and close < low[1] and strategy.position_size > 0
    strategy.close("Long")
if close < mashort and close > high[1] and strategy.position_size < 0
    strategy.close("Short")
```

> Detail

https://www.fmz.com/strategy/442973

> Last Modified

2024-02-27 17:46:55
