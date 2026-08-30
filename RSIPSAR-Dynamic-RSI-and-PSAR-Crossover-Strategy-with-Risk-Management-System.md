
> Name

Dynamic-RSI-and-PSAR-Crossover-Strategy-with-Risk-Management-System
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/63dc027521abcb9bbe7077864cedba91245c45138352df9fb376979beca36b39.png)
![IMG](assets/images/7ec04ba8f6d93764123da7b5ec8c1a7ba261381356bfece09990597ade3e1e98.png)




[trans]
#### Overview
This is a trading strategy that combines the RSI indicator and the Parabolic SAR (PSAR). It captures market trends by setting dynamic overbought and oversold ranges and matching the cross signals of price and PSAR. At the same time, this strategy integrates a complete risk management system, including stop-profit and stop-loss mechanisms and position management, to achieve more robust trading performance.
#### Strategy Principle
The strategy is mainly based on the following core logic:
1. Entry signal: When the price breaks through PSAR upward and RSI is in the oversold range (<30), the system sends a long signal
2. Exit signal: When the price falls below PSAR and RSI is in the overbought range (>70), the system sends a closing signal
3. Risk control: Set a 5% take-profit and a 3% stop-loss for each transaction, which can be adjusted according to actual needs.
4. Signal visualization: The RSI indicator visually displays the market status through dynamic color coding (green indicates oversold, red indicates overbought, and blue indicates neutral)
5. Transaction reminder: Automatically issue a transaction reminder when a buy or sell signal is triggered.
#### Strategic Advantages
1. Signal reliability: By combining PSAR and RSI double confirmation, false signals are effectively reduced
2. Controllable risk: built-in stop-profit and stop-loss mechanism to limit single transaction losses
3. Clear operation: visual interface design, intuitive and clear trading signals
4. Strong adaptability: parameters can be adjusted and suitable for different market environments
5. High degree of automation: supports automatic trading and backtest analysis
#### Strategy Risk
1. Not applicable to volatile markets: Frequent transactions may occur in sideways volatile markets.
2. Impact of slippage: In a high volatility environment, you may face greater risk of slippage.
3. Parameter sensitivity: Different parameter combinations may lead to large differences in strategy performance
4. Stop loss risk: fixed stop loss levels may not be flexible enough under certain market conditions
5. Signal lag: The indicator itself has a certain lag and may miss the best entry opportunity.
#### Strategy optimization direction
1. Introduce market environment judgment: add trend strength indicators and use different parameters in different market environments
2. Dynamic stop loss setting: automatically adjust the stop loss position according to market volatility
3. Optimize position management: introduce a dynamic position management system and adjust the position opening ratio based on risk assessment
4. Add time filtering: add trading time window to avoid trading during unfavorable periods
5. Signal confirmation mechanism: Increase auxiliary indicators such as trading volume to improve signal reliability
#### Summary
This strategy builds a complete trading system by combining the PSAR and RSI indicators. Its advantages lie in clear signals and controllable risks, but it is still necessary to pay attention to the adaptability of the market environment. Through continuous optimization and parameter adjustment, the strategy is expected to achieve better trading results. It is recommended to conduct sufficient backtest verification before real trading, and adjust parameter settings according to specific market characteristics. ||
#### Overview
This is a trading strategy that combines the RSI indicator with the Parabolic SAR (PSAR) indicator, capturing market trends through dynamic overbought/oversold zones and PSAR crossover signals. The strategy incorporates a comprehensive risk management system, including take-profit and stop-loss mechanisms, along with position management for more robust trading performance.

#### Strategy Principles
The strategy is based on the following core logic:
1. Entry Signal: Long position triggered when price crosses above PSAR and RSI is in oversold territory (<30)
2. Exit Signal: Position closed when price crosses below PSAR and RSI is in overbought territory (>70)
3. Risk Control: 5% take-profit and 3% stop-loss for each trade, adjustable based on requirements
4. Signal Visualization: RSI indicator with dynamic color coding (green for oversold, red for overbought, blue for neutral) for intuitive market state display
5. Trade Alerts: Automatic notifications when buy/sell signals are triggered

