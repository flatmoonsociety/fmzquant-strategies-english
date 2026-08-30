
> Name

Multi-MA-Pair-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy combines the ideas of double moving average screening and price pattern judgment to form a more comprehensive entry mechanism, aiming to improve signal quality. The strategy also adds profit trade-off control and maximum position period restrictions, achieving a relatively complete risk management mechanism.
### Strategy Principles
This strategy mainly includes the following indicators and trading rules:
1. 3 SMA moving averages: determine the direction of the large-level trend.
2. 2 EMA moving averages: judge the detailed direction.
3. SAR indicator: assists in judging trends and breakthroughs.
4. K-line pattern: Identify specific K-line patterns as one of the entry signals.
5. Maximum number of profit closing times: Limit the maximum number of profit closing times for a single position and fix the profit.
6. Maximum holding period: avoid loss expansion and control single losses.
This strategy integrates a variety of technical indicators for composite judgment to form a relatively stable entry signal and exit mechanism, which improves profits while controlling risks and achieving stable transactions.
### Advantage Analysis
Compared with the single indicator strategy, this strategy has the following advantages:
1. Multi-indicator combination improves signal accuracy.
2. K-line pattern recognition improves entry timing.
3. The number of profit closing times is controlled to ensure profit determination.
4. The position period limit prevents the expansion of single losses.
5. SMA moving average determines the general trend and exerts the trend following effect.
6. EMA moving average is used for detailed analysis to improve sensitivity.
7. The SAR indicator assists in judging the reliability of breakthroughs.
8. The overall risk-return balance is good, but it is difficult to fit.
9. Parameters can be adjusted according to the market to obtain stable excess returns.
### Risk Analysis
Although this strategy offers several advantages, the following risks should be noted:
1. The combination of multiple indicators increases complexity and makes implementation more difficult.
2. The scope of parameter optimization is wide and there are optimization risks.
3. The K-line pattern recognition effect is questionable, and wrong signals may occur.
4. It is easy to miss the opportunity after profit closing.
5. The position cycle limit makes the profit upper limit somewhat flouted.
6. There is a certain conflict between stability and revenue optimization.
7. The adaptability of multiple varieties to the market environment needs to be studied.
8. Continuous attention needs to be paid to policy robustness.
### Optimization direction
Based on the above analysis, this strategy can be optimized as follows:
1. Adjust parameter combinations to improve income stability.
2. Introduce machine learning technology to optimize entry timing.
3. Optimize and dynamically adjust stop-loss and take-profit strategies.
4. Evaluate the impact of different holding periods on the yield curve.
5. Test the adaptability of the strategy in different markets.
6. Add parameter robustness check to prevent over-optimization.
7. Develop a quantitative risk management system.
8. Continuously verify the effectiveness of strategies to prevent obsolescence and failure.
### Summarize
Generally speaking, this strategy forms a relatively stable trading system with the assistance of multiple indicators. However, any strategy needs to be continuously optimized and verified, and attention should be paid to parameter robustness so that the strategy can be adaptable to different market environments. Quantitative trading is an iterative process.
||


### Overview

This strategy combines dual moving average selection and price pattern recognition to form a more comprehensive entry mechanism for improving signal quality. It also incorporates profit taking control and maximum holding period to achieve robust risk management.

### Strategy Logic

The strategy includes the following indicators and rules:

1. 3 SMAs judge overall trend. 

2. 2 EMAs make detailed directional judgment.

3. SAR assists with trend and momentum. 

4. Price patterns identify formations as entry signals.

5. Max profit take limit controls profit booking.

6. Holding period limit avoids loss expansion.

The combination of multiple indicators forms robust entry signals and exit mechanisms, balancing profitability and risk control for steady trading.

### Advantages

Compared to single indicator strategies, the advantages are:

1. Multiple indicators improve accuracy.

2. Price pattern recognition improves entry timing.

3. Profit take control realizes profit.

4. Holding period avoids loss expansion. 

5. SMAs follow the trend.

6. EMAs improve sensitivity.

