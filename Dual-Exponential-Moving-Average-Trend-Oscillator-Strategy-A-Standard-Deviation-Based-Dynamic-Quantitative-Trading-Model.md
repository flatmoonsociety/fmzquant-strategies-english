
> Name

Dual-Exponential-Moving-Average-Trend-Oscillator-Strategy-A-Standard-Deviation-Based-Dynamic-Quantitative-Trading-Model
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d81a0f4dc7f81159b455.png)
![IMG](https://www.fmz.com/upload/asset/2d90daaa4bf73b99869ad.png)



[trans]

# Overview
The Double Exponential Moving Average Trend Oscillator strategy is a dynamic trend following method based on the standardized DEMA oscillator and standard deviation bands. The strategy adapts to market volatility in real time and is designed to improve entry accuracy and optimize risk management. The core mechanism is to visually identify the trend strength by normalizing the DEMA value to the 0-100 range, and combine it with the double-bar confirmation filter and the ATR multiple tracking stop to improve the reliability and profitability of the strategy. This is a comprehensive quantitative trading system that works across a variety of market conditions, especially for traders looking for consistent performance in trending markets.
#### Strategy Principle
The core logic of the Double Exponential Moving Average Trend Oscillator strategy is based on the fusion of multi-layer technical indicators:
1. Double Exponential Moving Average (DEMA) calculation: implemented through the function F_DEMA, the formula is 2 * E1 - E2, where E1 is the EMA of the price, and E2 is the EMA of E1. This calculation method reduces latency and makes the indicator more sensitive to price changes.
2. Standardization process: The strategy uses BASE (SMA of DEMA) and SD (standard deviation of DEMA multiplied by 2) to create upper and lower fluctuation bands (upperSD and lowerSD). The DEMA values ​​are then normalized to the range of 0-100 via the formula NormBase = 100 * (DEMA - lowerSD)/(upperSD - lowerSD).
3. Admission conditions:
   - Long entry: when NormBase > 55 and the candle low is above the upper SD band, while the previous candle formed a bullish pattern
   - Short entry: when NormBase < 45 and the candle high is below the lower SD band, while the previous candle formed a bearish pattern
4. Risk management: The strategy adopts a triple exit mechanism - a fixed stop loss located at the SD band, a dynamic take profit set at a risk-reward ratio of 1.5 times, and a trailing stop loss based on ATR (default is 2 times ATR).
5. Transaction direction control: Use the lastDirection variable to ensure that there will be no consecutive entries in the same direction, improving the efficiency of capital use.
The code implements parameter adjustability, allowing traders to optimize for different market conditions and personal risk preferences.
#### Strategic Advantages
Through an in-depth analysis of the code, the Double Exponential Moving Average Trend Oscillator strategy demonstrates several advantages:
1. Reduce signal delay: DEMA itself has lower lag than traditional EMA and SMA, responds faster to price changes, and combined with standardized processing, makes trend identification more timely and accurate.
2. Intelligent filtering mechanism: requires two consecutive bullish or bearish candles as confirmation, significantly reducing market noise and reducing the possibility of false signals.
3. Adaptive fluctuation band: Dynamically adjust the width of the fluctuation band through the standard deviation, so that the strategy can automatically adapt to different market fluctuation conditions, shrinking during low volatility and expanding during high volatility.
4. Multi-layer risk management: A triple protection mechanism that combines fixed stop loss, risk-reward ratio take-profit and ATR trailing stop-loss, which not only protects the safety of funds, but also maximizes returns in strong trends.
5. Visual intuitiveness: The strategy displays upper and lower SD fluctuation bands and entry signal arrows on the chart, allowing traders to intuitively understand the market status and strategy logic.
6. Parameter flexibility: All core parameters can be adjusted, including DEMA period, baseline length, entry threshold and risk management settings, allowing the strategy to adapt to different trading varieties and time frames.
7. Clear code structure: The strategy implementation is concise and clear, easy to understand and follow-up optimization, and lowers the technical threshold for strategy implementation.
#### Strategy Risk
Although this strategy is well designed, there are still several risks worth noting:
1. Poor performance in volatile markets: As a trend following strategy, frequent false signals may be generated in consolidating markets with no obvious trend, resulting in continuous small losses. The solution is to add a trend strength filter or pause trading when a consolidating market is identified.
2. Parameter sensitivity: Strategy performance is highly sensitive to parameters such as DEMA period, entry threshold and SD multiplier. Improper parameter settings may lead to overfitting or slow response. It is recommended to verify parameter robustness through backtesting over multiple market cycles.
3. Stop loss pressure: In highly volatile markets, a fixed stop loss located relatively close to the SD band may result in being triggered during normal price fluctuations. Consider dynamically adjusting the stop loss distance based on market volatility.
4. Direction conversion delay: Because the strategy uses the lastDirection variable to control the trading direction, important reverse signals may be missed in violent reversal markets. Consider adding a trend reversal detection mechanism.
5. Fund management risk: The code uses the account equity percentage (100%) by default for position management, which is too aggressive for real trading. This value should be lowered according to personal risk tolerance, and it is recommended not to exceed 5-10%.
6. Execution delays: In actual trading, order execution delays and slippage may cause the entry price to deviate from ideal conditions. It is recommended to include more realistic slippage settings in backtesting (2 points of slippage are included) and consider using limit orders instead of market orders.
#### Strategy optimization direction
Based on code analysis, the strategy can be further optimized in the following directions:
1. Market environment adaptation: Introduce market type identification mechanisms, such as ADX or volatility benchmarks, to automatically adjust thresholds or suspend trading in low-trend markets, thereby avoiding frequent losses in volatile markets.
2. Dynamic parameter optimization: Realize dynamic adjustment of DEMA cycle and threshold, automatically optimize parameters according to the market fluctuation characteristics of different time frames, and improve strategy adaptability.
3. Multi-time frame confirmation: Add trend confirmation of higher time frames, only enter the market when it is consistent with the trend of higher time frames, and improve signal quality and winning rate.
4. Improve exit mechanisms: The current fixed risk-reward ratio may not be suitable for all market conditions. Consider smart take-profit strategies based on support and resistance levels, volatility percentages, or dynamic targets.
5. Position size optimization: Introduce dynamic position adjustment based on volatility, increase positions in low-volatility and high-certainty environments, reduce positions in high-volatility environments, and optimize the smoothness of the capital curve.
6. Enhanced filtering mechanism: In addition to double-bar confirmation, transaction volume confirmation, price pattern identification or key price breakthrough confirmation can be added to further reduce false signals.
7. Sentiment indicator integration: Consider integrating market sentiment indicators such as RSI or MACD divergence to identify potential trend weakness or reversal signals to improve the predictability of the strategy.
8. Backtest robustness: Extend the backtest interval across different market environments, and implement step optimization to verify parameter stability and avoid overfitting to specific market cycles.
The above optimizations help improve the robustness, adaptability and long-term profitability of the strategy, especially in the face of different market conditions.
#### Summarize
The Double Exponential Moving Average Trend Oscillator strategy is a well-designed quantitative trading system that creates a solution that balances response speed and signal accuracy by fusing the DEMA technical indicator, standard deviation swing bands, and ATR trailing stops. Its core advantage lies in its ability to adapt to market fluctuations and its multi-layered risk management mechanism, allowing the strategy to perform well in trending markets.
Through double-bar confirmation filtering and standardization processing, this strategy effectively reduces false signals and improves entry accuracy. At the same time, the triple exit mechanism ensures that profit potential is maximized while protecting funds. The strategy's visual elements and clear code structure make it easy to understand and operate, making it suitable for traders of all experience levels.
Although this strategy may face challenges in volatile markets, its adaptability and robustness can be further enhanced through the recommended optimization directions, especially market environment identification and multi-time frame confirmation. Ultimately, the Dual Exponential Moving Average Trend Oscillator strategy provides a solid framework that traders can customize and adjust based on personal risk appetite and market conditions to achieve consistent trading performance over the long term. ||
# Overview

The Dual Exponential Moving Average Trend Oscillator Strategy is a dynamic trend-following approach based on the Normalized DEMA Oscillator and Standard Deviation bands. It adapts in real-time to market volatility with the goal of improving entry accuracy and optimizing risk management. The core mechanism involves normalizing DEMA values on a 0-100 scale for intuitive identification of trend strength, combined with a two-bar confirmation filter and ATR-multiple trailing stops to enhance reliability and profitability. This is a comprehensive quantitative trading system suitable for various market conditions, particularly for traders seeking consistent performance in trending markets.

#### Strategy Principles

The Dual Exponential Moving Average Trend Oscillator Strategy's core logic is built on multiple layers of technical indicators:

1. Dual Exponential Moving Average (DEMA) calculation: Implemented through the F_DEMA function with the formula 2 * E1 - E2, where E1 is the EMA of price and E2 is the EMA of E1. This calculation method reduces lag, making the indicator more responsive to price movements.

2. Normalization process: The strategy uses BASE (SMA of DEMA) and SD (standard deviation of DEMA multiplied by 2) to create upper and lower bands (upperSD and lowerSD). Subsequently, DEMA values are normalized to a 0-100 range using the formula NormBase = 100 * (DEMA - lowerSD)/(upperSD - lowerSD).

3. Entry conditions:
   - Long entry: When NormBase > 55 and the candle low is above the upper SD band, with the previous candle forming a bullish pattern
   - Short entry: When NormBase < 45 and the candle high is below the lower SD band, with the previous candle forming a bearish pattern

4. Risk management: The strategy employs a triple exit mechanism - fixed stop-loss at the SD band, dynamic take-profit set at a risk-reward ratio of 1.5, and an ATR-based trailing stop (default at 2x ATR).

5. Trade direction control: The lastDirection variable ensures no consecutive entries in the same direction, improving capital efficiency.

The code implements parameter adjustability, allowing traders to optimize based on different market conditions and individual risk preferences.

#### Strategy Advantages

Through in-depth code analysis, the Dual Exponential Moving Average Trend Oscillator Strategy demonstrates multiple advantages:

1. Reduced signal lag: DEMA itself has lower lag than traditional EMA and SMA, responding faster to price movements. With normalization processing, trend identification becomes more timely and accurate.

2. Intelligent filtering mechanism: Requiring two consecutive bullish or bearish candles for confirmation significantly reduces market noise and the possibility of false signals.

3. Adaptive volatility bands: The standard deviation dynamically adjusts band width, enabling the strategy to automatically adapt to different market volatility conditions, contracting during low volatility and expanding during high volatility.

4. Multi-layered risk management: The triple protection mechanism combining fixed stop-loss, risk-reward ratio take-profit, and ATR trailing stop both protects capital safety and maximizes returns in strong trends.

5. Visual intuitiveness: The strategy displays upper and lower SD bands and entry signal arrows on the chart, allowing traders to visually understand market conditions and strategy logic.

6. Parameter flexibility: All core parameters are adjustable, including DEMA period, base length, entry thresholds, and risk management settings, making the strategy adaptable to different trading instruments and timeframes.

7. Clear code structure: The strategy implementation is concise and easy to understand, facilitating subsequent optimization and lowering the technical barrier to strategy implementation.

#### Strategy Risks

Despite its well-designed structure, several noteworthy risks exist:

1. Poor performance in ranging markets: As a trend-following strategy, it may generate frequent false signals in consolidating markets without clear trends, leading to consecutive small losses. The solution is to add a trend strength filter or pause trading when ranging markets are identified.

2. Parameter sensitivity: Strategy performance is highly sensitive to parameters such as DEMA period, entry thresholds, and SD multiplier. Inappropriate parameter settings may lead to overfitting or slow response. It's recommended to validate parameter robustness through backtesting across multiple market cycles.

3. Stop-loss pressure: In highly volatile markets, fixed stop-loss at the SD band may be relatively close, triggering during normal price fluctuations. Consider dynamically adjusting stop-loss distance based on market volatility.

4. Direction change delay: As the strategy uses the lastDirection variable to control trade direction, it may miss important reversal signals in rapidly reversing markets. Consider adding a trend reversal detection mechanism.

5. Capital management risk: The code defaults to using account equity percentage (100%) for position sizing, which is too aggressive for live trading. This value should be adjusted according to personal risk tolerance, preferably not exceeding 5-10%.

6. Execution delay: In actual trading, order execution delays and slippage may cause entry prices to deviate from ideal conditions. It's advisable to include more realistic slippage settings in backtesting (2 pips slippage is already included) and consider using limit orders instead of market orders.

#### Strategy Optimization Directions

Based on code analysis, the strategy can be further optimized in the following directions:

1. Market environment adaptation: Introduce market type recognition mechanisms, such as ADX or volatility benchmarks, to automatically adjust thresholds or pause trading in low-trend markets, thereby avoiding frequent losses in ranging conditions.

2. Dynamic parameter optimization: Implement dynamic adjustment of DEMA periods and thresholds, automatically optimizing parameters based on market volatility characteristics across different timeframes, improving strategy adaptability.

3. Multi-timeframe confirmation: Add higher timeframe trend confirmation, only entering when aligned with higher timeframe trends, improving signal quality and win rate.

4. Improved exit mechanism: The current fixed risk-reward ratio may not adapt to all market conditions. Consider intelligent take-profit strategies based on support/resistance levels, volatility percentages, or dynamic targets.

5. Position size optimization: Introduce volatility-based dynamic position adjustment, increasing position size in low-volatility high-certainty environments and decreasing in high-volatility environments, optimizing equity curve smoothness.

6. Enhanced filtering mechanism: In addition to two-bar confirmation, add volume confirmation, price pattern recognition, or key level breakout confirmation to further reduce false signals.

7. Sentiment indicator integration: Consider integrating market sentiment indicators such as RSI or MACD divergence to identify potential trend weakness or reversal signals, enhancing strategy predictiveness.

8. Backtesting robustness: Extend backtesting intervals across different market environments and implement walk-forward optimization to verify parameter stability, avoiding overfitting to specific market cycles.

These optimizations help improve the strategy's robustness, adaptability, and long-term profitability, especially when facing different market conditions.

#### Summary

The Dual Exponential Moving Average Trend Oscillator Strategy is a well-designed quantitative trading system that creates a solution balancing response speed and signal accuracy by integrating DEMA technical indicators, standard deviation bands, and ATR trailing stops. Its core advantages lie in its ability to adapt to market volatility and its multi-layered risk management mechanisms, enabling the strategy to excel in trending markets.

Through two-bar confirmation filtering and normalization processing, the strategy effectively reduces false signals and improves entry accuracy. Meanwhile, the triple exit mechanism ensures profit potential is maximized while protecting capital. The strategy's visualization elements and clear code structure make it easy to understand and operate, suitable for traders of all experience levels.

Although the strategy may face challenges in ranging markets, through the suggested optimization directions, particularly market environment recognition and multi-timeframe confirmation, its adaptability and robustness can be further enhanced. Ultimately, the Dual Exponential Moving Average Trend Oscillator Strategy provides a solid framework that traders can customize and adjust according to personal risk preferences and market environments to achieve long-term consistent trading performance.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-03-18 00:00:00
end: 2025-04-15 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"TRX_USD"}]
*/

