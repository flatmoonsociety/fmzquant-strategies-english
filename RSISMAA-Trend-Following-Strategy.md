
> Name

Trend following strategy A-Trend-Following-Strategy based on RSI extreme value and SMA moving average filtering
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/af1ac74b0f6970576d.png)

[trans]

### Overview
This strategy combines the extreme value of the Relative Strength Index (RSI) indicator and the filtering of the Simple Moving Average (SMA) to achieve trend tracking. When RSI reaches the extreme value of overbought or oversold, the direction of long and short is determined based on the direction of SMA moving average. This strategy is suitable for U.S. stock indexes, European indexes, Asian indexes, gold and silver and other varieties. Through simple RSI and SMA judgment rules, it can capture the trend.
### Strategy Principles
1. Calculate the RSI indicator value, set the upper limit of the overbought threshold to 65, and the lower limit of the oversold threshold to 45.
2. Calculate the 200-day SMA and determine the trend direction.
3. Go long when the RSI is below 45 (oversold) and the price is above the SMA; go short when the RSI is above 65 (overbought) and the price is below the SMA.
4. When the RSI is above 75 (strongly overbought) and the price is above the SMA, close the long order; when the RSI is below 25 (strongly oversold) and the price is below the SMA, close the short order.
This strategy uses the overbought and oversold range of RSI to determine the entry timing, and then combines it with the trend filtering of SMA to effectively capture the trend. The extreme values ​​of the RSI indicate a possible price reversal, while the directional judgment of the SMA ensures that the trading direction is consistent with the trend. The combination of the two not only ensures reasonable transactions, but also improves the winning rate.
### Strategic Advantages
1. The strategic ideas are simple and clear, easy to understand and master.
2. Based on two well-known indicators, RSI and SMA, easy to operate.
3. RSI extreme values ​​indicate possible reversal points, and SMA filtering ensures the correct trading direction.
4. The parameters are set reasonably to avoid over-trading.
5. Can be widely applied to stock indexes, commodities and other varieties.
6. Can capture larger price fluctuations in trends.
Compared with using the RSI indicator alone, this strategy adds SMA trend judgment and avoids blind long and short positions. Compared with using the SMA system alone, this strategy uses RSI extreme values ​​to enter the market based on the SMA direction, which improves the efficiency of timing. Overall, this strategy combines the advantages of both and is a very practical trend following strategy.
### Risks and Solutions
1. When the SMA moving average crosses, there is a risk of trend reversal. The solution is to shorten the SMA cycle appropriately and increase the sensitivity to trend changes.
2. When RSI diverges, there is a risk of missing trading opportunities. The solution is to combine other indicators such as MACD to judge abnormal movements and prevent divergence.
3. In a volatile market, both RSI and SMA may produce false signals. The solution is to suspend strategic trading after a volatile market is detected.
4. Improper parameter settings may lead to over-trading or missed buying and selling. The solution is to optimize parameters and find the best parameter combination.
5. A single variety test is not enough to evaluate the strategy effect, and multi-variety backtest verification is required.
6. Backtesting is not equal to the actual offer. In the actual offer, capital management and risk management must be controlled.
### Optimization direction
1. Optimize RSI parameters and find the best RSI cycle parameters for different varieties.
2. Optimize the SMA cycle parameters and integrate multiple sets of SMA moving averages.
3. Add a stop-loss mechanism and improve risk control capabilities.
4. Add other indicator judgments to achieve multi-factor verification.
5. Combine with volatility indicators to improve entry rhythm.
6. Develop a parameter adaptive system to achieve dynamic parameter optimization.
7. Test different fund management methods to find the optimal fund management.
8. Create trading strategy sets based on different market conditions to achieve strategy integration.
### Summarize
This RSI extreme value and SMA filtering strategy combines the best of both worlds and realizes trend tracking through simple indicator judgment. The strategy ideas are clear and easy to understand, the parameter settings are reasonable, and it can be widely applied to a variety of varieties. Compared with single RSI and SMA strategies, this strategy significantly improves timing efficiency and winning rate. However, there is also some room for improvement in the strategy, and the robustness and adaptability of the strategy can be further enhanced through parameter optimization, stop-loss mechanisms and other methods. Overall, this strategy provides a very practical and effective trading tool for trend traders.
|| 

### Overview

This strategy combines the extremes of the Relative Strength Index (RSI) indicator and the filtering of the Simple Moving Average (SMA) to track trends. When the RSI reaches extreme overbought or oversold levels, long and short directions are determined based on the SMA direction. The strategy is suitable for US stock indexes, European indexes, Asian indexes, gold, silver and other varieties. Through simple RSI and SMA rules, it effectively captures trends. 

