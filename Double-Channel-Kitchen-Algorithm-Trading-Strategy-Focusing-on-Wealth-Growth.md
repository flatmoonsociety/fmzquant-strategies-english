
> Name

Double-Channel-Kitchen-Algorithm-Trading-Strategy-Focusing-on-Wealth-Growth
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy "Dual Channel Kitchen" uses two indicators, Supertrend and StochRSI, to analyze price trends and overbought and oversold conditions in different time periods to identify potential buy and sell signals. This strategy aims to trade in the direction of the main trend and capture the main direction of price in the medium to long term.
## Strategy Principle
This strategy uses the Supertrend indicator in two time periods, 1 hour and 4 hours, to determine the direction of the price trend. When the Supertrends of both time periods are in the same direction, we can consider that a strong price trend has emerged.
In addition, the strategy uses the StochRSI indicator to determine whether there are overbought or oversold conditions. The StochRSI indicator combines the advantages of the two indicators RSI and Stochastic Oscillator. When the StochRSI indicator line crosses the overbought line, it indicates that the price may be oversold; when the StochRSI indicator line crosses below the oversold line, it indicates that the price may be overbought.
While the double Supertrend confirms the price trend direction, if the StochRSI also shows overbought and oversold phenomena, then this is a better time to buy or sell. In order to further verify the signal, the strategy also sets a lookback period. After StochRSI displays an overbought and oversold signal, a certain number of K lines need to be looked back. If the price trend confirms the StochRSI signal during this period, then buying or selling will be triggered.
Overall, this strategy comprehensively uses the Supertrend method of dual time frames to determine the general trend, and the StochRSI method to determine local adjustments, and conducts trend following transactions in the medium and long term.
## Strategic Advantages
- Use multi-time period indicators for judgment, which can effectively filter out error signals
- Combine the advantages of Supertrend and StochRSI indicators to make trend judgments and overbought and oversold judgments
- Set a lookback period for signal verification to avoid unnecessary transactions
- Adopting medium and long-term operation strategies can reduce slippage losses caused by too frequent transactions.
- Easy to understand dual indicator combination, flexible parameter adjustment
## Strategy Risk
- During the period of market shock, the mid- to long-term trend is not obvious and there may be many false signals.
- If the lookback period is too long, you may miss better buying/selling opportunities
- Improper setting of StochRSI parameters may result in false overbought and oversold signals.
- Improper setting of Supertrend parameters may determine the wrong trend direction.
- Mechanically follow indicator signals and easily ignore major fundamental changes
Optimization method:
- Optimize the parameter combination of StochRSI and Supertrend
- Adjust the length of the lookback period under different market conditions
- Verify based on indicators such as trading volume
- Pay attention to important fundamental news and proactively intervene when necessary
## Strategy optimization direction
- Add more Supertrend indicators with different time periods to form multi-level filtering
- Replace the StochRSI indicator with other overbought and oversold indicators, such as KD, RSI, etc.
- Add a trailing stop loss strategy to strive for greater profits based on the trend
- Combine with important moving average indicators, such as the 30-period moving average, to determine the general trend
- Develop automatic parameter optimization procedures to make the strategy more robust
## Summarize
The "Double Channel Kitchen" strategy makes full use of Supertrend's method of judging general trends and StochRSI's method of judging local adjustments to achieve a reliable trend tracking strategy. This strategy focuses on medium and long-term operations, which can effectively avoid the loss of income caused by too frequent transactions. Through parameter optimization and combination indicator verification, this strategy can achieve stable positive returns. However, investors still need to pay attention to major fundamental changes and avoid mechanically following indicator signals. Overall, this strategy provides an effective technical analysis method for active investors to obtain positive returns with a certain risk awareness.
||

## Overview 

The "Double Channel Kitchen" strategy uses Supertrend and StochRSI indicators to analyze price trends and overbought/oversold conditions in different timeframes, in order to identify potential buy and sell signals. This strategy aims to trade along the major trend direction and capture the primary price movement over the medium to long term.

## Strategy Logic

The strategy employs the Supertrend indicator in both 1-hour and 4-hour timeframes to determine the price trend direction. When the Supertrends in both timeframes point in the same direction, it signifies a relatively strong price trend.

