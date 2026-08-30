
> Name

Dynamic-Trailing-Stop-Dual-Target-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/297ac396bdca3088148fd1f8da3c72a5703f659844726f65a32d33ca7d4b15be.png)

[trans]
#### Overview
This strategy is a trading system based on moving average crossover, which combines the risk management method of dynamic moving stop loss and dual target profit points. The strategy mainly determines the entry timing based on the intersection of price and the 200-period moving average, and also sets flexible stop loss and profit points to achieve risk control and profit maximization.
#### Strategy Principle
1. Entry signals:
   - Long entry: when price crosses the 200-period moving average upwards
   - Short entry: when the price crosses the 200-period moving average downwards
2. Risk management:
   - Initial stop loss: set 500 pips beyond the entry price
   - Dynamic trailing stop loss: When the price moves 200 points in a favorable direction, the stop loss will move to the entry price   
3. Profit target:
   - The first goal: when the price reaches 3000 points of the entry price, close 75% of the position
   - Second goal: The remaining 25% of the position will be closed when the price reaches 4000 points of the entry price
   - If dynamic trailing stop is triggered, the stop loss point of the remaining position will be set at the entry price
4. Position management:
   - Fixed quantity of 100 units per transaction
#### Strategic Advantages
1. Trend following: Using moving averages to capture market trends can help make profits in the general trend.
2. Risk control: Using a combination of initial stop loss and dynamic moving stop loss, it not only limits the maximum loss, but also protects the profits earned.
3. Profit maximization: By setting two target prices, you can continue to track the general trend while ensuring part of the profit.
4. Automation: The strategy is completely automated, reducing human emotional interference.
5. Flexibility: Various parameters such as moving average period, stop loss point, profit point, etc. can be adjusted according to market conditions.
#### Strategy Risk
1. Risk of volatile markets: In a volatile market, false breakthrough signals may be triggered frequently, leading to continuous losses.
2. Slippage risk: In rapid market conditions, the actual transaction price may deviate greatly from the ideal price.
3. Over-trading: Frequent cross signals may lead to over-trading and increase transaction costs.
4. Reliance on a single indicator: Relying solely on moving averages may ignore other important market information.
5. Fixed position risk: Fixed quantities for each transaction may not be suitable for all market environments.
#### Strategy optimization direction
1. Combination of multiple indicators: Consider introducing other technical indicators such as RSI, MACD, etc., and use them in conjunction with moving averages to improve the reliability of entry signals.
2. Dynamic position management: Dynamically adjust the number of transactions based on market volatility and account balance to better control risks.
3. Market environment filtering: Add trend strength indicators or volatility indicators to avoid entering the market in market environments that are not suitable for trading.
4. Parameter optimization: Use historical data to backtest different parameter combinations to find the optimal moving average cycle, stop loss point and profit point settings.
5. Time filter: Consider adding a time filter to avoid trading during periods of greater volatility or poor liquidity.
6. Add fundamental factors: Adjust the entry and exit timing of the strategy based on the release of important economic data or other fundamental events.
#### Summarize
The dynamic moving stop dual target price and moving average crossover strategy is a quantitative trading system that combines technical analysis and risk management. Capture market trends with moving averages, while leveraging dynamic stops and multiple profit targets to balance risk and reward. The main advantages of this strategy are its high degree of automation, flexible risk control, and the potential to obtain considerable returns in strong trending markets. However, users need to pay attention to the risks of volatile markets and consider further optimizing the strategy to improve its adaptability and stability. By continuously adjusting parameters, introducing additional market indicators, and considering more complex position management methods, the strategy is expected to achieve better performance in various market environments.
|| 

#### Overview

This strategy is a trading system based on moving average crossovers, combining dynamic trailing stops and dual profit targets for risk management. The strategy primarily uses the crossover of price with a 200-period moving average to determine entry points, while implementing flexible stop-loss and take-profit levels to achieve risk control and profit maximization.

#### Strategy Principles

1. Entry Signals:
   - Long Entry: When price crosses above the 200-period moving average
   - Short Entry: When price crosses below the 200-period moving average

2. Risk Management:
   - Initial Stop Loss: Set 500 points away from the entry price
   - Dynamic Trailing Stop: When price moves 200 points in the favorable direction, the stop loss is moved to the entry price
   
3. Profit Targets:
   - First Target: When price reaches 3000 points from the entry, 75% of the position is closed
   - Second Target: The remaining 25% of the position is closed when price reaches 4000 points from the entry
   - If the dynamic trailing stop is triggered, the stop loss for the remaining position is set at the entry price

4. Position Management:
   - Fixed quantity of 100 units per trade

#### Strategy Advantages

1. Trend Following: Utilizes moving averages to capture market trends, aiding in profiting from major market movements.

2. Risk Control: Combines initial stop loss with dynamic trailing stop, limiting maximum loss while protecting accrued profits.

3. Profit Maximization: By setting two target prices, it secures partial profits while continuing to track larger trends.

