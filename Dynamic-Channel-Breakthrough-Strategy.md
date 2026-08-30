
> Name

Based on Dynamic Channel Breakthrough StrategyDynamic-Channel-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11be9ee78d7176ac20a.png)
[trans]
### Overview
This strategy uses the Keltner channel indicator, combined with the moving average, to set dynamic breakthrough buying and selling prices to achieve breakthrough operations of buying low and selling high. The strategy automatically identifies channel breakout buying and selling opportunities.
### Strategy Principles
1. Calculate the middle track of the channel: use the exponential moving average to calculate the middle track of the price
2. Calculate the channel bandwidth: Calculate the channel bandwidth using the true amplitude or the moving average of the average true amplitude or the price amplitude.
3. Channel upper track and lower track: center track ±N times channel bandwidth
4. Entry sequence: When the price touches the upper rail line, set the breakthrough buying price and wait for the breakthrough; when the price touches the lower rail line, set the breakthrough selling price and wait for the breakthrough.
5. Exit sequence: stop loss when the price falls back to the middle track or when the highest price exceeds the entry price after buying; stop loss when it rebounds to the middle track after selling or when the lowest price is lower than the entry price
### Advantage Analysis
1. Use dynamic channels to quickly capture market trend changes
2. Using the middle rail is helpful in judging the direction of price trends.
3. N times bandwidth setting makes the channel range reasonable and avoids frequent position adjustments.
4. Use the breakthrough mechanism, conform to the trend theory, and follow the trend
5. Set stop loss conditions to strictly control risks
### Risk Analysis
1. The choice of the mid-track calculation method will affect the channel range and price matching effect.
2. If the N multiple is set too large or too small, it will affect the strategy’s return rate.
3. Breakthrough trading can easily form false signals, and losses should be strictly stopped
### Optimization direction
1. Try different mid-track calculation methods to find the best parameters
2. Test different N values and find the optimal multiple
3. Increase the scope of breakthroughs and avoid false signals
4. Optimize stop-loss logic and strictly control single losses
### Summarize
The overall application of this strategy is scientific and reasonable. It uses dynamic channel indicators to determine the price trend and direction, sets reasonable parameters to capture breakthrough signals, realizes buying low and selling high, and then obtains excess returns. At the same time, strategic risks are continuously optimized to enable it to operate stably in a variety of markets.
||

### Overview

This strategy uses the Keltner Channel indicator, combined with moving average lines, to set dynamic breakout buy and sell prices to achieve low-buy-high-sell breakthrough operations. The strategy can automatically identify channel breakout buy and sell opportunities.

### Strategy Principle  

1. Calculate channel median: Use exponential moving average to calculate the price median of the channel
2. Calculate channel bandwidth: Use the moving average of true volatility, average true volatility or price amplitude to calculate channel bandwidth  
3. Channel upper and lower rail: Median ± N times channel bandwidth  
4. Entry order: When the price touches the upper rail, set the breakthrough buy price and wait for the breakthrough; when the price touches the lower rail, set the breakthrough sell price and wait for the breakthrough
5. Exit order: Stop loss when price falls back to median after buying, or when highest price exceeds entry price; Stop loss when price bounces back to median after selling, or when lowest price is lower than entry price

### Advantage Analysis

1. Using dynamic channels can quickly capture changes in market trends  
2. Using median is conducive to judging the direction of price trends  
3. N times bandwidth setting makes the channel range reasonable to avoid frequent position adjustments  
4. Using breakthrough mechanisms conforms to trend theory and follows the trend
5. Setting stop loss conditions strictly controls risks  

### Risk Analysis

1. The selection of the method for calculating the median line will affect the matching effect of the channel range and prices  
2. Excessive large or small N multiples will affect the strategy's rate of return
3. Breakthrough buys and sells tend to form false signals and should be strictly stopped out

### Optimization Directions  

1. Try different median line calculation methods to find the optimal parameters  
2. Test different N values to find the optimal multiplier  
3. Increase the breakthrough amplitude to avoid false signals  
4. Optimize stop loss logic to strictly control single loss  

### Summary  

The overall strategy uses scientific and reasonable methods to judge price trends and directions through dynamic channel indicators, sets reasonable parameters to capture breakthrough signals, achieves low-buy-high-sell, and gains excess returns. At the same time, continuously optimize the risks of the strategy so that it can run stably in various markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|length|
|v_input_float_1|2|Multiplier|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|true|Use Exponential MA|
|v_input_string_1|0|Bands Style: Average True Range|True Range|Range|
|v_input_3|10|ATR Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-27 00:00:00
end: 2024-02-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(title="Keltner Strategy", overlay=true)
length = input.int(20, minval=1)
mult = input.float(2.0, "Multiplier")
src = input(close, title="Source")
exp = input(true, "Use Exponential MA")
BandsStyle = input.string("Average True Range", options = ["Average True Range", "True Range", "Range"], title="Bands Style")
atrlength = input(10, "ATR Length")
esma(source, length)=>
	s = ta.sma(source, length)
	e = ta.ema(source, length)
	exp ? e : s
ma = esma(src, length)
rangema = BandsStyle == "True Range" ? ta.tr(true) : BandsStyle == "Average True Range" ? ta.atr(atrlength) : ta.rma(high - low, length)
upper = ma + rangema * mult
lower = ma - rangema * mult
crossUpper = ta.crossover(src, upper)
crossLower = ta.crossunder(src, lower)
bprice = 0.0
bprice := crossUpper ? high+syminfo.mintick : nz(bprice[1])
sprice = 0.0
sprice := crossLower ? low -syminfo.mintick : nz(sprice[1])
crossBcond = false
crossBcond := crossUpper ? true
     : na(crossBcond[1]) ? false : crossBcond[1]
crossScond = false
crossScond := crossLower ? true
     : na(crossScond[1]) ? false : crossScond[1]
cancelBcond = crossBcond and (src < ma or high >= bprice )
cancelScond = crossScond and (src > ma or low <= sprice )
if (cancelBcond)
	strategy.cancel("KltChLE")
if (crossUpper)
	strategy.entry("KltChLE", strategy.long, stop=bprice, comment="KltChLE")
if (cancelScond)
	strategy.cancel("KltChSE")
if (crossLower)
	strategy.entry("KltChSE", strategy.short, stop=sprice, comment="KltChSE")
```

> Detail

https://www.fmz.com/strategy/442941

> Last Modified

2024-02-27 15:15:07
