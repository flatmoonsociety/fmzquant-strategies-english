
> Name

DPO-EMA Trend Crossover Quantitative Strategy Research-DPO-EMA-Trend-Crossover-Quantitative-Strategy-Research
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16568d1c750c42e2dd5.png)

[trans]
#### Overview
This strategy is a quantitative trading strategy based on the intersection of the Detrended Price Oscillator (DPO) and the Exponential Moving Average (EMA). The core idea of ​​the strategy is to capture changes in market trends by comparing the relationship between DPO and its 4-period EMA, thereby generating buy and sell signals. This strategy is particularly suitable for larger time periods of 4 hours and above, and works better when using smoothed candlesticks (Heikin Ashi).
#### Strategy Principle
The core logic of the strategy includes the following key steps:
1. Calculate the 24-period simple moving average (SMA) as the baseline
2. Move the SMA forward (length/2+1) periods and obtain the shifted SMA value.
3. Subtract the SMA after displacement from the closing price to get the DPO value
4. Calculate the 4-period exponential moving average of DPO
5. When DPO crosses above its 4-period EMA, a buy signal is generated
6. When DPO crosses below its 4-period EMA, a sell signal is generated
#### Strategic Advantages
1. Strong signal clarity: clear buying and selling points are generated through cross signals to avoid subjective judgments
2. Good trend tracking effect: DPO indicator can effectively filter market noise and better capture the main trend
3. Small time lag: using short-period (4-period) EMA as the signal line can respond to market changes faster
4. Strong adaptability: The strategy has certain adaptability in different market environments.
5. Simple operation: the strategy logic is clear and easy to understand and execute
#### Strategy Risk
1. Volatile market risk: Frequent false signals may occur in a volatile market.
2. Lagging risk: Although short-period EMA is used, there is still a certain lag.
3. Trend reversal risk: Large losses may occur when a strong trend suddenly reverses
4. Parameter sensitivity: The strategy effect is more sensitive to the selection of period parameters.
5. Dependence on market conditions: The performance of the strategy may not be ideal under certain market conditions.
#### Strategy optimization direction
1. Introduce volatility filtering: ATR or other volatility indicators can be added to filter signals in low volatility environments
2. Increase trend confirmation: Combine with other trend indicators such as ADX to confirm trend strength
3. Optimize the stop loss setting: the stop loss position can be dynamically adjusted according to market volatility
4. Improve signal filtering: add volume confirmation or other technical indicators to filter out false signals
5. Parameter adaptation: realize dynamic optimization of parameters to adapt to different market environments
#### Summary
The DPO-EMA trend crossover strategy is a quantitative trading strategy with a simple structure but significant effects. By combining detrending oscillators and moving averages, this strategy can effectively capture market trend changes. Although there are some inherent risks, through reasonable optimization and risk management measures, this strategy still has good practical application value. For mid- to long-term traders, this is a strategic option worth considering. ||
#### Overview
This strategy is a quantitative trading approach based on the crossover between the Detrended Price Oscillator (DPO) and its 4-period Exponential Moving Average (EMA). The core concept is to capture market trend changes by comparing the relationship between DPO and its 4-period EMA to generate buy and sell signals. The strategy is particularly effective on 4-hour and above timeframes, especially when using Heikin Ashi candles.

#### Strategy Principles
The core logic includes the following key steps:
1. Calculate 24-period Simple Moving Average (SMA) as the baseline
2. Shift the SMA forward by (length/2+1) periods to get the displaced SMA value
3. Subtract the displaced SMA from the closing price to obtain the DPO value
4. Calculate the 4-period EMA of the DPO
5. Generate buy signal when DPO crosses above its 4-period EMA
6. Generate sell signal when DPO crosses below its 4-period EMA

#### Strategy Advantages
1. Clear Signal Generation: Cross-over signals provide clear entry and exit points, avoiding subjective judgment
2. Effective Trend Following: DPO indicator effectively filters market noise for better trend capture
3. Minimal Time Lag: Using short-period (4-period) EMA as signal line enables quick market response
4. High Adaptability: Strategy shows consistent performance across different market conditions
5. Simple Operation: Strategy logic is clear, easy to understand and execute

#### Strategy Risks
1. Choppy Market Risk: May generate frequent false signals in sideways markets
2. Lag Risk: Despite using short-period EMA, some inherent lag still exists
3. Trend Reversal Risk: May incur significant losses during sudden trend reversals
4. Parameter Sensitivity: Strategy performance is sensitive to period parameter selection
5. Market Condition Dependency: Strategy may not perform optimally under certain market conditions

#### Strategy Optimization Directions
1. Implement Volatility Filter: Add ATR or other volatility indicators to filter signals in low volatility environments
2. Add Trend Confirmation: Incorporate other trend indicators like ADX to confirm trend strength
3. Optimize Stop Loss: Dynamically adjust stop loss positions based on market volatility
4. Improve Signal Filtering: Add volume confirmation or other technical indicators to filter false signals
5. Parameter Adaptation: Implement dynamic parameter optimization to adapt to different market conditions

#### Summary
The DPO-EMA Trend Crossover Strategy is a structurally simple but effective quantitative trading strategy. By combining the detrended oscillator with moving averages, the strategy effectively captures market trend changes. While inherent risks exist, the strategy maintains practical value through proper optimization and risk management measures. For medium to long-term traders, this strategy represents a viable trading approach worth consideration.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-04 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("DPO 4,24 Strategy", shorttitle="DPO Strategy", overlay=true)

// Define a fixed lookback period and EMA length
length = 24
ema_length = 4

// Calculate the Simple Moving Average (SMA) of the closing prices
sma = ta.sma(close, length)

// Calculate the shifted SMA value
shifted_sma = sma[length / 2 + 1]

// Calculate the Detrended Price Oscillator (DPO)
dpo = close - shifted_sma

// Calculate the 4-period Exponential Moving Average (EMA) of the DPO
dpo_ema = ta.ema(dpo, ema_length)

// Generate buy and sell signals based on crossovers
buy_signal = ta.crossover(dpo, dpo_ema)
sell_signal = ta.crossunder(dpo, dpo_ema)

// Overlay buy and sell signals on the candlestick chart
plotshape(series=buy_signal, location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=sell_signal, location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// Strategy entry and exit conditions
if (buy_signal)
    strategy.entry("Buy", strategy.long)

if (sell_signal)
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/474030

> Last Modified

2024-12-05 14:57:18
