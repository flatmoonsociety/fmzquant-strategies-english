
> Name

Aggregated-Multi-timeframe-MACD-RSI-CCI-StochRSI-MA-Linear-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/da44d68872e6836d6e.png)
 [trans]
### Overview
This strategy comprehensively uses multiple indicators such as MACD, RSI, CCI, StochRSI and 200-day simple moving average to form trading signals under the daily time frame. The strategy first determines whether the MACD line and signal line are golden crosses, then combines RSI, CCI, and StochRSI indicators to determine whether it is overbought or oversold, and finally determines whether the price breaks through the 200-day moving average, and filters out buy and sell signals based on these conditions.
### Strategy Principles
The core logic of this strategy is to determine whether other auxiliary indicators also send similar signals when MACD sends out buy and sell signals. If most indicators send out signals in the same direction, there is a high probability of forming an effective trading opportunity.
First of all, when the MACD line and the signal line cross golden, a buy signal is generated, and when the MACD line crosses dead, a sell signal is generated. This is the main basis for strategies to judge trend turning.
Secondly, the RSI indicator determines whether it is overbought or oversold. When the RSI is higher than the set overbought line, it is judged to be overbought, and it is combined with the MACD dead cross to send a sell signal; when the RSI is lower than the set oversold line, it is judged to be oversold, and it is combined with the MACD golden cross to send a buy signal.
Similarly, the CCI indicator determines whether it is overbought or oversold. When the CCI is higher than the set overbought line, it is judged to be overbought, and it is combined with the MACD dead cross to send a sell signal; when the CCI is lower than the set oversold line, it is judged to be oversold, and it is combined with the MACD golden cross to send a buy signal.
In the StochRSI indicator, when the K line is higher than the D line, it is judged to be overbought. At this time, it is combined with the MACD dead cross to send a sell signal; when the K line is lower than the D line, it is judged to be oversold. At this time, it is combined with the MACD golden cross to send a buy signal.
Finally, when the price is higher than the 200-day moving average, it is judged to be an upward trend. At this time, in conjunction with the MACD Golden Cross and other indicators, a buy signal is issued; when the price is lower than the 200-day moving average, it is judged to be a downward trend. At this time, in conjunction with the MACD Death Cross and other indicators, a sell signal is issued.
By aggregating information from multiple indicators, we can more accurately determine the overbought and oversold status of the market, filter out some false signals, and make high-probability buying and selling decisions.
### Analysis of strategic advantages
1. This strategy comprehensively uses multiple indicators as the basis for buying and selling decisions, which can effectively avoid misleading trading opportunities and improve the reliability of signals.
2. By judging the relationship between price and the 200-day moving average, and judging the timing of buying and selling based on the trend, trading risks can be reduced.
3. RSI, CCI, StochRSI and other indicator parameters are adjustable and can be optimized for different market environments to increase profitability.
4. The strategy operates at the daily level to avoid unnecessary transactions and is more suitable for long-term positions.
### Strategy Risk Analysis
1. There is a certain lag in the generation of strategic signals, and short-term trading opportunities may be missed.
2. The participation of multiple indicators in judgment increases the complexity of the strategy and is prone to logical errors.
3. Improper setting of indicator parameters may result in a large number of false signals.
4. Long-term positions are susceptible to market risks, and the maximum drawdown may be larger.
5. Short-term fluctuations within the day may cause losses to expand.
### Strategy optimization direction
1. Carry out parameter optimization, adjust the setting parameters of RSI, CCI, StochRSI and other indicators, and determine the best parameter combination for different market environments.
2. Add a stop loss strategy to lock in profits and control risks through trailing stop loss, percentage stop loss, etc.
3. Add technical indicators or mechanisms to re-enter the market to avoid missing important trading opportunities.
4. Combine with more technical indicators, such as Bollinger Bands, KD, etc., to determine the timing of buying and selling.
5. Analyze trend indicators at a longer cycle level and optimize the long-term position holding capacity of the strategy.
### Summarize
This strategy uses multiple indicators such as MACD, RSI, CCI, StochRSI and the 200-day moving average to judge the market and identify buying and selling opportunities at the daily level. The advantage of the strategy is that the signals are accurate and reliable, suitable for long-term positions, and can be adjusted according to the market environment through parameter optimization. However, there is also a certain lag and the inability to lock in short-term trading opportunities. Generally speaking, this strategy is relatively reliable as a multi-indicator trend following strategy, and is especially suitable for investors who pursue long-term stable returns.
||

### Overview

This strategy comprehensively utilizes indicators like MACD, RSI, CCI, StochRSI and 200-day simple moving average to generate trading signals at the daily timeframe. It first judges the MACD line and signal line for golden cross and death cross, then combined with RSI, CCI and StochRSI to determine overbought and oversold conditions, finally judges if the price breaks through the 200-day moving average line. Buying and selling signals are screened out based on these conditions.

### Strategy Principle  

The core logic of this strategy is to determine if other auxiliary indicators also give out similar signals when MACD sends out buying and selling signals. If most indicators give out signals pointing to the same direction, it is highly probable to form a valid trading opportunity.

Firstly, when MACD line does a golden cross over signal line, it generates a buying signal. When a death cross happens, it generates a selling signal. This is the main basis for the strategy to determine trend reversal.  

Secondly, RSI indicator judges overbought and oversold conditions. When RSI goes above the set overbought line, it is determined as overbought. At this time combined with MACD death cross, a selling signal is generated. When RSI falls below the set oversold line, it is determined as oversold. At this time combined with MACD golden cross, a buying signal is generated.

