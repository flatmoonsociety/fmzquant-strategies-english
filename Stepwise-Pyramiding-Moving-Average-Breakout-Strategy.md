
> Name

Stepwise-Pyramiding-Moving-Average-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13a4855ee824fbc5bca.png)
[trans]
### Overview
This strategy adopts the method of gradually increasing positions, and determines the market direction based on the comparison between the closing price and the previous day's closing price. When it is judged to be a bullish opportunity, the position will be gradually added to the long position in multiple times; when it is judged to be a bearish opportunity, the position will be gradually added to the short position in multiple times. The number of positions added can be set through parameters. At the same time, the strategy has added time period filtering, and trading signals will only be issued within the set time period.
### Strategy Principles
1. Compare the current K-line closing price close with the previous K-line closing price close[1]. If close > close[1], it is judged as a bullish opportunity and set longCondition=1; if close < close[1], it is judged as a bearish opportunity and set shortCondition=1.
2. Within the time period where trading is allowed, if longCondition=1, the position will be gradually increased to long positions; if shortCondition=1, the position will be gradually increased to short positions.
3. The number of positions added is set by the parameter pyramiding. You can choose to add positions 1 to 5 times. The default is 4 times.
4. Each time you add a position, hedging conditions will be set at the same time. If the market turns around, the loss will be stopped immediately.
5. You can choose to output trading signals to different trading interfaces, such as toast, telegram, etc.
This strategy mainly considers the advantages of breakthrough strategies and moving average strategies. When bullish or bearish, it adopts the method of gradually increasing positions, which can fully track the trend and control risks. At the same time, it is combined with time filtering to avoid GENERATED signals during non-main trading hours.
### Advantage Analysis
1. Gradually increasing positions can better track the trend
2. The number of positions added is adjustable and more flexible
3. You can choose different transaction interfaces and expand the quantity type
4. There is a stop-loss mechanism to control risks
5. Time filtering function to avoid false signals
### Risk Analysis
1. Improper parameter settings may lead to increased losses
2. Network problems may prevent losses from being stopped in time
3. Parameters need to be adjusted appropriately to adapt to different varieties
4. Stop losses at the right time to lock in profits
Solution:
1. Adjust the number of times to add positions, the default is 4 times.
2. Check network connection
3. Adjust parameters according to variety characteristics
4. Set stop loss level
### Optimization direction
1. You can consider adding more indicators to judge the strength of the signal.
2. Can test the optimization effect of different varieties of parameters
3. Machine learning algorithms can be added to optimize parameters
4. Can optimize risk management mechanism
### Summarize
The moving average breakthrough strategy of gradually adding positions integrates the advantages of trend tracking and risk control. When a valid signal is judged, the trend is tracked by gradually adding positions, and the risk exposure is controlled by adjusting the number of positions added. At the same time, it combines functions such as time period filtering to control false signals. This strategy can be optimized in a variety of ways and has great scalability. In general, this strategy has a very good effect on tracking trend varieties and is a recommended strategy.
||

### Overview  

This strategy uses a stepwise pyramiding approach based on the comparison between the current close price and previous close price to determine the market direction. When a long opportunity is identified, it will long with multiple gradual entries. When a short opportunity is identified, it will short with multiple gradual entries. The number of entries can be set through parameters. At the same time, the strategy incorporates time frame filters where trading signals are only generated within the configured trading time frame.

### Strategy Logic   

1. Compare current bar's close price (close) with previous bar's close price (close[1]). If close > close[1], it is determined as a long opportunity and set longCondition=1. If close < close[1], it is determined as a short opportunity and set shortCondition=1.

2. Within the allowed trading time frame, if longCondition=1, it will long with multiple gradual entries. If shortCondition=1, it will short with multiple gradual entries.

3. The number of entries is set through the pyramiding parameter, which can be configured from 1 to 5, with 4 as the default.  

4. A stop loss condition is set after each entry in case the market reverses. 

5. Trading signals can be output to different trading interfaces such as toast or telegram.

The strategy mainly considers the advantages of breakout and moving average strategies. During long or short opportunities, it uses a stepwise pyramiding approach to better follow the trend while controlling risks. It also incorporates time frame filters to avoid generating signals during non-major trading sessions.

### Advantage Analysis

1. Stepwise pyramiding follows trends better.  

2. Adjustable number of entries makes it more flexible.

3. Supports different trading interfaces for scalability.  

4. Has stop loss mechanisms to control risks.

5. Time frame filter avoids false signals.

### Risk Analysis

