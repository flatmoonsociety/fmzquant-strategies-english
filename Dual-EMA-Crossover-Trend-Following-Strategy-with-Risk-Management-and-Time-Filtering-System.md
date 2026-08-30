
> Name

Dual-EMA-Crossover-Trend-Following-Strategy-with-Risk-Management-and-Time-Filtering-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1dae60ec3dfc67abecc.png)

[trans]
#### Overview
This strategy is a complete trading system that combines double moving average crossover signals, stop-profit and stop-loss management, and time filtering. The core of the strategy is based on the intersection of fast and slow exponential moving averages (EMA) to capture market trends, and controls risks by setting take profit (Take Profit) and stop loss (Stop Loss). At the same time, the strategy also includes a time filter function, allowing traders to execute transactions within a specific time range.
#### Strategy Principle
Strategy operation is based on the following core mechanisms:
1. Use two exponential moving averages with different periods (default is 5 and 21)
2. When the fast EMA crosses the slow EMA upward, the system generates a long signal
3. When the fast EMA crosses the slow EMA downward, the system generates a short signal
4. Percentage stop loss and take profit levels are set for each trade
5. The trading direction can be flexibly configured as: long only, short only or two-way trading
6. Contains time filtering function to only execute transactions within the specified time range
7. The system will issue alerts at critical moments (opening a position, hitting stop loss/take profit)
#### Strategic Advantages
1. Systematic risk management: Provide clear risk control for each transaction through preset stop loss and take profit levels
2. Flexible parameter configuration: traders can adjust the EMA cycle and stop-loss and take-profit levels according to different market environments.
3. Free choice of direction: you can choose one-way or two-way trading to adapt to different market preferences
4. Time management ability: avoid trading during unfavorable periods through time filtering function
5. Real-time warning function: Help traders obtain trading signals and risk tips in a timely manner
6. Complete position management: The system automatically handles entry and exit without manual intervention.
#### Strategy Risk
1. Volatile market risk: False signals may be triggered frequently in sideways markets
2. Slippage risk: Severe market fluctuations may cause the actual stop-loss and take-profit prices to deviate from expectations.
3. Parameter sensitivity: The choice of EMA period has a greater impact on strategy performance
4. Trend dependence: Strategies may not perform well in non-trending markets
5. Money management risk: Fixed percentage stop loss may not be flexible enough under certain market conditions
#### Strategy optimization direction
1. Add market environment filtering:
   - Added volatility indicator to adapt to different market conditions
   - Introduced trend strength filter to avoid false breakouts
2. Dynamic parameter adjustment:
   - Dynamically adjust stop loss and take profit levels based on market volatility
   - Dynamically adjust the EMA period based on market trend strength
3. Enhance risk management:
   - Added trailing stop function to protect profits
   - Implement the mechanism of opening and reducing positions in batches
4. Improve entry accuracy:
   - Combined with volume indicators to confirm signal validity
   - Add other technical indicators as auxiliary confirmation
#### Summary
This is a well-designed trend following strategy that provides traders with a comprehensive trading solution by combining moving average systems, risk management and time filters. The strategy is highly configurable and suitable for traders with different risk preferences. There is room for further improvement of the strategy through the suggested optimization directions. The key is to adjust parameters based on actual market conditions and personal trading goals, and always maintain strict risk control.
||

#### Overview
This strategy is a complete trading system that combines dual EMA crossover signals, stop-loss/take-profit management, and time filtering. The core strategy is based on the crossover of fast and slow exponential moving averages (EMA) to capture market trends, with risk control through Take Profit and Stop Loss settings. Additionally, the strategy includes time filtering functionality that allows traders to execute trades within specific time ranges.

#### Strategy Principles
The strategy operates based on the following core mechanisms:
1. Uses two EMAs with different periods (default 5 and 21)
2. Generates long signals when fast EMA crosses above slow EMA
3. Generates short signals when fast EMA crosses below slow EMA
4. Each trade has percentage-based stop-loss and take-profit levels
5. Trading direction can be configured for: long-only, short-only, or both
6. Includes time filtering to execute trades only within specified timeframes
7. System generates alerts at key moments (entry, stop-loss/take-profit hits)

#### Strategy Advantages
1. Systematic risk management: Clear risk control through preset stop-loss and take-profit levels
2. Flexible parameter configuration: Traders can adjust EMA periods and risk levels
3. Directional freedom: Options for unidirectional or bidirectional trading
4. Time management capability: Avoids trading during unfavorable periods
5. Real-time alert system: Helps traders receive timely signals and risk notifications
6. Complete position management: Automated entry and exit without manual intervention

