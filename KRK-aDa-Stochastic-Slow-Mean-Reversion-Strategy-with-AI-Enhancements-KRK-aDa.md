
> Name

KRK-aDa-Stochastic-Slow-Mean-Reversion-Strategy-with-AI-Enhancements-KRK-aDa-Stochastic Slow Mean Reversion Strategy with Artificial Intelligence Enhancements
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/f355fa5d0889c3ac1d071046cfdd5023d6f73d9ac3ce3a4be98eb13fa7cda07f.png)

[trans]

#### Overview
This strategy uses the Stochastic Slow as the main trading signal and combines it with the 200-period Simple Moving Average (SMA) as the trend filter. Additionally, the strategy introduces a virtual artificial intelligence (AI) indicator to provide additional entry signals. The main idea of ​​the strategy is to buy in the oversold area and sell in the overbought area, while ensuring that the price is bought above the 200 SMA and sold below the 200 SMA to follow the current trend. The addition of AI indicators provides the strategy with more entry opportunities.
#### Strategy Principle
1. Calculate the K value and D value of the stochastic slow indicator, where the period of the K value is 26 and the D value is the 3-period SMA of the K value.
2. Set the overbought zone (OverBought) to 81, the oversold zone (OverSold) to 20, and the minimum K value (minKValue) to 11.
3. When the K line crosses the D line and the K value is less than the oversold zone and greater than the minimum K value, a buy signal is generated.
4. When the K line crosses the D line and the K value is greater than the overbought zone and greater than the minimum K value, a sell signal is generated.
5. Use the 200-period SMA as a trend filter, allowing buying when the price is above the 200 SMA and selling when the price is below the 200 SMA.
6. Introduce virtual AI indicators (use RSI>50 to indicate bullish, RSI<50 to indicate bearish), buy when the AI ​​indicator is bullish, and sell when it is bearish.
7. Combine the signals of stochastic indicators, trend filters and AI indicators to generate final trading signals.
8. Set a 10% stop loss when buying and a 10% stop loss when selling.
#### Strategic Advantages
1. The Stochastic Slow indicator effectively identifies the overbought and oversold areas of the market, providing a good entry point for trading.
2. Introducing 200 SMA as a trend filter to ensure that transactions are consistent with the current trend and improve the success rate.
3. Adding AI indicators provides the strategy with more entry opportunities and may increase the returns of the strategy.
4. Set stop loss orders to effectively control risks.
#### Strategy Risk
1. Stochastic indicators may produce more false signals in volatile markets.
2. The AI ​​indicator is currently only a virtual indicator, and the actual effect needs to be verified.
3. Stop loss setting may cause some profits to be stopped prematurely.
#### Strategy optimization direction
1. Optimize the parameters of the stochastic indicator and find the best cycle and overbought and oversold threshold settings.
2. Introduce more complex and effective AI models to improve the accuracy of AI signals.
3. Optimize stop loss and take profit settings to better control risks and lock in profits.
4. Consider introducing other effective technical indicators or fundamental data to improve the robustness of the strategy.
#### Summarize
This strategy combines stochastic slow indicators, trend filters and AI signals to form a multi-factor trading strategy. The stochastic indicator provides effective overbought and oversold signals, the trend filter ensures that the trading direction is consistent with the general trend, and the AI ​​signal provides the strategy with more entry opportunities. Although this strategy still has some potential risks and room for optimization, its overall thinking is clear and logical, and it is worthy of further exploration and improvement.
|| 

#### Overview

This strategy utilizes the Stochastic Slow indicator as the primary trading signal, combined with a 200-period Simple Moving Average (SMA) as a trend filter. Additionally, the strategy introduces a dummy Artificial Intelligence (AI) indicator to provide extra entry signals. The main idea is to buy in oversold areas and sell in overbought areas, while ensuring that the price is above the 200 SMA for long entries and below the 200 SMA for short entries, aligning with the current trend. The inclusion of the AI indicator offers more entry opportunities.

#### Strategy Principles

1. Calculate the K and D values of the Stochastic Slow indicator, with the K period set to 26 and the D value being a 3-period SMA of the K value.

2. Set the overbought level (OverBought) to 81, the oversold level (OverSold) to 20, and the minimum K value (minKValue) to 11.

