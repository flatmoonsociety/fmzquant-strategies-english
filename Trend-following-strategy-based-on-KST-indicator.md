
> Name

Trend following strategy based on KST indicator
> Author

ChaoZhang

> Strategy Description


[trans]  

This article will introduce in detail a quantitative trading strategy that uses the KST indicator for trend tracking. This strategy determines the price trend and generates trading signals by calculating the cross relationship between the KST line and the signal line.
1. Strategy Principle
This strategy mainly forms trading signals through the following steps:
1. Calculate the values ​​of multiple ROC indicators with different periods;
2. Perform a moving average on the ROC indicators respectively, and calculate the sum to obtain the KST line;
3. Perform a moving average on the KST line again to obtain the signal line;
4. When the KST line crosses the signal line, a long signal is generated; when it crosses below the signal line, a short signal is generated.
5. You can choose the appropriate position size.
By calculating the set sum value of the ROC indicator, the KST line can reflect both the short-term and long-term price trends. Its cross relationship with the signal line can be used for trend judgment.
2. Strategic advantages
The biggest advantage of this strategy is that the indicator calculation is comprehensive and reflects trend information in different time dimensions.
Another advantage is that the indicator is simple and intuitive to use, and the Signal line is easy to judge.
Finally, the overall risk exposure of the position control strategy can be adjusted.
3. Potential risks
But this strategy also has the following problems:
First, the indicator itself has a certain lag in price changes.
Secondly, it is easy to be confused by reversal by relying only on KST indicator.
Furthermore, the workload of parameter optimization is relatively large, and over-fitting problems need to be guarded against.
4. Content summary
This article introduces in detail a quantitative trading strategy that uses the KST indicator crossover for trend tracking. This strategy can reflect price trend changes through indicators and form trading signals. However, it is also necessary to pay attention to preventing and controlling lag problems and appropriately optimizing parameters. Overall, it provides a simple method of trend following.
||


Trend Following Strategy Using KST Indicator

This article explains in detail a quantitative trend following strategy using the KST indicator. It generates trading signals by calculating the crossover between the KST line and signal line. 

I. Strategy Logic

The main steps for signal generation are:

1. Calculate values of multiple ROC indicators with different periods.

2. Apply moving averages to the ROC values separately and take the sum to derive the KST line.

3. Further smooth the KST line using moving average to get the signal line. 

4. A buy signal is generated when the KST line crosses above the signal line, and vice versa for sell signals.

5. Appropriate position sizing can be selected.

By taking the sum of multiple ROC values, the KST line reflects both short-term and long-term price trends. Its crossover with the signal line can determine trend direction.

II. Advantages of the Strategy

The biggest advantage is the comprehensive indicator calculation, which incorporates trend information across timeframes.

Another advantage is the simple and intuitive indicator usage with a clear signal line.

Lastly, adjustable position sizing helps control overall risk exposure.

III. Potential Weaknesses

However, some issues exist:

Firstly, the indicator itself has some lag in reacting to price changes.

Secondly, reliance on just the KST makes it susceptible to reversals. 

Also, extensive optimization is required to avoid overfitting.

IV. Summary

In summary, this article has explained a quantitative trend following strategy using KST crossover signals. It reflects price trends through the indicator for trade signals, but requires managing indicator lag and proper parameter tuning. Overall it provides a simple trend tracking approach.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|10|ROC Length #1|
|v_input_int_2|15|ROC Length #2|
|v_input_int_3|20|ROC Length #3|
|v_input_int_4|30|ROC Length #4|
|v_input_int_5|10|SMA Length #1|
|v_input_int_6|10|SMA Length #2|
|v_input_int_7|10|SMA Length #3|
|v_input_int_8|15|SMA Length #4|
|v_input_int_9|9|Signal Line Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-15 00:00:00
end: 2023-09-14 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// strategy(title="KST Alert", shorttitle="KST Alert", format=format.price, precision=4)
roclen1 = input.int(10, minval=1, title = "ROC Length #1")
roclen2 = input.int(15, minval=1, title = "ROC Length #2")
roclen3 = input.int(20, minval=1, title = "ROC Length #3")
roclen4 = input.int(30, minval=1, title = "ROC Length #4")
smalen1 = input.int(10, minval=1, title = "SMA Length #1")
smalen2 = input.int(10, minval=1, title = "SMA Length #2")
smalen3 = input.int(10, minval=1, title = "SMA Length #3")
smalen4 = input.int(15, minval=1, title = "SMA Length #4")
siglen = input.int(9, minval=1, title = "Signal Line Length")
smaroc(roclen, smalen) => ta.sma(ta.roc(close, roclen), smalen)
kst = smaroc(roclen1, smalen1) + 2 * smaroc(roclen2, smalen2) + 3 * smaroc(roclen3, smalen3) + 4 * smaroc(roclen4, smalen4)
sig = ta.sma(kst, siglen)
plot(kst, color=#009688, title="KST")
plot(sig, color=#F44336, title="Signal")
hline(0, title="Zero", color = #787B86)
eL1=ta.crossover(kst,sig)
eS1=ta.crossunder(kst,sig)
ch = 0
t = year(time('D'))
ch := ta.change(t) != 0 ? 1 : 0
T1 = time(timeframe.period, "0915-1520")
session_open = na(t) ? false : true
newDay = ta.change(time("15m")) != 0
strategy.entry("Long1", strategy.long, when = eL1)
strategy.entry("Short1", strategy.short, when = eS1)

```

> Detail

https://www.fmz.com/strategy/426891

> Last Modified

2023-09-15 12:05:21
