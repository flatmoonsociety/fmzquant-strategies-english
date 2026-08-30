
> Name

VWAP Trading Strategy-VWAP-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/fcf57a998c3347076c08c642fe8a84693c70bc7147441d94f2d2fe94dd7e3b00.png)
[trans]

#### Overview
This strategy is a trading strategy based on EMA, VWAP and volume. The main idea is that within a specific trading time, when the closing price breaks through VWAP and EMA, and the trading volume is greater than the trading volume of the previous K line, an opening signal is generated. At the same time, stop loss and take profit are set, as well as conditions for closing positions within a specific time period.
#### Strategy Principle
1. Calculate EMA and VWAP indicators.
2. Determine whether it is within the specified trading time.
3. Conditions for opening a long position: the closing price is greater than VWAP and EMA, the trading volume is greater than the previous K line, and the closing price is greater than the opening price.
4. Short position opening conditions: the closing price is less than VWAP and EMA, the trading volume is greater than the previous K line, and the opening price is greater than the closing price.
5. Long position closing conditions: the closing price falls below VWAP or EMA, reaches the take-profit or stop-loss point, or reaches the specified exit time.
6. Short position closing conditions: the closing price breaks through VWAP or EMA, reaches the take-profit or stop-loss point, or reaches the specified exit time.
#### Strategic Advantages
1. Taking into account the price trend (EMA), fair market value (VWAP) and trading volume at the same time, the opening conditions are more stringent, which helps to improve the winning rate of the strategy.
2. Set stop loss and take profit to control risks and lock in profits.
3. The trading time and exit time are limited to avoid the risk of holding positions during non-trading periods and overnight.
#### Strategy Risk
1. This strategy may not perform well in volatile markets because frequent breakthroughs and retracements may lead to multiple openings and closings, thereby increasing transaction costs and slippage.
2. The stop loss point is fixed and may be triggered in advance when the market fluctuates violently, causing the strategy to suffer large losses.
3. This strategy does not consider the actual market depth and commission situation, and may face problems such as slippage and position opening failure in real trading.
#### Strategy optimization direction
1. You can consider adding more filtering conditions, such as ATR, RSI and other indicators, to further confirm the strength of the trend and momentum.
2. Stop loss and take profit points can be set dynamically, such as following ATR or percentage stop loss, to adapt to different market fluctuations.
3. Parameters can be optimized, such as EMA length, VWAP source, stop loss and take profit points, etc., to improve the stability and profitability of the strategy.
4. You can consider adding position management, such as adjusting the opening amount according to volatility or capital ratio, to control the overall risk.
#### Summarize
This strategy trades within specific trading hours by taking into account price trends, fair market value and trading volume. Although stop-loss and profit-limiting and limited trading time are set, in practical applications, you still need to pay attention to risks such as market shocks and slippage. In the future, the robustness and profitability of the strategy can be improved by adding more filtering conditions, optimizing parameters, and position management.
|| 

#### Overview

This strategy is a trading strategy based on EMA, VWAP, and volume. The main idea is to generate opening signals when the closing price breaks through VWAP and EMA, and the trading volume is greater than the previous candle's volume within a specific trading time. It also sets stop loss and take profit, as well as conditions for closing positions within a specific time period.

#### Strategy Principle

1. Calculate EMA and VWAP indicators.
2. Determine whether it is within the specified trading time.
3. Long entry condition: closing price is greater than VWAP and EMA, volume is greater than the previous candle, and closing price is greater than opening price.
4. Short entry condition: closing price is less than VWAP and EMA, volume is greater than the previous candle, and opening price is greater than closing price.
5. Long exit condition: closing price falls below VWAP or EMA, reaches stop loss or take profit levels, or reaches the specified exit time.
6. Short exit condition: closing price breaks above VWAP or EMA, reaches stop loss or take profit levels, or reaches the specified exit time.

#### Strategy Advantages

1. It considers price trend (EMA), market fair value (VWAP), and trading volume simultaneously, making the opening conditions more strict, which helps to improve the strategy's win rate.
2. It sets stop loss and take profit to control risk and lock in profits.
3. It limits trading time and exit time to avoid risks during non-trading hours and overnight holding.

#### Strategy Risks

1. The strategy may not perform well in a volatile market, as frequent breakthroughs and pullbacks may lead to multiple openings and closings, increasing transaction costs and slippage.
2. The stop loss level is fixed, which may be triggered prematurely when the market fluctuates violently, causing the strategy to suffer significant losses.
3. The strategy does not consider actual market depth and order status, which may face issues such as slippage and opening failures in real trading.

#### Strategy Optimization Direction

1. Consider adding more filtering conditions, such as ATR and RSI indicators, to further confirm the strength of the trend and momentum.
2. Stop loss and take profit levels can be set dynamically, such as following ATR or percentage stop loss, to adapt to different market volatilities.
3. Optimize parameters, such as EMA length, VWAP source, stop loss and take profit levels, etc., to improve the stability and profitability of the strategy.
4. Consider adding position management, such as adjusting the opening volume according to volatility or capital ratio, to control overall risk.

#### Summary

By comprehensively considering price trends, market fair value, and trading volume, this strategy trades within a specific trading time. Although stop loss, take profit, and limited trading time are set, it still needs to pay attention to risks such as volatile markets and slippage in actual application. In the future, the strategy's robustness and profitability can be improved by adding more filtering conditions, optimizing parameters, and managing positions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|21|EMA Length|
|v_input_source_1_hlc3|0|VWAP Source: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_float_1|100|Stop Loss (points)|
|v_input_float_2|200|Target (points)|
|v_input_1|0950-1430|Only take entry during|
|v_input_2|1515-1525|Exit Trade|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-27 00:00:00
end: 2024-04-28 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA, VWAP, Volume Strategy", overlay=true, process_orders_on_close=true)

// Inputs
emaLength = input.int(21, title="EMA Length")
vwapSource = input.source(defval=hlc3, title='VWAP Source')
stopLossPoints = input.float(100, title="Stop Loss (points)")
targetPoints = input.float(200, title="Target (points)")
session = input("0950-1430", title='Only take entry during')
exit = input(defval='1515-1525', title='Exit Trade')

tradein = not na(time(timeframe.period, session))
exit_time = not na(time(timeframe.period, exit))

// Calculate indicators
ema = ta.ema(close, emaLength)
vwapValue = ta.vwap(vwapSource)

// Entry Conditions
longCondition = close > vwapValue and close > ema and volume > volume[1] and close > open and tradein
shortCondition = close < vwapValue and close < ema and volume > volume[1] and open > close and tradein

// Exit Conditions
longExitCondition = ta.crossunder(close, vwapValue) or ta.crossunder(close, ema) or close - strategy.position_avg_price >= targetPoints or close - strategy.position_avg_price <= -stopLossPoints or exit_time
shortExitCondition = ta.crossover(close, vwapValue) or ta.crossover(close, ema) or strategy.position_avg_price - close >= targetPoints or strategy.position_avg_price - close <= -stopLossPoints or exit_time

// Plotting
plot(vwapValue, color=color.blue, title="VWAP")
plot(ema, color=color.green, title="EMA")

// Strategy
if longCondition
    strategy.entry("Long", strategy.long)

if shortCondition
    strategy.entry("Short", strategy.short)

if longExitCondition
    strategy.close('Long', immediately=true)

if shortExitCondition
    strategy.close("Short", immediately=true)

```

> Detail

https://www.fmz.com/strategy/449813

> Last Modified

2024-04-29 14:20:39
