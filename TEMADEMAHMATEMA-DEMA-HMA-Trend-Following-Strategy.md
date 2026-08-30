
> Name

TEMADEMAHMA combination trend following strategy TEMA-DEMA-HMA-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy uses a combination of three different types of moving averages: TEMA, DEMA and HMA. It enters the market when the short- and medium-term moving averages TEMA and DEMA send out golden cross/death cross signals, and uses the long-term moving average HMA to determine the trend direction and filter out counter-trend trading signals.
### Strategy Principles
1. Calculate three moving averages: TEMA, DEMA and HMA
2. When TEMA crosses DEMA, enter long position
3. When TEMA crosses DEMA, enter the market short
4. Calculate the trend direction of the long-term HMA and enter the market only when the HMA shows the same trend.
Specifically, this strategy simultaneously uses the double exponential moving average DEMA to determine the mid-term trend, the three-exponential moving average TEMA to determine the short-term trend, and the dense moving average HMA to determine the long-term trend. Only when the short and medium term start in the same direction (TEMA and DEMA break through in the same direction) and the long-term main trend is also in the same direction (the direction of HMA is consistent with the breakthrough), a trading signal is generated.
### Advantage Analysis
1. Combine multiple moving averages to improve judgment accuracy
2. HMA’s trend filtering can avoid counter-trend trading
3. TEMA and DEMA can form clearer trading signals
4. The parameters of the three moving averages can be customized to adapt to different periods.
5. Trade with the trend and have less risk of retracement
### Risk Analysis
1. The three-line combination is more complex and requires tuning of multiple parameters.
2. HMA trend judgment may lag behind price
3. There is a certain degree of lagging transaction risk
4. Improper parameters may increase unnecessary reverse transactions
Risks can be managed through multiple sets of parameter tests to find the best parameter combination, introduce stop-loss strategies, and appropriately relax entry conditions.
### Optimization direction
1. Test different moving average period parameters to find the optimal combination
2. Add indicators such as MACD to the evaluation as auxiliary judgments
3. Add a trailing stop to lock in profits and reduce drawdowns
4. Study the parameter preferences of different varieties and establish a parameter optimization system
5. Relax entry conditions and adopt trend trading when long-term trends exist
### Summarize
This strategy uses a combination of multiple moving average indicators to determine trends. The advantage is that the signal is clearly generated and the configurable space is large; the disadvantage is that there is a risk of lag and multi-parameter dependence. Risks can be controlled through parameter optimization, stop loss strategies, etc., and the advantages of the combined moving average can be brought into play. This strategy can help traders fully master trend trading skills.
|| 

### Overview 

This strategy combines TEMA, DEMA and HMA moving averages to enter on TEMA/DEMA golden cross/dead cross signals, using HMA to determine trend direction to filter counter-trend trades.

### Strategy Logic

1. Calculate TEMA, DEMA and HMA moving averages  
2. Go long when TEMA crosses above DEMA
3. Go short when TEMA crosses below DEMA
4. Calculate HMA trend direction, only enter if aligning with HMA trend

Specifically, it uses DEMA to gauge medium-term trend, TEMA for short-term trend, and HMA for long-term trend. Trades are taken only when short/medium-term moves in alignment (TEMA/DEMA coordinated breakout), and long-term trend agrees (HMA direction matches breakout). 

### Advantage Analysis

1. Combining multiple moving averages improves accuracy
2. HMA trend filter avoids counter-trend trades 
3. TEMA/DEMA forms clear trading signals
4. Custom periods for three lines fit different cycles  
5. Trading with trend reduces drawdown risks

### Risk Analysis

1. Complex multi-line combination requires parameter tuning
2. HMA trend may lag price movement
3. Risks of lagging entry exist 
4. Bad parameters may increase unnecessary reverse trades

Risks can be managed by parameter optimization, stop loss, relaxing entry rules etc.

### Optimization Directions

1. Test different period combinations to find optimal parameters
2. Evaluate adding MACD etc. as auxiliary confirmation
3. Add trailing stop loss to lock in profits, reduce drawdown
4. Study parameter preferences across different products  
5. Relax entry rules to trade with long term trend

### Summary

This strategy generates signals by combining multiple moving average indicators to determine trend. Pros are clear signals and high configurability; Cons are lagging risks and parameter dependency. Risks can be controlled via parameter optimization, stop loss etc. to utilize the power of a combined moving average system. It helps traders comprehensively master trend trading techniques.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|8|TEMA Length|
|v_input_2|43|DEMA Length|
|v_input_3|52|Hull Length|
|v_input_4|2|Hull Trend Test Length|


> Source (PineScript)

``` pinescript
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © tuned-com

//@version=4
strategy("TEMA/DEMA/HMA", overlay=true, pyramiding=0, default_qty_type=strategy.percent_of_equity, default_qty_value=100, initial_capital=1000000, commission_type=strategy.commission.percent, commission_value=0.1)

Tlength = input(8, title="TEMA Length", minval=1)
Dlength = input(43, title="DEMA Length", minval=1)
Hlength = input(52, title="Hull Length", minval=1)
Rlength = input(2, title="Hull Trend Test Length", minval=1)


//TEMA//
ema1 = ema(close, Tlength)
ema2 = ema(ema1, Tlength)
ema3 = ema(ema2, Tlength)
tema = 3 * (ema1 - ema2) + ema3

//DEMA//
e1 = ema(close, Dlength)
e2 = ema(e1, Dlength)
dema = 2 * e1 - e2

//HMA//
hma = wma(2 * wma(close, Hlength / 2) - wma(close, Hlength), round(sqrt(Hlength)))


up = crossunder(dema, tema) and rising(hma, Rlength)
down = crossover(dema, tema) and falling(hma, Rlength)

downc = crossunder(dema, tema)
upc = crossover(dema, tema)

plot(dema, color=color.green, linewidth=2)
plot(tema, color=color.aqua, linewidth=2)

plot(hma, color=rising(hma, Rlength) ? color.green : na, linewidth=2, transp=0)
plot(hma, color=falling(hma, Rlength) ? color.red : na, linewidth=2, transp=0)

bgcolor(rising(hma, Rlength) ? color.green : na, transp=70)
bgcolor(falling(hma, Rlength) ? color.red : na, transp=70)

plotarrow(tema - dema, colorup=color.green, colordown=color.red, transp=70)



if up
    strategy.entry("Long Entry", strategy.long)

if down
    strategy.entry("Short Entry", strategy.short)
```

> Detail

https://www.fmz.com/strategy/427449

> Last Modified

2023-09-21 10:56:41
