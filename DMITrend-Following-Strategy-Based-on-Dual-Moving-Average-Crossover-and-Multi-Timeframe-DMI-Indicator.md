
> Name

Trend-Following-Strategy-Based-on-Dual-Moving-Average-Crossover-and-Multi-Timeframe-DMI-Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/21dfc12d8ed6b3f98f9.png)
[trans]

## Strategy Overview
This article introduces a quantitative trading strategy called "Kyrie Crossover @zaytrade". This strategy combines the double moving average crossover and the multi-time period DMI indicator to make trading decisions by capturing market trends. The core of the strategy is to use the cross signals of the short-term moving average (10-period EMA) and the long-term moving average (323-period EMA), and at the same time combine the DMI indicators of multiple time periods such as 5 minutes, 15 minutes, 30 minutes and 1 hour to confirm the direction and strength of the trend.
## Strategy Principle
The rationale for this strategy can be divided into the following parts:
1. **Double Moving Average Crossover:** The strategy uses short-term EMA (10 periods) and long-term EMA (323 periods) to capture market trends. When the short-term EMA crosses above the long-term EMA, it indicates a potential long opportunity; when the short-term EMA crosses below the long-term EMA, it indicates a potential short opportunity. This moving average crossover method can effectively identify turning points and trend directions in the market.
2. **Multi-time period DMI indicator:** In order to further confirm the direction and intensity of the trend, the strategy uses the multi-time period DMI indicator. The DMI indicator consists of ADX (Average Directional Index), +DI (Upward Direction Index) and -DI (Downward Directional Index). By comparing the relative strength of +DI and -DI, ​​you can determine whether the current trend is bullish or bearish. The strategy calculates the DMI indicator on multiple time periods such as 5 minutes, 15 minutes, 30 minutes and 1 hour to obtain more comprehensive trend information.
3. **Trend Confirmation:** The strategy confirms the trend by comprehensively considering moving average crossover signals and multi-time period DMI indicators. When the moving average crossover signal is consistent with the trend direction of the DMI indicator, the strategy will generate corresponding trading signals. For example, when the short-term EMA crosses the long-term EMA and the DMI indicator on multiple time periods shows a bullish trend, the strategy will generate a long signal.
4. **Risk Management:** The strategy uses a position management method based on risk percentage. Users can control the risk exposure of each transaction by setting the `riskPercentageEMA` parameters. Additionally, the strategy utilizes stop-loss orders to limit potential losses.
## Strategic Advantages
1. **Capture market trends:** By combining double moving average crossovers and multi-time period DMI indicators, the strategy can effectively capture the main trends of the market. This method can help traders follow the general direction of the market and increase the probability of successful transactions.
2. **Multiple time period confirmation:** The strategy calculates the DMI indicator on multiple time periods, including 5 minutes, 15 minutes, 30 minutes and 1 hour. This multi-time period analysis method can provide more comprehensive and reliable trend confirmation signals and reduce the occurrence of false signals.
3. **Flexible parameter settings:** The strategy provides multiple adjustable parameters, such as short-term EMA period, long-term EMA period, ADX smoothing period and DI length, etc. Users can optimize these parameters according to their own trading style and market characteristics to obtain better trading performance.
4. **Risk Management:** The strategy has a built-in position management method based on risk percentage. Users can control the risk exposure of each transaction by setting the `riskPercentageEMA` parameters. In addition, the strategy also uses stop-loss orders to limit potential losses, improving the effectiveness of risk management.
## Strategy Risk
1. **Parameter Optimization:** The performance of the strategy depends largely on the choice of parameters. Improper parameter settings may lead to poor strategy performance or even large retracements. Therefore, in practical applications, parameters need to be optimized and tested to find the best parameter combination suitable for current market conditions.
2. **Trend Delay:** Since the strategy relies on moving average crossovers and DMI indicators to confirm trends, there may be a certain delay in the generation of signals when the market is changing rapidly. This means that the strategy may miss some early trend opportunities, or generate signals only when the trend has already reversed.
3. **Shocking Market:** In a volatile market, price fluctuations may lead to frequent moving average crossovers and changes in the DMI indicator. This may cause the strategy to generate more trading signals, increasing transaction costs and drawdown risk. Therefore, in volatile markets, the performance of the strategy may be affected.
4. **Black Swan Event:** The strategy is based on historical data and statistical models. For some extreme market events, such as black swan events, the strategy may not be able to respond correctly in time. This can cause the strategy to suffer larger losses in these special circumstances.
## Optimization direction
1. **Dynamic parameter adjustment:** You can consider introducing a dynamic parameter adjustment mechanism to adaptively adjust strategy parameters according to market volatility and trend intensity. This can help the strategy better adapt to different market environments and improve the robustness of the strategy.
2. **Multi-factor confirmation:** In addition to moving average crossover and DMI indicators, other technical indicators or fundamental factors can be introduced to further confirm the trend. For example, indicators such as trading volume, volatility, market sentiment, etc. can be combined to obtain more reliable trading signals.
3. **Take profit and stop loss optimization:** You can optimize the position of take profit and stop loss, such as using trailing stop loss, dynamic stop loss and other methods. This can help strategies better protect profits while limiting potential losses.
4. **Position Management:** More advanced position management methods can be introduced, such as Kelly's formula, fixed proportion investment, etc. This can help strategies dynamically adjust positions in different market environments and improve capital utilization efficiency and risk control capabilities.
5. **Machine learning optimization:** You can try to combine machine learning algorithms with this strategy, and optimize the parameter selection and signal generation of the strategy through learning and pattern recognition of historical data. This can help the strategy automatically adapt to market changes and improve the adaptability and robustness of the strategy.
## Summarize
This article introduces a quantitative trading strategy based on double moving average crossover and multi-time period DMI indicator. This strategy makes trading decisions by capturing market trends, while using risk management measures to control potential losses. The advantage of the strategy is that it can effectively identify the main trends of the market and improve the reliability of the signal through confirmation of multiple time periods. However, the strategy also has some risks, such as parameter optimization, trend delay, volatile markets and black swan events. In order to further optimize the strategy, you can consider introducing methods such as dynamic parameter adjustment, multi-factor confirmation, stop-profit and stop-loss optimization, position management and machine learning. In general, this strategy provides quantitative traders with a trading idea based on trend following. Through reasonable optimization and improvement, it is expected to achieve good performance in actual trading.
|| 

