
> Name

Dynamic-EMA-Crossover-with-Adaptive-Swing-High-Low-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8c15d0102ba398e0fae.png)
![IMG](https://www.fmz.com/upload/asset/2d8645bad6d73bdc7f953.png)




[trans]
#### Overview
This strategy is a trading system based on 22-period exponential moving average (EMA) crossover signals and swing points. It generates trading signals through the intersection of price and EMA, and uses adaptive swing highs and lows to set take-profit and stop-loss positions. This method not only ensures the basic function of trend tracking, but also increases the flexibility of risk management.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. Use the 22-period EMA as the main trend indicator. This period can better filter out market noise.
2. When the closing price crosses above the EMA, a long signal is triggered, and when the closing price crosses below, a short signal is triggered.
3. Calculate swing highs and lows from 14-period historical data
4. For long trades, use the latest swing high as the take-profit target and the swing low as the stop-loss level.
5. For short trades, use the recent swing low as your take-profit target and the swing high as your stop-loss level.
#### Strategic Advantages
1. Strong trend adaptability: The 22-period EMA can effectively capture the mid-term trend and avoid excessively frequent trading.
2. Dynamic risk management: Take-profit and stop-loss points will be automatically adjusted according to market fluctuations, improving the adaptability of the strategy.
3. Clear execution: The trading signals are clear and there is no fuzzy area of judgment.
4. Reasonable risk-return ratio: The stop-profit and stop-loss settings set at swing points ensure that the risk-return ratio of each transaction is relatively stable.
5. Good visualization: The strategy provides clear visual signals for traders to understand and monitor.
#### Strategy Risk
1. Risk of volatile market: Frequent false breakthrough signals may occur in a volatile market.
2. Slippage risk: During periods of severe volatility, the actual transaction price may deviate greatly from the signal price.
3. Gap risk: A market gap may cause stop loss to be ineffective, resulting in unexpected losses.
4. Trend turning risk: Continuous losses may occur near major trend turning points
#### Strategy optimization direction
1. Introducing trading volume indicators: the reliability of signals can be confirmed through trading volume
2. Add trend filter: combine with longer period moving average to filter out counter-trend signals
3. Optimize the stop loss method: You can consider using ATR to dynamically adjust the stop loss distance
4. Add time filtering: prohibit opening positions during specific time periods to avoid periods of greater volatility
5. Develop signal confirmation mechanism: combine with other technical indicators as signal confirmation to improve winning rate
#### Summary
This is a trend following strategy with complete structure and clear logic. Generate trading signals through EMA crossovers and use swing points to manage risks, forming a balanced trading system. The main advantage of the strategy lies in its ability to dynamically adapt to the market, while the main risk comes from sudden changes in market conditions. Through the suggested optimization direction, the stability and profitability of the strategy are expected to be further improved. ||
#### Overview
This strategy is a trading system based on the 22-period Exponential Moving Average (EMA) crossover signals and swing points. It generates trading signals through price-EMA crossovers and utilizes adaptive swing highs and lows for setting profit targets and stop losses. This approach ensures both trend-following functionality and flexible risk management.

#### Strategy Principles
The core logic includes several key elements:
1. Uses 22-period EMA as the main trend indicator, effectively filtering market noise
2. Triggers long signals when price closes above EMA, and short signals when below
3. Calculates swing highs and lows using 14-period historical data
4. Sets profit targets at recent swing highs and stop losses at swing lows for long trades
5. Sets profit targets at recent swing lows and stop losses at swing highs for short trades

#### Strategy Advantages
1. Strong trend adaptability: 22-period EMA effectively captures medium-term trends, avoiding excessive trading
2. Dynamic risk management: Profit targets and stop losses automatically adjust to market volatility
3. Clear execution: Trading signals are unambiguous with no grey areas
4. Reasonable risk-reward ratio: Swing points ensure relatively stable risk-reward ratios for each trade
5. Good visualization: Strategy provides clear visual signals for easy monitoring and understanding

#### Strategy Risks
1. Choppy market risk: May generate frequent false breakout signals in ranging markets
2. Slippage risk: Actual execution prices may significantly deviate from signal prices during volatile periods
3. Gap risk: Market gaps may render stops ineffective, causing unexpected losses
4. Trend reversal risk: May experience consecutive losses near major trend reversal points

#### Optimization Directions
1. Incorporate volume indicators: Can confirm signal reliability through volume analysis
2. Add trend filters: Combine with longer-period moving averages to filter counter-trend signals
3. Optimize stop loss methodology: Consider using ATR for dynamic stop loss adjustment
4. Implement time filters: Restrict trading during highly volatile periods
5. Develop signal confirmation mechanism: Integrate other technical indicators for signal confirmation

#### Summary
This is a well-structured trend-following strategy with clear logic. It generates trading signals through EMA crossovers and manages risk using swing points, forming a balanced trading system. The strategy's main advantage lies in its ability to dynamically adapt to market conditions, while its primary risks come from sudden market state changes. Through the suggested optimization directions, the strategy's stability and profitability can be further enhanced.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-21 00:00:00
end: 2025-02-18 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © GlenMabasa

//@version=6
strategy("22 EMA Crossover Strategy", overlay=true)

// Input for the EMA length
ema_length = input.int(22, title="EMA Length")

// Calculate the 22-day Exponential Moving Average
ema_22 = ta.ema(close, ema_length)

// Plot the 22 EMA
plot(ema_22, color=color.blue, title="22 EMA")

// Buy condition: Price crosses and closes above the 22 EMA
buy_condition = ta.crossover(close, ema_22) and close > ema_22

// Sell condition: Price crosses or closes below the 22 EMA
sell_condition = ta.crossunder(close, ema_22) or close < ema_22

// Swing high and swing low calculations
swing_high_length = input.int(14, title="Swing High Lookback")
swing_low_length = input.int(14, title="Swing Low Lookback")
swing_high = ta.highest(high, swing_high_length) // Previous swing high
swing_low = ta.lowest(low, swing_low_length)    // Previous swing low

// Profit target and stop loss for buys
buy_profit_target = swing_high
buy_stop_loss = swing_low

// Profit target and stop loss for sells
sell_profit_target = swing_low
sell_stop_loss = swing_high

// Plot buy and sell signals
plotshape(series=buy_condition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=sell_condition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// Strategy logic for backtesting
if (buy_condition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit/Stop Loss", "Buy", limit=buy_profit_target, stop=buy_stop_loss)

if (sell_condition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit/Stop Loss", "Sell", limit=sell_profit_target, stop=sell_stop_loss)
```

> Detail

https://www.fmz.com/strategy/482870

> Last Modified

2025-02-27 17:32:58
