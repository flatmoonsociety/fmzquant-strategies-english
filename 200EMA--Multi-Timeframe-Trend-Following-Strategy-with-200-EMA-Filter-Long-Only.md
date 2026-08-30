
> Name

Multi-Timeframe-Trend-Following-Strategy-with-200-EMA-Filter-Long-Only
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1646738d96f1f7190d5.png)

[trans]
#### Overview
This strategy is a trend following strategy based on the multi-timeframe exponential moving average (EMA) and the 200-period EMA filter. Its main idea is to use EMAs of different time frames to identify the trend direction of the market, and to establish a long position when the trend is upward and the price is above the 200-period EMA. This ensures that you only trade in strong uptrends to capitalize on sustained gains, while using stop-loss and take-profit mechanisms to control risk.
The strategy uses three time frames of 5 minutes, 15 minutes and 30 minutes to calculate fast EMA and slow EMA respectively. By comparing the fast EMA and slow EMA of each time frame, you can determine the trend direction of that time frame. The trend signals from the three time frames are then summed to obtain a comprehensive trend signal. When the comprehensive trend signal is 3 (that is, all time frames are uptrends) and the current closing price is above the 5-minute 200-period EMA, the strategy opens a long position; when the comprehensive trend signal is less than 3 or the price falls below the 5-minute 200-period EMA, the strategy closes the position.
#### Strategy Principle
1. Calculate fast EMA (default 9 periods) and slow EMA (default 21 periods) for the 5-minute, 15-minute and 30-minute time frames respectively.
2. Calculate the 200-period EMA on the 5-minute time frame as a trend filter.
3. For each time frame, compare the size of the fast EMA and the slow EMA. If the fast EMA is above, it is an upward trend (+1), and if the slow EMA is above, it is a downward trend (-1).
4. Add the trend signals of the three time frames to obtain a comprehensive trend signal with an interval of [-3, 3].
5. When the comprehensive trend signal is equal to 3 (strong rise) and the current closing price is above the 5-minute 200-period EMA, open a long position.
6. When the comprehensive trend signal is less than 3 (the upward trend weakens) or the price falls below the 5-minute 200-period EMA, close the position.
7. When opening a position, the stop loss is set 1% below the opening price, and the take profit is set 3% above the opening price.
#### Advantage Analysis
1. By using trend signals in multiple time frames, you can judge market trends more comprehensively and reduce false signals.
2. The 200-period EMA filter can ensure that you only trade in strong upward trends and increase the success rate.
3. Strict conditions for opening and closing positions and stop-loss and take-profit can help control risks and improve the risk-return ratio.
4. The parameters are adjustable and suitable for different markets and trading styles.
#### Risk Analysis
1. The reaction may be slow at the turning point of the trend and the best opportunity to open a position will be missed.
2. Frequent opening and closing of positions may increase transaction costs.
3. The stop loss position is fixed and may be stopped early in the volatile market.
4. Trend judgment is based on historical data and may not respond promptly to price fluctuations caused by emergencies.
#### Optimization direction
1. Introduce more time frames or optimize the selection of existing time frames to improve the accuracy and timeliness of trend judgment.
2. Optimize stop loss and take profit positions, such as introducing trailing stop loss or dynamic take profit to adapt to different market conditions.
3. In addition to trend signals, other signals such as trading volume, momentum, etc. are introduced to form multi-factor opening and closing conditions and improve the robustness of the strategy.
4. Optimize the parameters and find the parameter combination that is most suitable for the current market.
5. Consider adding a short-selling mechanism to expand the scope of application.
#### Summarize
This strategy determines the trend direction by comparing EMAs of multiple time frames, and uses the 200-period EMA as a trend filter to establish a long position when the trend is clearly upward and the price is above the long-term moving average to seize the strong rising market. Strict opening and closing conditions and fixed stop-loss and take-profit help control risks. However, this strategy may respond slowly at trend turning points, and the stop-loss and take-profit positions are fixed, which has limitations in responding to sudden market fluctuations.
In the future, the adaptability and robustness of the strategy can be improved by introducing more time frames, optimizing stop loss and profit, adding more trading signals, optimizing parameters, etc., so that it can better grasp market opportunities and control risks.
|| 

#### Overview

This strategy is a trend-following strategy based on multi-timeframe Exponential Moving Averages (EMAs) and a 200-period EMA filter. The main idea is to use EMAs on different timeframes to identify the market trend direction and establish long positions when the trend is up and the price is above the 200-period EMA. This ensures that trades are only entered during strong uptrends, aiming to capture sustained upward movements while managing risk with defined stop-loss and take-profit mechanisms.

The strategy uses three timeframes: 5-minute, 15-minute, and 30-minute, calculating fast and slow EMAs for each. By comparing the fast and slow EMAs for each timeframe, the trend direction can be determined. The trend signals from the three timeframes are then summed to obtain a combined trend signal. When the combined trend signal is 3 (indicating an uptrend across all timeframes) and the current closing price is above the 200-period EMA on the 5-minute timeframe, the strategy enters a long position. The position is closed when the combined trend signal falls below 3 or the price drops below the 5-minute 200-period EMA.

#### Strategy Principles

