
> Name

Dynamic-Dual-Exponential-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c76acb0f5e9b040035.png)
[trans]
### Overview
This strategy is called "Dynamic Double Exponential Moving Average Trading Strategy" and is a quantitative trading strategy based on Double Exponential Moving Average (DEMA). This strategy calculates the stock's price change rate, and then performs double exponential smoothing on its absolute value and non-absolute value to obtain the True Strength Index (TSI). The strategy generates buy and sell signals based on the TSI value and the golden cross of its signal line.
### Strategy Principles
The core indicator of this strategy is the True Strength Index (TSI). The calculation formula of TSI is:
TSI = 100 * (PC1 / PC2)

Among them, PC1 and PC2 are the double exponential smoothing average of the price change rate and the double exponential smoothing average of the absolute value of the price change rate respectively. The calculation process of the double exponential smoothing average is to first apply an exponential moving average to the price change rate for a period of time, and then apply another shorter-term exponential moving average to the resulting exponential moving average. In this way, through double smoothing, the randomness in the price change rate can be better eliminated, thereby improving the stability of the TSI indicator.
After calculating the TSI value, the strategy also calculates the signal line of the TSI value. The signal line is defined as an exponential moving average of the TSI value for a certain period. In actual trading, the strategy determines the market trend and generates trading signals by observing the relationship between the TSI value and the signal line. When the TSI value crosses above the signal line, we are bullish; when the TSI value crosses below the signal line, we are bearish.
Another feature of this strategy is that the trade size is dynamically adjusted. An initial capital and a risk exposure ratio are set as input parameters in the strategy code. These two parameters are combined with the current price of the stock to dynamically calculate each transaction quantity or risk exposure. This allows for better control of risk throughout the strategy.
### Advantage Analysis
The dynamic dual exponential moving average trading strategy brings various advantages. :
1. It uses the TSI indicator, which applies double exponential smoothing, making it less sensitive to market noise and able to produce more accurate signals.
2. It is based on a proven principle of crossing indicators and their signal lines to generate trading signals. This eliminates many false signals.
3. The strategy dynamically adjusts position size based on risk budget. This helps prevent over-trading and emotional manipulation.
4. It works on daily and weekly time frames and is suitable for swing trading and positioning trading.
5. Due to its simple input/output logic, it is easy to implement in robots and other trading systems.
6. There are not too many parameters to adjust, making optimizing the system easy.
Together, these advantages make it a powerful and versatile trading strategy for stock traders. Careful smoothing and position sizing can help prevent false signals and large losses.
### Risk Analysis
Although the Dynamic Double Exponential Moving Average trading strategy has many advantages, it also has some inherent risks, just like most stock strategies:
1. Since TSI and signal lines are based on historical price data, there is always a risk of false signals, especially in situations of high market volatility.
2. If the market fluctuates around the zero line of the TSI indicator, a pullback may occur. This may result in losses.
3. Large gaps...if the trend continues, TSI may reverse the trend prematurely and miss out on profits.
4. Due to leverage, it is possible to incur losses greater than the limits set by the risk parameters.
However, these risks can be mitigated by applying aspects such as position sizing, stop losses, and other risk management techniques. Additionally, parameters and filters can be further optimized to maximize performance under different market conditions.
### Optimization direction
Some ideas to optimize this strategy include:
1. Test different combinations of double smoothing parameters to find those that produce more accurate trading signals. Long and short cycle parameters can be adjusted for optimization.
2. Add filters based on volatility, trading volume or other indicators to reduce unnecessary trading signals. This reduces transaction frequency while increasing profitability per transaction.
3. Add stop loss logic. For example, stop loss when the TSI value crosses the zero axis. This can reduce unnecessary losses.
4. Evaluate the performance of different trading products such as indices, commodities, etc. under this strategy. Choose the best-performing products to focus on trading.
5. Filter the trading products optimally. For example, evaluate the liquidity and volatility indicators of varieties, and select varieties with higher parameter index rankings for trading.
6. Use machine learning methods to perform forward analysis and select the best parameter combination. This can reduce the bias caused by manual selection and obtain better parameters.
7. Use multiple parameter sets according to different market environments and switch dynamically. For example, a more aggressive parameter combination can be used in a bull market, and a more conservative combination can be used in a bear market.
By testing and optimizing all the above aspects, it is expected to further improve the stability and profitability of the strategy.
### Summarize
In general, this strategy is based on the dual exponential smoothing characteristics of the TSI indicator and designs a relatively stable and reliable stock trading strategy. By dynamically adjusting the position size, the overall risk level can be effectively controlled. This strategy has the advantages of being suitable for both short-term and medium- and long-term transactions.
Of course, like most quantitative trading strategies, this strategy also has certain limitations, mainly reflected in its susceptibility to severe market fluctuations. In addition, parameter selection and filtering conditions also need to be further tested and optimized to obtain stronger adaptability and profitability in a complex and ever-changing market.
||

### Overview

This strategy is named "Dynamic Dual Exponential Moving Average Trading Strategy". It is a quantitative trading strategy based on the dual exponential moving average (DEMA). The strategy calculates the price change rate of stocks, and then performs dual exponential smoothing on both its absolute value and non-absolute value, so as to obtain the True Strength Index (TSI). The strategy generates buy and sell signals based on the golden/dead cross of the TSI value and its signal line.

### Strategy Principle  

The core indicator of this strategy is the True Strength Index (TSI). The calculation formula of TSI is:  

TSI = 100 * (PC1 / PC2)

Where PC1 and PC2 are the dual exponential moving averages of the price change rate and the absolute value of the price change rate, respectively. The dual exponential moving average is calculated by first applying an exponential moving average with one length to the price change rate, and then applying another shorter exponential moving average to the obtained moving average. This dual smoothing can better eliminate the randomness in the price change rate and improve the stability of the TSI indicator.

