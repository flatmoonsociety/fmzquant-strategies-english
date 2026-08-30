
> Name

Follow-The-Bear-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/16ed7571374388d206f.png)
[trans]
## Overview
The Trailing Bear Strategy is a Forex trading strategy designed to capture the typical behavioral pattern of EUR/USD at the opening of European markets. This strategy takes advantage of the fact that euro bulls are trapped during the European market opening and are forced to close their positions to establish short positions. Specifically, after discovering that a reversal pattern candle (shooting star or hammer) appears on the 1-hour K-line of EUR/USD, this strategy will examine indicators such as RSI to filter the signal. Once it is confirmed that the conditions are met, it will decisively go short, with the stop loss level set above the high point of the reversal candle, and the target profit set based on the acceptable risk-return rate.
## Strategy Principle
The core trading logic of the tracking bear market strategy is based on the following assumption: During the opening of the European/London market, traders and algorithms that are long on the euro will push the price of the euro/dollar higher. But if prices then fail to continue rising or show signs of falling, these longs will be trapped. So when the price starts to pull back, they will be forced to close their long orders, thus exacerbating the decline.
This strategy exploits this bear market theory to capture short-term declines. Specifically, it looks for reversal pattern candle signals on the 1-hour K-line in the European time zone (e.g. 2am-7am). The criterion for judging the reversal pattern candle signal here is: the closing price of the body part of the candle is lower than the opening price, and the closing price does not exceed 0.5 times the overall candle fluctuation range (that is, the closing price is close to the candle low).
When such a reversal pattern candle appears, it means that longs are at risk of getting stuck. To further validate the signal, the strategy also checks the following filters:
1. The RSI indicator is above the overbought line (default 70);
2. The closing price of the previous K-line is higher than the opening price (long end signal);
3. When the high point of the K-line reaches a recent new high;
Once all filters are met, the strategy will go short on the close of the reversal candle, with a stop loss order placed above the candle's high, and a target profit based on an acceptable risk-to-reward ratio (the default risk-to-reward ratio is 1 for 1).
It should be noted that this strategy is only active in the European time zone. If the price leaves the European time zone, the status will be reset and wait for the next time zone trading opportunity.
## Advantage Analysis
This is a simple but practical short-term short-selling strategy. The main advantages are:
1. Capture a repeatable short-term behavioral pattern with a higher winning rate;
2. The strategy logic is simple, easy to understand and backtest and optimize;
3. Trade at night to avoid the market noise during the day;
4. Proper risk control and clear stop loss strategy;
5. Can be directly connected to MT4/5 automatic trading;
In general, as a short-term night arbitrage strategy, the tracking bear market strategy is a good choice due to its stability and practicality.
## Risk Analysis
Although this strategy has certain advantages, there are risks in trading any financial product. The main risks include:
1. The liquidity of the night market is poor and it is impossible to stop losses in time;
2. The strategy is too simple and can be easily seen through by the algorithm;
3. The behavioral rules that trap euro bulls may fail in certain market environments;
4. Sufficient historical data is needed to verify the effectiveness of the strategy;
5. The difference between backtest data and actual trading may be huge.
In response to the above risks, the following points are the response methods:
1. Adjust the stop loss range to prevent invalid stop loss;
2. Combine more indicators and filter conditions to make the strategy more robust;
3. Optimize strategy parameters and adapt to the broader market environment;
4. Use a longer backtest period;
5. Multiple real-time verifications to ensure reliable backtest results.
## Optimization direction
Considering the simplicity and potential risks of this strategy, the following are optimization directions that may be considered in the future:
1. **Multiple Time Frame Verification** - Reversal signals can be verified again on the 5-minute or 15-minute time frames to increase stability;
2. **Machine Learning Filtering** - Introduce machine learning algorithms to identify more patterns and filter out false signals;
3. **Dynamic Stop Loss** - According to the degree of market fluctuation, the stop loss point is adjusted in real time to prevent invalid stop loss;
4. **Stable Fund Management Optimization** - Optimize the fund management strategy and make profits more stable by adjusting positions.
## Summarize
The tracking bear market strategy is a simple short-term short-selling strategy with controllable trading risks. It achieves stable profits by capturing the short-term adjustments brought about by the long-term euro situation. This strategy is easy to understand and optimize, making it ideal for night arbitrage trading. Of course, there are risks in trading any financial product, and parameters need to be adjusted and properly optimized to adapt to changes in the market environment.
||

## Overview

The Follow The Bear (FTB) strategy is a forex trading strategy designed to capture a recurring pattern in EUR/USD's price action during the European market open. The strategy aims to take advantage of trapped euro bulls who are forced to unwind their long positions as the price starts retracing. Specifically, it watches for shooting star or hammer reversal candlesticks on the 1-hour chart of EUR/USD. Once detected and confirmed with additional filters like an overbought RSI, it will aggressively enter short positions with a tight stop above the reversal candle and a profit target based on a reasonable risk/reward ratio.