In addition, the StochRSI indicator is used to detect overbought/oversold conditions. The StochRSI combines the strengths of both the RSI and Stochastic Oscillator indicators. When the StochRSI line crosses above the overbought threshold, it indicates a possible oversold condition in price. When the StochRSI line crosses below the oversold threshold, it flags a potential overbought condition. 

Together with the dual Supertrend confirmation of the price trend, if the StochRSI also shows overbought/oversold signals, it presents a good opportunity to buy or sell. To further verify the signal, a lookback period is implemented where after the StochRSI overbought/oversold signal, the price movement in the past few bars is checked - if it confirms the StochRSI signal, then a buy or sell will be triggered.

In summary, this strategy uses the dual time frame Supertrend to determine the major trend, and StochRSI to identify local reversals, to carry out trend-following trades over the medium to long term.

## Advantages of the Strategy

- Using indicators across multiple timeframes helps to filter out false signals 
- Combines the strengths of Supertrend and StochRSI for trend and overbought/oversold analysis
- Lookback verification avoids unnecessary trades 
- Medium to long term operations avoid excessive trading and slippage
- Easy to understand dual-indicator setup, with flexible parameter tuning

## Risks of the Strategy

- Choppy markets without clear mid-long term trends can generate false signals
- Excessive lookback period may cause missing good entry opportunities 
- Poor StochRSI parameter settings may lead to incorrect overbought/oversold signals
- Improper Supertrend parameters can cause wrong trend direction judgement
- Mechanical signals following overlooks major fundamental changes

Improvements:

- Optimize combinations of StochRSI and Supertrend parameters
- Adjust lookback period based on different market conditions
- Add volume indicators for signal verification
- Monitor key fundamental news events, manual intervention when necessary

## Enhancement Areas

- Add more Supertrend indicators across different timeframes for multi-stage screening 
- Replace StochRSI with other overbought/oversold indicators e.g. KD, RSI
- Incorporate trailing stop loss strategies to ride trends
- Combine key moving averages e.g. 30-period MA to determine major trends
- Develop auto parameter optimization for robustness

## Conclusion

