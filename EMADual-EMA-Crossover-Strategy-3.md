
> Name

Dual-EMA-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/44ec31093e3883ffb5fbf3bc60076d6ebfb888d4c5942e48636897cd4d0b41c6.png)

[trans]


## Overview
This strategy is a golden cross and dead cross trading strategy based on the double EMA indicator. The strategy calculates the fast EMA and the slow EMA, going long when the fast line crosses the slow line, and closing the position when the fast line crosses below the slow line. This strategy is simple and easy to implement and suitable for short- and medium-term transactions.
## Strategy Principle
This strategy is mainly implemented based on the double EMA indicator. First calculate the fast EMA and slow EMA. The fast EMA has a short period and can sensitively reflect price changes; the slow EMA has a long period and reflects the long-term trend. When the fast line crosses the slow line from below, a golden cross signal is generated, indicating that the short-term price rise is strong, and you can buy long; when the fast line crosses the slow line from above, a dead cross signal is generated, indicating that the short-term price decline is strong, and the position should be closed.
Specifically, this strategy mainly includes the following steps:
1. Enter the parameters of fast EMA and slow EMA, including SMA cycle length, data source, etc.
2. Calculate fast EMA and slow EMA
3. Define the golden cross timing: the fast line crosses the slow line from below
4. Define the timing of the dead cross: the fast line crosses the slow line from above
5. Buy and go long during the golden cross
6. Close the position when the cross occurs
7. You can choose whether to allow short selling and whether to use a stop-loss and take-profit strategy.
8. Output buying and selling message notifications
Through this simple double EMA crossover strategy, you can capture the short-term price trend and realize profits.
## Advantage Analysis
This strategy has the following advantages:
1. The strategic ideas are simple and clear, easy to understand and master.
2. Only double EMA indicators are needed, which is easy to implement.
3. You can capture the short-term price trend and obtain arbitrage profits from fluctuations.
4. The EMA cycle can be customized to flexibly adapt to market environments of different cycles.
5. You can choose whether to allow short selling and flexibly control strategic risks.
6. You can choose whether to use stop-loss and take-profit strategies to control trading risks.
7. Can output transaction notifications to facilitate monitoring.
8. The strategy is easy to optimize, and EMA parameters can be set flexibly to optimize profit margins.
## Risk Analysis
There are also some risks with this strategy:
1. The double EMA strategy is prone to generating false signals, which may lead to unnecessary losses.
2. Unreasonable setting of stop loss points may expand losses.
3. The trading frequency may be too high, increasing transaction costs and slippage risk.
4. Fixed EMA parameters cannot adapt to market changes.
5. It is easy to chase highs and sell lows, and lose calm judgment.
6. It is impossible to judge the trend reversal and may open a position in the opposite direction.
Corresponding risk management measures:
1. Optimize EMA parameters to reduce the probability of false signals.
2. Set stop loss points reasonably to control single losses.
3. Optimize the EMA cycle and reduce the trading frequency.
4. EMA parameters can be dynamically adjusted in different market stages.
5. Add trend judgment indicators to avoid chasing the rise and killing the fall.
6. Combine with trend judgment indicators to determine the direction of the general trend.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Dynamically optimize EMA parameters and use different EMA cycle combinations in different market stages to optimize parameter arbitrage effects.
2. Add stock screening conditions and conduct strategic trading on stocks that meet certain conditions to increase the success rate.
3. Combined with volatility indicators, reduce positions to avoid risks during the low volatility stage.
4. Combined with trading volume indicators, signals will be generated only when high volume can confirm the trend.
5. Set price conditions, such as breaking through the 20-day line before conducting EMA strategy trading.
6. Optimize the stop-loss strategy and set the take-profit conditions to lock in profits.
7. Increase the judgment of large-level trends and avoid opening positions against the trend.
8. Combine deep learning algorithms and various machine learning algorithms to continuously optimize strategies.
## Summarize
To sum up, the overall idea of ​​the Double EMA Golden Cross and Dead Cross strategy is simple and clear, easy to understand and implement, and can capture price fluctuations to make profits, but there are also certain profit risks. We can control risks through parameter optimization, stop-loss and take-profit, stock filtering, large-level trend judgment and other means, and steadily obtain satisfactory returns. This strategy can be continuously optimized and upgraded and deserves continuous research and improvement.
||


## Overview

This is a dual EMA crossover trading strategy based on fast EMA and slow EMA indicators. The strategy generates long signals when the fast EMA crosses above the slow EMA, and closes long positions when the fast EMA crosses below the slow EMA. The strategy is simple and practical for medium-term trading.  

## Strategy Logic

The strategy is mainly implemented with the dual EMA indicators. The fast EMA has a shorter period to sensitively reflect price changes, while the slow EMA has a longer period to indicate long term trends. 

When the fast EMA crosses above the slow EMA, a golden cross is formed, indicating upward price momentum in the short term for going long. When the fast EMA crosses below the slow EMA, a death cross is formed, showing downward momentum to close long positions.

Specifically, the strategy includes:

1. Input parameters for fast and slow EMA, including period, source etc.

2. Calculate fast EMA and slow EMA.

3. Define golden cross when fast EMA crosses above slow EMA. 

4. Define death cross when fast EMA crosses below slow EMA.

5. Go long on golden crosses.

6. Close positions on death crosses.  

