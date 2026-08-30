
> Name

Rate-of-Change-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy determines when to buy and sell by calculating the rate of change over a certain period of time. It helps traders take advantage of short-term price movements.
## Strategy Principle
This strategy is mainly based on the following indicators:
1. Quick simple moving average (default 14 days): used to determine the short-term trend of prices
2. Slow simple moving average (default 100 days): used to determine the long-term trend of prices
3. Refer to the simple moving average (default 30 days): used to determine the general direction of buying and selling.
4. Rate of change: Determine the extent of price fluctuations by calculating the changes in the highest and lowest prices in a certain period in the past (default 12 K lines)
Specific buying rules:
1. Price is below the reference simple moving average
2. The change rate is higher than the set low change rate threshold (default 2.3%)
3. The fast SMA is rising and the slow SMA is falling, indicating that the two curves may cross.
Specific selling rules:
1. Price is above the reference simple moving average
2. The change rate is higher than the set high change rate threshold (default 4.7%)
3. The price rises 3 consecutive K lines
4. Currently profitable
5. Fast SMA is higher than slow SMA
The order size is set based on the percentage of total equity (default 96%), which can provide leverage.
## Strategic advantage analysis
This strategy mainly has the following advantages:
1. By using the rate of change to judge fluctuations, you can seize the opportunity of rapid rise or fall in short-term prices and achieve higher returns.
2. Combined with fast and slow SMA to judge the trend, you can more accurately grasp the timing of buying low and selling high.
3. Set the reference SMA as a general direction guide to avoid being misled by the short-term market prices.
4. Use trailing stops to lock in profits and reduce downside risks.
5. The order size provides a leverage effect and can amplify profits.
Generally speaking, this strategy makes full use of tools such as price change rate and SMA indicators, and can achieve better performance in volatile markets.
## Risk Analysis
This strategy also has the following risks:
1. Improper setting of change rate and SMA parameters may lead to missed or incorrect trading signals. Parameters need to be adjusted for different markets.
2. Excessive order size will amplify risks. It is recommended to optimize the order ratio during the testing phase.
3. Trailing stop loss may stop loss prematurely in volatile market conditions. Consider adjusting the stop loss range.
4. Strategy transactionsstab can walk the market and is susceptible to arbitrage. Risk management should be combined with trend judgment and stop loss.
5. Backtest data fitting risks. The robustness of the strategy should be verified multiple times in different markets.
For these risks, risk control can be carried out through parameter optimization, order adjustment, stop loss strategy optimization, real offer verification and other means.
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Add other technical indicator judgments, such as volatility, trading volume, etc., to improve signal accuracy.
2. Optimize the number of transactions and reduce the impact of transactionsstab market prices by reducing transaction frequency.
3. Combined with the breakout strategy, set up breakout trading signals near key price levels.
4. Use machine learning methods to automatically optimize parameter settings.
5. Test the robustness of the strategy in multiple markets and time periods to improve adaptability.
6. Consider the characteristics of different varieties such as stocks and foreign exchange, and set special parameter combinations.
7. Continuously iteratively optimize strategic signals and risk control methods based on real trading results.
## Summarize
This strategy uses the rate of change and SMA indicators to judge and look for trading opportunities in short-term price fluctuations. It is conducive to seizing fast market trends, but it also requires attention to risk control. Through parameter optimization, order adjustment, stop-loss strategy improvement and real-time verification, the robustness and adaptability of the strategy can be continuously improved. This strategy provides a reference template for quantitative trading, but in actual application it needs to be adjusted and optimized according to market characteristics.
||


## Overview

This strategy calculates the rate of change over time to determine buy/sell signals. It can help traders capture opportunities in short-term price fluctuations.

## Strategy Logic

The strategy is mainly based on the following indicators:

1. Fast Simple Moving Average (default 14 days): to gauge short-term trend
2. Slow Simple Moving Average (default 100 days): to gauge long-term trend
3. Reference Simple Moving Average (default 30 days): to determine overall direction
4. Rate of Change: calculated based on highest/lowest price over lookback period (default 12 bars) to judge magnitude of price fluctuation

Specific entry rules:

1. Price below reference SMA
2. ROC above preset low ROC threshold (default 2.3%) 
3. Fast SMA rising and slow SMA falling, indicating potential crossover

Specific exit rules:

1. Price above reference SMA
2. ROC above preset high ROC threshold (default 4.7%)
3. 3 consecutive rising bars  
4. Current profit > 0
5. Fast SMA above slow SMA

Position size is percentage (default 96%) of total equity for leverage.

## Advantage Analysis 

The strategy has the following advantages:

1. Using ROC to detect swings allows capturing upside/downside moves for higher returns.

2. Combining fast/slow SMA helps more accurately identify low/high points. 

3. Reference SMA provides overall direction to avoid distraction from short-term noise.

4. Trailing stop loss locks in profits and reduces downside risk.

5. Leverage from position sizing amplifies profits.

Overall, the strategy utilizes ROC, SMA and other tools effectively to capitalize on price oscillations. It can achieve good results in volatile markets.

## Risk Analysis

The strategy also has the following risks:

1. Incorrect ROC and SMA parameters may cause missed signals or bad trades. Optimization is needed for different markets.

2. Excessive position size increases risk. Order percentage should be tested and tuned.

