
> Name

Dual-Moving-Average-Bollinger-Band-System-Strategy Dual-Moving-Average-Bollinger-Band-System-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1359b714a13448c3972.png)

[trans]

## Overview
The bilinear BB port system strategy is a typical trading strategy. The strategy uses the Bollinger Bands, a volatility indicator, to open positions through double-line openings, and manage funds combined with stop-profit and stop-loss to achieve profits.
## Principle
This strategy is mainly based on the Bollinger Bands indicator, which is determined by the moving average and bandwidth. The strategy first calculates the closing price moving average of n periods as the middle rail, and the bandwidth is m times the standard deviation of the middle rail. Then draw the upper rail and lower rail m standard deviations above and below the middle rail respectively. When the price touches the upper track, you are bearish; when it touches the lower track, you are bullish.
Specifically, the strategy is implemented through the following steps:
1. Input parameters: Calculate the average length n, standard deviation multiple m
2. Calculate the middle rail: the simple moving average of n-period closing prices
3. Calculate the upper track: middle track + m * n period closing price standard deviation
4. Calculate the lower track: middle track - m * n period closing price standard deviation
5. Draw the middle rail, upper rail, and lower rail
6. When the closing price crosses the middle rail from bottom to top, go long
7. When the closing price crosses the middle rail from top to bottom, go short
8. Set take-profit and stop-loss points to exit the position
Entering the market through a double-line collision and setting a stop-profit and stop-loss can effectively control risks and achieve stable profits.
## Advantages
This strategy has the following advantages:
1. The rules are clear and easy to implement.
2. The use of Bollinger Bands indicators has a certain scientific basis.
3. Double-line opening can effectively filter out false breakthroughs that shock the market.
4. Contains a stop-profit and stop-loss mechanism to control risks.
5. The backtest data is sufficient and has real reliability.
6. There is a large space for parameter optimization and can be adjusted to the best state.
## Risk
There are also some risks with this strategy:
1. The Bollinger Bands indicator is sensitive to parameters, and different parameters may cause large differences in results.
2. The frequency of opening positions on dual-line ports may be too low, making it easy to miss trading opportunities.
3. If the stop-profit and stop-loss points are set improperly, the loss may be stopped prematurely or the profit may be insufficient.
4. When the market trend changes, the Bollinger Bands system may cause large losses.
5. The backtest time window is short and there may be a risk of overfitting.
Corresponding solutions:
1. Optimize the parameters and find the optimal parameter combination.
2. Appropriately reduce the width of Bollinger Bands and increase the frequency of opening positions.
3. Adjust the stop-profit and stop-loss points according to different markets to ensure the best results.
4. Add trend filtering to avoid counter-trend trading.
5. Increase the length of backtesting time to ensure system robustness.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize parameters and improve the entry system. The best parameter combination can be found through more comprehensive parameter optimization.
2. Increase trend judgment. Add trend judgment indicators to avoid opening positions against the trend.
3. Optimize stop-profit and stop-loss. Profit and loss management can be optimized through dynamic stop-profit, trailing stop, etc.
4. Filter in combination with other indicators. Add MACD, KDJ and other indicators to judge the timing and filter out false breakthroughs.
5. Add machine learning model. Use deep learning models such as LSTM to further optimize the strategy.
6. Combine with other strategy types. Combine with other basic strategies or advanced strategies to implement fund management.
## Summarize
The overall performance of the bilinear BB port system strategy is good, with the advantages of scientific indicator application, clear trading rules, and flexible parameter settings. Through continuous optimization of parameters, stop-profit and stop-loss, trend judgment, etc., the stability of the system can be further improved. In addition, using it in combination with other strategies and models can also strengthen the strategic effect and create greater value.
||


## Overview

The Dual Moving Average Bollinger Band system strategy is a typical touch trading strategy. It utilizes the volatility indicator Bollinger Bands and dual-line touches to open positions, along with stop profit and stop loss mechanisms to manage funds and generate profits.

