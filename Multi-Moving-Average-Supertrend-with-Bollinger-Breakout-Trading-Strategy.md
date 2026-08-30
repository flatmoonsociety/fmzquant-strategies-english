
> Name

Multi-Moving-Average-Supertrend-with-Bollinger-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13fb72bc227c431d160.png)

[trans]
#### Overview
This strategy is a compound trading system that combines multiple indicators, mainly based on the comprehensive analysis of exponential moving average (EMA), supertrend indicator (Supertrend), Bollinger Bands and relative strength indicator (RSI). The core logic of the strategy builds trading signals around EMA and Supertrend, while combining Bollinger Bands and RSI to provide auxiliary judgments on market volatility and momentum. The trading system uses a multi-period RSI analysis method, including daily, weekly and monthly cycles, to provide a more comprehensive market perspective for trading decisions.
#### Strategy Principle
The strategy uses a combination of multi-layered technical indicators to capture market trends and volatility opportunities:
1. Use triple EMA (13, 34, 100) to establish a trend tracking system and determine the trend direction through moving average crossover and position relationship.
2. Integrate Supertrend indicator as trend confirmation and stop loss reference
3. Use the ADX indicator to screen for strong trend markets, and set 25 as the trend strength threshold.
4. Use Bollinger Bands (20,2) to monitor the price fluctuation range
5. Use three-period RSI(14) to analyze the overbought and oversold state of the market
Trigger conditions for trading signals:
- Bull entry: Supertrend turns long + EMA13 crosses EMA34 + price stands above EMA100 + ADX>25
- Short entry: Supertrend turns long + EMA13 crosses EMA34 + price falls below EMA100 + ADX>25
- Position closing signal: exit the position in the corresponding direction when the price crosses Supertrend
#### Strategic Advantages
1. The integration of multiple technical indicators provides more reliable trading signals and effectively reduces false signals.
2. The triple EMA system can comprehensively grasp the trend characteristics of different periods.
3. The introduction of the ADX indicator ensures that you only trade in strong trending markets
4. Multi-period RSI analysis provides a more comprehensive assessment of market momentum
5. The Supertrend indicator provides an objective reference for stop loss positions.
6. The integration of Bollinger Bands helps determine market fluctuations and potential breakthrough opportunities
#### Strategy Risk
1. Multiple indicator systems may cause signal lag and affect entry timing.
2. Frequent false breakthrough signals may occur in volatile markets
3. The fixed ADX threshold may perform inconsistently in different market environments.
4. Rapid and severe market fluctuations may result in unreasonable stop loss positions.
Risk control suggestions:
- Dynamically adjust ADX threshold according to different market characteristics
- Introducing a volatility adaptive stop-loss mechanism
- Added volume analysis as signal confirmation
#### Strategy optimization direction
1. Optimization of indicator parameters
- Consider introducing adaptive EMA periods
- Dynamically adjust the Supertrend coefficient based on volatility
- Optimize Bollinger Band parameters to adapt to different market stages
2. Signal system enhancement
- Integrate volume factors to verify trading signals
- Added market structure analysis
- Introduced volatility filter
3. Improved risk management
- Design dynamic stop loss mechanism
- Establish a warehouse management system
- Added transaction time filter
#### Summary
This strategy builds a relatively complete trading system through the organic combination of multiple technical indicators. The cooperation of EMA and Supertrend provides main trading signals, ADX screening ensures that trading occurs in a strong trend environment, and the auxiliary analysis of Bollinger Bands and RSI provides additional market perspectives. The main advantage of the strategy is signal reliability and system integrity, but it also faces challenges of signal lag and parameter optimization. Through the proposed optimization direction, the strategy is expected to improve profitability while maintaining stability. ||
#### Overview
This strategy is a comprehensive trading system that combines multiple indicators, primarily based on Exponential Moving Averages (EMA), Supertrend indicator, Bollinger Bands (BB), and Relative Strength Index (RSI). The core logic builds trading signals around EMA and Supertrend, while incorporating BB and RSI for supplementary analysis of market volatility and momentum. The system employs multi-timeframe RSI analysis, including daily, weekly, and monthly periods, providing a more comprehensive market perspective for trading decisions.

#### Strategy Principles
The strategy utilizes a multi-layer technical indicator combination to capture market trends and volatility opportunities:
1. Uses triple EMA (13,34,100) to establish a trend-following system, determining trend direction through crossovers and relative positions
2. Integrates Supertrend indicator for trend confirmation and stop-loss reference
3. Employs ADX indicator to filter strong trends, setting 25 as the trend strength threshold
4. Utilizes Bollinger Bands (20,2) to monitor price volatility range
5. Implements triple-timeframe RSI (14) to analyze market overbought/oversold conditions

Trading signal triggers:
- Long Entry: Supertrend turns bullish + EMA13 crosses above EMA34 + price above EMA100 + ADX>25
- Short Entry: Supertrend turns bullish + EMA13 crosses below EMA34 + price below EMA100 + ADX>25
- Exit Signals: Price crosses Supertrend for respective position exits

