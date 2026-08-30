
> Name

Mean-Reversion-Envelope-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/c13eab218a43bc24d0834252d8c0d58666a3bbbe06825423f26345c38fa7d711.png)
[trans]

## Overview
The intention reversal envelope mean strategy is an intention reversal trading strategy based on moving averages. This strategy uses the double exponential moving average as the basic calculation, and adds multiple envelope bands above and below it. When the price touches the envelope band, open a long or short position depending on the direction. When the price returns to the moving average, close the position and exit.
## Strategy Principle
This strategy uses the Double Exponential Moving Average (DEMA) as the underlying indicator. The double exponential moving average is a moving average that is highly sensitive to price changes. On its basis, the strategy adds multiple price bands on the upper and lower sides respectively to form a moving average envelope area. The range of the envelope zone is set by the user, and each price band is separated by a certain percentage.
When the price rises and approaches the upper envelope band, this strategy will open a short position; when the price falls and touches the lower envelope band, this strategy will open a long position. Each time a new price band is touched, the position will be added. When the price returns near the moving average, the strategy will close all positions.
This strategy captures excessive price fluctuations through the envelope zone and exits with profits when the reversal comes, achieving the trading goal of buying low and selling high. It is suitable for market cycles with obvious mean reversion characteristics, such as digital currencies such as Bitcoin.

## Strategic Advantages
- Use double exponential moving averages, which are more sensitive to short-term price changes and can quickly capture trend turning points.
- An envelope zone is established near the moving average to capture price reversals more accurately.
- Open and add positions in batches to make full use of capital efficiency.
- Quickly switch directions after making profits and respond flexibly to market changes.
- Can be freely optimized by adjusting parameters.
## Strategy Risk
- It is impossible to profitably switch directions in a large market.
- Improper parameter settings may lead to too frequent transactions.
- Requires relatively stable market conditions and is not suitable for sharply volatile markets.
- If the envelope area is too small, it may be impossible to open a position.
Risks can be reduced by appropriately relaxing the scope of the envelope zone and increasing the sensitivity of triggering price changes. At the same time, adjust the moving average length parameters to adapt to different market cycles.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the moving average algorithm. You can test the effects of different types of moving average indicators.
2. Adjust the moving average length parameter. Shortening the period can improve the capture of short-term price changes, but it may also increase noise trading.
3. Optimize envelope zone parameters. Different percentage settings can be tested to find the optimal parameter combination.
4. Add a stop loss strategy. Setting a trailing stop or a retracement stop can effectively control a single loss.
5. Add filter conditions. Combine with other indicator signals to avoid invalid opening of positions under irrational market conditions.

## Summarize
The intention reversal envelope mean strategy effectively captures price reversal opportunities by constructing a moving average price channel. It can flexibly adjust parameters and is suitable for different market environments. This strategy has lower transaction cost and higher return rate. It is a recommended quantitative trading strategy.
||

## Overview

The Mean Reversion Envelope Moving Average Strategy is a mean reversion trading strategy based on moving averages. It uses Double Exponential Moving Average (DEMA) as the base calculation and adds several envelopes above and below it. When the price touches the envelope bands, it opens long or short positions based on the direction. When the price regresses to the moving average, it closes all positions.

## Strategy Logic

The strategy uses Double Exponential Moving Average (DEMA) as the base indicator, which is a moving average that is more sensitive to recent price changes. Above and below the DEMA, several price bands are added to form an envelope zone. The range of the envelope is set by the user, with a fixed percentage interval between each band.

When the price rises and approaches the upper envelope band, the strategy opens a short position. When the price falls and hits the lower envelope band, it opens a long position. It adds a new position each time when a new price band is touched. When the price regresses close to the moving average, all positions are closed.  

Through capturing excessive price fluctuations with the envelope bands and profiting from reversals, the strategy aims to buy low and sell high. It fits market cycles with obvious mean reversion tendencies, such as cryptocurrencies like Bitcoin.

## Advantages

- Uses Double Exponential Moving Average, which is sensitive to short-term price changes for catching trend reversals.
- The envelope bands around moving average can accurately capture price reversals. 
- Opens positions in batches, fully utilizing capital efficiency.
- Quickly switch directions after profiting to adapt to market changes.
- Parameters can be freely optimized.

