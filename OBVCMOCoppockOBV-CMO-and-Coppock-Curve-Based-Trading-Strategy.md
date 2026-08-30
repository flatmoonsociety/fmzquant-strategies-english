
> Name

Trading strategy based on OBVCMO and Coppock curveOBV-CMO-and-Coppock-Curve-Based-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/a48f9e49d148f1d5107d9f2f3e2d6680f428e2c80203e0e8cb79e3384b2dee56.png)
[trans]
## Overview
The RB quantitative trading three-in-one strategy is a composite strategy that combines the market popularity indicator OBV, the short- and medium-term movement volume indicator CMO, and the long-term movement volume indicator Coppock curve. This strategy comprehensively considers the three dimensions of the market's long and short popularity, short- and medium-term trends, and long-term trends to form trading signals to achieve more reliable entry.
## Strategy Principle
The trading signals for this strategy are derived from a combination of the following three indicators:
1. OBV: reflects the popularity of the market and the strength of the long and short forces. An increase in OBV represents the strengthening of bullish forces, while a decrease in OBV represents the strengthening of short forces.
2. CMO: reflects the trend of short- and medium-term price change rates. A positive CMO represents an upward trend in the short to medium term, and a negative CMO represents a downward trend.
3. Coppock curve: reflects the trend of long-term price change rate. The upward Coppock curve indicates that the long-term trend is in an upward phase, and the downward trend indicates that the long-term trend is in a downward trend.
A buy signal is generated when the OBV rises and the CMO and Coppock curves rise simultaneously. This means that the multiple forces in the market have strengthened and are in an upward channel in the medium to long term, making it a better buying point.
On the contrary, when the OBV falls and the CMO and Coppock curves fall simultaneously, a sell signal is generated. This means that the forces of the short side have strengthened and the mid- to long-term downward channel has opened, which is a better time to leave the market.

## Strategic Advantages
The biggest advantage of this strategy is that it comprehensively considers the three dimensions of the market's long and short enthusiasm, short-term and long-term trends, and long-term trends. It ensures that trend changes are consistent from the market level, the short-term level, and the long-term level before generating trading signals, so it can effectively avoid false breakthroughs. At the same time, while using the sensitivity of CMO to seize short-term opportunities, the Coppock curve provides long-term filtering to ensure that the general direction is correct.
In addition, this strategy also uses the construction of two-way signals for buying and selling, which can achieve better capital utilization.
## Strategy Risk
The main risk of this strategy is that the Coppock curve and the ROC calculation cycle used by CMO are long and will have a certain lag. When market emergencies change violently, the Coppock curve and CMO indicators may delay judgment. At this time, you need to rely on the rapid judgment of OBV. However, OBV, as an accumulation energy line, will also lag behind several K lines in response to emergencies.
In addition, simply merging the three indicators together for judgment does not consider the weight setting between the indicators, which will also affect the accuracy of the judgment.
## Strategy optimization direction
This strategy can be optimized in the following aspects:
1. Use adaptive ROC cycle settings for the Coppock curve and CMO indicators, so that the parameters of the indicators can automatically adapt to the changing frequency of the market.
2. Increase the weight setting of indicators, let some indicators with more accurate judgments play a leading role, and improve the stability of signals.
3. Add a stop-loss strategy and use indicators similar to ATR to set the stop-loss range of transactions to effectively control the maximum loss of a single transaction.
4. Take advantage of OBV’s quick response and set OBV reversal as a stop loss signal to avoid large losses.
## Summarize
The RB quantitative trading three-in-one strategy comprehensively considers the three dimensions of market popularity, short- and medium-term movement volume, and long-term movement volume to form buying and selling signals. It combines the advantages of multiple indicators to ensure that the market's long and short situation and medium and long-term trends converge to generate trading signals. The main advantage is that the signal is stable and reliable, effectively avoiding false breakthroughs. Through subsequent optimization design, the actual combat effect of the strategy will be further improved.
||

## Overview

The RB quant trading combo strategy is a composite strategy that combines volume-based indicator OBV, momentum oscillator CMO and long-term momentum indicator Coppock curve. This strategy takes into account market sentiment, mid-term trend and long-term trend from three dimensions and generates trading signals for more reliable market entry.  

## Strategy Logic

The trading signals of this strategy come from a combination of the following three indicators:

1. OBV: Reflects market sentiment and strength of bulls vs bears. Rising OBV represents strengthening of bulls while falling OBV represents bears taking over.

2. CMO: Captures mid-term trend of price rate of change. Positive CMO indicates mid-term uptrend while negative CMO shows downtrend.  