### Strategy Logic

1. Calculate the RSI indicator value, set the overbought threshold upper limit to 65, and the oversold threshold lower limit to 45.

2. Calculate the 200-day SMA to determine the trend direction. 

3. When RSI is below 45 (oversold) and price is above SMA, go long; when RSI is above 65 (overbought) and price is below SMA, go short.

4. When RSI is above 75 (strongly overbought) and price is above SMA, close long positions; when RSI is below 25 (strongly oversold) and price is below SMA, close short positions.

The strategy captures trends effectively by using RSI extremes to time entries and SMA direction for filtering. RSI extremes indicate potential reversals, while SMA direction ensures trades align with the trend. Together, they ensure reasonable trades and higher win rates.

### Advantages

1. Simple and clear strategy logic, easy to understand and master. 

2. Based on well-known RSI and SMA indicators, easy to implement.

3. RSI extremes indicate potential reversal points, SMA filters ensure directional correctness. 

4. Reasonable parameter settings avoid excessive trading.

5. Applicable to multiple products like indexes and commodities. 

6. Captures significant price swings during trends.

Compared to RSI alone, the strategy adds SMA trend filter to avoid blind long/short. Compared to SMA systems alone, the strategy improves timing efficiency by using RSI extremes. Overall, it combines the strengths of both for a practical trend following strategy.

### Risks and Solutions

1. SMA death cross poses trend reversal risks. Use shorter SMA periods for increased sensitivity.

2. RSI divergences risk missing trades. Add other indicators like MACD to detect anomalies.

3. Both RSI and SMA may generate false signals during ranging markets. Pause trading when range-bound market detected.

4. Improper parameter settings lead to overtrading or missed trades. Optimize parameters to find best combination.

5. Single product backtest insufficient to evaluate strategy. Validate across multiple products. 

6. Backtest ≠ live trading. Manage risk and capital in live trading.

### Improvement Directions

1. Optimize RSI periods for different products.

2. Optimize SMA periods, integrate multiple SMAs. 

3. Add stop loss for better risk control.

4. Add other indicators for multi-factor confirmation.

5. Improve entry timing with volatility indicators. 

6. Develop adaptive parameter system for dynamic optimization.

7. Test different capital management approaches for optimum.

8. Create strategy ensemble for different market conditions.

### Conclusion

The RSI extremes with SMA filter strategy combines the strengths of both for effective trend following. The logic is clear and parameters solid. It works across multiple products to significantly improve timing efficiency and win rate compared to RSI or SMA systems alone. There is room for improvements like parameter optimization and stop loss to further enhance robustness and adaptiveness. Overall, it provides trend traders with a very useful and effective tool.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|RSI lenght|
|v_input_int_2|200|  SMA Lenght|
|v_input_float_1|5| stop loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-23 00:00:00
end: 2023-10-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This work is licensed under a Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0) https://creativecommons.org/licenses/by-nc-sa/4.0/
// © wielkieef

//@version=5

strategy('Relative Strength Index Extremes with 200-Day Moving Average Filte', overlay=true, pyramiding=1, initial_capital=10000, default_qty_type=strategy.cash, default_qty_value=36000, calc_on_order_fills=false, slippage=0, commission_type=strategy.commission.percent, commission_value=0.01)

// Rsi
rsi_lenght = input.int(14, title='RSI lenght', minval=0)
rsi_up = ta.rma(math.max(ta.change(close), 0), rsi_lenght)
rsi_down = ta.rma(-math.min(ta.change(close), 0), rsi_lenght)
rsi_value = rsi_down == 0 ? 100 : rsi_up == 0 ? 0 : 100 - 100 / (1 + rsi_up / rsi_down)


//Sma
Length1 = input.int(200, title='  SMA Lenght', minval=1)
SMA1 = ta.sma(close, Length1)

//Strategy Logic
Long = rsi_value < 45 and close > SMA1
Long_exit = rsi_value > 75 and close > SMA1

Short = rsi_value > 65 and close < SMA1
Short_exit = rsi_value < 25 and close < SMA1


if Long
    strategy.entry('Long', strategy.long)

if Short
    strategy.entry('Short', strategy.short)

strategy.close_all(Long_exit or Short_exit)

pera(pcnt) =>
    strategy.position_size != 0 ? math.round(pcnt / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)
stoploss = input.float(title=' stop loss', defval=5, minval=0.5)
los = pera(stoploss)

strategy.exit('SL', loss=los)



//by wielkieef


```

> Detail

https://www.fmz.com/strategy/430044

> Last Modified

2023-10-24 14:47:38
