
> Name

Chaotic-Trading-Rules-Stop-Loss-Strategy Chaotic-Trading-Rules-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13ca5d7387e5e85916f.png)
[trans]

## Overview
The core idea of ​​this strategy is to add some key transaction management rules on the basis of the RSI strategy, including stop loss, take profit, trailing stop, and leverage trailing stop. This allows the strategy to obtain higher returns in trending markets during the backtest period while minimizing losses in volatile markets.
## Strategy Principle
This strategy first calculates the RSI indicator, going long when the RSI is below the overbought line, and going short when the RSI is above the oversold line.
After the long signal is triggered, the highest price at that moment is recorded as the reference point for trailing stop loss. If the price is lower than the trailing stop point minus the stop loss width, the position will be closed with a stop loss.
After the short signal is triggered, the lowest price at that moment is recorded as the reference point for trailing stop loss. If the price is higher than the trailing stop loss point plus the stop loss width, the position will be closed with a stop loss.
Set fixed take-profit and stop-loss distances at the same time. If the price reaches the stop-profit distance, the position will be cleared with profit; if the price reaches the stop-loss distance, the position will be cleared with stop-loss.
In addition, set the leverage trailing stop line according to the leverage. If the price touches the leverage trailing stop loss line, the position will be cleared and the stop loss will be cleared.
By tracking the highest price stop loss when the trend is upward, tracking the lowest price stop loss when the trend is downward, combined with fixed take profit and stop loss distance, you can obtain higher profits in the trending market. At the same time, setting a leverage trailing stop can avoid the expansion of losses as much as possible.
## Advantage Analysis
The biggest advantage of this strategy is that it introduces multiple transaction management rules, which can better control risks while giving full play to the advantages of the RSI strategy.
Specifically, the advantages of the strategy are:
1. In the trending market, trailing stop loss can continue to follow the trend and make profits, thereby obtaining higher profits.
2. Fixed stop-profit and stop-loss distances can lock in part of the profit and prevent all profits from being locked up when the trend reverses.
3. Leverage trailing stop loss can try to avoid loss expansion and control risks.
4. The combination of multiple stop loss methods can give full play to their respective advantages in different market environments and improve the overall stability of the strategy.
5. Strategy parameters can be flexibly adjusted to adapt to different trading varieties and market environments.
6. The strategy logic is clear and easy to understand, making it easy to verify, optimize and apply.
## Risk Analysis
The main risks of this strategy come from:
1. The RSI strategy itself has a certain risk of wrong trading, and stop loss may be triggered. It can be optimized by adjusting the RSI parameter.
2. Oscillating near the stop loss point may frequently trigger the stop loss. This can be avoided by appropriately expanding the stop loss distance.
3. The take-profit distance cannot completely lock in the profits in the trending market. It can be combined with other indicators to determine when the trend ends.
4. The fixed stop loss distance may be too small to completely avoid losses. Consider using oscillatory stop loss or dynamic stop loss.
5. Excessive leverage may cause the leverage trailing stop to be too close to the opening price. Leverage settings should be appropriately lowered.
6. The backtesting time range cannot fully represent future market conditions. Risk control should be done well and the effects in different time periods should be verified.
The above risks can be mitigated through parameter adjustment, optimization of stop loss mechanisms, risk control, etc. However, no strategy can completely avoid market risks, and risk control needs to be done.
## Optimization direction
This strategy can be further optimized from the following directions:
1. Optimize RSI parameters to reduce the probability of wrong transactions. Optimal parameter combinations for different markets can be tested.
2. Try other indicators to determine the timing of entry, such as KD, MACD, etc., combined with RSI to form multiple filters.
3. Use machine learning and other methods to dynamically optimize stop-loss and take-profit parameters.
4. Try more complex stop loss methods, such as oscillating stop loss, average stop loss, dynamic stop loss, etc.
5. Optimize the setting of leverage levels and the impact of different leverages on returns and risk control.
6. Automatically adjust parameters according to changes in market environment, such as α-Dual Thrust.
7. Combine with other factors to judge the continuity of the trend, such as trading volume, energy, etc.
8. Use technologies such as deep learning to develop more stable and explainable stop loss methods.
9. Test data of different varieties and time periods to evaluate the robustness of the strategy.
## Summarize
This strategy adds a variety of stop loss methods based on the RSI strategy, giving full play to the dual role of stop loss in trend profit and risk control. There is still a lot of room for strategy optimization, and strategies can be improved and risks reduced from many aspects. The idea of ​​stop-loss strategy is highly universal and can be extended to more strategies and trading varieties. It is a direction worth studying. Through continuous optimization and verification, stop loss strategies can become an extremely important part of the mechanical trading system.
|| 

