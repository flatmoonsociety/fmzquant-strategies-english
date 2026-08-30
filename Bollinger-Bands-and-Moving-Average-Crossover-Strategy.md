
> Name

Bollinger Bands Cross Moving Average Strategy-Bollinger-Bands-and-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3970f8693dcec500c52edf9ba761f964c3015bfcbb6fd3f807eed39e63783fe1.png)

[trans]
#### Overview
This strategy combines two technical indicators, the Bollinger Bands and the Moving Average, and uses the relative position of the Bollinger Bands and the price as well as the cross signals of the fast and slow moving averages to judge the market trend, thereby achieving timing of buying and selling. When the price breaks through the lower track of the Bollinger Bands, open a long position, and when it breaks through the upper track, open a short position; at the same time, when the fast moving average crosses the slow moving average, open a long position, and close the position when it crosses below. This strategy can help investors grasp market trends and achieve stable investment returns.
#### Strategy Principle
1. Bollinger Bands consists of three lines: middle track, upper track and lower track. The middle rail is the moving average, and the upper and lower rails are the standard deviation plus or minus a certain multiple of the middle rail. When the price breaks through the upper band, it indicates that the market is overbought and a correction may occur; when it breaks through the lower band, it indicates that the market is oversold and a rebound may occur.
2. The intersection of fast and slow moving averages is also a commonly used trend judgment method. When the fast moving average crosses the slow moving average, it is called a "golden cross", indicating that the market may become stronger; when the fast moving average crosses below the slow moving average, it is called a "dead cross", indicating that the market may weaken.
3. This strategy uses Bollinger Bands to determine overbought and oversold, and uses moving average crossovers to determine trends. The combination of the two can form a more reliable trading signal. Go long when the price breaks through the lower Bollinger Band and the fast moving average crosses the slow moving average, and close the position until the price breaks through the upper Bollinger Band or the fast moving average crosses the slow moving average.
#### Advantage Analysis
1. Bollinger Bands can adaptively adjust according to the size of price fluctuations and are more sensitive to changes in volatility.
2. The moving average system can effectively track market trends and help investors grasp the main trend direction.
3. Combine Bollinger Bands with moving averages to form a breakthrough + trend tracking trading system, which can effectively reduce trading frequency and costs and improve system stability.
4. Multiple parameters are set in the code, such as moving average type, period, etc., which can be flexibly adjusted to adapt to different market conditions.
#### Risk Analysis
1. When market volatility suddenly increases, the Bollinger Bands channel will expand sharply, and more stops may occur.
2. The moving average system may lag behind in judging the trend, resulting in inaccurate entry and exit timings.
3. Trend strategies perform generally in volatile markets and need to be optimized in combination with other methods.
4. Improper parameter settings may cause the strategy to fail, requiring continuous tuning and testing.
#### Optimization direction
1. On the basis of moving average crossover, other trend indicators such as MACD can be added to further confirm the trend signal.
2. Bollinger Band breakthroughs can be combined with stop loss indicators such as ATR to control retracement risks.
3. On the basis of trend judgment, methods such as market divergence and pattern recognition can be added to judge trend turning points in advance.
4. For different targets and periods, parameters need to be optimized to find a suitable parameter combination.
#### Summary
The Bollinger Band Cross Moving Average strategy is a classic trend following strategy. It uses Bollinger Bands to determine overbought and oversold, and uses moving average crossovers to determine trends. It can effectively grasp market trends and achieve steady returns. However, in actual application, it is necessary to pay attention to controlling retracement, optimizing parameters, and continuously improving it in combination with other methods to adapt to the changing market environment.
|| 

#### Overview
This strategy combines two technical indicators, Bollinger Bands and moving averages, to determine market trends based on the relative position of price to the Bollinger Bands and the crossover signals of fast and slow moving averages, thus realizing timely buying and selling. When the price breaks through the lower band of the Bollinger Bands, it opens a long position, and when it breaks through the upper band, it opens a short position. At the same time, when the fast moving average crosses above the slow moving average, it opens a long position, and when it crosses below, it closes the position. This strategy can help investors grasp market trends and achieve stable investment returns.

