
> Name

Breakout-Band-Fixed-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13c2c9c2cb70a5b92e8.png)

[trans]

## Overview
The main idea of ​​this strategy is to use breakout bands to identify the trend direction and combine it with fixed stops for risk management. The strategy first calculates the highest price and lowest price within a certain period to form a breakthrough zone. A trading signal is generated when the price breaks through the breakout band. Additionally, the strategy allows traders to set fixed stop loss amounts. For each transaction, the system will reversely calculate the number of transactions based on the fixed stop loss amount, thereby achieving a fixed loss for each order.
## Strategy Principle
The strategy mainly consists of four parts: position management, breakout zone identification, stop loss setting and quantity calculation.
First, the strategy must determine whether a position is currently held. If a position is already held, no new signal is generated.
Secondly, the strategy will calculate the highest price and lowest price within a certain period to form a breakthrough zone. A trading signal is generated when the price breaks from the inside to the outside of the breakout band. Specifically, if the price breaks through the upper band of the breakout band, a long signal is generated; if the price breaks through the lower band of the breakout band, a short signal is generated.
In addition, when a long signal is generated, the strategy will set the stop loss level at the midpoint of the breakout zone. When a short signal is generated, a stop loss level will also be set. In order to track the stop loss, the strategy will also adjust the stop loss level in real time during the position period.
Finally, the strategy allows setting a fixed stop loss amount. When a signal is generated, the strategy will calculate the distance in points from the stop loss point to the current price, and then combine the quotation unit, exchange rate and other factors to calculate the amount represented by the price change between the stop loss points. The trade quantity is then calculated backwards based on the fixed stop loss amount.
These are the main principles of the strategy. Identifying the trend direction through the breakout zone and using fixed stop loss for risk control are the core ideas of this strategy.
## Advantage Analysis
This breakout with fixed stop strategy offers the following advantages:
1. Advanced stop loss thinking. The strategy uses a fixed stop loss amount rather than a fixed stop loss distance. This avoids the problem of unfixable risks caused by different point values ​​between different varieties. From a risk management perspective, fixed amount stop loss is more advanced.
2. The quantity calculation is reasonable. The strategy can intelligently calculate the number of transactions based on the fixed stop loss amount, making the loss of each order controllable, thereby reasonably controlling risk exposure.
3. Breakthrough identification is simple and effective. The identification method of breakout zones is simple and direct, and can effectively identify the trend direction. Compared with just breaking through a certain price level, such breakthrough zone identification can avoid more false signals that deviate from the trend direction.
4. Trailing stop loss increases profit. The strategy can adjust the stop loss position in real time and perform trailing stop loss to help lock in more profits.
5. Wide range of applications. The strategy is applicable to any variety. As long as the parameters are set, the risk of a fixed amount of stop loss can be controlled, so it has very wide applicability.
6. The code structure is clear. The strategy code structure is reasonable and clear, and each functional module is well decoupled, making it easy to understand and subsequently optimize.
## Risk Analysis
Although this strategy has the above advantages, there are still certain risks that need to be noted:
1. The quality of the breakthrough pattern cannot be judged. The strategy cannot judge the morphological quality of the breakthrough, which may produce some low-quality signals. It needs to be filtered in combination with other indicators.
2. Fixed stops may be too mechanical. Market prices often have the characteristics of short jumps, and fixed stop losses may rely too much on rules and cannot be adjusted flexibly.
3. Unable to limit transaction frequency. The strategy cannot limit the trading frequency and may exit the market too frequently. Need to combine with other rules to limit the frequency.
4. Fixed stop loss depends on parameter settings. The setting of the fixed stop loss amount is related to the overall exposure control and needs to be set appropriately based on various aspects such as fund size and risk preference.
5. Breakout directions may generate false signals. When prices fluctuate or pull back, false breakout signals may be generated. Multiple conditions need to be combined for optimization.
6. Lack of take profit setting. The strategy currently does not have a profit-taking mechanism and cannot proactively determine profits. This can lead to suboptimal profits.
In response to the above risks, we can optimize from the following aspects:
1. Add indicators to judge the form and filter the signal quality. For example, MACD, KD, etc.
2. Evaluate breakthrough quality based on breakthrough strength indicators. For example, judging the strength of a breakthrough through changes in trading volume.
3. Increase the position opening frequency limit. Such as only trading once a day or similar rules.
4. Optimize fixed stop loss setting logic. For example, changing to a percentage stop loss based on a specific threshold, etc.
5. Add other filter conditions. For example, enhanced stop loss, price volatility, etc.
6. Add a take profit strategy. For example, take profit when approaching a resistance level.
## Optimization direction
Based on the above analysis, this strategy can be optimized from the following aspects:
1. Add filtering conditions to improve signal quality. A variety of technical indicators can be added to determine the quality of the trend and avoid undesirable breakthrough signals. Breakthrough strength can also be judged.
2. Optimize the stop loss strategy and make it more flexible. It can be changed to a proportional stop loss after breaking through and retracing a certain distance. Stop loss distance can also be optimized in real time based on volatility.
3. Control the frequency of transactions and avoid excessive trading. Filter conditions can be set for time periods or times to reduce transaction frequency.
4. Combine with trend judgment indicators to improve entry timing. For example, the optimization is to enter the market after the trend is confirmed.
5. Optimize the profit-taking strategy and improve profitability. You can set target profit, moving take profit, fluctuation take profit, etc.
6. Optimize risk parameter settings. A better parameter combination can be set based on the backtest results, such as fixed stop loss amount, breakthrough period, etc.
7. Improve code structure and enhance scalability. Further decouple modules such as signal generation, filtering, risk control, and profit.
8. Test the arbitrage space of more varieties. Evaluate the arbitrage advantages of different product combinations.
Through the above multiple aspects of optimization, the stability and profitability of the breakout stop loss strategy can be further enhanced. At the same time, it also lays the foundation for expanding to more strategic combinations in the future.
## Summarize
The overall idea of ​​this strategy is reasonable, using breakout bands to identify trends, and using fixed amount stop losses for risk control. This is progressive in risk management. At the same time, the idea of ​​calculating the number of transactions is also more reasonable, and the loss of each order can be controlled. However, the strategy can be optimized in many aspects to improve signal quality, stop loss strategy flexibility, profitability, etc. If filtering is combined with trend judgment indicators, the profit-taking method is improved, and the trading frequency is strictly controlled, the effect of this strategy still has a lot of room for improvement. Overall, this strategy provides a set of risk management and quantity calculation methods that can be learned, laying the foundation for further research on arbitrage and multi-strategy combinations.
|| 

