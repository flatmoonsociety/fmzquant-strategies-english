
> Name

Gold Quick Breakout Strategy Breakout-Scalper-Catching-Trend-Changes-Quickly
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/745dc7fc74f530ed8a11d122c0c1f00f5664531c91efcaa93739c512c29a70b2.png)

[trans]


## Overview
The Gold Rapid Breakout Strategy is a strategy that utilizes fast and slow lines for breakout trading. It sets a fast window and a slow window to determine the trend direction and enter the market at the breakthrough point. At the same time, it also sets stop-loss closing points to control risks. This strategy is suitable for highly volatile varieties and can capture rapid changes in trends to make profits.
## Strategy Principle
This strategy sets both a fast window and a slow window. The default fast window is 13 periods, which is used to capture short-term trends; the default slow window is 52 periods, which is used to determine the direction of medium and long-term trends. The strategy calculates the midline of the fast and slow windows and plots them on the chart. When the fast midline crosses the slow midline, it indicates a short-term trend change, and a new upward trend may be formed; when the fast midline crosses below the slow midline, it indicates a short-term trend shift, and a new downward trend may be formed.
When the fast midline crosses the slow midline, if the real-time price is also higher than the fast midline, a buy signal is formed, and the highest price of the slow window is used as a buy stop order to open a long position. When the fast midline crosses the slow midline, if the real-time price is also lower than the fast midline, a sell signal is formed, and the lowest price of the slow window is used as a sell stop order to open a short position.
In addition, the strategy also sets stop-loss closing points. The stop-loss closing point for long is the larger value of the lowest price of the fast window and the lowest price of the slow window, and the stop-loss closing point for short is the smaller value of the highest price of the fast window and the highest price of the slow window. This ensures that the stop loss is outside the current trend direction to control risk.
When the long and short conditions are not met, the strategy will close the position. This avoids unnecessary losses when the trend consolidates.
## Advantage Analysis
This strategy has the following advantages:
1. Quickly judge trend changes, suitable for high volatility varieties. Through the combination of fast window and slow window, changes in short-term, medium- and long-term trends can be quickly captured, which is suitable for highly volatile products such as gold.
2. Risk control is in place. Through a reasonable stop-loss mechanism, losses can be stopped in time and strategic risks can be effectively controlled.
3. The transaction logic is clear and simple. It is very simple and clear to judge based on the intersection of fast and slow moving averages, and then set a reasonable stop loss point.
4. Easy to optimize and expand. It can be optimized by adjusting parameters, etc., or it can be expanded by adding more judgment indicators.
## Risk Analysis
There are also some risks with this strategy:
1. The fast window is easily affected by noise. As a short-term judgment indicator, the fast window may be affected by greater market noise, resulting in false signals.
2. The slow window has hysteresis. When the mid- to long-term trend turns, there may be a certain lag in the slow window, resulting in delayed signal judgment.
3. The stop may be too close. The stop loss point directly takes the speed window data, which may be too close to the nearest price and is easily stopped.
4. Inability to effectively handle consolidating markets. When the market continues to consolidate, this strategy is prone to generating false signals and leading to losses.
Corresponding solutions:
1. Adjust the fast window period and add other filtering indicators.
2. Optimize the slow window period and add indicators such as moving averages to assist judgment.
3. Set the stop loss point with a certain buffer zone from the recent price.
4. Add indicators to judge consolidation to avoid wrong signals.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize the period parameters of the fast window and slow window to better adapt to different varieties.
2. Add a position management mechanism to control risks by adjusting positions.
3. Add a profit-taking strategy and take the initiative to stop profit after a certain percentage of profit.
4. Add more indicator filters to form more stable trading signals. Such as enhancing buying and selling points and avoiding false signals.
5. Increase the judgment of specific forms, such as triangle convergence, head and shoulders divergence, etc., to improve the winning rate of the strategy.
6. Add machine learning algorithms, use big data to train judgment models, and automatically optimize the parameters of the strategy.
## Summarize
The gold fast breakout strategy is a trend breakout strategy based on the intersection of fast and slow moving averages. It can quickly capture trend changes and is suitable for highly volatile varieties such as gold. At the same time, it also sets up a reasonable stop-loss mechanism to control risks. This strategy has the advantages of simple and clear trading logic and easy optimization. We also found the possible risks of this strategy through analysis and gave corresponding optimization directions. Overall, this strategy provides us with an efficient way to capture trend changes and has very good practical value. Through continuous optimization and improvement, it can be built into a stable and reliable trend breakthrough trading system.
|| 

## Overview

The Breakout Scalper strategy is a breakout trading strategy that utilizes fast and slow moving averages to identify trend changes. It sets up entry stops and trailing exit stops for risk management. The strategy closes positions manually when the market goes sideways. It is suitable for volatile instruments to capitalize on fast trend shifts.

## Strategy Logic

The strategy employs a fast window and a slow window. The default periods are 13 and 52 respectively. The fast window captures short-term trends while the slow window determines overall market direction. The mid prices of the two windows are plotted. When the fast mid-price crosses above the slow mid-price, an uptrend may be forming. When the fast mid-price crosses below the slow one, a downtrend may be starting.

