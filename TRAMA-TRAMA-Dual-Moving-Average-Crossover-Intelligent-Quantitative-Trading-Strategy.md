
> Name

TRAMA Dual-Moving-Average-Crossover-Intelligent-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b96cda544c89fb0d25.png)

[trans]
#### Overview
This is an intelligent quantitative trading strategy based on TRAMA (Triangular Moving Average) and Simple Moving Average (SMA). The strategy combines two moving average systems to generate trading signals, and sets a stop-profit and stop-loss mechanism to control risks. This strategy uses 4-period and 28-period SMA crossovers and TRAMA indicators to confirm trading signals, and improves the accuracy of trading through multiple signal confirmations.
#### Strategy Principle
The strategy uses two core components to generate trading signals. The first is a crossover system based on the 4-period and 28-period SMA. When the short-term moving average crosses the long-term moving average upward, a long signal is generated, and when the short-term moving average crosses downward, a short signal is generated. Secondly, the strategy introduces the TRAMA indicator as an auxiliary confirmation system. TRAMA is a modified moving average with faster response and lower lag. When price breaks above TRAMA, additional trading signals are generated. The strategy also sets a percentage-based take-profit and stop-loss mechanism, which are 2% take-profit and 1% stop-loss.
#### Strategic Advantages
1. The dual signal confirmation mechanism significantly improves the reliability of transactions
2. TRAMA indicator can capture changes in market trends more quickly
3. Have a clear risk control mechanism and protect funds through stop-profit and stop-loss
4. The strategy logic is clear and easy to understand and maintain.
5. Long and short two-way transactions can be carried out at the same time, increasing profit opportunities.
#### Strategy Risk
1. Too many trading signals may be generated in volatile markets
2. Fixed take-profit and stop-loss ratios may not be suitable for all market environments
3. Short-term moving averages may be more sensitive to price noise
4. Possible risk of slippage in highly volatile markets
5. The impact of transaction costs on strategy performance needs to be considered
#### Strategy optimization direction
1. Introducing a volatility-adaptive stop-profit and stop-loss mechanism
2. Add market environment filters and adjust strategy parameters under different market conditions
3. Optimize the selection method of TRAMA parameters and consider using adaptive cycles
4. Add transaction volume confirmation indicator to improve signal reliability
5. Consider adding a trend strength filter to avoid trading in weak trends
#### Summary
This is a strategy that combines traditional technical analysis with modern quantitative trading concepts. Through multiple signal confirmations and strict risk control, the strategy shows good practicality. Although there are some areas that need optimization, the overall framework design is reasonable and has good application prospects. It is recommended that traders conduct sufficient historical data backtesting and parameter optimization before using it in real trading. ||
#### Overview
This is an intelligent quantitative trading strategy based on TRAMA (Triangular Moving Average) and Simple Moving Average (SMA). The strategy combines two moving average systems for generating trading signals and implements a stop-loss/take-profit mechanism for risk control. It uses 4-period and 28-period SMA crossovers along with the TRAMA indicator to confirm trading signals, improving accuracy through multiple signal confirmation.

#### Strategy Principles
The strategy employs two core components for generating trading signals. First is the crossover system based on 4-period and 28-period SMAs, generating long signals when the short-term MA crosses above the long-term MA, and short signals when it crosses below. Second, the strategy incorporates the TRAMA indicator as an auxiliary confirmation system. TRAMA is an improved moving average with faster response time and less lag. Additional trading signals are generated when price breaks through the TRAMA. The strategy also includes percentage-based take-profit and stop-loss mechanisms set at 2% and 1% respectively.

#### Strategy Advantages
1. Dual signal confirmation mechanism significantly improves trading reliability
2. TRAMA indicator enables faster capture of market trend changes
3. Clear risk control mechanism through stop-loss and take-profit levels
4. Clear and easy-to-maintain strategy logic
5. Enables both long and short trading, increasing profit opportunities

#### Strategy Risks
1. May generate excessive trading signals in ranging markets
2. Fixed stop-loss and take-profit percentages may not suit all market conditions
3. Short-term moving average may be sensitive to price noise
4. Potential slippage risks in volatile markets
5. Need to consider the impact of trading costs on strategy performance

#### Strategy Optimization Directions
1. Introduce volatility-adaptive stop-loss and take-profit mechanisms
2. Add market environment filters to adjust strategy parameters under different conditions
3. Optimize TRAMA parameter selection method, consider using adaptive periods
4. Add volume confirmation indicators to improve signal reliability
5. Consider adding trend strength filters to avoid trading in weak trends

#### Summary
This is a strategy that combines traditional technical analysis with modern quantitative trading concepts. Through multiple signal confirmation and strict risk control, the strategy demonstrates good practicality. While there are areas for optimization, the overall framework design is reasonable with good application prospects. Traders are advised to conduct thorough historical data backtesting and parameter optimization before live trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ivanvallejoc

//@version=5
strategy("MANCOS2.0", overlay=true, margin_long=80, margin_short=80)

longCondition = ta.crossover(ta.sma(close, 4), ta.sma(close, 28))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = ta.crossunder(ta.sma(close, 4), ta.sma(close, 28))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)

// Parámetros de la TRAMA
length = input(1.5, title="TRAMA Length")
src = close
filt = 2 / (length + 1)
trama = 0.0
var tramaPrev = na(trama[1]) ? close : trama[1]
trama := (src - tramaPrev) * filt + tramaPrev

// Plot de la TRAMA
plot(trama, color=color.blue, linewidth=2, title="TRAMA")

// Señales de compra y venta basadas en TRAMA
buySignal = ta.crossover(close, trama)
sellSignal = ta.crossunder(close, trama)

// Configuración de Take Profit y Stop Loss
takeProfitPerc = input(2, title="Take Profit (%)") / 100
stopLossPerc = input(1, title="Stop Loss (%)") / 100

// Precios de TP y SL
takeProfitPrice = strategy.position_avg_price * (1 + takeProfitPerc)
stopLossPrice = strategy.position_avg_price * (1 - stopLossPerc)

// Condiciones de entrada en largo
if (buySignal)
    strategy.entry("Long", strategy.long)

// Condiciones de salida para posición larga (TP/SL)
if (strategy.position_size > 0)
    strategy.exit("TP/SL", "Long", limit=takeProfitPrice, stop=stopLossPrice)

// Entrada en corto basada en TRAMA
if (sellSignal)
    strategy.entry("Short", strategy.short)

// Precios de TP y SL para posiciones cortas
takeProfitPriceShort = strategy.position_avg_price * (1 - takeProfitPerc)
stopLossPriceShort = strategy.position_avg_price * (1 + stopLossPerc)

if (strategy.position_size < 0)
    strategy.exit("TP/SL", "Short", limit=takeProfitPriceShort, stop=stopLossPriceShort)

```

> Detail

https://www.fmz.com/strategy/473362

> Last Modified

2024-11-29 15:25:13
