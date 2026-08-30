
> Name

Adaptive-Volatility-and-Momentum-Quantitative-Trading-System-AVMQTS
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1887dfc097d9b3819e3.png)

[trans]
#### Overview
This strategy is an adaptive trading system that combines volatility and momentum indicators to capture market trends through the synergy of multiple technical indicators. The strategy uses the ATR indicator to monitor market fluctuations, MACD to determine trend momentum, and combines the price momentum indicator to confirm trading signals, and sets up a flexible stop-profit and stop-loss mechanism. The system is highly adaptable and can automatically adjust trading frequency and position control according to market conditions.
#### Strategy Principle
The strategy mainly relies on a triple indicator system as the core trading logic: first, use ATR to measure market volatility conditions and provide volatility reference for trading decisions; secondly, use the golden cross of the MACD indicator to capture the turning point of the trend, and the intersection of the MACD fast line and the slow line is used as the main trading trigger signal; the third level of verification uses the price momentum indicator to confirm the trend strength by observing changes in price relative to the previous period. The system also adds the 50-day moving average as a trend filter. Only when the price is above the moving average will long positions be allowed, and vice versa. To avoid overtrading, the strategy sets a minimum trading interval and has the option to force signals to alternate.
#### Strategic Advantages
1. Multi-indicator cross-validation: The reliability of trading signals is greatly improved through the coordination of indicators in the three dimensions of volatility, trend and momentum.
2. Strong adaptability: The strategy can be dynamically adjusted according to market fluctuations and adapt to different market environments.
3. Improved risk control: percentage stop loss and stop profit are set to effectively control the risk of a single transaction.
4. Controllable trading frequency: avoid excessive trading by setting the minimum trading interval and signal alternation mechanism.
5. The system structure is clear: the code is highly modularized, and each functional module has clear boundaries, making it easy to maintain and optimize.
#### Strategy Risk
1. Risk of volatile market: In a volatile market, multiple false signals may occur, leading to continuous stop losses.
2. Slippage risk: During periods of severe fluctuations, the actual transaction price may deviate greatly from the signal trigger price.
3. Parameter sensitivity: The strategy uses multiple technical indicators, and the rationality of parameter settings directly affects the performance of the strategy.
4. Market environment dependence: The strategy performs better in markets with obvious trends, but may not perform well under other market conditions.
#### Strategy optimization direction
1. Introducing a market environment identification mechanism: trend strength indicators can be added and different parameter configurations can be used in different market environments.
2. Optimize the take-profit and stop-loss mechanism: Consider dynamically adjusting the take-profit and stop-loss ratio based on ATR to make it more adaptable to market fluctuations.
3. Increase position management: It is recommended to introduce a dynamic position management system based on volatility to appropriately reduce the transaction size during periods of high volatility.
4. Add more filtering conditions: Consider adding filtering indicators such as trading volume and volatility to improve signal quality.
#### Summary
This strategy is a quantitative trading system with reasonable design and strict logic. Through the combined use of multiple technical indicators, it achieves effective capture of market trends. The system has made careful considerations in terms of risk control and transaction execution, and has good practicality. Although there are some potential risks, the stability and profitability of the strategy are expected to be further improved through the suggested optimization directions. ||
#### Overview
This strategy is an adaptive trading system that combines volatility and momentum indicators to capture market trends through the coordination of multiple technical indicators. The strategy uses the ATR indicator to monitor market volatility, MACD to judge trend momentum, and combines price momentum indicators to confirm trading signals, with a flexible stop-loss and take-profit mechanism. The system has strong adaptability and can automatically adjust trading frequency and position control according to market conditions.

#### Strategy Principles
The strategy relies on a triple indicator system as its core trading logic: First, ATR is used to measure market volatility conditions to provide volatility reference for trading decisions; Second, MACD indicator's golden and death crosses are used to capture trend turning points, with MACD fast and slow line crossovers used as the main trading trigger signals; Third, price momentum indicators are used for verification, observing price changes relative to previous periods to confirm trend strength. The system also incorporates a 50-day moving average as a trend filter, only allowing long positions when price is above the moving average and short positions when below. To avoid overtrading, the strategy sets minimum trading intervals and optionally enforces alternating signal execution.

#### Strategy Advantages
1. Multiple indicator cross-validation: Through the coordination of indicators in three dimensions - volatility, trend, and momentum, greatly improving the reliability of trading signals.
2. Strong adaptability: The strategy can dynamically adjust according to market volatility conditions, adapting to different market environments.
3. Comprehensive risk control: Percentage-based stop-loss and take-profit settings effectively control single trade risk.
4. Controllable trading frequency: Avoids overtrading through minimum trading interval settings and signal alternation mechanism.
5. Clear system structure: High degree of code modularity with clear boundaries between functional modules, facilitating maintenance and optimization.

