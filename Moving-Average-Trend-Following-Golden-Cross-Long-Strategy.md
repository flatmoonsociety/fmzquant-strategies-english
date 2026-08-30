
> Name

Moving-Average-Trend-Following-Golden-Cross-Long-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/84de706e57cdf7dedb6d35cf653ebf88cf8c070c62ff7766a2b32c949ebccb00.png)

[trans]


### Overview
This strategy combines the moving average indicator and MACD indicator to design a relatively conservative long strategy. This strategy mainly determines the market trend based on whether the price stands above the 200-day simple moving average, and then selects the buying opportunity based on the 20-day exponential moving average and the golden cross of the MACD indicator. When the market is up, buy only when MACD is golden cross, and stop loss when MACD is dead cross; when the market is down, buy only when the price is above the 20-day exponential moving average and MACD is golden cross, and stop loss when MACD is dead cross. This double confirmation mechanism can effectively avoid frequent buying and selling in volatile market conditions.
### Strategy Principles
First, this strategy uses the 200-day simple moving average SMA to determine the current price trend. If the closing price is higher than the SMA, the market is judged to be in an upward trend; if the closing price is lower than the SMA, the market is judged to be in a downward trend.
Secondly, in an uptrend, the strategy ignores the conditions of the 20-day exponential moving average EMA and only issues a buy signal when the fast line of MACD breaks above the slow line (i.e. MACD golden cross). At this time, a trend following strategy is adopted. As long as MACD remains golden cross, hold long orders. When the MACD fast line crosses the slow line (i.e. MACD crosses), a stop loss is executed.
In a downtrend, the strategy becomes conservative and a buy signal will only be issued when the price closes above the 20-day EMA and the MACD crosses golden, which requires double confirmation. At this time, the stop loss is still when MACD crosses.
Through this mechanism, the strategy adopts a more aggressive strategy when the trend is clear (when the price is above or below the 200-day SMA), and a more cautious strategy when the price is in a volatile range, which can effectively avoid unnecessary transactions caused by false signals.
### Strategic Advantages
1. This strategy combines trend judgment and double confirmation mechanism, which can effectively filter noise and avoid false signals, thereby reducing unnecessary transactions.
2. When the trend is obvious, the strategy follows the trend in time; when the trend is not obvious, the strategy adopts a cautious attitude, which can reduce losses.
3. The strategy uses a combination of moving average indicators and MACD indicators to make buying and selling signals more reliable.
4. The strategy is simple to operate and easy to implement, and is suitable for investors of different levels.
5. The strategy adopts fixed stop loss conditions, which can effectively control single losses.
### Strategy Risk
1. This strategy relies too much on technical indicators and cannot cope with the tense market caused by emergencies.
2. The double confirmation mechanism may cause the strategy to sometimes miss buying opportunities.
3. The MACD indicator has hysteresis, which may cause delays in buying and selling points.
4. If the stop loss point is set improperly, it may cause the loss to expand.
5. The 200-day SMA cannot accurately judge the long-term trend, and errors in judgment may occur.
6. As a filter, the moving average can easily produce trading signals with too small amplitude.
### Strategy optimization
1. You can consider adding other indicators to the combination, such as KDJ, Bollinger Bands, etc., to make the buying and selling signals more accurate.
2. You can test other long-term moving averages, such as the 120-day EMA, to see if you can better judge the long-term trend.
3. You can optimize the number of days of the moving average and find the best parameter combination.
4. You can add a take-profit strategy instead of just relying on stop-loss to lock in more profits.
5. The moving average parameters can be adjusted according to different markets to make the strategy more adaptable.
6. You can consider adding machine learning algorithms, using historical data to train models and automatically optimize parameters.
### Summarize
This strategy integrates the advantages of moving averages and MACD indicators, achieving better risk control while remaining relatively simple. By judging trends and double confirmation, noise signals can be effectively filtered. However, the strategy also has certain limitations and needs to be further optimized and improved in its ability to respond to emergencies. Overall, this strategy provides a solid reference plan for conservative investors.
||


### Overview

