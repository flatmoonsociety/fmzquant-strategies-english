
> Name

Configurable-Multi-MA-Crossover-Voting-System
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy sets multiple combinations of fast and slow moving averages through configuration. When all fast lines cross the slow line, go long; when at least one fast line crosses the slow line, close the position. The strategy makes full use of the advantages of multiple moving averages to form a strong position decision-making system.
### Strategy Principles
The main components and rules of the strategy are as follows:
1. Multiple sets of fast and slow moving averages: Use multiple moving average indicators such as SMA, WMA, VWMA, etc.
2. Buy signal: go long when all fast lines cross the slow lines.
3. Position closing signal: Close the position when any fast line crosses the slow line.
4. Take profit and stop loss: Set a fixed take profit and stop loss point based on the ATR value.
5. Configurable: Multiple sets of moving average parameters can be flexibly configured.
Entering the market through multi-moving average combination position voting can effectively enhance the reliability of the signal. Multiple moving average parameters can be customized and configured with flexibility.
### Advantage Analysis
Compared with a single moving average strategy, this strategy has the following advantages:
1. Multiple moving average combinations can provide more comprehensive trend judgment.
2. The voting method avoids noise trading by mistake.
3. Each moving average parameter can be configured freely, with large room for optimization.
4. Supports multiple moving average indicators and is flexible to use.
5. Set take-profit and stop-loss points to control single profit and loss.
6. Longer period of use has better effect and can reduce curve oscillation.
7. The calculation is simple and intuitive, easy to implement and operate.
8. Generally speaking, the stability and battery life are better than the single moving average.
### Risk Analysis
But this strategy also has certain risks:
1. Multiple moving averages increase the complexity of the strategy.
2. There is a risk of over-optimization of parameters.
3. The moving average essentially lags in identifying trend changes.
4. Without considering the trading volume, quilt trap may occur.
5. The stop-profit and stop-loss settings are arbitrary and may result in unnecessary closing of positions.
6. The effect fluctuates greatly with changes in the market environment.
7. Pay attention to the return drawdown ratio to prevent the curve from being too jagged.
8. The robustness of the parameters in multiple varieties needs to be tested.
### Optimization direction
Based on the above analysis, this strategy can be enhanced from the following aspects:
1. Test the robustness of moving average parameters in different varieties.
2. Increase trading volume or volatility verification.
3. Optimize the stop-profit and stop-loss parameters.
4. Set the maximum retracement tolerance.
5. Build a dynamic position management mechanism.
6. Evaluate the effect of introducing machine learning.
7. Pay attention to the maximum retracement and the jaggedness of the return curve.
8. Continuously iterate strategies to prevent over-optimization.
### Summarize
This strategy forms a more robust position decision-making mechanism by setting multiple moving average combinations through allocation. But any strategy needs to prevent overfitting and make dynamic adjustments according to the market environment. Only through continuous optimization and testing can quantitative strategies adapt to the market in the long term.
||

### Overview

This strategy allows flexible configuration of multiple fast/slow moving average pairs. It goes long when all fast MAs crossover above slow MAs, and exits when any fast MA crosses below slow MA. The voting mechanism with multiple MAs aims to form robust position holding decisions. 

### Strategy Logic

The key components and rules are:

1. Multiple fast/slow MAs: Using SMA, WMA, VWMA etc.

2. Long signal: All fast MAs crossing above slow MAs. 

3. Exit signal: Any fast MA crossing below slow MA.

4. Profit/loss points: Fixed points based on ATR.

5. Configurable: Flexible configuration of multiple MA pairs.

The voting-based entry with multiple MAs improves signal reliability. Custom configurations provide flexibility.

### Advantages

Compared to single MA strategies, the advantages are:

1. Multiple MAs provide more comprehensive trend assessment.

2. Voting avoids false signals from noise.

3. Large tuning space from custom MA configurations.

4. Support for different MA types enhances adaptability.

5. Defined profit/loss points control per trade risk/reward. 

6. Works better on longer timeframes, less curve whipsaws.

