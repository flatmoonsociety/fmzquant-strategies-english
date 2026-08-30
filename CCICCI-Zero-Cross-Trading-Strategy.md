
> Name

CCI Zero-Cross-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/127b26e09a635fb4c4d.png)
[trans]

#### Overview
CCI Zero Cross Trading Strategy is a quantitative trading strategy based on the Commodity Channel Index (CCI). This strategy generates trading signals by tracking the intersection of the CCI indicator and the zero axis. It goes long when CCI crosses the zero axis above and goes short when CCI crosses below the zero axis. It is a trend following type strategy.
#### Strategy Principle
The basic principles of the CCI Zero Point Reversal trading strategy are:
1. Use the CCI indicator to determine whether the market is overbought or oversold. The CCI indicator value crosses the 100 line when the market is overbought, and when it crosses the -100 line below, it is an oversold signal.
2. Monitor the intersection of the CCI indicator and the zero axis. When CCI crosses the zero line from bottom to top, a long signal is generated; when CCI crosses the zero line from top to bottom, a short signal is generated.
3. Enter the market based on the long and short signals of CCI crossing the zero axis, and set the CCI overbought and oversold area as a stop loss level.
Specifically, the entry rules for this strategy are:
1. When the CCI indicator crosses the zero axis from negative to positive, enter the market long and set the stop loss price at the -100 line.
2. When the CCI indicator crosses the zero axis from positive to negative, enter the market short and set the stop loss price at the 100 line.
This strategy mainly relies on the CCI indicator to determine the degree of overbought and oversold in the market, and makes profits by capturing its reversal opportunities. The CCI crossing zero axis can effectively capture the transition point of the market's mid-term trend. Overall, the strategy is simple and clear in logic and easy to implement.
#### Advantage Analysis
The main advantages of the CCI Zero Point Reversal trading strategy are:
1. The strategy signal comes from a single source and is only based on the intersection of the CCI indicator and the zero axis, achieving simple and effective trend tracking.
2. Use the reversal characteristics of the CCI indicator to effectively capture the transition point of the mid-term trend, with great profit potential.
3. The stop loss point is set in the overbought and oversold area of ​​CCI, which can stop losses in time and control risks.
4. The strategy implementation logic is simple and clear, parameter selection is easy, and it is suitable for the algorithmization of quantitative trading.
5. The CCI indicator is universally applicable to the market, the strategy has strong adaptability, and can be applied to various types of quantitative transactions.
#### Risk Analysis
There are also some risks in the CCI zero-point reversal trading strategy, which are mainly concentrated in the following aspects:
1. The CCI indicator has a certain lag and may miss the best entry point for rapid price reversal.
2. The stop loss range is relatively small and cannot withstand greater market fluctuations.
3. Relying only on the CCI indicator is susceptible to false breakthroughs and produces false signals.
4. Failure to effectively filter out shocks in trends will increase trading frequency and slippage costs.
5. The holding time of long and short positions is uncertain, and it is impossible to predict the time point of profit-taking.
In response to the above risks, we can improve and control them through parameter optimization, stop loss range adjustment, and adding filter conditions.
#### Optimization direction
There is room for further optimization of the CCI zero-point reversal trading strategy, which mainly includes:
1. Optimize CCI parameters and find indicator parameters that are more suitable for the characteristics of the variety.
2. Add price breakthrough or form conditions to filter out volatile situations and reduce false signals.
3. Add a trailing stop loss method to track profits, or a trailing stop profit with a preset profit ratio.
4. Combine with other indicators to form multi-indicator filtering conditions to improve strategy stability.
5. Increase your position when the trend becomes clearer, and reduce your position when it fluctuates.
Through parameter adjustment, risk control optimization, dynamic take-profit and other methods, the efficiency and profitability of the CCI zero-point reversal trading strategy can be further improved.
#### Summarize
The CCI Zero Point Reversal trading strategy is a simple and effective quantitative strategy based on the Commodity Channel Index. It takes advantage of the trend-following characteristics of the CCI indicator and gains profits by capturing its reversal nodes. The advantages of the strategy are mainly reflected in simple implementation, strong applicability, and few parameters, but it also faces certain risks, and it is necessary to introduce auxiliary technical indicators and optimization methods for control. Overall, the strategy process is clear and easy to expand, making it one of the quantitative trading strategies worth considering.
||

#### Overview

