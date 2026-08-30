
> Name

Trend Persistence Analysis Strategy of Moving Average Momentum Hybrid Trading System-Hybrid-EMA-Momentum-Trading-System-with-Trend-Persistence-Analysis-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/104746c52a489785d68.png)


[trans]
#### Overview
This strategy is a hybrid trading system based on multiple technical indicators, combining the moving average (EMA), the relative strength indicator (RSI) and the super trend (SuperTrend) to capture market trends. The strategy uses fixed parameter settings and is optimized specifically for the 2-hour timeframe, identifying trends through a 21/55/200 period moving average system, while managing risk by combining RSI (14) momentum filters and SuperTrend (3,14) stops. The strategy also requires a 1.5x breakout in volume and confirmation of volatility via ATR, thus increasing the reliability of the trade.
#### Strategy Principle
The core logic of the strategy is based on a multi-layer technical analysis framework:
1. The trend identification system uses triple moving averages (21/55/200 periods) to determine the trend direction through moving average crossovers and position relationships.
2. The momentum confirmation system uses the RSI(14) indicator and combines it with its moving average to filter out false breakthroughs
3. The risk control system integrates the SuperTrend indicator as a dynamic stop loss and sets a 6-hour trading cooling period.
4. The trading trigger condition requires that the trading volume exceeds 1.5 times the 20-period average, and the ATR needs to be higher than its 48-period average.
#### Strategic Advantages
1. Parameter optimization: using pre-optimized fixed parameters, no need for frequent adjustments
2. Trend Grasping: Through the cooperation of multiple technical indicators, sustainable trends can be effectively captured
3. Risk control: Built-in transaction cooling mechanism to avoid excessive trading
4. Market adaptability: perform well in volatile markets
5. Transaction confirmation: multiple condition filtering to improve the reliability of trading signals
#### Strategy Risk
1. Short gap risk: In a 24-hour trading market, you may face losses caused by short gaps.
2. News impact: Major news events may cause violent price fluctuations and affect strategy performance.
3. Stop loss rigidity: fixed stop loss settings may not be flexible enough
4. Dependence on market environment: Frequent false signals may occur in a consolidating market
5. Slippage risk: You may face greater slippage in less liquid markets
#### Strategy optimization direction
1. Dynamic parameter adjustment: SuperTrend parameters can be automatically adjusted according to market volatility
2. Market environment identification: Add a market environment judgment module and adopt different parameter settings under different market conditions.
3. Stop loss optimization: Introduce a dynamic stop loss mechanism and adaptively adjust the stop loss position according to market volatility
4. Enhanced trading volume analysis: Add a more complex trading volume analysis model to improve the accuracy of trading signals.
5. Risk management optimization: Introduce a dynamic position management system and adjust positions according to the market environment
#### Summary
This strategy builds a relatively complete trading system through the combination of multiple technical indicators. Its advantage is that it can effectively capture market trends and improve the reliability of transactions through multiple conditional filters. Although there are some inherent risks, there is room for improvement in the overall performance of the strategy through optimization and improvement. The strategy is particularly suitable for use in volatile markets, but you need to pay attention to changes in the market environment and risk control.
|| 

#### Overview
This strategy is a hybrid trading system that combines multiple technical indicators, including Exponential Moving Averages (EMA), Relative Strength Index (RSI), and SuperTrend to capture market trends. The strategy uses fixed parameters optimized for 2-hour timeframes, employing a 21/55/200 EMA system for trend identification, combined with RSI(14) momentum filter and SuperTrend(3,14) stop-loss for risk management. It also requires a 1.5x volume surge and ATR volatility confirmation to enhance trading reliability.

#### Strategy Principles
The core logic is built on a multi-layered technical analysis framework:
1. Trend identification system uses triple EMAs (21/55/200 periods) to determine trend direction through crossovers and relative positions
2. Momentum confirmation system employs RSI(14) indicator combined with its EMA to filter false breakouts
3. Risk control system integrates SuperTrend indicator as dynamic stop-loss and implements a 6-hour trade cooldown period
4. Trade trigger conditions require volume exceeding 1.5x of 20-period average volume and ATR above its 48-period EMA

