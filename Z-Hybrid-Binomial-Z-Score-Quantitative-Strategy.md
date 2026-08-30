
> Name

Hybrid-Binomial-Z-Score-Quantitative-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/09d596b72247a7d8e283d0f10aed880d104bcc84f24852f2e072dfd7a2fe5f2c.png)

[trans]
#### Overview
The strategy uses a hybrid quantitative analysis approach that combines binomial distribution models and regression analysis to identify different market states. The strategy first calculates the Simple Moving Average (SMA) and Bollinger Bands (BB) indicators, and then calculates the Z-score based on the mean and standard deviation of historical returns. When the Z score is lower than the lower threshold and the price is lower than the lower track, the strategy opens a long position; when the Z score is higher than the upper threshold and the price is higher than the upper track, the strategy closes the position.
#### Strategy Principle
The core principle of this strategy is to use the Z-score to measure the position of current returns relative to the distribution of historical returns. The Z-score is calculated as: (current return - mean historical return) / standard deviation of historical returns. The higher the Z-score, the more extreme the current returns are, and the greater the possibility of overbought; the lower the Z-score, the more extreme the current returns, and the greater the possibility of oversold. At the same time, the strategy also combines the Bollinger Bands indicator, with the price breaking through the upper and lower rails as a secondary confirmation. The strategy will generate a trading signal only when both the Z-score and the Bollinger Bands signal meet the conditions. This combination can effectively reduce the occurrence of false signals.
#### Strategic Advantages
1. Quantitative analysis: This strategy is completely based on quantitative indicators, with clear rules and easy to implement and backtest.
2. Double confirmation: The strategy uses both Z-score and Bollinger Bands indicators to form a double filtering mechanism to improve signal accuracy.
3. Statistical basis: Z-score is derived from the normal distribution theory in statistics. It has a solid theoretical foundation and can objectively measure the extreme degree of current returns.
4. Flexible parameters: Users can adjust parameters such as SMA cycle, Bollinger Band multiples, and Z score thresholds as needed to flexibly adapt to different markets.
#### Strategy Risk
1. Parameter sensitivity: Different parameter settings may lead to large differences in strategy performance, and sufficient parameter optimization and stability testing are required.
2. Trend risk: When there is a strong trend in the market, the Z score may be in an extreme area for a long time, resulting in scarce or complete lack of strategic signals.
3. Risk of over-fitting: If the policy parameters are over-optimized, it may lead to over-fitting and poor out-of-sample performance.
4. Black swan risk: Under extreme market conditions, historical statistical laws may fail, and the strategy faces greater risk of retracement.
#### Strategy optimization direction
1. Dynamic parameters: Consider dynamically adjusting the Z score threshold and Bollinger Band multiples based on market volatility, trend strength and other indicators to improve adaptability.
2. Add trend filtering: Superimpose trend judgment indicators, such as MA crossover, DMI, etc., on the existing mechanism to avoid too many invalid signals under strong trends.
3. Combination optimization: Combine this strategy with other quantitative strategies (such as momentum, mean reversion, etc.) to give full play to their respective advantages and improve robustness.
4. Stop-loss and stop-profit: Introduce a reasonable stop-loss and stop-profit mechanism to control single transaction risk exposure and increase risk-adjusted returns.
#### Summary
The hybrid two-state Z-score quantitative strategy is a quantitative trading strategy based on statistical principles. It identifies potential overbought and oversold opportunities by comparing current returns with historical return distributions. At the same time, the strategy uses Bollinger Band indicators for secondary confirmation to improve signal reliability. The strategy rules are clear and easy to implement and optimize, but it also faces challenges such as parameter sensitivity, trend risk, and overfitting risk. In the future, the strategy can be optimized from aspects such as dynamic parameters, trend filtering, portfolio optimization, stop loss and take profit to improve its adaptability and robustness. Overall, this strategy provides a simple and effective idea for quantitative trading, which is worthy of further exploration and improvement.
|| 

#### Overview
This strategy employs a hybrid quantitative analysis approach, combining binomial distribution model and regression analysis, to identify different market regimes. The strategy first calculates the Simple Moving Average (SMA) and Bollinger Bands (BB) indicators, then computes the Z-score based on the mean and standard deviation of historical returns. When the Z-score is below the lower threshold and the price is below the lower band, the strategy enters a long position; when the Z-score is above the upper threshold and the price is above the upper band, the strategy closes the position.

#### Strategy Principle
The core principle of this strategy is to use the Z-score to measure the position of current returns relative to the distribution of historical returns. The formula for calculating the Z-score is: (Current Return - Historical Return Mean) / Historical Return Standard Deviation. A higher Z-score indicates that the current return is more extreme and the probability of overbought is higher; a lower Z-score indicates that the current return is more extreme and the probability of oversold is higher. At the same time, the strategy also incorporates the Bollinger Bands indicator, using price breakouts above or below the bands as a secondary confirmation. The strategy generates trading signals only when both the Z-score and Bollinger Bands conditions are met simultaneously. This combination approach can effectively reduce the occurrence of false signals.

