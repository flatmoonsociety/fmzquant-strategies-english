
> Name

4-Hour-CCI-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy is a reversal trading strategy based on the CCI indicator. It will conduct reverse trading when the CCI indicator appears in the overbought and oversold zone. Overall, this strategy uses the overbought and oversold characteristics of the CCI indicator to capture price reversal opportunities for trading.
### Strategy Principles
First, the strategy is based on the CCI indicator. The calculation formula of CCI index is:
CCI = (Typical Price - Simple Moving Average) / (0.015 * Mean Error)
Among them,
Typical Price = (Highest Price + Lowest Price + Closing Price)/3
Simple moving average = moving average of Typical Price over the past N days
Mean square error = mean of the sum of squares of Typical Price deviations in the past N days
This strategy uses the CCI indicator with a length of 11. And set -150 as the oversold zone and 150 as the overbought zone.
At the closing of each K line, the CCI indicator with a length of 11 will be detected. If CCI crosses below -150, a long signal is issued; if CCI crosses above 150, a short signal is issued.
After receiving the signal, open a position with a market order. And set a 1% take profit and a 0.5% stop loss.
### Strategic Advantages
1. Using the CCI indicator can effectively capture price reversal opportunities.
2. CCI parameters are adjustable and better parameters can be tested
3. Adopting a fixed proportion of stop-profit and stop-loss can effectively control risks
4. The strategy logic is simple and clear, easy to understand and implement
### Risks and Solutions
1. The CCI indicator can generate a large number of false signals, and the signals entering the market may not be reliable.
- Solution: Optimize CCI parameters and combine filtering with other indicators
2. Fixed take-profit and stop-loss ratios, parameters for different varieties may not be reasonable.
- Solution: Add dynamic stop-profit and stop-loss
3. The strategy is only based on CCI, has single risk and is prone to failure.
- Solution: Multiple indicator combinations to improve stability
4. Without considering transaction costs, the actual offer effect may be poor.
- Solution: Add slippage control to reduce transaction frequency
### Optimization direction
1. Optimize the parameters of CCI and find a better parameter combination
2. Add other indicators such as MACD, KDJ and other indicators to filter the market entry
3. Develop a dynamic stop-profit and stop-loss mechanism instead of a simple fixed ratio
4. Optimize strategies to reduce transaction frequency to reduce the impact of transaction costs
5. Carry out backtest optimization to find the optimal parameter combination and prepare for real trading.
### Summarize
The 4-hour CCI reversal strategy is overall a simple strategy that uses the CCI indicator for reversal trading. It has the advantages of clear strategic logic and easy implementation. However, there are also shortcomings such as unstable CCI signals and inflexible take-profit and stop-loss. By optimizing CCI parameters, adding filter indicators, and developing dynamic stop-profit and stop-loss, the effect of this strategy can be further enhanced. Generally speaking, this strategy provides an idea based on the CCI indicator for quantitative trading, but it needs further optimization before it can be applied in real markets.
||


### Overview

This is a reversal trading strategy based on the CCI indicator. It will open reverse trades when the CCI indicator shows overbought or oversold levels. Overall, this strategy utilizes the overbought and oversold features of the CCI indicator to capture price reversal opportunities.

### Strategy Logic

Firstly, this strategy is based on the CCI indicator. The CCI indicator formula is:

CCI = (Typical Price - Simple Moving Average) / (0.015 * Standard Deviation)

Where,
Typical Price = (Highest + Lowest + Close) / 3
Simple Moving Average = Moving average of Typical Price over past N days  
Standard Deviation = Square root of variance of Typical Price over past N days

This strategy uses a 11-period CCI indicator. And -150 is set as the oversold level, while 150 as the overbought level.

On every bar close, the 11-period CCI indicator will be checked. If CCI crosses below -150, a long signal is generated. If CCI crosses above 150, a short signal is generated.

After receiving the signal, market order will be used to open position. 1% profit target and 0.5% stop loss are set.

### Advantage Analysis  

1. Using CCI indicator can effectively capture price reversal opportunities
2. CCI parameters are adjustable for optimization
3. Fixed profit target and stop loss ratio effectively controls risk 
4. Simple and clear strategy logic, easy to understand and implement

### Risk Analysis

1. CCI indicator may generate lots of false signals, entry signals may not be reliable
- Solution: Optimize CCI parameters, add filter with other indicators

2. Fixed profit target and stop loss ratio may not suit different products
- Solution: Add dynamic profit target and stop loss 

3. Strategy relies solely on CCI, risk of ineffectiveness is high
- Solution: Combine multiple indicators to improve robustness 

4. No consideration on trading cost, live performance may suffer
- Solution: Add slippage control, reduce trading frequency

### Optimization Directions

1. Optimize CCI parameters to find better parameter combinations
2. Add other indicators like MACD, KDJ for signal filtering 
3. Develop dynamic profit target and stop loss instead of fixed ratio
4. Optimize strategy to lower trading frequency, reducing trading cost impact
5. Conduct backtesting optimization to find best parameter combination for live trading

### Summary

The 4-hour CCI reversal strategy is a simple strategy utilizing CCI indicator for reversal trading. It has the advantage of clear logic and easy implementation. But it also has weaknesses like unreliable CCI signals and inflexible profit target/stop loss. Further improvements can be made by optimizing CCI parameters, adding filter indicators, developing dynamic exits, etc. Overall this strategy provides a CCI-based idea for quantitative trading, but requires further optimization before live application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|11|length|
|v_input_2|-150|overSold|
|v_input_3|150|overBought|
|v_input_4|15|Timeframe|
|v_input_5|16|Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-12 00:00:00
end: 2023-10-12 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("4H CCI Strategy", overlay=true)
length = input( 11 )
overSold = input( -150 )
overBought = input( +150 )
price1 = high
price2 = low
ucci = cci(price1, length)
dcci = cci(price2, length)
vcci = cci(ohlc4, 11)

resCustom = input(title="Timeframe", defval="15")
Length = input(16, minval=1)
xPrice = request.security(syminfo.tickerid, resCustom, hlc3)
xvnoise = abs(xPrice - xPrice[1])
nfastend = 0.666
nslowend = 0.0645
nsignal = abs(xPrice - xPrice[Length])
nnoise = sum(xvnoise, Length)
nefratio = iff(nnoise != 0, nsignal / nnoise, 0)
nsmooth = pow(nefratio * (nfastend - nslowend) + nslowend, 2) 
nAMA = nz(nAMA[1]) + nsmooth * (xPrice - nz(nAMA[1]))
basis1 = nAMA
slope = change(basis1,1)

if (not na(vcci))
    if (crossover(dcci, overSold))
        strategy.entry("CCILE", strategy.long, comment="CCILE")
        strategy.exit("exit", "CCILE", profit = 0.01, loss = 0.005)
    if (crossunder(ucci, overBought))
        strategy.entry("CCISE", strategy.short, comment="CCISE")
        strategy.exit("exit", "CCISE", profit = 0.01, loss = 0.005)
//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/429145

> Last Modified

2023-10-13 15:29:05
