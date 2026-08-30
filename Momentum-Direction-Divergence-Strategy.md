
> Name

Momentum-Direction-Divergence-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7d1bc0ab35cff150285edc1ddaad16d9fd6245e51e355983dd3e7312925f274c.png)
[trans]

## Overview
The Momentum Direction Divergence Strategy is one of the techniques described by William Blau in his book Momentum, Direction and Divergence. This strategy focuses on three key aspects: momentum, direction, and divergence. Mr. Blau, an electrical engineer turned trader, delved into the relationship between price and momentum. On this basis, he analyzed the shortcomings of other oscillators and introduced some innovative techniques, including a new bullish oscillator interpretation. On the issue of directionality, he analyzes the complexities of ADX and provides a unique approach to help define trending and non-trending cycles.
This strategy plots the momentum directional divergence index (Ergotic CSI) and its smooth line to filter out noise.
## Strategy Principle
The beginning of the code defines an adaptive dynamic index (ADX) function fADX, which accepts the parameter Len to represent the smoothing period. This function calculates the gated moving average (RMA) of the true range (TR) as the denominator, calculates the RMA of bull momentum and short momentum as the numerator, and divides them to get a ratio, which represents the relative strength of the bulls and bears. Finally, the value of ADX is obtained by combining the long strength and short strength through a formula.
Then comes the definition of strategy parameters. r represents the smoothing parameter of ATR, Length represents the length of ADX, BigPointValue represents the large point value, SmthLen represents the length of smoothed CSI, SellZone and BuyZone represent the qualified selling and buying areas. reverse indicates whether to reverse the trading signal.
The key logic is in calculating CSI. First calculate the true fluctuation range ATR and ADX. Then the penalty coefficient K is calculated, including the consideration of large point values, ATR and ADX. Calculate the standardized residual nRes, which combines the information of ATR, ADX and closing price. Finally, calculate the CSI value, and then find its smooth SMA.
Determine the trading direction based on the SMA value of CSI. If it is higher than BuyZone, go long; if it is lower than SellZone, go short. Plot the CSI curve and its SMA, and color-code the different trading ranges.
## Advantage Analysis
This strategy combines the advantages of the momentum indicator ATR and the trend indicator ADX, taking into account both market volatility and the degree of trend, and avoids the limitations of using only ATR and only ADX. The design of the penalty coefficient K cleverly integrates the relationship between these indicators and large point values.
The standardized residual nRes adds the use of price information, focusing not only on the momentum trend, but also on the absolute level of the price. This is different from the general oscillator and enhances the expressiveness of the strategy.
Smoothing processing and segment judgment provide clear trading signals for strategic decision-making, which is conducive to real-time operations.
## Risk Analysis
This strategy is sensitive to parameter settings, such as the cycle length of ATR and ADX, the setting of large point values, CSI smoothing parameters, etc., which will all affect the performance of the strategy. Extensive backtesting is required to determine the appropriate combination of parameters.
As a newly proposed oscillator, CSI's effectiveness needs to be verified in more different markets. If the indicator is not effective, it will affect strategy profitability.
The strategy itself does not have a stop-loss mechanism. Directly follow the CSI signal to go long and short. There is a certain degree of risk and it needs to be used in combination with stop-loss.
## Optimization direction
You can test parameter combinations in different markets to find a more general combination.
A dynamic ADX cycle length mechanism can be introduced to adjust the parameters of ADX according to market conditions.
It can be combined with other oscillator indicators to determine the timing of buying and selling to make the strategy more robust. Such as bottom divergence, top divergence and other effects.
A stop loss strategy can be added to make the overall strategy more complete.
## Summarize
The momentum directional divergence strategy integrates the advantages of multiple indicators, using multiple dimensions of price, momentum, and trend to design CSI indicators and conduct transactions. This strategy has flexible parameter settings and strong expressiveness. It deserves further testing and optimization, and can become a beneficial tool for quantitative trading.
||

## Overview  

The Momentum Direction Divergence Strategy is one of the techniques described by William Blau in his book "Momentum, Direction and Divergence". The strategy focuses on three key aspects: momentum, direction and divergence. Blau, who was an electrical engineer before becoming a trader, thoroughly examines the relationship between price and momentum. From this grounding, he then looks at the deficiencies in other oscillators and introduces some innovative techniques, including a fresh twist on Stochastics. On directional issues, he analyzes the intricacies of ADX and offers a unique approach to help define trending and non-trending periods.  

The strategy plots Ergotic CSI and its smoothed line to filter out noise.

## Strategy Logic  

The code starts by defining an Adaptive Direction Index (ADX) function fADX, which takes parameter Len as the smoothing period. The function calculates the RMA of True Range (TR) as denominator, and RMA of upside momentum and downside momentum as numerator, then divides them to get ratios indicating the relative strength of upside and downside. Finally, ADX is obtained by combining upside strength and downside strength.  

