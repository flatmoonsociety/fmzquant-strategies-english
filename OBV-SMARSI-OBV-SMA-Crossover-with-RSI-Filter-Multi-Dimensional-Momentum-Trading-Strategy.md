
> Name

Multi-Dimensional Momentum Trading Strategy Based on OBV-SMA Crossover and RSI Filter-OBV-SMA-Crossover-with-RSI-Filter-Multi-Dimensional-Momentum-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1273a07a3e7665fe5c5.png)

[trans]
#### Overview
This strategy is a multi-dimensional momentum trading system that combines the Volume Energy Indicator (OBV), the Moving Average (SMA), and the Relative Strength Index (RSI). The strategy captures market momentum by monitoring the cross signals of OBV and its moving average, and uses the RSI indicator to filter to effectively avoid excessive pursuit of gains and losses. The strategy also integrates percentage stop loss and profit-taking mechanisms to achieve balanced management of risk and return.
#### Strategy Principle
The core logic of the strategy is based on three dimensions:
1. The OBV indicator is used to measure the market sentiment of cumulative trading volume. It reflects the comparison of buying and selling power in the market by calculating the direction of price changes and the accumulation of trading volume.
2. The 20-period moving average of OBV is used as the baseline. When OBV crosses the moving average upwards and the RSI is below 70, a long signal is triggered; when OBV crosses the moving average downwards and the RSI is above 30, a short signal is triggered.
3. The introduction of the RSI indicator serves as a filter to prevent opening positions in excessively overbought and oversold areas, effectively reducing the risk of false breakthroughs.
The strategy uses fixed percentages of stop loss (2%) and profit target (4%). This symmetrical risk management framework helps maintain a stable return-to-risk ratio.
#### Strategic Advantages
1. Multi-dimensional signal confirmation mechanism reduces the impact of false signals
2. Organically combine trading volume, price momentum and overbought and oversold indicators
3. Clear risk management framework, fixed stop loss and profit targets
4. The strategy logic is simple and clear, easy to understand and maintain
5. Excellent visual design, clear display of trading signals and indicators
#### Strategy Risk
1. Stop loss may be triggered frequently in highly volatile markets
2. Fixed percentage stop loss may not be suitable for all market conditions
3. RSI filters may miss some important trend starting points
4. The OBV indicator may produce misleading signals in low liquidity environments
5. The strategy does not consider the impact of market cyclical characteristics
#### Strategy optimization direction
1. Introduce adaptive stop-loss mechanisms, such as ATR stop-loss or volatility-adjusted stop-loss
2. Add trend filters, such as long-period moving averages to determine the main trend direction
3. Optimize RSI parameters and consider dynamically adjusting overbought and oversold thresholds
4. Add trading volume filter conditions to ensure that the signal is triggered under the support of effective trading volume
5. Consider introducing time filtering to avoid periods of high volatility
6. Add a position management mechanism to realize dynamic adjustment of positions
#### Summary
This is a well-designed multi-dimensional momentum trading strategy that combines the advantages of technical indicators to build a complete trading system. The core advantage of the strategy lies in its multi-level signal confirmation mechanism and standardized risk management framework. Although there are some potential risks, the robustness and adaptability of the strategy can be further improved through the suggested optimization directions. The practical value of a strategy is mainly reflected in its clear logic, ease of implementation and maintenance. It is recommended that traders fully test the performance in different market environments and optimize parameters according to specific needs before applying it in real markets. ||
#### Overview
This strategy is a multi-dimensional momentum trading system that combines On-Balance Volume (OBV), Simple Moving Average (SMA), and Relative Strength Index (RSI). It captures market momentum by monitoring crossover signals between OBV and its moving average, while using RSI as a filter to avoid excessive trend chasing. The strategy also incorporates percentage-based stop-loss and take-profit mechanisms to achieve balanced risk-reward management.

#### Strategy Principles
The core logic is built on three dimensions:
1. OBV indicator measures cumulative volume sentiment by calculating the accumulated volume based on price movement direction to reflect market buying and selling power.
2. The 20-period moving average of OBV serves as a baseline. Long signals are triggered when OBV crosses above its moving average with RSI below 70, while short signals are triggered when OBV crosses below with RSI above 30.
3. RSI implementation serves as a filter to prevent trading in overbought/oversold areas, effectively reducing false breakout risks.

