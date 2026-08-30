
> Name

Bollinger Bands Dynamic Take Profit Strategy-Dynamic-Take-Profit-Bollinger-Bands-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13e205166f875bf6bf6.png)

[trans]
#### Overview
This strategy uses the Bollinger Bands indicator to go short when the price hits the upper track and go long when it hits the lower track. It also sets a dynamic take-profit level and closes the position when the position reaches a profit of 1%. The core idea of ​​this strategy is that the price always fluctuates within the Bolinger band and has the characteristics of mean reversion. Therefore, when the price deviates too far from the moving average, reverse operations can be performed to gain spread profits.
#### Strategy Principle
1. Calculate the moving average and standard deviation: Use the simple moving average (SMA) to calculate the moving average (basis) of the closing price, and then calculate the standard deviation (dev) of the closing price relative to the moving average.
2. Calculate the upper track and lower track: the upper track (upper) is basis + dev \* multiplier, and the lower track (lower) is basis - dev \* multiplier, where multiplier is the multiple of the fluctuation amplitude.
3. Generate trading signals: when the closing price crosses the lower rail and the current closing price is less than the opening price, a long signal is generated; when the closing price crosses the upper rail and the current closing price is greater than the opening price, a short signal is generated.
4. Dynamic take-profit: After opening a position, the take-profit price is calculated based on the opening price and take-profit ratio (takeProfitPercentage), and the position is closed when the price reaches the take-profit price.
5. Visualization: Plot Bollinger Bands, Moving Averages, and Trading Signals on the chart.
#### Strategic Advantages
1. Simple and effective: The strategy has clear logic and only uses one technical indicator, making it easy to understand and implement.
2. Wide applicability: Bollinger bands are universal and can be used for a variety of different trading targets and markets.
3. Dynamic take-profit: Compared with fixed take-profit, dynamic take-profit can maximize the profit of profitable orders while controlling risks.
4. Effectively grasp the trend: In the trend market, after the price touches the upper or lower rail, it will usually continue to run in the original direction for a period of time. This strategy can effectively grasp this trend opportunity.
#### Strategy Risk
1. Poor performance in a volatile market: When the market is in a wide range of fluctuations and the price repeatedly breaks through the Bolinger band, this strategy may frequently produce trading signals, resulting in too many transactions and increased handling fee costs.
2. Deep retracement in trending market: If the trend lasts for a long time and the price deviates from the moving average for a long time, this strategy goes against the trend and the retracement may be deep.
3. Difficulty in parameter selection: The parameters of the Bollinger belt (such as length, multiple) have a great impact on the performance of the strategy, but there are no optimal parameters that are universally applicable.
#### Strategy optimization direction
1. Combined with trend judgment: Add trend judgment indicators (such as moving averages) to the strategy, and you can suspend trading or trade with the trend in the trend market.
2. Optimize take-profit and stop-loss: Take-profit and stop-loss can be dynamically adjusted based on volatility indicators such as ATR in order to obtain a better return-to-risk ratio.
3. Multi-factor combination: Consider using Bollinger Bands in conjunction with other technical indicators (such as RSI, MACD, etc.) to improve signal accuracy and reduce false signals.
4. Fundamental filtering: After generating a trading signal, it can be confirmed twice through fundamental data (such as financial reports, industry data, etc.) to improve the robustness of the strategy.
#### Summary
This strategy uses the Bollinger Band to build a simple and effective trading system, taking the price touching the upper and lower rails as a signal, and at the same time using a dynamic stop-profit method to control risks. The strategy performs better in trending markets, but may face frequent trading problems in volatile markets. In the future, the strategy can be improved from the aspects of trend judgment, stop-profit and stop-loss optimization, factor combination, fundamental filtering, etc., in order to obtain more stable returns.
|| 

#### Overview
This strategy utilizes the Bollinger Bands indicator to go short when the price touches the upper band and go long when it touches the lower band. It sets a dynamic take profit level and closes the position when it reaches 1% profit. The core idea is that the price always fluctuates within the Bollinger Bands and has a mean-reverting characteristic, so we can take reverse positions when the price deviates too far from the moving average to capture the price difference.

#### Strategy Principles
1. Calculate the moving average and standard deviation: Use the Simple Moving Average (SMA) to calculate the moving average of the closing price (basis), and then calculate the standard deviation (dev) of the closing price relative to the moving average.
2. Calculate the upper and lower bands: The upper band is basis + dev \* multiplier, and the lower band is basis - dev \* multiplier, where multiplier is a multiple of the volatility amplitude.
3. Generate trading signals: When the closing price crosses above the lower band and the current close is less than the open, a long signal is generated; when the closing price crosses below the upper band and the current close is greater than the open, a short signal is generated.
4. Dynamic take profit: After opening a position, calculate the take profit price based on the entry price and the take profit percentage. Close the position when the price reaches the take profit level.
5. Visualization: Plot the Bollinger Bands, moving average, and trading signals on the chart.

