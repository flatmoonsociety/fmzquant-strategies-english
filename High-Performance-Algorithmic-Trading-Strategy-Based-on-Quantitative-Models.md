
> Name

High-Performance-Algorithmic-Trading-Strategy-Based-on-Quantitative-Models customized based on quantitative models
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/93b2e076d866a67f9f30f2a416a70616c77b61cc1a5c4fda7b08a2e1f5f09d2a.png)
[trans]

## Overview
This strategy is an efficient quantitative trading strategy customized based on a quantitative model. The strategy uses the Modelius Volume model as the basic model, and is expanded and optimized on this basis. This strategy can capture quantitative trading opportunities in the market and achieve stable profits.
## Strategy Principle
The core of this strategy is the Modelius Volume model. This model uses changes in price and trading volume to identify quantitative trading opportunities in the market. Specifically, the strategy uses a combination of close price, open price, highest price, and lowest price to calculate the direction of the current K-line according to certain rules. When the direction of the K-line changes, the quality of the quantitative trading opportunity is judged based on the size of the trading volume. In addition, the strategy also combines the SAR indicator and the moving average indicator to assist in determining the timing of entry and exit.
The basic trading logic is that when the indicator breaks through from negative to positive, go long; when the indicator breaks through from positive to negative, go short. In addition, the strategy also sets stop loss, take profit, and trailing stop loss to control risks.
## Advantage Analysis
The biggest advantage of this strategy is that it can effectively identify quantitative trading opportunities using the Modelius Volume model. Compared with traditional technical indicators, this model pays more attention to changes in trading volume, which is very practical in current high-frequency quantitative trading. In addition, the entry rules of the strategy are relatively strict, which can effectively avoid missing quantitative trading opportunities while minimizing the probability of disorder.
## Risk Analysis
The main risk with this strategy is that the Modelius Volume model itself is not completely immune to noise. When the market fluctuates abnormally, it will cause errors in trading signals. In addition, the parameter settings in the strategy will also have an impact on the final results.
In order to control risks, parameters can be adjusted appropriately and combined with other indicators to assist judgment. In addition, it is also necessary to set reasonable stop loss and take profit positions.
## Optimization direction
This strategy still has some room for optimization. For example, you can consider combining machine learning algorithms to dynamically optimize parameter settings. Or combine indicators such as sentiment analysis to improve the accuracy of decision-making. In addition, the correlation between different varieties can also be studied and a multi-variety arbitrage model can be established.
## Summarize
In general, this strategy takes advantage of the Modelius Volume quantitative model to design a set of highly operable quantitative trading strategies. It can be optimized and improved through parameter adjustment, model expansion, machine learning and other methods to obtain better and stable returns in actual transactions.
||

## Overview

This strategy is a high-performance algorithmic trading strategy based on quantitative models. It uses the Modelius Volume model as the basic model and further extends and optimizes it. This strategy can capture quantitative trading opportunities in the market and achieve steady profits.  

## Strategy Principle  

The core of this strategy is the Modelius Volume model. This model identifies quantitative trading opportunities in the market by detecting price and volume changes. Specifically, the strategy combines close price, open price, highest price, lowest price to calculate the direction of the current K-line based on certain rules. When the K-line direction changes, the quality of the quantitative trading opportunity is judged based on the trading volume. In addition, the strategy also combines the SAR indicator and moving average indicator to assist in determining entry and exit timing.  

The basic trading logic is to go long when the indicator breaks through from negative to positive and go short when the indicator breaks through from positive to negative. In addition, stop loss, take profit, trailing stop loss are set up to control risks.

## Advantage Analysis 

The biggest advantage of this strategy is that the Modelius Volume model can effectively identify quantitative trading opportunities. Compared with traditional technical indicators, this model pays more attention to volume changes, which is very practical in today's high-frequency quantitative trading. In addition, the entry rules of the strategy are relatively strict, which can effectively avoid missing quantitative trading opportunities while reducing the probability of disorder as much as possible.

## Risk Analysis   

The main risk of this strategy is that the Modelius Volume model itself cannot completely avoid noise. When there is abnormal market fluctuation, it will lead to wrong trading signals. In addition, the parameter settings in the strategy will also affect the final results.  