7. Simple and intuitive logic, easy to implement and operate.

8. Overall more stable with greater longevity versus single MA.

### Risks

However, some risks exist:

1. Increased complexity with multiple MAs. 

2. Risks of over-optimization.

3. Fundamental lagging in identifying trend changes.

4. No volume considered, risks being trapped.

5. Profit/loss points may cause unnecessary exits.

6. Performance subject to changing market regimes.

7. Need to monitor reward/risk ratios and curve smoothness.

8. Robustness across instruments requires validation.

### Enhancements

Based on the analysis, enhancements may involve:

1. Testing parameter robustness across different instruments. 

2. Adding volume or volatility confirmation.

3. Optimizing profit/loss points.

4. Setting maximum tolerable drawdown limit.

5. Constructing dynamic position sizing models.

6. Evaluating effect from introducing machine learning.

7. Monitoring maximum drawdown and curve smoothness.

8. Continual iterations to avoid overfitting.

### Conclusion

The configurable multi-MA approach forms a robust position holding mechanism. But preventing overfitting and dynamic adaptations to changing markets are key for any strategy's longevity. Only through rigorous ongoing optimizations and testing can a quant strategy sustain success.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_string_1|2x4,3x5,4x6|Crossover Config|
|v_input_source_1_high|0|source: high|close|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_string_2|0|Moving Average Type: WMA|SMA|VWMA|
|v_input_1|14|ATR Period|
|v_input_2|10|Profit ATR x|
|v_input_3|5|Loss ATR x|


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
// © levieux

//@version=5
strategy(title='Configurable Multi MA Crossover Voting System', shorttitle='Configurable Multi MA Crossover Voting System', initial_capital=1000, overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.1)
crossoverConfig= input.string(defval="2x4,3x5,4x6", title="Crossover Config")
source= input.source(high)
maType= input.string("WMA", title="Moving Average Type", options=["WMA","SMA","VWMA"])
atrPeriod= input(14, title="ATR Period")
profitAtr = input(10, title="Profit ATR x")
lossAtr = input(5, title="Loss ATR x")


ma(src,length,type) => 
    float ma = switch type
	    "SMA" => ta.sma(src, length)
	    "WMA" => ta.wma(src, length)
	    "VWMA" => ta.vwma(src, length)

crossoverGroups= str.split(crossoverConfig, ",")
crossoverCount= array.size(crossoverGroups)
crossovers= array.new_string(crossoverCount)
positions= array.new_int(crossoverCount, 0)
longVotes= 0
for i= 0 to crossoverCount-1
    crossover= str.tostring(array.get(crossoverGroups, i))
    crossoverBoundaries= str.split(crossover, "x")
    int fastLength= math.round(str.tonumber(array.get(crossoverBoundaries, 0)))
    int slowLength= math.round(str.tonumber(array.get(crossoverBoundaries, 1)))
    wmaFast= ma(source,fastLength,maType)
    wmaSlow= ma(source,slowLength,maType)
    if wmaFast>wmaSlow
        longVotes:= longVotes + 1
        array.set(positions, i, 1)

longCondition= longVotes==crossoverCount and strategy.position_size==0


//profitTicks = profitAtr*ta.atr(atrPeriod)/syminfo.mintick
//lossTicks = lossAtr*ta.atr(atrPeriod)/syminfo.mintick
profitPrice= close+profitAtr*ta.atr(atrPeriod)
lossPrice= close-lossAtr*ta.atr(atrPeriod)

if strategy.position_size>0
    profitPrice:= profitPrice[1]
    lossPrice:= lossPrice[1]

plot(profitPrice, color=color.green)
plot(lossPrice, color=color.red)

if longCondition and profitPrice>0
    strategy.entry("Long", strategy.long)

if longVotes<crossoverCount and strategy.position_size>0 and (high>profitPrice or low<lossPrice)
    strategy.close("Long")
    
longVotes:= 0
```

> Detail

https://www.fmz.com/strategy/427680

> Last Modified

2023-09-23 15:52:06