#### Strategy Advantages
1. Simple and effective: The strategy logic is clear and uses only one technical indicator, making it easy to understand and implement.
2. Wide applicability: Bollinger Bands have universal applicability and can be used for various trading instruments and markets.
3. Dynamic take profit: Compared to fixed take profit, dynamic take profit can maximize the profit of winning trades while controlling risk.
4. Effectively capture trends: In trending markets, after the price touches the upper or lower band, it usually continues to move in the original direction for some time. This strategy can effectively seize such trend opportunities.

#### Strategy Risks
1. Poor performance in ranging markets: When the market is in wide fluctuations and prices repeatedly break through the Bollinger Bands, the strategy may generate frequent trading signals, resulting in excessive trading and increased transaction costs.
2. Deep retracements in trending markets: If a trend lasts for a long time and prices deviate from the moving average for an extended period, the strategy goes against the trend, potentially leading to deep retracements.
3. Difficulty in parameter selection: The parameters of the Bollinger Bands (such as length and multiplier) have a significant impact on the strategy performance, but there are no universally optimal parameters.

#### Strategy Optimization Directions
1. Incorporate trend analysis: Add trend identification indicators (such as moving averages) to the strategy. In trending markets, trading can be suspended or follow the trend.
2. Optimize take profit and stop loss: Dynamically adjust the take profit and stop loss based on volatility indicators such as ATR to achieve a better risk-reward ratio.
3. Multi-factor combination: Consider combining Bollinger Bands with other technical indicators (such as RSI, MACD, etc.) to improve signal accuracy and reduce false signals.
4. Fundamental filtering: After generating trading signals, use fundamental data (such as financial reports, industry data, etc.) for secondary confirmation to enhance the robustness of the strategy.

#### Summary
This strategy constructs a simple and effective trading system using Bollinger Bands, taking the price touching the upper and lower bands as signals, and adopting dynamic take profit to control risk. The strategy performs well in trending markets but may face frequent trading issues in ranging markets. Further improvements can be made in terms of trend analysis, take profit and stop loss optimization, factor combination, and fundamental filtering to achieve more robust returns.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-01 00:00:00
end: 2024-04-30 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Future Price Prediction", overlay=true)

// Ayarlar
length = input.int(14, "Length")
mult = input.float(2.0, "Multiplier")
showBands = input.bool(true, "Show Bands")
takeProfitPercentage = 1.0

// Ortalama ve Standart Sapma Hesaplamaları
basis = ta.sma(close, length)
dev = mult * ta.stdev(close, length)

// Üst ve Alt Bantlar
upper = basis + dev
lower = basis - dev

// Grafikte Gösterim
plot(basis, color=color.blue, linewidth=2, title="Basis")
plot(showBands ? upper : na, color=color.red, linewidth=1, title="Upper Band")
plot(showBands ? lower : na, color=color.green, linewidth=1, title="Lower Band")

// Al-Sat Sinyalleri
longCondition = ta.crossover(close[1], lower[1]) and close[1] < open[1]
shortCondition = ta.crossunder(close[1], upper[1]) and close[1] > open[1]

// Kar al seviyeleri
float longTakeProfit = na
float shortTakeProfit = na

if longCondition
    longTakeProfit := close * (1 + takeProfitPercentage / 100)
if shortCondition
    shortTakeProfit := close * (1 - takeProfitPercentage / 100)

// Strateji Giriş ve Çıkış
if longCondition
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit", from_entry="Buy", limit=longTakeProfit)

if shortCondition
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit", from_entry="Sell", limit=shortTakeProfit)

// Al-Sat Sinyalleri Grafikte Gösterim
plotshape(series=longCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=shortCondition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// Bilgi Tablosu
var table data = table.new(position.bottom_right, 2, 2, frame_color=color.black, frame_width=1)
if barstate.islast
    table.cell(data, 0, 0, "Current Price", text_color=color.white)
    table.cell(data, 1, 0, str.tostring(close))
    table.cell(data, 0, 1, "Predicted Basis", text_color=color.white)
    table.cell(data, 1, 1, str.tostring(basis))

```

> Detail

https://www.fmz.com/strategy/452360

> Last Modified

2024-05-24 17:54:47