## Overview

The main idea of this strategy is to use the breakout band to identify trend direction and combine fixed stop loss for risk management. The strategy first calculates the highest and lowest prices over a certain period to form a breakout band. When the price breaks through the breakout band, a trading signal is generated. In addition, the strategy allows traders to set a fixed stop loss amount. Each time a trade is placed, the system will calculate the position size based on the fixed stop loss amount, so that each loss is fixed.

## Strategy Principle 

The strategy consists of four main parts: position management, breakout band identification, stop loss setting and position sizing.

Firstly, the strategy checks if there is any open position. If there is, no new signals will be generated.

Secondly, the strategy calculates the highest and lowest prices over a period to form a breakout band. When the price breaks out of the band, a trading signal is generated. Specifically, if the price breaks above the upper band, a long signal is generated. If the price breaks below the lower band, a short signal is generated.

In addition, when a long signal is generated, the strategy sets the midpoint of the breakout band as the stop loss. The same goes for short signals. To trail the stop loss, the strategy also adjusts the stop loss in real-time when in position. 

Finally, the strategy allows setting a fixed stop loss amount. When a signal is generated, the strategy calculates the number of pips from stop loss to current price, and combines factors like tick size and exchange rate, to determine the price change between stop loss and current price in monetary terms. The position size is then calculated based on the fixed stop loss amount.

Above are the main principles of the strategy. Identifying trend direction with breakout bands and controlling risk with fixed stop loss are the core concepts.

## Advantages

This breakout band fixed stop loss strategy has the following advantages:

1. Advanced stop loss concept. The strategy uses fixed stop loss amount instead of fixed stop loss distance. This avoids the problem of unable to fix risk across products with different tick values. From a risk management perspective, fixed monetary stop loss is more advanced.