#### Strategy Risks
1. Choppy market risk: May generate frequent false signals in ranging markets
2. Slippage risk: Actual stop-loss/take-profit prices may deviate during high volatility
3. Parameter sensitivity: Strategy performance heavily depends on EMA period selection
4. Trend dependency: May underperform in non-trending markets
5. Money management risk: Fixed percentage stops may not be flexible enough in certain conditions

#### Optimization Directions
1. Add market environment filtering:
   - Incorporate volatility indicators for different market states
   - Implement trend strength filters to avoid false breakouts
2. Dynamic parameter adjustment:
   - Adjust stop-loss/take-profit levels based on market volatility
   - Modify EMA periods according to trend strength
3. Enhanced risk management:
   - Add trailing stop functionality to protect profits
   - Implement scaling in/out mechanisms
4. Improve entry precision:
   - Incorporate volume indicators to confirm signal validity
   - Add supplementary technical indicators for confirmation

#### Summary
This is a well-designed trend-following strategy that combines a moving average system, risk management, and time filtering to provide a comprehensive trading solution. The strategy offers high configurability, suitable for traders with different risk preferences. Through the suggested optimization directions, there is room for further improvement. The key is to adjust parameters based on actual market conditions and personal trading objectives while maintaining strict risk control. [/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Estrategia Cruce de EMAs con: Stop Loss, Take Profit, Días de Operación y Alertas (Modificables)", overlay=true, commission_value = 0.2, process_orders_on_close = true, initial_capital = 1000)

// Parámetros de las EMAs
emaRapidaLen = input.int(5, title="Periodo EMA rápida")
emaLentaLen = input.int(21, title="Periodo EMA lenta")

// Parámetros de Stop Loss y Take Profit
stopLoss = input.float(3.0, title="Stop Loss (%)", step=0.1) / 100
takeProfit = input.float(6.0, title="Take Profit (%)", step=0.1) / 100

// Tipo de operación: Largo, Corto o Ambos
operacion = input.string(title="Tipo de operación", defval="Largo", options=["Largo", "Corto", "Ambos"])

// Parámetros de la duración de la estrategia (días)
diasInicio = input(timestamp("2009-01-03 00:00"), title="Fecha de inicio (YYYY-MM-DD HH:MM)")
diasFin = input(timestamp("2024-09-11 00:00"), title="Fecha de fin (YYYY-MM-DD HH:MM)")

// Comprobar si estamos dentro del rango de días definido
dentroDeRango = true

// Cálculo de las EMAs
emaRapida = ta.ema(close, emaRapidaLen)
emaLenta = ta.ema(close, emaLentaLen)

// Condiciones para cruce de EMAs
cruceAlcista = ta.crossover(emaRapida, emaLenta)
cruceBajista = ta.crossunder(emaRapida, emaLenta)

// Operaciones en Largo (solo si estamos en el rango de días definido)
if dentroDeRango and (operacion == "Largo" or operacion == "Ambos") and cruceAlcista 
    strategy.entry("Compra", strategy.long)
    alert("Posición larga abierta: Cruce alcista de EMAs", alert.freq_once_per_bar_close)

// Operaciones en Corto (solo si estamos en el rango de días definido)
if dentroDeRango and (operacion == "Corto" or operacion == "Ambos") and cruceBajista
    strategy.entry("Venta", strategy.short)
    alert("Posición corta abierta: Cruce bajista de EMAs", alert.freq_once_per_bar_close)

// Cálculo del Stop Loss y Take Profit para largos
if (strategy.position_size > 0 and strategy.opentrades.entry_id(strategy.opentrades - 1) == "Compra")
    strategy.exit("Cerrar Compra", "Compra", stop=strategy.position_avg_price * (1 - stopLoss), limit=strategy.position_avg_price * (1 + takeProfit))
    alert("Posición larga cerrada: Alcanzado Stop Loss o Take Profit", alert.freq_once_per_bar_close)

// Cálculo del Stop Loss y Take Profit para cortos
if (strategy.position_size < 0 and strategy.opentrades.entry_id(strategy.opentrades - 1) == "Venta")
    strategy.exit("Cerrar Venta", "Venta", stop=strategy.position_avg_price * (1 + stopLoss), limit=strategy.position_avg_price * (1 - takeProfit))
    alert("Posición corta cerrada: Alcanzado Stop Loss o Take Profit", alert.freq_once_per_bar_close)

// Plot de las EMAs
plot(emaRapida, color=color.blue, title="EMA rápida", linewidth = 2)
plot(emaLenta, color=color.red, title="EMA lenta", linewidth = 2)

```

> Detail

https://www.fmz.com/strategy/473355

> Last Modified

2024-11-29 15:05:45