7. SAR verifies breakout reliability.

8. Overall good risk-reward balance, robustness.

9. Tuning parameters can achieve steady alpha.

### Risks

Despite the merits, the following risks should be noted:

1. Multiple indicators increase complexity.

2. Broad parameter tuning risks over-optimization.

3. Price pattern recognition effectiveness uncertain.

4. Profit taking risks missing trend continuation.

5. Holding period limits profit potential.

6. Stability and profitability have tradeoff. 

7. Multi-market robustness requires validation. 

8. Ongoing monitoring of model robustness critical.

### Enhancement

Based on the analysis, enhancements may include:

1. Adjust parameters for return stability.

2. Incorporate machine learning for entry timing.

3. Optimize dynamic stop loss and take profit.

4. Assess impact of holding period on equity curve.

5. Test robustness across different markets.

6. Add parameter robustness checks to prevent overfitting.

7. Develop quantitative risk management.

8. Continually validate strategy efficacy.

### Conclusion

In summary, the multi-indicator approach forms a relatively robust trading system. But continual optimization and validation are key for any strategy, with focus on parameter robustness for market adaptability. Quant trading is an iterative process.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Quantity|
|v_input_2|3|SMA Period 01|
|v_input_3|8|SMA Period 02|
|v_input_4|10|SMA Period 03|
|v_input_5|5|EMA Period 01|
|v_input_6|3|EMA Period 02|
|v_input_7|5|Max Profit Close|
|v_input_8|10|Max Total Bars|


> Source (PineScript)

``` pinescript
//@version=3
strategy("Free Strategy #08 (Combo of #01 and #02) (ES / SPY)", overlay=true)

// Inputs
Quantity = input(1, minval=1, title="Quantity")
SmaPeriod01 = input(3, minval=1, title="SMA Period 01")
SmaPeriod02 = input(8, minval=1, title="SMA Period 02")
SmaPeriod03 = input(10, minval=1, title="SMA Period 03")
EmaPeriod01 = input(5, minval=1, title="EMA Period 01")
EmaPeriod02 = input(3, minval=1, title="EMA Period 02")
MaxProfitCloses = input(5, minval=1, title="Max Profit Close")
MaxBars = input(10, minval=1, title="Max Total Bars")

// Misc Variables
src = close
BarsSinceEntry = 0
MaxProfitCount = 0
Sma01 = sma(close, SmaPeriod01)
Sma02 = sma(close, SmaPeriod02)
Sma03 = sma(close, SmaPeriod03)
Ema01 = ema(close, EmaPeriod01)
Ema02 = ema(close, EmaPeriod02)
OHLC = (open + high + low + close) / 4.0

// Conditions
Cond00 = strategy.position_size == 0
Cond01 = close < Sma03
Cond02 = close <= Sma01
Cond03 = close[1] > Sma01[1]
Cond04 = open > Ema01
Cond05 = Sma02 < Sma02[1]
Entry01 = Cond00 and Cond01 and Cond02 and Cond03 and Cond04 and Cond05

Cond06 = close < Ema02
Cond07 = open > OHLC
Cond08 = volume <= volume[1]
Cond09 = (close < min(open[1], close[1]) or close > max(open[1], close[1]))
Entry02 = Cond00 and Cond06 and Cond07 and Cond08 and Cond09

// Update Exit Variables
BarsSinceEntry := Cond00 ? 0 : nz(BarsSinceEntry[1]) + 1
MaxProfitCount := Cond00 ? 0 : (close > strategy.position_avg_price and BarsSinceEntry > 1) ? nz(MaxProfitCount[1]) + 1 : nz(MaxProfitCount[1])

// Entries
strategy.entry(id="L1", long=true, qty=Quantity, when=(Entry01 or Entry02))
 
// Exits
strategy.close("L1", (BarsSinceEntry - 1 >= MaxBars or MaxProfitCount >= MaxProfitCloses))
```

> Detail

https://www.fmz.com/strategy/427670

> Last Modified

2023-09-23 15:16:50
