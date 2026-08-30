
> Name

Ichimoku-Cloud-and-MACD-Momentum-RidingIchimoku-Cloud-and-MACD-Momentum-Riding-Strategy

> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ea938d9f7ea2701322e24286ea75b7e11119e4de280533d3c59ac87b01df03f9.png)

[trans]

## Overview
Ichimoku Cloud and MACD Momentum Riding is a trend following strategy that combines the Ichimoku Cloud indicator and the MACD Momentum indicator. This strategy uses the Ichimoku cloud chart to determine the trend direction and support and resistance levels, as well as the MACD indicator to determine momentum reversal, and enter the market at the right time during the trend. At the same time, the strategy uses trailing stop loss to lock in profits and reduce retracement.
## Strategy Principle
### Ichimoku cloud map
The Ichimoku cloud chart consists of the turning line (Tenkan-Sen), the base line (Kijun-Sen), the leading line (Senkou-Span A), the delay line (Senkou-Span B) and the confirmation line (Chikou-Span). This strategy uses the following signals to determine trend direction and support and resistance:
- When the price is above the cloud chart, it is an upward trend.
- The price is below the cloud chart, indicating a downward trend
- When the steering line crosses the baseline, it is a bullish signal
- When the reversal line crosses the baseline, it is a short signal
### MACD indicator
Moving Average Convergence Divergence, or MACD, is a momentum indicator. In this strategy, when the fast line of MACD crosses the slow line, it is a long signal, and when it crosses below, it is a short signal.
### Entry and Exit
When the turning line crosses the baseline, the delay line crosses the closing price of the previous 26 K lines, the closing price breaks through the upper edge of the cloud chart, and MACD is golden cross, enter the market long.
When the price rises by 3%, the strategy will move the stop loss line to 97% of the current price to lock in profits and track the price increase. If the retracement exceeds 3%, stop loss and exit.
When the turning line crosses the baseline, the delay line crosses the closing price of the previous 26 K lines, the closing price falls below the lower edge of the cloud chart, and MACD crosses dead, enter the market short.
When the price drops by 3%, the strategy will move the stop loss line to 103% of the current price to lock in profits and track the price drop. If the rebound exceeds 3%, stop loss and exit.

## Advantage Analysis
This strategy combines trend judgment and entry timing to obtain better returns in trending markets.
1. Ichimoku cloud chart can clearly determine the trend direction. The strategy only enters the market when the direction of the cloud chart is consistent to avoid counter-trend operations.
2. MACD can effectively determine short-term momentum reversal. Combined with cloud chart judgment, the accuracy of entry can be improved.
3. Trailing stop loss allows the strategy to run in the trend for a long time. Strategies can be used in conjunction with fund management to effectively control single transaction risks.

## Risk Analysis
This strategy also has certain risks:
1. Cloud image generation requires a long data cycle, and the judgment may be inaccurate in the short term.
2. As an indicator that fluctuates with price, MACD is prone to generating false signals. The judgment should be revised based on more indicators.
3. Trailing stop loss is only suitable for trending markets, and the stop loss range should be adjusted appropriately. Otherwise, you may stop losses too frequently in volatile market conditions.
4. The strategy itself does not have a risk control module, and users should cooperate with fund management to control losses.

## Optimization direction
Regarding the Ichimoku Cloud and MACD Momentum Riding strategy, it can be optimized from the following directions:
1. Optimize parameters, adjust the period parameters of the steering line, baseline, etc., and optimize the parameters of MACD to make the signal clearer.
2. Add filtering conditions and combine RSI, Bollinger Bands and other indicators to verify the signal and reduce the misjudgment rate.
3. Add dynamic stop loss and dynamically adjust the stop loss range according to the degree of market volatility and risk preference.
4. Combined with fund management, limit the proportion of single losses and effectively control overall losses.
5. Develop the function of automatically selecting contracts and adjusting positions. Expand the adaptability of strategies and apply them in more markets.