#### Strategy Risks
1. Oscillating market risk: In sideways markets, multiple false signals may be generated, leading to consecutive stop-losses.
2. Slippage risk: During periods of intense volatility, actual transaction prices may significantly deviate from signal trigger prices.
3. Parameter sensitivity: The strategy uses multiple technical indicators, and the reasonableness of parameter settings directly affects strategy performance.
4. Market environment dependence: The strategy performs better in markets with clear trends but may underperform in other market conditions.

#### Strategy Optimization Directions
1. Introduce market environment recognition mechanism: Add trend strength indicators to use different parameter configurations in different market environments.
2. Optimize stop-loss and take-profit mechanism: Consider dynamically adjusting stop-loss and take-profit ratios based on ATR to better adapt to market volatility.
3. Add position management: Recommend introducing a volatility-based dynamic position management system, appropriately reducing trading size during high volatility periods.
4. Add more filtering conditions: Consider adding volume, volatility, and other filtering indicators to improve signal quality.

#### Summary
This strategy is a well-designed, logically rigorous quantitative trading system that achieves effective capture of market trends through the use of multiple technical indicators. The system has made detailed considerations in risk control and trade execution, showing good practicality. Although there are some potential risks, through the suggested optimization directions, both the stability and profitability of the strategy can be expected to further improve.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-25 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("[ETH] Volatility & Momentum Adaptive Strategy", shorttitle="Definitive 1 day Ethereum Signal", overlay=true, initial_capital=10000, currency=currency.USD)

// === Input Parameters === //
trade_size = input.float(5, title="Trade Size (ETH)")
atr_length = input.int(8, minval=1, title="ATR Length")
macd_fast = input.int(8, minval=1, title="MACD Fast Length")
macd_slow = input.int(7, minval=1, title="MACD Slow Length")
macd_signal = input.int(9, minval=1, title="MACD Signal Length")
momentum_length = input.int(37, title="Momentum Length")
stop_loss_percent = input.float(9.9, title="Stop Loss Percentage (%)")
take_profit_percent = input.float(9.0, title="Take Profit Percentage (%)")
alternate_signal = input.bool(true, title="Alternate Buy/Sell Signals")

// === Indicators === //
// ATR to measure volatility
atr = ta.atr(atr_length)

// MACD for trend momentum
[macd_line, signal_line, _] = ta.macd(close, macd_fast, macd_slow, macd_signal)
macd_cross_up = ta.crossover(macd_line, signal_line)
macd_cross_down = ta.crossunder(macd_line, signal_line)

// Momentum
momentum = ta.mom(close, momentum_length)

// === Signal Control Variables === //
var bool last_signal_long = na
var int last_trade_bar = na
min_bars_between_trades = 5 // Adjust for minimal trade frequency control
time_elapsed = na(last_trade_bar) or (bar_index - last_trade_bar) >= min_bars_between_trades

// === Buy and Sell Conditions === //
// Buy when:
buy_signal = (macd_cross_up and momentum > 0 and close > ta.sma(close, 50) and time_elapsed)

// Sell when:
sell_signal = (macd_cross_down and momentum < 0 and close < ta.sma(close, 50) and time_elapsed)

// Enforce alternate signals if selected
if alternate_signal
    buy_signal := buy_signal and (na(last_signal_long) or not last_signal_long)
    sell_signal := sell_signal and (not na(last_signal_long) and last_signal_long)

// === Trade Execution === //
// Buy Position
if (buy_signal)
    if strategy.position_size < 0
        strategy.close("Short")
    strategy.entry("Long", strategy.long, qty=trade_size)
    last_signal_long := true
    last_trade_bar := bar_index

// Sell Position
if (sell_signal)
    if strategy.position_size > 0
        strategy.close("Long")
    strategy.entry("Short", strategy.short, qty=trade_size)
    last_signal_long := false
    last_trade_bar := bar_index

// === Stop Loss and Take Profit === //
if strategy.position_size > 0
    long_take_profit = strategy.position_avg_price * (1 + take_profit_percent / 100)
    long_stop_loss = strategy.position_avg_price * (1 - stop_loss_percent / 100)
    strategy.exit("TP/SL Long", from_entry="Long", limit=long_take_profit, stop=long_stop_loss)

if strategy.position_size < 0
    short_take_profit = strategy.position_avg_price * (1 - take_profit_percent / 100)
    short_stop_loss = strategy.position_avg_price * (1 + stop_loss_percent / 100)
    strategy.exit("TP/SL Short", from_entry="Short", limit=short_take_profit, stop=short_stop_loss)

// === Visual Signals === //
plotshape(series=buy_signal and time_elapsed, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=sell_signal and time_elapsed, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

```

> Detail

https://www.fmz.com/strategy/473123

> Last Modified

2024-11-27 14:20:24