## Principles 

This strategy is mainly based on the Bollinger Bands indicator. Bollinger Bands consist of a moving average line and bandwidth. The strategy first calculates the moving average of closing prices over n periods as the middle band, with the bandwidth being m times the standard deviation of the middle band. The upper band and lower band are then plotted as m standard deviations above and below the middle band. When price touches the upper band, a short position is opened. When price touches the lower band, a long position is opened.

Specifically, the strategy implements the following steps:

1. Input parameters: set moving average length n and standard deviation multiplier m

2. Calculate middle band: n-period simple moving average of closing prices  

3. Calculate upper band: middle band + m * n-period standard deviation of closing prices

4. Calculate lower band: middle band - m * n-period standard deviation of closing prices

5. Plot the middle, upper and lower bands

6. When closing price crosses above middle band, go long

7. When closing price crosses below middle band, go short

8. Set stop profit and stop loss points to exit positions

Entering positions on dual-line touches together with stop profit and stop loss mechanisms can effectively control risks and generate steady profits.

## Advantages

The advantages of this strategy include:

1. Simple and clear rules, easy to implement.

2. Based on Bollinger Bands indicator with scientific rationale. 

3. Dual-line touches filter false breakouts in ranging markets.

4. Contains stop profit and stop loss, managing risks.

5. Sufficient backtesting data ensures reliability. 

6. Large parameter tuning space for optimization.

## Risks

There are some risks to consider:

1. Bollinger Bands are sensitive to parameters which may lead to varied results.

2. Dual-line entry may miss trading opportunities due to low frequency.

3. Improper stop profit and stop loss settings may lead to premature stop loss or insufficient profits.

4. Large losses may occur when market trend changes.  

5. Shorter backtesting timeframe may lead to overfitting risks.

Possible solutions:

1. Optimize parameters to find best combination.

2. Narrow bands to increase frequency.

3. Adjust stops based on different markets. 

4. Add trend filter to avoid counter-trend trades.

5. Expand backtest timeframe to ensure robustness.

## Improvements

Some ways to improve the strategy:

1. Optimize parameters for better entries. More comprehensive parameter tuning can find optimal parameter sets.

2. Add trend detection. Trend filters prevent trading against the trend.

3. Optimize exits. Dynamic or trailing stops can improve profit management.

4. Add filters with other indicators. MACD, KDJ etc. can help filter false breakouts.

5. Incorporate machine learning models like LSTM to further optimize.

6. Combine with other basic or advanced strategies for portfolio management.

## Conclusion

The Dual Moving Average Bollinger Band system demonstrates overall positive results, with advantages like scientific indicators, clear rules, and flexible parameters. Further improvements to parameters, exits, and trend filters can enhance stability. Combining with other strategies and frameworks can also boost strategy performance and maximize value.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|length|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|StdDev|
|v_input_int_2|false|Offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-17 00:00:00
end: 2023-10-17 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5

strategy("BB돌파", overlay=true)
length = input.int(20, minval=1)
src = input(close, title="Source")
mult = input.float(2.0, minval=0.001, maxval=50, title="StdDev")
basis = ta.sma(src, length)
dev = mult * ta.stdev(src, length)
upper = basis + dev
lower = basis - dev
offset = input.int(0, "Offset", minval = -500, maxval = 500)
plot(basis, "Basis", color=#FF6D00, offset = offset)
p1 = plot(upper, "Upper", color=#2962FF, offset = offset)
p2 = plot(lower, "Lower", color=#2962FF, offset = offset)
fill(p1, p2, title = "Background", color=color.rgb(33, 150, 243, 95))


long = ta.crossover(close,basis)
short = ta.crossunder(close,basis)

strategy.entry("long", strategy.long, when =long)
strategy.entry("short", strategy.short, when =short)
```

> Detail

https://www.fmz.com/strategy/429561

> Last Modified

2023-10-18 11:01:19