3. Coppock Curve: Tracks long-term trend of price rate of change. Upward Coppock curve shows long term bull phase while downward direction represents long term bear phase.

Buy signal is generated when OBV rises with CMO and Coppock curve turning up together. This indicates market sentiment backing up the bulls with mid to long term uptrend intact, making it a good buying opportunity.  

Sell signal is triggered when OBV declines and both CMO and Coppock curve turning down in unison. This shows bears in control with mid-long term downtrend channel opening up, serving as good timing for position exit.

## Advantages  

The biggest edge of this strategy lies in synthesizing market sentiment, mid-term and long-term trends from three perspectives. Trading signals are only formed after confirmation of trend change across market breadth, mid-term and long horizon, thus avoiding false breakout effectively. Meanwhile Coppock curve provides long term directional bias while CMO captures short-term opportunities with swiftness.  

Another advantage comes from bi-directional buy and sell signals enabling efficient capital utilization.  

## Risks

Main risks of this strategy originates from the lagging nature of Coppock Curve and CMO due to their long ROC calculation periods. Sudden volatile market events could fail to trigger timely signals from these two long-term gauges. Fast determination has to count on OBV in such scenarios. However, OBV as an accumulated volume indicator also suffers from a few bars of delay facing sudden turning points. 

In addition, simple combination of the three indicators without weighting could compromise the judging accuracy.  

## Enhancement Opportunities 

The strategy could be upgraded in the following aspects going forward:

1. Adopt adaptive ROC periods for Coppock Curve and CMO to automatically calibrate parameters responding to market regime changes.  

2. Introduce weighting system emphasizing signals from more precise indicators, improving overall signal quality and stability. 

3. Incorporate stop loss based on volatility measurements like ATR, effectively capping maximum loss per trade.

4. Utilize swift change in OBV to gauge stop loss signals, avoiding heavy losses.

## Conclusion  

The RB Quant Combo strategy synthesizes market breadth, mid-term and long-term momentum to generate buy / sell signals, amalgamating strengths of multiple indicators. Trading opportunities arise only after alignment of market sentiment and mid-long term trends. Its key advantage lies in signal reliability and false breakout avoidance. With further optimizations, strategy performance could be lifted to the next level in live trading.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Chande Momentum Oscillator Period|
|v_input_2|14|Coppock Curve Long ROC Period|
|v_input_3|11|Coppock Curve Short ROC Period|
|v_input_4|10|Coppock Curve WMA Period|
|v_input_5|50|CMO Buy Threshold|
|v_input_6|-50|CMO Sell Threshold|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-13 00:00:00
end: 2024-02-19 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("RB - OBV Coppock CMO Strategy", overlay=true)

// Input for CMO period
cmo_period = input(14, title="Chande Momentum Oscillator Period")
// Input for Coppock Curve periods
coppock_long = input(14, title="Coppock Curve Long ROC Period")
coppock_short = input(11, title="Coppock Curve Short ROC Period")
coppock_wma = input(10, title="Coppock Curve WMA Period")
// Thresholds for CMO
cmo_buy_threshold = input(50, title="CMO Buy Threshold")
cmo_sell_threshold = input(-50, title="CMO Sell Threshold")

// Calculating OBV
obv = cum(close > close[1] ? volume : close < close[1] ? -volume : 0)

// Calculating Coppock Curve
roc_long = roc(close, coppock_long)
roc_short = roc(close, coppock_short)
coppock_curve = wma(roc_long + roc_short, coppock_wma)

// Calculating Chande Momentum Oscillator
cmo = cmo(close, cmo_period)

// Generate buy and sell signals
buy_signal = obv > obv[1] and coppock_curve > 0 and coppock_curve > coppock_curve[1] and cmo > cmo_buy_threshold
sell_signal = obv < obv[1] and coppock_curve < 0 and coppock_curve < coppock_curve[1] and cmo < cmo_sell_threshold

// Plotting signals on the chart
plotshape(series=buy_signal, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=sell_signal, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// Setting up the strategy entry and exit points
if (buy_signal)
    strategy.entry("Buy", strategy.long)

if (sell_signal)
    strategy.close("Buy")

// Plot OBV and Coppock Curve for reference
plot(obv, title="On Balance Volume", color=color.blue)
hline(0, "Zero Line", color=color.gray)
plot(coppock_curve, title="Coppock Curve", color=color.purple)
plot(series=cmo, title="Chande Momentum Oscillator", color=color.orange)


```

> Detail

https://www.fmz.com/strategy/442212

> Last Modified

2024-02-20 11:26:46