#### Strategy Advantages
1. Quantitative Analysis: The strategy is entirely based on quantitative indicators, with clear rules that are easy to implement and backtest.
2. Dual Confirmation: The strategy employs both the Z-score and Bollinger Bands indicators, forming a dual filtering mechanism to improve signal accuracy.
3. Statistical Foundation: The Z-score originates from the normal distribution theory in statistics, with a solid theoretical foundation, and can objectively measure the extremity of current returns.
4. Parameter Flexibility: Users can adjust parameters such as the SMA period, Bollinger Bands multiplier, and Z-score thresholds according to their needs, flexibly adapting to different markets.

#### Strategy Risks
1. Parameter Sensitivity: Different parameter settings may lead to significant differences in strategy performance, requiring extensive parameter optimization and stability testing.
2. Trend Risk: When the market exhibits strong trends, the Z-score may remain in extreme regions for an extended period, resulting in infrequent or completely absent strategy signals.
3. Overfitting Risk: If the strategy parameters are over-optimized, it may lead to overfitting and poor out-of-sample performance.
4. Black Swan Risk: Under extreme market conditions, historical statistical patterns may fail, exposing the strategy to significant drawdown risks.

#### Strategy Optimization Directions
1. Dynamic Parameters: Consider dynamically adjusting the Z-score thresholds and Bollinger Bands multiplier based on indicators such as market volatility and trend strength to improve adaptability.
2. Trend Filtering: Overlay trend determination indicators, such as MA crossover or DMI, on top of the existing mechanism to avoid excessive invalid signals during strong trends.
3. Portfolio Optimization: Combine this strategy with other quantitative strategies (such as momentum, mean reversion, etc.) to leverage their respective strengths and improve robustness.
4. Stop-Loss and Take-Profit: Introduce reasonable stop-loss and take-profit mechanisms to control risk exposure per trade and improve risk-adjusted returns.

#### Summary
The Hybrid Binomial Z-Score Quantitative Strategy is a quantitative trading strategy based on statistical principles, identifying potential overbought and oversold opportunities by comparing current returns with the distribution of historical returns. Additionally, the strategy employs the Bollinger Bands indicator for secondary confirmation, enhancing signal reliability. The strategy rules are clear and easy to implement and optimize, but it also faces challenges such as parameter sensitivity, trend risk, overfitting risk, etc. In the future, the strategy can be optimized in terms of dynamic parameters, trend filtering, portfolio optimization, stop-loss and take-profit mechanisms, etc., to improve its adaptability and robustness. Overall, this strategy provides a simple yet effective approach for quantitative trading, worthy of further exploration and refinement.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-22 00:00:00
end: 2024-05-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Estratégia Híbrida Quantitativa", overlay=true)

// Definição de parâmetros
sma_length = input.int(20, title="Período da SMA")
threshold_high = input.float(1.5, title="Threshold Alto")
threshold_low = input.float(-1.5, title="Threshold Baixo")
lookback_period = input.int(252, title="Período de Retorno Histórico (dias)")

// Funções auxiliares
f_sma(source, length) =>
    ta.sma(source, length)

f_bollinger_band(source, length, mult) =>
    basis = ta.sma(source, length)
    dev = mult * ta.stdev(source, length)
    [basis + dev, basis - dev]

// Cálculo dos indicadores
sma = f_sma(close, sma_length)
[upper_band, lower_band] = f_bollinger_band(close, sma_length, 2)

// Regime de Mercado: Binomial
retornos = ta.change(close, 1)
media_retornos = ta.sma(retornos, lookback_period)
desvio_padrao_retornos = ta.stdev(retornos, lookback_period)

// Indicador de Regime: Z-Score
z_score = (retornos - media_retornos) / desvio_padrao_retornos

// Sinal de Compra e Venda
sinal_compra = z_score < threshold_low and close < lower_band
sinal_venda = z_score > threshold_high and close > upper_band

// Execução de Ordem
if (sinal_compra)
    strategy.entry("Long", strategy.long)
if (sinal_venda)
    strategy.close("Long")

// Plotagem dos Indicadores
plot(sma, title="SMA", color=color.blue)
plot(upper_band, title="Upper Bollinger Band", color=color.red)
plot(lower_band, title="Lower Bollinger Band", color=color.green)
hline(threshold_high, "Threshold Alto", color=color.red, linestyle=hline.style_dashed)
hline(threshold_low, "Threshold Baixo", color=color.green, linestyle=hline.style_dashed)
plot(z_score, title="Z-Score", color=color.purple)

```

> Detail

https://www.fmz.com/strategy/452742

> Last Modified

2024-05-28 17:38:08
