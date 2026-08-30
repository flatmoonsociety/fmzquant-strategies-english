
> Name

Multi-Indicator Dynamic Balance Quantitative Trading System-Multi-Indicator-Dynamic-Equilibrium-Quantitative-Trading-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1b1ca2a30c61ffa51bf.png)

[trans]
#### Overview
This strategy is a dynamically balanced trading system based on multiple technical indicators. It comprehensively uses multiple technical analysis tools such as the relative strength index (RSI), Bollinger Bands (BB), exponential moving average (EMA), and moving average convergence divergence indicator (MACD) to identify buying and selling opportunities in the market through mutual verification between indicators. The strategy adopts a percentage position management method, with a default investment of 10% of the total assets in each transaction. This conservative position management helps control risks.
#### Strategy Principle
The core logic of the strategy is to improve the reliability of trading signals through the collaborative confirmation of multiple indicators. Specifically:
1. Use the 14-period RSI indicator to monitor overbought and oversold conditions in the market.
2. Determine the price fluctuation range through the Bollinger Bands of 20 periods and 2 times standard deviation.
3. Use the 50 and 200 period EMA to determine the mid- to long-term trend
4. Use MACD(12,26,9) parameter combination to capture trend turning points
A buy signal must meet at least two of the following conditions:
- Oversold zone with RSI below 30
- Price hits the lower Bollinger Band
- The fast EMA crosses the slow EMA
- The MACD line crosses the signal line
A sell signal is triggered when any of the following conditions occur:
- Overbought zone with RSI above 70
- Price breaks above the upper Bollinger Band
#### Strategic Advantages
1. Multi-indicator cross-validation improves signal reliability
2. Adopt percentage holding strategy to effectively control risks
3. Combines the advantages of trend following and band operation
4. The signal conditions are flexible and adjustable, and have strong adaptability.
5. Graphical interface intuitively displays trading signals
#### Strategy Risk
1. Multiple indicators may cause signal lag
2. Too many false signals may be generated in volatile markets
3. Fixed parameter settings may not adapt to changes in market conditions
4. Failure to consider trading volume factors may affect the accuracy of judgment
5. The fund management method is relatively simple and may affect the rate of return
#### Strategy optimization direction
1. Introduce trading volume indicators as auxiliary confirmation
2. Develop adaptive parameter adjustment mechanism
3. Refine fund management strategies
4. Add stop loss and trailing stop loss mechanisms
5. Add market environment identification module
6. Optimize signal filtering mechanism
#### Summary
This strategy builds a relatively complete trading system through the combined application of multiple technical indicators. Through cross-validation between indicators, the reliability of trading signals is improved. At the same time, conservative position management is used to control risks. Although there are some aspects that need to be optimized, the overall framework design is reasonable and has practical application value. ||
#### Overview
This strategy is a dynamic equilibrium trading system based on multiple technical indicators. It integrates various technical analysis tools including Relative Strength Index (RSI), Bollinger Bands (BB), Exponential Moving Average (EMA), and Moving Average Convergence Divergence (MACD) to identify market opportunities through cross-validation between indicators. The strategy employs percentage-based position management, defaulting to 10% of total assets per trade, which helps control risk.

#### Strategy Principles
The core logic of the strategy is to enhance trading signal reliability through multiple indicator confirmation. Specifically:
1. Uses 14-period RSI to monitor market overbought/oversold conditions
2. Employs 20-period, 2-standard deviation Bollinger Bands to determine price volatility ranges
3. Utilizes 50 and 200-period EMAs to judge medium and long-term trends
4. Adopts MACD(12,26,9) parameter combination to capture trend reversal points

Buy signals require at least two of the following conditions:
- RSI below 30 (oversold zone)
- Price touching lower Bollinger Band
- Fast EMA crossing above slow EMA
- MACD line crossing above signal line

Sell signals trigger when either:
- RSI above 70 (overbought zone)
- Price breaking above upper Bollinger Band

#### Strategy Advantages
1. Multiple indicator cross-validation improves signal reliability
2. Percentage-based position management effectively controls risk
3. Combines benefits of trend following and range trading
4. Flexible signal conditions with strong adaptability
5. Graphical interface provides intuitive signal display

#### Strategy Risks
1. Multiple indicators may lead to signal lag
2. May generate excessive false signals in ranging markets
3. Fixed parameters may not adapt to changing market conditions
4. Lack of volume consideration might affect judgment accuracy
5. Relatively simple money management approach may impact returns

#### Strategy Optimization Directions
1. Incorporate volume indicators as auxiliary confirmation
2. Develop adaptive parameter adjustment mechanisms
3. Refine money management strategy
4. Add stop-loss and trailing stop mechanisms
5. Include market environment recognition module
6. Optimize signal filtering mechanism

#### Summary
This strategy constructs a relatively complete trading system through the combined application of multiple technical indicators. Cross-validation between indicators enhances trading signal reliability. While adopting conservative position management to control risk, there are aspects requiring optimization, but the overall framework design is reasonable and has practical application value.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-16 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("ETH/USDT Multi-Indicator Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=250)

// Parametri za RSI
rsiPeriod = 14
rsiOversold = 30
rsiOverbought = 70

// Parametri za Bollinger Bands
bbLength = 20
bbStdDev = 2

// Parametri za EMA
emaShort = 50
emaLong = 200

// Parametri za MACD
[macdLine, signalLine, _] = ta.macd(close, 12, 26, 9)

// RSI izračun
rsi = ta.rsi(close, rsiPeriod)

// Bollinger Bands izračun
basis = ta.sma(close, bbLength)
upperBand = basis + bbStdDev * ta.stdev(close, bbLength)
lowerBand = basis - bbStdDev * ta.stdev(close, bbLength)

// EMA izračun
emaFast = ta.ema(close, emaShort)
emaSlow = ta.ema(close, emaLong)

// Pravilo 1: RSI prelazi iznad 30 nakon preprodatosti
rsiSignal = rsi < rsiOversold

// Pravilo 2: Cena dotakne donju Bollinger traku
bbSignal = close < lowerBand

// Pravilo 3: EMA crossover (zlatni krst)
emaSignal = emaFast > emaSlow

// Pravilo 4: MACD prelazak iznad signalne linije
macdSignal = macdLine > signalLine

// Kombinovani signal za kupovinu (bar dva uslova ispunjena)
buySignal = (rsiSignal and bbSignal) or (emaSignal and macdSignal)

// Pravilo za prodaju (RSI prekupljen ili cena iznad gornje Bollinger trake)
sellSignal = rsi > rsiOverbought or close > upperBand

// Vizualizacija signala
plotshape(series=buySignal, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=sellSignal, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// Strategija: Otvaranje i zatvaranje pozicija
if (buySignal)
    strategy.entry("Buy", strategy.long)

if (sellSignal)
    strategy.close("Buy")

// Bollinger Bands vizualizacija
plot(upperBand, color=color.new(color.blue, 50), title="Upper Band")
plot(lowerBand, color=color.new(color.blue, 50), title="Lower Band")
plot(basis, color=color.blue, title="Basis")

// EMA vizualizacija
plot(emaFast, color=color.orange, title="EMA Short")
plot(emaSlow, color=color.red, title="EMA Long")

```

> Detail

https://www.fmz.com/strategy/482441

> Last Modified

2025-02-18 14:44:29
