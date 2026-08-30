
> Name

Adaptive-Trend-Following-Strategy-Combining-Dual-Moving-Average-Crossover-and-RSI
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d928bf19c8cca8c9ebb3.png)
![IMG](https://www.fmz.com/upload/asset/2d8a42ee842e07ce2c2c0.png)




[trans]
#### Overview
This strategy is a trend following strategy that combines a double moving average crossover system with the Relative Strength Index (RSI). The market trend is captured through the intersection of the 9-period and 21-period exponential moving averages (EMA), while the RSI indicator is used to filter overbought and oversold, and combined with volume confirmation to improve the reliability of trading signals. The strategy also integrates a dynamic stop-loss mechanism based on the true fluctuation range (ATR) to achieve comprehensive risk control.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Use the crossover of fast EMA (9 periods) and slow EMA (21 periods) to identify potential trend changes
2. Use the RSI indicator to filter overbought and oversold conditions. Trading is only allowed when the RSI value is within the range of 40-60.
3. Set the minimum trading volume threshold (100,000) as the transaction confirmation condition
4. Use 1.5 times ATR as the dynamic stop loss distance to achieve flexible risk control
When the fast EMA crosses the slow EMA upward, the RSI is greater than 40, and the trading volume exceeds the threshold, the system generates a long signal. On the contrary, when the fast EMA crosses the slow EMA downward, the RSI is less than 60, and the trading volume is confirmed, the system generates a short signal.
#### Strategic Advantages
1. The indicator combination is scientific and reasonable: organically combine trend tracking, momentum indicators and trading volume analysis
2. Improved risk control: multi-level risk management through RSI filtering and dynamic stop loss
3. Flexible parameter setting: key parameters can be optimized and adjusted according to different market characteristics
4. Strict signal confirmation: multiple conditions are required to be met at the same time, effectively reducing false signals
5. Clear execution logic: The strategy rules are clear, which facilitates real-time operation and backtest verification.
#### Strategy Risk
1. Sideways markets may produce frequent transactions: there are more double moving average crossovers in a volatile market
2. RSI filtering may miss part of the starting point of the trend: RSI may have been at a high level in the early stages of a strong market
3. Trading volume filtering may be too strict in some markets: some low-liquidity products are difficult to meet the conditions.
4. ATR stop loss with a fixed multiple may not be flexible enough during severe fluctuations
5. Failure to set a fixed profit-taking point may affect the efficiency of capital utilization.
#### Strategy optimization direction
1. Introduce adaptive parameters: EMA period and RSI threshold can be dynamically adjusted according to market volatility
2. Optimize the stop loss mechanism: set multi-level stop losses based on support and resistance levels
3. Add market environment filtering: add trend strength indicator and only trade in clear trends
4. Improve fund management: adjust position size based on signal strength and market fluctuations
5. Add a take-profit mechanism: set a dynamic take-profit point based on ATR
#### Summary
This strategy builds a logically rigorous trend tracking system through a scientific combination of classic technical indicators. The strategy's multiple filtering mechanisms and risk control methods make it have strong practical application value. There is room for further improvement of the strategy through the suggested optimization directions. It is particularly suitable for markets with large fluctuations and sufficient liquidity, but it requires full testing and parameter optimization before use. ||
#### Overview
This strategy is a trend following system that combines a dual moving average crossover with the Relative Strength Index (RSI). It captures market trends through the crossover of 9-period and 21-period Exponential Moving Averages (EMA), while using RSI for overbought/oversold filtering and volume confirmation to enhance signal reliability. The strategy also incorporates a dynamic stop-loss mechanism based on Average True Range (ATR) for comprehensive risk control.

#### Strategy Principles
The core logic is based on several key elements:
1. Using fast EMA (9-period) and slow EMA (21-period) crossovers to identify potential trend changes
2. Filtering through RSI indicator, allowing trades only when RSI is between 40-60
3. Setting minimum volume threshold (100,000) as trade confirmation
4. Implementing 1.5x ATR as dynamic stop-loss distance for flexible risk control

Long signals are generated when the fast EMA crosses above the slow EMA, RSI is above 40, and volume exceeds the threshold. Conversely, short signals occur when the fast EMA crosses below the slow EMA, RSI is below 60, and volume confirms.

#### Strategy Advantages
1. Scientific indicator combination: integrating trend following, momentum, and volume analysis
2. Comprehensive risk control: multi-level risk management through RSI filtering and dynamic stops
3. Flexible parameters: key parameters can be optimized for different market characteristics
4. Strict signal confirmation: multiple conditions required, effectively reducing false signals
5. Clear execution logic: explicit rules facilitating live trading and backtesting

#### Strategy Risks
1. Frequent trades in ranging markets: multiple crossovers during consolidation
2. RSI filter may miss trend beginnings: RSI might be high at strong trend initiation
3. Volume filter might be too strict: challenging for low liquidity instruments
4. Fixed multiplier ATR stops may lack flexibility during extreme volatility
5. Absence of fixed take-profit levels may affect capital efficiency

#### Optimization Directions
1. Introduce adaptive parameters: dynamically adjust EMA periods and RSI thresholds based on volatility
2. Optimize stop-loss mechanism: implement multi-level stops using support/resistance
3. Add market environment filtering: incorporate trend strength indicators
4. Improve money management: adjust position sizes based on signal strength and volatility
5. Add take-profit mechanism: implement ATR-based dynamic take-profit levels

#### Summary
The strategy constructs a logically rigorous trend following system through scientific combination of classic technical indicators. Its multiple filtering mechanisms and risk control measures provide strong practical value. There's room for further improvement through the suggested optimizations. It's particularly suitable for volatile and liquid markets, but requires thorough testing and parameter optimization before implementation.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-07 00:00:00
end: 2025-02-18 08:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Call & Put Options Strategy (Optimized)", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// ? Configuration Parameters
emaShort = input(9, title="Short EMA")
emaLong = input(21, title="Long EMA")
rsiLength = input(14, title="RSI Period")
rsiOverbought = input(60, title="RSI Overbought") // Adjusted for more signals
rsiOversold = input(40, title="RSI Oversold")   // More flexible to confirm buys
atrLength = input(14, title="ATR Period")
atrMult = input(1.5, title="ATR Multiplier for Stop Loss")
minVol = input(100000, title="Minimum Volume to Confirm Entry") // Volume filter

// ? Indicator Calculations
emaFast = ta.ema(close, emaShort)
emaSlow = ta.ema(close, emaLong)
rsi = ta.rsi(close, rsiLength)
atr = ta.atr(atrLength)
vol = volume

// ? Entry Signal Conditions
condCALL = ta.crossover(emaFast, emaSlow) and rsi > rsiOversold and vol > minVol
condPUT = ta.crossunder(emaFast, emaSlow) and rsi < rsiOverbought and vol > minVol

// ? Plot signals on the chart
plotshape(condCALL, location=location.belowbar, color=color.green, style=shape.labelup, title="CALL", size=size.small)
plotshape(condPUT, location=location.abovebar, color=color.red, style=shape.labeldown, title="PUT", size=size.small)

// ? Alert conditions
alertcondition(condCALL, title="CALL Signal", message="? CALL signal confirmed")
alertcondition(condPUT, title="PUT Signal", message="? PUT signal confirmed")

// ? Risk Management - Stop Loss and Take Profit
longStop = close - (atr * atrMult)
shortStop = close + (atr * atrMult)

strategy.entry("CALL", strategy.long, when=condCALL)
strategy.exit("CALL Exit", from_entry="CALL", stop=longStop)

strategy.entry("PUT", strategy.short, when=condPUT)
strategy.exit("PUT Exit", from_entry="PUT", stop=shortStop)

```

> Detail

https://www.fmz.com/strategy/482877

> Last Modified

2025-02-27 17:32:08
