
> Name

Dynamic-Stop-Loss-and-Take-Profit-Strategy-Based-on-VWAP-and-Cross-Timeframe-Signals
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/5b2f3596920a843d5d387d8c00a7482fd3f62c496763a7ea6a199ee870273313.png)
[trans]
## Overview
This strategy uses the daily VWAP (Volume Weighted Average Price) as entry and exit signals. When the closing price crosses VWAP, a long position is triggered, and the stop loss is set at the low point of the previous K line below VWAP, and the target price is set 3 points above the opening price; when the closing price crosses below VWAP, a short position is triggered, the stop loss is set at the high point of the previous K line above VWAP, and the target price is set 3 points below the opening price. This strategy does not include exit conditions and the trade will be held until a reversal signal occurs.
## Strategy Principle
1. Obtain daily VWAP data as a basis for trend judgment and trading signals.
2. Determine whether the current closing price crosses above/under VWAP, as trigger conditions for long and short positions respectively.
3. When going long, if the low point of the previous K line is below VWAP, use it as the stop loss level, otherwise use VWAP directly as the stop loss; when going short, the opposite is true.
4. After opening a position, set a fixed 3-point take-profit level.
5. The strategy continues to run until a reverse signal is triggered to close the position and open a new position.
By judging the trend through cross-cycle VWAP data, and using dynamic stop loss and fixed point take profit, you can effectively grasp the trend market, control the risk of retracement, and lock in profits in a timely manner.
## Advantage Analysis
1. Simple and effective: The strategy logic is clear. Trend judgment and signal triggering can be achieved by using only one indicator, VWAP. It is simple and easy to implement and optimize.
2. Dynamic stop loss: Setting stop loss based on the high and low points of the previous K line can better adapt to market fluctuations and reduce risks.
3. Fixed point profit stop: Setting the target price with a fixed point helps to lock in profits in a timely manner and avoid profit taking.
4. Timely stop loss and take profit: The strategy will immediately close the position when a reverse signal is triggered, without causing additional losses to existing profits. At the same time, it will open a new position to capture the new trend market.
## Risk Analysis
1. Parameter optimization: The strategy uses a fixed 3 points as a take-profit. In actual transactions, it may be necessary to optimize and select the best parameters based on different targets and market characteristics.
2. Volatile market conditions: Under volatile market conditions, frequent entries and exits may lead to higher transaction costs and affect returns.
3. Trend persistence: The strategy depends on the trend market. If the market is in range oscillation, or the trend sustainability is poor, more trading signals may appear, bringing more risks.
## Optimization direction
1. Trend filtering: Add other trend indicators such as moving averages, MACD, etc. to confirm the trend twice and improve signal reliability.
2. Dynamic take-profit: Dynamically adjust the take-profit points based on market volatility, ATR and other indicators to better adapt to the market.
3. Position management: Dynamically adjust the position size of each transaction based on account funds, risk preference and other factors.
4. Trading period selection: Select the best trading period based on the characteristics of the target and the level of trading activity to improve strategy efficiency.
## Summarize
This strategy uses cross-cycle VWAP data for trend judgment and signal triggering. It also uses dynamic stop loss and fixed point take-profit to control risks and lock in profits. It is a simple and effective quantitative trading strategy. Through optimization of trend filtering, dynamic take-profit, position management, and trading period selection, the robustness and profit potential of the strategy can be further improved. However, in practical applications, it is still necessary to pay attention to factors such as market characteristics, transaction costs, and parameter optimization in order to obtain better strategic performance.
|| 

## Overview

This strategy uses the VWAP (Volume Weighted Average Price) from the daily timeframe as a signal for entering and exiting trades. When the close price crosses above the VWAP, it triggers a long entry with the stop loss set at the previous candle's low if it's below the VWAP, and the target price set 3 points above the entry price. Conversely, when the close price crosses below the VWAP, it triggers a short entry with the stop loss set at the previous candle's high if it's above the VWAP, and the target price set 3 points below the entry price. This strategy doesn't include an exit condition, so trades remain open until the opposing signal occurs.

## Strategy Principle

1. Obtain the VWAP data from the daily timeframe, which serves as the basis for trend determination and trading signals.
2. Determine whether the current close price crosses above/below the VWAP, acting as the trigger for long and short entries, respectively.
3. For long entries, if the previous candle's low is below the VWAP, it is used as the stop loss; otherwise, the VWAP itself is used. The opposite applies for short entries.
4. After entering a position, set a fixed 3-point take profit level.
5. The strategy continues to run until a reverse signal triggers the position to close and open a new one.

By using cross-timeframe VWAP data to determine trends and leveraging dynamic stop losses and fixed-point take profits, the strategy can effectively capture trending markets, control drawdown risks, and timely lock in profits.

