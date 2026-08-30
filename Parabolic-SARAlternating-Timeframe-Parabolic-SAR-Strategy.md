
> Name

Alternating-Timeframe-Parabolic-SAR-Strategy Alternating-Timeframe-Parabolic-SAR-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/fffc4ddd12e02923f4c855db0e000441a4f7194856525b68d2503474243cd81c.png)

[trans]


## Overview
The core idea of ​​this strategy is to use Parabolic SAR, a Momentum Indicators indicator, alternately in different time periods to capture the turning point of the market trend in different time periods. This strategy monitors Parabolic SAR signals in multiple time periods at the same time. Once a higher time period SAR signal is issued, it enters the corresponding long or short position.
## Strategy Principle
First, the strategy calculates the value of Parabolic SAR in different time periods (15 minutes, daily, weekly, monthly).
Secondly, the strategy monitors the weekly SAR value. Once the weekly SAR goes above the recent high, go long; once the weekly SAR goes below the recent low, go short.
Finally, the strategy uses weekly SAR as the stop loss point. Specifically, if you have gone long, the weekly SAR will be used as the stop loss point of the long position; if you have gone short, the weekly SAR will be used as the stop loss point of the short position.
In this way, the strategy realizes the idea of ​​entering the market when a signal is sent in a higher time period and taking a stop loss in a lower time period. Monitoring weekly SAR signals can more accurately determine trend turning points and reduce losses caused by false breakthroughs; using 15-minute SAR as a stop loss can quickly stop losses and avoid excessive losses when a reversal comes.
## Advantage Analysis
This strategy of using Parabolic SAR alternately across multiple time frames has the following advantages:
1. Take advantage of SAR in different time periods. Weekly SAR can accurately determine trend turning and reduce the risk of losses caused by false breakthroughs; 15-minute SAR can quickly stop losses and control single losses.
2. The strategy is highly flexible. The parameters of SAR can be adjusted according to different varieties and market conditions to optimize the strategy effect.
3. The strategic trading frequency is low. Only enter when the higher time frame SAR signals and avoid over-trading.
4. High capital utilization efficiency. Only deploy funds when it is judged that there is a high probability of a trend reversal, effectively avoiding long-term idle funds.
5. Easily control risks. With fixed stops, the risk exposure of each position can be clearly calculated.
## Risk Analysis
There are also some risks with this strategy:
1. Improper setting of SAR parameters may cause the stop loss to be too loose or too tight, thus affecting the strategy effect.
2. The target price may fluctuate violently, directly breaking through the stop loss line set by the strategy, resulting in large losses.
3. If you only rely on SAR signals for trading, you may miss other statistically advantageous trading opportunities in the trend.
4. Under multiple time frames, SARs of different periods may emit conflicting signals, and signal priority issues need to be dealt with.
5. Improper selection of periods, excessive short-period noise, or long-period lag in identifying turning points may affect the effectiveness of the strategy.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize SAR parameter settings to reduce the probability of whipsaw situations. You can adjust parameters multiple times through backtesting to find the optimal parameter combination.
2. Add stop loss strategies, such as trailing stop loss, stepped stop loss, etc., to further control single losses.
3. Combine with other indicators, such as MACD, KDJ, etc., to find more evidence to determine the trend turning point and reduce the probability of wrong transactions.
4. Add fund management strategies, such as fixed fund utilization rate, fixed profit and loss ratio, etc., to control the size of each position and overall control strategic risks.
5. Optimize the time period settings, test the strategy effects under different period combinations, and find the best period matching.
## Summarize
This strategy is based on the alternate use of Parabolic SAR indicators in different time periods. It determines the turning point of the trend in a higher time frame and stops losses in a lower time frame, thus realizing the complementary advantages of different time periods. This strategy effectively reduces the trading frequency and the risk of false breakthroughs caused by the whipsaw phenomenon. Through further improvement through parameter optimization, stop loss strategies, fund management and other means, excellent strategic effects can be obtained.

||


## Overview

The core idea of this strategy is to use the Parabolic SAR, one of the Momentum Indicators, alternately across different timeframes to capture trend reversals in the market. The strategy monitors Parabolic SAR signals simultaneously on multiple timeframes, and enters a corresponding long or short position once a SAR signal is triggered on a higher timeframe.

## Strategy Logic

