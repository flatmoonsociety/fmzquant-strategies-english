
> Name

Daily high and low points combined with multi-timeframe EMA trend quantitative trading strategy-Multi-Timeframe-EMA-Trend-Strategy-with-Daily-High-Low-Breakout-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18b7662527b7f1342ed.png)

[trans]
#### Overview
This is a quantitative trading strategy that combines daily high and low breakouts with multi-time period EMA trends. The strategy mainly judges the trading timing by monitoring the price's breakthrough of the previous day's high and low points, combined with the EMA moving average and the capital flow indicator (CMF). The strategy uses both the hourly and daily 200-period EMA moving averages in two time periods, and improves the accuracy of trading through the verification of multiple technical indicators.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. Use the request.security function to obtain the highest and lowest prices of the previous day as key support and resistance levels.
2. Combine the 24-period EMA as the baseline for trend judgment.
3. Introduce CMF (20 periods) as a comprehensive indicator of trading volume and price, used to judge market capital flows.
4. Calculate the 200 moving average of the current time period and the 1-hour period at the same time, which is used to determine the trend direction of the larger period.
The specific trading rules are as follows:
Conditions for going long: price breaks through the previous day's high + closing price is above EMA + CMF is positive
Short selling conditions: price falls below the previous day's low + closing price below EMA + CMF is negative
Conditions for closing the position: the price falls below the EMA when going long, and the price breaks through EMA when going short.
#### Strategic Advantages
1. Comprehensive verification of multiple technical indicators improves the reliability of transactions
2. Through multi-time period analysis, market trends can be grasped more comprehensively
3. The CMF indicator combined with the relationship between volume and price can better judge the capital status of the market.
4. Using the previous day’s high and low points as key prices is in line with the trading habits of market participants.
5. The strategy has clear logic and is easy to understand and execute.
6. Have clear entry and exit conditions to reduce subjective judgments
#### Strategy Risk
1. Wrong signals may occur frequently in volatile markets
2. Not sensitive enough to instantaneous price breakthroughs
3. May miss trading opportunities in key positions
4. Failure to consider the larger cycle trend environment
5. Severe market fluctuations may cause large retracements.
Risk control suggestions:
1. Set a reasonable stop loss position
2. Adjust parameters according to different market environments
3. Add trend filter
4. Consider adding a volatility indicator
#### Strategy optimization direction
1. Introduce an adaptive parameter optimization mechanism
2. Add more market environment filter conditions
3. Optimize stop-loss and take-profit mechanisms
4. Add volatility indicators to adapt to different market environments
5. Consider adding a location management mechanism
6. Add transaction volume analysis indicators
#### Summary
This is a complete trading system that combines multiple technical indicators and multi-time period analysis. The strategy looks for trading opportunities through comprehensive analysis of intraday high and low breakouts, moving average trends and capital flows. Although there are certain risks, this strategy has good application value through reasonable risk control and continuous optimization and improvement. It is recommended that traders conduct sufficient backtesting and parameter optimization before using it in real trading.
|| 

#### Overview
This is a quantitative trading strategy that combines daily high-low breakouts with multi-timeframe EMA trends. The strategy primarily identifies trading opportunities by monitoring price breakouts of the previous day's high and low levels, combined with EMA trends and the Chaikin Money Flow (CMF) indicator. It utilizes 200-period EMAs on both hourly and daily timeframes to enhance trading accuracy through multiple technical indicator validation.

#### Strategy Principles
The core logic includes the following key elements:
1. Uses request.security function to obtain previous day's high and low prices as key support and resistance levels.
2. Incorporates 24-period EMA as the baseline for trend determination.
3. Implements CMF (20-period) as a comprehensive indicator of volume and price to assess market money flow.
4. Calculates 200 EMAs on both current and 1-hour timeframes to determine larger trend directions.

