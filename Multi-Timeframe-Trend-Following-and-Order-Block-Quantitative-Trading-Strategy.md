
> Name

Quantitative trading strategy that combines multi-timeframe trend tracking and order block-Multi-Timeframe-Trend-Following-and-Order-Block-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/26a625fbbc4d59a01bbbdb406ac1af66587494ed311d2a62c829313dd91d2326.png)

[trans]
#### Overview
This is a complex quantitative trading strategy that combines multiple technical indicators and trading concepts. This strategy is mainly based on order block (Order Block), trend change detection, moving average crossover and multi-time frame analysis to generate trading signals. The core idea of ​​the strategy is to use the price action and technical indicators of the smaller time frame (5 minutes) to accurately enter and exit in the trend direction of the larger time frame (1 hour).
#### Strategy Principle
1. Order Block: The strategy uses a custom function to calculate the order block, which is an important price level and usually represents the concentrated area of ​​large institutional orders.
2. Trend change detection: Use simple moving average (SMA) crossovers to identify potential trend changes.
3. Multi-time frame analysis: Calculates 50-period and 200-period exponential moving averages (EMA) on the 1-hour time frame for determining larger market trends.
4. Admission conditions:
   - Long: When an uptrend signal appears on the 5-minute chart, the price breaks out of the order block, and the 50EMA is above the 200EMA on the 1-hour chart.
   - Short: When a downtrend signal appears on the 5-minute chart, the price falls below the order block, and the 50EMA is below the 200EMA on the 1-hour chart.
5. Exit strategy: Use fixed percentage take-profit and stop-loss levels to manage risk and lock in profits.
#### Strategic Advantages
1. Multi-dimensional analysis: combines multiple time frames and technical indicators to provide a more comprehensive market perspective.
2. Trend following: By trading in the direction of the general trend, the probability of profit is increased.
3. Precise entry: Use order blocks and short-term trend changes to optimize entry timing.
4. Risk management: Use preset take-profit and stop-loss percentages to effectively control the risk of each transaction.
5. Strong adaptability: The strategy parameters are adjustable and can adapt to different market environments.
#### Strategy Risk
1. Excessive trading: In a volatile market, frequent trading signals may be generated, increasing transaction costs.
2. Slippage risk: In a market with poor liquidity, the actual execution price may deviate greatly from the ideal price.
3. Trend reversal risk: Near the trend turning point, the strategy may suffer continuous losses.
4. Parameter sensitivity: Strategy performance may be highly sensitive to parameter settings and requires continuous optimization.
5. Market environment dependence: In sideways markets or rapidly volatile markets, the strategy may not be effective.
#### Strategy optimization direction
1. Dynamic parameter adjustment: Consider automatically adjusting the stop-profit and stop-loss percentages based on market volatility.
2. Add filters: Introduce additional technical indicators or market sentiment indicators to reduce false signals.
3. Time filtering: Add trading time window restrictions to avoid low liquidity periods.
4. Position management: Implement more complex position management strategies, such as volatility-based position adjustments.
5. Backtesting and optimization: Conduct more extensive historical data backtesting to find the optimal parameter combination.
6. Increase market environment recognition: Develop algorithms to identify different market states and adjust strategies accordingly.
#### Summarize
This is a comprehensive and logically complex quantitative trading strategy that combines multi-time frame analysis, order block theory and trend tracking technology. Strategies are designed to increase the success rate of trades by finding precise entry points in the direction of the general trend. However, due to its complexity, the strategy also faces challenges such as overfitting and parameter sensitivity. Future optimization should focus on improving the adaptability and robustness of the strategy, including dynamic parameter adjustment, adding filters, and more sophisticated position management methods. Overall, this strategy provides a good framework for high-frequency trading, but requires careful implementation and ongoing monitoring and adjustment.
|| 

#### Overview

This is a complex quantitative trading strategy that combines multiple technical indicators and trading concepts. The strategy is primarily based on Order Block, trend change detection, moving average crossovers, and multi-timeframe analysis to generate trading signals. The core idea is to use price action and technical indicators on a smaller timeframe (5 minutes) to precisely enter and exit trades in the direction of the trend on a larger timeframe (1 hour).

#### Strategy Principles

1. Order Block: The strategy uses a custom function to calculate the Order Block, which is a significant price level typically representing areas of concentrated institutional orders.

2. Trend Change Detection: Uses crossovers of a Simple Moving Average (SMA) to identify potential trend changes.

3. Multi-Timeframe Analysis: Calculates 50-period and 200-period Exponential Moving Averages (EMA) on a 1-hour timeframe to determine the broader market trend.

4. Entry Conditions:
   - Long: When an uptrend signal appears on the 5-minute chart, price breaks above the Order Block, and the 50 EMA is above the 200 EMA on the 1-hour chart.
   - Short: When a downtrend signal appears on the 5-minute chart, price breaks below the Order Block, and the 50 EMA is below the 200 EMA on the 1-hour chart.