## Risks

- Unable to profit from strongly trending markets.
- Improper parameters may cause over-trading.
- Needs relatively stable markets, not suitable for highly volatile environments. 
- Too narrow envelopes may prevent entering positions.

The risks can be reduced by appropriately expanding the envelope range to increase sensitivity and adjusting the moving average length to fit different market cycles.

## Optimization Directions 

The strategy can be optimized in the following aspects:

1. Test different moving average algorithms.

2. Adjust the moving average length parameter for better adapting to short-term fluctuations.

3. Optimize the envelope parameters by testing different percentage settings.

4. Add stop loss methods like trailing stop loss to limit single trade loss.

5. Add filtering conditions with other indicators to avoid invalid entries in irrational markets.


## Conclusion

The Mean Reversion Envelope Moving Average Strategy effectively captures mean reversion opportunities by building a price channel around the moving average. It can be flexibly adapted to different market environments through parameter adjustments. With relatively low transaction costs and high returns, this is a recommended quantitative trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|(?Moving Average)Moving Average Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|5|Moving Average Window|
|v_input_string_1|0|Moving Average Type: 4. DEMA|2. EMA|3. RMA|1. SMA|
|v_input_float_1|0.05|(?Envelope)Delta Per Enveloppe|
|v_input_int_2|0|Envelope count: 5|2|3|4|1|
|v_input_bool_1|true|(?Orders)Use Long Orders ?|
|v_input_bool_2|false|Use Short Orders ?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-27 00:00:00
end: 2023-12-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Mean Reversion - Envelope Strategy", overlay=true )

// ----------------------- DESCRIPTION -----------------------
// THIS SCRIPT IS A MEAN REVERSION SYSTEM THAT USES A MOVING AVERAGE AS BASE CALCULATION AND A % OF THIS MOVING AVERAGE TO CALCULATE THE ENVELOPE
// BY DEFAULT, THE SYSTEM WILL PLACE LONG ORDERS ON THE MOVING AVERAGE -5% PER ENVELOPE COUNT (5%, 10% AND SO ON...)
// YOU CAN ENABLE THE SHORT ORDERS THAT WILL FOLLOW THE SAME LOGIC ON THE OPPOSITE SIDE
// THE SYSTEM WILL CLOSE EVERY ONGOING TRADE WHEN THE PRICE RETURNS TO THE MEAN

// ---------------------------------------------
// ---------------- SETTINGS -------------------
src = input(close, "Moving Average Source", group = "Moving Average")
ma_window = input.int(5, "Moving Average Window", step = 1, group = "Moving Average")
ma_type = input.string('4. DEMA', "Moving Average Type", options=['1. SMA', '2. EMA', '3. RMA', '4. DEMA'], group = "Moving Average")
enveloppe_step = input.float(0.05, "Delta Per Enveloppe", step = 0.01, group = "Envelope")
envelope_count = input.int(5, "Envelope count", options = [1, 2, 3, 4, 5], group = "Envelope")
use_longs = input.bool(true, 'Use Long Orders ?', group = "Orders") 
use_short = input.bool(false, 'Use Short Orders ?', group = "Orders")


// ---------------------------------------------
// -------------- INDICATORS -------------------
ma_funct() =>
    if(ma_type == '1. SMA') 
        ta.sma(src, ma_window)
    if(ma_type == '2. EMA') 
        ta.ema(src, ma_window)
    if(ma_type == '3. RMA') 
        ta.rma(src, ma_window)
    if(ma_type == '4. DEMA') 
        2 * ta.ema(src, ma_window) - ta.ema(ta.ema(src, ma_window), ma_window)

ma_base = ma_funct()

ma_high_1 = envelope_count > 0 ? ma_base * (1 + enveloppe_step) : na
ma_high_2 = envelope_count > 1 ? ma_base * (1 + enveloppe_step * 2) : na
ma_high_3 = envelope_count > 2 ? ma_base * (1 + enveloppe_step * 3) : na
ma_high_4 = envelope_count > 3 ? ma_base * (1 + enveloppe_step * 4) : na
ma_high_5 = envelope_count > 4 ? ma_base * (1 + enveloppe_step * 5) : na

