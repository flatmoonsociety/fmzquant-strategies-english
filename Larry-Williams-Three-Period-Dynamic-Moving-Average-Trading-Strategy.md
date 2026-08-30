
> Name

Larry Williams Three-Period Dynamic Moving Average Trading Strategy-Larry-Williams-Three-Period-Dynamic-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/116475a349ea13a1aa7.png)

[trans]
#### Overview
This article introduces a trading strategy based on the Larry Williams three-period dynamic moving average. This strategy uses two exponential moving averages (EMA) to capture price trends, and generates trading signals when the closing prices of three consecutive K lines exceed the EMA. The strategy parameters are adjustable and suitable for different markets and cycles.
#### Strategy Principle
1. Calculate two EMAs: the high price EMA and the low price EMA of the closing price, with adjustable periods.
2. Determine whether the current time is within the set trading range.  
3. Determine whether the last three K lines have continuously closed above the EMA (bullish) or below (bearish).
4. If 3 is true and the position is 0, open a long position; if the opposite of 3 is true and the position is long, close the position.
5. If you hold a position at the close of the day, it will be closed.
#### Strategic Advantages
1. Flexible parameters: EMA cycle, trading time interval and other parameters are adjustable to adapt to different markets.
2. Trend following: Using the direction of EMA and continuous K-line to judge the trend is helpful to capture the trend market.
3. Stop loss in time: close the position immediately when it breaks through EMA against the trend and control the retracement.
4. Close positions within the day: close positions at the close to avoid overnight risks.
#### Strategy Risk
1. Risk of volatile market: When the trend is unclear, frequent trading may lead to losses.
2. Parameter risk: Different parameters perform differently in different markets and require targeted optimization.
3. Gap risk: A gap at the opening may lead to a spread in the opening price of the strategy, increasing the risk.
#### Strategy optimization direction
1. Trend filtering: Add ATR, RSI and other indicators to assist in judging the strength of the trend and avoid volatile markets.
2. Dynamic parameter optimization: dynamically adjust parameters according to recent market characteristics to improve adaptability.
3. Position management: Adjust positions according to the strength of the trend and capital conditions to control risks.
4. Add stop-loss and take-profit: set reasonable stop-loss levels and take-profit targets to reduce the risk of a single transaction.
#### Summary
Larry Williams' three-period dynamic moving average trading strategy is a trend following strategy based on double EMA and continuous K-line direction, which can be adapted to different markets through parameter optimization. However, the strategy itself is relatively simple, performs poorly in volatile markets, and lacks risk control measures, so it needs further optimization and improvement. Taking into account the advantages and disadvantages of the strategy, this strategy is more suitable for use in markets with clear trends, and is combined with position management and risk control measures to improve overall performance and stability.
|| 

#### Overview
This article introduces a trading strategy based on Larry Williams' three-period dynamic moving average. The strategy utilizes two exponential moving averages (EMAs) to capture price trends and generates trading signals when the closing price of three consecutive candles breaks through the EMAs. The strategy parameters are adjustable and suitable for different markets and timeframes.

#### Strategy Principles
1. Calculate two EMAs: high price EMA and low price EMA of closing prices, with adjustable periods.
2. Determine if the current time is within the set trading interval.
3. Determine if the last three candles consecutively closed above (bullish) or below (bearish) the EMAs.
4. If condition 3 is met and the position is 0, open a long position; if the opposite of condition 3 is met and a long position is held, close the position.
5. Close the position at the end of each trading day if holding a position.

#### Strategy Advantages
1. Flexible parameters: EMA periods, trading time intervals, and other parameters are adjustable to adapt to different markets.
2. Trend tracking: Utilizes EMAs and the direction of consecutive candles to identify trends, which helps capture trending markets.
3. Timely stop-loss: Immediately closes the position when the price breaks through the EMAs against the trend, controlling drawdowns.
4. Intraday position closing: Closes positions at the end of each trading day, avoiding overnight risks.

#### Strategy Risks
1. Choppy market risk: Frequent trading in trendless markets may lead to losses.
2. Parameter risk: Performance varies greatly with different parameters in different markets, requiring targeted optimization.
3. Gap risk: Opening gaps may cause slippage in the strategy's entry price, increasing risk.

#### Strategy Optimization Directions
1. Trend filters: Incorporate indicators like ATR and RSI to help assess trend strength and avoid choppy markets.
2. Dynamic parameter optimization: Dynamically adjust parameters based on recent market characteristics to improve adaptability.
3. Position management: Adjust positions based on trend strength and capital, controlling risks.
4. Incorporate stop-loss and profit-taking: Set reasonable stop-loss levels and profit targets to reduce single-trade risk.

#### Summary
Larry Williams' three-period dynamic moving average trading strategy is a trend-following strategy based on dual EMAs and the direction of consecutive candles. With parameter optimization, it can adapt to different markets. However, the strategy itself is relatively simple, performs poorly in choppy markets, and lacks risk control measures, requiring further optimization and improvement. Considering the strategy's pros and cons, it is more suitable for use in markets with clear trends and should be combined with position management and risk control measures to improve overall performance and stability.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-05 00:00:00
end: 2024-05-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Larry Williams 3 Periodos Editável de MarcosJr", overlay=true, process_orders_on_close=true)

// Parametrização do período do EMA
emaPeriodHighs = input.int(title="Highs Period", defval=3, minval=1, maxval=9999)
emaPeriodLows = input.int(title="Lows Period", defval=3, minval=1, maxval=9999)

// Parametrização da data de início e fim do período a ser coletado
startYear = input.int(title="Start Year", defval=2020)
startMonth = input.int(title="Start Month", defval=1, minval=1, maxval=12)
startDay = input.int(title="Start Day", defval=1, minval=1, maxval=31)

endYear = input.int(title="End Year", defval=2020)
endMonth = input.int(title="End Month", defval=12, minval=1, maxval=12)
endDay = input.int(title="End Day", defval=31, minval=1, maxval=31)

// Convertendo data de início e fim para timestamp
startDate = timestamp(startYear, startMonth, startDay, 00, 00)
endDate = timestamp(endYear, endMonth, endDay, 23, 59)

// EMA
emaH = ta.ema(high, emaPeriodHighs)
emaL = ta.ema(low, emaPeriodLows)

// PLOT:
// Desenha as linhas EMA no gráfico
plot(emaH, color=color.green, linewidth=2)
plot(emaL, color=color.red, linewidth=2)

// Condições
inDateRange = true

// Verifica se houve mais de três candles consecutivos do mesmo sentido
checkThreeConsecutiveCandles = (close[0] > close[1] and close[1] > close[2] and close[2] > close[3]) or (close[0] < close[1] and close[1] < close[2] and close[2] < close[3])

if(close < emaL and inDateRange and checkThreeConsecutiveCandles and barstate.isconfirmed)
    strategy.entry("Long", strategy.long, comment="Long", when=strategy.position_size == 0)
if(close > emaH and inDateRange and checkThreeConsecutiveCandles and barstate.isconfirmed)
    strategy.close("Long", comment="Close Long")

// Fechar a operação no fechamento do pregão
if(strategy.position_size > 0 and na(time_close[0]))
    strategy.close("Long", comment="Close Long")

```

> Detail

https://www.fmz.com/strategy/451075

> Last Modified

2024-05-11 17:35:22