#### Strategy Advantages
1. Parameter Optimization: Uses pre-optimized fixed parameters requiring no frequent adjustments
2. Trend Capture: Effectively captures persistent trends through multiple technical indicator coordination
3. Risk Control: Built-in trade cooldown mechanism prevents overtrading
4. Market Adaptability: Performs well in highly volatile markets
5. Trade Confirmation: Multiple condition filters enhance trading signal reliability

#### Strategy Risks
1. Gap Risk: Potential losses from gaps in 24-hour trading markets
2. News Impact: Major news events may cause severe price volatility affecting strategy performance
3. Stop-Loss Rigidity: Fixed stop-loss settings may lack flexibility
4. Market Environment Dependence: May generate frequent false signals in ranging markets
5. Slippage Risk: Potential significant slippage in markets with poor liquidity

#### Strategy Optimization Directions
1. Dynamic Parameter Adjustment: Implement automatic SuperTrend parameter adjustment based on market volatility
2. Market Environment Recognition: Add market state identification module for different parameter settings in various market conditions
3. Stop-Loss Optimization: Introduce dynamic stop-loss mechanism adapting to market volatility
4. Volume Analysis Enhancement: Incorporate more sophisticated volume analysis models to improve signal accuracy
5. Risk Management Optimization: Implement dynamic position sizing system based on market conditions

#### Summary
This strategy constructs a relatively complete trading system through the combination of multiple technical indicators. Its strength lies in effective trend capture and enhanced trading reliability through multiple condition filters. While inherent risks exist, the strategy's overall performance can be improved through optimization and refinement. It is particularly suitable for volatile markets but requires attention to market environment changes and risk control.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-16 08:00:00
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Hybrid Trend Momentum Strategy by Biege ver. 1.0", overlay=true)

// ———— SUPERTREND FIX ————
supertrendWrapper(factor, atrPeriod) =>
    [stLine, stDir] = ta.supertrend(factor, atrPeriod)
    [stLine, stDir]

// ———— GLOBAL EMA CALCULATIONS ————
fastEMA = ta.ema(close, 21)
slowEMA = ta.ema(close, 55)
trendEMA = ta.ema(close, 200)
atrVal = ta.atr(14)
atrEMA = ta.ema(atrVal, 48)
rsiVal = ta.rsi(close, 14)
rsiEMA = ta.ema(rsiVal, 14)
volumeEMA = ta.ema(volume, 20)
[supertrendLine, supertrendDir] = supertrendWrapper(3, 14)

// ———— TRADE THROTTLING SYSTEM ————
var int lastTradeTime = na
tradeCooldown = input.int(360, "Cooldown (minutes)", minval=60, step=15) * 60 * 1000

// ———— ENHANCED ENTRY CONDITIONS ————
entryCondition = 
     ta.crossover(fastEMA, slowEMA) and
     rsiVal > rsiEMA + 10 and
     close > supertrendLine and
     close > trendEMA and
     volume > volumeEMA * 1.5 and
     atrVal > atrEMA and
     (na(lastTradeTime) or time - lastTradeTime >= tradeCooldown)

// ———— ULTRA-OPTIMIZED EXIT CONDITIONS ————
exitCondition = 
     ta.crossunder(fastEMA, slowEMA) or                   // Main EMA cross remains
     ta.crossunder(rsiVal, rsiEMA - 15) or                // Increased from -10 to -15 (harder trigger)
     ta.crossunder(close, supertrendLine * 0.98)          // Changed from 1.01 to 0.98 (2% buffer below)

// ———— TRADE EXECUTION ————
if entryCondition
    strategy.entry("Buy", strategy.long)
    lastTradeTime := time

if exitCondition
    strategy.close("Buy")

// ———— VISUALS ————
plot(fastEMA, "Fast EMA", color.new(#2962FF, 0), 2)
plot(slowEMA, "Slow EMA", color.new(#FF6D00, 0), 2)
plot(trendEMA, "Trend EMA", color.new(#AA00FF, 0), 2)
plot(supertrendLine, "SuperTrend", color.new(#00C853, 0), 2)

plotshape(entryCondition, "Buy", shape.triangleup, 
  location.belowbar, color.new(#00E676, 0), size=size.small)
plotshape(exitCondition, "Sell", shape.triangledown, 
  location.abovebar, color.new(#FF1744, 0), size=size.small)
```

> Detail

https://www.fmz.com/strategy/482465

> Last Modified

2025-02-18 15:27:29
