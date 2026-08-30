
> Name

Multi-Indicator-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


### Overview
This strategy judges the general trend by integrating multiple indicators and generates trading decisions based on the same direction changes in the indicator combination signals. The strategy integrates moving average speed, STOCH indicator and MACD indicator to form a more comprehensive and robust trend tracking mechanism.
### Strategy Principles
This strategy is mainly based on the following indicators for trend judgment:
1. Moving average speed: a trend indicator that reflects the speed of price changes.
2. STOCH indicator: Determine Trend turning in overbought and oversold areas.
3. MACD indicator: The difference between the two moving averages reflects the trend change.
The specific trading rules are as follows:
1. The moving average speed is upward, giving a bullish signal.
2. The STOCH indicator enters the oversold area, giving a bearish signal.
3. The MACD moving average crosses in the positive direction, giving a bullish signal.
4. When any two indicator signals are in the same direction, make corresponding entry decisions.
5. If the indicator signal changes, close the position and leave the market.
This strategy comprehensively considers multiple factors of the trend, filters out misleading factors through combined signals, and forms a stable trading system with strong confirmation power.
### Advantage Analysis
Compared with a single indicator, this combination strategy has the following advantages:
1. Comprehensive judgment improves accuracy.
2. Combination filtering reduces erroneous transactions.
3. Combine trend and reversal indicators to provide a comprehensive perspective.
4. Signals in the same direction have strong confirmation power and can avoid false breakthroughs.
5. The rules are simple, clear and easy to implement.
6. Flexible parameter adjustment and strong adaptability.
7. Universal for different time periods and wide range of use.
8. Machine learning training indicator weights can be introduced.
9. Overall stability and profitability are better than a single indicator.
### Risk Analysis
Although this strategy has several advantages, the following risks need to be considered:
1. Multiple indicators increase the complexity of the strategy.
2. Parameter optimization and weight setting are difficult.
3. There may be conflicting signals between different indicators.
4. Some indicators have a lag in giving, and losses cannot be completely avoided.
5. The unilateral holding time is uncertain and there is an element of luck.
6. Combining signals does not eliminate the monitoring inherent in trend trading.
7. High transaction frequency is susceptible to transaction fees.
8. Pay attention to the earnings drawdown ratio indicator.
### Optimization direction
Based on the above analysis, the strategy can be improved as follows:
1. Evaluate the effectiveness of different indicators in different markets.
2. Add parameter robustness check to prevent over-optimization.
3. Optimize indicator weight settings to reduce signal conflicts.
4. Set stop loss and stop profit to avoid serious losses.
5. Use time exits to control unilateral non-target positions.
6. Evaluate the impact of transaction frequency on transaction fees.
7. Introduce risk indicator constraints.
8. Test multi-market robustness.
9. Continuously verify strategies to prevent obsolescence and failure.
### Summarize
This strategy determines the trend by integrating multiples indicators to form a stable combined signal system. However, any strategy needs to be continuously optimized and improved, paying attention to risk indicators and preventing overfitting. Quantitative trading is a process of continuous learning and iteration.
||

### Overview 

This strategy integrates multiple indicators for trend identification, and generates trading signals based on aligned directional changes. It combines moving average speed, STOCH and MACD to form a comprehensive and robust trend following system.

### Strategy Logic

The core indicators are:

1. Moving average speed: Reflects price momentum. 

2. STOCH: Oversold/overbought for trend changes.

3. MACD: Trend changes from dual moving averages. 

The trading rules are:

1. Rising moving average speed gives bullish signal.

2. STOCH in overbought zone gives bearish signal.

3. MACD positive crossover gives bullish signal. 

4. Enter when any 2 indicators align signals.

5. Exit when indicator signals change.

The combination evaluates trend from multiple dimensions, filtering noise for high-conviction signals.

### Advantages

Compared to single indicators, the combo strategy has the following pros:

1. Combined view improves accuracy. 

2. Ensemble filtering reduces false signals.

3. Incorporates trend and mean-reversion indicators.

4. Aligned signals have high conviction, avoiding false breakouts.

5. Simple and clear rules, easy to implement. 

6. Flexible parameter tuning, robustness.  

7. Applicable to different timeframes.

