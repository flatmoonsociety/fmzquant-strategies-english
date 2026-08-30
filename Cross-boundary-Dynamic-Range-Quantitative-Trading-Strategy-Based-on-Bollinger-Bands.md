
> Name

Cross-boundary-Dynamic-Range-Quantitative-Trading-Strategy-Based-on-Bollinger-Bands
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ee5322520b33ae0773.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on the Bollinger Bands indicator, which captures market trends through dynamic range breakout signals. The strategy uses the standard deviation channel as the core indicator and combines it with the fund management system to achieve dynamic adjustment of the entire position. The overall design focuses on risk control and the pursuit of stable returns.
#### Strategy Principle
The strategy uses the 20-period moving average as the central axis, and takes 2 times the standard deviation above and below to form a dynamic channel. When the price breaks through the lower track, it is regarded as an oversold signal, and the system buys the entire position; when the price breaks through the upper track, it is regarded as an overbought signal, and the system sells the entire position. Measure volatility through standard deviation to ensure the dynamic adaptability of trading signals. At the same time, the strategy integrates the fund management system and automatically adjusts the position size based on account equity. In addition, the strategy also includes an automated trading interface, which can realize automated execution with the exchange through WebHook.
#### Strategic Advantages
1. Strong dynamic adaptability: Bollinger Bands are based on standard deviation calculations and can automatically adjust the trading range according to market fluctuations to adapt to different market environments.
2. Improved risk management: adopt percentage position management, dynamically adjust the transaction scale according to account equity, and effectively control risks.
3. High degree of automation: Integrated exchange API interface, supports automatic execution of signals and reduces human intervention.
4. The strategy logic is clear: trading signals are determined based on the intersection of price and Bollinger Bands, and the judgment criteria are clear.
5. Excellent calculation efficiency: The core indicators are simple to calculate and suitable for high-frequency trading environments.
#### Strategy Risk
1. A volatile market is unfavorable: A volatile market can easily produce false signals, causing frequent trading.
2. Trend lag: The moving average is essentially a lagging indicator and may miss the best entry opportunity during sharp fluctuations.
3. Fund efficiency: The full-position trading method may lead to excessive capital utilization and increase risks.
4. Technical dependence: Automated execution depends on network and API stability, and there are technical risks.
#### Strategy optimization direction
1. Signal filtering: It is recommended to introduce trend confirmation indicators, such as MACD or RSI, to reduce false signals.
2. Position management: A progressive position building plan can be adopted to avoid the risk of a single full position operation.
3. Stop loss optimization: Add a trailing stop loss mechanism to improve profitability.
4. Parameter optimization: It is recommended to optimize the Bollinger Band parameters through backtesting to improve the stability of the strategy.
5. Market adaptation: A market status judgment module can be added to adopt different parameters in different market environments.
#### Summary
This strategy builds a complete quantitative trading system through Bollinger Bands technical indicators, combines fund management and automated execution, and has strong practicality. Although there are certain limitations, the stability and profitability of the strategy can be further improved through the suggested optimization directions. The strategy is suitable for volatile market environments and has reference value for investors pursuing stable returns.
|| 

#### Overview
This strategy is a quantitative trading system based on the Bollinger Bands indicator, capturing market trends through dynamic range breakthrough signals. The strategy uses standard deviation channels as core indicators, combined with a fund management system to achieve full position dynamic adjustment. The overall design focuses on risk control and pursuit of stable returns.

#### Strategy Principles
The strategy uses a 20-period moving average as the central axis, taking 2 times the standard deviation up and down to form dynamic channels. When the price breaks through the lower rail, it is seen as an oversold signal, and the system buys with full position; when the price breaks through the upper rail, it is seen as an overbought signal, and the system sells with full position. Volatility is measured through standard deviation to ensure the dynamic adaptability of trading signals. Meanwhile, the strategy integrates a fund management system, automatically adjusting position size according to account equity. Additionally, the strategy includes an automated trading interface that can achieve automated execution through WebHook with exchanges.