2. Reasonable position sizing. The strategy can intelligently calculate position size based on the fixed stop loss amount, so that the loss per trade is controlled, thereby reasonably managing risk exposure.

3. Simple and effective breakout identification. Identifying breakout with bands is simple and direct, and can effectively identify trend direction. Compared to breakout of a single price level, this breakout band identification can avoid more false signals away from the trend. 

4. Trailing stop loss increases profit. The strategy's ability to adjust stop loss in real-time for trailing stop loss helps lock in more profits.

5. Wide applicability. The strategy is applicable to any products. As long as parameters are set properly, fixed amount stop loss risk control can be achieved, making the strategy highly versatile.

6. Clean code structure. The code structure is clear and modular, making it easy to understand and optimize.

## Risks

Despite the advantages, there are some risks to note for the strategy:

1. Breakout pattern quality untested. The strategy does not judge breakout pattern quality and may generate some low quality signals. Other indicators are needed to filter signals.

2. Fixed stop loss may be too mechanical. Market prices often gap. Fixed stop loss may rely too much on rules and lacks flexibility in adjustment. 

3. No limit on trade frequency. The strategy does not limit trade frequency and may trade too often. Other rules are needed to limit frequency.

4. Fixed stop loss depends on parameter setting. Setting fixed stop loss amount is crucial for overall risk control and needs to consider capital size, risk appetite etc.

5. Breakout direction may give wrong signals. Wrong breakout signals may occur during price oscillations or pullbacks. More conditions are needed to optimize the strategy. 

6. No profit taking mechanism. The strategy currently has no profit taking capability to actively lock in profits. This may lead to unsatisfactory profits.

To address these risks, some ways to optimize the strategy include:

1. Adding indicators to filter signal quality, e.g. MACD, KD etc. 

2. Incorporating breakout strength indicators to evaluate quality. For example, judging strength through volume changes.

3. Adding open trade frequency limits, e.g. one trade per day.

4. Optimizing fixed stop loss logic, e.g. percentage-based stop loss above a threshold. 

5. Adding other filters, e.g. volatility, enhance stop loss etc. 

6. Incorporating profit taking strategies, e.g. taking profit near resistance.

## Optimization Directions

Based on the analysis, the strategy can be optimized in the following aspects:

1. Adding filters to improve signal quality using multiple technical indicators and assessing trend quality. Also judging breakout strength.

2. Optimizing stop loss for more flexibility. Can switch to percentage-based trailing stop after a certain retracement. Can also optimize dynamically based on volatility.

3. Controlling trade frequency to avoid over-trading by adding filters on time periods or frequency.

4. Incorporating trend indicators to improve timing, e.g. waiting for trend confirmation. 

5. Optimizing profit taking strategies to improve profitability via profit target, trailing profit stop, volatility stop etc.

6. Optimizing risk parameters based on backtests, such as fixed stop amount, breakout period etc.

7. Refactoring code for better extensibility by further decoupling signal, filter, risk, profit modules. 

8. Testing more products for arbitrage opportunities. Evaluate advantage across different product combinations.

Through these optimization dimensions, the breakout stop loss strategy can become more robust and profitable. It also lays the foundation for expanding into more strategy combinations.

## Conclusion

Overall the strategy is reasonable in using breakout bands to identify trends and fixed amount stops for risk control. The concepts are progressive for risk management. The position sizing logic is also sound for controlling loss per trade. But the strategy can be enhanced through various optimizations to improve signal quality, flexibility in stop loss, profitability etc. By incorporating trend filters, improving profit taking, and strictly controlling trade frequency, significant improvement can be achieved. In conclusion, the strategy provides a framework for learning risk management and position sizing techniques, laying the groundwork for further research into more complex arbitrage and multi-strategy systems.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|100|(?Money management)Risk price for each entry|
|v_input_2|0|Deposit currency: USD|
|v_input_3|100|(?Entry strategy)Entry band bar count|
|v_input_4|2018|(?Backtesting range)From Year|
|v_input_5|true|From Month|
|v_input_6|true|From Day|
|v_input_7|2020|To Year|
|v_input_8|12|To Month|
|v_input_9|31|To Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-26 00:00:00
end: 2023-10-28 03:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
//@version=4
//@author=Takazudo

