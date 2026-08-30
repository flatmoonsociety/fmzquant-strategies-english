
> Name

Multi-Trend-Breakout-Momentum-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/1675a0bc0924002504f93ca8d4c9257288058b8947e6f78d9bf70e6431e8c405.png)
![IMG](assets/images/232789c2fdf0f9acbce148668696230818db44a5c8afbd77c9fdfb63405758ff.png)






[trans]
#### Overview
This strategy is a trend tracking system that combines multiple indicators. It mainly captures market trend opportunities by identifying price breakthroughs, volume confirmation and the cooperation of the moving average system. The strategy identifies trading signals by monitoring price breakouts of recent highs/lows, significant volume amplification, and alignment of multiple exponential moving averages (EMAs). At the same time, the strategy also includes an innovative narrow-range consolidation identification mechanism to capture potential short-selling opportunities.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Price Breakout System: Monitor price breakouts of the past 20 period highs/lows
2. Trading volume confirmation: The trading volume at the time of breakthrough is required to be at least twice the average trading volume in the past 20 periods.
3. Moving average system: Use the 30/50/200 period EMA to build a trend confirmation system
4. Long conditions: price breaks new highs, trading volume increases, price stands above 200EMA, short-term moving average is above mid-term moving average and mid-term moving average is above long-term moving average
5. Short selling conditions: including two entry mechanisms:
   - Traditional breakthrough short selling: the price breaks new lows, trading volume increases, the moving averages are arranged in a short position and the 200EMA slopes downwards
   - Narrow consolidation and short selling: the price forms a narrow consolidation below the mid-term moving average, and the consolidation range is less than 0.5 times of ATR.
#### Strategic Advantages
1. Multiple confirmation mechanism: improve signal reliability through triple confirmation of price breakthrough, trading volume and moving average
2. Flexible short-selling mechanism: Provides two independent short-selling entry methods to increase trading opportunities
3. Strong adaptability: ATR is used to define narrow consolidation, so that the strategy can adapt to different market fluctuation environments.
4. Improved risk control: Use 200EMA as a stop loss reference to provide a clear exit mechanism
5. Parameter adjustability: key parameters can be optimized according to different market characteristics
#### Strategy Risk
1. Risk of false breakthrough: The market may have a false breakthrough, resulting in false signals
2. Risk of slippage: At the moment of breakthrough when trading volume increases sharply, you may face larger slippage.
3. Trend reversal risk: In a strong trending market, using moving average stop loss may lead to premature exit
4. Parameter sensitivity: Strategy performance is more sensitive to parameter settings and needs to be optimized carefully.
5. Dependence on market environment: Frequent false signals may occur in volatile markets
#### Strategy optimization direction
1. Introduce trend strength filtering: you can add trend strength indicators such as ADX to filter signals in weak trend environments
2. Optimize the stop loss mechanism: dynamic stop loss based on ATR can be introduced to improve the flexibility of stop loss
3. Improve position management: dynamically adjust position size based on breakthrough intensity and market volatility
4. Add time filtering: Add intraday time filtering to avoid trading during the opening and closing periods with high volatility
5. Introduce market environment classification: dynamically adjust strategy parameters according to different market environments (trends/shocks)
#### Summary
The Multiple Trend Breakout Momentum Trading Strategy is a comprehensive trend tracking system that uses multiple technical indicators to ensure signal reliability while providing flexible trading opportunities. The innovation of the strategy is that it combines traditional breakthrough trading methods with a new narrow-range consolidation identification mechanism, making it adaptable to different market environments. Although there are certain risks, through reasonable parameter optimization and risk management measures, the strategy is expected to achieve stable performance in trending markets.  ||
#### Overview
This strategy is a comprehensive trend-following system that combines multiple indicators to capture market trend opportunities through price breakouts, volume confirmation, and EMA alignment. The strategy monitors price breakouts of recent highs/lows, significant volume increases, and the arrangement of multiple Exponential Moving Averages (EMAs). It also includes an innovative narrow consolidation detection mechanism for capturing potential short opportunities.

#### Strategy Principles
The core logic of the strategy is based on the following key elements:
1. Price Breakout System: Monitors price breakouts above/below the highs/lows of the past 20 periods
2. Volume Confirmation: Requires breakout volume to be at least 2x the 20-period average volume
3. EMA System: Uses 30/50/200 period EMAs to build a trend confirmation framework
4. Long Conditions: Price breaks new high, volume increases, price above 200EMA, short-term EMA above medium-term EMA, and medium-term EMA above long-term EMA
5. Short Conditions: Includes two entry mechanisms:
   - Traditional Breakout Short: Price breaks new low, volume increases, bearish EMA alignment with downward sloping 200EMA
   - Narrow Consolidation Short: Price forms a narrow consolidation below medium-term EMA, with range less than 0.5x ATR

#### Strategy Advantages
1. Multiple Confirmation Mechanism: Enhances signal reliability through price breakout, volume, and EMA triple confirmation
2. Flexible Short Entry: Provides two independent short entry methods, increasing trading opportunities
3. Strong Adaptability: Uses ATR to define narrow consolidation, allowing adaptation to different market volatility environments
4. Robust Risk Control: Uses 200EMA as stop-loss reference, providing clear exit mechanisms
5. Parameter Adjustability: Key parameters can be optimized for different market characteristics

