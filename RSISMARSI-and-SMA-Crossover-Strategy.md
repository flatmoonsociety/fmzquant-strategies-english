
> Name

RSI-and-SMA-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/259bea65aa19a7ae39f6b92d2d71ebf44cfc40f50fa7abb013987332607ced5a.png)
[trans]

### Overview
This strategy is named "RSI and SMA golden cross strategy". Its core idea is to use the RSI indicator to determine overbought and oversold, and combine it with the golden cross of the SMA moving average to form a trading signal. Go long when the RSI is above 50 and the short-term SMA is above the long-term SMA, and go short when the RSI is below 50 and the short-term SMA is below the long-term SMA.
### Strategy Principles
This strategy mainly uses a combination of RSI indicator and SMA moving average to form trading signals. Among them, the RSI indicator is used to determine whether the security price is overbought or oversold. An RSI index above 50 indicates an overbought zone, and an RSI index below 50 indicates an oversold zone. The golden cross of the SMA moving average is also often used to judge trading opportunities. This strategy combines the cross signals of the RSI indicator and the SMA moving average to form the basis for trading decisions.
Specifically, when the RSI indicator is above 50 (overbought zone) and the short-term SMA crosses the long-term SMA (golden cross), go long; when the RSI indicator is below 50 (oversold zone) and the short-term SMA moves below the long-term SMA (death cross), go short. This not only utilizes the function of RSI to determine overbought and oversold, but also utilizes the golden cross signal of the SMA moving average. The combination of the two can improve the accuracy of decision-making.
### Analysis of strategic advantages
Compared with using RSI indicator or SMA moving average alone, the advantages of this strategy combining both are:
1. Can more accurately determine the overbought and oversold conditions of the price. When looking only at the SMA moving average, the price may have entered the overbought and oversold area; when looking only at the RSI, the turning point of the price trend cannot be completely judged. The combination of the two can form a relatively complete basis for judgment.
2. Can filter out some noise signals. Only relying on the golden cross of the SMA moving average may produce some false signals, but combining it with the RSI indicator can filter out these noises.
3. More opportunities to seize trends. When there is a clear trend in the market, RSI alone may miss some opportunities, but combined with the SMA moving average, you can continue to follow the trend and participate in the larger market.
In general, the combination of RSI and SMA can complement each other to form a more complete basis for trading decisions. It can also reduce false signals while capturing trends, and thus may obtain better backtesting indicators.
### Risk Analysis
There are also some potential risks that need to be noted in this strategy:
1. Parameter setting risks. The length of the RSI period and the SMA moving average need to be set appropriately. If the parameters are set improperly, trading signals will be confused.
2. Special market risk. In some special market conditions, the indicator may become invalid, such as price limit Up/Down, price gap after suspension and resumption of trading, etc. This is when trading signals may be wrong.
3. Drawback risk. When there is a major correction in the market, the strategy account will also experience a certain retracement. The maximum loss in this area can be controlled by increasing position management.
4. Implementation difficulty risk. RSI and SMA moving averages are relatively simple, but adjusting parameters and achieving actual profits requires certain skills and experience.
### Optimization direction
This strategy can also be optimized from the following aspects:
1. Test optimized combinations under different parameters. You can try RSI and SMA with different length periods to find the best parameter combination.
2. Add a stop loss strategy. For example, set up trailing stop loss, shrinking stop loss, etc. to lock in profits and control risks.
3. Filter signals in combination with other indicators. Indicators such as MACD and Bollinger Bands can be used to assist in confirming trading signals and reducing errors.
4. Differentiation of parameters for different varieties. Some species parameter settings can be differentially optimized to obtain the best results.
5. Optimize position management strategies. For example, advanced position opening methods such as iskycan, or the establishment of a volatility position adjustment mechanism, etc.
### Summarize
This strategy combines the RSI indicator and the intersection of the SMA moving average to make decisions, which can not only determine whether the price is overbought or oversold, but also seize trend opportunities. Compared with a single indicator, it has the advantages of more accurate judgment and better noise filtering. At the same time, you also need to pay attention to risks such as controlling retracements and optimizing parameter combinations. Better strategic effects can be obtained through continuous optimization. In general, this strategy is simple and practical, and it is a very typical strategy idea for quantitative trading.
||

### Overview  

This strategy named "RSI and SMA Crossover Strategy", its core idea is to use the RSI indicator to judge overbought and oversold conditions, and combine the golden cross and dead cross of SMA lines to generate trading signals. Go long when RSI is higher than 50 and short term SMA is higher than long term SMA, go short when RSI is lower than 50 and short term SMA is lower than long term SMA.  