Similarly, CCI indicator also judges overbought and oversold scenarios. When CCI surpasses the overbought line, combined with MACD death cross, a selling opportunity occurs. When CCI drops below the oversold line, matched with MACD golden cross, a buying signal occurs.

Inside StochRSI indicator, when K line goes above D line, it indicates an overbought situation. At this time matched with MACD death cross, a selling signal is sent out. When K line falls below D line, it determines an oversold status. At this time combined with MACD golden cross, a buying signal is generated.  

Finally, when price goes above the 200-day moving average line, it is determined as an upward trend. At this time combined with MACD golden cross and other indicators, a buying signal is generated. When price falls below 200-day MA, it is a downward trend. At this time matched with MACD death cross and other indicators, a selling signal occurs.

By aggregating information from multiple indicators, overbought and oversold market status can be more accurately determined. Some false signals can be filtered out, so that high probability buying and selling decisions can be made.

### Advantage Analysis

1. The strategy synthesizes multiple indicators as basis for buying and selling decisions, which can effectively avoid misleading trading opportunities and increase signal reliability.  

2. By judging the relationship between price and 200-day moving average, combined with trend judgment, buying and selling timing risk can be reduced.

3. Parameters inside indicators like RSI, CCI and StochRSI can be adjustable for different market environments to increase profit rate.  

4. The strategy operates at daily timeframe to avoid unnecessary trades, more suitable for long-term position holding.

### Risk Analysis  

1. Strategy signals have some lag, which may miss short-term trading chances.  

2. Multiple indicators increase complexity, easier to generate logic errors.

3. Improper parameter settings may lead to numerous false signals. 

4. Long-term holding is vulnerable to market risks, maximum drawdown could be relatively large.

5. Intraday short-term fluctuations may expand losses.

### Optimization Directions

1. Conduct parameter optimization, adjust settings for RSI, CCI, StochRSI to determine the best parameter combination for different market environments.

2. Add stop loss mechanisms like moving stop loss, percentage stop loss to lock in profits and control risks.

3. Add technical indicators or mechanisms to re-enter the markets, avoiding missing significant trading opportunities.  

4. Incorporate more technical indicators like Bollinger Bands, KD to determine trading timing.

5. Analyze longer cycle trend indicators to optimize long position holding capability.

### Conclusion

This strategy utilizes indicators like MACD, RSI, CCI, StochRSI and 200-day moving average to determine market conditions and identify trading signals at the daily chart. Its advantages are accurate and reliable signals, suitable for long-term holding. Parameters can be optimized to adapt to different environments. Disadvantages are certain lagging and inability to capture short-term chances. Overall as a multi-indicator trend following strategy, it is quite reliable and suitable for investors seeking steady long-term gains.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|Fast Length|
|v_input_2|26|Slow Length|
|v_input_3|9|Signal Length|
|v_input_4|14|RSI Length|
|v_input_5|70|RSI Overbought Level|
|v_input_6|14|CCI Length|
|v_input_7|100|CCI Overbought Level|
|v_input_8|14|Stoch Length|
|v_input_9|3|Stoch K|
|v_input_10|3|Stoch D|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-15 00:00:00
end: 2024-01-17 06:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("MACD RSI CCI StochRSI MA Strategy", shorttitle="MRCSSMA", overlay=true)

// MACD göstergesi
fastLength = input(12, title="Fast Length")
slowLength = input(26, title="Slow Length")
signalLength = input(9, title="Signal Length")
[macdLine, signalLine, _] = macd(close, fastLength, slowLength, signalLength)

// RSI göstergesi
rsiLength = input(14, title="RSI Length")
rsiLevel = input(70, title="RSI Overbought Level")
rsiValue = rsi(close, rsiLength)

// CCI göstergesi
cciLength = input(14, title="CCI Length")
cciLevel = input(100, title="CCI Overbought Level")
cciValue = cci(close, cciLength)

// Stochastic Oscillator göstergesi
stochLength = input(14, title="Stoch Length")
stochK = input(3, title="Stoch K")
stochD = input(3, title="Stoch D")
stochValue = stoch(close, high, low, stochLength)
stochDValue = sma(stochValue, stochD)

// 200 günlük hareketli ortalama
ma200 = sma(close, 200)

// Alış ve Satış Sinyalleri
buySignal = crossover(macdLine, signalLine) and rsiValue < rsiLevel and cciValue < cciLevel and stochValue > stochDValue and close > ma200
sellSignal = crossunder(macdLine, signalLine) and rsiValue > (100 - rsiLevel) and cciValue > (100 - cciLevel) and stochValue < stochDValue and close < ma200

// Ticaret stratejisi uygula
strategy.entry("Buy", strategy.long, when = buySignal)
strategy.close("Buy", when = sellSignal)
strategy.entry("Sell", strategy.short, when = sellSignal)
strategy.close("Sell", when = buySignal)

// Göstergeleri çiz
hline(rsiLevel, "RSI Overbought", color=color.red)
hline(100 - rsiLevel, "RSI Oversold", color=color.green)
hline(cciLevel, "CCI Overbought", color=color.red)
hline(100 - cciLevel, "CCI Oversold", color=color.green)

// 200 günlük hareketli ortalama çiz
plot(ma200, color=color.blue, title="200-day MA")

// Grafik üzerinde sinyal okları çiz
plotshape(series=buySignal, title="Buy Signal", color=color.green, style=shape.triangleup, location=location.belowbar, size=size.small)
plotshape(series=sellSignal, title="Sell Signal", color=color.red, style=shape.triangledown, location=location.abovebar, size=size.small)

```

> Detail

https://www.fmz.com/strategy/439734

> Last Modified

2024-01-23 14:11:26