After calculating the TSI value, the strategy also calculates a signal line for the TSI value. The signal line is defined as an exponential moving average of the TSI value over a certain period. In actual trading, the strategy judges market trends and generates trading signals by observing the relationship between the TSI value and its signal line. When the TSI value crosses above the signal line, it is a buy signal. When the TSI value crosses below the signal line, it is a sell signal.  

Another feature of this strategy is that the trade size is dynamically adjusted. The strategy code sets an initial capital and a risk exposure ratio as input parameters. These two parameters combine with the current price of the stock to dynamically calculate the number of contracts traded or risk exposure. This can better control the overall risk of the entire strategy.

### Advantage Analysis

The dynamic dual exponential moving average trading strategy comes with several advantages:

1. It utilizes the TSI indicator which applies dual exponential smoothing, making it less sensitive to market noise and able to generate more accurate signals.  

2. It builds upon the proven principle of crossing of an indicator and its signal line to generate trading signals. This eliminates many false signals.

3. The strategy dynamically adjusts position sizing based on the risk budget. This helps prevent overtrading and emotions.  

4. It works on daily and weekly timeframes, suitable for both swing trading and positional trading.

5. It is easy to implement in bots and other trading systems due to the simple entry/exit logic.  

6. There are not too many parameters to tune, making the system easy to optimize.

These advantages combined make it a robust and versatile trading strategy for stock traders. The careful smoothing and position sizing help prevent false signals and large losses.  

### Risk Analysis

While the dynamic dual exponential moving average trading strategy has many advantages, it also has some inherent risks like most stock strategies:

1. Since the TSI and signal line are based on historical price data, there is always the risk of incorrect signals especially during volatile market conditions.

2. Whipsaws may occur if the market oscillates around the zero line of the TSI indicator. This can lead to losses.  

3. Large gap moves may result in the strategy closing at a loss since it was not able to exit in time. 

4. If the market continues in a strong trend, the TSI may prematurely reverse the trend resulting in missed profits.

5. Due to the leverage effect, larger losses than the limit set by the risk parameters are possible.

These risks can however be mitigated by aspects like position sizing, stop losses and other risk management techniques. Also, the parameters and filters can be further optimized to maximize performance across varying market conditions.

### Optimization Directions  

Some ideas to optimize this strategy include:

1. Testing different combinations of dual smoothing parameters to find the combination that generates the most accurate trading signals. The long and short cycle parameters can be adjusted for optimization.

2. Adding filters based on volatility, trading volume or other indicators to reduce unnecessary trading signals. This can reduce trade frequency while increasing the profitability of each trade.

3. Incorporating stop loss logic. For example, stopping out when TSI value crosses the zero line. This can reduce unnecessary losses.  

4. Evaluating performance of different trading instruments like indices, commodities etc. under this strategy. Concentrate trading on instruments with best performance.

5. Selectively filtering trading instruments. For example, assess liquidity, volatility metrics of instruments and select ones with higher ranked parameters.  

6. Using machine learning methods like walk-forward analysis to select optimal parameter combinations. This can reduce human bias in selection and obtain better parameters.

7. Employing multiple parameter sets based on varying market regimes, and dynamically switch between them. For example, more aggressive parameters during bull markets, and conservative parameters during bear markets.

By testing and optimizing various aspects above, there is potential to further improve this strategy's stability and profitability.

### Summary  

In summary, this strategy leverages the dual exponential smoothing properties of the TSI indicator to design a relatively stable and reliable stock trading strategy. By dynamically adjusting position sizes, the overall risk level can be effectively controlled. The strategy combines the advantages of being suitable for both short-term and medium-long term trading.

Of course, like most quantitative trading strategies, this strategy also has some limitations, mainly reflected in being prone to effects of drastic market fluctuations. In addition, parameter selection and filtering criteria need further testing and optimization in order to obtain stronger adaptiveness and profitability in the ever-changing financial markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10000|Initial Capital|
|v_input_2|true|Risk Percentage|
|v_input_3|12|Long Length|
|v_input_4|9|Short Length|
|v_input_5|12|Signal Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-06 00:00:00
end: 2024-02-05 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © shankardey7310

//@version=5
strategy("TSI STOCKS", shorttitle="TSI", overlay=true)

initialCapital = input(10000, title="Initial Capital")
riskPercent = input(1, title="Risk Percentage") / 100

longLength = input(12, title="Long Length")
shortLength = input(9, title="Short Length")
signalLength = input(12, title="Signal Length")

price = close
pc = ta.change(price)

double_smooth(src, long, short) =>
    first_smooth = ta.ema(src, long)
    ta.ema(first_smooth, short)

double_smoothed_pc = double_smooth(pc, longLength, shortLength)
double_smoothed_abs_pc = double_smooth(math.abs(pc), longLength, shortLength)
tsi_value = 100 * (double_smoothed_pc / double_smoothed_abs_pc)
tsi_signal = ta.ema(tsi_value, signalLength)

riskAmount = (initialCapital * riskPercent) / close

if (tsi_value > tsi_signal and tsi_value[1] <= tsi_signal[1])
    strategy.entry("Long", strategy.long)

if (tsi_value < tsi_signal and tsi_value[1] >= tsi_signal[1])
    strategy.close("Long")

plot(tsi_value, title="True Strength Index", color=#2962FF)
plot(tsi_signal, title="Signal", color=#E91E63)
hline(0, title="Zero", color=#787B86)
```

> Detail

https://www.fmz.com/strategy/441134

> Last Modified

2024-02-06 09:38:32