1. Improper parameter settings may lead to larger losses.  

2. Network issues may prevent timely stop loss.  

3. Parameters need adjustments for different products.

4. Need timely stop loss to lock in profits.

Solutions:

1. Default 4 entries is appropriate.  

2. Check network connectivity.

3. Adjust parameters according to product characteristics.  

4. Set stop loss levels.

### Optimization Directions   

1. Consider adding more indicators to judge signal strength.

2. Test parameter optimization results across different products.  

3. Incorporate machine learning algorithms to optimize parameters.  

4. Enhance risk management mechanisms.

### Summary
This stepwise pyramiding moving average breakout strategy integrates the advantages of trend following and risk control. When effective signals are identified, it uses stepwise pyramiding to follow the trend while controlling risk exposure through configurable number of entries. It also incorporates functionalities like time frame filter to avoid false signals. The strategy can be further optimized in many aspects and has great extensibility. In general, it is very effective for trending products and is strongly recommended.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(31 Jan 2024 00:00 +0900)|(?매매 시간세팅)매매 시작|
|v_input_2|timestamp(31 Dec 2030 00:00 +0900)|매매 종료|
|v_input_string_1|0|(?봇선택)봇선택: POA|TVEXTBOT|
|v_input_string_2|아무거나입력|(?계정정보)계정|
|v_input_string_3||TVExtBot 인증키|
|v_input_float_1|4|(?진입 세팅)분할진입수|
|v_input_string_4||(?진입주문 메세지입력)롱 진입1|
|v_input_string_5||롱 진입2|
|v_input_string_6||롱 진입3|
|v_input_string_7||롱 진입4|
|v_input_string_8||롱 진입5|
|v_input_string_9||숏 진입1|
|v_input_string_10||숏 진입2|
|v_input_string_11||숏 진입3|
|v_input_string_12||숏 진입4|
|v_input_string_13||숏 진입5|
|v_input_string_14||(?종료주문 메세지입력)롱 전체종료|
|v_input_string_15||숏 전체종료|

> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-05 00:00:00
end: 2024-02-04 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © torresbitmex

//@version=5
strategy("torres_strategy_real_test_v1.0", process_orders_on_close=true, overlay=true, initial_capital=1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_value=0.03, calc_on_order_fills=false, pyramiding=4)

in_trade(int start_time, int end_time) =>    
    allowedToTrade = (time>=start_time) and (time<=end_time)
    if barstate.islastconfirmedhistory
        var myLine = line(na)
        line.delete(myLine)
        myLine := line.new(start_time, low, start_time, high, xloc=xloc.bar_time, color = color.rgb(255, 153, 0, 50), width = 3, extend = extend.both, style = line.style_dashed)
    allowedToTrade

// 매매시간세팅
start_time = input(timestamp("31 Jan 2024 00:00 +0900"), title="매매 시작", group='매매 시간세팅')
end_time = input(timestamp("31 Dec 2030 00:00 +0900"), title="매매 종료", group='매매 시간세팅')
start_trade = true
bgcolor(start_trade ? color.new(color.gray, 90)   : color(na))


var bool Alarm_TVExtbot = false
var bool Alarm_Alert = false

bot_mode = input.string(title='봇선택', defval = "POA", options = ["TVEXTBOT", "POA"], group = "봇선택", inline = '1')
if bot_mode == "TVEXTBOT"
    Alarm_TVExtbot := true
else if bot_mode == "POA"
    Alarm_Alert := true
else
    Alarm_TVExtbot := false
    Alarm_Alert := false

// 계정정보
account = input.string(title='계정', defval='아무거나입력', inline='1', group='계정정보')
token = input.string(title='TVExtBot 인증키', defval='', inline='1', group='계정정보')

mul_input = input.float(4, minval=1, maxval=5, step=1, title="분할진입수", group='진입 세팅', inline='1')
// 진입주문메세지입력
buyOrderid = input.string(title='롱 진입1', defval='', group='진입주문 메세지입력', inline='2')
buyOrderid2 = input.string(title='롱 진입2', defval='', group='진입주문 메세지입력', inline='3')
buyOrderid3 = input.string(title='롱 진입3', defval='', group='진입주문 메세지입력', inline='4')
buyOrderid4 = input.string(title='롱 진입4', defval='', group='진입주문 메세지입력', inline='5')
buyOrderid5 = input.string(title='롱 진입5', defval='', group='진입주문 메세지입력', inline='6')
sellOrderid = input.string(title='숏 진입1', defval='', group='진입주문 메세지입력', inline='2')
sellOrderid2 = input.string(title='숏 진입2', defval='', group='진입주문 메세지입력', inline='3')
sellOrderid3 = input.string(title='숏 진입3', defval='', group='진입주문 메세지입력', inline='4')
sellOrderid4 = input.string(title='숏 진입4', defval='', group='진입주문 메세지입력', inline='5')
sellOrderid5 = input.string(title='숏 진입5', defval='', group='진입주문 메세지입력', inline='6')

