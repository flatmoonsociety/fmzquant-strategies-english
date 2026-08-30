
> Name

Cumulative-RSI-Breakout-Strategy Cumulative-RSI-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/106d30b65ba8259770b.png)

[trans]

### Overview
This strategy uses the cumulative RSI indicator to identify trends and perform buy and sell operations when the cumulative value of the RSI indicator breaks through a key threshold. This strategy can effectively filter market noise and lock in longer-term trend trading opportunities.
### Strategy Principles
This strategy mainly makes trading decisions based on the cumulative RSI indicator. The cumulative RSI indicator is the cumulative value of the RSI indicator. By setting the parameter cumlen, the values ​​of the RSI indicator within cumlen days can be accumulated to obtain the cumulative RSI indicator. This indicator can filter out short-term market noise.
When the cumulative RSI indicator crosses the upper band of the bolter band, a buy position operation is performed; when the cumulative RSI indicator crosses the lower band of the bolter band, a sell position operation is performed. Bolinger's upper and lower rails are calculated through years of historical data and are dynamically changing reference prices.
In addition, the strategy also adds a trend filter option. Only when the price is above the 100-day moving average, that is, when it is in an upward trend channel, a buy position will be opened. This filter prevents false trades during price shocks.
### Strategic Advantages
- Use the cumulative RSI indicator to effectively filter noise and lock in the medium and long-term trends
- Add trend filter to avoid unreasonable transactions
- Use breakthrough dynamic reference prices instead of fixed values to make judgments
- There are many configurable parameters, and parameters can be adjusted for different markets
- The 10-year backtest results are excellent, and the income is much higher than the buy and hold strategy
### Strategy risks and improvements
- The strategy only makes decisions based on a single indicator, cumulative RSI, and other judgment indicators or filters can be added for comprehensive judgment.
- The fixed multiple leverage is relatively high, and the leverage ratio can be adjusted according to the retracement situation.
- Only go long direction, consider increasing short selling opportunities
- Parameter combinations can be optimized, and parameter settings will vary greatly under different market conditions.
- Can enrich position closing conditions, add stop loss position, trailing stop loss and other methods
- Can be considered in combination with other strategies to achieve synergistic effects
### Summarize
The overall operation of this cumulative RSI breakthrough strategy is smooth and logical. It effectively filters and increases trend judgment through the cumulative RSI indicator, accurately grasps the medium and long-term trends, and has excellent historical backtesting performance. However, there is still room for optimization, which can be achieved by adjusting parameter settings, adding judgment indicators, and enriching closing conditions to create a more robust and comprehensive trend strategy. This strategy is novel and worthy of further exploration and application.
||

### Overview

This strategy utilizes the Cumulative RSI indicator to identify trends and makes buy and sell decisions when the cumulative RSI value breaks through key threshold levels. It can effectively filter market noise and capture longer-term trend trading opportunities.

### Strategy Logic

The strategy is primarily based on the Cumulative RSI indicator for trading decisions. The Cumulative RSI indicator is the accumulation of RSI values. By setting the cumlen parameter, the RSI values over the past cumlen days are added up to derive the Cumulative RSI indicator. This indicator can filter out short-term market noise.

When the Cumulative RSI indicator crosses above the Bollinger Band upper rail, a long position will be opened. When the Cumulative RSI crosses below the Bollinger Band lower rail, the open position will be closed. The Bollinger Band rails are dynamically calculated based on historical data over many years. 

Additionally, a trend filter option is added. Long trades will only be opened when the price is above the 100-day Moving Average, meaning it is in an upward trend channel. This filter avoids erroneous trades during market fluctuations.

### Advantages

- Effectively filter noise and capture mid-to-long-term trends using Cumulative RSI 
- Avoid unreasonable trades with the trend filter
- Use dynamic reference levels instead of fixed values for decision making
- Highly configurable parameters for adjustments based on different markets
- Outstanding backtest results over 10 years, significantly outperforming buy and hold

### Risks and Improvements

- Decisions based solely on one indicator, can add other indicators or filters
- Fixed high leverage ratio, can adjust based on drawdowns
- Only long trades, can look into shorting opportunities
- Optimize parameters combinations which vary significantly across markets
- Enrich exit conditions with stop loss, moving stop loss etc.
- Consider combining with other strategies for synergistic effects

### Summary

The Cumulative RSI breakout strategy has smooth logic flow and accurately identifies mid-to-long term trends by filtering with Cumulative RSI and adding trend judgment. The backtest results are exceptional over the past decade. There is still room for improvements in areas like parameter tuning, adding indicators, enriching exit conditions to make the strategy more robust. The novel concept is worth further exploration and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|3|RSI Length|
|v_input_1|3|RSI Cumulation Length|
|v_input_2|94|Oversold Level|
|v_input_3|20|Overbought Level|
|v_input_4|false|Only Trade When Price is Above EMA?|
|v_input_5|100|EMA Length|
|v_input_int_2|true|Start Date|
|v_input_int_3|true|Start Month|
|v_input_int_4|2010|Start Year|
|v_input_int_5|true|End Date|
|v_input_int_6|true|End Month|
|v_input_int_7|2099|End Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-26 00:00:00
end: 2023-10-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// @version=5
// Author = TradeAutomation


strategy(title="Cumulative RSI Strategy", shorttitle="CRSI Strategy", process_orders_on_close=true, overlay=true, commission_type=strategy.commission.cash_per_contract, commission_value=.0035, slippage = 1, margin_long = 75, initial_capital = 25000, default_qty_type=strategy.percent_of_equity, default_qty_value=110)


// Cumulative RSI Indicator Calculations //
rlen  = input.int(title="RSI Length", defval=3, minval=1)
cumlen = input(3, "RSI Cumulation Length")
rsi = ta.rsi(close, rlen)
cumRSI = math.sum(rsi, cumlen)
ob = (100*cumlen*input(94, "Oversold Level")*.01)
os = (100*cumlen*input(20, "Overbought Level")*.01)


// Operational Function //
TrendFilterInput = input(false, "Only Trade When Price is Above EMA?")
ema = ta.ema(close, input(100, "EMA Length"))
TrendisLong = (close>ema)
plot(ema)


// Backtest Timeframe Inputs // 
startDate = input.int(title="Start Date", defval=1, minval=1, maxval=31)
startMonth = input.int(title="Start Month", defval=1, minval=1, maxval=12)
startYear = input.int(title="Start Year", defval=2010, minval=1950, maxval=2100)
endDate = input.int(title="End Date", defval=1, minval=1, maxval=31)
endMonth = input.int(title="End Month", defval=1, minval=1, maxval=12)
endYear = input.int(title="End Year", defval=2099, minval=1950, maxval=2100)
InDateRange = (time >= timestamp(syminfo.timezone, startYear, startMonth, startDate, 0, 0)) and (time < timestamp(syminfo.timezone, endYear, endMonth, endDate, 0, 0))


// Buy and Sell Functions //
if (InDateRange and TrendFilterInput==true)
    strategy.entry("Long", strategy.long, when = ta.crossover(cumRSI, os) and TrendisLong, comment="Buy", alert_message="buy")
    strategy.close("Long", when = ta.crossover(cumRSI, ob) , comment="Sell", alert_message="Sell")
if (InDateRange and TrendFilterInput==false)
    strategy.entry("Long", strategy.long, when = ta.crossover(cumRSI, os), comment="Buy", alert_message="buy")
    strategy.close("Long", when = ta.crossover(cumRSI, ob), comment="Sell", alert_message="sell")
if (not InDateRange)
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/430328

> Last Modified

2023-10-27 11:20:50
