
> Name

VWAP-Deviation-and-OBV-RSI-Combined-Mean-Reversion-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/62341d7c7e6994b706.png)

[trans]
#### Overview
This is a compound mean reversion trading strategy that combines VWAP (Volume Weighted Average Price) deviation and OBV (Power Wave Indicator) RSI. This strategy monitors the deviation of price relative to VWAP and the overbought and oversold status of the OBV-RSI indicator to trade when the market experiences extreme conditions. When the price deviates from VWAP to a certain extent and the OBV-RSI indicator shows an overbought or oversold state, the strategy will issue a trading signal and close the position when the price returns to VWAP.
#### Strategy Principle
The strategy is mainly based on two core indicators:
1. VWAP deviation indicator: Use the 60-period weighted moving average (WMA) to calculate the VWAP baseline, and calculate the upper and lower 2 times standard deviation channels through the standard deviation. This channel is used to identify extreme deviations in price.
2. OBV-RSI indicator: Apply traditional RSI to OBV to calculate the relative strength of 14 periods. OBV reflects the intensity of price movement through accumulated trading volume, while RSI is used to identify overbought and oversold conditions in OBV.
Conditions for opening a position:
- Go long: when OBV-RSI <= 30 (oversold) and the price is below the lower track
- Short: When OBV-RSI >= 70 (overbought) and price is above the upper track
Conditions for closing positions:
- When the price returns to the VWAP baseline
- Set a 0.6% stop loss to control risk
#### Strategic Advantages
1. Multi-dimensional confirmation: combines price, volume and momentum indicators to provide more reliable trading signals
2. Perfect risk control: dual protection using fixed stop loss and mean return closing mechanism
3. Strong adaptability: can adapt to different market environments through parameter adjustment
4. Clear logic: The trading signals are clear and easy to understand and execute.
5. Mean reversion characteristics: taking advantage of trading opportunities brought by market overreaction
#### Strategy Risk
1. Trending market risk: Wrong signals may be triggered frequently in strong trending markets.
2. Slippage risk: You may face larger slippage when fluctuations occur.
3. False breakout risk: Prices may continue to move in extreme directions after triggering the signal
4. Parameter sensitivity: Different parameter combinations may lead to large differences in strategy performance
5. Liquidity risk: It may be difficult to execute transactions in a timely manner in an illiquid market
#### Strategy optimization direction
1. Dynamic parameter adjustment: adaptively adjust VWAP and RSI parameters according to market volatility
2. Market environment filtering: Add trend filters to reduce trading frequency in strong trending markets
3. Optimization of the profit-taking mechanism: Design a dynamic profit-taking mechanism to improve profit sustainability
4. Improved position management: dynamically adjust position size based on volatility and risk assessment
5. Signal confirmation enhancement: add additional technical indicators or time filtering to improve signal quality
#### Summary
This strategy builds a robust mean reversion trading system by combining the VWAP deviation and OBV-RSI indicators. The strategy looks for trading opportunities in extreme market conditions and protects fund security through multiple risk control mechanisms. Although there are certain risks, through continuous optimization and improvement, the strategy is expected to maintain stable performance in different market environments. It is recommended that traders conduct sufficient backtesting and parameter optimization before using it in real trading, and adjust strategy parameters according to specific market characteristics. ||
#### Overview
This is a combined mean reversion trading strategy that integrates VWAP (Volume-Weighted Average Price) deviation and OBV (On-Balance Volume) RSI. The strategy monitors price deviations from VWAP and OBV-RSI's overbought/oversold conditions to execute trades during extreme market conditions. Signals are generated when price deviates significantly from VWAP while OBV-RSI shows overbought or oversold conditions, with positions closed when price reverts to VWAP.

#### Strategy Principles
The strategy is based on two core indicators:
1. VWAP Deviation Indicator: Uses a 60-period Weighted Moving Average (WMA) to calculate the VWAP baseline and 2-standard deviation channels. These channels identify extreme price deviations.
2. OBV-RSI Indicator: Applies traditional RSI to OBV with a 14-period calculation. OBV accumulates volume to reflect price movement strength, while RSI identifies overbought/oversold conditions.

Entry Conditions:
- Long: When OBV-RSI <= 30 (oversold) and price below lower band
- Short: When OBV-RSI >= 70 (overbought) and price above upper band