#### Strategy Advantages
1. Strong Dynamic Adaptability: Bollinger Bands, based on standard deviation calculations, can automatically adjust trading ranges according to market volatility, adapting to different market environments.
2. Comprehensive Risk Management: Uses percentage position management, dynamically adjusting trading size according to account equity, effectively controlling risk.
3. High Automation Level: Integrates exchange API interface, supports automatic signal execution, reducing human intervention.
4. Clear Strategy Logic: Determines trading signals based on price and Bollinger Bands crossovers, with clear judgment criteria.
5. Excellent Calculation Efficiency: Simple core indicator calculation, suitable for high-frequency trading environments.

#### Strategy Risks
1. Unfavorable in Oscillating Markets: Prone to false signals in sideways oscillating markets, causing frequent trading.
2. Trend Lag: Moving averages are inherently lagging indicators, possibly missing optimal entry timing during sharp fluctuations.
3. Capital Efficiency: Full position trading method may lead to excessive capital utilization, increasing risk.
4. Technical Dependence: Automated execution depends on network and API stability, posing technical risks.

#### Strategy Optimization Directions
1. Signal Filtering: Recommend introducing trend confirmation indicators, such as MACD or RSI, to reduce false signals.
2. Position Management: Can adopt progressive position building scheme to avoid single full position operation risk.
3. Stop Loss Optimization: Add trailing stop loss mechanism to improve profit capability.
4. Parameter Optimization: Recommend optimizing Bollinger Bands parameters through backtesting to improve strategy stability.
5. Market Adaptation: Can add market state judgment module to use different parameters in different market environments.

#### Summary
This strategy constructs a complete quantitative trading system through the Bollinger Bands technical indicator, combining fund management and automated execution, possessing strong practicality. Although there are certain limitations, through the suggested optimization directions, the strategy's stability and profitability can be further enhanced. The strategy is suitable for markets with higher volatility and has reference value for investors pursuing stable returns.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-26 00:00:00
end: 2024-12-25 08:00:00
period: 3h
basePeriod: 3h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands Strategy", overlay=true, initial_capital=86, default_qty_type=strategy.percent_of_equity)

// Parameter für die Bollinger-Bänder
length = input.int(20, title="Bollinger Bands Length")
mult = input.float(2.0, title="Bollinger Bands Multiplier")

// Berechnung der Bollinger-Bänder
basis = ta.sma(close, length)
upper = basis + mult * ta.stdev(close, length)
lower = basis - mult * ta.stdev(close, length)

// Startkapital
usdt_balance = 86.0 // Anfangsbetrag in USDT
zerebro_balance = 52.0 // Anfangsbetrag in ZEREBRO

// Bedingungen für Kauf- und Verkaufssignale
longCondition = ta.crossover(close, lower)
shortCondition = ta.crossunder(close, upper)

// Kauf- und Verkaufslogik
if (longCondition and usdt_balance > 0)
    strategy.entry("Buy", strategy.long, qty=usdt_balance / close)
    usdt_balance := 0 // Alle USDT werden verwendet
    zerebro_balance += strategy.position_size // Gekaufte ZEREBRO hinzufügen

if (shortCondition and zerebro_balance > 0)
    strategy.close("Buy")
    usdt_balance += strategy.position_size * close // Verkaufserlös in USDT
    zerebro_balance := 0 // Alle ZEREBRO verkauft

// Plot der Bollinger-Bänder
plot(basis, color=color.blue, title="Basis")
plot(upper, color=color.green, title="Upper Band")
plot(lower, color=color.red, title="Lower Band")

// Alerts für Bybit-Verbindung
alertcondition(longCondition, title="Buy Alert", message='{"action": "buy", "symbol": "ZEREBRO/USDT"}')
alertcondition(shortCondition, title="Sell Alert", message='{"action": "sell", "symbol": "ZEREBRO/USDT"}')

// Automatische Verknüpfung mit Bybit
// Stellen Sie sicher, dass Sie den Webhook-URL in TradingView einstellen und korrekt mit Bybit verbinden.


```

> Detail

https://www.fmz.com/strategy/476270

> Last Modified

2024-12-27 15:39:49