This strategy combines moving average indicators and the MACD indicator to design a relatively conservative long strategy. It mainly uses the 200-day simple moving average to judge the trend, and combines the 20-day exponential moving average and MACD golden cross to select buying opportunities. In an uptrend, it only buys when there is a MACD golden cross and stops loss when there is a MACD dead cross. In a downtrend, it will only buy when the price is above the 20-day EMA and there is a MACD golden cross, and stop loss when there is a MACD dead cross. This dual confirmation mechanism can effectively avoid frequent trading in a volatile market.

### Strategy Logic  

Firstly, the strategy uses the 200-day simple moving average (SMA) to judge the current price trend. If the closing price is above SMA, the trend is judged to be rising. If the closing price is below SMA, the trend is judged to be falling.

Secondly, in an uptrend, the strategy ignores the 20-day exponential moving average (EMA) condition and only sends a buy signal when the MACD fast line crosses above the slow line (MACD golden cross). It holds the long position as long as the MACD stays golden crossed. When the MACD fast line crosses below the slow line (MACD dead cross), it stops loss.

In a downtrend, the strategy becomes more conservative. It only sends a buy signal when the closing price crosses above the 20-day EMA and there is a MACD golden cross, requiring dual confirmation. It still stops loss on MACD dead cross. 

Through this mechanism, the strategy adopts a more aggressive approach when the trend is clear (price is above or below the 200-day SMA). When the price is in a range, it takes a more cautious approach, effectively avoiding false signals.

### Advantages

1. The strategy combines trend judgment and dual confirmation to filter noise and avoid false signals, reducing unnecessary trades.

2. It timely follows the trend when the trend is clear, and adopts a cautious attitude when the trend is unclear, reducing losses.

3. Combining moving averages and MACD makes trading signals more reliable. 

4. The strategy is simple to implement, suitable for investors at all levels.

5. The fixed stop loss mechanism effectively controls single trade loss.

### Risks

1. The strategy relies heavily on technical indicators and cannot adapt to black swan events.

2. The dual confirmation may cause missed buying opportunities sometimes.

3. MACD has lagging issues which may delay trading signals. 

4. Improper stop loss setting may lead to larger losses.

5. The 200-day SMA may not accurately determine long term trends.

6. Moving averages as filters may generate trivial trading signals.

### Optimization

1. Consider combining other indicators like KDJ, Bollinger Bands to make signals more accurate.

2. Test other long term moving averages like 120-day EMA to better determine long term trends.

3. Optimize moving average periods to find the best parameter combination. 

4. Incorporate take profit strategies, not just stop loss, to lock in more profits.

5. Adjust moving average parameters for different markets to improve adaptability.

6. Consider machine learning algorithms to optimize parameters by training models on historical data.

### Summary

The strategy integrates the advantages of moving averages and MACD, achieving good risk control while remaining relatively simple. By judging the trend and requiring dual confirmation, it can filter out noise effectively. But the strategy also has some limitations and needs further optimization and adaptability to black swan events. Overall, it provides conservative investors with a robust reference solution.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|v_input_1|
|v_input_2|20|v_input_2|
|v_input_3|12|fastLength|
|v_input_4|26|slowlength|
|v_input_5|9|MACDLength|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-15 00:00:00
end: 2023-10-22 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title="MACD/EMA Long Strategy",overlay=true,scale=scale.left)



// SMA Indicator - Are we in a Bull or Bear market according to 200 SMA?
SMA = sma(close, input(200))



// EMA Indicator - Are we in a rally or not?
EMA = ema(close, input(20))



//MACD Indicator - Is the MACD bullish or bearish?

fastLength = input(12)
slowlength = input(26)
MACDLength = input(9)

MACD = ema(close, fastLength) - ema(close, slowlength)
aMACD = ema(MACD, MACDLength)
delta = MACD - aMACD

// Set Buy/Sell conditions

[main,signal,histo]=macd(close,fastLength,slowlength,MACDLength)

buy_entry= if close>SMA
    delta>0
else
    delta>0 and close>EMA
    
strategy.entry("Buy",true , when=buy_entry)

alertcondition(delta, title='Long', message='MACD Bullish')


sell_entry = if close<SMA
    delta<0 
else
    delta<0 and close<EMA
strategy.close("Buy",when= sell_entry)


alertcondition(delta, title='Short', message='MACD Bearish')

//plot(delta, title="Delta", style=cross, color=delta>=0 ? green : red )
```

> Detail

https://www.fmz.com/strategy/429951

> Last Modified

2023-10-23 15:22:48
