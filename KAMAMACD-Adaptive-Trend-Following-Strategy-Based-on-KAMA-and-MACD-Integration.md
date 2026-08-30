
> Name

Adaptive-Trend-Following-Strategy-Based-on-KAMA-and-MACD-Integration
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d84f912c1386464ecb08.png)
![IMG](https://www.fmz.com/upload/asset/2d82c0bb83b573432666b.png)



[trans]
#### Overview
This strategy is a trend following system based on Kaufman Adaptive Moving Averages (KAMA) and MACD. By using KAMA as the main trend judgment indicator and MACD as the momentum confirmation indicator, it achieves intelligent tracking of market trends and precise grasp of trading opportunities. The strategy runs on the 4-hour time frame and uses dynamic stop loss and profit targets to manage risk.
#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. KAMA calculation: Use the 50-period KAMA as the main trend indicator, and dynamically adjust the smoothing coefficient through the efficiency ratio so that the moving average can better adapt to market conditions.
2. MACD confirmation: Use the MACD with slower settings (26, 52, 18) as a trend confirmation tool to ensure that the trading direction is consistent with the overall momentum.
3. ATR stop loss: Use 3 times the 14-period ATR as the basis for calculating dynamic stop loss and profit targets.
4. Trading rules:
   - Long condition: price crosses KAMA and MACD is bullish
   - Conditions for closing: price crosses KAMA and MACD is bearish
   - Risk management: Set dynamic stop loss and profit targets based on ATR
#### Strategic Advantages
1. Strong adaptability: KAMA can automatically adjust sensitivity according to market efficiency and maintain good performance in different market environments.
2. Reliable signal: combined with MACD confirmation significantly reduces the risk of false breakthroughs.
3. Improved risk management: Dynamic stop loss and profit targets based on volatility are adopted to make risk management more adaptable.
4. Large space for parameter optimization: key parameters can be adjusted according to different market characteristics.
#### Strategy Risk
1. Trend reversal risk: More false signals may appear in violently volatile markets.
2. Lagging risk: Both KAMA and MACD have a certain lag, and may miss the best entry opportunity.
3. Parameter sensitivity: Parameters may need to be adjusted under different market conditions to maintain strategy effects.
4. Impact of transaction costs: Frequent transactions may lead to higher transaction costs.
#### Strategy optimization direction
1. Introduce market volatility filter to adjust strategy parameters or suspend trading in high volatility environment.
2. Add trading volume analysis indicators to improve the accuracy of trend judgment.
3. Optimize MACD parameter settings to make them more suitable for the 4-hour time frame.
4. Implement adaptive stop loss multiples and dynamically adjust ATR multipliers based on market volatility.
5. Add a time filter to avoid trading during periods of low market liquidity.
#### Summary
This is a trend following strategy that innovatively combines the classic technical indicators KAMA and MACD. Through the combination of adaptive moving averages and momentum confirmation, as well as a complete risk management system, this strategy has strong practicality and stability. Although there are certain risks of hysteresis and parameter sensitivity, the robustness and profitability of the strategy can be further improved through the suggested optimization directions.  ||

#### Overview
This strategy is a trend-following system that combines the Kaufman Adaptive Moving Average (KAMA) with MACD. It uses KAMA as the primary trend indicator and MACD as momentum confirmation, achieving intelligent trend tracking and precise trade timing. The strategy operates on a 4-hour timeframe with dynamic stop-loss and take-profit targets for risk management.

#### Strategy Principles
The core logic is based on the following key components:
1. KAMA Calculation: Uses a 50-period KAMA as the main trend indicator, dynamically adjusting the smoothing coefficient through efficiency ratio to better adapt to market conditions.
2. MACD Confirmation: Employs slower settings (26,52,18) for MACD as trend confirmation, ensuring trade direction aligns with overall momentum.
3. ATR Stops: Uses 3 times the 14-period ATR for calculating dynamic stop-loss and take-profit levels.
4. Trading Rules:
   - Long Entry: Price crosses above KAMA with bullish MACD
   - Exit: Price crosses below KAMA with bearish MACD
   - Risk Management: Dynamic stop-loss and take-profit based on ATR

#### Strategy Advantages
1. High Adaptability: KAMA automatically adjusts sensitivity based on market efficiency, maintaining good performance across different market conditions.
2. Reliable Signals: MACD confirmation significantly reduces false breakout risks.
3. Comprehensive Risk Management: Volatility-based dynamic stops and targets provide adaptive risk control.
4. Extensive Parameter Optimization Space: Key parameters can be adjusted for different market characteristics.

#### Strategy Risks
1. Trend Reversal Risk: May generate false signals in highly volatile markets.
2. Lag Risk: Both KAMA and MACD have inherent lag, potentially missing optimal entry points.
3. Parameter Sensitivity: Different market conditions may require parameter adjustments.
4. Transaction Cost Impact: Frequent trading may lead to high transaction costs.

#### Optimization Directions
1. Implement market volatility filter to adjust parameters or pause trading in high volatility environments.
2. Add volume analysis indicators to improve trend identification accuracy.
3. Optimize MACD parameters for better alignment with 4-hour timeframe.
4. Implement adaptive stop-loss multiplier to dynamically adjust ATR multiplier based on market volatility.
5. Include time filters to avoid trading during low liquidity periods.

#### Summary
This is an innovative trend-following strategy that combines the classic technical indicators KAMA and MACD. Through the coordination of adaptive moving averages and momentum confirmation, along with a comprehensive risk management system, the strategy demonstrates strong practicality and stability. While it faces certain risks related to lag and parameter sensitivity, the suggested optimization directions can further enhance its robustness and profitability.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-20 00:00:00
end: 2025-02-18 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mckat

//@version=5
strategy("4-Hour KAMA Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)
// === Inputs ===
ama_length = input.int(50, title="KAMA Length for 4H")
fast_length = input.int(3, title="KAMA Fast Length")
slow_length = input.int(30, title="KAMA Slow Length")
atr_length = input.int(14, title="ATR Length")
atr_mult = input.float(3.0, title="ATR Multiplier for Stop-Loss & Take-Profit")
// === KAMA Calculation ===
var float kama = na
price_change = math.abs(close - close[ama_length])
volatility_sum = 0.0
for i = 0 to ama_length - 1
    volatility_sum := volatility_sum + math.abs(close[i] - close[i + 1])
efficiency_ratio = price_change / volatility_sum
smoothing_constant = math.pow(efficiency_ratio * (2 / (fast_length + 1) - 2 / (slow_length + 1)) + 2 / (slow_length + 1), 2)
kama := na(kama[1]) ? close : kama[1] + smoothing_constant * (close - kama[1])
// Plot KAMA
plot(kama, color=color.blue, title="KAMA (50)")
// === ATR for Stop-Loss and Take-Profit ===
atr = ta.atr(atr_length)
stop_loss = close - atr * atr_mult
take_profit = close + atr * atr_mult
// === MACD for Momentum Confirmation (Slow Settings for 4H) ===
[macd_line, signal_line, _] = ta.macd(close, 26, 52, 18)
macd_bullish = macd_line > signal_line
macd_bearish = macd_line < signal_line
// === Entry and Exit Conditions ===
buy_condition = ta.crossover(close, kama) and macd_bullish
sell_condition = ta.crossunder(close, kama) and macd_bearish
// === Execute Trades ===
if (buy_condition)
    strategy.entry("Buy", strategy.long)
if (sell_condition)
    strategy.close("Buy")
// === Dynamic Stop-Loss and Take-Profit ===
strategy.exit("Exit", "Buy", stop=stop_loss, limit=take_profit)
// === Plot Signals ===
plotshape(series=buy_condition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=sell_condition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")
```

> Detail

https://www.fmz.com/strategy/482779

> Last Modified

2025-02-20 15:01:37