4. Automation: The strategy is fully automated, reducing emotional interference in trading decisions.

5. Flexibility: Various parameters such as moving average period, stop loss points, and profit targets can be adjusted according to market conditions.

#### Strategy Risks

1. Choppy Market Risk: In range-bound, oscillating markets, frequent false breakout signals may lead to consecutive losses.

2. Slippage Risk: In fast-moving markets, actual execution prices may significantly deviate from ideal prices.

3. Overtrading: Frequent crossover signals may result in excessive trading, increasing transaction costs.

4. Single Indicator Dependency: Relying solely on moving averages may overlook other important market information.

5. Fixed Position Risk: Trading a fixed quantity for each trade may not be suitable for all market environments.

#### Strategy Optimization Directions

1. Multi-Indicator Integration: Consider introducing other technical indicators such as RSI, MACD, etc., to be used in conjunction with moving averages to improve entry signal reliability.

2. Dynamic Position Sizing: Adjust trading quantity based on market volatility and account balance to better control risk.

3. Market Environment Filtering: Add trend strength or volatility indicators to avoid entries in unfavorable market conditions.

4. Parameter Optimization: Use historical data to backtest different parameter combinations to find optimal settings for moving average periods, stop loss points, and profit targets.

5. Time Filtering: Consider adding time filters to avoid trading during highly volatile or low liquidity periods.

6. Fundamental Factor Integration: Incorporate important economic data releases or other fundamental events to adjust strategy entry and exit timing.

#### Conclusion

The Dynamic Trailing Stop Dual Target Moving Average Crossover Strategy is a quantitative trading system that combines technical analysis with risk management. It captures market trends using moving averages while balancing risk and reward through dynamic stop losses and multiple profit targets. The strategy's main advantages lie in its high degree of automation, flexible risk control, and potential for significant returns in strong trend markets. However, users need to be aware of the risks in choppy markets and consider further optimizations to improve adaptability and stability. Through continuous parameter adjustment, introduction of additional market indicators, and consideration of more complex position management methods, this strategy has the potential to perform well in various market environments.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-07-29 00:00:00
end: 2024-07-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("SOL/USDT Trading Strategy", overlay=true)

// Параметры стратегии
input_quantity = input(2, title="Trade Size (SOL)")
stop_loss_points = input(500, title="Stop Loss Points")
take_profit_points_1 = input(3000, title="First Take Profit Points")
take_profit_points_2 = input(4000, title="Second Take Profit Points")
move_stop_to_entry_points = input(200, title="Move Stop to Entry Points")
ma_period = input(180, title="MA Period")

// Расчет скользящей средней
ma = ta.sma(close, ma_period)

// Условия входа в сделку
long_condition = ta.crossover(close, ma)
short_condition = ta.crossunder(close, ma)

// Текущая цена
var float entry_price = na

// Логика открытия и закрытия сделок
if (long_condition)
    entry_price := close
    strategy.entry("Long", strategy.long, qty=input_quantity)
if (short_condition)
    entry_price := close
    strategy.entry("Short", strategy.short, qty=input_quantity)

// Логика выхода из сделок
if (strategy.position_size > 0)
    if (close >= entry_price + take_profit_points_1 * syminfo.mintick)
        strategy.exit("Partial Take Profit", "Long", qty=0.75 * input_quantity, limit=close)
        strategy.exit("Remaining Take Profit", "Long", qty=0.25 * input_quantity, limit=entry_price + take_profit_points_2 * syminfo.mintick, stop=entry_price)

    if (close >= entry_price + move_stop_to_entry_points * syminfo.mintick)
        strategy.exit("Stop Loss at Entry", "Long", qty=strategy.position_size, stop=entry_price)
    else
        strategy.exit("Take Profit/Stop Loss", "Long", stop=entry_price - stop_loss_points * syminfo.mintick, limit=entry_price + take_profit_points_1 * syminfo.mintick)

if (strategy.position_size < 0)
    if (close <= entry_price - take_profit_points_1 * syminfo.mintick)
        strategy.exit("Partial Take Profit", "Short", qty=0.75 * input_quantity, limit=close)
        strategy.exit("Remaining Take Profit", "Short", qty=0.25 * input_quantity, limit=entry_price - take_profit_points_2 * syminfo.mintick, stop=entry_price)

    if (close <= entry_price - move_stop_to_entry_points * syminfo.mintick)
        strategy.exit("Stop Loss at Entry", "Short", qty=strategy.position_size, stop=entry_price)
    else
        strategy.exit("Take Profit/Stop Loss", "Short", stop=entry_price + stop_loss_points * syminfo.mintick, limit=entry_price - take_profit_points_1 * syminfo.mintick)

// Отображение скользящей средней
plot(ma, title="200 MA", color=color.blue)

```

> Detail

https://www.fmz.com/strategy/458045

> Last Modified

2024-07-29 14:40:23