## Strategy Overview

This article introduces a quantitative trading strategy named "Kyrie Crossover @zaytrade". The strategy combines dual moving average crossover and multi-timeframe DMI indicator to capture market trends for trading decisions. The core of the strategy is to utilize the crossover signals of a short-term moving average (10-period EMA) and a long-term moving average (323-period EMA), while confirming the trend direction and strength using DMI indicators across multiple timeframes such as 5-minute, 15-minute, 30-minute, and 1-hour.

## Strategy Principles

The principles of this strategy can be divided into the following parts:

1. **Dual Moving Average Crossover:** The strategy uses a short-term EMA (10-period) and a long-term EMA (323-period) to capture market trends. When the short-term EMA crosses above the long-term EMA, it indicates a potential long opportunity; when the short-term EMA crosses below the long-term EMA, it indicates a potential short opportunity. This moving average crossover method can effectively identify market turning points and trend directions.

2. **Multi-Timeframe DMI Indicator:** To further confirm the trend direction and strength, the strategy employs DMI indicators across multiple timeframes. The DMI indicator consists of ADX (Average Directional Index), +DI (Positive Directional Indicator), and -DI (Negative Directional Indicator). By comparing the relative strength of +DI and -DI, it can be determined whether the current trend is bullish or bearish. The strategy calculates DMI indicators on 5-minute, 15-minute, 30-minute, and 1-hour timeframes to obtain more comprehensive trend information.

3. **Trend Confirmation:** The strategy confirms the trend by comprehensively considering the moving average crossover signals and multi-timeframe DMI indicators. When the moving average crossover signal aligns with the trend direction indicated by the DMI indicators, the strategy generates corresponding trading signals. For example, when the short-term EMA crosses above the long-term EMA, and multiple timeframes of DMI indicators show a bullish trend, the strategy generates a long signal.

4. **Risk Management:** The strategy employs a risk percentage-based position sizing method. Users can control the risk exposure of each trade by setting the `riskPercentageEMA` parameter. Additionally, the strategy utilizes stop-loss orders to limit potential losses.

## Strategy Advantages

1. **Trend Capturing:** By combining dual moving average crossover and multi-timeframe DMI indicators, the strategy can effectively capture the main trends in the market. This approach helps traders align with the market's overall direction, increasing the probability of successful trades.

