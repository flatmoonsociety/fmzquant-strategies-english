
> Name

Mean-Reversion-Bollinger-Bands-Trading-Strategy-with-Rational-Return-Signal
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1efe4c5d9655f94dee3.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on the Bollinger Bands and price mean reversion principles. By monitoring the deviation between the price and the moving average, combined with the breakthrough signals of the upper and lower Bollinger Bands, we can trade when the market is overbought and oversold and expects the price to return to the mean. The strategy uses a percentage threshold to measure the degree of price deviation, and filters out false signals by setting reasonable trigger conditions to improve the accuracy of transactions.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Use the 20-day moving average as the middle track and 2 times the standard deviation to construct the Bollinger Bands channel.
2. Introduce a 3.5% price deviation threshold to identify significant deviations
3. Track whether the price is deviating through the is_outside variable
4. When the price returns to the Bollinger Bands range, a trading signal will be triggered
5. The specific trading rules are:
   - Go long when price returns from deviation and breaks above the upper band
   - Go short when the price returns from the deviation and breaks through the lower band
#### Strategic Advantages
1. Mean regression logic is robust
   - Based on the statistical law that prices will eventually return to the mean
   - Ensure the salience of trading opportunities through deviation thresholds
2. Improved risk control
   - Bollinger Bands provide a clear reference for fluctuation ranges
   - Off-state tracking to avoid trading in violent fluctuations
3. Highly adjustable parameters
   - Bollinger Band parameters can be adjusted according to the characteristics of the species
   - Deviation threshold can be set according to risk appetite
#### Strategy Risk
1. Trend market failure risk
   - Frequent false signals may occur in strong trending markets
   - It is recommended to add trend filter to identify market status
2. Parameter sensitivity risk
   - Improper parameter settings may affect strategy performance
   - Need to optimize parameters through historical data backtesting
3. Slippage cost risk
   - Frequent transactions may bring higher transaction costs
   - It is recommended to increase the position limit and cost control
#### Strategy optimization direction
1. Increase market environment identification
   - Introducing trend strength indicators such as ADX
   - Dynamically adjust parameters based on market conditions
2. Improve the stop-profit and stop-loss mechanism
   - Set dynamic stop loss based on ATR
   - Introducing moving take-profit to protect profits
3. Optimize transaction frequency
   - Added minimum holding time limit
   - Set transaction intervals to control costs
#### Summary
This strategy captures overbought and oversold opportunities in the market through Bollinger Bands and mean reversion principles, and combines reasonable deviation thresholds and state tracking mechanisms to effectively control trading risks. The strategy framework has good scalability and can adapt to different market environments through parameter optimization and function improvement. It is recommended to pay attention to risk control in real trading applications and adjust parameters according to the characteristics of specific varieties. ||
#### Overview
This strategy is a quantitative trading system based on Bollinger Bands and price mean reversion principles. It monitors price deviation from the moving average, combined with Bollinger Bands breakout signals, to trade when expecting price regression after market overbought/oversold conditions. The strategy uses percentage thresholds to measure price deviation and sets reasonable trigger conditions to filter false signals and improve trading accuracy.

#### Strategy Principles
The core logic is based on the following key elements:
1. Uses 20-day moving average as middle band, with 2 standard deviations to construct Bollinger Bands
2. Introduces 3.5% price deviation threshold to identify significant divergence
3. Tracks price deviation status through is_outside variable
4. Triggers trading signals when price returns within Bollinger Bands
5. Specific trading rules:
   - Long when price returns from deviation and breaks above upper band
   - Short when price returns from deviation and breaks below lower band

#### Strategy Advantages
1. Robust Mean Reversion Logic
   - Based on statistical principle of price returning to mean
   - Ensures trading opportunity significance through deviation threshold
2. Comprehensive Risk Control
   - Bollinger Bands provide clear volatility range reference
   - Deviation status tracking avoids trading during extreme volatility
3. Strong Parameter Adjustability
   - Bollinger Bands parameters adjustable to instrument characteristics
   - Deviation threshold can be set according to risk preference

#### Strategy Risks
1. Trend Market Ineffectiveness Risk
   - May generate frequent false signals in strong trend markets
   - Recommend adding trend filter to identify market conditions
2. Parameter Sensitivity Risk
   - Improper parameter settings may affect strategy performance
   - Requires parameter optimization through historical data backtesting
3. Slippage Cost Risk
   - Frequent trading may incur high transaction costs
   - Recommend adding position time limits and cost controls

#### Strategy Optimization Directions
1. Add Market Environment Recognition
   - Introduce trend strength indicators like ADX
   - Dynamically adjust parameters based on market conditions
2. Improve Stop-Loss and Take-Profit Mechanisms
   - Set dynamic stops based on ATR
   - Introduce trailing stops to protect profits
3. Optimize Trading Frequency
   - Add minimum position holding time
   - Set trading interval to control costs

#### Summary
This strategy captures market overbought/oversold opportunities through Bollinger Bands and mean reversion principles, effectively controlling trading risks with reasonable deviation thresholds and status tracking mechanisms. The strategy framework has good scalability and can adapt to different market environments through parameter optimization and functionality improvements. It's recommended to focus on risk control in live trading and adjust parameters according to specific instrument characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-06 00:00:00
end: 2025-01-04 08:00:00
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Estratégia com Bandas de Bollinger e Sinal de Retorno", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=200)

// Configurações das Bandas de Bollinger
length = input.int(20, title="Período da média")
mult = input.float(2.0, title="Desvio padrão")
bbBasis = ta.sma(close, length)
bbUpper = bbBasis + mult * ta.stdev(close, length)
bbLower = bbBasis - mult * ta.stdev(close, length)

// Configuração para a distância da média
percent_threshold = input.float(3.5, title="Distância da média (%)") / 100

dist_from_mean = 0.0
trigger_condition = false
if not na(bbBasis)
    dist_from_mean := math.abs(close - bbBasis) / bbBasis
    trigger_condition := dist_from_mean >= percent_threshold

// Variáveis para identificar o estado do afastamento
var bool is_outside = false
var color candle_color = color.new(color.white, 0)

if trigger_condition
    is_outside := true

if is_outside and close <= bbUpper and close >= bbLower
    is_outside := false
    candle_color := color.new(color.blue, 0) // Atribui uma cor válida
else
    candle_color := color.new(color.white, 0)

// Aplicar cor às velas
barcolor(candle_color)

// Plotar Bandas de Bollinger
plot(bbBasis, color=color.yellow, title="Média")
plot(bbUpper, color=color.red, title="Banda Superior")
plot(bbLower, color=color.green, title="Banda Inferior")

// Lógica de entrada e saída
longCondition = not is_outside and close > bbUpper
if (longCondition)
    strategy.entry("Buy", strategy.long)

shortCondition = not is_outside and close < bbLower
if (shortCondition)
    strategy.entry("Sell", strategy.short)

```

> Detail

https://www.fmz.com/strategy/477583

> Last Modified

2025-01-06 15:33:01