## Summarize
The Ichimoku Cloud and MACD Momentum Riding strategy is a quantitative strategy that considers both trend judgment and trading signals. With the cooperation of unfinished parameter optimization and risk control measures, this strategy can achieve better strategic profitability. It is suitable for investors with certain quantitative and programming foundations to use as a trend tracking strategy, and also provides a reference example for quantitative beginners to learn indicator combination and strategy development.

||


## Overview

The Ichimoku Cloud and MACD Momentum Riding is a trend following strategy combining the Ichimoku Cloud indicator and the MACD momentum indicator. The strategy utilizes the Ichimoku Cloud to determine trend direction and support/resistance levels, as well as the MACD indicator to detect momentum reversal, and enters the market timed during a trend. Meanwhile, the strategy adopts a trailing stop loss to lock in profits and reduce drawdowns.

## Strategy Logic  

### Ichimoku Cloud  

The Ichimoku Cloud consists of the Turning Line (Tenkan-Sen), Base Line (Kijun-Sen), Leading Span A (Senkou-Span A), Leading Span B (Senkou-Span B) and Confirmation Line (Chikou-Span). The strategy uses the following signals to determine trend direction and support/resistance:  

- Price above Cloud - Uptrend
- Price below Cloud - Downtrend 
- Turning Line crosses above Base Line - Bullish signal
- Turning Line crosses below Base Line - Bearish signal

### MACD Indicator 

The Moving Average Convergence Divergence, or MACD, is a momentum indicator. In this strategy, when MACD's fast line crosses above slow line it's a buy signal, and when fast line crosses below slow line it's a sell signal.  

### Entries and Exits  

When Turning Line crosses above Base Line, Confirmation Line crosses above close price of 26 bars ago, close price breaks above top band of Cloud, and MACD's fast line has bullish crossover over slow line, go long.   

When price rises 3%, the strategy will move stop loss to 97% of current price to lock in profits and trail the upside move. If drawdown exceeds 3%, stop out with loss.  

When Turning Line crosses below Base Line, Confirmation Line crosses below close price of 26 bars ago, close price breaks below bottom band of Cloud, and MACD's fast line has bearish crossover below slow line, go short.  

When price drops 3%, the strategy will move stop loss to 103% of current price to lock in profits and trail the downside move. If rise exceeds 3%, stop out with loss.


## Advantage Analysis  

This strategy combines trend identification and timing of entry, which can achieve good returns during trending markets.

1. Ichimoku Cloud can clearly identify trend direction. The strategy only enters aligning with Cloud direction, avoiding counter-trend trades.  

2. MACD is effective in detecting short-term momentum reversals. Combining with Cloud it improves entry accuracy.   

3. Trailing stop loss allows the strategy to keep running during a trend. Proper position sizing ensures controlled risk per trade.


## Risk Analysis   

There are also certain risks with this strategy:   

1. Cloud needs relatively long lookback periods and may give inaccurate signals in the short term.  

2. MACD oscillates with price and can generate false signals. More filters are needed to confirm signals.

3. Trailing stop loss only suits trending markets. Stop loss percentage needs to be adjusted accordingly, otherwise whipsaws may stop out too frequently during ranging markets.  

4. The strategy itself does not manage risk. User needs to implement external risk management techniques to control losses.


## Optimization Directions   

The Ichimoku Cloud and MACD Momentum Riding strategy can be optimized in the following ways:  

1. Parameter tuning - Adjust Turning Line, Base Line lookback periods, optimize MACD parameters for clearer signals.  

2. Add filtration - Use other indicators like RSI, Bollinger Bands to filter out bad signals, reducing false signals.

3. Dynamic stops - Base stop loss percentage on market volatility and risk preference.

4. Incorporate position sizing - Limit max loss per trade to control overall drawdown.  

5. Auto selecting contracts & rebalancing - Expand adaptability to more markets.


## Conclusion   