#### Strategy Advantages
1. Signal Reliability: Reduces false signals through dual confirmation with PSAR and RSI
2. Risk Control: Built-in take-profit and stop-loss mechanisms limit single trade losses
3. Clear Operation: Visual interface design provides intuitive trading signals
4. High Adaptability: Adjustable parameters suit different market conditions
5. High Automation: Supports automated trading and backtesting analysis

#### Strategy Risks
1. Unsuitable for Ranging Markets: May generate frequent trades in sideways markets
2. Slippage Impact: Potential significant slippage risk in high volatility environments
3. Parameter Sensitivity: Different parameter combinations may lead to varying strategy performance
4. Stop Loss Risk: Fixed stop-loss levels may lack flexibility in certain market conditions
5. Signal Lag: Indicators have inherent lag, possibly missing optimal entry points

#### Strategy Optimization Directions
1. Market Environment Assessment: Add trend strength indicators for parameter adaptation
2. Dynamic Stop-Loss: Automatically adjust stop-loss levels based on market volatility
3. Position Management Optimization: Implement dynamic position sizing based on risk assessment
4. Time Filtering: Add trading time windows to avoid unfavorable periods
5. Signal Confirmation: Include volume and other auxiliary indicators to improve signal reliability

#### Summary
The strategy establishes a complete trading system by combining PSAR and RSI indicators. Its strengths lie in clear signals and controlled risk, though market environment adaptability requires attention. Through continuous optimization and parameter adjustment, the strategy can achieve better trading results. It's recommended to conduct thorough backtesting before live trading and adjust parameters according to specific market characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-25 00:00:00
end: 2025-02-22 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=5
strategy("PSAR & RSI Strategy with Risk Management", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// User Inputs
psar_start = input.float(0.02, title="PSAR Start")
psar_increment = input.float(0.02, title="PSAR Increment")
psar_max = input.float(0.2, title="PSAR Max")
rsi_length = input.int(14, title="RSI Length")
rsi_overbought = input.int(70, title="RSI Overbought Level")
rsi_oversold = input.int(30, title="RSI Oversold Level")

tp_percent = input.float(5, title="Take Profit %") / 100  // Take Profit Level
sl_percent = input.float(3, title="Stop Loss %") / 100    // Stop Loss Level

// PSAR Calculation
psar = ta.sar(psar_start, psar_increment, psar_max)

// RSI Calculation
rsi = ta.rsi(close, rsi_length)

// Buy & Sell Conditions
buy_signal = ta.crossover(close, psar) and rsi < rsi_oversold
sell_signal = ta.crossunder(close, psar) and rsi > rsi_overbought

// Plot PSAR on Chart
plot(psar, style=plot.style_cross, color=color.blue, title="PSAR")

// Buy & Sell Signals on Chart
plotshape(series=buy_signal, location=location.belowbar, color=color.green, style=shape.labelup, title="BUY Signal")
plotshape(series=sell_signal, location=location.abovebar, color=color.red, style=shape.labeldown, title="SELL Signal")

// RSI Visualization (Dynamic Colors)
rsi_color = rsi > rsi_overbought ? color.red : rsi < rsi_oversold ? color.green : color.blue
plot(rsi, title="RSI", color=rsi_color, linewidth=2)
hline(rsi_overbought, "Overbought", color=color.red)
hline(rsi_oversold, "Oversold", color=color.green)

// Alerts for Buy & Sell
alertcondition(buy_signal, title="BUY Alert", message="Buy Signal Triggered!")
alertcondition(sell_signal, title="SELL Alert", message="Sell Signal Triggered!")

// Strategy Execution with Take Profit & Stop Loss
if buy_signal
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit / Stop Loss", from_entry="Buy", limit=close * (1 + tp_percent), stop=close * (1 - sl_percent))

if sell_signal
    strategy.close("Buy")
```

> Detail

https://www.fmz.com/strategy/483528

> Last Modified

2025-02-24 10:27:37