1. Calculate the fast EMA (default 9 periods) and slow EMA (default 21 periods) for the 5-minute, 15-minute, and 30-minute timeframes.
2. Calculate the 200-period EMA on the 5-minute timeframe as a trend filter.
3. For each timeframe, compare the fast and slow EMAs. Fast above slow indicates an uptrend (+1), slow above fast indicates a downtrend (-1).
4. Sum the trend signals from the three timeframes to obtain a combined trend signal in the range [-3, 3].
5. Enter a long position when the combined trend signal equals 3 (strong uptrend) and the current closing price is above the 5-minute 200-period EMA.
6. Close the position when the combined trend signal falls below 3 (weakening uptrend) or the price drops below the 5-minute 200-period EMA.
7. Set the stop-loss 1% below the entry price and the take-profit 3% above the entry price.

#### Advantages

1. By utilizing trend signals from multiple timeframes, the strategy can more comprehensively assess the market trend and reduce false signals.
2. The 200-period EMA filter ensures that trades are only entered during strong uptrends, increasing the success rate.
3. Strict entry and exit conditions, along with stop-loss and take-profit, help control risk and improve the risk-reward ratio.
4. Adjustable parameters make the strategy adaptable to different markets and trading styles.

#### Risks

1. The strategy may react slowly at trend turning points, missing optimal entry opportunities.
2. Frequent entries and exits may increase trading costs.
3. Fixed stop-loss levels may lead to premature exits in highly volatile markets.
4. Trend determination is based on historical data and may not react promptly to sudden price movements caused by unexpected events.

#### Optimization Directions

1. Introduce more timeframes or optimize the selection of existing timeframes to improve the accuracy and timeliness of trend identification.
2. Optimize stop-loss and take-profit levels, such as implementing trailing stops or dynamic take-profits, to adapt to different market conditions.
3. Incorporate additional signals like volume, momentum, etc., alongside trend signals to form multi-factor entry and exit conditions, enhancing the strategy's robustness.
4. Optimize parameters to find the most suitable combination for the current market.
5. Consider adding a short-selling mechanism to expand the strategy's applicability.

#### Summary

This strategy determines the trend direction by comparing EMAs on multiple timeframes while using a 200-period EMA as a trend filter. It establishes long positions when the trend is clearly upward and the price is above the long-term moving average, aiming to capture strong uptrends. Strict entry and exit conditions and fixed stop-loss and take-profit levels help manage risk. However, the strategy may react slowly at trend turning points and has limitations in dealing with sudden market volatility due to fixed stop-loss and take-profit levels.
In the future, the strategy's adaptability and robustness can be improved by introducing more timeframes, optimizing stop-loss and take-profit levels, incorporating additional trading signals, optimizing parameters, etc. This will enable the strategy to better seize market opportunities while controlling risks.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-17 00:00:00
end: 2024-05-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Multi-Timeframe Trend Following with 200 EMA Filter - Longs Only", shorttitle="MTF_TF_200EMA_Longs", overlay=true, initial_capital=1000, default_qty_type=strategy.fixed, default_qty_value=1)

// Inputs
fast_length = input.int(9, title="Fast EMA Length", minval=1)
slow_length = input.int(21, title="Slow EMA Length", minval=1)
filter_length_200 = input.int(200, title="200 EMA Length", minval=1)
stop_loss_perc = input.float(1.0, title="Stop Loss Percentage", minval=0.1) / 100
take_profit_perc = input.float(3.0, title="Take Profit Percentage", minval=0.1) / 100

// Calculate EMAs for 5-minute, 15-minute, and 30-minute timeframes
ema_fast_5min = request.security(syminfo.tickerid, "5", ta.ema(close, fast_length), lookahead=barmerge.lookahead_on)
ema_slow_5min = request.security(syminfo.tickerid, "5", ta.ema(close, slow_length), lookahead=barmerge.lookahead_on)

ema_fast_15min = request.security(syminfo.tickerid, "15", ta.ema(close, fast_length), lookahead=barmerge.lookahead_on)
ema_slow_15min = request.security(syminfo.tickerid, "15", ta.ema(close, slow_length), lookahead=barmerge.lookahead_on)

ema_fast_30min = request.security(syminfo.tickerid, "30", ta.ema(close, fast_length), lookahead=barmerge.lookahead_on)
ema_slow_30min = request.security(syminfo.tickerid, "30", ta.ema(close, slow_length), lookahead=barmerge.lookahead_on)

// Calculate 200 EMA for the 5-minute timeframe
ema_200_5min = ta.ema(close, filter_length_200)

// Determine the trend for each timeframe
trend_5min = ema_fast_5min > ema_slow_5min ? 1 : -1
trend_15min = ema_fast_15min > ema_slow_15min ? 1 : -1
trend_30min = ema_fast_30min > ema_slow_30min ? 1 : -1

// Combine trend signals
combined_trend = trend_5min + trend_15min + trend_30min

// Define entry and exit conditions with 200 EMA filter
enter_long = combined_trend == 3 and close > ema_200_5min
exit_long = combined_trend < 3 or close < ema_200_5min

// Plot EMAs for the 5-minute timeframe
plot(ema_fast_5min, color=color.blue, linewidth=2, title="Fast EMA 5min")
plot(ema_slow_5min, color=color.red, linewidth=2, title="Slow EMA 5min")
plot(ema_200_5min, color=color.green, linewidth=2, title="200 EMA 5min")

// Strategy execution
if (enter_long)
    strategy.entry("Long", strategy.long, stop=close * (1 - stop_loss_perc), limit=close * (1 + take_profit_perc))
if (exit_long)
    strategy.close("Long")

```

> Detail

https://www.fmz.com/strategy/452279

> Last Modified

2024-05-23 18:07:50
