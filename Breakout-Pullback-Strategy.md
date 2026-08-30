
> Name

A trend-following breakout-Pullback-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/181c883399e6520b891.png)
[trans]

## Overview
The Breakout Retracement Strategy is a trend following strategy. Its basic principle is to go long and short when it breaks through the highest price or lowest price of the previous K line. After setting the stop profit and stop loss, let the profit continue to run.
## Strategy Principle
This strategy mainly determines the Entry timing by judging whether the price breaks through the highest price or lowest price of the previous K line. The specific logic is:
If the highest price of the current K-line is higher than the highest price of the previous K-line, a long signal is issued.
If the lowest price of the current K line is lower than the lowest price of the previous K line, a short signal is issued.
Enter the market immediately after receiving a long or short signal. After entering the market, set the take profit to 50 points and the stop loss to 100 points.
Actively exit when the loss is greater than or equal to the stop loss points or the profit is greater than or equal to the take profit points.
## Advantage Analysis
This breakout callback strategy has the following advantages:
1. The operation logic is simple and easy to implement.
2. You can effectively seize the beginning of the trend and enter the market in time. 
3. After setting a stop-profit and stop-loss, profits can continue to run and avoid leaving the market prematurely.
4. Strong retracement and risk control capabilities.
## Risk Analysis
There are also some risks with this strategy:
1. The breakthrough signal may be a false breakthrough, leading to mistaken entry.
2. When the market consolidates, it is easy to get trapped.
3. It is necessary to set reasonable stop-profit and stop-loss points to control risks.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Increase the validity judgment of price breakthroughs and avoid false breakthroughs. For example, indicator filtering and volume verification can be added.
2. Add a trend judgment mechanism to avoid the risk of hold-up caused by market consolidation. Trend indicators such as moving averages can be added.
3. Optimize the stop-profit and stop-loss strategies, such as trailing stop-loss, moving stop-loss after profit, etc., to maximize profits.
4. Optimize parameters and find the best take-profit and stop-loss points.
## Summarize
In general, this breakthrough callback strategy has simple logic and is easy to implement. It can effectively capture the beginning of the trend and has strong retracement and risk control capabilities. With further optimization it can become a very practical quantitative strategy.
||

## Overview  

The breakout pullback strategy is a trend following strategy. Its basic principle is to go long or short when the price breaks through the high or low of the previous candlestick and let the profit continue to run after setting the take profit and stop loss.  

## Strategy Logic   

The core logic of this strategy is to determine the entry timing by judging whether the price breaks through the high or low of the previous candlestick. The specific logic is:  

If the high of the current candlestick is higher than the high of the previous candlestick, a long signal is triggered.  

If the low of the current candlestick is lower than the low of the previous candlestick, a short signal is triggered.

Once receiving the long or short signal, enter the position immediately. After entering the position, set the take profit to 50 pips and stop loss to 100 pips.  

When the loss is greater than or equal to the stop loss pips or profit is greater than or equal to the take profit pips, exit the position actively.

## Advantage Analysis   

This breakout pullback strategy has the following advantages:  

1. The logic is simple and easy to implement.  
2. It can effectively capture the beginning of trends and enter positions in a timely manner.
3. Setting take profit and stop loss allows profits to continue to run, avoiding premature exits.  
4. Good ability of controlling drawdowns and risks.

## Risk Analysis   

This strategy also has some risks:   

1. Breakout signals may be false breakouts, causing wrong entries.
2. It is easy to be trapped in range-bound consolidate markets.   
3. Reasonable take profit and stop loss pips should be set to control risks.  

## Optimization Directions  

The strategy can be further optimized in the following aspects:  

1. Add validity check for price breakouts to avoid false breakouts, such as using indicators filters and volume confirmation.  

2. Add trend determination mechanism to avoid trapping risks in range-bound markets. Moving average and other trend indicators can be used.
  
3. Optimize take profit and stop loss strategy, such as trailing stop loss, moving stop loss after profit, etc, to maximize profits.
  
4. Parameter optimization to find the optimal take profit and stop loss pips.

## Conclusion  

In general, this breakout pullback strategy has the advantage of simple logic, easy implementation, and effectively capturing trend starts. It also has good ability of controlling risks and drawdowns. With further optimizations, it can become a very practical quant strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Take Profit (in pips)|
|v_input_2|100|Stop Loss (in pips)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-25 00:00:00
end: 2024-01-31 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Breakout Strategy", shorttitle="BS", overlay=true)

// Input for take profit and stop loss in pips
tp_pips = input(50, title="Take Profit (in pips)")
sl_pips = input(100, title="Stop Loss (in pips)")

// Calculate take profit and stop loss levels in points
tp_level = tp_pips * syminfo.mintick
sl_level = sl_pips * syminfo.mintick

// Function to check if a breakout has occurred
breakout(high_or_low) =>
    high_or_low > request.security(syminfo.tickerid, "D", high[1]) ? true : false

// Buy condition
buy_condition = breakout(high)
strategy.entry("Buy", strategy.long, when=buy_condition)

// Sell condition
sell_condition = breakout(low)
strategy.entry("Sell", strategy.short, when=sell_condition)

// Take profit and stop loss conditions for Buy
tp_buy_condition = strategy.position_avg_price + tp_level
sl_buy_condition = strategy.position_avg_price - sl_level
strategy.exit("Take Profit/Close Buy", from_entry="Buy", profit=tp_buy_condition, loss=sl_buy_condition)

// Take profit and stop loss conditions for Sell
tp_sell_condition = strategy.position_avg_price - tp_level
sl_sell_condition = strategy.position_avg_price + sl_level
strategy.exit("Take Profit/Close Sell", from_entry="Sell", profit=tp_sell_condition, loss=sl_sell_condition)

```

> Detail

https://www.fmz.com/strategy/440715

> Last Modified

2024-02-01 14:37:02