Firstly, the strategy calculates Parabolic SAR values separately on different timeframes (15m, D, W, M).

Secondly, the strategy monitors the weekly SAR value. It goes long when the weekly SAR rises above the recent high, and goes short when the weekly SAR falls below the recent low. 

Finally, the strategy uses the weekly SAR as the stop loss. Specifically, if already long, the weekly SAR is set as the stop loss for that long position; if already short, the weekly SAR is set as the stop loss for that short position.

This way, the strategy enters based on signals from higher timeframes, and stops out on lower timeframes. Monitoring weekly SAR signals can more accurately identify trend reversals, while stopping out on 15m SAR can realize quick cut losses to avoid excessive drawdowns when reversals come.

## Advantage Analysis 

This Parabolic SAR alternating timeframe strategy has the following edges:

1. Utilizes the advantages of SAR on different timeframes. Weekly SAR can accurately identify trend reversals and reduce whipsaw losses; 15m SAR allows quick stop loss management.

2. High flexibility. SAR parameters can be adjusted for different products and market conditions to optimize strategy performance. 

3. Low trading frequency. Only enters on signals from higher timeframe SAR, avoiding overtrading.

4. High capital utilization efficiency. Deploys capital only when high probability reversal is identified, avoiding capital sitting idle.

5. Easy risk control. Adopting fixed stop loss points allows clear calculation of risk exposure for each position.

## Risk Analysis

This strategy also has some risks:

1. Improper SAR parameter setting may lead to stop loss being too wide or too tight, thus impacting strategy performance.

2. Sharp price spikes may directly penetrate the stop loss level, leading to large losses.

3. Relying solely on SAR signals may miss other statistically profitable opportunities during trends. 

4. Conflicting signals may arise from SAR on different timeframes. Signal priority needs to be handled.

5. Improper timeframe selection, too much noise on lower periods or lag in identifying reversals on higher periods, may both impact strategy efficacy. 

## Optimization Directions

The strategy can be improved in the following aspects:

1. Optimize SAR parameters to reduce whipsaw occurrences. Multiple backtests can be run to find optimal parameter combinations.

2. Add stop loss strategies like trailing stop, staggered stop loss etc to further control single trade loss.

3. Incorporate other indicators like MACD, KDJ to find more evidence for trend reversals, reducing trading errors.

4. Add capital management strategies like fixed fractional position sizing, fixed risk-reward ratio etc to size each position and control overall strategy risk. 

5. Optimize timeframe combinations by testing strategy performance under different period settings to find best match.

## Conclusion

This strategy utilizes Parabolic SAR alternately across timeframes, identifying reversal points on higher periods and stopping out on lower periods, achieving synergistic effect. It effectively reduces whipsaw trades and risk from false breakouts. With further enhancements like parameter optimization, stop loss strategies and capital management, outstanding strategy results can be achieved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|15|Resolution|
|v_input_2|D|Resolution|
|v_input_3|W|Resolution|
|v_input_4|M|Resolution|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-18 00:00:00
end: 2023-10-18 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy ("SAR alternating timeframe", overlay=true)

//resolution
res1=input("15", title="Resolution")
res2=input("D", title="Resolution")
res3=input("W", title="Resolution")
res4=input("M", title="Resolution")

//output functions
out = sar(0.02,0.02,0.2)

// Security
SAR1 = request.security(syminfo.tickerid, res1, out)
SAR2 = request.security(syminfo.tickerid, res2, out)
SAR3 = request.security(syminfo.tickerid, res3, out)
SAR4 = request.security(syminfo.tickerid, res4, out)

//Plots
//plot(SAR1 , title="SAR 15", color = red, linewidth = 2)
//plot(SAR2 , title="SAR D", color = green, linewidth = 3)
plot(SAR3 , title="SAR W", color =blue, linewidth = 4)
//plot(SAR4 , title="SAR W", color =purple, linewidth = 5))


/////////////////////////////////////////////////////////////////////
//trade
if (SAR3 >= high)
    strategy.entry("ParLE", strategy.long, stop=SAR3, comment="ParLE")
else
    strategy.cancel("ParLE")

if (SAR3 <= low)
    strategy.entry("ParSE", strategy.short, stop=SAR3, comment="ParSE")
else
    strategy.cancel("ParSE")


```

> Detail

https://www.fmz.com/strategy/429688

> Last Modified

2023-10-19 18:08:47
