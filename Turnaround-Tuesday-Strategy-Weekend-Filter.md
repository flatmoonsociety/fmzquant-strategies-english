
> Name

Tuesday Reversal Strategy Weekend Filter-Turnaround-Tuesday-Strategy-Weekend-Filter
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/193efd44d5ffdd0c77c.png)

[trans]
#### Overview
The strategy is called "Tuesday Reversal Strategy (Weekend Filter)". The main idea is to buy at the opening of Monday and sell at the opening of Wednesday based on the moving average and other filtering conditions to capture Tuesday's reversal. This strategy filters out indicators such as RSI and ATR and excludes specific times such as May to improve the strategy's winning rate and return-to-risk ratio.
#### Strategy Principle
1. Use the 30-day moving average as the basis for trend judgment. When the closing price of the previous trading day is lower than the 30-day moving average, the trend is considered downward and one of the buying conditions is met.
2. Use 3-day RSI and 10-day ATR as filter conditions. When the 3-day RSI is less than 51 and the closing price is less than 95% relative to the 10-day ATR, it is considered that the market sentiment is pessimistic, but there is no extreme market, and the buying conditions are met.
3. Excluding May, the stock market is usually weak due to the "Sell in May and go away" effect.
4. Based on the above conditions, buy on Monday when all filter conditions are met, and sell on Wednesday when the market opens.
#### Strategic Advantages
1. Based on the combined judgment of moving averages and sentiment indicators, it can effectively capture Tuesday's reversal market.
2. Through double filtering of RSI and ATR, transactions under extreme market conditions are eliminated, improving the winning rate and return-to-risk ratio of the strategy.
3. Excluding May avoids a time period that usually performs poorly and improves strategy performance.
4. Only buy on Monday and sell on Wednesday, the transaction frequency is low and the handling fee cost is small.
#### Strategy Risk
1. For a market with a strong trend and the reversal is not obvious, the strategy will perform poorly.
2. Fixed trading time may miss better trading opportunities, limiting the flexibility and profit space of the strategy.
3. Relying on indicator judgment, there is a risk of indicator failure when the market undergoes drastic changes.
4. The month judgment is based on historical experience and does not mean that the situation will be the same in the future, and there are timeliness risks.
#### Strategy optimization direction
1. You can consider introducing more effective filtering indicators, such as trading volume, volatility, etc., to improve the robustness and adaptability of the strategy.
2. Optimize the selection of trading opportunities, such as adding intraday breakthrough confirmation and other conditions to improve the flexibility and profit margin of the strategy.
3. For the optimization of the holding period, a longer holding time can be considered to more fully capture the trend.
4. Set different parameters according to different market conditions to improve the adaptability of the strategy.
5. Add position management and risk control modules to cope with extreme market conditions.
#### Summary
Tuesday's reversal strategy (weekend filtering) uses a combination of moving averages, RSI, ATR and other indicators to buy and sell the target at a specific time to capture Tuesday's reversal. The trading frequency of the strategy is low, the handling fee cost is small, and through time period filtering and indicator filtering, the winning rate and risk-return ratio of the strategy are improved. However, the strategy also has certain limitations and risks, such as poor performance in trending markets, fixed buying and selling timing and fixed holding periods. In the future, optimization and improvements can be made by introducing more filtering conditions, optimizing exit timing, dynamically adjusting parameters, position management and risk control, so that the strategy can better adapt to changing market conditions.
|| 

#### Overview
The strategy is named "Turnaround Tuesday Strategy (Weekend Filter)". The main idea is to buy at the Monday open and sell at the Wednesday open when certain conditions based on moving averages and other filters are met, in order to capture the Tuesday turnaround. By filtering with RSI, ATR, and excluding specific times like May, the strategy aims to improve its win rate and risk-reward ratio.

#### Strategy Principles
1. Use the 30-day moving average as a trend determination basis. When the previous trading day's close is below the 30-day MA, it is considered a downtrend and meets one of the buying conditions.
2. Use the 3-day RSI and 10-day ATR as filter conditions. When the 3-day RSI is less than 51 and the close relative to the 10-day ATR is less than 95%, the market sentiment is considered pessimistic but without extreme conditions, meeting the buying conditions.
3. Exclude the month of May due to the "Sell in May and go away" effect, as the stock market tends to be sluggish.
4. Combining the above conditions, buy on Monday when all filter conditions are met, and sell at the Wednesday open.