Exit Conditions:
- When price reverts to VWAP baseline
- 0.6% stop-loss for risk management

#### Strategy Advantages
1. Multi-dimensional confirmation: Combines price, volume, and momentum indicators for more reliable signals
2. Comprehensive risk control: Dual protection with fixed stop-loss and mean reversion exits
3. High adaptability: Adjustable parameters for different market conditions
4. Clear logic: Explicit trading signals, easy to understand and execute
5. Mean reversion characteristics: Capitalizes on market overreaction opportunities

#### Strategy Risks
1. Trend market risk: May generate false signals in strong trending markets
2. Slippage risk: Significant slippage possible during high volatility
3. False breakout risk: Price may continue moving in extreme direction after signal
4. Parameter sensitivity: Different parameter combinations may lead to varying performance
5. Liquidity risk: Execution challenges in low liquidity markets

#### Strategy Optimization Directions
1. Dynamic parameter adjustment: Adapt VWAP and RSI parameters based on market volatility
2. Market environment filtering: Add trend filters to reduce trading frequency in strong trends
3. Profit-taking optimization: Design dynamic profit-taking mechanisms for sustained profitability
4. Position management improvement: Dynamically adjust position sizes based on volatility and risk assessment
5. Signal confirmation enhancement: Add additional technical indicators or time filters for better signal quality

#### Summary
This strategy combines VWAP deviation and OBV-RSI indicators to create a robust mean reversion trading system. It seeks trading opportunities in extreme market conditions while protecting capital through multiple risk control mechanisms. Although certain risks exist, continuous optimization and refinement can help maintain stable performance across different market environments. Traders are advised to conduct thorough backtesting and parameter optimization before live trading, adjusting strategy parameters according to specific market characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-16 08:00:00
period: 4h
basePeriod: 4h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy('[Hoss] Combined Strategy', overlay=true)

// Indikator 1: [Hoss] VWAP Deviation
indicator_vwap = input.bool(true, title="Show VWAP Deviation Indicator", group="Visibility")
length = input.int(60, title="VWAP Length", group="VWAP Settings")
src = input(close, title="Source", group="VWAP Settings")

// Berechnungen für VWAP
vwmean = ta.wma(src, length)
dev = ta.stdev(src, length)
basis = vwmean
upper_dev2 = vwmean + dev * 2
lower_dev2 = vwmean - dev * 2

// Plotting VWAP Deviation
plot(indicator_vwap ? basis : na, color=color.gray, title='Basis', linewidth=2)
plot1 = plot(indicator_vwap ? upper_dev2 : na, color=color.red, title='Upper Dev 2', linewidth=2)
plot2 = plot(indicator_vwap ? lower_dev2 : na, color=color.green, title='Lower Dev 2', linewidth=2)
fill(plot1, plot2, color=color.new(color.green, 80), title='Deviation Band')

// Indikator 2: [Hoss] OBV RSI
indicator_obv_rsi = input.bool(true, title="Show OBV RSI Indicator", group="Visibility")
len = input.int(14, title="RSI Length", group="OBV RSI Settings")
obv = ta.cum(ta.change(src) > 0 ? volume : ta.change(src) < 0 ? -volume : 0)
rsi = ta.rsi(obv, len)

// Plotting OBV RSI
plot(indicator_obv_rsi ? rsi : na, color=color.blue, title="OBV RSI", linewidth=2)
hline(70, title="Overbought", color=color.red, linestyle=hline.style_dashed)
hline(30, title="Oversold", color=color.green, linestyle=hline.style_dashed)

// Strategie: Kauf- und Verkaufssignale
long_condition = not na(rsi) and rsi <= 30 and close <= lower_dev2
short_condition = not na(rsi) and rsi >= 70 and close >= upper_dev2

if (long_condition)
    strategy.entry("Long", strategy.long, stop=close * 0.994) // Stop-Loss bei 0.6%

if (short_condition)
    strategy.entry("Short", strategy.short, stop=close * 1.006) // Stop-Loss bei 0.6%

// Flash Close beim Erreichen des VWAP
if (strategy.position_size > 0 and close >= basis)
    strategy.close("Long")

if (strategy.position_size < 0 and close <= basis)
    strategy.close("Short")

```

> Detail

https://www.fmz.com/strategy/482452

> Last Modified

2025-02-18 15:02:17
