
> Name

Dynamic-Liquidity-Cascade-Capture-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d97bca43c4d813fa7dfb.png)
![IMG](https://www.fmz.com/upload/asset/2d933f58cfeb8f853e688.png)

[trans]
#### Overview
This strategy is a quantitative trading system specifically designed to capture periods of extreme market volatility. It monitors the deviation between price and the moving average to identify possible liquidity depletion in the market, thereby capturing market reversal opportunities. The strategy uses moving average combination, volatility tracking and dynamic stop loss mechanism to build a complete trading system.
#### Strategy Principle
The core of the strategy is to identify market anomalies by calculating the deviation of price from the moving average. Specific implementations include:
1. Use a combination of the 15-period simple moving average (SMA) and the 30-period exponential moving average (EMA) as the base price
2. Calculate the percentage deviation between the current price and the moving average combination
3. Determine historical extreme values through the highest and lowest values of 89 periods
4. Enter the long position when the long-position liquidity is exhausted three times in a row.
5. A triple exit mechanism is set up: technical rebound, reverse liquidity depletion signal and trailing stop loss
#### Strategic Advantages
1. Precise market timing: improve entry accuracy through multiple indicator confirmations
2. Improved risk control: adopt a multi-level stop-loss mechanism to effectively control downside risks
3. Strong adaptability: the strategy can automatically adjust the stop loss range according to market volatility
4. Strong execution: The strategy sets clear entry and exit conditions to reduce subjective judgments
5. High degree of systematization: the entire trading process is based on quantitative indicators and is easy to automate
#### Strategy Risk
1. False signal risk: False liquidity depletion signals may be generated in sideways markets
2. Slippage risk: Under extreme market conditions, you may face greater execution slippage.
3. Parameter sensitivity: The strategy effect is more sensitive to the moving average period and stop loss multiple.
4. Market environment dependence: In a low volatility environment, strategic returns may not be ideal.
5. Technical risk: system stability needs to be ensured to avoid signal delay or loss
#### Strategy optimization direction
1. Introducing trading volume indicators: Confirm the effectiveness of liquidity depletion signals through trading volume
2. Optimization parameter adaptation: dynamically adjust strategy parameters according to market fluctuations
3. Add market environment filtering: suspend trading in unsuitable market conditions
4. Improve the stop loss mechanism: consider adding a dynamic stop loss based on volatility
5. Optimize the signal confirmation mechanism: add more technical indicators to filter out false signals
#### Summary
The dynamic liquidity cascade capture strategy is a quantitative trading system focused on capturing market extremes. Through scientific indicator combinations and strict risk control, the strategy can capture trading opportunities when the market fluctuates violently. Although there are certain risks, through continuous optimization and improvement, the strategy is expected to maintain stable performance in various market environments.
|| 

#### Overview
This strategy is a quantitative trading system specifically designed to capture extreme market volatility periods. It monitors the deviation between price and moving averages to identify potential market liquidity exhaustion situations and capture market reversal opportunities. The strategy incorporates moving average combinations, volatility tracking, and dynamic stop-loss mechanisms to build a complete trading system.

#### Strategy Principles
The core of the strategy is to identify market anomalies by calculating the deviation between price and moving averages. Specific implementation includes:
1. Using a combination of 15-period Simple Moving Average (SMA) and 30-period Exponential Moving Average (EMA) as benchmark prices
2. Calculating the percentage deviation between current price and moving average combination
3. Determining historical extremes through 89-period highs and lows
4. Entering long positions when three consecutive long-side liquidity exhaustion signals occur
5. Implementing a triple exit mechanism: technical rebound, reverse liquidity exhaustion signals, and trailing stop-loss

#### Strategy Advantages
1. Precise Market Timing: Multiple indicator confirmation improves entry accuracy
2. Comprehensive Risk Control: Multi-layered stop-loss mechanism effectively controls downside risk
3. High Adaptability: Strategy automatically adjusts stop-loss range based on market volatility
4. Strong Execution: Clear entry and exit conditions reduce subjective judgment
5. High Systematization: Entire trading process is based on quantitative indicators, easy to automate

#### Strategy Risks
1. False Signal Risk: May generate incorrect liquidity exhaustion signals in sideways markets
2. Slippage Risk: May face significant execution slippage under extreme market conditions
3. Parameter Sensitivity: Strategy performance is sensitive to moving average periods and stop-loss multipliers
4. Market Environment Dependency: Strategy returns may be suboptimal in low volatility environments
5. Technical Risk: System stability must be maintained to avoid signal delays or losses

#### Strategy Optimization Directions
1. Incorporate Volume Indicators: Confirm liquidity exhaustion signals through volume analysis
2. Optimize Parameter Adaptivity: Dynamically adjust strategy parameters based on market volatility states
3. Add Market Environment Filters: Pause trading in unsuitable market conditions
4. Enhance Stop-Loss Mechanism: Consider adding volatility-based dynamic stop-loss
5. Improve Signal Confirmation: Add more technical indicators to filter false signals

#### Summary
The Dynamic Liquidity Cascade Capture Strategy is a quantitative trading system focused on capturing extreme market situations. Through scientific indicator combinations and strict risk control, the strategy can capture trading opportunities during intense market volatility. While certain risks exist, through continuous optimization and improvement, the strategy has the potential to maintain stable performance across various market environments.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-22 00:00:00
end: 2025-02-19 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Liquidation Cascade Strategy", overlay=true)

// Paramètres de l'indicateur de liquidation
var float lastHigh = na
var float lastLow = na
var float lastPriceLow = na
var float lastPriceHigh = na
var bool shortLiq = na
var bool longLiq = na

src = close
maLength1 = 15
maLength2 = 30
ma1 = ta.sma(src, maLength1)
ma2 = ta.ema(src, maLength2)
avgLine = (ma1 + ma2) / 2
distVal = ((src - avgLine) / avgLine) * 100

ph = ta.highest(distVal, 89)
pl = ta.lowest(distVal, 89)

if ph == distVal and ph > 0 
    lastHigh := distVal
    lastPriceHigh := high

if pl == distVal and pl < 0 
    lastLow := distVal
    lastPriceLow := low

shortLiq := not na(lastHigh) and lastHigh == distVal and distVal > 0
longLiq := not na(lastLow) and lastLow == distVal and distVal < 0

// Condition d'achat : 3 liquidations longues consécutives
buyCondition = ta.valuewhen(longLiq, longLiq, 0) and ta.valuewhen(longLiq, longLiq, 1) and ta.valuewhen(longLiq, longLiq, 2)
if (buyCondition)
    strategy.entry("Buy", strategy.long)

// Conditions de vente
var float entryPrice = na
var bool positionOpen = false

// Mise à jour du prix d'entrée
if (buyCondition)
    entryPrice := close
    positionOpen := true

// 1. Vente sur rebond technique (distVal > -1%)
sellCondition1 = distVal > -1 and positionOpen

// 2. Vente sur liquidation courte
sellCondition2 = shortLiq and positionOpen

// 3. Trailing Stop (2x ATR)
atr = ta.atr(14)
trailingStop = close - 2 * atr
sellCondition3 = close < trailingStop and positionOpen

// Exécution des ventes
if (sellCondition1 or sellCondition2 or sellCondition3)
    strategy.close("Buy")
    positionOpen := false

// Visualisation
plot(avgLine, color=color.blue, title="Avg Line")
plot(distVal, color=distVal > 0 ? color.red : color.green, style=plot.style_columns)
```

> Detail

https://www.fmz.com/strategy/483051

> Last Modified

2025-02-24 15:16:23
