
> Name

ALMA moving average crossover strategyALMA-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy uses two fast and slow Arnaud Legoux moving averages (ALMA) to judge trading signals. ALMA is an improvement over the traditional moving average that reduces lag and smoothes the curve. The strategy uses the fast ALMA to cross above the slow ALMA to generate a buy signal, and the fast ALMA to cross below the slow ALMA to generate a sell signal. At the same time, it is combined with volume filtering to form a more stable cross signal.
### Strategy Principles
The core indicators and trading rules of this strategy are as follows:
1. Fast ALMA: The period is shorter and used to capture breakthroughs.
2. Slow ALMA: has a longer period and is used to determine the general trend.
3. Trading volume filter: effective when the short-term average exceeds the long-term average.
4. Long signal: the fast ALMA crosses the slow ALMA and the volume filtering is effective.
5. Long-term signal: Fast ALMA crosses below slow ALMA.
6. Short signal: Fast ALMA crosses below slow ALMA and volume filtering is effective.
7. Flat signal: fast ALMA crosses above slow ALMA.
This strategy is simple and intuitive, and it integrates a variety of technical indicators such as trend judgment, breakthrough capture, and trading volume verification to form a relatively stable trading system. The combination of fast and slow moving averages can effectively determine the trend direction; the use of the ALMA algorithm reduces the impact of lag on trading; the addition of trading volume avoids many uncertain false breakthroughs.
### Advantage Analysis
Compared with the traditional moving average crossover strategy, this strategy mainly has the following advantages:
1. ALMA algorithm can reduce lag and improve signal quality.
2. Volume filtering can avoid losses caused by false breakthroughs.
3. Use fast and slow moving averages to determine the general trend and avoid reverse trading.
4. The rules are simple and intuitive, easy to understand and implement.
5. The moving average parameters can be flexibly adjusted and suitable for different markets.
6. The fund management settings are reasonable and single losses can be controlled.
7. The strategy effect can be further improved by optimizing the moving average parameters.
8. Generally speaking, compared with the traditional equal intersection strategy, the stability and signal quality of this strategy are improved.
### Risk Analysis
Although this strategy has many advantages, the following risks should be noted:
1. The moving average strategy is inherently susceptible to market shocks and chaos, resulting in multiple losses.
2. The parameter settings of the ALMA algorithm will affect the strategy effect.
3. The volume amplification effect may mislead the judgment of trading signals.
4. There is a certain lag and losses cannot be completely avoided.
5. Parametrics optimization has the risk of overfitting.
6. The signal will be invalid when the trading volume is abnormal.
7. Algorithms such as machine learning may achieve better results.
8. Pay attention to the earnings drawdown ratio indicator to avoid the curve being too jagged.
### Optimization direction
Taking into account the above risk factors, this strategy can be optimized from the following aspects:
1. Optimize ALMA moving average parameters and improve response sensitivity.
2. Try different ways of calculating volume.
3. Introduce stop-loss strategies and strictly control single losses.
4. Combine with other indicators to build a three-dimensional trading signal system.
5. Add a machine learning module to achieve more intelligent signal adjustment.
6. Deploy multiple varieties and disperse strategies.
7. Optimize fund management strategies and adjust positions according to different markets.
8. Study the robustness of the strategy to prevent overfitting.
### Summarize
Overall, this strategy improves the signal quality and stability through the ALMA algorithm and trading volume verification compared to the traditional moving average crossover strategy. However, trading strategy optimization is a continuous process, and it is still necessary to pay attention to risks and enhance the strategy from multiple dimensions so that it can adapt to more complex market environments.
||

### Overview

This strategy uses two Arnaud Legoux Moving Averages (ALMA), one fast and one slow, to generate crossover signals. ALMA reduces lag and smooths the signal line compared to traditional MAs. Volume filter is added to improve signal accuracy. It is optimized for crypto but can be adjusted for other instruments. Alerts are included.

### Strategy Logic

The core indicators and rules are:

1. Fast ALMA: Shorter period to catch breakouts. 

2. Slow ALMA: Longer period to gauge the trend.

3. Volume filter: Valid when short EMA crosses above long EMA.

4. Buy signal: Fast ALMA crosses above slow ALMA and volume filter passes.

5. Sell signal: Fast ALMA crosses below slow ALMA.

6. Short signal: Fast ALMA crosses below slow ALMA and volume filter passes.

7. Cover signal: Fast ALMA crosses above slow ALMA.

The strategy combines trend, momentum and volume analysis for robust signals. ALMA reduces lagging while volume avoids false breakouts.

### Advantages

Compared to traditional moving average strategies, the main advantages are:

1. ALMA reduces lag and improves signal quality.

2. Volume filter avoids losses from false breakouts.

3. Fast/slow combo gauges the trend direction. 

4. Simple and intuitive rules, easy to implement.

5. Flexible tuning of MA parameters for different markets.

6. Reasonable risk management.

7. Further optimization potential through parameter tuning.

8. Overall improved stability and quality over traditional crossover strategies.

### Risks

Despite the merits, the following risks should be noted:

1. Crossover systems are intrinsically vulnerable to whipsaws.

2. ALMA performance depends on parameter tuning.

3. Volume spikes may mislead signal generation. 

4. Some lag always exists, cannot avoid all losses.

5. Overfitting risk from excessive optimization.

6. Signals fail when volume is abnormal. 

7. Machine learning techniques may generate better results.

8. Monitor reward/risk ratio to avoid excessive drawdowns.

### Enhancement

To address the risks, enhancements can be made in the following areas:

1. Optimize ALMA parameters for better sensitivity.

2. Experiment with different volume metrics. 