### Strategy Principle

This strategy mainly combines the RSI indicator and the SMA moving average to form trading signals. The RSI indicator is used to judge the overbought and oversold conditions of security prices. RSI index higher than 50 indicates an overbought area, and lower than 50 indicates an oversold area. The golden cross and dead cross of SMA lines are also commonly used to determine buy and sell timing. This strategy combines the cross signals of the RSI indicator and SMA lines to form the basis for trading decisions.  

Specifically, when the RSI indicator is higher than 50 (overbought area) and the short-term SMA crosses above the long-term SMA (golden cross), go long; when the RSI indicator is lower than 50 (oversold area) and the short-term SMA crosses below the long-term SMA (dead cross), go short. This utilizes both the RSI's ability to judge overbought and oversold conditions, as well as the SMA lines' golden cross and dead cross signals, so that combining the two can improve the accuracy of decisions.

### Advantage Analysis   

Compared with using the RSI indicator or SMA lines alone, the advantages of combining the two in this strategy include:  

1. It can more accurately judge the overbought and oversold conditions of prices. Looking at the SMA lines alone, the price may have already entered the overbought or oversold zone; looking at RSI alone cannot fully determine turns in price trends. Combining the two can form a more complete basis for judgments.

2. It can filter out some noisy signals. Relying solely on the SMA lines' golden crosses and dead crosses, some wrong signals may appear. Combining with the RSI indicator can filter out this noise.  

3. It can capture more trend opportunities. In the event of a clear trend in the market, relying solely on RSI may miss some opportunities, while combining SMA lines can continue to track and participate in bigger market moves.   

In summary, the combination of RSI and SMA complements each other to form a more complete basis for trading decisions. It can capture trends while reducing incorrect signals, thus potentially yielding better backtesting metrics.  

### Risk Analysis  

This strategy also has some potential risks to be aware of:   

1. Parameter setting risk. The periods for RSI and lengths of the SMA lines need to be set appropriately. Incorrect settings may lead to messy trading signals.  

2. Special market conditions risk. Under certain special market conditions, the indicators may fail, such as limit up/down of prices, price gaps after suspensions, etc. Signals may be incorrect in these cases.  

3. Drawdown risk. In the event of larger market pullbacks, the strategy account will also face drawdowns to some extent. This can be controlled by increasing position sizing management.

4. Implementation difficulty risk. Though RSI and SMA lines are relatively simple, fine tuning the parameters and actual profitability requires certain skills and experience.

### Optimization Directions   

This strategy can also be optimized in the following aspects:  

1. Test optimal combination under different parameter settings. Try different period lengths for RSI and SMA to find the optimum.

2. Add stop loss mechanisms, such as trailing stop loss, percentage based stops etc to lock in profits and control risk.  

3. Combine with other indicators to filter signals, such as MACD, Bollinger Bands etc to confirm trades and reduce errors.

4. Differentiate parameters by product. Some products may need differentiated optimization of parameters for best results.   

5. Optimize position sizing schemes, such as iSkycan, volatility adjusted sizing etc.

### Conclusion   

This strategy makes decisions by combining the crossover signals of RSI and SMA, allowing judgement of overbought/oversold conditions while also capturing trend opportunities. Compared to single indicators, it has the advantage of more accurate judgements and noise filtering. At the same time, controlling drawdowns, optimizing parameter combinations and other risks need to be noted as well. With continuous optimization, better strategy performance can be obtained. In summary, this is a simple and practical strategy that demonstrates a typical quantitative trading strategy logic flow.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_2|14|length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-27 00:00:00
end: 2024-01-03 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

/// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ExpertCryptoo1

//@version=5
strategy('RSI and SMA',
         overlay=true,
         initial_capital=1000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=30,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 1, 1, 0, 0)
notInTrade = strategy.position_size <= 0

//==================================Buy Conditions============================================
//RSI
length = input(14)
rsi = ta.rsi(close, length)

//SMA
fastEMA = ta.sma(close, 100)
slowEMA = ta.sma(close, 150)
plot(fastEMA, color = color.green)
plot(slowEMA, color = color.blue)


bullish = ta.crossover(fastEMA, slowEMA) and rsi > 50
bearish = ta.crossover(slowEMA, fastEMA) and rsi < 50

strategy.entry("Long", strategy.long, when=bullish and timePeriod)
strategy.close("Exit", when=bearish)

strategy.entry("Short", strategy.short, when=bearish and timePeriod)
strategy.close("Exit", when=bullish)

```

> Detail

https://www.fmz.com/strategy/437631

> Last Modified

2024-01-04 14:33:24
