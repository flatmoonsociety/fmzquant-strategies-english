
> Name

Golden-Trade-Hour-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]
## Overview
The trading prime time strategy automatically determines which time period of the day is most suitable for buying and selling through historical data backtesting, and sends trading signals at the corresponding time period. This strategy uses the ROC indicator to calculate the rise and fall of the K-line in different periods, and then evaluates the trading effects in different periods to find the best buying and selling periods.
## Strategy Principle
1. Use the existing time to get the current hour now_hour.
2. Use the ROC indicator to calculate the hourly K-line rise and fall indicator.
3. Calculate the cumulative product buy_hourXindicator_cum of indicator and now_hour.
4. Calculate the cumulative sum of indicator buy_indicator_cum.
5. The best buying time is buy_hour = buy_hourXindicator_cum / buy_indicator_cum.
6. Calculate the best selling period sell_hour in the same way.
7. Compare now_hour with buy_hour and sell_hour to determine whether the current period is the best buying or selling period.
8. Send corresponding signals during the best buying and selling periods.
9. Use different background colors to display the best buying and selling periods in real time.
## Advantage Analysis
The biggest advantage of this strategy is that it can automatically determine the most suitable time period for trading every day. There is no need to manually observe historical data to determine the best trading period, saving a lot of time and energy. At the same time, this strategy can adjust the best trading period based on real-time data and respond quickly to market changes. Compared with fixed trading periods, this strategy has more advantages.
In addition, this strategy effectively utilizes the ROC indicator. By calculating the rise and fall of the hourly K-line, the trading effects of different periods can be more accurately judged. The ROC indicator is sensitive to fluctuations in different directions and can reflect market changes.
## Risk Analysis
The biggest risk of this strategy lies in the limitations of the ROC indicator itself. ROC only considers the rate of price change and is insensitive to changes in trading volume. At the same time, ROC is not effective in markets with narrow consolidation ranges. If you encounter a sideways market, the effect of the ROC indicator will be compromised.
In addition, the strategy is used to backtest historical data to find the best trading period. But historical laws may not apply to the current market. Structural changes may occur in the market, and the original trading rules no longer apply. This requires adjusting parameters according to the current market conditions and cannot rely entirely on backtesting results.
In this regard, you can consider combining other indicators for composite calculations, such as trading volume, to obtain a more comprehensive judgment of market status. At the same time, parameter adjustment testing needs to be carried out according to the current market conditions to ensure that the trading signals comply with the new market conditions.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Try to replace the ROC indicator with other indicators, such as trading volume, and find a more suitable indicator to calculate the strength of the period.
2. Add other filtering conditions, use moving averages, oscillators, etc. to determine local trends and avoid unreasonable transactions.
3. Optimize the time period parameters and test the impact of different time period parameters on the results.
4. Add a stop-loss mechanism, set reasonable stop-loss points, and control transaction risks.
5. Combined with machine learning methods, use larger amounts of data to find the optimal trading period.
## Summarize
This trading prime time strategy is overall a viable and effective approach. It uses the ROC indicator to automatically determine the best buying and selling periods every day, saving a lot of time and energy. But we must also pay attention to the limitations of the ROC indicator and historical backtesting, and adjust parameters according to the current market conditions. In addition, this strategy still has a lot of room for improvement and can be optimized from many aspects to make the signal more accurate and reliable. If used for real trading, it is recommended to strictly abide by the stop loss rules and control transaction risks.
|| 

## Overview

The golden trade hour strategy automatically determines the best hours to buy and sell each day by backtesting historical data. It utilizes the ROC indicator to calculate the rise and fall percentage of candlesticks in different hours and thereby evaluate the trading performance to find the optimal buy and sell hours.

## Strategy Principle  

1. Use the current time to get the current hour now_hour.

2. Use the ROC indicator to calculate the hourly rise and fall percentage of candlesticks indicator.

3. Calculate the cumulative product of indicator and now_hour as buy_hourXindicator_cum. 

4. Calculate the cumulative sum of indicator as buy_indicator_cum.

5. The best buy hour buy_hour = buy_hourXindicator_cum / buy_indicator_cum.

6. Similarly calculate the best sell hour sell_hour.  

7. Compare now_hour with buy_hour and sell_hour to determine if the current hour is the optimal buy or sell hour.

8. Send corresponding signals during the optimal buy and sell hours.

9. Use different background colors to display the optimal buy and sell hours in real time.

## Advantage Analysis

The biggest advantage of this strategy is the ability to automatically determine the best trading hours of the day. It saves a lot of time and effort from manually observing historical data to judge the optimal trading hours. Also, the strategy can adjust the optimal trading hours in real time based on live data to respond quickly to market changes. This strategy has more advantages compared to fixed trading hours.

In addition, the strategy makes good use of the ROC indicator. By calculating the hourly rise and fall percentage of candlesticks, it can more accurately judge the trading performance of different periods. The ROC indicator is sensitive to asymmetric fluctuations and can reflect market changes.

