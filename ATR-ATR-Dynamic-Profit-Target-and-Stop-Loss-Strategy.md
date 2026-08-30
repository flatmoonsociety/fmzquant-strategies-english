
> Name

ATR-Dynamic-Profit-Target-and-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description



[trans]

## Strategy Principle
This strategy uses dynamic take-profit and stop-loss points to trade. Take profit and stop loss points are adjusted in real time based on the current price and volatility.
Specific transaction logic:
1. Calculate the average true fluctuation range ATR for a certain period (such as 20 days)
2. When in a bullish state, the take-profit and stop-loss points are the highest price minus the ATR multiplier
3. When in a bearish state, the take-profit and stop-loss points are the lowest price plus the ATR multiplier
4. Carry out reverse trading when the price exceeds the take-profit and stop-loss points
5. Change the trend status when the price breaks through the take-profit and stop-loss points
6. Adjust the take profit and stop loss levels according to the new status
This strategy makes full use of ATR to automatically set stop loss and profit levels to achieve dynamic tracking. Able to lock in profits in time and avoid losses from expanding.
## Strategic Advantages
- ATR automatically calculates take profit and stop loss levels
- Dynamically adjust and track prices in real time
- Stop losses and profits in time to control risks
## Strategy Risk
- ATR parameters require repeated testing and optimization
- The stop loss is too close and it is easy to be stopped.
- Pay attention to real-time changes in ATR value
## Summarize
This strategy uses ATR to dynamically set take profit and stop loss levels to achieve automatic tracking. Optimizing ATR parameters can achieve better stop loss effect. However, a stop loss that is too close should be used with caution.

||

## Strategy Logic

This strategy uses dynamic profit targets and stop losses that adjust based on current price and volatility.

The logic is:

1. Calculate Average True Range (ATR) over a period (e.g. 20 days)

2. In uptrend, profit target/stop is highest price minus ATR multiple 

3. In downtrend, profit target/stop is lowest price plus ATR multiple

4. Reverse trade when price exceeds profit target/stop 

5. Trend changes when price breaches profit target/stop

6. Adjust profit target/stop based on new trend state

The strategy leverages ATR to automatically set dynamic trailing profit targets and stops. This allows timely locking in of profits and preventing excessive losses.

## Advantages

- ATR automatically calculates profit/stop levels

- Dynamic adjustment trails price in real-time

- Timely profit taking and stopping controls risk

## Risks 

- ATR parameters require optimization

- Stops too close risks being stopped out

- Need to monitor real-time ATR changes

## Summary

This strategy uses ATR to dynamically set profit/stop levels for automatic trailing. ATR tuning can improve stop performance. But over-tight stops require caution.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|length|
|v_input_2|true|mult|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-09-13 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Dhananjay Volatility stop strategy v1.0", overlay=true)


length = input(20)
mult = input(1)
atr_ = atr(length)
max1 = max(nz(max_[1]), close)
min1 = min(nz(min_[1]), close)
is_uptrend_prev = nz(is_uptrend[1], true)
stop = is_uptrend_prev ? max1 - mult * atr_ : min1 + mult * atr_
vstop_prev = nz(vstop[1])
vstop1 = is_uptrend_prev ? max(vstop_prev, stop) : min(vstop_prev, stop)
is_uptrend = close - vstop1 >= 0
is_trend_changed = is_uptrend != is_uptrend_prev
max_ = is_trend_changed ? close : max1
min_ = is_trend_changed ? close : min1
vstop = is_trend_changed ? is_uptrend ? max_ - mult * atr_ : min_ + mult * atr_ : vstop1
plot(vstop, color = is_uptrend ? green : red, style=line, linewidth=2)

bearish = close < vstop 
bullish = close > vstop 


if (bullish)
    strategy.entry("Buy", strategy.long, 1)
    
    

if (bearish)
    strategy.entry("Sell", strategy.short, 1)
    
    
```

> Detail

https://www.fmz.com/strategy/426801

> Last Modified

2023-09-14 16:22:53