5. Exit Strategy: Uses fixed percentage take-profit and stop-loss levels to manage risk and lock in profits.

#### Strategy Advantages

1. Multi-dimensional Analysis: Combines multiple timeframes and technical indicators, providing a more comprehensive market perspective.

2. Trend Following: By trading in the direction of the larger trend, it increases the probability of profitable trades.

3. Precise Entries: Utilizes Order Blocks and short-term trend changes to optimize entry timing.

4. Risk Management: Employs preset take-profit and stop-loss percentages, effectively controlling risk for each trade.

5. Adaptability: Strategy parameters can be adjusted to adapt to different market environments.

#### Strategy Risks

1. Overtrading: May generate frequent trading signals in highly volatile markets, increasing transaction costs.

2. Slippage Risk: In less liquid markets, actual execution prices may deviate significantly from ideal prices.

3. Trend Reversal Risk: The strategy may suffer consecutive losses near trend turning points.

4. Parameter Sensitivity: Strategy performance may be highly sensitive to parameter settings, requiring continuous optimization.

5. Market Environment Dependency: The strategy may not perform well in ranging or rapidly oscillating markets.

#### Strategy Optimization Directions

1. Dynamic Parameter Adjustment: Consider automatically adjusting take-profit and stop-loss percentages based on market volatility.

2. Additional Filters: Introduce extra technical or market sentiment indicators to reduce false signals.

3. Time Filtering: Add trading time window restrictions to avoid low liquidity periods.

4. Position Management: Implement more sophisticated position management strategies, such as volatility-based position sizing.

5. Backtesting and Optimization: Conduct more extensive historical data backtesting to find optimal parameter combinations.

6. Market Environment Recognition: Develop algorithms to identify different market states and adjust the strategy accordingly.

#### Summary

This is a comprehensive and logically complex quantitative trading strategy that combines multi-timeframe analysis, Order Block theory, and trend-following techniques. By seeking precise entry points in the direction of the larger trend, the strategy aims to improve the success rate of trades. However, due to its complexity, the strategy also faces challenges such as overfitting and parameter sensitivity. Future optimizations should focus on improving the strategy's adaptability and robustness, including dynamic parameter adjustment, additional filters, and more sophisticated position management methods. Overall, this strategy provides an excellent framework for high-frequency trading but requires careful implementation and continuous monitoring and adjustment.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-06-28 00:00:00
end: 2024-07-28 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("S&P 500", overlay=true)
// Parámetros
length = input(14, "Longitud")
src = input(close, "Fuente")
profit_percent = input.float(0.08955, "Porcentaje de ganancia", step=0.00001, minval=0)
stop_loss_percent = input.float(0.04477, "Porcentaje de stop loss", step=0.00001, minval=0)
// Función para calcular el Order Block
order_block(src, len) =>
    highest = ta.highest(high, len)
    lowest = ta.lowest(low, len)
    mid = (highest + lowest) / 2
    ob = src > mid ? highest : lowest
    ob
// Cálculo del Order Block
ob = order_block(src, length)
// Función para detectar cambios de tendencia
trend_change(src, len) =>
    up = ta.crossover(src, ta.sma(src, len))
    down = ta.crossunder(src, ta.sma(src, len))
    [up, down]
// Detectar cambios de tendencia
[trend_up, trend_down] = trend_change(src, length)
// Calcular EMA 50 y EMA 200 en timeframe de 1 hora
ema50_1h = request.security(syminfo.tickerid, "60", ta.ema(close, 50))
ema200_1h = request.security(syminfo.tickerid, "60", ta.ema(close, 200))
// Condiciones de EMA
ema_buy_condition = ema50_1h > ema200_1h
ema_sell_condition = ema50_1h < ema200_1h
// Señales de compra y venta
buy_signal = trend_up and close > ob and ema_buy_condition
sell_signal = trend_down and close < ob and ema_sell_condition
// Ejecutar la estrategia
if (buy_signal)
    strategy.entry("Compra", strategy.long)
if (sell_signal)
    strategy.entry("Venta", strategy.short)
// Calcular precios de toma de ganancias y stop loss
if (strategy.position_size != 0)
    entry_price = strategy.position_avg_price
    is_long = strategy.position_size > 0
    take_profit = entry_price * (1 + (is_long ? 1 : -1) * profit_percent / 100)
    stop_loss = entry_price * (1 + (is_long ? -1 : 1) * stop_loss_percent / 100)
    strategy.exit(is_long ? "Long TP/SL" : "Short TP/SL", limit=take_profit, stop=stop_loss)
// Visualización
plot(ob, "Order Block", color.purple, 2)
plot(ta.sma(src, length), "SMA", color.blue)
plot(ema50_1h, "EMA 50 1h", color.yellow)
plot(ema200_1h, "EMA 200 1h", color.white)
bgcolor(buy_signal ? color.new(color.green, 90) : sell_signal ? color.new(color.red, 90) : na)
```

> Detail

https://www.fmz.com/strategy/458033

> Last Modified

2024-07-29 13:57:12