#### Strategy Risks
1. False Breakout Risk: Markets may exhibit false breakouts leading to incorrect signals
2. Slippage Risk: Significant slippage may occur during high-volume breakout moments
3. Trend Reversal Risk: Using EMA-based stops may lead to premature exits in strong trend markets
4. Parameter Sensitivity: Strategy performance is sensitive to parameter settings, requiring careful optimization
5. Market Environment Dependency: May generate frequent false signals in ranging markets

#### Strategy Optimization Directions
1. Introduce Trend Strength Filtering: Add indicators like ADX to filter signals in weak trend environments
2. Optimize Stop-Loss Mechanism: Implement ATR-based dynamic stops for more flexible risk management
3. Improve Position Management: Dynamically adjust position sizes based on breakout strength and market volatility
4. Add Time Filtering: Implement intraday time filters to avoid trading during volatile opening and closing periods
5. Incorporate Market Environment Classification: Dynamically adjust strategy parameters based on different market conditions (trending/ranging)

#### Summary
The Multi-Trend Breakout Momentum Trading Strategy is a comprehensive trend-following system that ensures signal reliability while providing flexible trading opportunities through the combination of multiple technical indicators. The strategy innovates by combining traditional breakout trading methods with a new narrow consolidation detection mechanism, making it adaptable to different market environments. While certain risks exist, the strategy has the potential to achieve stable performance in trending markets through proper parameter optimization and risk management measures.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-21 00:00:00
end: 2025-02-18 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Breakout Strategy (Long & Short) + Slope of 200 EMA", overlay=true)

// -------------------
// 1. Settings
// -------------------
breakout_candles = input.int(20, title="Number of Candles for Breakout")
range_candles    = input.int(10, title="Number of Candles for Previous Range")

ema_long_period   = input.int(200, title="Long EMA Period")
ema_medium_period = input.int(50,  title="Medium EMA Period")
ema_short_period  = input.int(30,  title="Short EMA Period")

// Checkbox to allow/disallow short positions
allowShort = input.bool(true, title="Allow Short Positions")

// Inputs for the new Narrow Consolidation Short setup
consolidationBars     = input.int(10,   "Consolidation Bars",   minval=1)
narrowThreshInAtr     = input.float(0.5,"Narrowness (ATR Mult.)",minval=0.0)
atrLength             = input.int(14,   "ATR Length for Range")

// -------------------
// 2. Calculations
// -------------------
breakout_up   = close > ta.highest(high, breakout_candles)[1]
breakout_down = close < ta.lowest(low,  breakout_candles)[1]

prev_range_high = ta.highest(high, range_candles)[1]
prev_range_low  = ta.lowest(low,  range_candles)[1]

ema_long   = ta.ema(close, ema_long_period)
ema_medium = ta.ema(close, ema_medium_period)
ema_short  = ta.ema(close, ema_short_period)

average_vol      = ta.sma(volume, breakout_candles)
volume_condition = volume > 2 * average_vol

// 200 EMA sloping down?
ema_long_slope_down = ema_long < ema_long[1]

// For the Narrow Consolidation Short
rangeHigh   = ta.highest(high, consolidationBars)
rangeLow    = ta.lowest(low,  consolidationBars)
rangeSize   = rangeHigh - rangeLow

atrValue    = ta.atr(atrLength)

// Condition: Price range is "narrow" if it's less than (ATR * threshold)
narrowConsolidation = rangeSize < (atrValue * narrowThreshInAtr)

// Condition: All bars under Medium EMA if the highest difference (high - ema_medium) in last N bars is < 0
allBelowMedium = ta.highest(high - ema_medium, consolidationBars) < 0

// -------------------
// 3. Long Entry
// -------------------
breakout_candle_confirmed_long = ta.barssince(breakout_up) <= 3

long_condition = breakout_candle_confirmed_long
     and volume_condition
     and close > prev_range_high
     and close > ema_long
     and ema_short > ema_medium
     and ema_medium > ema_long
     and strategy.opentrades == 0

if long_condition
    strategy.entry("Long", strategy.long)

// -------------------
// 4. Short Entries
// -------------------

// (A) Original breakout-based short logic
breakout_candle_confirmed_short = ta.barssince(breakout_down) <= 3
short_condition_breakout = breakout_candle_confirmed_short
     and volume_condition
     and close < prev_range_low
     and close < ema_long
     and ema_short < ema_medium
     and ema_medium < ema_long
     and ema_long_slope_down
     and strategy.opentrades == 0

// (B) NEW: Narrow Consolidation Short
short_condition_consolidation = narrowConsolidation
     and allBelowMedium
     and strategy.opentrades == 0

// Combine them: if either short scenario is valid, go short
short_condition = (short_condition_breakout or short_condition_consolidation) and allowShort

if short_condition
    // Use a different order ID if you want to distinguish them
    // but "Short" is fine for a single position
    strategy.entry("Short", strategy.short)

// -------------------
// 5. Exits
// -------------------
if strategy.position_size > 0 and close < ema_long
    strategy.close("Long", qty_percent=100)

if strategy.position_size < 0 and close > ema_long
    strategy.close("Short", qty_percent=100)

// ======================================================================
// 5. ADDITIONAL PARTIAL EXITS / STOPS
// ======================================================================
// You can add partial exits for shorts or longs similarly.
// For example:
// if strategy.position_size < 0 and close > stop_level_for_short
//     strategy.close("Short", qty_percent=50)
```

> Detail

https://www.fmz.com/strategy/482819

> Last Modified

2025-02-20 14:53:56
