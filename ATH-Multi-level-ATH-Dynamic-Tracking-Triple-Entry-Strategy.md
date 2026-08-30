
> Name

Multi-level decline ATH dynamic tracking three-stage buying strategy-Multi-level-ATH-Dynamic-Tracking-Triple-Entry-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9e4720e6542e0c722f.png)

[trans]
#### Overview
This is a multi-level buying strategy based on dynamic tracking of all-time high prices (ATH). The strategy monitors the retracement of the price from ATH, implements batch buying operations at different drop levels, and sells them all to make a profit when the price is close to ATH. This strategy makes full use of market volatility and reduces the overall position cost through systematic batch opening of positions.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. Dynamic ATH tracking: Continuously updates the historical high price and resets the buy mark when it breaks a new high
2. Three-level decline trigger: Set buying points at the 10%, 15% and 20% retracements respectively.
3. Fixed capital management: use the same amount of capital ($1000) for each purchase
4. Retracement closing mechanism: When the price returns to within 5% of ATH, all positions will be closed
Through this progressive position building method, the strategy gradually reduces the average position cost during the decline, and locks in profits by uniformly closing positions when the market rebounds.
#### Strategic Advantages
1. Risk diversification: reducing the risk of time point selection by opening positions in batches
2. Cost optimization: Use larger corrections to reduce average holding costs
3. Trend tracking: Dynamically update ATH to ensure continued operation in an upward trend
4. Fund efficiency: Fixed fund allocation ensures the controllability of fund use
5. Automated execution: clear entry and exit conditions facilitate systematic operation
#### Strategy Risk
1. Trend reversal risk: Continuous lock-in may occur in a long-term downward trend
2. Risk of running out of funds: available funds may be quickly consumed in violently volatile markets
3. Missed opportunity risk: Strict buying conditions may result in missing some good opportunities
4. Risk of position closing timing: Uniform position closing conditions may not be suitable for all market environments
It is recommended to manage these risks by setting maximum drawdown limits and overall position controls.
#### Strategy optimization direction
1. Introduce trend filters: add moving averages or momentum indicators to confirm the overall trend
2. Optimize fund management: dynamically adjust the amount of funds purchased each time based on volatility
3. Improve the position closing mechanism: add batch closing options to avoid the risk of closing positions at a single price
4. Add a stop loss mechanism: set an absolute stop loss level to control the maximum risk
5. Dynamic parameter optimization: automatically adjust buying levels according to different market cycles
#### Summary
This strategy makes good use of market volatility through a systematic batch opening of positions and a unified closing mechanism. The successful operation of the strategy relies on the market having sufficient volatility and an eventual upward trend. Through reasonable risk control and parameter optimization, strategies can maintain stable performance in different market environments.
|| 

#### Overview
This is a multi-level entry strategy based on dynamic All-Time High (ATH) tracking. The strategy monitors price retracements from ATH, implements batch purchases at different decline levels, and sells all positions when the price approaches ATH. It effectively utilizes market volatility through systematic position building to reduce overall holding costs.

#### Strategy Principles
The core logic includes the following key elements:
1. Dynamic ATH Tracking: Continuously updates historical highs and resets buy markers when new highs are broken
2. Three-level Decline Triggers: Sets entry points at 10%, 15%, and 20% retracements
3. Fixed Capital Management: Uses the same amount ($1000) for each purchase
4. Recovery Exit Mechanism: Closes all positions when price recovers to within 5% of ATH
The strategy uses this progressive position building approach to gradually lower average holding costs during declines and locks in profits through unified exits during market rebounds.

#### Strategy Advantages
1. Risk Diversification: Reduces timing risk through batch position building
2. Cost Optimization: Uses larger pullbacks to lower average holding costs
3. Trend Following: Dynamic ATH updates ensure operation in uptrends
4. Capital Efficiency: Fixed capital allocation ensures controllable fund usage
5. Automated Execution: Clear entry/exit conditions facilitate systematic operation

#### Strategy Risks
1. Trend Reversal Risk: May result in consecutive trapped positions in long-term downtrends
2. Capital Depletion Risk: May rapidly consume available funds in volatile markets
3. Missed Opportunity Risk: Strict entry conditions may cause missing good opportunities
4. Exit Timing Risk: Unified exit conditions may not suit all market environments
Recommend managing these risks through maximum drawdown limits and overall position control.

#### Optimization Directions
1. Introduce Trend Filters: Add moving averages or momentum indicators to confirm overall trend
2. Optimize Capital Management: Dynamically adjust entry amounts based on volatility
3. Improve Exit Mechanism: Add partial exit options to avoid single-price exit risks
4. Add Stop-Loss Mechanism: Set absolute stop-loss levels to control maximum risk
5. Dynamic Parameter Optimization: Automatically adjust entry levels based on different market cycles