The "Double Channel Kitchen" strategy effectively utilizes the Supertrend for major trend and StochRSI for local reversals, to implement a reliable trend following system. It focuses on medium-long term holdings to avoid excessive trading and slippage. Through parameter optimization, combining indicators, this strategy can achieve steady positive results. However investors should still watch out for major fundamental changes, instead of just mechanically following indicator signals. Overall, this strategy offers an effective technical analysis approach for active investors to generate positive returns with proper risk awareness.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(01 January 2017 13:30 +0000)|(? ################# BACKTEST DATE ################ )Start_Time|
|v_input_2|timestamp(30 April 2024 19:30 +0000)|End_Time|
|v_input_3|10|(? #################  Supertrend  ################ )ATR Length|
|v_input_4|3|Factor|
|v_input_string_1|0|Short Time Period: 07 1h|02 3m|03 5m|04 15m|05 30m|06 45m|01 1m|08 2h|09 3h|10 4h|11 1D|12 1W|
|v_input_string_2|0|Long Time Period: 10 4h|02 3m|03 5m|04 15m|05 30m|06 45m|07 1h|08 2h|09 3h|01 1m|11 1D|12 1W|
|v_input_float_1|15|(? #################  Stoch RSI   ################ )Stoch Rsi Low Limit|
|v_input_float_2|85|Stoch Rsi Up Limit|
|v_input_int_1|20|Stoch Rsi retroactive length|
|v_input_int_2|3|Stochastic RSI K|
|v_input_int_3|14|RSI Length|
|v_input_int_4|14|Stochastic Length|
|v_input_5_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_3|20000|(? #################  Strategy Settings  ################ )Dollar Cost Per Position |
|v_input_string_3|0|Trade_direction: BOTH|SHORT|LONG|
|v_input_6|Long Open|Long Open Message|
|v_input_7|Short Open|Short Open Message|
|v_input_8|Long Close|Long Close Message|
|v_input_9|Short Close|Short Close Message|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-09 00:00:00
end: 2023-10-09 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Baby_whale_to_moon

//@version=5
strategy('Kitchen [ilovealgotrading]', overlay=true, format=format.price, initial_capital = 1000)

// BACKTEST DATE
Start_Time = input(defval=timestamp('01 January 2017 13:30 +0000'), title='Start_Time', group = " ################# BACKTEST DATE ################ " )
End_Time = input(defval=timestamp('30 April 2024 19:30 +0000'), title='End_Time', group = " ################# BACKTEST DATE ################ " )

// supertrend 
atrPeriod = input(10, 'ATR Length', group = " #################  Supertrend  ################ ")
factor = input(3, 'Factor', group = " #################  Supertrend  ################ ")

time1 = input.string(title='Short Time Period', defval='07 1h', options=['01 1m','02 3m','03 5m',  '04 15m', '05 30m', '06 45m', '07 1h', '08 2h', '09 3h', '10 4h', '11 1D', '12 1W' ], group = " #################  Supertrend  ################ ",tooltip = "this timeframe is the value of our short-time supertrend indicator")
time2 = input.string(title='Long Time Period', defval='10 4h', options=[ '01 1m','02 3m','03 5m', '04 15m', '05 30m', '06 45m', '07 1h', '08 2h', '09 3h', '10 4h', '11 1D', '12 1W' ], group = " #################  Supertrend  ################ ",tooltip = "this timeframe is the value of our long-time supertrend indicator")


res(Resolution) =>
    if Resolution == '00 Current'
        timeframe.period
    else
        if Resolution == '01 1m'
            '1'
        else
            if Resolution == '02 3m'
                '3'
            else
                if Resolution == '03 5m'
                    '5'
                else
                    if Resolution == '04 15m'
                        '15'
                    else
                        if Resolution == '05 30m'
                            '30'
                        else
                            if Resolution == '06 45m'
                                '45'
                            else
                                if Resolution == '07 1h'
                                    '60'
                                else
                                    if Resolution == '08 2h'
                                        '120'
                                    else
                                        if Resolution == '09 3h'
                                            '180'
                                        else
                                            if Resolution == '10 4h'
                                                '240'
                                            else
                                                if Resolution == '11 1D'
                                                    '1D'
                                                else
                                                    if Resolution == '12 1W'
                                                        '1W'
                                                    else
                                                        if Resolution == '13 1M'
                                                            '1M'


// supertrend Long time period 
[supertrend2, direction2] = request.security(syminfo.tickerid, res(time2), ta.supertrend(factor, atrPeriod))
bodyMiddle4 = plot((open + close) / 2, display=display.none)
upTrend2 = plot(direction2 < 0 ? supertrend2 : na, 'Up Trend', color=color.new(color.green, 0), style=plot.style_linebr, linewidth=2)
downTrend2 = plot(direction2 < 0 ? na : supertrend2, 'Down Trend', color=color.new(color.red, 0), style=plot.style_linebr, linewidth=2)

// supertrend short time period 
[supertrend1, direction1] = request.security(syminfo.tickerid, res(time1), ta.supertrend(factor, atrPeriod))
bodyMiddle = plot((open + close) / 2, display=display.none)
upTrend = plot(direction1 < 0 ? supertrend1 : na, 'Up Trend', color=color.new(color.yellow, 0), style=plot.style_linebr)
downTrend = plot(direction1 < 0 ? na : supertrend1, 'Down Trend', color=color.new(color.orange, 0), style=plot.style_linebr)


// Stochastic RSI
low_limit_stoch_rsi = input.float(title = 'Stoch Rsi Low Limit', step=0.5, defval=15, group = " #################  Stoch RSI   ################ ", tooltip = "when Stock rsi value crossover Low Limit value we get Long")
up_limit_stoch_rsi = input.float(title = 'Stoch Rsi Up Limit', step=0.5, defval=85, group = " #################  Stoch RSI   ################ ", tooltip = "when Stock rsi value crossunder Up Limit value we get Short")
stocrsi_back_length = input.int(20, 'Stoch Rsi retroactive length', minval=1, group = " #################  Stoch RSI   ################ ", tooltip = "How many candles are left behind, even if there is a buy or sell signal, it will be valid now")
smoothK = input.int(3, 'Stochastic RSI K', minval=1, group = " #################  Stoch RSI   ################ ")
lengthRSI = input.int(14, 'RSI Length', minval=1, group = " #################  Stoch RSI   ################ ")
lengthStoch = input.int(14, 'Stochastic Length', minval=1, group = " #################  Stoch RSI   ################ ")
src_rsi = input(close, title='RSI Source', group = " #################  Stoch RSI   ################ ")
rsi1 = request.security(syminfo.tickerid, '240', ta.rsi(src_rsi, lengthRSI))
k = request.security(syminfo.tickerid, '240', ta.sma(ta.stoch(rsi1, rsi1, rsi1, lengthStoch), smoothK))

// Strategy settings 
dollar = input.float(title='Dollar Cost Per Position ', defval=20000, group = " #################  Strategy Settings  ################ ")
trade_direction = input.string(title='Trade_direction', group = " #################  Strategy Settings  ################ ", options=['LONG', 'SHORT', 'BOTH'], defval='BOTH')
Long_message_open = input('Long Open', title = "Long Open Message", group = " #################  Strategy Settings  ################ ", tooltip = "if you write your alert window this code {{strategy.order.alert_message}} .When trigger Long signal you will get dynamically what you pasted here for Long Open Message ")
Short_message_open = input('Short Open', title = "Short Open Message", group = " #################  Strategy Settings  ################ ", tooltip = "if you write your alert window this code {{strategy.order.alert_message}} .When trigger Long signal you will get dynamically what you pasted here for Short Open Message ")
Long_message_close = input('Long Close', title = "Long Close Message", group = " #################  Strategy Settings  ################ ", tooltip = "if you write your alert window this code {{strategy.order.alert_message}} .When trigger Long signal you will get dynamically what you pasted here for Long Close Message ")
Short_message_close = input('Short Close', title = "Short Close Message", group = " #################  Strategy Settings  ################ ", tooltip = "if you write your alert window this code {{strategy.order.alert_message}} .When trigger Long signal you will get dynamically what you pasted here for Short Close Message ")

Time_interval = true
bgcolor(Time_interval ? color.rgb(255, 235, 59, 95) : na)

back_long = 0
back_short = 0

for i = 1 to stocrsi_back_length by 1
    if ta.crossover(k, low_limit_stoch_rsi)[i] == true 
        back_long += i
        back_long
    if ta.crossunder(k, up_limit_stoch_rsi)[i] == true 
        back_short += i
        back_short

// bgcolor(back_long>0?color.rgb(153, 246, 164, 54):na)
// bgcolor(back_short>0?color.rgb(246, 153, 153, 54):na)

buy_signal = false
sell_signal = false

if direction2 < 0 and direction1 < 0 and back_long > 0
    buy_signal := true
    buy_signal

if direction2 > 0 and direction1 > 0 and back_short > 0
    sell_signal := true
    sell_signal


//bgcolor(buy_signal  ? color.new(color.lime,90) : na ,title="BUY bgcolor")
plotshape( buy_signal[1] == false and  strategy.opentrades == 0 and Time_interval and buy_signal  ? supertrend2 : na, title="Buy", text="Buy", location=location.absolute, style=shape.labelup, size=size.tiny, color=color.green, textcolor=color.white)

//bgcolor(sell_signal  ? color.new(color.red,90) : na ,title="SELL bgcolor")
plotshape(sell_signal[1] == false and strategy.opentrades == 0 and Time_interval and sell_signal  ? supertrend2 : na , title="Sell", text="Sell", location=location.absolute, style=shape.labeldown, size=size.tiny, color=color.red, textcolor=color.white)


// Strategy entries 
if strategy.opentrades == 0 and Time_interval and buy_signal and ( trade_direction == 'LONG' or trade_direction == 'BOTH')
    strategy.entry('Long_Open', strategy.long, qty=dollar / close, alert_message=Long_message_open)

if strategy.opentrades == 0 and Time_interval and sell_signal and ( trade_direction == 'SHORT' or trade_direction == 'BOTH')
    strategy.entry('Short_Open', strategy.short, qty=dollar / close, alert_message=Short_message_open)


// Strategy Close
if close < supertrend1 and strategy.position_size > 0 
    strategy.exit('Long_Close',from_entry = "Long_Open", stop=close, qty_percent=100, alert_message=Long_message_close)

if close > supertrend1 and strategy.position_size < 0 
    strategy.exit('Short_Close',from_entry = "Short_Open", stop=close, qty_percent=100, alert_message=Short_message_close)


```

> Detail

https://www.fmz.com/strategy/428894

> Last Modified

2023-10-10 15:25:53