3. Generate a buy signal when the K line crosses above the D line, and the K value is below the oversold level and above the minimum K value.

4. Generate a sell signal when the K line crosses below the D line, and the K value is above the overbought level and above the minimum K value.

5. Use the 200-period SMA as a trend filter, allowing long entries only when the price is above the 200 SMA and short entries when the price is below the 200 SMA.

6. Introduce a dummy AI indicator (using RSI>50 for bullish and RSI<50 for bearish), entering long when the AI signal is bullish and short when it is bearish.

7. Combine the signals from the Stochastic indicator, trend filter, and AI indicator to generate the final trading signals.

8. Set a 10% stop loss for long entries and a 10% stop loss for short entries.

#### Strategy Advantages

1. The Stochastic Slow indicator effectively identifies overbought and oversold areas in the market, providing good entry points for trades.

2. The 200 SMA trend filter ensures that trades align with the current trend, increasing the success rate.

3. The inclusion of the AI indicator offers more entry opportunities, potentially increasing the strategy's profitability.

4. The use of stop-loss orders effectively manages risk.

#### Strategy Risks

1. The Stochastic indicator may generate false signals in choppy markets.

2. The AI indicator is currently a dummy indicator, and its actual effectiveness needs to be verified.

3. The stop-loss settings may lead to some profits being cut short prematurely.

#### Strategy Optimization Directions

1. Optimize the parameters of the Stochastic indicator to find the best period and overbought/oversold threshold settings.

2. Introduce more complex and effective AI models to improve the accuracy of AI signals.

3. Fine-tune the stop-loss and take-profit settings for better risk control and profit capture.

4. Consider incorporating other effective technical indicators or fundamental data to enhance the strategy's robustness.

#### Summary

This strategy combines the Stochastic Slow indicator, trend filter, and AI signals to form a multi-factor trading approach. The Stochastic indicator provides effective overbought and oversold signals, the trend filter ensures that trades align with the overall trend, and the AI signals offer additional entry opportunities. Although the strategy has some potential risks and room for improvement, its overall logic is clear and reasonable, making it worth further exploration and refinement.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|26|length|
|v_input_1|81|OverBought|
|v_input_2|20|OverSold|
|v_input_int_2|3|smoothK|
|v_input_int_3|3|smoothD|
|v_input_3|11|Minimum K Value|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-01 00:00:00
end: 2024-03-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Stochastic Slow Strategy with More Entries and AI", overlay=true)

length = input.int(26, minval=1)
OverBought = input(81)
OverSold = input(20)
smoothK = input.int(3, minval=1)
smoothD = input.int(3, minval=1)
minKValue = input(11, title="Minimum K Value")

// Stochastic calculations
k = ta.sma(ta.stoch(close, high, low, length), smoothK)
d = ta.sma(k, smoothD)
co = ta.crossover(k, d)
cu = ta.crossunder(k, d)

// Trend filter (200-period simple moving average)
ema200 = ta.sma(close, 200)

// Artificial Intelligence indicator (dummy example)
// Aquí puedes colocar la lógica de tu red neuronal artificial
// Por ahora, simplemente usaremos una señal aleatoria
ai_signal = ta.rsi(close, 14) > 50 ? 1 : -1

// Entry conditions
longCondition = ta.crossover(close, ema200) and k < OverSold and k > minKValue and ai_signal == 1
shortCondition = ta.crossunder(close, ema200) and k > OverBought and k > minKValue and ai_signal == -1

if (not na(k) and not na(d))
    if (co and k < OverSold and k > minKValue)
        strategy.entry("StochLE", strategy.long, comment="StochLE")
    if (cu and k > OverBought and k > minKValue)
        strategy.entry("StochSE", strategy.short, comment="StochSE")
    if (longCondition)
        strategy.entry("LongEntry", strategy.long, comment="LongEntry")
        strategy.exit("StopLoss", "LongEntry", loss = close * 0.9) // Stop loss del 10%
    if (shortCondition)
        strategy.entry("ShortEntry", strategy.short, comment="ShortEntry")
        strategy.exit("StopLoss", "ShortEntry", loss = close * 1.1) // Stop loss del 10%

// Plotting
plot(ema200, color=color.blue, title="200 SMA")

```

> Detail

https://www.fmz.com/strategy/449521

> Last Modified

2024-04-26 15:41:18