strategy("Fixed price SL",
  overlay=true,
  default_qty_type=strategy.fixed,
  initial_capital=0,
  currency=currency.USD)

var COLOR_TRANSPARENT = color.new(#000000, 100)
var COLOR_ENTRY_BAND = color.new(#43A6F5, 30)

//============================================================================
// config
//============================================================================

// Money management
_g1 = 'Money management'
var config_riskPrice = input(100, minval=1, title="Risk price for each entry", group=_g1)
var config_depositCurrency = input(title="Deposit currency", type=input.string, defval="USD", options=["USD"], group=_g1)

// Entry strategy
_g2 = 'Entry strategy'
var config_entryBandBars = input(defval = 100, title = "Entry band bar count",  minval=1, group=_g2)

// Backtesting range
_g3 = 'Backtesting range'
fromYear  = input(defval = 2018, title = "From Year",  minval = 1970, group=_g3)
fromMonth = input(defval = 1,    title = "From Month", minval = 1, maxval = 12, group=_g3)
fromDay   = input(defval = 1,    title = "From Day",   minval = 1, maxval = 31, group=_g3)
toYear  = input(defval = 2020, title = "To Year",  minval = 1970, group=_g3)
toMonth = input(defval = 12,    title = "To Month", minval = 1, maxval = 12, group=_g3)
toDay   = input(defval = 31,    title = "To Day",   minval = 1, maxval = 31, group=_g3)

//============================================================================
// exchange caliculations
//============================================================================

// mico pip size caliculation
// ex1: AUDCAD -> 0.0001
// ex2: USDJPY -> 0.01
f_calcMicroPipSize() =>
    _base = syminfo.basecurrency
    _quote = syminfo.currency
    _result = 0.0001
    if _quote == 'JPY'
        _result := _result * 100
    if _base == 'BTC'
        _result := _result * 100
    _result

// convert price to pips
f_convertPriceToPips(_price) =>
    _microPipSize = f_calcMicroPipSize()
    _price / _microPipSize

// caliculate exchange rate between deposit and quote currency
f_calcDepositExchangeSymbolId() =>
    _result = ''
    _deposit = config_depositCurrency
    _quote = syminfo.currency
    if (_deposit == 'USD') and (_quote == 'USD')
        _result := na
    if (_deposit == 'USD') and (_quote == 'AUD')
        _result := 'OANDA:AUDUSD'
    if (_deposit == 'EUR') and (_quote == 'USD')
        _result := 'OANDA:EURUSD'
    if (_deposit == 'USD') and (_quote == 'GBP')
        _result := 'OANDA:GBPUSD'
    if (_deposit == 'USD') and (_quote == 'NZD')
        _result := 'OANDA:NZDUSD'
    if (_deposit == 'USD') and (_quote == 'CAD')
        _result := 'OANDA:USDCAD'
    if (_deposit == 'USD') and (_quote == 'CHF')
        _result := 'OANDA:USDCHF'
    if (_deposit == 'USD') and (_quote == 'JPY')
        _result := 'OANDA:USDJPY'
    _result

// Let's say we need CAD to USD exchange
// However there's only "OANDA:USDCAD" symbol.
// Then we need to invert the exhchange rate.
// this function tells us whether we should invert the rate or not
f_calcShouldInvert() =>
    _result = false
    _deposit = config_depositCurrency
    _quote = syminfo.currency
    if (_deposit == 'USD') and (_quote == 'CAD')
        _result := true
    if (_deposit == 'USD') and (_quote == 'CHF')
        _result := true
    if (_deposit == 'USD') and (_quote == 'JPY')
        _result := true
    _result

// caliculate how much quantity should I buy or sell
f_calcQuantitiesForEntry(_depositExchangeRate, _slPips) =>
    _microPipSize = f_calcMicroPipSize()
    _priceForEachPipAsDeposit = _microPipSize * _depositExchangeRate
    _losePriceOnSl = _priceForEachPipAsDeposit * _slPips
    floor(config_riskPrice / _losePriceOnSl)

//============================================================================
// Quantity caliculation
//============================================================================

depositExchangeSymbolId = f_calcDepositExchangeSymbolId()

// caliculate deposit exchange rate
rate = security(depositExchangeSymbolId, timeframe.period, hl2)
shouldInvert = f_calcShouldInvert()
depositExchangeRate = if config_depositCurrency == syminfo.currency
    // if USDUSD, no exchange of course
    1
else
    // else, USDCAD to CADUSD invert if we need
    shouldInvert ? (1 / rate) : rate

//============================================================================
// Range Edge caliculation
//============================================================================

f_calcEntryBand_high() =>
    _highest = max(open[3], close[3])
    for i = 4 to (config_entryBandBars - 1)
        _highest := max(_highest, open[i], close[i])
    _highest

f_calcEntryBand_low() =>
    _lowest = min(open[3], close[3])
    for i = 4 to (config_entryBandBars - 1)
        _lowest := min(_lowest, open[i], close[i])
    _lowest

entryBand_high = f_calcEntryBand_high()
entryBand_low = f_calcEntryBand_low()
entryBand_height = entryBand_high - entryBand_low

plot(entryBand_high, color=COLOR_ENTRY_BAND, linewidth=1)
plot(entryBand_low, color=COLOR_ENTRY_BAND, linewidth=1)

rangeBreakDetected_long = entryBand_high < close
rangeBreakDetected_short = entryBand_low > close

shouldMakeEntryLong = (strategy.position_size == 0) and rangeBreakDetected_long
shouldMakeEntryShort = (strategy.position_size == 0) and rangeBreakDetected_short

//============================================================================
// SL & Quantity
//============================================================================

var sl_long = hl2
var sl_short = hl2

entryQty = 0
slPips = 0.0

// just show info bubble
f_showEntryInfo(_isLong) =>
    _str =
      'SL pips: ' + tostring(slPips) + '\n' +
      'Qty: ' + tostring(entryQty)
    _bandHeight = entryBand_high - entryBand_low
    _y = _isLong ? (entryBand_low + _bandHeight * 1/4) : (entryBand_high - _bandHeight * 1/4)
    _style = _isLong ? label.style_label_up : label.style_label_down
    label.new(bar_index, _y, _str, size=size.large, style=_style)

if shouldMakeEntryLong
    sl_long := (entryBand_high + entryBand_low) / 2
    slPips := f_convertPriceToPips(close - sl_long)
    entryQty := f_calcQuantitiesForEntry(depositExchangeRate, slPips)
if shouldMakeEntryShort
    sl_short := (entryBand_high + entryBand_low) / 2
    slPips := f_convertPriceToPips(sl_short - close)
    entryQty := f_calcQuantitiesForEntry(depositExchangeRate, slPips)

// trailing SL
if strategy.position_size > 0
    sl_long := max(sl_long, entryBand_low)
if strategy.position_size < 0
    sl_short := min(sl_short, entryBand_high)

//============================================================================
// backtest duration
//============================================================================

// Calculate start/end date and time condition
startDate  = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear,   toMonth,   toDay,   00, 00)

//============================================================================
// make entries
//============================================================================

if (true)
    if shouldMakeEntryLong
        strategy.entry(id="Long", long=true, stop=close, qty=entryQty)
        f_showEntryInfo(true)
    if shouldMakeEntryShort
        strategy.entry(id="Short", long=false, stop=close, qty=entryQty)
        f_showEntryInfo(false)

strategy.exit('Long-SL/TP', 'Long', stop=sl_long)
strategy.exit('Short-SL/TP', 'Short', stop=sl_short)

//============================================================================
// plot misc
//============================================================================

sl = strategy.position_size > 0 ? sl_long :
  strategy.position_size < 0 ? sl_short : na

plot(sl, color=color.red, style=plot.style_cross, linewidth=2, title="SL")

value_bgcolor = rangeBreakDetected_long ? color.green :
  rangeBreakDetected_short ? color.red : COLOR_TRANSPARENT

bgcolor(value_bgcolor, transp=95)

```

> Detail

https://www.fmz.com/strategy/430975

> Last Modified

2023-11-03 14:31:21