#### Summary
This strategy effectively utilizes market volatility through systematic batch position building and unified exit mechanisms. Successful strategy operation depends on sufficient market volatility and ultimate upward trends. Through proper risk control and parameter optimization, the strategy can maintain stable performance across different market environments.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-18 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © bsticks22

//@version=6

strategy("Long-term Bean Dip (v.1)", overlay=true)

// === Inputs ===
dip1 = input.float(10.0, "First Dip (%)", step=0.1)       // 10%
dip2 = input.float(15.0, "Second Dip (%)", step=0.1)      // 15%
dip3 = input.float(20.0, "Third Dip (%)", step=0.1)       // 20%
recovery_threshold = input.float(5.0, "Sell when within X% of ATH", step=0.1) // 5%
buy_amount = input.float(50000.0, "Buy Amount ($)", step=100) // $1000 increments

// === Variables ===
var float all_time_high = na
var bool dip1_bought = false
var bool dip2_bought = false
var bool dip3_bought = false

// === Update All-Time High ===
if na(all_time_high)
    all_time_high := high
else
    // Update ATH to the previous bar's high to exclude current bar's high
    all_time_high := math.max(all_time_high[1], high[1])
    if high[1] > all_time_high[1]
        // New ATH reached on the previous bar
        dip1_bought := false
        dip2_bought := false
        dip3_bought := false

// === Calculate Percentage Drop from ATH ===
percent_drop = (all_time_high - close) / all_time_high * 100.0

// === Define Dip Conditions ===
buyDip1 = (percent_drop >= dip1) and not dip1_bought
buyDip2 = (percent_drop >= dip2) and not dip2_bought
buyDip3 = (percent_drop >= dip3) and not dip3_bought

// === Calculate Quantity to Buy ===
qty1 = buy_amount / close

// === Execute Buys on Dips ===
if buyDip1
    strategy.entry("Dip1 Buy", strategy.long, qty=qty1)
    dip1_bought := true

if buyDip2
    strategy.entry("Dip2 Buy", strategy.long, qty=qty1)
    dip2_bought := true

if buyDip3
    strategy.entry("Dip3 Buy", strategy.long, qty=qty1)
    dip3_bought := true

// === Sell Condition: Recovery to Within X% of ATH ===
sell_condition = close >= all_time_high * (1 - recovery_threshold / 100.0)

// === Execute Sell on Recovery ===
if sell_condition and strategy.position_size > 0
    strategy.close_all()

// === Plotting ===
plot(all_time_high, title="All-Time High", color=color.new(color.blue, 0))
plot(all_time_high * (1 - dip1 / 100.0), title="Dip1 Level", color=color.new(color.green, 50), style=plot.style_linebr)
plot(all_time_high * (1 - dip2 / 100.0), title="Dip2 Level", color=color.new(color.orange, 50), style=plot.style_linebr)
plot(all_time_high * (1 - dip3 / 100.0), title="Dip3 Level", color=color.new(color.red, 50), style=plot.style_linebr)
plot(all_time_high * (1 - recovery_threshold / 100.0), title="Recovery Level", color=color.new(color.purple, 50), style=plot.style_linebr)

// === Plot Buy and Sell Signals ===
plotshape(buyDip1, title="Dip1 Buy", location=location.belowbar, color=color.green, style=shape.labelup, text="Buy10%")
plotshape(buyDip2, title="Dip2 Buy", location=location.belowbar, color=color.orange, style=shape.labelup, text="Buy15%")
plotshape(buyDip3, title="Dip3 Buy", location=location.belowbar, color=color.red, style=shape.labelup, text="Buy20%")
plotshape(sell_condition and strategy.position_size > 0, title="Sell", location=location.abovebar, color=color.purple, style=shape.labeldown, text="Sell")

// === Alerts ===
alertcondition(buyDip1, title="Dip1 Buy", message="Price dipped 10% from ATH, buying $1000")
alertcondition(buyDip2, title="Dip2 Buy", message="Price dipped 15% from ATH, buying $1000")
alertcondition(buyDip3, title="Dip3 Buy", message="Price dipped 20% from ATH, buying $1000")
alertcondition(sell_condition and strategy.position_size > 0, title="Sell at Recovery", message="Price recovered to within 5% of ATH, selling all")
```

> Detail

https://www.fmz.com/strategy/475604

> Last Modified

2024-12-20 14:53:04