The CCI Zero Cross Trading Strategy is a quantitative trading strategy based on the Commodity Channel Index (CCI). It generates trading signals by tracking the crossover situations between the CCI indicator and the zero level. It establishes long positions when the CCI crosses above zero and short positions when the CCI falls below zero. The strategy belongs to the trend-following type.

#### Strategy Principle  

The basic principle of the CCI Zero Cross Trading Strategy is:

1. Use the CCI indicator to determine overbought and oversold conditions in the market. The CCI moving above 100 indicates an overbought signal while falling below -100 gives an oversold signal.  

2. Monitor the crossover situations between the CCI and the zero level. A buy signal is generated when the CCI crosses zero from below. A sell signal is generated when the CCI drops below zero from the top.

3. Enter trades based on the buy and sell signals from CCI's zero line crossovers, with stops set at the CCI overbought/oversold areas.

Specifically, the entry rules are:

1. When the CCI crosses from negative to positive values through the zero level, establish long positions with stops at -100.

2. When the CCI drops from positive to negative values through the zero level, go short with stops at +100.

The strategy mainly relies on the CCI indicator to determine overbought/oversold conditions in the market and aims to profit from capturing reversal opportunities. CCI's zero line crossovers can effectively identify mid-term trend reversal points. Overall, the logic is simple and easy to implement.

#### Advantage Analysis

The main advantages of the CCI Zero Cross Trading Strategy are:

1. The signal depends solely on CCI's zero line crossovers, enabling simple and effective trend tracking.  

2. It captures mid-term trend reversal points effectively based on CCI's reversal characteristics, giving large profit potential.

3. The stops are set at CCI overbought/oversold zones, allowing timely stop-outs and risk control.

4. The logic is simple and clear, easy to parameterize for algorithmic trading.

5. CCI is widely applicable across different markets, making the strategy highly adaptable.

#### Risk Analysis

The CCI Zero Cross Trading Strategy also has some risks:

1. CCI can lag prices, potentially missing optimal entry timing for fast reversals.

2. The stop range is relatively small and may fail to withstand larger price swings. 

3. Relying solely on CCI makes it vulnerable to false breakouts and wrong signals.  

4. It cannot effectively filter out range-bound price action and may increase trade frequency and slippage.

5. It does not define trade duration and profit targets.

These risks can be managed through parameter optimization, wider stops, adding filters etc.

#### Optimization Directions

Further optimizations for the strategy involve:  

1. Optimizing CCI parameters based on asset characteristics. 

2. Adding price breakout or pattern filters to avoid ranging markets.

3. Using trailing stops or take-profit levels to lock in profits.  

4. Combining other indicators to create robust multi-indicator filters.

5. Increasing position size in established trends and decreasing in ranges.

Through parameter tuning, risk controls, adaptive exits etc., the efficiency and profitability of the strategy can be significantly improved.

#### Conclusion

The CCI Zero Cross Trading Strategy is a simple and effective CCI-based quantitative strategy. It profits from trend-trading signals generated by detecting CCI reversal points. Its advantages lie in simplicity, adaptability and fewer parameters, but also has inherent risks that need to be addressed through additional techniques. Overall, it has clear logic and room for extensions, making it a worthwhile addition to a quantitative trader's playbook.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|CCI Period Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-30 00:00:00
end: 2023-12-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("CCI 0Trend Strategy (by Marcoweb) v1.0", shorttitle="CCI_0T_Strat_v1.0", overlay=true)

///////////// CCI
CCIlength = input(20, minval=1, title="CCI Period Length") 
CCIoverSold = -100
CCIoverBought = 100
CCIzeroLine = 0
CCI = cci(hlc3, CCIlength)
price = hlc3
vcci = cci(price, CCIlength)

source = close
buyEntry = crossover(source, CCIoverSold)
sellEntry = crossunder(source, CCIoverBought)
plot(CCI, color=black,title="CCI")
p1 = plot(CCIoverSold, color=red,title="-100")
p2 = plot(CCIoverBought, color=blue,title="100")
p3 = plot(CCIzeroLine, color=orange,title="0")

///////////// CCI 0Trend v1.0 Strategy 
if (not na(vcci))

    if (crossover(CCI, CCIoverSold))
        strategy.entry("CCI_L", strategy.long, stop=CCIoverSold,  comment="CCI_L")
    else
        strategy.cancel(id="CCI_L")
        
    if (crossunder(CCI, CCIoverBought))
        strategy.entry("CCI_S", strategy.short, stop=CCIoverBought,  comment="CCI_S")
    else
        strategy.cancel(id="CCI_S")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/434612

> Last Modified

2023-12-07 18:18:41
