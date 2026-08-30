
> Name

Mean-Reversion-Strategy-Based-on-ATR
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1218162083385551378.png)

[trans]


## Overview
This strategy uses the hypothesis testing method to determine whether ATR deviates from the mean, and combines it with the prediction of price trends to implement a mean reversion trading strategy based on ATR. When ATR deviates significantly, it indicates that there may be abnormal fluctuations in the market. At this time, if the price trend is predicted to be bullish, a long position can be established.
## Strategy Principle
1. Hypothesis testing
- Perform a two-sample t test on fast ATR period (parameter atr_fast) and slow ATR period (parameter atr_slow). The null hypothesis H0 of the hypothesis test is that there is no significant difference between the means of the two samples.
- If the test statistic is higher than the threshold (the confidence interval specified by the parameter reliability_factor), the null hypothesis is rejected, that is, the fast ATR is considered to have significantly deviated from the slow ATR.
2. Price trend prediction    
- Calculate the moving average of log returns as the expected drift rate (parameter drift).    
- If the drift rate increases, it is judged that the current trend is bullish.
3. Entry and stop-loss exit
- When the difference between fast and slow ATR is significant and the trend is bullish, enter the market long.    
- Then use ATR calculation to continuously adjust the stop loss line. Stop loss and exit when the price falls below the stop loss line.
## Advantage Analysis
- Using hypothesis testing to determine ATR abnormal deviation is more scientific and parameter adaptive.
- Combined with price trend prediction, it avoids making wrong transactions based on ATR deviation alone.
- Continuously adjust stop loss to reduce the risk of loss.
## Risk Analysis
- When the price drops off a cliff, you cannot stop the loss.
- There is an error in trend judgment, and you may buy at the highest point.
- Improper parameter setting will miss the correct trading time or increase unnecessary transactions.
## Optimization suggestions
- Consider adding other indicators for multi-factor confirmation to avoid erroneous transactions caused by a single indicator.
- You can test different ATR parameter combinations to find more stable parameters.
- Increase judgment on breakthroughs of key price levels and avoid buying false breakthroughs.
## Summarize
The overall idea of ​​this strategy is clear, and it is advisable to use hypothesis testing to judge abnormal fluctuations. However, ATR deviation cannot completely judge the trend, and it is necessary to increase the basis for judgment to improve accuracy. The stop loss rule is reliable, but it cannot cope with a cliff-like decline. In the future, improvements can be made in terms of entry conditions, parameter selection, stop loss optimization, etc.
||


## Overview

This strategy uses hypothesis testing to determine if ATR deviates from its mean value. Combined with prediction of price trend, it implements a mean reversion strategy based on ATR. Significant deviation of ATR indicates potential abnormal volatility in the market. If the price trend is predicted to be bullish, a long position can be established.

## Strategy Logic

1. Hypothesis Testing

    - Conduct two-sample t-test between fast ATR period (atr_fast) and slow ATR period (atr_slow). Null hypothesis H0 is that there is no significant difference between the two sample means.

    - If test statistic exceeds threshold (confidence interval specified by reliability_factor), reject null hypothesis, i.e. fast ATR is considered to deviate significantly from slow ATR.

2. Price Trend Prediction
    
    - Moving average of logarithmic returns is calculated as expected drift rate (drift). 
    
    - If drift is increasing, current trend is judged as bullish.

3. Entry and Stop Loss Exit

    - Go long when fast and slow ATR differs significantly and trend is bullish.
    
    - Continuously adjust stop loss using ATR. Exit position when price breaks below stop loss.

## Advantage Analysis 

- Using hypothesis testing to determine ATR deviation is more scientific and adaptive.

- Combining with price trend prediction avoids wrong trades based solely on ATR deviation.  

- Adjusting stop loss continually manages downside risk.

## Risk Analysis

- Unable to stop loss when price crashes.

- Incorrect trend prediction may result in buying at the top.

- Improper parameter settings may miss correct entry or add unnecessary trades.

## Optimization Suggestions

- Consider adding other indicators for multifactor confirmation to avoid mistakes.

- Test different ATR parameter combinations to find more stable values. 

- Add criteria on breakthrough of key price levels to avoid false breakout.

## Conclusion

The overall logic of this strategy is clear. Using hypothesis testing to detect abnormal volatility is reasonable. However, ATR deviation alone is insufficient to determine trend. More confirming factors are needed to improve accuracy. The stop loss rules are reliable but ineffective against cliff-style crashes. Future improvements can be made in areas like entry criteria, parameter selection, stop loss optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(01 Apr 2000 13:30 +0000)|Backtest Start Time|
|v_input_2|14|(?Stop loss)Length of ATR for trailing stop loss|
|v_input_3|2|ATR Multiplier for trailing stop loss|
|v_input_4|14|(?Hypothesis testing)Length of ATR (fast) for diversion test|
|v_input_5|28|Length of ATR (slow) for diversion test|
|v_input_float_1|1.645|Reliability factor|
|v_input_6|14|(?Trend prediction)Length of drift|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-16 00:00:00
end: 2023-10-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © DojiEmoji