## Overview

The core idea of this strategy is to add some key trading management rules on the basis of RSI strategy, including stop loss, take profit, trailing stop loss, and leverage tracking stop loss. This allows the strategy to achieve higher returns during trending markets and minimize losses during ranging markets in backtest. 

## Strategy Logic

The strategy first calculates the RSI indicator. It goes long when RSI is below the oversold level and goes short when RSI is above the overbought level.

After a long signal is triggered, the highest price at that time is recorded as the trailing stop loss reference point. If the price falls below the stop loss point minus the stop loss range, the position is closed by stop loss.

After a short signal is triggered, the lowest price at that time is recorded as the trailing stop loss reference point. If the price rises above the stop loss point plus the stop loss range, the position is closed by stop loss.

At the same time, fixed take profit and stop loss distances are set. If the price reaches the take profit distance, take profit to close position. If it reaches the stop loss distance, close position by stop loss.

In addition, a leverage tracking stop loss line is set based on the leverage. If the price hits the leverage tracking stop loss line, the position is closed by stop loss.

By trailing the highest price during uptrends and the lowest price during downtrends, combined with fixed take profit and stop loss distances, higher returns can be achieved in trending markets. Meanwhile, leverage tracking stop loss helps avoid expanding losses.

## Advantage Analysis

The biggest advantage of this strategy is the introduction of multiple trading management rules that better control risks while leveraging the strengths of RSI strategy.

Specifically, the advantages are:

1. Trailing stop loss can continuously follow the trend to gain higher profit during trending markets.

2. Fixed take profit and stop loss lock in some profits and avoid full profits being wiped out when trend reverses.

3. Leverage tracking stop loss helps avoid expanding losses and controls risk.

4. The combination of various stop loss methods can exert their strengths in different market environments, improving overall stability of the strategy.

5. Flexible adjustment of strategy parameters fits different trading instruments and market environments. 

6. Easy to understand logic facilitates verification, optimization and application.

## Risk Analysis

The main risks of this strategy come from:

1. RSI strategy itself has some whipsaw risks, which may trigger stop loss. RSI parameters can be optimized.

2. Oscillation around stop loss points may frequently trigger stop loss. Stop loss range can be widened.

3. Take profit distance cannot fully lock in profits during trending markets. Other indicators can help determine trend ending.

4. Fixed stop loss distance may be too small to fully avoid losses. Consider using oscillating stop loss or dynamic stop loss.

5. Excessive leverage leads to stop loss being too close to entry price. Lower leverage setting should be used.

6. Backtest period may not fully represent future market conditions. Proper risk control should be implemented and different periods tested.

The above risks can be mitigated through parameter tuning, optimizing stop loss mechanisms, risk control etc. But no strategy can completely avoid market risks. Proper risk control is a must.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Optimize RSI parameters to reduce whipsaw trades, and test optimum parameters for different markets.

2. Try other indicators like KD, MACD combined with RSI to filter entries. 

3. Use machine learning to dynamically optimize stop loss and take profit parameters.

4. Test more complex stop loss mechanisms like oscillating stop loss, average stop loss, dynamic stop loss etc.

5. Optimize leverage setting and study impacts on profit and risk control.

6. Auto adjust parameters based on market regime changes, like α-Dual Thrust.

7. Incorporate other factors to determine trend persistence, e.g. volume energy.

8. Use deep learning models to develop more robust and interpretable stop loss ways.

9. Test data from different instruments and time periods to evaluate strategy robustness.

## Conclusion

