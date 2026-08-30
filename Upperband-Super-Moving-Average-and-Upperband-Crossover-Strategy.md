
> Name

Super-Moving-Average-and-Upperband-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1a7f5301ac18a28ea9a483d6100c2ef111b0a7868c6b58d32b5bb018c4930a42.png)

[trans]
#### Overview
The Super Moving Average and Upperband crossover strategy is a quantitative trading strategy based on technical indicators. This strategy utilizes the Exponential Moving Average (EMA) and Upperband indicators to capture the market’s upward trends. When the closing price breaks through the Upperband and meets certain conditions, the strategy will issue a buy signal; when the closing price falls below the 3-day EMA, the strategy will issue a sell signal. This strategy is suitable for markets with large trading volumes and obvious trends, such as Bitcoin.
#### Strategy Principle
The core of this strategy is to use two technical indicators, EMA and Upperband, to determine market trends and buying and selling opportunities. First, the strategy calculates the Upperband indicator, which takes into account the volatility of the price. When the price deviates greatly from the average price, the value of the Upperband will increase accordingly. Then, the strategy determines whether the closing price breaks through the upperband's moving average and whether other buying conditions are met. If so, it issues a buy signal. After holding the position, the strategy will issue a sell signal when the closing price falls below the 3-day EMA.
#### Strategic Advantages
1. Suitable for markets with strong trends: This strategy performs well in rising trends, and is especially suitable for products with large fluctuations and obvious trends like Bitcoin.
2. Combining price and volatility: The Upperband indicator comprehensively considers price levels and price volatility, which can reflect the market status more comprehensively.
3. Simple and easy to use: The strategy has clear logic, simple indicators, and is easy to understand and implement.
4. Suitable for short-term trading: This strategy has a high frequency of buying and selling signals and is suitable for short-term trading.
#### Strategy Risk
1. Risk of volatile markets: In volatile markets with no obvious trend, this strategy may result in frequent transactions, resulting in larger slippages and transaction costs.
2. Indicator parameter risk: This strategy is relatively sensitive to indicator parameters, and improper parameter settings may lead to poor performance of the strategy.
3. Overfitting risk: This strategy performs well in a specific market, but it may not be able to adapt to changes in the market environment, and there is a risk of overfitting.
#### Strategy optimization direction
1. Introduce trend confirmation indicators: Trend confirmation indicators such as MACD can be introduced to filter out false signals in a volatile market.
2. Optimization parameter selection: Optimization methods such as genetic algorithms can be used to find the optimal combination of indicator parameters.
3. Add risk control module: Risk control measures such as stop loss and dynamic position management can be introduced to reduce strategic risks.
4. Multi-variety adaptation: Machine learning and other methods can be used to enable strategies to adapt to different varieties and market environments.
#### Summarize
The Super Moving Average and Upperband crossover strategy is a simple and practical quantitative trading strategy, suitable for markets with strong trends. This strategy uses EMA and Upperband indicators to capture the upward trend, with clear logic and easy implementation. However, this strategy also has certain risks, such as market shock risk, parameter risk and over-fitting risk. In the future, the strategy can be optimized from aspects such as trend confirmation, parameter optimization, risk control and multi-variety adaptation to improve the robustness and adaptability of the strategy.
|| 

#### Overview

The Super Moving Average and Upperband Crossover Strategy is a quantitative trading strategy based on technical indicators. The strategy utilizes the Exponential Moving Average (EMA) and Upperband indicators to capture upward trends in the market. When the closing price breaks through the Upperband and meets certain conditions, the strategy generates a buy signal. When the closing price falls below the 3-day EMA, the strategy generates a sell signal. This strategy is suitable for markets with high trading volumes and clear trends, such as Bitcoin.

#### Strategy Principle

The core of this strategy is to use the EMA and Upperband technical indicators to determine market trends and timing for buying and selling. First, the strategy calculates the Upperband indicator, which takes into account price volatility. When the price deviation from the average price is large, the value of the Upperband will increase accordingly. Then, the strategy determines whether the closing price has broken through the moving average of the Upperband and whether it meets other buying conditions. If so, it generates a buy signal. After holding a position, when the closing price falls below the 3-day EMA, the strategy generates a sell signal.

#### Strategy Advantages

1. Suitable for markets with strong trends: This strategy performs well in upward trends and is especially suitable for instruments with high volatility and clear trends, such as Bitcoin.

2. Combines price and volatility: The Upperband indicator comprehensively considers price levels and price volatility, and can more fully reflect market conditions.

3. Simple and easy to use: The strategy logic is clear, and the indicators used are simple and easy to understand and implement.

4. Suitable for short-term trading: The strategy generates buy and sell signals frequently, making it suitable for short-term trading.

#### Strategy Risks

1. Oscillating market risk: In a highly volatile and trendless oscillating market, the strategy may trade frequently, resulting in large slippage and transaction costs.

2. Indicator parameter risk: The strategy is sensitive to indicator parameters, and improper parameter settings may lead to poor strategy performance.

3. Overfitting risk: The strategy performs well in specific markets but may not be able to adapt to changes in market conditions, leading to overfitting risk.

#### Strategy Optimization Directions

1. Introduce trend confirmation indicators: Trend confirmation indicators such as MACD can be introduced to filter out false signals in oscillating markets.

2. Optimize parameter selection: Optimal indicator parameter combinations can be found through optimization methods such as genetic algorithms.

3. Add risk control module: Risk control measures such as stop-loss and dynamic position management can be introduced to reduce strategy risk.

4. Multi-variety adaptation: Machine learning and other methods can be used to make the strategy adaptable to different varieties and market environments.

#### Summary

The Super Moving Average and Upperband Crossover Strategy is a simple and practical quantitative trading strategy suitable for markets with strong trends. The strategy uses EMA and Upperband indicators to capture upward trends, and its logic is clear and easy to implement. However, the strategy also has certain risks, such as oscillating market risk, parameter risk, and overfitting risk. In the future, the strategy can be optimized in terms of trend confirmation, parameter optimization, risk control, and multi-variety adaptation to improve the strategy's robustness and adaptability.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-11 00:00:00
end: 2024-05-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Estratégia de Cruzamento de Bandas", overlay=true)

// Entradas
factor = input(0.001, title="Factor")
length = input(20, title="Length")

// Cálculo da Upperband
Upperband = high * (1 + 2 * ((((high - low) / ((high + low) / 2)) * 1000) * factor))

// Condição de Compra
buy_condition = close > ta.ema(close, 3)

// Variável para controlar se a compra foi feita
var bought = false

// Sinal de compra
buy_signal = (close[1] <= ta.sma(Upperband, length)[1]) and (close > ta.sma(Upperband, length)) and buy_condition

// Sinal de venda
sell_signal = close < ta.ema(close, 3) and bought

// Atualizar o status de compra
if buy_signal
    bought := true
    strategy.entry("Compra", strategy.long)
else if sell_signal
    bought := false
    strategy.close("Compra")

// Plotagem dos sinais de compra e venda no gráfico
plotshape(series=buy_signal, title="Compra", color=color.green, style=shape.triangleup, location=location.belowbar)
plotshape(series=sell_signal, title="Venda", color=color.red, style=shape.triangledown, location=location.abovebar)
```

> Detail

https://www.fmz.com/strategy/451713

> Last Modified

2024-05-17 13:50:50
