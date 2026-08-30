
> Name

Volume-Price-Indicator-Balanced-Trading-Strategy Based on Volume-Price-Indicator-Balanced-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d59f469553540c160e.png)

[trans]


## Overview
This strategy is a multi-time frame volume and price indicator trading strategy. It uses a combination of the Relative Strength Index (RSI), Average True Range (ATR), Simple Moving Average (SMA), and custom volume and price conditions to identify potential long signals. This strategy will establish a long position when certain conditions such as oversold, volume and price indicator crossover, and price breakthrough are met. At the same time, it also sets stop loss and take profit levels to control the risk-benefit ratio of each order.
## Strategy Principle
This strategy is mainly based on the following key points:
1. When the RSI is lower than the oversold line and has been oversold continuously within the last 10 K lines, it is considered an oversold signal.
2. Multiple sets of volume and price conditions are defined. These volume and price conditions need to be met at the same time before the volume and price indicators are considered to send a long signal.
3. When the closing price breaks through the 13-period SMA from bottom to top, it is regarded as a breakthrough signal for the price.
4. The small period of ATR is lower than the large period, which is also a boosting signal.
5. Combine the above multiple indicator signals to form the final long decision
Specifically, this strategy sets the length and oversold line parameters for the RSI indicator, and calculates the RSI value based on these parameters. When the RSI indicator has multiple consecutive K lines below the oversold line, an oversold signal is generated.
In addition, the strategy defines three transaction volume thresholds and sets multiple sets of volume and price conditions based on data in different time periods. For example, the 90-period magnitude is greater than 1.5 times the 49-period magnitude. When these volume and price conditions are met at the same time, a long signal of the volume and price indicators is issued.
In terms of price, this strategy calculates the 13-period SMA indicator and counts the number of K lines since the price broke through the SMA upward. When the price breaks through the SMA from bottom to top and the number of K lines after the breakthrough is less than 5, it is regarded as a price breakthrough signal.
In terms of ATR period parameters, this strategy specifies the ATR of small period 5 and large period 14. When the small-cycle ATR is lower than the large-cycle ATR, it means that market fluctuations are accelerating and shrinking, which serves as a boosting long signal.
Ultimately, this strategy takes into account the multiple buying conditions mentioned above, including oversold, volume and price indicators, price breakouts, and ATR indicators. When these conditions are met at the same time, a final long signal is generated and a long position is established.
## Strategic Advantages
This strategy has several advantages:
1. Judgment of volume and price indicators in multiple time frames to improve accuracy. The strategy not only considers the volume and price data of a single period, but also evaluates the intersection of multiple sets of volume and price conditions in different periods, which can more accurately determine the concentration of volume and energy.
2. The triple judgment mechanism of oversold + volume + price ensures the reliability of buying signals. Oversold provides the most basic selection of buying timing. In addition, the intersection of volume and price indicators adds additional confirmation to the buying timing, which is highly reliable.
3. Set up a stop-loss and stop-profit mechanism to strictly control the risk of a single transaction. Stop loss and take profit parameters can be adjusted according to personal risk preferences, so as to maximize profits while reasonably controlling the risk of each order.
4. Multi-index integrated judgment increases flexibility. Even if some indicators fail or make errors, other indicators can still be relied upon to ensure certain continued operation capabilities.
## Risks and Countermeasures
There are also some risks with this strategy:
1. Parameter configuration risks. The parameter settings of various indicators directly affect the judgment results, and unreasonable parameters may cause deviations in trading signals. The reasonable values ​​of the parameters need to be carefully verified.
2. The profit margin is limited. As a strategy that integrates multiple indicators for integrated judgment, the frequency of signal generation is relatively conservative, the number of transactions per unit time is small, and there are certain limitations in the profit margin.
3. Risk of indicator divergence. When some indicators send long signals and other indicators send short signals, the strategy cannot determine the optimal decision. This requires identifying and resolving possible divergence between indicators in advance.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Add machine learning model to assist judgment. It can train volume, price and fluctuation characteristic models, assist manually set parameters, and realize the dynamics of parameters.
2. Improve the maturity of the take-profit strategy. For example, you can set floating take-profit, batch take-profit, tracking take-profit, etc., which can further increase the income of each order while preventing swaps.
3. Evaluate the imported handicap data. In addition to K-line volume and price data, position distribution can also be judged by combining in-depth buying and selling data, which can provide additional reference signals.
4. Test and verify the integration of other indicators. This strategy mainly uses indicators such as RSI, ATR and SMA for integration. You can also try to introduce other indicator combinations such as Bollinger Bands and KDJ to enrich and optimize the sources of trading signals.
## Summarize
This strategy comprehensively uses RSI, ATR, SMA and customized volume and price condition judgments to identify potential long opportunities. It also has the advantages of multi-time frame volume and price indicator judgment, triple signal confirmation mechanism, and stop-loss and take-profit risk control. Of course, you also need to pay attention to issues such as parameter configuration risks and profit margin limitations. In the future, this strategy can be further optimized in terms of machine learning assistance, take-profit strategy optimization, handicap data introduction, and indicator integration expansion.
||