#### Strategy Advantages
1. The combination of moving average and sentiment indicators can effectively capture the Tuesday turnaround.
2. The dual filtering of RSI and ATR excludes trades in extreme conditions, improving the strategy's win rate and risk-reward ratio.
3. Excluding May avoids trading during typically underperforming periods, enhancing strategy performance.
4. Trading only from Monday to Wednesday results in low trading frequency and small commission costs.

#### Strategy Risks
1. The strategy may underperform when the trend is strong and the reversal is not evident.
2. Fixed buying and selling times may miss better entry and exit points, limiting the strategy's flexibility and profit potential.
3. Relying on indicator judgments risks invalidity when the market changes drastically.
4. Monthly judgments based on historical experience do not guarantee future situations will be the same, posing a timeliness risk.

#### Strategy Optimization Directions
1. Consider introducing more effective filtering indicators, such as volume and volatility, to improve the strategy's robustness and adaptability.
2. Optimize the selection of buying and selling timings, such as adding intraday breakout confirmation conditions, to increase flexibility and profit potential.
3. For holding period optimization, consider longer holding times to more fully capture trends.
4. Set different parameters for different market conditions to enhance the strategy's adaptability.
5. Incorporate position management and risk control modules to cope with extreme market situations.

#### Summary
The Turnaround Tuesday Strategy (Weekend Filter) uses a combination of moving averages, RSI, ATR, and other indicators to buy and sell at specific times, aiming to capture the Tuesday turnaround. The strategy has low trading frequency, small commission costs, and improves its win rate and risk-reward ratio through time period and indicator filtering. However, the strategy also has certain limitations and risks, such as underperformance in trending markets and fixed buying/selling times and holding periods. Future optimizations can introduce more filtering conditions, optimize exit timings, dynamically adjust parameters, manage positions, and control risk to better adapt to changing market conditions.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|Moving Average Period|
|v_input_2|true|Use RSI Filter|
|v_input_3|true|Use ATR Filter|
|v_input_4|true|Exclude May|
|v_input_5|timestamp(2009-01-01 00:00:00)|Start Backtest|
|v_input_6|timestamp(2025-01-01 00:00:00)|End Backtest|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-01 00:00:00
end: 2024-03-31 23:59:59
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © muikol  

//@version=5
strategy("Turnaround Tuesday", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.035)

// Inputs for MA period, filter_1, filter_2, month filter, and testing period
ma_period = input(30, title="Moving Average Period")
use_filter_1 = input(true, title="Use RSI Filter")
use_filter_2 = input(true, title="Use ATR Filter")
use_month_filter = input(true, title="Exclude May")
start_date = input(defval=timestamp("2009-01-01 00:00:00"), title="Start Backtest")
end_date = input(defval=timestamp("2025-01-01 00:00:00"), title="End Backtest")

// Data calculations
MA_tt = ta.sma(close, ma_period)
atr10 = ta.atr(10)
rsi3 = ta.rsi(close, 3)
c_1 = close[1]

// Entry conditions
isMonday = dayofweek == dayofweek.monday
bear = close[1] < MA_tt[1]
filter_1 = use_filter_1 ? rsi3[1] < 51 : true
filter_2 = use_filter_2 ? c_1/atr10[1] < 95 : true
notMay = use_month_filter ? month != 5 : true
entryCondition = isMonday and bear and notMay and filter_1 and filter_2

// Date check
inTestPeriod = true
// Exit conditions
isWednesdayOpen = dayofweek == dayofweek.wednesday 

// Entry and exit triggers
if entryCondition and inTestPeriod
    strategy.entry("Buy", strategy.long)

if isWednesdayOpen and strategy.position_size > 0 and inTestPeriod
    strategy.close("Buy")

// Plot the moving average
plot(MA_tt, title="Moving Average", color=color.blue)

```

> Detail

https://www.fmz.com/strategy/449948

> Last Modified

2024-04-30 16:07:45