#### Strategy Advantages
1. Integration of multiple technical indicators provides more reliable trading signals, effectively reducing false signals
2. Triple EMA system captures trend characteristics across different timeframes
3. ADX incorporation ensures trading only in strong trend markets
4. Multi-timeframe RSI analysis offers comprehensive market momentum assessment
5. Supertrend indicator provides objective stop-loss reference points
6. Bollinger Bands integration aids in determining market volatility states and potential breakout opportunities

#### Strategy Risks
1. Multiple indicator system may lead to lagging signals, affecting entry timing
2. May generate frequent false breakout signals in ranging markets
3. Fixed ADX threshold may perform inconsistently across different market environments
4. Rapid market volatility may result in suboptimal stop-loss placement
Risk control suggestions:
- Dynamically adjust ADX threshold based on market characteristics
- Introduce volatility-adaptive stop-loss mechanism
- Add volume analysis for signal confirmation

#### Strategy Optimization Directions
1. Indicator Parameter Optimization
- Consider introducing adaptive EMA periods
- Dynamically adjust Supertrend multiplier based on volatility
- Optimize Bollinger Bands parameters for different market phases

2. Signal System Enhancement
- Integrate volume factors for trade signal verification
- Add market structure analysis
- Implement volatility filters

3. Risk Management Improvement
- Design dynamic stop-loss mechanism
- Establish position sizing system
- Add trading time filters

#### Summary
This strategy constructs a relatively complete trading system through the organic combination of multiple technical indicators. EMA and Supertrend cooperation provides primary trading signals, ADX filtering ensures trading occurs in strong trend environments, while Bollinger Bands and RSI auxiliary analysis provides additional market perspectives. The strategy's main advantages lie in signal reliability and system completeness, but it also faces challenges in signal lag and parameter optimization. Through the proposed optimization directions, the strategy has the potential to enhance profitability while maintaining stability.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-04 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//made by Chinmay 

//@version=6
strategy("CJ - Multi1", overlay=true)

// Input for RSI length
rsi_length = input.int(14, title="RSI Length")

// Calculate Daily RSI
daily_rsi = ta.rsi(close, rsi_length)

// Calculate Weekly RSI (using security function to get weekly data)
weekly_rsi = request.security(syminfo.tickerid, "W", ta.rsi(close, rsi_length))

// Calculate Monthly RSI (using security function to get weekly data)
monthly_rsi = request.security(syminfo.tickerid, "M", ta.rsi(close, rsi_length))

// Plot the RSIs
plot(daily_rsi, color=color.blue, title="Daily RSI", linewidth=2)
plot(weekly_rsi, color=color.red, title="Weekly RSI", linewidth=2)
plot(monthly_rsi, color=color.black, title="Monthly RSI", linewidth=2)

// Create horizontal lines at 30, 50, and 70 for RSI reference
hline(30, "Oversold", color=color.green)
hline(70, "Overbought", color=color.red)
hline(50, "Neutral", color=color.gray)

// Bollinger Bands Calculation
bb_length = 20
bb_mult = 2
bb_stddev = ta.stdev(close, bb_length)
bb_average = ta.sma(close, bb_length)
bb_upper = bb_average + bb_mult * bb_stddev
bb_lower = bb_average - bb_mult * bb_stddev

plot(bb_upper, color=color.new(#ffb13b, 0), linewidth=2)
plot(bb_average, color=color.new(#b43bff, 0), linewidth=2)
plot(bb_lower, color=color.new(#ffb13b, 0), linewidth=2)

// Inputs for EMA
ema_L1 = input.int(defval=13, title="EMA Length 1")
ema_L2 = input.int(defval=34, title="EMA Length 2")
ema_L3 = input.int(defval=100, title="EMA Length 3")
adx_level = input.int(defval=25, title="ADX Level")

// Inputs for Supertrend
atr_l = input.int(defval=10, title="ATR Length")
factor = input.float(defval=3.0, title="Supertrend Multiplier")

// Calculate EMA
ema1 = ta.ema(close, ema_L1)
ema2 = ta.ema(close, ema_L2)
ema3 = ta.ema(close, ema_L3)

// Calculate Supertrend
[supertrend, direction] = ta.supertrend(factor, atr_l)

// Calculate ADX and DI
[diplus, diminus, adx] = ta.dmi(14,14)

// Buy and Sell Conditions
buy = direction == -1 and ema1 > ema2 and close > ta.ema(close, 100) and adx > adx_level
short = direction == -1 and ema1 < ema2 and close < ta.ema(close, 100) and adx > adx_level

sell = ta.crossunder(close, supertrend)
cover = ta.crossover(close, supertrend)

// Strategy Logic
if buy
    strategy.entry("Buy", strategy.long, comment="Long Entry")

if sell
    strategy.close("Buy", comment="Sell Exit")

// Uncomment for Short Strategy
if short
    strategy.entry("Short", strategy.short, comment="Short Entry")

if cover
    strategy.close("Short", comment="Cover Exit")

```

> Detail

https://www.fmz.com/strategy/477553

> Last Modified

2025-01-06 13:48:19
