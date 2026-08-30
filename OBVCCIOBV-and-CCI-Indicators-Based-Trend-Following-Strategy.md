
> Name

Trend following strategy based on OBV and CCI indicatorsOBV-and-CCI-Indicators-Based-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1c2e593d0089bc483b5.png)
[trans]
### Overview
This strategy is a trend following strategy based on the OBV and CCI indicators. It determines market trends and capital flows through the OBV indicator, and then uses the CCI indicator to filter and generate trading signals. When both OBV and CCI indicators confirm that the current trend is up, go long; when both OBV and CCI indicators confirm that the current trend is down, go short.
### Strategy Principles
This strategy mainly relies on two indicators: OBV and CCI. The OBV indicator can reflect the market's capital flow. When the OBV is green, it means that the current trend is capital inflow; when the OBV is red, it means the current trend is capital outflow. The CCI indicator is used to filter and set a threshold. When CCI is above the threshold, it is considered a long market, and when CCI is below the threshold, it is considered a short market.
In terms of entry signal judgment, if the OBV value in the previous period is green (capital inflow) and the CCI is higher than the threshold (belonging to a long market), and at the same time the OBV line crosses its EMA moving average, a buy signal is generated.
In judging the closing signal, if the OBV value in the previous period is red (capital outflow) and the CCI is lower than the threshold (a short market), and at the same time the OBV line crosses its EMA moving average, a sell signal is generated.
In this way, the general direction is judged through OBV, and the CCI indicator is used for filtering. The two are combined with the golden cross of the moving average to generate specific trading signals, realizing trend tracking.
### Advantage Analysis
This strategy mainly has the following advantages:
1. Use OBV to determine market capital flow and trend direction to avoid being disturbed by short-term market noise;
2. Use the CCI indicator for filtering to make trading signals more reliable;
3. Use EMA moving average golden cross and dead cross to generate specific trading signal points, which are of higher quality;
4. The rules are clear and simple, easy to understand and implement.
### Risk Analysis
There are also some potential risks with this strategy:
1. The possibility of OBV and CCI indicators sending wrong signals;
2. Frequent trading signals and easy over-trading;
3. You may get stuck during the correction;
4. Improper parameter settings lead to poor strategy effects.
These risks can be controlled and optimized by optimizing parameters, adjusting trading frequency, setting stop losses, and using filters.
### Optimization direction
This strategy can be optimized from the following directions:
1. Evaluate the impact of different parameters on the strategy effect and find the optimal parameter combination;
2. Set trading frequency limits to avoid excessive trading;
3. Add a stop-loss mechanism to control single losses;
4. Add other indicator filters to improve signal quality;
5. Optimize entry and exit logic to make trading signals more reliable.
### Summarize
Overall, this strategy is a basic strategy that can effectively track price trends and avoid noise interference. However, there are also certain risks, which need to be improved through parameter optimization, stop loss setting, and transaction frequency control. If the parameters are selected scientifically, the backtesting effect can be significantly improved. This strategy is suitable for higher-level quantitative traders to learn and practice.
||

### Overview  

This strategy is a trend following strategy based on OBV and CCI indicators. It uses OBV indicator to judge market trend and capital flow, and then uses CCI indicator for filtering to generate trading signals. When both OBV and CCI indicators confirm the current uptrend, go long; when both indicators confirm the current downtrend, go short.

### Strategy Logic  

The strategy mainly relies on OBV and CCI two indicators. OBV indicator can reflect the capital flow in the market. When OBV is green, it means the current trend is capital inflow; when OBV is red, it means the current trend is capital outflow. The CCI indicator is used as a filter. By setting a threshold, when CCI is above threshold, it is considered a bull market; when CCI is below threshold, it is considered a bear market.

For entry signals, if last period OBV value is green (capital inflow) and CCI is above threshold (in a bull market), meanwhile OBV line crosses above its EMA line, a buy signal is generated.  

For exit signals, if last period OBV value is red (capital outflow) and CCI is below threshold (in a bear market), meanwhile OBV line crosses below its EMA line, a sell signal is generated.

So by judging the major trend using OBV, filtering with CCI indicator, and combining them using EMA crossovers to generate concrete trading signals, the strategy realizes trend following.  

### Advantage Analysis

The main advantages of this strategy are:

1. Using OBV to determine market capital flow and trend direction, avoiding short-term market noise interference;

2. Leveraging CCI indicator for filtering, making trading signals more reliable;  

3. Using EMA crossovers to generate high quality concrete trading points;

4. The rules are clear and simple, easy to understand and implement.

### Risk Analysis   

There are also some potential risks for this strategy:  

1. Possibility of OBV and CCI indicators generating wrong signals;

2. Frequent trading signals, easy to overtrade;

3. May be trapped during retracements;  

4. Poor parameter tuning leading to bad strategy performance.

To control these risks, methods like parameter optimization, adjusting trading frequency, setting stop loss and using filters can be applied.

### Optimization Directions   

The strategy can be optimized from the following aspects:

1. Evaluate the impact of different parameters and find the optimal parameter combination;  

2. Set trading frequency limit to avoid over trading;

3. Add stop loss mechanism to control single trade loss;

4. Add other indicators as filters to improve signal quality;

5. Optimize entry and exit logic to make trading signals more reliable.  

### Summary

In summary, this is a basic trend following strategy that can effectively track price trends and avoid noise interference. But there are still some risks, requiring improvements like parameter optimization, stop loss, trading frequency control etc. If parameters are set scientifically, significant backtest performance improvement can be achieved. The strategy suits more advanced quant traders for learning and practicing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|CCI Length|
|v_input_2|false|CCI threshold for OBV coding|
|v_input_3|13|EMA length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-14 00:00:00
end: 2024-02-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//author: SudeepBisht
//@version=3
strategy("SB_CCI coded OBV Strategy", overlay=true)

src = close
length = input(20, minval=1, title="CCI Length")
threshold=input(0, title="CCI threshold for OBV coding")
lengthema=input(13, title="EMA length")
obv(src) => 
    cum(change(src) > 0 ? volume : change(src) < 0 ? -volume : 0*volume)
    
o=obv(src)
c=cci(src, length)
col=c>=threshold?green:red
chk=col==green?1:0
ema_line=ema(o,lengthema)

//plot(o, color=c>=threshold?green:red, title="OBV_CCI coded", linewidth=2)
//plot(ema(o,lengthema), color=orange, linewidth=2)


if (not na(ema_line))
    if (crossover(o, ema_line) and chk[1]==1)
        strategy.entry("RsiLE", strategy.long, comment="RsiLE")
    if (crossunder(o, ema_line) and chk[1]==0)
        strategy.entry("RsiSE", strategy.short, comment="RsiSE")

```

> Detail

https://www.fmz.com/strategy/442364

> Last Modified

2024-02-21 14:05:12