#### Strategy Principle
1. Bollinger Bands consist of three lines: the middle band, the upper band, and the lower band. The middle band is the moving average, and the upper and lower bands are the middle band plus or minus a certain multiple of standard deviations. When the price breaks through the upper band, it indicates that the market is overbought and may experience a pullback; when it breaks through the lower band, it indicates that the market is oversold and may experience a rebound.
2. The crossover of fast and slow moving averages is also a commonly used method for judging trends. When the fast moving average crosses above the slow moving average, it is called a "golden cross", indicating that the market may turn strong; when the fast moving average crosses below the slow moving average, it is called a "death cross", indicating that the market may turn weak.
3. This strategy uses Bollinger Bands to judge overbought and oversold conditions, and uses the moving average crossover to judge trends. The combination of the two can form a relatively reliable trading signal. When the price breaks through the lower band of the Bollinger Bands and the fast moving average crosses above the slow moving average, it goes long until the price breaks through the upper band or the fast moving average crosses below the slow moving average, at which point it closes the position.

#### Advantage Analysis
1. Bollinger Bands can adaptively adjust according to the size of price fluctuations and are more sensitive to changes in volatility.
2. The moving average system can effectively track market trends and help investors grasp the main trend direction.
3. Combining Bollinger Bands and moving averages to form a breakout + trend following trading system can effectively reduce trading frequency and costs, and improve system stability.
4. The code sets multiple parameters, such as the moving average type and period, which can be flexibly adjusted to adapt to different market conditions.

#### Risk Analysis
1. When market volatility suddenly increases, the Bollinger Band channel will expand sharply, and more stop-losses may occur.
2. The moving average system's judgment of trends may lag, resulting in inaccurate entry and exit timing.
3. Trend-following strategies perform generally in range-bound markets and need to be optimized in combination with other methods.
4. Improper parameter settings may cause the strategy to fail, requiring continuous optimization and testing.

#### Optimization Direction
1. On the basis of moving average crossovers, other trend indicators such as MACD can be added to further confirm trend signals.
2. Bollinger Band breakouts can be combined with stop-loss indicators such as ATR to control drawdown risk.
3. On the basis of trend judgment, methods such as market divergence and pattern recognition can be added to judge trend turning points earlier.
4. For different underlying assets and time periods, parameters need to be optimized to find suitable parameter combinations.

#### Summary
The Bollinger Bands and Moving Average Crossover strategy is a classic trend-following strategy that uses Bollinger Bands to judge overbought and oversold conditions and moving average crossovers to judge trends, which can effectively grasp market trends and achieve stable returns. However, in practical application, it is necessary to pay attention to controlling drawdowns, optimizing parameters, and continuously improving in combination with other methods to adapt to the changing market environment.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-05-01 00:00:00
end: 2024-05-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(shorttitle="BB Strategy", title="Bollinger Bands Strategy", overlay=true)

// Input parameters
length = input.int(20, minval=1)
maType = input.string("SMA", "Basis MA Type", options=["SMA", "EMA", "SMMA (RMA)", "WMA", "VWMA"])
src = input(close, title="Source")
mult = input.float(2.0, minval=0.001, maxval=50, title="StdDev")
offset = input.int(0, "Offset", minval=-500, maxval=500)

// Moving average function
ma(source, length, _type) =>
    switch _type
        "SMA" => ta.sma(source, length)
        "EMA" => ta.ema(source, length)
        "SMMA (RMA)" => ta.rma(source, length)
        "WMA" => ta.wma(source, length)
        "VWMA" => ta.vwma(source, length)

// Calculate Bollinger Bands
basis = ma(src, length, maType)
dev = mult * ta.stdev(src, length)
upper = basis + dev
lower = basis - dev

// Plot Bollinger Bands
plot(basis, "Basis", color=color.blue, offset=offset)
p1 = plot(upper, "Upper", color=color.red, offset=offset)
p2 = plot(lower, "Lower", color=color.green, offset=offset)
fill(p1, p2, title="Background", color=color.rgb(33, 150, 243, 95))

// Strategy entry and exit conditions
if (ta.crossover(close, lower))
    strategy.entry("Buy", strategy.long)

if (ta.crossunder(close, upper))
    strategy.entry("Sell", strategy.short)

```

> Detail

https://www.fmz.com/strategy/453647

> Last Modified

2024-06-07 14:52:49