3. Introduce stop loss to control loss per trade.

4. Incorporate other indicators for robust signals.

5. Add machine learning module for smarter signal adjustment.

6. Deploy across multiple products for strategy diversification. 

7. Optimize position sizing models for different markets.

8. Research robustness to prevent overfitting. 

### Conclusion

In conclusion, compared to traditional crossover strategies, this strategy improves signal quality and robustness through the ALMA algorithm and volume filter. But strategy optimization is an iterative process. It is important to keep improving the strategy from multiple dimensions to adapt to changing markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long Entry|
|v_input_2|true|Short Entry|
|v_input_float_1|0.85|Arnaud Legoux (ALMA) - Offset Value|
|v_input_int_1|6|Arnaud Legoux (ALMA) - Sigma Value|
|v_input_float_2|0.85|Arnaud Legoux (ALMA) - Offset Value|
|v_input_int_2|6|Arnaud Legoux (ALMA) - Sigma Value|
|v_input_int_4|10|Long Length|
|v_input_float_4|2|Short Take Profit|
|v_input_float_6|2.5|Short Stop Loss|
|v_input_3|100|(?ALMA Fast Length Settings)ALMA Lenghth 1|
|v_input_4|120|(?ALMA Slow Length Settings)ALMA Length 2|
|v_input_int_3|5|(?Volume Settings)Short Length|
|v_input_float_3|2|(?Take Profit Percentage)Long Take Profit|
|v_input_float_5|2.5|(?Stop Percentage)Long Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-16 00:00:00
end: 2023-09-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Sarahann999
// Calculations for TP/SL based off: https://kodify.net/tradingview/orders/percentage-profit/
//@version=5
strategy("ALMA Cross", overlay=true)

//User Inputs
src= (close)
long_entry = input(true, title='Long Entry')
short_entry = input(true, title='Short Entry')

//Fast Settings
ALMA1 = input(100, "ALMA Lenghth 1", group= "ALMA Fast Length Settings")
alma_offset = input.float(defval=0.85, title='Arnaud Legoux (ALMA) - Offset Value', minval=0, step=0.01)
alma_sigma = input.int(defval=6, title='Arnaud Legoux (ALMA) - Sigma Value', minval=0)
Alma1 = ta.alma(src, ALMA1, alma_offset, alma_sigma)

//Slow Settings
ALMA2 = input(120, "ALMA Length 2", group = "ALMA Slow Length Settings")
alma_offset2 = input.float(defval=0.85, title='Arnaud Legoux (ALMA) - Offset Value', minval=0, step=0.01)
alma_sigma2 = input.int(defval=6, title='Arnaud Legoux (ALMA) - Sigma Value', minval=0)
Alma2 = ta.alma(src, ALMA2, alma_offset2, alma_sigma2)

//Volume
var cumVol = 0.
cumVol += nz(volume)
if barstate.islast and cumVol == 0
    runtime.error("No volume is provided by the data vendor.")
shortlen = input.int(5, minval=1, title = "Short Length", group= "Volume Settings")
longlen = input.int(10, minval=1, title = "Long Length")
short = ta.ema(volume, shortlen)
long = ta.ema(volume, longlen)
osc = 100 * (short - long) / long

//Define Cross Conditions
buy = ta.crossover(Alma1, Alma2)
sell = ta.crossunder(Alma1, Alma2)

//Calculate Take Profit Percentage
longProfitPerc = input.float(title="Long Take Profit", group='Take Profit Percentage',
     minval=0.0, step=0.1, defval=2) / 100
shortProfitPerc = input.float(title="Short Take Profit",
     minval=0.0, step=0.1, defval=2) / 100
     
// Figure out take profit price 1
longExitPrice  = strategy.position_avg_price * (1 + longProfitPerc)
shortExitPrice = strategy.position_avg_price * (1 - shortProfitPerc)

// Make inputs that set the stop %  1
longStopPerc = input.float(title="Long Stop Loss", group='Stop Percentage',
     minval=0.0, step=0.1, defval=2.5) / 100
shortStopPerc = input.float(title="Short Stop Loss",
     minval=0.0, step=0.1, defval=2.5) / 100

// Figure Out Stop Price
longStopPrice  = strategy.position_avg_price * (1 - longStopPerc)
shortStopPrice = strategy.position_avg_price * (1 + shortStopPerc)

//Define Conditions
buySignal = buy and osc > 0
     and strategy.position_size == 0

//sellSignal 
sellSignal = sell and osc > 0
     and strategy.position_size == 0

// Submit entry orders
if buySignal and long_entry
    strategy.entry(id="Long", direction=strategy.long, alert_message="Enter Long")
    alert(message="BUY Trade Entry Alert", freq=alert.freq_once_per_bar)
    
if sellSignal and short_entry
    strategy.entry(id="Short", direction=strategy.short, alert_message="Enter Short")
    alert(message="SELL Trade Entry Alert", freq=alert.freq_once_per_bar)
    
// Submit exit orders based on take profit price
if (strategy.position_size > 0)
    strategy.exit(id="Long TP/SL", limit=longExitPrice, stop=longStopPrice, alert_message="Long Exit 1 at {{close}}")
if (strategy.position_size < 0)
    strategy.exit(id="Short TP/SL", limit=shortExitPrice, stop=shortStopPrice, alert_message="Short Exit 1 at {{close}}")

//Draw
plot(Alma1,"Alma Fast", color=color.purple, style=plot.style_circles)
plot(Alma2,"Alma Slow", color=#acb5c2, style=plot.style_circles)
```

> Detail

https://www.fmz.com/strategy/427669

> Last Modified

2023-09-23 15:11:02