8. Can train indicator weights with machine learning.

9. Overall better stability and profitability than single indicators.

### Risks

Despite the merits, risks to consider include:

1. Increased complexity with multiple indicators.

2. Challenging parameter optimization and weighting.

3. Conflicting indicator signals may occur. 

4. Some lag always exists, cannot avoid all losses.

5. Uncertain unidirectional holding period with luck factor.

6. Ensemble signals cannot eliminate inherent trend trading risks.

7. High trade frequency increases transaction costs.

8. Need to monitor reward/risk ratios.

### Enhancements

Based on the analysis, enhancements may involve:

1. Evaluate indicator efficacy across different markets. 

2. Add parameter robustness checks to prevent overfitting.

3. Optimize indicator weighting to reduce conflicts.

4. Implement stops to limit severe losses.

5. Use time exits to control unlimited holding periods.

6. Assess trading frequency impact on transaction costs.

7. Incorporate risk metrics constraints. 

8. Test robustness across multiple markets. 

9. Continually validate strategy efficacy.

### Conclusion

This strategy forms stable ensemble signals by integrating multiple indicators for trend assessment. But continual optimization is key for any strategy, monitoring risks and preventing overfitting. Quant trading is a continuous learning process.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|50|(?MA Speed)Avg Length|
|v_input_int_2|true|Rate of Change Length|
|v_input_int_3|10|Avg Rate of Change Length|
|v_input_int_4|14|(?Stochastic)Stochastic Length|
|v_input_int_5|3|Stochastic Smooth K|
|v_input_float_1|80|Stochastic Overbought|
|v_input_float_2|20|Stochastic Oversold|
|v_input_2|12|(?MACD)Fast Length|
|v_input_3|26|Slow Length|
|v_input_int_6|9|MACD Avg Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-16 00:00:00
end: 2023-09-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// By TradeStation
//@version=5

strategy("Mov Avg Speed Strategy", overlay=true)

src = input(close, title="Source")

// MA Speed  
avg_len = input.int(50, minval=1, title="Avg Length", group="MA Speed")
roc_len = input.int(1, minval=1, title="Rate of Change Length", group="MA Speed")
avg_roc_len = input.int(10, minval=1, title="Avg Rate of Change Length", group="MA Speed")

// Stochastic
stoch_len = input.int(14, minval=1, title="Stochastic Length", group="Stochastic")
smooth_k = input.int(3, minval=1, title="Stochastic Smooth K", group="Stochastic")
overbought = input.float(80, title="Stochastic Overbought", group="Stochastic")
oversold = input.float(20, title="Stochastic Oversold", group="Stochastic")

// MACD
fast_length = input(12, title="Fast Length", group="MACD")
slow_length = input(26, title="Slow Length", group="MACD")
macd_avg_length = input.int(9, title="MACD Avg Length",  minval=1, group="MACD")

// MA Speed
avg = ta.sma(src, avg_len)
roc = ta.roc(avg, roc_len)
avg_roc = ta.sma(roc, avg_roc_len)
avg_roc_signal = avg_roc > 0 ? 1 : avg_roc < 0 ? -1 : 0 

// Stochastic k
k = ta.sma(ta.stoch(close, high, low, stoch_len), smooth_k)
stochastic_signal = k <= oversold ? 1 : k >= overbought ? -1 : 0

// MACD
fast_ma = ta.ema(src, fast_length)
slow_ma = ta.ema(src, slow_length)
macd = fast_ma - slow_ma
macd_avg = ta.ema(macd, macd_avg_length)
macd_signal = macd_avg > macd_avg[1] ? 1 : macd_avg < macd_avg[1] ? -1 : 0

// set the signal couint
long_count = 0
short_count = 0

if macd_signal == 1
    long_count += 1

else if macd_signal == -1
    short_count += 1
 
if stochastic_signal == 1
    long_count += 1

else if stochastic_signal == -1
    short_count += 1
 
if avg_roc_signal == 1
    long_count += 1

else if avg_roc_signal == -1
    short_count += 1

if (long_count >= 2)
    strategy.entry("Long", strategy.long)

if (short_count >= 2)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/427671

> Last Modified

2023-09-23 15:19:46