2. **Multi-Timeframe Confirmation:** The strategy calculates DMI indicators on multiple timeframes, including 5-minute, 15-minute, 30-minute, and 1-hour. This multi-timeframe analysis approach provides more comprehensive and reliable trend confirmation signals, reducing the occurrence of false signals.

3. **Flexible Parameter Settings:** The strategy offers various adjustable parameters, such as short-term EMA period, long-term EMA period, ADX smoothing period, and DI length. Users can optimize these parameters based on their trading style and market characteristics to achieve better trading performance.

4. **Risk Management:** The strategy incorporates a risk percentage-based position sizing method, allowing users to control the risk exposure of each trade by setting the `riskPercentageEMA` parameter. Moreover, the strategy utilizes stop-loss orders to limit potential losses, enhancing risk management effectiveness.

## Strategy Risks

1. **Parameter Optimization:** The performance of the strategy largely depends on the choice of parameters. Improper parameter settings may lead to suboptimal strategy performance or even significant drawdowns. Therefore, in practical application, it is necessary to optimize and test the parameters to find the best parameter combination suitable for the current market conditions.

2. **Trend Delay:** As the strategy relies on moving average crossovers and DMI indicators to confirm trends, there may be a certain delay in signal generation during rapidly changing market conditions. This means that the strategy may miss some early trend opportunities or generate signals after the trend has already reversed.

3. **Choppy Markets:** In choppy markets, price fluctuations may lead to frequent moving average crossovers and changes in DMI indicators. This can result in the strategy generating more trading signals, increasing trading costs and drawdown risks. Therefore, the strategy's performance may be affected in choppy market conditions.

4. **Black Swan Events:** The strategy is based on historical data and statistical models. For extreme market events, such as black swan events, the strategy may not be able to react correctly in a timely manner. This can lead to significant losses for the strategy in these special circumstances.

## Optimization Directions

1. **Dynamic Parameter Adjustment:** Consider introducing a dynamic parameter adjustment mechanism that adaptively adjusts strategy parameters based on market volatility and trend strength. This can help the strategy better adapt to different market environments and improve its robustness.

2. **Multi-Factor Confirmation:** In addition to moving average crossovers and DMI indicators, other technical indicators or fundamental factors can be introduced to further confirm trends. For example, combining volume, volatility, market sentiment, and other indicators can provide more reliable trading signals.

3. **Stop-Loss and Take-Profit Optimization:** Optimize the placement of stop-loss and take-profit levels, such as using trailing stops or dynamic stop-loss methods. This can help the strategy better protect profits while limiting potential losses.

4. **Position Sizing:** Introduce more advanced position sizing methods, such as the Kelly Criterion or fixed fractional investing. This can help the strategy dynamically adjust positions in different market environments, improving capital utilization efficiency and risk control capabilities.

5. **Machine Learning Optimization:** Attempt to combine machine learning algorithms with the strategy. Through learning and pattern recognition of historical data, optimize the strategy's parameter selection and signal generation. This can help the strategy automatically adapt to market changes, enhancing its adaptability and robustness.

## Conclusion

This article introduced a quantitative trading strategy based on dual moving average crossover and multi-timeframe DMI indicator. The strategy makes trading decisions by capturing market trends while employing risk management measures to control potential losses. The strategy's advantages lie in its ability to effectively identify the main trends in the market and improve signal reliability through multi-timeframe confirmation. However, the strategy also has certain risks, such as parameter optimization, trend delay, choppy markets, and black swan events. To further optimize the strategy, methods such as dynamic parameter adjustment, multi-factor confirmation, stop-loss and take-profit optimization, position sizing, and machine learning can be considered. Overall, this strategy provides quantitative traders with a trend-following trading approach. With reasonable optimization and improvement, it has the potential to achieve good performance in actual trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|Short-Term EMA Period|
|v_input_int_2|21|Long-Term EMA Period|
|v_input_float_1|true|Risk Percentage EMA|
|v_input_1|14|ADX Smoothing|
|v_input_2|14|DI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-16 00:00:00
end: 2024-03-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Kyrie Crossover @zaytrade ", overlay=true, calc_on_every_tick=true)

// Input parameters for EMA
shortTermEMA = input.int(9, title="Short-Term EMA Period")
longTermEMA = input.int(21, title="Long-Term EMA Period")
riskPercentageEMA = input.float(1, title="Risk Percentage EMA", minval=0.1, maxval=5, step=0.1)

