
> Name

KP Moving Average Trend Strategy Heyping-Moving-Average-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1394ba94a9019d912c6.png)
[trans]

### Overview
KP moving average trend strategy is a trend following strategy based on a combination of technical analysis indicators. This strategy mainly uses the average moving average indicator to identify the price trend direction, and uses the moving average crossover signal to determine the entry timing. Strategies can be implemented on the TradingView platform and achieve better performance through parameter optimization.
### Strategy Principles
KP strategy mainly uses three types of indicators:
1. Average lines: fast EMA and slow SMA. EMA is more sensitive to price changes, and SMA is more stable. When used together, the fast EMA crosses the slow SMA to generate trading signals.
2. Hicken Ash candlestick chart: a special candlestick chart with clearer trend characteristics. The price data source used in the strategy to draw the EMA moving average.
3. Logarithmic transformation option: Optional logarithmic transformation of price data makes it easier to observe percentage price changes.
The specific trading logic is that when the fast EMA breaks through the slow SMA upward, go long; when it breaks down below, close the position. This strategy is a typical trend following strategy.
### Advantage Analysis
1. The parameters are highly adjustable and can be adapted to different varieties and trading periods.
2. The combination of visual indicators forms a clear and easy-to-read trend trading strategy.
3. Add logarithmic transformation options to deal with more volatile varieties
4. Hiken Ash candlestick chart is better for determining the trend direction.
5. Integrate stop loss mechanism to control risks
### Risk Analysis
1. Risk of trend reversal, need to stop losses in time
2. Parameter optimization requires caution to avoid overfitting.
3. Trading type and time period selection have a great impact on strategy performance
4. Adequate backtesting is required to ensure parameter robustness
### Optimization direction
1. Add adaptive parameter optimization module
2. Integrate more indicators to filter out false signals
3. Add algorithmic trading module to realize automated order placing
4. Combine machine learning technology to determine key points
5. Optimize the stop loss strategy and implement dynamic tracking stop loss
### Summarize
KP moving average trend strategy integrates a variety of technical indicators to determine the trend direction, with flexible parameter settings and excellent visualization effects. This strategy can be used as a basic trend following strategy and can be used for real trading after appropriate optimization and adjustment. However, users must keep in mind that no strategy can predict the market perfectly, and they need to control risks and operate prudently.
|| 

## Overview  

The Heyping Moving Average Trend Strategy is a technical indicator combo strategy designed to track price trends. It generates entry and exit signals based on moving average crossovers to time the market. The strategy can be implemented on the TradingView platform and optimized for performance.

## Strategy Logic

The KP strategy utilizes three types of indicators:

1. Moving Averages: A faster EMA and slower SMA. The EMA reacts faster to price changes while the SMA is more stable. Crossovers between the two produce trade signals.  

2. Heiken Ashi Candles: Special candlestick charts with clearer trend definition. Used as the price data source for plotting the EMAs.

3. Log Transformation: An option to log transform price data to better visualize percentage changes.

The specific logic is to go long when the faster EMA crosses above the slower SMA, and to exit the position when the reverse crossover happens. This strategy belongs to the trend following category. 

## Advantage Analysis 

1. Highly customizable parameters catering to different products and timeframes
2. Visual indicators combined into an easy-to-read system  
3. Log transformation option to handle volatile instruments
4. Heiken Ashi candles offer superior trend determination
5. Integrates stop loss to control risk

## Risk Analysis

1. Trend reversal risk. Timely stop loss required
2. Careful parameter optimization to avoid overfitting  
3. Instrument and timeframe selections greatly impact results
4. Robustness must be validated through backtesting

## Optimization Directions

1. Add adaptive parameter optimization module
2. Incorporate more filters to avoid false signals
3. Build algo trading module for automation
4. Apply machine learning models at inflection points
5. Enhance stop loss strategy for dynamic trailing stop loss

## Conclusion

The Heyping Moving Average Trend Strategy combines various technical indicators to define trend directions with flexible configurations and great visualization. It can serve as a baseline trend following strategy and be further tuned for live trading while noting no strategy is perfect. Risk management is key.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|D|Heikin Ashi Candle Time Frame|
|v_input_2|false|Heikin Ashi Candle Time Frame Shift|
|v_input_3|W|Heikin Ashi EMA Time Frame|
|v_input_4|false|Heikin Ashi EMA Time Frame Shift|
|v_input_5|10|Heikin Ashi EMA Period|
|v_input_6|false|Heikin Ashi EMA Shift|
|v_input_7|100|Slow EMA Period|
|v_input_8|false|Slow EMA Shift|
|v_input_9|false|Log Transform|
|v_input_10|true|Stop Loss|
|v_input_11|true|Show Plots|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-27 00:00:00
end: 2024-01-02 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("KP 15min Strategy", shorttitle="KP15", overlay=false)

res = input("D",title="Heikin Ashi Candle Time Frame")
hshift = input(0, title="Heikin Ashi Candle Time Frame Shift")
res1 = input("W",title="Heikin Ashi EMA Time Frame")
mhshift = input(0, title="Heikin Ashi EMA Time Frame Shift")
fama = input(10, title="Heikin Ashi EMA Period")
test = input(0, title="Heikin Ashi EMA Shift")
sloma = input(100, title="Slow EMA Period")
slomas = input(0, title="Slow EMA Shift")
logtransform = input(false, title="Log Transform")
stoploss = input(true, title="Stop Loss")
showplots = input(true, title="Show Plots")

ha_t = request.security(syminfo.tickerid, res, expression=hlc3)
ha_close = request.security(syminfo.tickerid, res, expression=logtransform ? math.log(close[hshift]) : close[hshift])
mha_close = request.security(syminfo.tickerid, res1, expression=logtransform ? math.log(close[mhshift]) : close[mhshift])

fma = ta.ema(mha_close[test], fama)
sma = ta.ema(ha_close[slomas], sloma)

plot(showplots ? (logtransform ? math.exp(fma) : fma) : na, title="MA", color=color.new(color.blue, 0), linewidth=2, style=plot.style_line)
plot(showplots ? (logtransform ? math.exp(sma) : sma) : na, title="SMA", color=color.new(color.orange, 0), linewidth=2, style=plot.style_line)

golong = ta.crossover(fma, sma)
exitLong = ta.crossunder(fma, sma)

if (golong)
    strategy.entry("Buy", strategy.long)

if (exitLong)
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/437508

> Last Modified

2024-01-03 12:18:29