## Strategy Logic

The core premise of the FTB strategy is based on the assumption that euro bulls and algorithms pushing the EUR/USD price up will get trapped when the uptrend stalls or reverses soon after the European/London market open. As the price starts retracing, these trapped longs are forced to unwind their positions, fueling further downside momentum.  

The strategy aims to capitalize on this bearish theory by watching for reversal candlestick patterns during the European timezone (e.g. 2am-7am). The criteria for a reversal candle is that the close must be below the open and within the lower 50% of the candle's range (closer to the low than open).  

When such a candle forms, it signals trapped longs are facing liquidation. To further qualify the signal, additional filters are checked:

1. RSI above 70 overbought level
2. Previous candle closed up 
3. Current candle made new recent high

On passing all filters, the strategy enters short positions on candle close with a stop loss placed just above the high and a profit target calculated based on a 1:1 risk/reward ratio (configurable).  

One key detail is the strategy only trades during the European session. Outside that, it resets and awaits the next trading period.

## Advantage Analysis  

As a simple short-term mean-reversion strategy, the FTB approach has several key strengths:

1. Captures a tradable behavioral pattern with good win rate
2. Easy logic to understand and optimize  
3. Avoids daytime noise by trading overnight
4. Well-defined risk management rules
5. Seamless connectivity to auto-trading

Overall, as a low-frequency night scalping strategy, the stability and reliability of FTB is quite attractive.

## Risk Analysis

While the strategy has merits, as with any trading system, risks exist including:  

1. Wider spreads and gaps overnight  
2. Simplicity could lead to over-optimization
3. Failure of pattern accuracy in certain markets
4. Limited historical data viability 
5. Backtest limitations

Some ways to address the risks:

1. Adjust stop loss buffer
2. Add filters and combine strategies  
3. Optimize for robustness across market conditions  
4. Use longer backtest period
5. Extensive forward testing before live trading

## Optimization Paths

Given the basic nature of the strategy and risks involved, some areas to consider improving:

1. **Multi-timeframe** – confirm signals on 5m or 15m for robustness 
2. **Machine learning** – train model to screen signals  
3. **Dynamic stops** – adjust stops based on volatility  
4. **Risk smoothing** – optimize position sizing for steadier growth

## Conclusion

The Follow the Bear strategy provides a straightforward approach to short-term short selling by capitalizing on retracements fueled by trapped euro bulls. Easy to grasp and enhance, FTB suits systematic overnight scalping. Naturally risks exist in all trading, hence parameter tuning and optimizations help ensure relevance across changing market landscapes.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|(?Risk Settings)Stop Pips|
|v_input_2|true|Risk:Reward|
|v_input_3|0200-0700|(?Filter Settings)Timezone|
|v_input_4|13457|Days To Trade|
|v_input_5|true|RSI OB/OS?|
|v_input_6|false|Previous Bar Must Be Bullish?|
|v_input_7|false|High Filter|
|v_input_8|10|High Lookback|
|v_input_9|0.5|Candle Close %|
|v_input_10|3|RSI Length|
|v_input_11|70|RSI OB|
|v_input_12|YOUR_ID|(?PineConnector Settings)License ID|
|v_input_13|true|Risk Per Trade|
|v_input_14||MetaTrader Prefix|
|v_input_15||MetaTrader Suffix|
|v_input_16|0.5|Spread|
|v_input_17|true|Use Limit Order?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-18 00:00:00
end: 2024-02-25 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ZenAndTheArtOfTrading / PineScriptMastery
// FTB Strategy (PineConnector Version)
// Last Updated: 21st July, 2021
// @version=4
strategy("[2021] FTB Strategy", shorttitle="FTB", overlay=true)

