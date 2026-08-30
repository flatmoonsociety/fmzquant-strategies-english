
> Name

Quantitative trading strategy combining dynamic trend channel and relative strength indicator-Dynamic-Trend-Channel-and-Relative-Strength-Momentum-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ee12a441ceee6caeb4.png)

[trans]
#### Overview
This strategy is a quantitative trading system that combines the Keltner Channel and the Relative Strength Index (RSI). This strategy uses the combination of dynamic price channels and momentum indicators to capture trading opportunities in market fluctuations. The strategy uses the exponential moving average (EMA) and the average true range (ATR) to calculate the price channel, and combines the RSI indicator to confirm trading signals, achieving dual filtering of trend tracking and overbought and oversold.
#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. Construction of Keltner Channel: Use the 20-period EMA as the middle rail, and multiply the 10-period ATR by 1.5 times to determine the upper and lower rails to form a dynamic price fluctuation range.
2. Application of RSI indicator: Use 14-period RSI calculation, and set 70 and 30 as the critical values ​​for overbought and oversold.
3. Generation of trading signals:
   - Conditions for going long: price breaks through the lower track of the channel and RSI is below 30
   - Short selling conditions: price breaks through the channel upper rail and RSI is above 70
4. Position closing logic:
   - Closing of long positions: Price falls below EMA or RSI rises above 50
   - Short position closing: price breaks above EMA or RSI falls below 50
#### Strategic Advantages
1. Multi-dimensional confirmation: Through the cooperation of price breakthroughs and momentum indicators, the reliability of trading signals is improved.
2. Dynamic adaptation: Keltner Channel can automatically adjust the range width according to market volatility to adapt to different market environments.
3. Risk control: Using the neutral levels of EMA and RSI as closing conditions helps to stop profits and losses in a timely manner.
4. Visual support: The strategy provides a clear graphical interface, including channels, RSI levels and trading signal markers.
#### Strategy Risk
1. False breakthrough risk: Frequent false breakthrough signals may appear in volatile markets.
2. Hysteresis problem: Both EMA and RSI have a certain degree of lag, which may cause delays in entry or exit timing.
3. Parameter sensitivity: The strategy effect is more sensitive to parameter settings, and different market environments may require adjusting parameters.
4. Trend dependence: In markets with no obvious trend, strategies may perform poorly.
#### Strategy optimization direction
1. Parameter adaptation: An adaptive mechanism can be introduced to dynamically adjust channel parameters and RSI thresholds according to market volatility.
2. Signal filtering: Increase auxiliary indicators such as trading volume and volatility to improve signal quality.
3. Position management: Introduce a dynamic position management mechanism to adjust positions based on signal strength and market risk.
4. Market environment identification: Add a market environment judgment module and use different parameter combinations under different market conditions.
#### Summary
This strategy builds a relatively complete trading system by combining price channels and momentum indicators. The advantage of the strategy lies in the multi-dimensional confirmation of signals and dynamic adaptability, but it is also necessary to pay attention to risks such as false breakthroughs and parameter sensitivity. By further optimizing parameter adaptability and signal filtering mechanism, the stability and reliability of the strategy are expected to be improved. This strategy is suitable for applications in markets with obvious trends, and is a better choice for traders who hope to capture market momentum through technical indicators.
|| 

#### Overview
This strategy is a quantitative trading system that combines the Keltner Channel and Relative Strength Index (RSI). It captures trading opportunities in market volatility through the combination of dynamic price channels and momentum indicators. The strategy uses Exponential Moving Average (EMA) and Average True Range (ATR) to calculate price channels, coupled with RSI for trade signal confirmation, achieving dual filtration of trend following and overbought/oversold conditions.

#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. Keltner Channel Construction: Uses 20-period EMA as the middle band, 10-period ATR multiplied by 1.5 for upper and lower bands, forming a dynamic price fluctuation range.
2. RSI Application: Uses 14-period RSI calculation, with 70 and 30 as overbought and oversold thresholds.
3. Trade Signal Generation:
   - Long Entry: Price breaks above lower channel band and RSI is below 30
   - Short Entry: Price breaks below upper channel band and RSI is above 70
4. Exit Logic:
   - Long Exit: Price falls below EMA or RSI rises above 50
   - Short Exit: Price rises above EMA or RSI falls below 50

#### Strategy Advantages
1. Multi-dimensional Confirmation: Improves signal reliability through the combination of price breakouts and momentum indicators.
2. Dynamic Adaptation: Keltner Channel automatically adjusts range width based on market volatility, adapting to different market environments.
3. Risk Control: Uses EMA and RSI neutral levels for exit conditions, helping with timely profit-taking and stop-loss.
4. Visual Support: Strategy provides clear graphical interface including channels, RSI levels, and trade signal markers.