Then strategy parameters are defined. r is the smoothing parameter for ATR, Length is the length of ADX, BigPointValue is big point value, SmthLen is the smoothing length for CSI, SellZone and BuyZone are sell and buy zones that meet the criteria. reverse indicates whether to reverse the trading signals.

The key logic is in CSI calculation. First ATR and ADX are computed. Then the penalty coefficient K is calculated, incorporating considerations of big point value, ATR and ADX. The standardized residual nRes combines information from ATR, ADX and close price. Finally CSI value is obtained, and its SMA is calculated.  

Trading direction is determined according to SMA value of CSI. Go long if above BuyZone, go short if below SellZone. Plot CSI curve and its SMA, color code different trading zones.  

## Advantage Analysis  

The strategy combines the advantages of momentum indicator ATR and trend indicator ADX, considering both market volatility and trend strength, avoiding limitations of using ATR or ADX alone. The design of penalty coefficient K cleverly integrates the relationships between these indicators and big point value.

The standardized residual nRes incorporates price information, paying attention not only to momentum trend but also absolute price level, which is different from typical oscillators, enhancing the strategy's performance.  

The smoothing process and zone determination provide clear trading signals for practical trading.

## Risk Analysis  

The strategy is quite sensitive to parameter settings like periods of ATR and ADX, big point value etc., which can affect performance. Extensive backtests are needed to determine proper parameter combinations.  

As a newly proposed oscillator, the efficacy of CSI needs validation across more diverse markets. Poor CSI performance would hurt strategy profitability.

The strategy itself does not have a stop loss mechanism, just directly long or short per CSI signals. There are risks that need to be mitigated by incorporating stop loss.

## Optimization Directions   

Test parameter combinations across different markets to find relatively universal settings.  

Introduce a dynamic ADX period mechanism adjusting ADX parameters based on market states.  

Incorporate other oscillator indicators to determine entries and exits to make the strategy more robust. Effects like bottom divergence, top divergence can be useful.  

Add stop loss mechanisms to complete the strategy.

## Summary   

The Momentum Direction Divergence Strategy integrates advantages of multiple indicators, utilizing price, momentum, trend dimensions to design CSI indicator for trading. With flexible parameter settings and strong capacity, the strategy deserves further testing and optimization, and can become a beneficial quantitative trading tool.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|32|r|
|v_input_2|true|Length|
|v_input_3|true|BigPointValue|
|v_input_4|5|SmthLen|
|v_input_5|0.004|SellZone|
|v_input_6|0.024|BuyZone|
|v_input_7|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-20 00:00:00
end: 2023-12-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 20/06/2018
// This is one of the techniques described by William Blau in his book 
// "Momentum, Direction and Divergence" (1995). If you like to learn more, 
// we advise you to read this book. His book focuses on three key aspects 
// of trading: momentum, direction and divergence. Blau, who was an electrical 
// engineer before becoming a trader, thoroughly examines the relationship between 
// price and momentum in step-by-step examples. From this grounding, he then looks 
// at the deficiencies in other oscillators and introduces some innovative techniques, 
// including a fresh twist on Stochastics. On directional issues, he analyzes the 
// intricacies of ADX and offers a unique approach to help define trending and 
// non-trending periods.
// This indicator plots Ergotic CSI and smoothed Ergotic CSI to filter out noise. 
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
fADX(Len) =>
    up = change(high)
    down = -change(low)
    trur = rma(tr, Len)
    plus = fixnan(100 * rma(up > down and up > 0 ? up : 0, Len) / trur)
    minus = fixnan(100 * rma(down > up and down > 0 ? down : 0, Len) / trur)
    sum = plus + minus 
    100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), Len)

strategy(title="Ergodic CSI Backtest")
r = input(32, minval=1)
Length = input(1, minval=1)
BigPointValue = input(1.0, minval=0.00001)
SmthLen = input(5, minval=1)
SellZone = input(0.004, minval=0.00001)
BuyZone = input(0.024, minval=0.001)
reverse = input(false, title="Trade reverse")
hline(BuyZone, color=green, linestyle=line)
hline(SellZone, color=red, linestyle=line)
source = close
K = 100 * (BigPointValue / sqrt(r) / (150 + 5))
xTrueRange = atr(1) 
xADX = fADX(Length)
xADXR = (xADX + xADX[1]) * 0.5
nRes = iff(Length + xTrueRange > 0, K * xADXR * xTrueRange / Length,0)
xCSI = iff(close > 0,  nRes / close, 0)
xSMA_CSI = sma(xCSI, SmthLen)
pos = iff(xSMA_CSI > BuyZone, 1,
       iff(xSMA_CSI <= SellZone, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(xCSI, color=green, title="Ergodic CSI")
plot(xSMA_CSI, color=red, title="SigLin")
```

> Detail

https://www.fmz.com/strategy/436767

> Last Modified

2023-12-27 15:37:31
