
> Name

Consecutive-Up-Down-N-Days-Strategy

> Author

ChaoZhang

> Strategy Description

[trans]

This is a long-only, not short-selling strategy, which determines entries and exits based on the number of consecutive rising days and consecutive falling days set by the user. Its trading logic is very simple and straightforward.
Strategy principles
First, we need to set two parameters:
consecutiveBarsUp: number of consecutive rising days
consecutiveBarsDown: Number of consecutive down days
Then we record two variables:
ups: the current number of consecutive days of ups
dns: The current number of consecutive days of decline
Every day, we judge whether the day has risen or fallen based on the comparison between the closing price and the previous day's closing price. If there are rising days, ups will be increased by 1, and if there are falling days, dns will be increased by 1.
When ups reaches consecutiveBarsUp, we go long; when dns reaches consecutiveBarsDown, we close the position.
This completes a simple continuous rise and fall strategy. We only go long when prices continue to rise for a certain number of days after bottoming out, and close after a certain number of days of continuous price decline. Avoid frequent trading in volatile market conditions.
strategic advantage
1. Simple logic, easy to understand and implement
2. By setting the number of consecutive rising and falling days, you can filter some short-term fluctuations and avoid frequent transactions.
3. Only going long can reduce transaction frequency, transaction costs and slippage effects
4. Easy to set stop loss, which can effectively control single loss
Potential risks
1. You cannot go short when it reaches the top, and you may miss the short-selling opportunity.
2. It needs to rise for a certain number of consecutive days before entering the market, and you may miss the lowest buying point.
3. There is a certain time lag and the turning point cannot be captured in real time.
4. If you do not set a stop loss, it may bring greater risk of single loss.
Summarize
The N-day continuous rise and fall strategy is very popular among investors for its simple trading logic and low trading frequency. By setting parameters appropriately, shocks can be effectively filtered and frequent transactions can be avoided. However, there is also a certain time lag and the limitation of short selling. It needs to be implemented after comprehensive consideration by investors. Generally speaking, this strategy is suitable for investors who track medium and long-term trends and can provide stable investment returns.
||
Consecutive Up/Down N Days Strategy 

This article will introduce in detail the trading logic, pros, potential risks and summary of the Consecutive Up/Down N Days strategy.

This is a long-only strategy that determines entries and exits based on user-defined consecutive up days and consecutive down days. The trading logic is very straightforward. 

Strategy Logic

Firstly, we need to set two parameters:

consecutiveBarsUp: consecutive up days
consecutiveBarsDown: consecutive down days

Then we record two variables: 

ups: current consecutive up days
dns: current consecutive down days

Each day we compare the close price with previous close to determine if it's an up day or down day. If up, ups + 1, if down, dns + 1.

When ups reaches consecutiveBarsUp, we go long. When dns reaches consecutiveBarsDown, we exit positions.

That's the simple logic for a consecutive up/down strategy. We only go long after consecutive up days from bottom. And exit after consecutive down days. This avoids frequent trading in range-bound markets.

Pros

1. Simple logic, easy to understand and implement

2. Filtering short-term fluctuations by the consecutive days setting

3. Long only, less trades, lower transaction costs and slippage impact

4. Easy to set stop loss, effectively control single trade loss

Potential Risks 

1. Unable to short tops, missing shorting opportunities 

2. Need consecutive up days to enter, possibly missing best entry point

3. Time lag, not capturing turns in real time

4. Large single trade loss without stop loss

Summary

The consecutive up/down days strategy is widely popular for its simplicity and low frequency trading. With proper parameter tuning, it can filter out whipsaws effectively. But it also has limitations like time lag and inability to short. Investors need to consider carefully before adopting. Overall it suits investors seeking stable returns when tracking medium-long term trends.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|consecutiveBarsUp|
|v_input_2|true|consecutiveBarsDown|
|v_input_3|timestamp(2021-01-01T00:00:00)|startDate|
|v_input_4|timestamp(2021-12-31T00:00:00)|finishDate|
|v_input_5|{{strategy.order.alert_message}}|Buy message|
|v_input_6|{{strategy.order.alert_message}}|Sell message|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-12 00:00:00
end: 2023-09-11 00:00:00
period: 12h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

// Strategy
// strategy("Up/Down Long Strategy", overlay=true, initial_capital = 10000, default_qty_value = 10000, default_qty_type = strategy.cash)

// There will be no short entries, only exits from long.
// strategy.risk.allow_entry_in(strategy.direction.long)

consecutiveBarsUp = input(1)
consecutiveBarsDown = input(1)

price = close

ups = 0.0
ups := price > price[1] ? nz(ups[1]) + 1 : 0

dns = 0.0
dns := price < price[1] ? nz(dns[1]) + 1 : 0

// Strategy Backesting
startDate  = input(timestamp("2021-01-01T00:00:00"), type = input.time)
finishDate = input(timestamp("2021-12-31T00:00:00"), type = input.time)

time_cond  = true

// Messages for buy and sell
message_buy  = input("{{strategy.order.alert_message}}", title="Buy message")
message_sell = input("{{strategy.order.alert_message}}", title="Sell message")

// Strategy Execution

if (ups >= consecutiveBarsUp) and time_cond
    strategy.entry("Long", strategy.long, stop = high + syminfo.mintick, alert_message = message_buy)
    
if (dns >= consecutiveBarsDown) and time_cond
    strategy.entry("Short", strategy.short, stop = low + syminfo.mintick, alert_message = message_sell)

```

> Detail

https://www.fmz.com/strategy/426464

> Last Modified

2023-09-12 11:51:10