#### Strategy Risks
1. False Breakout Risk: Frequent false breakout signals may occur in ranging markets.
2. Lag Issues: Both EMA and RSI have inherent lag, potentially causing delayed entry or exit timing.
3. Parameter Sensitivity: Strategy effectiveness is sensitive to parameter settings, different market environments may require parameter adjustments.
4. Trend Dependency: Strategy may underperform in markets without clear trends.

#### Strategy Optimization Directions
1. Parameter Adaptation: Introduce adaptive mechanisms to dynamically adjust channel parameters and RSI thresholds based on market volatility.
2. Signal Filtering: Add auxiliary indicators like volume and volatility to improve signal quality.
3. Position Management: Introduce dynamic position management mechanisms to adjust holdings based on signal strength and market risk.
4. Market Environment Recognition: Add market environment assessment module to use different parameter combinations in different market states.

#### Summary
This strategy builds a relatively complete trading system by combining price channels and momentum indicators. Its strengths lie in multi-dimensional signal confirmation and dynamic adaptation capability, but attention must be paid to risks such as false breakouts and parameter sensitivity. Through further optimization of parameter adaptability and signal filtering mechanisms, the strategy's stability and reliability can be improved. The strategy is suitable for application in markets with clear trends and is a good choice for traders looking to capture market momentum through technical indicators.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-16 08:00:00
period: 3h
basePeriod: 3h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Keltner Channel + RSI Stratégiia", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=200)

// Parametre Keltner Channel
ema_length = input.int(20, title="EMA Perióda")
atr_length = input.int(10, title="ATR Perióda")
multiplier = input.float(1.5, title="ATR Multiplikátor")

// Výpočet Keltner Channel
ema = ta.ema(close, ema_length)
atr = ta.atr(atr_length)
upper_kc = ema + (multiplier * atr)
lower_kc = ema - (multiplier * atr)

// Parametre RSI
rsi_length = input.int(14, title="RSI Perióda")
rsi_overbought = input.int(70, title="RSI Prekúpenosť")
rsi_oversold = input.int(30, title="RSI Prepredanosť")

// Výpočet RSI
rsi = ta.rsi(close, rsi_length)

// Obchodné podmienky

// Nákupná podmienka: Cena prechádza nad dolnou Keltner Channel a RSI je pod prepredanosťou
long_condition = ta.crossover(close, lower_kc) and (rsi < rsi_oversold)

// Predajná podmienka: Cena prechádza pod hornou Keltner Channel a RSI je nad prekúpenosťou
short_condition = ta.crossunder(close, upper_kc) and (rsi > rsi_overbought)

// Uzatváranie pozícií
close_long_condition = ta.crossunder(close, ema) or (rsi > 50)
close_short_condition = ta.crossover(close, ema) or (rsi < 50)

// Vstupy do pozícií
if (long_condition)
    strategy.entry("Long", strategy.long)

if (short_condition)
    strategy.entry("Short", strategy.short)

// Uzatváranie pozícií
if (close_long_condition)
    strategy.close("Long")

if (close_short_condition)
    strategy.close("Short")

// Vizualizácia indikátorov

// Keltner Channel
plot_ema = plot(ema, title="EMA", color=color.blue, linewidth=2)
plot_upper = plot(upper_kc, title="Horná Keltner Channel", color=color.green, linewidth=1)
plot_lower = plot(lower_kc, title="Dolná Keltner Channel", color=color.red, linewidth=1)
fill(plot_upper, plot_lower, color=color.new(color.purple, 90), title="Keltner Channel Fill")  // Nastavenie transparentnosti priamo v farbe

// RSI
hline_overbought = hline(rsi_overbought, "RSI Overbought", color=color.red, linestyle=hline.style_dotted)
hline_oversold = hline(rsi_oversold, "RSI Oversold", color=color.green, linestyle=hline.style_dotted)
plot_rsi = plot(rsi, title="RSI", color=color.orange, linewidth=2, offset=0)

// Šípky pre signály
plotshape(series=long_condition, location=location.belowbar, color=color.green, style=shape.labelup, title="Nákupný Signál", text="BUY")
plotshape(series=short_condition, location=location.abovebar, color=color.red, style=shape.labeldown, title="Predajný Signál", text="SELL")

```

> Detail

https://www.fmz.com/strategy/482459

> Last Modified

2025-02-18 15:15:48