## Risk Analysis

The biggest risk of this strategy lies in the limitations of the ROC indicator itself. ROC only considers price changes and is insensitive to changes in trading volume. Also, ROC does not perform well in range-bound markets with narrow bands. If encountering sideways range-bound markets, the effectiveness of the ROC indicator will be discounted.

In addition, the strategy uses backtesting of historical data to determine the optimal trading hours. But historical patterns may not apply to the current market. Structural changes may occur in the market, and original trading rules may no longer apply. This requires adjusting parameters based on current market conditions rather than purely relying on backtesting results.

To address this, we can consider combining other indicators such as trading volume to obtain a more comprehensive judgment of market conditions. Also we need to test parameter adjustments based on current market conditions to ensure trading signals align with new market states.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Try other indicators to replace the ROC indicator, such as trading volume, to find more suitable indicators for calculating hourly strength and weakness.

2. Add other filtering conditions using moving averages, oscillators etc to judge local trends and avoid unreasonable trading. 

3. Optimize the time period parameters and test the impact of different time periods on results.

4. Add stop loss mechanisms and set reasonable stop loss points to control trading risks.

5. Combine machine learning methods and larger data sets to solve the optimal trading hours.

## Summary

In summary, the golden trade hour strategy is a feasible and effective approach. It uses the ROC indicator to automatically determine the optimal intraday buy and sell hours, saving much time and effort. But we should also note the limitations of the ROC indicator and historical backtesting, and adjust parameters based on current market conditions. Furthermore, there is still much room for improvement by optimizing this strategy in many aspects to generate more accurate and reliable signals. If used for live trading, it is recommended to strictly follow stop loss rules to control trading risks.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_string_1|0|timezone: Europe/London|America/Los_Angeles|America/Chicago|America/Phoenix|America/Toronto|America/Vancouver|America/Argentina|America/El_Salvador|America/Sao_Paulo|America/Bogota|Europe/Moscow|Europe/Athens|Europe/Berlin|America/New_York|Europe/Madrid|Europe/Paris|Europe/Warsaw|Australia/Sydney|Australia/Brisbane|Australia/Adelaide|Australia/ACT|Asia/Almaty|Asia/Ashkhabad|Asia/Tokyo|Asia/Taipei|Asia/Singapore|Asia/Shanghai|Asia/Seoul|Asia/Tehran|Asia/Dubai|Asia/Kolkata|Asia/Hong_Kong|Asia/Bangkok|Pacific/Auckland|Pacific/Chatham|Pacific/Fakaofo|Pacific/Honolulu|
|v_input_source_1_close|0|source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|true|ROC Timeperiod|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mablue (Masoud Azizi)

//@version=5
strategy("Trade Hour V3",overlay=false)
timezone = input.string("Europe/London",options=["America/New_York","America/Los_Angeles","America/Chicago","America/Phoenix","America/Toronto","America/Vancouver","America/Argentina" ,"America/El_Salvador","America/Sao_Paulo","America/Bogota","Europe/Moscow","Europe/Athens","Europe/Berlin","Europe/London","Europe/Madrid","Europe/Paris","Europe/Warsaw","Australia/Sydney","Australia/Brisbane","Australia/Adelaide","Australia/ACT","Asia/Almaty","Asia/Ashkhabad","Asia/Tokyo","Asia/Taipei","Asia/Singapore","Asia/Shanghai","Asia/Seoul","Asia/Tehran","Asia/Dubai","Asia/Kolkata","Asia/Hong_Kong","Asia/Bangkok","Pacific/Auckland","Pacific/Chatham","Pacific/Fakaofo","Pacific/Honolulu"]	)
source = input.source(close)
tp = input.int(1,"ROC Timeperiod")

now_hour = hour(time,timezone)

indicator = ta.roc(source,tp)

buy_hourXindicator_cum = ta.cum(indicator* now_hour)
buy_indicator_cum = ta.cum(indicator)
buy_hour = buy_hourXindicator_cum/buy_indicator_cum

sell_hourXindicator_cum = ta.cum( (1/indicator ) * now_hour)
sell_indicator_cum = ta.cum(1/indicator)
sell_hour = sell_hourXindicator_cum/sell_indicator_cum

plot(buy_hour,color=color.green)
plot(sell_hour,color=color.red)
plot(now_hour,color=color.gray,display=display.none)


bool isLongBestHour = now_hour==math.round(buy_hour)
bool isShortBestHour = now_hour==math.round(sell_hour)

bgcolor(isLongBestHour ? color.new(color.green,80) : na)
bgcolor(isShortBestHour ? color.new(color.red,80) : na)
strategy.order("buy", strategy.long, when =isLongBestHour)
strategy.order("sell", strategy.short, when = isShortBestHour)
```

> Detail

https://www.fmz.com/strategy/427263

> Last Modified

2023-09-19 16:03:52