// 종료주문메세지입력
buycloseOrderid = input.string(title='롱 전체종료', defval='', group='종료주문 메세지입력', inline='1')
sellcloseOrderid = input.string(title='숏 전체종료', defval='', group='종료주문 메세지입력', inline='1')

longCondition = 0, shortCondition = 0

if(close[1] < close)
    longCondition := 1
else
    longCondition := 0
if(close[1] > close)
    shortCondition := 1
else
    shortCondition := 0

if start_trade
    if Alarm_Alert
        if strategy.position_size == 0
            if (longCondition == 1)
                strategy.entry("buy1", strategy.long, alert_message = buyOrderid)

            if (shortCondition == 1)
                strategy.entry("sell1", strategy.short, alert_message = sellOrderid)

        if strategy.position_size > 0
            if (longCondition == 1)
                if (strategy.opentrades == 1) and (mul_input == 2 or mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("buy2", strategy.long, alert_message = buyOrderid2)  
                if (strategy.opentrades == 2) and (mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("buy3", strategy.long, alert_message = buyOrderid3)  
                if (strategy.opentrades == 3) and (mul_input == 4 or mul_input == 5)
                    strategy.entry("buy4", strategy.long, alert_message = buyOrderid4)  
                if (strategy.opentrades == 4) and (mul_input == 5)
                    strategy.entry("buy5", strategy.long, alert_message = buyOrderid5)  

        if strategy.position_size < 0
            if (shortCondition == 1)
                if (strategy.opentrades == 1) and (mul_input == 2 or mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("sell2", strategy.short, alert_message = sellOrderid2)  
                if (strategy.opentrades == 2) and (mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("sell3", strategy.short, alert_message = sellOrderid3)  
                if (strategy.opentrades == 3) and (mul_input == 4 or mul_input == 5)
                    strategy.entry("sell4", strategy.short, alert_message = sellOrderid4)
                if (strategy.opentrades == 4) and (mul_input == 5)
                    strategy.entry("sell5", strategy.short, alert_message = sellOrderid5)

        if (longCondition == 1 and strategy.position_size > 0)
            if mul_input == 1 and strategy.opentrades == 1
                strategy.close_all(comment='롱전체종료', alert_message = buycloseOrderid)
            if mul_input == 2 and strategy.opentrades == 2
                strategy.close_all(comment='롱전체종료', alert_message = buycloseOrderid)
            if mul_input == 3 and strategy.opentrades == 3
                strategy.close_all(comment='롱전체종료', alert_message = buycloseOrderid)
            if mul_input == 4 and strategy.opentrades == 4
                strategy.close_all(comment='롱전체종료', alert_message = buycloseOrderid)
            if mul_input == 5 and strategy.opentrades == 5
                strategy.close_all(comment='롱전체종료', alert_message = buycloseOrderid)
        if (shortCondition == 1 and strategy.position_size < 0)
            if mul_input == 1 and strategy.opentrades == 1
                strategy.close_all(comment='숏전체종료', alert_message = sellcloseOrderid)
            if mul_input == 2 and strategy.opentrades == 2
                strategy.close_all(comment='숏전체종료', alert_message = sellcloseOrderid)
            if mul_input == 3 and strategy.opentrades == 3
                strategy.close_all(comment='숏전체종료', alert_message = sellcloseOrderid)
            if mul_input == 4 and strategy.opentrades == 4
                strategy.close_all(comment='숏전체종료', alert_message = sellcloseOrderid)
            if mul_input == 5 and strategy.opentrades == 5
                strategy.close_all(comment='숏전체종료', alert_message = sellcloseOrderid)
    else if Alarm_TVExtbot
        if strategy.position_size == 0
            if (longCondition == 1)
                strategy.entry("buy1", strategy.long, alert_message = '롱 1차 진입 ?? TVM:{"orderid":"' + buyOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')

            if (shortCondition == 1)
                strategy.entry("sell1", strategy.short, alert_message = '숏 1차 진입 ?? TVM:{"orderid":"' + sellOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')

        if strategy.position_size > 0
            if (longCondition == 1)
                if (strategy.opentrades == 1) and (mul_input == 2 or mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("buy2", strategy.long, alert_message = '롱 2차 진입 ?? TVM:{"orderid":"' + buyOrderid2 + '","memo":"' + account + '","token":"' + token + '"}:MVT')  
                if (strategy.opentrades == 2) and (mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("buy3", strategy.long, alert_message = '롱 3차 진입 ?? TVM:{"orderid":"' + buyOrderid3 + '","memo":"' + account + '","token":"' + token + '"}:MVT')  
                if (strategy.opentrades == 3) and (mul_input == 4 or mul_input == 5)
                    strategy.entry("buy4", strategy.long, alert_message = '롱 4차 진입 ?? TVM:{"orderid":"' + buyOrderid4 + '","memo":"' + account + '","token":"' + token + '"}:MVT')  
                if (strategy.opentrades == 4) and (mul_input == 5)
                    strategy.entry("buy5", strategy.long, alert_message = '롱 5차 진입 ?? TVM:{"orderid":"' + buyOrderid5 + '","memo":"' + account + '","token":"' + token + '"}:MVT') 

        if strategy.position_size < 0
            if (shortCondition == 1)
                if (strategy.opentrades == 1) and (mul_input == 2 or mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("sell2", strategy.short, alert_message = '숏 2차 진입 ?? TVM:{"orderid":"' + sellOrderid2 + '","memo":"' + account + '","token":"' + token + '"}:MVT')  
                if (strategy.opentrades == 2) and (mul_input == 3 or mul_input == 4 or mul_input == 5)
                    strategy.entry("sell3", strategy.short, alert_message = '숏 3차 진입 ?? TVM:{"orderid":"' + sellOrderid3 + '","memo":"' + account + '","token":"' + token + '"}:MVT')  
                if (strategy.opentrades == 3) and (mul_input == 4 or mul_input == 5)
                    strategy.entry("sell4", strategy.short, alert_message = '숏 4차 진입 ?? TVM:{"orderid":"' + sellOrderid4 + '","memo":"' + account + '","token":"' + token + '"}:MVT')
                if (strategy.opentrades == 4) and (mul_input == 5)
                    strategy.entry("sell5", strategy.short, alert_message = '숏 5차 진입 ?? TVM:{"orderid":"' + sellOrderid5 + '","memo":"' + account + '","token":"' + token + '"}:MVT')
        
        if (longCondition == 1 and strategy.position_size > 0)
            if mul_input == 1 and strategy.opentrades == 1
                strategy.close_all(comment='롱전체종료', alert_message = '롱 종료 ?⛔TVM:{"orderid":"' + buycloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 2 and strategy.opentrades == 2
                strategy.close_all(comment='롱전체종료', alert_message = '롱 종료 ?⛔TVM:{"orderid":"' + buycloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 3 and strategy.opentrades == 3
                strategy.close_all(comment='롱전체종료', alert_message = '롱 종료 ?⛔TVM:{"orderid":"' + buycloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 4 and strategy.opentrades == 4
                strategy.close_all(comment='롱전체종료', alert_message = '롱 종료 ?⛔TVM:{"orderid":"' + buycloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 5 and strategy.opentrades == 5
                strategy.close_all(comment='롱전체종료', alert_message = '롱 종료 ?⛔TVM:{"orderid":"' + buycloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')            
        if (shortCondition == 1 and strategy.position_size < 0)
            if mul_input == 1 and strategy.opentrades == 1
                strategy.close_all(comment='숏전체종료', alert_message = '숏 종료 ?⛔TVM:{"orderid":"' + sellcloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 2 and strategy.opentrades == 2
                strategy.close_all(comment='숏전체종료', alert_message = '숏 종료 ?⛔TVM:{"orderid":"' + sellcloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 3 and strategy.opentrades == 3
                strategy.close_all(comment='숏전체종료', alert_message = '숏 종료 ?⛔TVM:{"orderid":"' + sellcloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 4 and strategy.opentrades == 4
                strategy.close_all(comment='숏전체종료', alert_message = '숏 종료 ?⛔TVM:{"orderid":"' + sellcloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')
            if mul_input == 5 and strategy.opentrades == 5
                strategy.close_all(comment='숏전체종료', alert_message = '숏 종료 ?⛔TVM:{"orderid":"' + sellcloseOrderid + '","memo":"' + account + '","token":"' + token + '"}:MVT')

  
```

> Detail

https://www.fmz.com/strategy/441079

> Last Modified

2024-02-05 14:09:14