The strategy employs fixed percentage stop-loss (2%) and take-profit (4%) levels, creating a symmetric risk management framework that helps maintain a stable risk-reward ratio.

#### Strategy Advantages
1. Multi-dimensional signal confirmation reduces the impact of false signals
2. Organic integration of volume, price momentum, and overbought/oversold indicators
3. Clear risk management framework with fixed stop-loss and profit targets
4. Simple and clear strategy logic, easy to understand and maintain
5. Excellent visualization design with clear trading signals and indicator display

#### Strategy Risks
1. May trigger frequent stop-losses in high volatility markets
2. Fixed percentage stops may not suit all market conditions
3. RSI filtering conditions might miss important trend initiations
4. OBV indicators may generate misleading signals in low liquidity environments
5. Strategy doesn't account for market cyclical characteristics

#### Strategy Optimization Directions
1. Introduce adaptive stop-loss mechanisms, such as ATR-based or volatility-adjusted stops
2. Add trend filters, such as long-period moving averages for main trend direction
3. Optimize RSI parameters, consider dynamic adjustment of overbought/oversold thresholds
4. Add volume screening conditions to ensure signals trigger with valid volume support
5. Consider time filters to avoid high volatility periods
6. Implement position management mechanisms for dynamic position adjustment

#### Summary
This is a well-designed multi-dimensional momentum trading strategy that builds a complete trading system by combining the advantages of technical indicators. The core strength lies in its multi-layered signal confirmation mechanism and standardized risk management framework. While there are potential risks, the suggested optimization directions can further enhance the strategy's robustness and adaptability. The strategy's practical value is mainly reflected in its clear logic, ease of implementation, and maintenance. Traders are advised to thoroughly test performance under different market conditions and optimize parameters according to specific needs before live deployment.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-28 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("OBV Strategy with SMA, RSI, SL and TP (Improved Visualization)", overlay=true)

// حساب OBV يدويًا
obv = ta.cum(math.sign(close - close[1]) * volume)

// إعداد المتوسط المتحرك البسيط لـ OBV
lengthOBV = input(20, title="OBV SMA Length")
obvSMA = ta.sma(obv, lengthOBV)

// إعداد مؤشر RSI
lengthRSI = input(14, title="RSI Length")
rsi = ta.rsi(close, lengthRSI)

// إعدادات وقف الخسارة وجني الأرباح
stopLossPerc = input(2.0, title="Stop Loss %") / 100   // 2% وقف خسارة
takeProfitPerc = input(4.0, title="Take Profit %") / 100   // 4% جني أرباح

// حساب مستوى وقف الخسارة وجني الأرباح
longStopLoss = close * (1 - stopLossPerc)
longTakeProfit = close * (1 + takeProfitPerc)
shortStopLoss = close * (1 + stopLossPerc)
shortTakeProfit = close * (1 - takeProfitPerc)

// إعداد شروط الشراء
longCondition = ta.crossover(obv, obvSMA) and rsi < 70
if (longCondition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit/Stop Loss", "Buy", stop=longStopLoss, limit=longTakeProfit)

// إعداد شروط البيع
shortCondition = ta.crossunder(obv, obvSMA) and rsi > 30
if (shortCondition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit/Stop Loss", "Sell", stop=shortStopLoss, limit=shortTakeProfit)

// رسم OBV والمؤشرات الأخرى على الرسم البياني
plot(obv, title="OBV", color=color.blue, linewidth=2) // رسم OBV بخط أزرق عريض
plot(obvSMA, title="OBV SMA", color=color.orange, linewidth=2) // رسم SMA بخط برتقالي

// رسم إشارات الشراء والبيع على الرسم البياني
plotshape(series=longCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=shortCondition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// رسم RSI في نافذة منفصلة بوضوح أكبر
hline(70, "RSI Overbought", color=color.red, linestyle=hline.style_dashed)
hline(30, "RSI Oversold", color=color.green, linestyle=hline.style_dashed)
plot(rsi, title="RSI", color=color.purple, linewidth=2)

// إضافة منطقة RSI بالألوان
bgcolor(rsi > 70 ? color.new(color.red, 90) : rsi < 30 ? color.new(color.green, 90) : na)

```

> Detail

https://www.fmz.com/strategy/473395

> Last Modified

2024-11-29 16:31:19