## Overview

This strategy is a multi-timeframe volume price indicator trading strategy. It comprehensively utilizes the Relative Strength Index (RSI), Average True Range (ATR), Simple Moving Average (SMA) and custom volume price conditions to identify potential long signals. When certain oversold, volume price crossover, price breakout and other entry conditions are met, this strategy will establish long positions. It also sets stop loss and take profit levels to control the risk-reward ratio per trade.

## Strategy Logic

The key points of this strategy are:

1. When the RSI is below the oversold level and stays oversold for the recent 10 bars, it is considered an oversold signal
2. Multiple sets of volume price conditions are defined, and all these conditions need to be satisfied at the same time to trigger the volume price indicator long signal  
3. When the close price breaks above the 13-period SMA, it is considered a price breakout signal
4. The ATR small period being lower than the ATR big period is also a contributing long signal
5. The strategy combines all the above signals to make the final long entry decision

Specifically, this strategy sets the length and oversold parameters for the RSI indicator and calculates the RSI values based on these parameters. When the RSI stays below the oversold level for multiple successive bars, an oversold signal is triggered.

In addition, the strategy defines 3 volume thresholds and sets up multiple sets of volume price conditions based on data from different timeframes. For example, the volume value of the 90-period is greater than 1.5 times that of the 49-period. When all these volume price conditions are met at the same time, the volume price indicator generates a long signal.

On the price aspect, the strategy calculates the 13-period SMA and counts the number of bars since the price breaks above the SMA. When the price breaks out above the SMA and the number of bars after breakout is less than 5, it is considered a price breakout signal. 

For the ATR period parameters, this strategy specifies a small period of 5 and a big period of 14 for the ATR. When the small period ATR is lower than the big period ATR, it signals that the market volatility is accelerating downward and contributes to the long signal.

Finally, the strategy takes into account all the above entry criteria, including oversold, volume price, price breakout and ATR indicators. When all these conditions are met at the same time, the final long signal is triggered and a long position is established.

## Advantages

This strategy has the following advantages:

1. Multi-timeframe volume price condition judgement improves accuracy. By evaluating multiple sets of volume price data across different timeframes instead of just a single timeframe, the strategy can judge the concentration of trading volumes more precisely.  

2. The triple confirmation mechanism of oversold + volume price + price breakout ensures reliable entry signals. The oversold condition provides the basic timing for entries, while the additional confirmations from volume price and price indicators further ensure the reliability of the long signals.

3. The stop loss and take profit mechanism strictly controls the risk per trade. The stop loss and take profit parameters can be adjusted based on personal risk appetite to maximize profits while reasonably controlling the risk per trade.

4. Integrating multiple indicators increases robustness. Even if some indicators fail or malfunction, the strategy can still rely on other indicators for judgement and ensure a certain level of resilience.

## Risks and Countermeasures
 
There are also some risks with this strategy:

1. Parameter configuration risk. The parameter settings of indicators directly impact the judgement, and improper parameters may lead to biases in the trading signals. The reasonable parameter values need to be carefully validated. 

2. Limited profit potential. As a strategy integrating multiple indicators for collective judgement, its signals tend to be more conservative with relatively fewer trades per unit time, thus the profit potential has some constraints.

3. Indicator divergence risk. When some indicators give out long signals while others give out short signals, the strategy cannot determine the optimal decision. Such potential divergence amongst indicators needs to be identified and resolved in advance.

## Optimization Directions

This strategy can be further optimized in the following aspects:

1. Incorporate machine learning models to aid judgement. Models can be trained on the volume price and volatility features to dynamically tune the manually defined parameters.  

2. Improve the sophistication of take profit strategies, such as trailing stop take profit, partial take profits, etc. to further increase the profit per trade while preventing loss of profit.

3. Evaluate incorporating order book data. In addition to price & volume chart data, order book data also reveals depth liquidity distribution information to provide supplementary reference signals.  

