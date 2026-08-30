
> Name

BBB StrategyBBB-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The BB%B strategy is a quantitative trading strategy that uses the percentage B value of the Bollinger Band indicator to make investment decisions. It can issue a buy or sell signal when the price approaches the upper or lower track of the Bollinger Band, and is a trend following strategy.
## Strategy Principle
This strategy first calculates the moving average and standard deviation of the closing price of the specifiedPeriod days, and then obtains the upper and lower rails of the Bollinger Bands. The BB%B indicator is based on the current price minus the lower rail price, and then divided by the upper rail price minus the lower rail price, indicating the position of the current price within the Bollinger Bands. A buy signal is generated when BB%B is lower than the oversold threshold, and a sell signal is generated when it is higher than the overbought threshold. After the trading signal is issued, if BB%B falls back to near the opposite threshold, the position will be closed.
Specifically, the strategy first calculates the SMA of the 21-day closing price and 2 times the standard deviation to obtain the upper and lower Bollinger Bands. Then calculate the BB%B value of the current closing price. If the BB%B value is lower than -0.2 (configurable) and there is currently no position, go long; if the BB%B value is higher than 1.2 (configurable) and there is currently no position, go short. The closing signal is when the BB%B value crosses 1.0 when holding a long position (configurable); when the BB%B value falls below 0.2 when holding a short position (configurable).
This strategy relies on the BB%B indicator to determine whether the current price is too high or too low, and relies on the moving average to determine the current trend direction. When the price exceeds the upper and lower rails of the Bollinger Bands, a trading signal is generated. The frequency of the policy can be adjusted by configuring different parameters.
## Advantage Analysis
- Use the Bollinger Bands indicator to determine overbought and oversold
The upper and lower bands of Bollinger Bands respectively represent a certain standard deviation range of the current price. When the price approaches or touches the upper band, it represents overbought, and when it approaches or touches the lower band, it represents oversold. The BB%B strategy makes full use of this feature to determine the appropriate time to buy and sell.
- Flexible configuration, adjustable strategy frequency
The BB%B threshold, moving average parameters, and retracement thresholds in the strategy can be freely configured, which provides convenience for adjusting the frequency of the strategy. Using longer moving averages and larger pullback thresholds can reduce trading frequency.
- Judgment based on trends
In addition to judging overbought and oversold by Bollinger Bands, it also combines moving averages to judge the general trend to avoid counter-trend trading.
- Pullback mechanism reduces false signals
When the price touches the upper or lower Bollinger Band for the first time, it is likely to be marked as overbought or oversold, but it may also be a short-term false breakthrough. This strategy adds a fallback threshold. The position will only be closed when BB%B clearly falls back to the opposite direction, which can filter out false signals.
## Risk Analysis
- Unable to judge price trends
This strategy only looks at the Bollinger Bands indicator to judge possible price reversals and ignores the judgment of the general trend, which may lead to losses in counter-trend trading.
- Improper setting of the fallback threshold can easily miss opportunities
If the pullback threshold is set too large, it may result in the inability to switch the position direction in time after the trend reverses, and miss the opportunity.
- When Bollinger Bands expand, the price difference between buying and selling points becomes larger.
When market volatility increases, the distance between the upper and lower rails of the Bollinger Bands expands, the price difference between buying and selling points becomes larger, and the risk of single loss increases.
-Higher transaction frequency
Compared with the long-term strategy, this strategy has a higher trading frequency and will generate more transaction costs and slippage losses.
## Optimization direction
- Filter signals combined with trend indicators
Trend judgment indicators such as MACD and KDJ can be added to send trading signals only when the trend direction is consistent to avoid counter-trend trading.
- Add stop loss mechanism
Set a fixed value or percentage stop loss to control the risk of a single loss and prevent the loss from expanding.
- Optimize parameter combination
Adjust parameters such as moving average length, BB%B threshold, and fallback threshold to find the optimal parameter combination to filter out more noise and improve strategy stability.
- Consider transaction cost factors
According to the transaction cost of different varieties, adjust the parameters of the strategy, reduce the frequency of transactions, and reduce the impact of transaction costs.
## Summarize
The BB%B strategy is a simple and practical quantitative trading strategy. It uses Bollinger Bands to judge the timing of possible price reversal, cooperates with the moving average to judge the general trend, and trades near overbought and oversold points. The policy configuration is flexible and the frequency of the policy can be adjusted. However, there are also certain risks, which require further optimization and consideration of factors such as general trends, stop losses, and transaction costs to improve strategy stability and actual profitability. If used properly, the BB%B strategy can become an effective part of the quantitative trading system.
|| 


## Overview

The BB%B strategy is a quantitative trading strategy that utilizes the percentage B value of Bollinger Bands to make investment decisions. It can generate buy and sell signals when price approaches the upper or lower rail of the Bollinger Bands, and belongs to trend-following strategies.

## Strategy Logic

The strategy first calculates the SMA of closing prices over a specifiedPeriod, as well as standard deviation, to obtain the upper and lower rails of the Bollinger Bands. The BB%B indicator represents the position of current price within the Bollinger Bands, calculated by the formula (Current Price - Lower Rail) / (Upper Rail - Lower Rail). When BB%B falls below the oversold threshold, a buy signal is generated. When BB%B rises above the overbought threshold, a sell signal is generated. After the trading signal is triggered, if BB%B retreats back to the opposite threshold, the position will be closed.