When the fast mid-price is above the slow mid-price, and the instant price is also above the fast mid-price, a buy signal is generated. The entry stop is placed at the slow window's highest price. When the fast mid-price is below the slow one, and the instant price is below the fast mid-price, a sell signal is triggered, with the entry stop at the slow window's lowest price.

In addition, exit stops are defined for risk control. The long exit stop is the max of the fast and slow windows' lowest prices. The short exit stop is the min of the fast and slow windows' highest prices. This ensures the stops are placed outside the current trend direction for risk mitigation.

Positions are closed when the entry conditions are no longer valid, avoiding unnecessary losses during sideways markets.

## Advantage Analysis

The key advantages of this strategy include:

1. Quickly catches trend changes suitable for volatile assets. The combination of the fast and slow windows enables responsive trend change detection.

2. Effective risk management via reasonable stops. The stops allow timely exits to control losses.

3. Simple and clear logic based on moving average crosses and stops. Easy to understand and implement.

4. Easily optimizable and extensible. Parameters can be tuned and more indicators can be added.

## Risk Analysis

The main risks are:

1. Fast window prone to noise. Market noise can generate incorrect signals.

2. Slow window lag. Turning points may be detected late. 

3. Stops too close to market. Stops based directly on window prices may be too tight.

4. Sideways markets lead to whipsaws. Choppy markets generate false signals.

Mitigations:

1. Optimize fast window and add filters.

2. Improve slow window and add confirming indicators.

3. Buffer stops from market price. 

4. Detect sideways and avoid signals.

## Optimization Opportunities

The strategy can be enhanced in several aspects:

1. Optimize window periods for different assets.

2. Add position sizing for better risk control. 

3. Implement profit taking mechanisms.

4. Add more filters to create robust signals.

5. Incorporate pattern detection like triangles and divergences.

6. Utilize machine learning to optimize parameters.

## Conclusion

The Breakout Scalper aims to catch trend changes quickly based on fast and slow moving average crosses. It is suitable for volatile markets like gold. The stops provide risk management. The simple logic makes it easy to understand and optimize. The identified risks and enhancements offer ways to improve the strategy further. Overall, this is an efficient trend trading system that can be refined into a robust approach.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|13|Fast Window|
|v_input_2|52|Slow Window|
|v_input_3|3|Instant Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-17 00:00:00
end: 2023-10-24 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Breakout Scalper", overlay=true)

fast_window = input(title="Fast Window",  defval=13, minval=1)
slow_window = input(title="Slow Window",  defval=52, minval=1)
instant_period = input(title="Instant Period",  defval=3, minval=1)

fast_low = lowest(fast_window)
fast_high = highest(fast_window)
fast_mid = (fast_low + fast_high) / 2

slow_low = lowest(slow_window)
slow_high = highest(slow_window)
slow_mid = (slow_low + slow_high) / 2

instant_price = ema(close, instant_period)

plot(instant_price, title="Instant Price", color=black, transp=50)
fp = plot(fast_mid, title="Fast Mid", color=green)
sp = plot(slow_mid, title="Slow Mid", color=red)
fill(fp, sp, color=(fast_mid > slow_mid ? green : red))

is_buy_mode = (instant_price > fast_mid) and (fast_mid > slow_mid)
is_sell_mode = (instant_price < fast_mid) and (fast_mid < slow_mid)
entry_color = is_buy_mode ? green : (is_sell_mode ? red : na)
exit_color = is_buy_mode ? red : (is_sell_mode ? green : na)

entry_buy_stop = slow_high
entry_sell_stop = slow_low
exit_buy_stop = max(fast_low, slow_low)
exit_sell_stop = min(fast_high, slow_high)
strategy.entry("long", strategy.long, stop=entry_buy_stop, when=is_buy_mode)
strategy.exit("stop", "long", stop=exit_buy_stop)
strategy.entry("short", strategy.short, stop=entry_sell_stop, when=is_sell_mode)
strategy.exit("stop", "short", stop=exit_sell_stop)
strategy.close("long", when=(not is_buy_mode))
strategy.close("short", when=(not is_sell_mode))

entry_buy_stop_color = (strategy.position_size == 0) ? (is_buy_mode ? green : na) : na
plotshape(entry_buy_stop, location=location.absolute, color=entry_buy_stop_color, style=shape.circle)
entry_sell_stop_color = (strategy.position_size == 0) ? (is_sell_mode ? red : na) : na
plotshape(entry_sell_stop, location=location.absolute, color=entry_sell_stop_color, style=shape.circle)
exit_buy_stop_color = (strategy.position_size > 0) ? red : na
plotshape(exit_buy_stop, location=location.absolute, color=exit_buy_stop_color, style=shape.xcross)
exit_sell_stop_color = (strategy.position_size < 0) ? green : na
plotshape(exit_sell_stop, location=location.absolute, color=exit_sell_stop_color, style=shape.xcross)

```

> Detail

https://www.fmz.com/strategy/430175

> Last Modified

2023-10-25 17:58:11
