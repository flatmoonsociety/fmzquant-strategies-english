
> Name

Quantitative-Trading-Strategy-Based-on-Voss-Filter-and-Trend-Indicator
> Author

ChaoZhang

> Strategy Description

[trans]
## Overview
This strategy comprehensively uses the Voss prediction filter and the Ehlers instantaneous trend line indicator to identify market cyclical turning points and achieve quantitative trading. The Voss filter can send out buy/sell signals in advance, while the instantaneous trend line indicator is used to determine the overall trend direction, reducing the misleading of the Voss filter in trending markets. This strategy can be used for cyclical products such as Bitcoin, and it performs well in backtesting.
## Strategy Principle
### Voss prediction filter
The Voss prediction filter comes from John F. Ehlers' article "A Peek Into The Future". The calculation formula of this filter is as follows:
```pine
_filt = 0.5 * _s3 * _x1 + _f1 * _s2 * _filt[1] - _s1 * _filt[2]
_voss = _x2 * _filt - _sumC
```

Among them, _x1 is the first-order difference of the price; _x2 is the smoothing factor; _s1, _s2, _s3 are filtering parameters; _f1 is the period parameter; _filt is the filtering result; _voss is the final output.
This filter can be thought of as a smoothing filter that emphasizes information from the current and past periods, thereby issuing buy/sell signals in advance. Due to the inherent group delays, it is like "looking into the future" and can send out predictive signals before other indicators.
### Instantaneous Trendline Indicator
The Instantaneous Trendline indicator is calculated by the following formula:
```pine 
_it = (_a-((_a*_a)/4.0))*_src+0.5*_a*_a*_src[1]-(_a-0.75*_a*_a)*_src[2]+2*(1-_a)*nz(_it[1])+-(1-_a)*(1-_a)*nz(_it[2])
```

This indicator draws a trend line that is most consistent with the price in real time, and can accurately determine the direction and strength of the trend.
### Strategy logic
A buy signal is generated when Voss turns from negative to positive and crosses the filter result.
A sell signal is generated when Voss turns from positive to negative and crosses below the filter result.
At the same time, a trading signal will only be issued when the instantaneous trendline indicator confirms the direction of the trend. This filters out false signals that the Voss filter may send out in trending markets.
## Strategic Advantages
- Voss filter can send out predictive signals in advance and capture periodic reversal points
- The instantaneous trend line indicator can accurately determine the trend direction and avoid false signals sent out in advance by the filter.
- Configurable parameters for optimization, suitable for different cycles and market environments
- Stop loss strategies can be added to control risks
## Strategic risks and solutions
- This strategy relies on filters to send signals in advance and may skip some trend markets
- In a strong trend, counterproductive trading signals may be generated, resulting in losses
Risks can be reduced by:
- Optimize cycle parameters to match the periodicity of different varieties
- Adjust bandwidth parameters, reduce filtering intensity, and reduce misleading signals
- Add trend filtering to avoid false signals under strong trends
-Set stop loss strategy to control single loss
## Strategy optimization direction
This strategy can be optimized from the following aspects:
- Try different price sources, such as closing price, moving average, etc., to get better input
- Adjust the filter period parameters to match the periodicity of specific varieties
- Optimize trend indicator parameters to obtain more accurate trend judgments
- Try different trend indicators to find a more suitable combination
- Add stop loss and trailing stop strategies to better control risks
- Carry out parameter optimization and find the best parameter combination
## Summarize
This strategy combines the Voss filter and trend indicators to effectively identify cyclical reversal points in the market. By optimizing parameters and controlling risks, this strategy can achieve a stable quantitative trading system. It can be widely used in varieties with obvious periodicity and has shown good trading results in backtesting. Overall, this strategy has unique predictive capabilities and can be optimized in many aspects, so it has broad application prospects.
||

## Overview

This strategy combines the Voss Predictive Filter and Ehlers Instantaneous Trendline indicator to identify cyclical turning points in the market for quantitative trading. The Voss filter provides early buy/sell signals, while the trendline indicator determines the overall trend direction to avoid misleads from the Voss filter in trending markets. This strategy works well on instruments like Bitcoin that exhibit cyclical patterns, as evidenced by good backtest results.

