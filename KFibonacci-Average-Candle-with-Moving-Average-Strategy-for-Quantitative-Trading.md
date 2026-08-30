
> Name

Quantitative trading strategy Fibonacci-Average-Candle-with-Moving-Average-Strategy-for-Quantitative-Trading based on Fibonacci average K-line and moving average
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/108818bc053c805e45f.png)
 [trans]
## Overview
This strategy builds an average K-line and a moving average calculated based on the Fibonacci sequence, combined with a variety of price technical indicator rules, to achieve quantitative trading that is only long but not short. Preliminary tests show that this strategy performs better on large cycle graphics.
## Strategy Principle
This strategy is mainly implemented through the following steps:
1. Based on the Fibonacci sequence, calculate the average closing price, highest price, lowest price and opening price of the last 10 Fibonacci cycles, and construct an average K-line.
2. Calculate the exponential moving average (EMA) of periods 1, 2, 3, 5, 8, 13, 21, 34 and 55 for the average closing price, and calculate the average of these 9 EMAs to obtain the average EMA.
3. Set the conditions for long and close positions: open a long position when the average K-line pattern shows a long signal (close positive, yang wraps yang, etc.) and the closing price is higher than the average EMA; close the position when the average K-line pattern shows a short signal (close yin, yin wraps yin, etc.) and the closing price is lower than the average EMA.
By calculating the average K-line to filter price fluctuations, and then combining the moving average indicators to send trading signals, you can effectively identify trends and control trading risks.
## Strategic Advantages
1. Calculate the average K-line based on the Fibonacci sequence, which can effectively filter random price fluctuations and identify trend signals.
2. Constructing an average EMA from multiple EMA averages can enhance the stability of support and resistance levels and improve signal quality.
3. Only going long but not short can reduce the number of transactions, transaction costs and the impact of slippage.
4. It performs well in large cycles and is suitable for medium and long-term operations.
## Strategy Risk
1. A long-only strategy may suffer larger losses in a short market.
2. The EMA moving average is prone to lag, and the best entry point may be missed.
3. If you pursue large-cycle operations too much, you may miss short- and medium-term opportunities.
4. The space for parameter optimization is limited, and the real performance may be weaker than the backtest results of parameter optimization.
## Optimization direction
1. You can test and add appropriate stop-loss strategies to stop losses and exit when losses expand.
2. It can be combined with volatility indicators such as ATR to dynamically adjust the position size.
3. You can test the appropriate intervention in short selling in the downward trend to increase the strategic income.
4. You can optimize the period parameters of EMA and find the best parameter combination.
## Summarize
This strategy realizes quantitative trading by constructing Fibonacci average K-line and moving average indicators to identify trend signals. The strategy has the advantage of calculating the average K-line filter price and only doing long operations to reduce transaction costs. At the same time, there are also long-only market risks and the problem of EMA lagging. Generally speaking, this strategy controls trading risks from multiple dimensions, performs well in large cycles, and is suitable for medium and long-term operations. By continuing to optimize, strategy stability and profit levels can be improved.
||

## Overview

This strategy constructs average candles and moving averages based on the Fibonacci sequence to implement quantitative trading with only long positions and no short positions. Initial tests show that this strategy performs better on larger timeframes.

## Strategy Principle  

The main steps of this strategy are:

1. Calculate the average close, high, low and open prices of the most recent 10 Fibonacci cycles to construct an average candle.

2. Compute 1-, 2-, 3-, 5-, 8-, 13-, 21-, 34- and 55-period exponential moving averages (EMA) of the average close price, and take their average to obtain the average EMA.

3. Set long and close conditions: open long position when the average candle shows bullish patterns (like closing above open, bullish engulfing) and close is above average EMA; close long position when average candle shows bearish patterns (like closing below open, bearish engulfing) and close is below average EMA.

By calculating average candles to filter price fluctuations and combining with moving average indicators to generate trading signals, this strategy can effectively identify trends and control trading risks.

## Advantages

1. Average candles based on Fibonacci sequence can filter random price noise effectively and identify trend signals.

2. Average of multiple EMAs enhances stability of support/resistance levels and improves signal quality.

3. Only long positions reduces number of trades, lowers trading costs and slippage impacts. 

4. Performs well on larger timeframes, suitable for medium-to-long term trading.

## Risks

1. Only-long strategy can incur significant losses in bearish markets.

2. EMA lines are prone to lagging, potentially missing best entry points.

3. Overly pursuing large timeframes may miss opportunities in shorter timeframes.  

4. Limited parameter optimization space means real trading performance may underperform backtest results.

## Enhancement Areas

1. Can test adding appropriate stop loss to exit positions when losses mount.

2. Can combine volatility measures like ATR to dynamically adjust position sizing.

3. Can test taking short positions appropriately during downtrends to increase profits.

4. Can optimize EMA period parameters to find best combinations.

## Conclusion

This strategy identifies trend signals for quantitative trading by constructing Fibonacci average candles and moving average indicators. It takes advantage of filtering price noise with average candles and reducing trading costs by only going long. It also has the risks of bearish markets for only-long positions and EMA lagging issues. Overall, this strategy controls trading risks from multiple aspects and performs well on larger timeframes, suitable for medium-to-long term trading. Further optimizations can improve robustness and profitability.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SoftKill21

//@version=4
strategy("Fibonacci candle", overlay=false  )


//plot of our fibonacci candle
// Fibonacci 
// Fn = Fn-1 + Fn-2
// F10 = 55
// 0 1 2 3 5 8 13 21 34 55

avg_close = (close[0] + close[1] + close[2] + close[3] +close[5] + close[8] + close[13]+ close[21] + close[34] + close[55]) / 10
avg_high = (high[0] + high[1] + high[2] + high[3] +high[5] + high[8] + high[13]+ high[21] + high[34] + high[55]) / 10
avg_low = (low[0] + low[1] + low[2] + low[3] +low[5] + low[8] + low[13]+ low[21] + low[34] + low[55]) / 10
avg_open = (open[0] + open[1] + open[2] + open[3] +open[5] + open[8] + open[13]+ open[21] + open[34] + open[55]) / 10


src = avg_close//input(avg_close, title="Source")


out55 = ema(src, 55)
out1 = ema(src, 1)
out2 = ema(src, 2)
out3 = ema(src, 3)
out5 = ema(src, 5)
out8 = ema(src, 8)
out13 = ema(src, 13)
out21 = ema(src, 21)
out34 = ema(src, 34)

avg_ema = (out55 + out1 + out2 + out3+ out5 + out8 + out13 + out21 + out34)/9

plot(avg_ema)

plotcandle(avg_open, avg_high, avg_low, avg_close, title='Title', color = avg_open < avg_close ? color.green : color.red, wickcolor=color.white)

long = avg_open < avg_close and avg_close > avg_close[1] and avg_high > avg_high[1] and  avg_close[1] > avg_close[2] and avg_high[1] > avg_high[2]
short = avg_open > avg_close and avg_close < avg_close[1] and avg_low < avg_low[1] and avg_close[1] < avg_close[2] and avg_low[1] < avg_low[2]

strategy.entry("long",1,when=long and avg_close > avg_ema)
strategy.close('long',when=short and avg_close < avg_ema)

```

> Detail

https://www.fmz.com/strategy/439350

> Last Modified

2024-01-19 14:36:45