// This Pine Script® code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © PakunFX

//@version=6
strategy("DEMA Trend Oscillator Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// === INPUTS ===
src_dema = input.source(close, "Calculation src_dema (Dema)")
len_dema = input.int(40, "Dema Period")
base_len = input.int(20, 'Base length')
Lu       = input.float(55, 'Long Threshold')
Su       = input.float(45, 'Short Threshold')
RR       = input.float(1.5, "Risk Reward Ratio", step=0.1)
trailATRmult = input.float(2.0, "ATR Multiplier for Trailing Stop", step=0.1)

// === FUNCTION ===
F_DEMA(SRC, LEN) =>
    E1 = ta.ema(SRC, LEN)
    E2 = ta.ema(E1, LEN)
    2 * E1 - E2

// === DEMA & NORMALIZATION ===
DEMA     = F_DEMA(src_dema, len_dema)
BASE     = ta.sma(DEMA, base_len)
SD       = ta.stdev(DEMA, base_len) * 2
upperSD  = BASE + SD
lowerSD  = BASE - SD
NormBase = 100 * (DEMA - lowerSD)/(upperSD - lowerSD)

// === ENTRY CONDITIONS ===
long_cond  = NormBase > Lu and low > upperSD
short_cond = NormBase < Su and high < lowerSD

// === DELAYED ENTRY TRIGGERS ===
long_trigger  = long_cond[1]
short_trigger = short_cond[1]

// === ATR-BASED TRAILING STOP ===
atr = ta.atr(14)
trail_offset = atr * trailATRmult
trail_points = trail_offset / syminfo.mintick

// === TRADE DIRECTION CONTROL ===
var string lastDirection = "none"

// === ENTRY LOGIC ===
if long_trigger and lastDirection != "long"
    strategy.entry("Long", strategy.long)
    strategy.exit("TP/SL/Trail Long", from_entry="Long", stop=upperSD, limit=close + (close - upperSD) * RR, trail_points=trail_points, trail_offset=trail_points)
    lastDirection := "long"

if short_trigger and lastDirection != "short"
    strategy.entry("Short", strategy.short)
    strategy.exit("TP/SL/Trail Short", from_entry="Short", stop=lowerSD, limit=close - (lowerSD - close) * RR, trail_points=trail_points, trail_offset=trail_points)
    lastDirection := "short"

```

> Detail

https://www.fmz.com/strategy/491035

> Last Modified

2025-04-18 09:19:05