## Strategy Logic

### Voss Predictive Filter 

The Voss filter comes from John F. Ehlers' article "A Peek Into The Future". Its calculation is as follows:

```pine
_filt = 0.5 * _s3 * _x1 + _f1 * _s2 * _filt[1] - _s1 * _filt[2] 
_voss = _x2 * _filt - _sumC
```

Where _x1 is the 1st order price difference; _x2 is a smoothing factor; _s1, _s2, _s3 are filter parameters; _f1 is the cycle parameter; _filt is the filter output; _voss is the final output.

The filter can be seen as a smoothed filter that emphasizes current and past cycle information to generate early signals. Due to inherent group delays, it "looks into the future" to produce predictive signals ahead of other indicators.

### Instantaneous Trendline Indicator

The trendline indicator is calculated as:

```pine
_it = (_a-((_a*_a)/4.0))*_src+0.5*_a*_a*_src[1]-(_a-0.75*_a*_a)*_src[2]+2*(1-_a)*nz(_it[1])+-(1-_a)*(1-_a)*nz(_it[2]) 
```

It plots a trendline in real-time that closely fits the price action, accurately determining trend direction and strength.

### Strategy Logic

A buy signal is generated when the Voss crosses up through the filter result. 

A sell signal is generated when the Voss crosses down through the filter result.

Trading signals are only accepted if confirmed by the trendline indicator. This avoids wrong signals from the Voss filter in trending markets.

## Advantages

- Voss filter provides early predictive signals to catch cyclical turns  
- Trendline indicator accurately determines trend direction, avoiding wrong signals
- Parameters can be optimized for different cycles and market environments
- Stops can be added to control risk

## Risks and Mitigation

- Strategy relies on early signals, potentially missing some trends
- Counter-trend signals may occur in strong trends, causing losses

Risks can be reduced by:

- Optimizing period parameter for instrument cycles
- Reducing filter bandwidth to decrease false signals 
- Adding trend filters to avoid signals against strong trends  
- Using stops to control loss per trade

## Enhancement Opportunities

The strategy can be improved by:

- Trying different price sources like close, moving averages etc. 
- Adjusting filter period for specific instrument cycles
- Optimizing trend indicator parameters for better trend detection
- Trying different trend indicators for better combinations
- Adding stops, trailing stops for better risk control
- Parameter optimization for best parameter sets

## Conclusion

This strategy combines the Voss filter and trend indicator to effectively identify cyclical turns in the market. With optimized parameters and risk controls, it can produce a robust quantitative trading system. It is widely applicable to instruments exhibiting cyclical patterns, as evidenced by good backtest results. Overall, the strategy has unique predictive capabilities, and broad potential for enhancement through multi-dimensional optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|20|period|
|v_input_3|4|predict|
|v_input_4|0.25|bandwidth|
|v_input_5_hl2|0|Source IT: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_6|0.07|Alpha|
|v_input_7|false|Fill Trend Region|
|v_input_8|false|Enable barcolors|
|v_input_9|false|Hide Ribbon|
|v_input_10|true|Custom Backtesting Dates|
|v_input_11|2019|Backtest Start Year|
|v_input_12|true|Backtest Start Month|
|v_input_13|true|Backtest Start Day|
|v_input_14|false|Backtest Start Hour|
|v_input_15|2020|Backtest Stop Year|
|v_input_16|2|Backtest Stop Month|
|v_input_17|29|Backtest Stop Day|
|v_input_18|false|Backtest Stop Hour|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// A Peek Into the Future
// John F. Ehlers
// TASC Aug 2019

// Created by e2e4mfck for tradingview.com
// Modified by © Bitduke

//@version=4
//strategy("Voss Strategy (Filter + IT)", overlay=false, calc_on_every_tick=false,pyramiding=0, default_qty_type=strategy.cash,default_qty_value=1000, currency=currency.USD, initial_capital=1000,commission_type=strategy.commission.percent, commission_value=0.075)