ma_low_1 = envelope_count > 0 ? ma_base * (1 - enveloppe_step) : na
ma_low_2 = envelope_count > 0 ? ma_base * (1 - enveloppe_step * 2) : na
ma_low_3 = envelope_count > 0 ? ma_base * (1 - enveloppe_step * 3) : na
ma_low_4 = envelope_count > 0 ? ma_base * (1 - enveloppe_step * 4) : na
ma_low_5 = envelope_count > 0 ? ma_base * (1 - enveloppe_step * 5) : na


// ---------------------------------------------
// --------------- STRATEGY --------------------
if use_longs
    if envelope_count > 0 and strategy.opentrades < 1
        strategy.entry('long 1', strategy.long, limit=ma_low_1, qty=(strategy.equity / ma_low_1) * (1 / envelope_count))
    if envelope_count > 1 and strategy.opentrades < 2
        strategy.entry('long 2', strategy.long, limit=ma_low_2, qty=(strategy.equity / ma_low_2) * (1 / envelope_count))
    if envelope_count > 2 and strategy.opentrades < 3
        strategy.entry('long 3', strategy.long, limit=ma_low_3, qty=(strategy.equity / ma_low_3) * (1 / envelope_count))
    if envelope_count > 3 and strategy.opentrades < 4
        strategy.entry('long 4', strategy.long, limit=ma_low_4, qty=(strategy.equity / ma_low_4) * (1 / envelope_count))
    if envelope_count > 4 and strategy.opentrades < 5
        strategy.entry('long 5', strategy.long, limit=ma_low_5, qty=(strategy.equity / ma_low_5) * (1 / envelope_count))


if use_short
    if envelope_count > 0 and strategy.opentrades < 1
        strategy.entry('short 1', strategy.short, limit=ma_high_1, qty=(strategy.equity / ma_high_1) * (1 / envelope_count))
    if envelope_count > 1 and strategy.opentrades < 2
        strategy.entry('short 2', strategy.short, limit=ma_high_2, qty=(strategy.equity / ma_high_2) * (1 / envelope_count))
    if envelope_count > 2 and strategy.opentrades < 3
        strategy.entry('short 3', strategy.short, limit=ma_high_3, qty=(strategy.equity / ma_high_3) * (1 / envelope_count))
    if envelope_count > 3 and strategy.opentrades < 4
        strategy.entry('short 4', strategy.short, limit=ma_high_4, qty=(strategy.equity / ma_high_4) * (1 / envelope_count))
    if envelope_count > 4 and strategy.opentrades < 5
        strategy.entry('short 5', strategy.short, limit=ma_high_5, qty=(strategy.equity / ma_high_5) * (1 / envelope_count))

strategy.exit('close', limit=ma_base)


// ---------------------------------------------
// ------------------ PLOT ---------------------
ma_base_plot = plot(ma_base, title = "Base MA", color = color.orange, linewidth = 3, offset = 1)

ma_high_1_plot = plot(ma_high_1, title = "MA high 1", color = color.red, offset = 1)
ma_high_2_plot = plot(ma_high_2, title = "MA high 2", color = color.red, offset = 1)
ma_high_3_plot = plot(ma_high_3, title = "MA high 3", color = color.red, offset = 1)
ma_high_4_plot = plot(ma_high_4, title = "MA high 4", color = color.red, offset = 1)
ma_high_5_plot = plot(ma_high_5, title = "MA high 5", color = color.red, offset = 1)

ma_low_1_plot = plot(ma_low_1, title = "MA low 1", color = color.green, offset = 1)
ma_low_2_plot = plot(ma_low_2, title = "MA low 2", color = color.green, offset = 1)
ma_low_3_plot = plot(ma_low_3, title = "MA low 3", color = color.green, offset = 1)
ma_low_4_plot = plot(ma_low_4, title = "MA low 4", color = color.green, offset = 1)
ma_low_5_plot = plot(ma_low_5, title = "MA low 5", color = color.green, offset = 1)

```

> Detail

https://www.fmz.com/strategy/434190

> Last Modified

2023-12-04 16:12:39