//@version=5
strategy("Mean Reversion (ATR) Strategy v2 [KL] ", overlay=true, pyramiding=1)
var string ENUM_LONG = "Long"
var string GROUP_TEST = "Hypothesis testing"
var string GROUP_TSL = "Stop loss"
var string GROUP_TREND = "Trend prediction"

backtest_timeframe_start = input(defval=timestamp("01 Apr 2000 13:30 +0000"), title="Backtest Start Time")
within_timeframe = true

// TSL: calculate the stop loss price. {
ATR_TSL      = ta.atr(input(14, title="Length of ATR for trailing stop loss", group=GROUP_TSL)) * input(2.0, title="ATR Multiplier for trailing stop loss", group=GROUP_TSL)
TSL_source      = low
TSL_line_color  = color.green
TSL_transp      = 100
var stop_loss_price = float(0)

if strategy.position_size == 0 or not within_timeframe
    TSL_line_color := color.black
    stop_loss_price := TSL_source - ATR_TSL
else if strategy.position_size > 0
    stop_loss_price := math.max(stop_loss_price, TSL_source - ATR_TSL)
    TSL_transp := 0

plot(stop_loss_price, color=color.new(TSL_line_color, TSL_transp))
// } end of "TSL" block

// Entry variables {
// ATR diversion test via Hypothesis testing (2-tailed):
//     H0 : atr_fast equals atr_slow
//     Ha : reject H0 if z_stat is above critical value, say reliability factor of 1.96 for a 95% confidence interval
len_fast    = input(14,title="Length of ATR (fast) for diversion test", group=GROUP_TEST)
atr_fast    = ta.atr(len_fast)
std_error   = ta.stdev(ta.tr, len_fast) / math.pow(len_fast, 0.5) // Standard Error (SE) = std / sq root(sample size)

atr_slow = ta.atr(input(28,title="Length of ATR (slow) for diversion test", group=GROUP_TEST))
test_stat = (atr_fast - atr_slow) / std_error
reject_H0 = math.abs(test_stat) > input.float(1.645,title="Reliability factor", tooltip="Strategy uses 2-tailed test; Confidence Interval = Point Estimate (avg ATR) +/- Reliability Factor x Standard Error; i.e use 1.645 for a 90% confidence interval", group=GROUP_TEST)

// main entry signal, subject to confirmation(s), gets passed onto the next bar
var _signal_diverted_ATR = false
if not _signal_diverted_ATR
    _signal_diverted_ATR := reject_H0


// confirmation: trend prediction; based on expected lognormal returns
_prcntge_chng = math.log(close / close[1]) 

// Expected return (drift) = average percentage change + half variance over the lookback period
len_drift = input(14, title="Length of drift", group=GROUP_TREND)
_drift = ta.sma(_prcntge_chng, len_drift) - math.pow(ta.stdev(_prcntge_chng, len_drift), 2) * 0.5
_signal_uptrend = _drift > _drift[1]

entry_signal_all = _signal_diverted_ATR and _signal_uptrend // main signal + confirmations
// } end of "Entry variables" block

// MAIN {
// Update the stop limit if strategy holds a position
if strategy.position_size > 0 and ta.change(stop_loss_price)
    strategy.exit(ENUM_LONG, comment="sl", stop=stop_loss_price)

// Entry
if within_timeframe and entry_signal_all
    strategy.entry(ENUM_LONG, strategy.long, comment=strategy.position_size > 0 ? "adding" : "initial")

// Alerts
_atr = ta.atr(14)
alert_helper(msg) =>
    prefix = "[" + syminfo.root + "] "
    suffix = "(P=" + str.tostring(close, "#.##") + "; atr=" + str.tostring(_atr, "#.##") + ")"
    alert(str.tostring(prefix) + str.tostring(msg) + str.tostring(suffix), alert.freq_once_per_bar)

if strategy.position_size > 0 and ta.change(strategy.position_size)
    if strategy.position_size > strategy.position_size[1]
        alert_helper("BUY")
    else if strategy.position_size < strategy.position_size[1]
        alert_helper("SELL")

// Clean up - set the variables back to default values once no longer in use
if strategy.position_size == 0
    stop_loss_price := float(0)
if ta.change(strategy.position_size)
    _signal_diverted_ATR := false
// } end of MAIN block
```

> Detail

https://www.fmz.com/strategy/429496

> Last Modified

2023-10-17 16:27:44