Specific trading rules:
Long Entry: Price breaks above previous day's high + Close above EMA + Positive CMF
Short Entry: Price breaks below previous day's low + Close below EMA + Negative CMF
Exit: Cross below EMA for longs, cross above EMA for shorts

#### Strategy Advantages
1. Multiple technical indicator validation improves trading reliability
2. Multi-timeframe analysis provides comprehensive trend assessment
3. CMF indicator integration better captures market money flow conditions
4. Previous day's high-low levels align with market participants' trading habits
5. Clear strategy logic that's easy to understand and execute
6. Well-defined entry and exit conditions minimize subjective judgment

#### Strategy Risks
1. May generate frequent false signals in ranging markets
2. Not sufficiently responsive to instantaneous price breakouts
3. Potential missed opportunities at key levels
4. Lacks consideration of larger timeframe trends
5. May experience significant drawdowns during extreme market volatility

Risk Control Suggestions:
1. Implement appropriate stop-loss levels
2. Adjust parameters based on market conditions
3. Add trend filters
4. Consider incorporating volatility indicators

#### Optimization Directions
1. Implement adaptive parameter optimization mechanisms
2. Add more market condition filters
3. Optimize stop-loss and take-profit mechanisms
4. Include volatility indicators for different market conditions
5. Consider position management mechanisms
6. Add volume analysis indicators

#### Summary
This is a complete trading system combining multiple technical indicators and multi-timeframe analysis. The strategy seeks trading opportunities through comprehensive analysis of intraday high-low breakouts, moving average trends, and money flow. While certain risks exist, the strategy holds good practical value through proper risk control and continuous optimization. Traders are advised to conduct thorough backtesting and parameter optimization before live implementation.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-28 00:00:00
end: 2024-11-27 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(title='The security Daily HIGH/LOW strategy', overlay=true, initial_capital=10000, calc_on_every_tick=true, 
         default_qty_type=strategy.percent_of_equity, default_qty_value=100, 
         commission_type=strategy.commission.percent, commission_value=0.1)

// General Inputs
len = input.int(24, minval=1, title='Length MA', group='Optimization parameters')
src = input.source(close, title='Source MA', group='Optimization parameters')
out = ta.ema(src, len)

length = input.int(20, minval=1, title='CMF Length', group='Optimization parameters')
ad = close == high and close == low or high == low ? 0 : (2 * close - low - high) / (high - low) * volume
mf = math.sum(ad, length) / math.sum(volume, length)

// Function to get daily high and low
f_secureSecurity(_symbol, _res, _src) =>
    request.security(_symbol, _res, _src[1], lookahead=barmerge.lookahead_on)

pricehigh = f_secureSecurity(syminfo.tickerid, 'D', high)
pricelow = f_secureSecurity(syminfo.tickerid, 'D', low)

// Plotting previous daily high and low
plot(pricehigh, title='Previous Daily High', style=plot.style_linebr, linewidth=2, color=color.new(color.white, 0))
plot(pricelow, title='Previous Daily Low', style=plot.style_linebr, linewidth=2, color=color.new(color.white, 0))

// Entry Conditions
short = ta.crossunder(low, pricelow) and close < out and mf < 0
long = ta.crossover(high, pricehigh) and close > out and mf > 0

if short and barstate.isconfirmed
    strategy.entry('short', strategy.short, stop=pricelow[1])
    strategy.close('short', when=close > out)

if long and barstate.isconfirmed
    strategy.entry('long', strategy.long, stop=pricehigh[1])
    strategy.close('long', when=close < out)

// 200 EMA on 1-hour timeframe
ema_200 = ta.ema(close, 200)
ema_200_1h = request.security(syminfo.tickerid, "60", ta.ema(close, 200))

plot(ema_200_1h, color=color.purple, title="200 EMA (1H)")
plot(ema_200, color=color.white, title="200 EMA")
```

> Detail

https://www.fmz.com/strategy/473239

> Last Modified

2024-11-28 15:20:59