// Risk Settings
var g_risk      = "Risk Settings"
pips            = input(title="Stop Pips", type=input.float, defval=2.0, group=g_risk, tooltip="How many pips above high to put stop loss")
rr              = input(title="Risk:Reward", type=input.float, defval=1.0, group=g_risk, tooltip="This determines the risk:reward profile of the setup")
// Filters
var g_filter    = "Filter Settings"
timezone        = input(title="Timezone", type=input.session, defval="0200-0700", group=g_filter, tooltip="Which timezone to search for FTB signals in")
days            = input(title="Days To Trade", defval="13457", group=g_filter, tooltip="Which days to trade this strategy on (Monday & Friday disabled by default)")
useRsiFilter    = input(title="RSI OB/OS?", type=input.bool, defval=true, group=g_filter, tooltip="If true then the RSI must be considered overbought before a signal is valid")
useCloseFilter  = input(title="Previous Bar Must Be Bullish?", type=input.bool, defval=false, group=g_filter, tooltip="If true then the previous bar must have closed bullish")
useHighFilter   = input(title="High Filter", type=input.bool, defval=false, group=g_filter, tooltip="If true then the signal bar must be the highest bar over X bars")
highLookback    = input(title="High Lookback", type=input.integer, defval=10, group=g_filter, tooltip="This is for setting the High Filter lookback distance")
fib             = input(title="Candle Close %", defval=0.5, group=g_filter, tooltip="For identifying shooting star candles (0.5 = must close <= 50% mark of candle size)")
rsiLen          = input(title="RSI Length", type=input.integer, defval=3, group=g_filter, tooltip="RSI length")
rsiOB           = input(title="RSI OB", type=input.float, defval=70.0, group=g_filter, tooltip="RSI overbought threshold")
// PineConnector Settings
var g_pc        = "PineConnector Settings"
pc_id           = input(title="License ID", defval="YOUR_ID", type=input.string, group=g_pc, tooltip="This is your PineConnector license ID")
pc_risk         = input(title="Risk Per Trade", defval=1, step=0.5, type=input.float, group=g_pc, tooltip="This is how much to risk per trade (% of balance or lots)")
pc_prefix       = input(title="MetaTrader Prefix", defval="", type=input.string, group=g_pc, tooltip="This is your broker's MetaTrader symbol prefix")
pc_suffix       = input(title="MetaTrader Suffix", defval="", type=input.string, group=g_pc, tooltip="This is your broker's MetaTrader symbol suffix")
pc_spread       = input(title="Spread", defval=0.5, type=input.float, group=g_pc, tooltip="Enter your average spread for this pair (used for offsetting limit order)")
pc_limit        = input(title="Use Limit Order?", defval=true, type=input.bool, group=g_pc, tooltip="If true a limit order will be used, if false a market order will be used")

// Generate PineConnector alert string
var symbol = pc_prefix + syminfo.ticker + pc_suffix
var limit = pc_limit ? "limit" : ""
pc_entry_alert(direction, sl, tp) =>
    price = pc_limit ? "price=" + tostring(pc_spread) + "," : ""
    pc_id + "," + direction + limit + "," + symbol + "," + price + "sl=" + tostring(sl) + ",tp=" + tostring(tp) + ",risk=" + tostring(pc_risk)

// Get RSI filter
rsiValue = rsi(close, rsiLen)
rsiFilter = not useRsiFilter or rsiValue >= rsiOB

// Check high & close filter
highFilter = not useHighFilter or high == highest(high, highLookback)
closeFilter = not useCloseFilter or close[1] > open[1]

// InSession() determines if a price bar falls inside the specified session
inSession(sess) => na(time(timeframe.period, sess + ":" + days)) == false

// Calculate 50% mark of candle size
bearFib = (high - low) * fib + low

// Check filters
filters = inSession(timezone) and closeFilter and high > high[1] and rsiFilter and highFilter and open != close

// Detect valid shooting star pinbar pattern
var takenTradeAlready = false
star = true

// Calculate stops & targets
shortStopPrice = high + (syminfo.mintick * pips * 10)
shortStopDistance = shortStopPrice - close
shortTargetPrice = close - (shortStopDistance * rr)

// Save stops & targets for the current trade
var tradeStopPrice = 0.0
var tradeTargetPrice = 0.0

// If we detect a valid shooting star, save our stops & targets, enter short and generate alert
if star and barstate.isconfirmed
    tradeStopPrice := shortStopPrice
    tradeTargetPrice := shortTargetPrice
    takenTradeAlready := true
    alertString = pc_entry_alert("sell", tradeStopPrice, tradeTargetPrice)
    alert(alertString, alert.freq_once_per_bar_close)
    strategy.entry(id="Short", long=strategy.short, when=strategy.position_size == 0, comment=alertString)

// If we have exited the FTB session then reset our takenTradeAlready flag for the next session
if not inSession(timezone) and inSession(timezone)[1]
    takenTradeAlready := false
    
// If price has exceeded target then cancel limit order if it's still active
if pc_limit and low <= tradeTargetPrice and strategy.position_size == 0
    alert(pc_id + ",cancelshort," + symbol)
    tradeTargetPrice := na

// Draw stops & targets
plot(star ? tradeStopPrice : na, color=color.red, style=plot.style_linebr, title="SL")
plot(star ? shortTargetPrice : na, color=color.green, style=plot.style_linebr, title="TP")
// Draw short signals
plotshape(star ? 1 : na, style=shape.triangledown, color=color.red)
// Change background color to highlight detection zone
bgcolor(color=inSession(timezone) ? color.new(color.red,80) : na, title="Session")

// Exit trade whenever our stop or target is hit
strategy.exit(id="Short Exit", from_entry="Short", limit=tradeTargetPrice, stop=tradeStopPrice, when=strategy.position_size != 0)
```

> Detail

https://www.fmz.com/strategy/442836

> Last Modified

2024-02-26 14:12:09