7. Options for shorting and stop loss/profit taking.

8. Output buy and sell notifications.

With this simple dual EMA crossover system, the strategy can catch short-term trends for profits.

## Advantage Analysis 

The strategy has the following advantages:

1. The logic is simple and clear, easy to understand.

2. Only uses dual EMA, easy to implement. 

3. Can catch short-term trends for swing profits.

4. Customizable EMA periods for different markets.

5. Option for shorting to control risks.

6. Option for stop loss/profit taking. 

7. Buy/sell notifications for monitoring.

8. Easy to optimize EMA parameters for better profits.

## Risk Analysis

There are also some risks:

1. Dual EMA may generate false signals causing unnecessary losses.

2. Improper stop loss setting may magnify losses.

3. High trading frequency increases costs and slippage risks.

4. Fixed EMA parameters cannot adapt to market changes.

5. Prone to chasing momentum, lose calm judgement. 

6. Cannot identify trend reversal, may open reverse positions.

Corresponding risk management measures:

1. Optimize EMA parameters to reduce false signals.

2. Set proper stop loss to limit per trade loss.

3. Optimize EMA periods to reduce frequency.

4. Adjust EMA dynamically for different market stages.

5. Add trend indicators to avoid chasing momentum. 

6. Identify major trend direction with trend tools.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Dynamic optimization of EMA parameters for different markets.

2. Add stock filters to improve accuracy. 

3. Incorporate volatility index to reduce position in low volatility environments.

4. Add volume confirmation for signals.

5. Set price levels, like 20SMA breakout before taking signals.

6. Improve stop loss and take profit strategies. 

7. Add analysis of major trend to avoid trading against trend. 

8. Continuously optimize the strategy with machine learning algorithms.

## Summary

In summary, the dual EMA crossover strategy has simple and clear logic for capturing short-term trends, but also has some profit risks. We can manage risks by optimizing parameters, implementing stop loss/profit taking, filtering stocks, judging major trends etc, to steadily obtain satisfactory returns. The strategy can be incrementally improved with continuous research and enhancements.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Fast MA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|3|Fast MA Period|
|v_input_3_close|0|Slow MA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|9|Slow MA Period|
|v_input_5|false|Allow Shorting?|
|v_input_6|false|Use Initial Stop Loss?|
|v_input_7|25|Initial Stop Loss Points|
|v_input_8|false|Use Trailing Stop?|
|v_input_9|120|Trail Points|
|v_input_10|false|Use Offset For Trailing Stop?|
|v_input_11|20|Trail Offset Points|
|v_input_12|Buy message|Buy Alert Message|
|v_input_13|Sell message|Sell Alert Message|
|v_input_14|timestamp(2021-01-01T00:00:00)|startDate|
|v_input_15|timestamp(2021-12-31T00:00:00)|finishDate|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-15 00:00:00
end: 2023-10-15 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

strategy("EMA Strategy", shorttitle="EMA Strategy", overlay=true, pyramiding=0, default_qty_type=strategy.percent_of_equity, default_qty_value=100)


// === Inputs ===
// short ma
maFastSource = input(defval=close, title="Fast MA Source")
maFastLength = input(defval=3, title="Fast MA Period", minval=1)

// long ma
maSlowSource = input(defval=close, title="Slow MA Source")
maSlowLength = input(defval=9, title="Slow MA Period", minval=1)

// invert trade direction
shorting = input(defval=false, title="Allow Shorting?")
// risk management
useStop = input(defval=false, title="Use Initial Stop Loss?")
slPoints = input(defval=25, title="Initial Stop Loss Points", minval=1)
useTS = input(defval=false, title="Use Trailing Stop?")
tslPoints = input(defval=120, title="Trail Points", minval=1)
useTSO = input(defval=false, title="Use Offset For Trailing Stop?")
tslOffset = input(defval=20, title="Trail Offset Points", minval=1)

// Messages for buy and sell
message_buy  = input("Buy message", title="Buy Alert Message")
message_sell   = input("Sell message", title="Sell Alert Message")

// Calculate start/end date and time condition
startDate  = input(timestamp("2021-01-01T00:00:00"), type = input.time)
finishDate = input(timestamp("2021-12-31T00:00:00"), type = input.time)
 
time_cond  = true

// === Vars and Series ===
fastMA = ema(maFastSource, maFastLength)
slowMA = ema(maSlowSource, maSlowLength)

plot(fastMA, color=color.blue)
plot(slowMA, color=color.purple)

goLong() =>
    crossover(fastMA, slowMA)
killLong() =>
    crossunder(fastMA, slowMA)
strategy.entry("Buy", strategy.long, when=goLong() and time_cond, alert_message = message_buy)
strategy.close("Buy", when=killLong() and time_cond, alert_message = message_sell)

// Shorting if using
if shorting
    strategy.entry("Sell", strategy.short, when=killLong() and time_cond, alert_message = message_sell)
    strategy.close("Sell", when=goLong() and time_cond, alert_message = message_buy)

if useStop
    strategy.exit("XLS", from_entry="Buy", stop=strategy.position_avg_price / 1.08)
    strategy.exit("XSS", from_entry="Sell", stop=strategy.position_avg_price * 1.08)


```

> Detail

https://www.fmz.com/strategy/429389

> Last Modified

2023-10-16 16:15:38