// Calculate EMAs
emaShort = ta.ema(close, shortTermEMA)
emaLong = ta.ema(close, longTermEMA)

// EMA Crossover Strategy
longConditionEMA = ta.crossover(emaShort, emaLong)
shortConditionEMA = ta.crossunder(emaShort, emaLong)

// Input parameters for DMI
adxlen = input(14, title="ADX Smoothing")
dilen = input(14, title="DI Length")

// DMI Logic
dirmov(len) =>
    up = ta.change(high)
    down = -ta.change(low)
    truerange = ta.tr
    plus = fixnan(100 * ta.rma((up > down ? up : 0), len) / truerange)
    minus = fixnan(100 * ta.rma((down > up ? down : 0), len) / truerange)
    [plus, minus]

adx(dilen, adxlen) => 
    [plus, minus] = dirmov(dilen)
    sum = plus + minus
    adxValue = 100 * ta.rma(math.abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
    [adxValue, plus, minus]

// Function to get trend and strength for a given timeframe
getTrendAndStrength(_source, _dilen, _adxlen) =>
    [adxValue, up, down] = adx(_dilen, _adxlen)
    var string trendIndication = ""
    var string trendStrength = ""
    if (up > down) or ((up > down) and (up > down) and (up > adxValue)) // Bullish condition
        trendIndication := "Bullish"
        trendStrength := "Strengthening" 
    else if (down > up) or ((down > up) and (down > up) and (down > adxValue)) // Bearish condition
        trendIndication := "Bearish"
        trendStrength := "Weakening" 
    else
        trendIndication := "No Clear Trend"
        trendStrength := "Sideways"
    [trendIndication, trendStrength]

// Get trend and strength for selected timeframes
[tf1_trend, tf1_strength] = request.security(syminfo.tickerid, "5", getTrendAndStrength(close, dilen, adxlen))
[tf2_trend, tf2_strength] = request.security(syminfo.tickerid, "15", getTrendAndStrength(close, dilen, adxlen))
[tf3_trend, tf3_strength] = request.security(syminfo.tickerid, "30", getTrendAndStrength(close, dilen, adxlen))
[tf4_trend, tf4_strength] = request.security(syminfo.tickerid, "60", getTrendAndStrength(close, dilen, adxlen))
[current_trend, _] = getTrendAndStrength(close, dilen, adxlen)

// Define colors based on trend indication
tf1_color = tf1_trend == "Bullish" ? color.green : (tf1_trend == "Bearish" ? color.red : color.white)
tf2_color = tf2_trend == "Bullish" ? color.green : (tf2_trend == "Bearish" ? color.red : color.white)
tf3_color = tf3_trend == "Bullish" ? color.green : (tf3_trend == "Bearish" ? color.red : color.white)
tf4_color = tf4_trend == "Bullish" ? color.green : (tf4_trend == "Bearish" ? color.red : color.white)
current_color = current_trend == "Bullish" ? color.green : (current_trend == "Bearish" ? color.red : color.white)

// Create and fill the enhanced table for DMI
var table dmiTable = na
if (barstate.islast)
    dmiTable := table.new(position.top_right, 6, 1)
    table.cell(dmiTable, 0, 0, "DMI Metrics", bgcolor=color.new(color.black, 90), width=15, height=4, text_color=color.white)
    table.cell(dmiTable, 1, 0, "5m Trend: " + tf1_trend, bgcolor=tf1_color, width=15, height=4, text_color=color.white)
    table.cell(dmiTable, 2, 0, "15m Trend: " + tf2_trend, bgcolor=tf2_color, width=15, height=4, text_color=color.white)
    table.cell(dmiTable, 3, 0, "30m Trend: " + tf3_trend, bgcolor=tf3_color, width=15, height=4, text_color=color.white)
    table.cell(dmiTable, 4, 0, "1h Trend: " + tf4_trend, bgcolor=tf4_color, width=15, height=4, text_color=color.white)
    table.cell(dmiTable, 5, 0, "Current Trend: " + current_trend, bgcolor=current_color, width=15, height=4, text_color=color.white)

// Strategy logic
if (longConditionEMA)
    strategy.entry("Long", strategy.long)
if (shortConditionEMA)
    strategy.entry("Short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/445813

> Last Modified

2024-03-22 14:23:30