3. Trailing stop loss may exit prematurely in choppy markets. Stop loss percentage can be adjusted.

4. Prone to whipsaws in ranging markets. Should incorporate trend filters and risk management. 

5. Backtest overfitting risk. Robustness should be verified through live trading across markets.

Risks can be managed through parameter optimization, position sizing, stop loss adjustments, robustness testing etc.

## Optimization Directions

The strategy can be improved in the following aspects:

1. Add other technical indicators like volatility, volume to improve signal accuracy.

2. Optimize number of trades by reducing trading frequency to minimize whipsaw impacts.

3. Incorporate breakout techniques around key price levels.

4. Use machine learning to auto optimize parameters.

5. Test robustness across different markets and time frames. 

6. Tune specialized parameters for different products like stocks, forex etc.

7. Continuously refine signals and risk controls based on live results.

## Summary

This strategy identifies trading opportunities around short-term oscillations using ROC and SMA analysis. It helps capitalize on quick swings but also requires proper risk controls. Fine tuning parameters, position sizing, stop losses and robustness testing can enhance its stability and adaptability. The strategy serves as a reference template for quantified trading but needs customization for different markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|SMA Fast (days)|
|v_input_2|100|SMA Slow (days)|
|v_input_3|30|SMA Reference (days)|
|v_input_4|0.023|ROC Low (%)|
|v_input_5|0.047|ROC High (%)|
|v_input_6|0.96|Order Stake (%)|
|v_input_7|12|Lookback Candles|
|v_input_8|3.62|Trailing Stoploss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-21 00:00:00
end: 2023-09-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// @version=4
// Author: Sonny Parlin (highschool dropout)
// Best if run on 5m timeframe
strategy(shorttitle="ROC+Strategy", title="Rate of Change Strategy",
                                      overlay=true,  currency=currency.USD,
                                      initial_capital=10000)

// Inputs and variables
ss = input(14, minval=10, maxval=50, title="SMA Fast (days)")
ff = input(100, minval=55, maxval=200, title="SMA Slow (days)")
ref = input(30, minval=20, maxval=50, title="SMA Reference (days)")
lowOffset = input(0.023, "ROC Low (%)", minval=0, step=0.01)
highOffset = input(0.047, "ROC High (%)", minval=0, step=0.01)
orderStake = input(0.96, "Order Stake (%)", minval=0, step=0.01)
lookback = input(12, "Lookback Candles", minval=1, step=1) 

// SMA
smaFast = sma(close, ss)
smaSlow = sma(close, ff)
smaRef = sma(close, ref)
ROC = (max(close[lookback],close) - min(close[lookback],close)) / max(close[lookback],close)

// Set up SMA plot but don't show by default
plot(smaFast, "smaFast", color=#00ff00, display = 0)
plot(smaSlow, "smaSlow", color=#ff0000, display = 0)
plot(smaRef, "smaRef", color=#ffffff, display = 0)

// The buy stratey:
// Guard that the low is under our SMA Reference line 
// Guard that the rate of change over the lookback period is greater than our 
// ROC lowOffset %, default is 0.023. (low < smaRef) and (ROC > lowOffset)
// SMA fast is on the rise and SMA slow is falling and they are very likely
// to cross. (rising(smaFast,1)) and (falling(smaSlow, 1)) 
enterLong = (low < smaRef) and (ROC > lowOffset) and (rising(smaFast,1)) and (falling(smaSlow,1)) 

// The sell Strategy:
// Guard that close is higher than our SMA reference line and that the rate of 
// change over the lookback period is greater than our highOffset %, default
// is 0.047. (close > smaRef) and (ROC > highOffset)
// Guard that close has risen by 3 candles in a row (rising(close,3)) 
// Guard that we currently have profit (strategy.openprofit > 0)
// Guard that SMA fast is higher than smaSlow (smaFast > smaSlow)
// If it keeps going up past our close position the trailing stoploss will kick in!
enterShort = (close > smaRef) and (ROC > highOffset) and (rising(close,3)) and (strategy.openprofit > 0) and (smaFast > smaSlow)

// Order size is based on total equity
// Example 1:
// startingEquity = 2000
// close = 47434.93
// orderStake = 0.45
// (2,000 × orderStake) / close = orderSize = 0.0189733599 = approx $900

// Example 2:
// startingEquity = 2000
// close = 1.272
// orderStake = 0.45
// (startingEquity × orderStake) / close = orderSize = 707.5471698113 = approx $900
orderSize = (strategy.equity * orderStake) / close

// Trailing Stoploss
// I'm using 2.62 as my default value, play with this for different results.
longTrailPerc = input(title="Trailing Stoploss (%)",
     type=input.float, minval=0.0, step=0.1, defval=3.62) * 0.01
     
longStopPrice = 0.0

longStopPrice := if (strategy.position_size > 0)
    stopValue = close * (1 - longTrailPerc)
    max(stopValue, longStopPrice[1])
else
    0

if (enterLong)
    strategy.entry("Open Long Position", strategy.long, orderSize, when=strategy.position_size <= 0)
    
if (enterShort)
    strategy.exit(id="Close Long Position", stop=longStopPrice)


//plot(strategy.equity)
```

> Detail

https://www.fmz.com/strategy/428060

> Last Modified

2023-09-28 11:26:44
