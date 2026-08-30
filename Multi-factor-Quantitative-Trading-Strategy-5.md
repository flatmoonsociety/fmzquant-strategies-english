
> Name

Multi-factor-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

A multi-factor quantitative trading strategy that comprehensively considers moving average factors and oscillator factors to control risks and improve stability. This article will introduce in detail the principles, advantages and possible risks of this trading strategy.
## Strategy Principle
This strategy mainly consists of three modules:
1. Moving Average Factor
Use 5 EMA moving averages with different periods (8-day, 13-day, 21-day, 34-day, 55-day) to build a trend filter. The moving averages are arranged from short to long. Only when the short-period moving average crosses the long-period moving average, it will have trend characteristics and generate a trading signal.
2. Oscillator factors
At the same time, the two major oscillator indicators RSI and Stochastic are combined to verify the breakthrough to avoid a large number of false breakthroughs in the volatile market.
The parameter of RSI is 14. When RSI is in the 40-70 range, it meets the long conditions, and when it is in the 30-60 range, it meets the short conditions.
The Stochastic parameter is (14, 3, 3). When the K line is in the 20-80 range, it meets the long conditions, and when it is in the 5-95 range, it meets the short conditions.
3. Entry and exit logic
Only when the moving average factor and the oscillator factor meet the conditions at the same time will the entry signal be triggered; when any factor no longer meets the conditions, an exit signal will be generated.
The entire strategy adopts a strict multi-factor filtering mechanism to maintain a high winning rate while ensuring the stability and reliability of trading signals.
## Strategic Advantages
- Multi-factor design effectively filters market noise and avoids over-trading
- Consider both trend factors and reversal factors, combining the advantages of trend tracking and point trading
- Combined with moving averages and oscillators, you can capture reversal points in trends
- There is a large space for optimization, and better strategic effects can be obtained by adjusting parameters
## Risk warning
- The signal frequency of multi-factor strategy is low and some trading opportunities may be missed.
- The moving average lags behind and should be verified with shorter period indicators
- Oscillators are prone to false signals and should be used only as auxiliary factors
- Need to regularly optimize parameters to adapt to changes in the market environment
## Summarize
This strategy successfully combines the advantages of trend following and reversal trading. The multi-factor model effectively controls risks and can obtain stable excess returns. This is a very practical quantitative trading strategy model that deserves in-depth research and application by the artificial intelligence community.
||

The multi-factor quantitative trading strategy that integrates moving average factors and oscillating indicators to control risks and improve stability. This article explains the rationale, advantages and potential risks of this trading strategy in detail.

## Strategy Logic

The strategy consists of three main modules:

1. Moving Average Factors

Using 5 EMAs with different periods (8, 13, 21, 34, 55) to build a trend filter. The MAs are arranged from short to long. Only when faster EMA crosses above slower EMA, the trend signal is generated.

2. Oscillating Indicators 

Combine RSI and Stochastic oscillators to validate the breakout signals, avoiding excessive false breaks in ranging markets. 

RSI (14) generates long signal when in 40-70 range and short signal when in 30-60 range.

Stochastic (14,3,3) gives long signal when K line is between 20-80 and short signal when K line is between 5-95.

3. Entry and Exit Logic

Entry signal is triggered only when both factors are aligned. Exit signal is generated when either factor is no longer valid.

The strict multi-factor filter ensures high win rate and reliable signals.

## Advantages

- Multi-factor design effectively filters market noise and prevents over-trading.
- Combines trend following and mean-reversion, balancing dynamic trading andlocation trading.
- Captures reversal points within trends using MA and oscillators. 
- Large optimization space to obtain better performance.

## Risks

- Relatively low signal frequency, may miss some opportunities.
- MA lagging should be verified with faster oscillators.
- Oscillators prone to false signals, should be used as auxiliary factors.
- Parameters need periodic optimization to adapt to changing market conditions.

## Conclusion

This strategy successfully combines the strengths of trend following and reversal trading strategies. The multi-factor risk control model delivers stable alpha. It is a highly practical quantitative trading strategy worth in-depth research and application by the AI community.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-12 00:00:00
end: 2022-11-15 00:00:00
period: 2d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title = "Combined Strategy", default_qty_type = strategy.percent_of_equity, default_qty_value = 100, commission_type=strategy.commission.percent, commission_value = .0020, pyramiding = 0, slippage = 3, overlay = true)

//----------//
// MOMENTUM //
//----------//
ema8 = ema(close, 8)
ema13 = ema(close, 13)
ema21 = ema(close, 21)
ema34 = ema(close, 34)
ema55 = ema(close, 55)

plot(ema8, color=red, style=line, title="8", linewidth=1)
plot(ema13, color=orange, style=line, title="13", linewidth=1)
plot(ema21, color=yellow, style=line, title="21", linewidth=1)
plot(ema34, color=aqua, style=line, title="34", linewidth=1)
plot(ema55, color=lime, style=line, title="55", linewidth=1)

longEmaCondition = ema8 > ema13 and ema13 > ema21 and ema21 > ema34 and ema34 > ema55
exitLongEmaCondition = ema13 < ema55

shortEmaCondition = ema8 < ema13 and ema13 < ema21 and ema21 < ema34 and ema34 < ema55
exitShortEmaCondition = ema13 > ema55

// ----------  //
// OSCILLATORS //
// ----------- //
rsi = rsi(close, 14)
longRsiCondition = rsi < 70 and rsi > 40
exitLongRsiCondition = rsi > 70

shortRsiCondition = rsi > 30 and rsi < 60
exitShortRsiCondition = rsi < 30

// Stochastic
length = 14, smoothK = 3, smoothD = 3
kFast = stoch(close, high, low, 14)
dSlow = sma(kFast, smoothD)

longStochasticCondition = kFast < 80
exitLongStochasticCondition = kFast > 95

shortStochasticCondition = kFast > 20
exitShortStochasticCondition = kFast < 5

//----------//
// STRATEGY //
//----------//

longCondition = longEmaCondition and longRsiCondition and longStochasticCondition and strategy.position_size == 0
exitLongCondition = (exitLongEmaCondition or exitLongRsiCondition or exitLongStochasticCondition) and strategy.position_size > 0

if (longCondition)
    strategy.entry("LONG", strategy.long)
if (exitLongCondition)
    strategy.close("LONG")
    
shortCondition = shortEmaCondition and shortRsiCondition and shortStochasticCondition and strategy.position_size == 0
exitShortCondition = (exitShortEmaCondition or exitShortRsiCondition or exitShortStochasticCondition) and strategy.position_size < 0

if (shortCondition)
    strategy.entry("SHORT", strategy.short)
if (exitShortCondition)
    strategy.close("SHORT")
```

> Detail

https://www.fmz.com/strategy/426581

> Last Modified

2023-09-13 14:46:59