To control risks, parameters can be adjusted accordingly and combined with other indicators for auxiliary judgment. In addition, stop loss and take profit should be set reasonably.

## Optimization Directions

There is still room for optimizing this strategy. For example, machine learning algorithms can be considered to dynamically optimize parameter settings. Or combine sentiment analysis and other indicators to improve decision accuracy. In addition, the correlation between different varieties can be studied to establish a multi-variety arbitrage model.  

## Summary  

In summary, this strategy utilizes the advantages of the Modelius Volume quantitative model and designs a set of algorithmic trading strategies with high operability. It can be further optimized and enhanced through parameter tuning, model expansion, machine learning, etc. to obtain relatively good and steady returns in actual trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Renko Assignment Method: ATR|Traditional|Part of Price|
|v_input_2|14|Value|
|v_input_3|0|Price Source: Close|Open / Close|High / Low|
|v_input_4|0|Use True Range instead of Volume: Auto|Always|Never|
|v_input_5|true|Oscillating|
|v_input_6|false|Normalize|
|v_input_7|false|TP|
|v_input_8|false|SL|
|v_input_9|true|TS|
|v_input_10|3|TO|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-15 00:00:00
end: 2023-12-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


//@version=3
strategy(title="strategy modelius volume model ", shorttitle="mvm",overlay=true, calc_on_order_fills=true, default_qty_type=strategy.percent_of_equity, default_qty_value=50, overlay=false)

method = input(defval="ATR", options=["ATR", "Traditional", "Part of Price"], title="Renko Assignment Method")
methodvalue = input(defval=14.0, type=float, minval=0, title="Value")
pricesource = input(defval="Close", options=["Close", "Open / Close", "High / Low"], title="Price Source")
useClose = pricesource == "Close"
useOpenClose = pricesource == "Open / Close" or useClose
useTrueRange = input(defval="Auto", options=["Always", "Auto", "Never"], title="Use True Range instead of Volume")
isOscillating=input(defval=true, type=bool, title="Oscillating")
normalize=input(defval=false, type=bool, title="Normalize")
vol = useTrueRange == "Always" or (useTrueRange == "Auto" and na(volume))? tr : volume
op = useClose ? close : open
hi = useOpenClose ? close >= op ? close : op : high
lo = useOpenClose ? close <= op ? close : op : low

if method == "ATR"
    methodvalue := atr(round(methodvalue))
if method == "Part of Price"
    methodvalue := close/methodvalue

currclose = na
prevclose = nz(currclose[1])
prevhigh = prevclose + methodvalue
prevlow = prevclose - methodvalue
currclose := hi > prevhigh ? hi : lo < prevlow ? lo : prevclose

direction = na
direction := currclose > prevclose ? 1 : currclose < prevclose ? -1 : nz(direction[1])
directionHasChanged = change(direction) != 0
directionIsUp = direction > 0
directionIsDown = direction < 0

barcount = 1
barcount := not directionHasChanged and normalize ? barcount[1] + barcount : barcount
vol := not directionHasChanged ? vol[1] + vol : vol
res = barcount > 1 ? vol/barcount : vol


x=isOscillating and directionIsDown ? -res : res

TP = input(0) * 10
SL = input(0) * 10
TS = input(1) * 10
TO = input(3) * 10
CQ = 100

TPP = (TP > 0) ? TP : na
SLP = (SL > 0) ? SL : na
TSP = (TS > 0) ? TS : na
TOP = (TO > 0) ? TO : na

longCondition = crossover(x,0)
if (longCondition)
    strategy.entry("Long", strategy.long)


shortCondition = crossunder(x,0)
if (shortCondition)
    strategy.entry("Short", strategy.short)

strategy.exit("Close Short", "Short", qty_percent=CQ, profit=TPP, loss=SLP, trail_points=TSP, trail_offset=TOP)
strategy.exit("Close Long", "Long", qty_percent=CQ, profit=TPP, loss=SLP, trail_points=TSP, trail_offset=TOP)
```

> Detail

https://www.fmz.com/strategy/436227

> Last Modified

2023-12-22 13:14:33
