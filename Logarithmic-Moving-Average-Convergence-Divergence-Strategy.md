
> Name

Logarithmic-Moving-Average-Convergence-Divergence-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy generates trading signals based on the Logarithmic MACD. It determines market trends and opportunities by calculating the difference between fast and slow logarithmic moving averages.
## Strategy Principle
The main logic of this strategy is:
- Calculate fast logarithmic moving average (default 12 days) and slow logarithmic moving average (default 26 days)
- Logarithmic MACD is the difference between the two and expresses market momentum
- The signal line is the smoothed moving average of MACD (default 9 days)
- Go long when the MACD line breaks above the signal line from below
- Go short when the MACD line falls below the signal line from above
- Express the difference between MACD and signal line in the form of a histogram
Compared with the simple moving average MACD, the logarithmic MACD can highlight the changing trends of exponential growth markets. After logarithmic transformation, values ​​with large fluctuations can remain relatively comparable on the chart.
## Strategic Advantages
- Use logarithmic transformation to detect price changes at the exponential level
- Logarithmic MACD highlights price movement information
- The signal line smoothes MACD to form a trading signal
- Histogram MACD intuitively expresses the trend direction
## Strategy Risk
- Logarithmic transformation may amplify price shocks
- Frequent signals, easy to over trade
- Failure to consider stop loss management and incomplete risk control
Countermeasures:
- Adjust parameters and reduce signal frequency
- Add filter conditions to avoid generating signals during oscillations
- Set stop loss strategies to control single losses
## Strategy optimization direction
- Optimize parameters and improve stability
- Try other exponential conversion methods, such as exponential moving averages
- Filter signals combined with trend indicators
- Add stop loss strategy
- Use machine learning to determine signal reliability
## Summarize
This strategy uses logarithmic transformation to improve the sensitivity of the MACD indicator and can detect trend changes earlier. However, attention should be paid to controlling the frequency of transactions. Through parameter optimization, risk control and other improvements, this strategy can become a stable and personalized quantitative trading system.
|| 

## Overview 

This strategy generates trading signals using the Logarithmic MACD indicator. It calculates the difference between fast and slow logarithmic moving averages to gauge market momentum and opportunities.

## Strategy Logic

The main logic is:

- Calculate fast logarithmic MA (default 12) and slow logarithmic MA (default 26)

- Logarithmic MACD is their difference, expressing market momentum

- Signal line is smoothed MA of MACD (default 9) 

- Go long when MACD crosses above signal from below

- Go short when MACD crosses below signal from above

- MACD-Signal difference plotted as histogram 

Compared to simple MACD, logarithmic MACD can better highlight exponential growth trends. Log transform maintains comparability of volatile values on the chart.

## Advantages

- Detects exponential price movements using logarithmic transform

- Log MACD highlights price fluctuation information

- Signal line smooths MACD into trading signals  

- MACD histogram intuitively shows trend direction

## Risks

- Log transform may amplify price noise 

- Frequent signals, risks over-trading

- No stop loss management, incomplete risk control

Mitigations:

- Adjust parameters to reduce signal frequency

- Add filters to avoid signals in choppy conditions

- Implement stop loss to control loss per trade

## Enhancement Opportunities 

- Optimize parameters for stability

- Try other transforms like exponential moving average

- Add trend filter to screen signals

- Incorporate stop loss strategies

- Use machine learning to judge signal reliability

## Conclusion

The logarithmic transform enhances MACD's sensitivity for early trend detection. But trade frequency should be controlled. With optimizations in parameters, risk management etc., this strategy can become a stable and unique quantitative system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|Fast Length|
|v_input_2|26|Slow Length|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|9|Signal Smoothing|
|v_input_5|false|Simple MA(Oscillator)|
|v_input_6|false|Simple MA(Signal Line)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-14 00:00:00
end: 2023-09-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="Logarithmic Moving Average Convergence Divergence Strategy", shorttitle="LMACD Strategy")

// Getting inputs
fast_length = input(title="Fast Length",  defval=12)
slow_length = input(title="Slow Length",  defval=26)
src = input(title="Source",  defval=close)
signal_length = input(title="Signal Smoothing",  minval = 1, maxval = 50, defval = 9)
sma_source = input(title="Simple MA(Oscillator)",  defval=false)
sma_signal = input(title="Simple MA(Signal Line)", defval=false)

// Plot colors
col_grow_above = #26A69A
col_grow_below = #FFCDD2
col_fall_above = #B2DFDB
col_fall_below = #EF5350
col_macd = #0094ff
col_signal = #ff6a00

// Calculating
fast_ma = sma_source ? sma(src, fast_length) : ema(src, fast_length)
slow_ma = sma_source ? sma(src, slow_length) : ema(src, slow_length)
lmacd = log(fast_ma) - log(slow_ma)
signal = sma_signal ? sma(lmacd, signal_length) : ema(lmacd, signal_length)
hist = lmacd - signal

plot(hist, title="Histogram", style=columns, color=(hist>=0 ? (hist[1] < hist ? col_grow_above : col_fall_above) : (hist[1] < hist ? col_grow_below : col_fall_below) ), transp=0 )
plot(lmacd, title="LMACD", color=col_macd, transp=0)
plot(signal, title="Signal", color=col_signal, transp=0)

if (crossover(hist, 0))
	strategy.entry("Long", strategy.long, comment="LMACD long")
if (crossunder(hist, 0))
	strategy.entry("Short", strategy.short, comment="LMACD short")
```

> Detail

https://www.fmz.com/strategy/427482

> Last Modified

2023-09-21 15:38:05