4. Test combinations with other indicators. This strategy mainly utilizes indicators like RSI, ATR and SMA. Other indicators such as Bollinger Bands and KDJ can also be combined to diversify and optimize the sources of trading signals.


## Conclusion

This strategy utilizes a combination of indicators including RSI, ATR, SMA and custom volume price conditions to identify potential long entry opportunities. It has advantages like multi-timeframe volume price evaluation, triple confirmation mechanism and stop loss/take profit risk controls. Nonetheless, risks like parameter configuration, constrained profit potential also need to be noted. In the future, this strategy can be further enhanced via machine learning augmentation, more sophisticated take profit design, incorporation of order book data as well as expanded indicator combinations.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|3|(?▶ Stop Loss/Take Profit => Long-Strategy)Stop-Loss (SL) %|
|v_input_float_2|2|Take-Profit (TP) %|
|v_input_int_1|true|(?▶ ValueWhen)occurrence_ValueWhen_1|
|v_input_int_2|5|occurrence_ValueWhen_2|
|v_input_int_3|170|distance_value_occurrence|
|v_input_int_4|60|(?▶ RSI)Oversold Level|
|v_input_int_5|40|RSI Length|
|v_input_float_3|0.5|(?▶ Volume)volume_threshold_1|
|v_input_float_4|0.4|volume_threshold_2|
|v_input_float_5|0.62|volume_threshold_3|
|v_input_int_6|5|(?▶ Atr)ATR_Small|
|v_input_int_7|14|ATR_Big |
|v_input_int_8|true|(?▶ Time-Period for Back-Testing)Start Day|
|v_input_int_9|true|until Day|
|v_input_int_10|7|Start Month|
|v_input_int_11|true|until Month|
|v_input_int_12|2022|Start Year|
|v_input_int_13|2077|until Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-24 00:00:00
end: 2023-11-23 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// © Kimply_Tr
//@version=5

// Strategy settings and parameters
strategy(title='Volume ValueWhen Velocity', overlay=true)

// Define the stop-loss and take-profit percentages for the long strategy
long_stoploss_value = input.float(defval=3, title='Stop-Loss (SL) %', minval=0, group='▶ Stop Loss/Take Profit => Long-Strategy', inline='2')
long_stoploss_percentage = close * (long_stoploss_value / 100) / syminfo.mintick  // Calculate long stop-loss percentage
long_takeprofit_value = input.float(defval=2, title='Take-Profit (TP) %', minval=0, group='▶ Stop Loss/Take Profit => Long-Strategy', inline='2')
long_takeprofit_percentage = close * (long_takeprofit_value / 100) / syminfo.mintick  // Calculate long take-profit percentage

// Define parameters related to ValueWhen occurrences
occurrence_ValueWhen_1 = input.int(title='occurrence_ValueWhen_1', defval=1, maxval=100, step=1, group="▶ ValueWhen",tooltip ="Its value must be smaller than (occurrence_ValueWhen_2)")  
occurrence_ValueWhen_2 = input.int(title='occurrence_ValueWhen_2', defval=5, maxval=100, step=1, group="▶ ValueWhen" ,tooltip="Its value must be greater than (occurrence_ValueWhen_1)")
distance_value=input.int(title='distance_value_occurrence', defval=170, maxval=5000, step=1, group="▶ ValueWhen" ,tooltip="It indicates the minimum distance between the occurrences of 1 and 2, i.e. the difference between the occurrences of 1 and 2 is greater than (distance_value_occurrence)")

// Define RSI-related parameters
rsi_over_sold = input.int(defval=60, minval=1, title='Oversold Level', group='▶ RSI',inline ='2')  // Input for oversold level in RSI
rsi_length = input.int(defval=40, minval=1, title='RSI Length', group='▶ RSI',inline ='2')  // Input for RSI length
rsi = ta.rsi(close, rsi_length)  // Calculate RSI

// Define volume thresholds
volume_threshold1 = input.float(title='volume_threshold_1', defval=0.5, maxval=10, step=0.1, group="▶ Volume")  
volume_threshold2 = input.float(title='volume_threshold_2', defval=0.4, maxval=10, step=0.1, group="▶ Volume")  
volume_threshold3 = input.float(title='volume_threshold_3', defval=0.62, maxval=10, step=0.1, group="▶ Volume")  

// ATR (Average True Range)
// Define ATR parameters
atr_small = input.int(title='ATR_Small', defval=5, maxval=500, step=1, group="▶ Atr",inline ='2') 
atr_big = input.int(title='ATR_Big ', defval=14, maxval=500, step=1, group="▶ Atr",inline ='2') 