The Ichimoku Cloud and MACD Momentum Riding strategy considers both trend and timing, which can achieve good return when parameters are properly tuned and risk controls are in place. It suits investors with some programming skills as a trend following strategy, and serves as a reference to quant trading beginners for learning technical indicators and strategy development.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_int_1|9|Tenkan-Sen Bars|
|v_input_int_2|26|Kijun-Sen Bars|
|v_input_int_3|52|Senkou-Span B Bars|
|v_input_int_4|26|Chikou-Span Offset|
|v_input_int_5|26|Senkou-Span Offset|
|v_input_2|true|Long Entry|
|v_input_3|true|Short Entry|
|v_input_float_1|3|Trail Long Loss (%)|
|v_input_float_2|3|Trail Short Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-21 00:00:00
end: 2023-11-03 05:20:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('Ichimoku Cloud with MACD and Trailing Stop Loss',
         overlay=true,
         initial_capital=1000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=30,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 6, 1, 0, 0)


// Inputs
ts_bars = input.int(9, minval=1, title='Tenkan-Sen Bars')
ks_bars = input.int(26, minval=1, title='Kijun-Sen Bars')
ssb_bars = input.int(52, minval=1, title='Senkou-Span B Bars')
cs_offset = input.int(26, minval=1, title='Chikou-Span Offset')
ss_offset = input.int(26, minval=1, title='Senkou-Span Offset')
long_entry = input(true, title='Long Entry')
short_entry = input(true, title='Short Entry')

middle(len) => math.avg(ta.lowest(len), ta.highest(len))

// Ichimoku Components
tenkan = middle(ts_bars)
kijun = middle(ks_bars)
senkouA = math.avg(tenkan, kijun)
senkouB = middle(ssb_bars)

// Plot Ichimoku Kinko Hyo
plot(tenkan, color=color.new(#0496ff, 0), title='Tenkan-Sen')
plot(kijun, color=color.new(#991515, 0), title='Kijun-Sen')
plot(close, offset=-cs_offset + 1, color=color.new(#459915, 0), title='Chikou-Span')
sa = plot(senkouA, offset=ss_offset - 1, color=color.new(color.green, 0), title='Senkou-Span A')
sb = plot(senkouB, offset=ss_offset - 1, color=color.new(color.red, 0), title='Senkou-Span B')
fill(sa, sb, color=senkouA > senkouB ? color.green : color.red, title='Cloud color', transp=90)

ss_high = math.max(senkouA[ss_offset - 1], senkouB[ss_offset - 1])
ss_low = math.min(senkouA[ss_offset - 1], senkouB[ss_offset - 1])


// MACD
[macd, macd_signal, macd_histogram] = ta.macd(close, 12, 26, 9)


// Entry/Exit Signals
tk_cross_bull = tenkan > kijun
tk_cross_bear = tenkan < kijun
cs_cross_bull = ta.mom(close, cs_offset - 1) > 0
cs_cross_bear = ta.mom(close, cs_offset - 1) < 0
price_above_kumo = close > ss_high
price_below_kumo = close < ss_low

bullish = tk_cross_bull and cs_cross_bull and price_above_kumo and ta.crossover(macd, macd_signal)
bearish = tk_cross_bear and cs_cross_bear and price_below_kumo and ta.crossunder(macd, macd_signal)

// Configure trail stop level with input options
longTrailPerc = input.float(title='Trail Long Loss (%)', minval=0.0, step=0.1, defval=3) * 0.01
shortTrailPerc = input.float(title='Trail Short Loss (%)', minval=0.0, step=0.1, defval=3) * 0.01

// Determine trail stop loss prices
longStopPrice = 0.0
shortStopPrice = 0.0

longStopPrice := if strategy.position_size > 0
    stopValue = close * (1 - longTrailPerc)
    math.max(stopValue, longStopPrice[1])
else
    0

shortStopPrice := if strategy.position_size < 0
    stopValue = close * (1 + shortTrailPerc)
    math.min(stopValue, shortStopPrice[1])
else
    999999

strategy.entry('Long', strategy.long, when=bullish and long_entry and timePeriod)
strategy.exit('Exit', stop = longStopPrice, limit = shortStopPrice)
//strategy.close('Long', when=bearish and not short_entry)

//strategy.entry('Short', strategy.short, when=bearish and short_entry and timePeriod)
//strategy.close('Short', when=bullish and not long_entry)



```

> Detail

https://www.fmz.com/strategy/432875

> Last Modified

2023-11-22 13:59:36