Specifically, the strategy first calculates the 21-day SMA and 2x standard deviation to obtain the upper and lower rails of the Bollinger Bands. It then calculates the current closing price's BB%B value. If BB%B is below -0.2 (configurable) and there is no current position, go long. If BB%B is above 1.2 (configurable) and there is no current position, go short. The exit signals are triggered when the long position exists and BB%B crosses above 1.0 (configurable), or when the short position exists and BB%B crosses below 0.2 (configurable).

The strategy relies on the BB%B indicator to determine if the current price is overextended on the upside or downside, and also uses the SMA to judge the current trend direction. It generates trading signals when price exceeds the Bollinger Bands rails. Tweaking different parameters can adjust the frequency of the strategy.

## Advantage Analysis

- Utilize Bollinger Bands to identify overbought/oversold levels

The upper and lower rails of Bollinger Bands represent a certain standard deviation range of the current price. Prices approaching or touching the upper rail signal overbought conditions, while approaching or touching the lower rail signal oversold conditions. The BB%B strategy makes full use of this characteristic to determine appropriate entry and exit points.

- Flexible configuration to adjust frequency

The BB%B thresholds, SMA periods, pullback thresholds are all configurable, which provides convenience to adjust the trading frequency. Using longer SMA and larger pullback threshold can reduce frequency.

- Combine trend identification 

In addition to overbought/oversold determination with Bollinger Bands, it also combines SMA to judge the overall trend, avoiding trading against the trend.

- Pullback mechanism to avoid false signals

When price first touches the Bollinger Bands rails, the probability of overbought/oversold is high, but it could also be short-term false breakout. This strategy adopts pullback threshold, only exiting positions after BB%B clearly pulls back to the opposite side, filtering out false signals.

## Risk Analysis

- Unable to determine price trend

The strategy solely looks at the Bollinger Bands indicator to determine potential reversals, ignoring the overall trend, which may lead to trading against the trend and losses.

- Improper pullback threshold may miss opportunities 

If pullback threshold is set too high, trend reversal may not trigger position change in time, missing opportunities.

- Wider price spread when Bollinger Bands expand

When market volatility increases, the distance between the upper and lower rails also increases, leading to larger price spread for entry and exit, thus higher risk per trade.

- Relatively high trading frequency

Compared to long-term strategies, this strategy has higher trading frequency, incurring more trading costs and slippage. 

## Improvement Directions

- Incorporate trend indicators for signal filtering

Add trend determining indicators like MACD, KDJ to only trigger trades along the trend direction, avoiding counter-trend trades.

- Implement stop loss mechanism 

Set fixed amount or percentage stop loss to control per trade risk and avoid loss expansion.

- Optimize parameter combinations

Adjust SMA periods, BB%B thresholds, pullback thresholds etc to find the optimal parameter combination, filtering out more noise and improve stability.

- Consider trading costs 

For different products, adjust parameters to lower trading frequency based on their trading costs profile to reduce impact.

## Summary

The BB%B strategy is a simple and practical quantitative trading strategy. It uses Bollinger Bands to identify potential reversal price points, combines with SMA for trend direction, and trades around overbought/oversold levels. The strategy is flexible to adjust frequency. But it also has risks that need further improvements, considering factors like overall trend, stop loss, trading costs, to enhance stability and profitability. When used properly, BB%B strategy can become an effective component in quantitative trading systems.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|21|length|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|StdDev|
|v_input_float_2|1.2|Overbought Line|
|v_input_float_3|true|Overbought Close|
|v_input_float_4|-0.2|Oversold Line|
|v_input_float_5|0.2|Oversold Close|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-25 00:00:00
end: 2023-09-24 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// strategy(title = "BB%B Strat", shorttitle = "BB%B Strat", format=format.price, precision=2, default_qty_type=strategy.percent_of_equity, default_qty_value=20)
length = input.int(21, minval=1)
src = input(close, title="Source")
mult = input.float(2.0, minval=0.001, maxval=50, title="StdDev")
ob = input.float(1.2, "Overbought Line", step=0.1)
ob_close = input.float(1.0, "Overbought Close", step=0.1)
os = input.float(-0.2, "Oversold Line", step=0.1)
os_close = input.float(0.2, "Oversold Close", step=0.1)
basis = ta.sma(src, length)
dev = mult * ta.stdev(src, length)
upper = basis + dev
lower = basis - dev
bbr = (src - lower)/(upper - lower)
p = plot(bbr, "Bollinger Bands %B", color=#26A69A)
ob_hline = hline(ob, "Overbought", color=color.red, linestyle=hline.style_dashed)
obc_hline = hline(ob_close, "Overbought Close", color=color.red, linestyle=hline.style_dashed)
os_hline = hline(os, "Oversold", color=color.green, linestyle=hline.style_dashed)
osc_hline = hline(os_close, "Oversold Close", color=color.green, linestyle=hline.style_dashed)
fill(ob_hline, obc_hline, color=color.new(color.red, 80), title="Overbought")
fill(os_hline, osc_hline, color=color.new(color.green, 80), title="Overbought")
bgcolor(bbr > ob ? color.new(color.fuchsia, 80) : (bbr < os ? color.new(color.lime, 80) : na))

if bbr < os and strategy.position_size == 0
    strategy.entry("L", strategy.long)
if bbr >= os_close and strategy.position_size > 0
    strategy.close_all()

if bbr > ob and strategy.position_size == 0
    strategy.entry("S", strategy.short)
if bbr <= ob_close and strategy.position_size < 0
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/427816

> Last Modified

2023-09-25 17:53:36