atr_value3 = ta.atr(15)  // Calculate ATR value 3
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Date Range
// Define the date range for back-testing
start_date = input.int(title='Start Day', defval=1, minval=1, maxval=31, group='▶ Time-Period for Back-Testing', inline='1')  // Input for start day
end_date = input.int(title='until Day', defval=1, minval=1, maxval=31, group='▶ Time-Period for Back-Testing', inline='1')  // Input for end day
start_month = input.int(title='Start Month', defval=7, minval=1, maxval=12, group='▶ Time-Period for Back-Testing', inline='2')  // Input for start month
end_month = input.int(title='until Month', defval=1, minval=1, maxval=12, group='▶ Time-Period for Back-Testing', inline='2')  // Input for end month
start_year = input.int(title='Start Year', defval=2022, minval=1800, maxval=3000, group='▶ Time-Period for Back-Testing', inline='3')  // Input for start year
end_year = input.int(title='until Year', defval=2077, minval=1800, maxval=3000, group='▶ Time-Period for Back-Testing', inline='3')  // Input for end year
in_date_range = time >= timestamp(syminfo.timezone, start_year, start_month, start_date, 0, 0) and time < timestamp(syminfo.timezone, end_year, end_month, end_date, 0, 0)  // Check if the current time is within the specified date range
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
was_over_sold = ta.barssince(rsi <= rsi_over_sold) <= 10  // Check if RSI was oversold in the last 10 bars
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
getVolume(symbol, bar) =>
    request.security(syminfo.tickerid, "D", volume)[bar]  // Function to get volume data for a specific symbol and bar

getVolume2(symbol, bar) =>
    request.security(syminfo.tickerid, "39", volume)[bar]  // Function to get volume data for a specific symbol and bar 2
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

firstCandleColor1 = request.security(syminfo.tickerid, "D", close[2] > open[1] ? 1 : 0)
firstCandleColor2 = request.security(syminfo.tickerid, "1", close[2] > open[0] ? 1 : 0)
firstCandleColor3 = request.security(syminfo.tickerid, "W", close[1] > open[1] ? 1 : 0)

firstCandleColor= ((firstCandleColor1+firstCandleColor2)) > firstCandleColor3 ? 1 : 0

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
sma = ta.sma(close, 13)  // Calculate the simple moving average (SMA) of the close price over 13 periods
numCandles = ta.barssince(close > sma)  // Count the number of candles since the close price crossed above the SMA
atr1=request.security(syminfo.tickerid, "30", ta.atr(atr_small)<ta.atr(atr_big))  // Get the ATR value for the specific security and timeframe (30 minutes) and check if ATR_small is less than ATR_big

prevClose = ta.valuewhen(close > sma, close, occurrence_ValueWhen_1)  // Get the close price when it first crosses above the SMA based on occurrence_ValueWhen_1
prevCloseBarsAgo = ta.valuewhen(close > sma, close, occurrence_ValueWhen_2)  // Get the close price when it first crosses above the SMA based on occurrence_ValueWhen_2
prevCloseChange =  (prevCloseBarsAgo - prevClose )  // Calculate the change in the close price between the occurrences of crossing above the SMA

atrval=(atr_value3>140) or (atr_value3 < 123)  // Check if atr_value3 is either greater than 140 or less than 123

Condition =  getVolume(syminfo.tickerid, 90) > volume_threshold1 * getVolume(syminfo.tickerid, 49)   and getVolume(syminfo.tickerid, 110) > volume_threshold3 * getVolume(syminfo.tickerid, 49)  and getVolume2(syminfo.tickerid, 30) > volume_threshold2 * getVolume2(syminfo.tickerid, 55) and getVolume2(syminfo.tickerid, 7) > volume_threshold2 * getVolume2(syminfo.tickerid, 3)  // Check multiple volume conditions

buy_signal=Condition  and atrval and firstCandleColor==0 and  was_over_sold and  prevCloseChange> distance_value and atr1 and  numCandles<5  // Determine if the buy signal is generated based on various conditions

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Long Strategy
// Enter long position if the buy signal conditions are met and within the specified date range
if buy_signal and in_date_range
    strategy.entry('Long', strategy.long, alert_message='Open Long Position')  // Enter long position
    strategy.exit('Long SL/TP', from_entry='Long', loss=long_stoploss_percentage, profit=long_takeprofit_percentage, alert_message='Your SL/TP-Limit for the Long-Strategy has been activated.')  // Exit long position with stop-loss and take-profit



```

> Detail

https://www.fmz.com/strategy/433102

> Last Modified

2023-11-24 14:35:13