## Advantage Analysis

1. Simplicity and effectiveness: The strategy logic is clear, using only the VWAP indicator for trend determination and signal triggering, making it simple to implement and optimize.
2. Dynamic stop loss: By setting the stop loss based on the previous candle's high or low, the strategy adapts better to market fluctuations and reduces risk.
3. Fixed-point take profit: Setting the target price with a fixed number of points helps to lock in profits promptly and avoid profit erosion.
4. Timely stop loss and take profit: The strategy immediately closes the position when a reverse signal is triggered, preventing additional losses on existing profits. It also opens a new position to capture new trending moves.

## Risk Analysis

1. Parameter optimization: The strategy uses a fixed 3 points for take profit, which may require optimization based on different instruments and market characteristics to select the optimal parameters for actual trading.
2. Choppy markets: In choppy market conditions, frequent entries and exits may lead to higher trading costs, affecting profitability.
3. Trend sustainability: The strategy relies on trending markets. If the market is range-bound or lacks trend sustainability, there may be more trading signals generated, introducing more risk.

## Optimization Directions

1. Trend filtering: Incorporate other trend indicators like moving averages, MACD, etc., to confirm trends and improve signal reliability.
2. Dynamic take profit: Adjust the take profit points dynamically based on market volatility, ATR, or other indicators to better adapt to market conditions.
3. Position sizing: Dynamically adjust the position size for each trade based on account size, risk tolerance, and other factors.
4. Trading session selection: Choose the optimal trading sessions based on the characteristics and liquidity of the instrument to improve strategy efficiency.

## Summary

This strategy utilizes cross-timeframe VWAP data for trend determination and signal triggering while employing dynamic stop losses and fixed-point take profits to control risks and lock in profits. It is a simple and effective quantitative trading strategy. Through optimizations in trend filtering, dynamic take profit, position sizing, and trading session selection, the strategy's robustness and profit potential can be further enhanced. However, when applying the strategy in practice, attention should be paid to market characteristics, trading costs, and parameter optimization to achieve better strategy performance.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-06 00:00:00
end: 2024-03-07 00:00:00
period: 45m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('Pine Script Tutorial Example Strategy 1', overlay=true, initial_capital=1000, default_qty_value=100, default_qty_type=strategy.percent_of_equity)
// fastEMA = ta.ema(close, 24)
// slowEMA = ta.ema(close, 200)
// Higher Time Frame
float sl = na
float tgt = na
posSize = 1
vwap_1d = request.security(syminfo.tickerid, "1D", ta.vwap(close))
// plot(vwap_1d)

// To avoid differences on historical and realtime bars, you can use this technique, which only returns a value from the higher timeframe on the bar after it completes:
// indexHighTF = barstate.isrealtime ? 1 : 0
// indexCurrTF = barstate.isrealtime ? 0 : 1
// nonRepaintingVWAP = request.security(syminfo.tickerid, "1D", close[indexHighTF])[indexCurrTF]
// plot(nonRepaintingVWAP, "Non-repainting VWAP")

enterLong = ta.crossover(close, vwap_1d)
exitLong  = ta.crossunder(close, vwap_1d)

enterShort = ta.crossunder(close, vwap_1d)
exitShort  = ta.crossover(close, vwap_1d)

if enterLong
    sl := low[1]>vwap_1d ?low[1]:vwap_1d
    tgt:=close+3
    strategy.entry("EL", strategy.long, qty=posSize)
    strategy.exit('exitEL', 'EL', stop=sl, limit=tgt)
if enterShort
    sl := high[1]<vwap_1d ?high[1]:vwap_1d
    tgt := close-3
    strategy.entry("ES", strategy.short, qty=posSize)
    strategy.exit('exitES', 'ES', stop=sl, limit=tgt)

// if exitLong
//     strategy.close("EL")
// if exitShort
//     strategy.close("ES")





// goLongCondition1 = ta.crossover(close, vwap_1d)
// timePeriod = time >= timestamp(syminfo.timezone, 2021, 01, 01, 0, 0)
// notInTrade = strategy.position_size <= 0
// if goLongCondition1 and timePeriod and notInTrade
//     stopLoss = low[1]
//     takeProfit = close+3
//     strategy.entry('long', strategy.long)
//     strategy.exit('exit', 'long', stop=stopLoss, limit=takeProfit)
plot(close, color=color.new(#00c510, 0))
plot(vwap_1d, color=color.new(#f05619, 0))
plot(sl, color=color.new(#fbff00, 0))
plot(tgt, color=color.new(#00e1ff, 0))
```

> Detail

https://www.fmz.com/strategy/444041

> Last Modified

2024-03-08 17:37:21