// voss filter

source = input(close, type = input.source)
period = input(20, type = input.integer)
predict = input(4, type = input.integer)
bandwidth = input(0.25, type = input.float)

// it trendline

src = input(hl2, title="Source IT")
a = input(0.07, title="Alpha", step=0.01) 
fr = input(false, title="Fill Trend Region")
ebc = input(false, title="Enable barcolors")
hr = input(false, title="Hide Ribbon")


voss_filter (_period, _predict, _bandwidth, _source) =>
	float _filt = 0, float _sumC = 0, float _voss = 0
	_PI		= 2 * asin(1)
	_order	= 3 * _predict
	_f1		= cos(2 * _PI / _period)
	_g1		= cos(_bandwidth * 2 * _PI / _period)
	_s1		= 1 / _g1 - sqrt(1 / (_g1 * _g1) - 1)
	_s2		= 1 + _s1
	_s3		= 1 - _s1
	_x1		= _source - _source[2]
	_x2		= (3 + _order) / 2

	for _i = 0 to (_order - 1)
		_sumC := _sumC + ((_i + 1) / _order) * _voss[_order - _i]

	if bar_index <= _order
		_filt := 0		
		_voss := 0		
	else			
		_filt := 0.5 * _s3 * _x1 + _f1 * _s2 * _filt[1] - _s1 * _filt[2]
		_voss := _x2 * _filt - _sumC

	[_voss, _filt]


[Voss, Filt] = voss_filter(period, predict, bandwidth, source)


instantaneous_trendline (_src, _a, _freq, _ebc, _hr) =>
    _it = 0.0
    _it := (_a-((_a*_a)/4.0))*_src+0.5*_a*_a*_src[1]-(_a-0.75*_a*_a)*_src[2]+2*(1-_a )*nz(_it[1], ((_src+2*_src[1]+_src[2])/4.0))-(1-_a)*(1-_a)*nz(_it[2], ((_src+2*_src[1]+_src[2])/4.0))
    _lag = 2.0*_it-nz(_it[2])
    
    [_it, _lag]

[it, lag] = instantaneous_trendline(src, a, fr, ebc, hr)

// - - - - -  - - - - - //

plot(Filt, title = "Filter", style = plot.style_line, color = color.red, linewidth = 2)
plot(Voss, title = "Voss", style = plot.style_line, color = color.blue,	linewidth = 2)
hline(0.0, title = "Zero", linestyle = hline.style_dashed, color = color.black,	linewidth = 1)
plot(hr? na:it, title="IT Trend", color= fr? color.gray : color.red, linewidth=1)
plot(hr? na:lag, title="IT Trigger", color=fr? color.gray : color.blue, linewidth=1)


// Strategy Logic
longCondition =  lag < it  and crossover(Voss,Filt) 
shortCondition = it > lag and crossover(Filt,Voss) 

strategy.entry("Voss_Short", strategy.short, when=shortCondition)
strategy.entry("Voss_Long", strategy.long, when=longCondition)


// === Backtesting Dates === thanks to Trost

testPeriodSwitch = input(true, "Custom Backtesting Dates")
testStartYear = input(2019, "Backtest Start Year")
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testStartHour = input(0, "Backtest Start Hour")
testPeriodStart = timestamp(testStartYear, testStartMonth, testStartDay, testStartHour, 0)
testStopYear = input(2020, "Backtest Stop Year")
testStopMonth = input(2, "Backtest Stop Month")
testStopDay = input(29, "Backtest Stop Day")
testStopHour = input(0, "Backtest Stop Hour")
testPeriodStop = timestamp(testStopYear, testStopMonth, testStopDay, testStopHour, 0)
testPeriod() =>
    time >= testPeriodStart and time <= testPeriodStop ? true : false
testPeriod_1 = testPeriod()
isPeriod = true
// === /END

if not isPeriod
    strategy.cancel_all()
    strategy.close_all()

```

> Detail

https://www.fmz.com/strategy/427275

> Last Modified

2023-09-19 16:59:10