This strategy complements RSI strategy with various stop loss methods, giving full play to the dual effects of stop loss in profiting from trends and controlling risks. There is still large room for optimization. The ideas can be extended to more strategies and trading instruments. Stop loss strategies are worth in-depth research and can become a very important part of mechanical trading systems after continuous optimization and verification.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2011|Backtest Start Year|
|v_input_2|8|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2016|Backtest Stop Year|
|v_input_5|9|Backtest Stop Month|
|v_input_6|29|Backtest Stop Day|
|v_input_7|true|Color Background?|
|v_input_8|14|length|
|v_input_9|30|overSold|
|v_input_10|70|overBought|
|v_input_11|99999|Trailing Stop|
|v_input_12|99999|Take Profit|
|v_input_13|99999|Stop Loss|
|v_input_14|200|Leverage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-06 00:00:00
end: 2023-11-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Adding some essential components to a prebuilt RSI strategy", overlay=true)

/////////////// Component Code Start ///////////////
testStartYear = input(2011, "Backtest Start Year") 
testStartMonth = input(8, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

testStopYear = input(2016, "Backtest Stop Year")
testStopMonth = input(9, "Backtest Stop Month")
testStopDay = input(29, "Backtest Stop Day")
// testStopDay = testStartDay + 1
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,0,0)

// A switch to control background coloring of the test period
testPeriodBackground = input(title="Color Background?", type=bool, defval=true)
testPeriodBackgroundColor = testPeriodBackground and (time >= testPeriodStart) and (time <= testPeriodStop) ? #00FF00 : na
bgcolor(testPeriodBackgroundColor, transp=97)

testPeriod() => true
/////////////// Component Code Stop ///////////////

///////////// RSI component /////////////
length = input( 14 )
overSold = input( 30 )
overBought = input( 70 )
price = close

vrsi = rsi(price, length)
notna = not na(vrsi)

/////////////// STRATEGY ///////////////
ts = input(99999, "Trailing Stop") / 100
tp = input(99999, "Take Profit") / 100
sl = input(99999, "Stop Loss") / 100

long = notna and crossover(vrsi, overSold)
short = notna and crossunder(vrsi, overBought)

last_long = long ? time : nz(last_long[1])
last_short = short ? time : nz(last_short[1])

long_signal = crossover(last_long, last_short)
short_signal = crossover(last_short, last_long)

last_open_long_signal = long_signal ? open : nz(last_open_long_signal[1])
last_open_short_signal = short_signal ? open : nz(last_open_short_signal[1])

last_long_signal = long_signal ? time : nz(last_long_signal[1])
last_short_signal = short_signal ? time : nz(last_short_signal[1])

in_long_signal = last_long_signal > last_short_signal
in_short_signal = last_short_signal > last_long_signal

last_high = not in_long_signal ? na : in_long_signal and (na(last_high[1]) or high > nz(last_high[1])) ? high : nz(last_high[1])
last_low = not in_short_signal ? na : in_short_signal and (na(last_low[1]) or low < nz(last_low[1])) ? low : nz(last_low[1])

long_ts = not na(last_high) and high <= (last_high - ts) //and high >= last_open_long_signal
short_ts = not na(last_low) and low >= (last_low + ts) //and low <= last_open_short_signal

long_tp = high >= (last_open_long_signal + tp)
short_tp = low <= (last_open_short_signal - tp)

long_sl = low <= (last_open_long_signal - sl)
short_sl = high >= (last_open_short_signal + sl)

leverage = input(200, "Leverage")
long_call = last_open_long_signal - (0.8 + 0.2 * (1/leverage)) / leverage * last_open_long_signal
short_call = last_open_short_signal + (0.78 + 0.2 * (1/leverage)) / leverage * last_open_short_signal
long_call_signal = low <= long_call
short_call_signal = high >= short_call

if testPeriod()
    strategy.entry("Long", strategy.long, when=long_signal)
    strategy.entry("Short", strategy.short, when=short_signal)

    // plot(long_call, color=red)
    // plot(short_call, color=green)
    strategy.close("Long", when=long_call_signal)
    strategy.close("Short", when=short_call_signal)
    strategy.close("Long", when=long_tp)
    strategy.close("Short", when=short_tp)
    strategy.close("Long", when=long_sl)
    strategy.close("Short", when=short_sl)
    strategy.close("Long", when=long_ts)
    strategy.close("Short", when=short_ts)
```

> Detail

https://www.fmz.com/strategy/431415

> Last Modified

2023-11-07 16:44:31
