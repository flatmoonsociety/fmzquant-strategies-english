
> Name

EMA double cross dynamic stop loss quantitative strategy-EMA-Dual-Crossover-Dynamic-Stop-Loss-Quantitative-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/ba0870c8e73f198d2ef68ba1a968319c220a355db646016e87d4194459d8a185.png)
![IMG](assets/images/2471077501f16de4df04ec24b2f1add5210b4b9c4be6029d3f4b75178f6640e6.png)



[trans]
#### Overview
This strategy is designed based on the double crossover principle of the exponential moving average (EMA) and combined with a dynamic stop loss mechanism. The strategy uses the golden cross/death cross of the 10-day EMA and the 20-day EMA as the main trading signal, uses the 50-day EMA as the trend filter, and uses the 10-day EMA as the dynamic stop loss line. A buy signal is generated when the price is above the 50-day EMA and the 10-day EMA is above the 20-day EMA; a sell signal is generated when the price is below the 50-day EMA and the 10-day EMA is below the 20-day EMA. During the holding period, if the price reversely breaks through the 10-day EMA, the stop loss exit will be triggered.
#### Strategy Principles
1. **Judgment of long and short conditions**:
   - Bull condition: When the 10-day EMA crosses the 20-day EMA (golden cross) from below, and the current closing price is higher than the 50-day EMA, the bull trend is confirmed.  
   - Short conditions: When the 10-day EMA crosses the 20-day EMA (die cross) from above, and the current closing price is lower than the 50-day EMA, the short trend is confirmed.  
2. **Dynamic stop loss mechanism**:
   - During the long position, if the closing price falls below the 10-day EMA, the stop loss will be triggered to close the position.  
   - During the short position period, if the closing price rises above the 10-day EMA, the stop loss will be triggered to close the position.  
3. **Trend Filter**: The 50-day EMA serves as a long-term trend filter to avoid frequent trading in volatile markets.
#### Advantage Analysis
1. **Trend tracking ability**: Double EMA crossover can effectively capture the mid-term trend, and 50-day EMA filtering reduces false signals.  
2. **Dynamic Risk Management**: The 10-day EMA serves as a dynamic stop loss line, which can adjust the exit point according to the trend to protect profits.  
3. **Visual design**: The three EMAs are distinguished by different colors and line widths, and the buying and selling signals are marked to facilitate real-time monitoring.  
4. **Parameter Adjustability**: The EMA period can be flexibly adjusted by inputting parameters to adapt to different market volatility.
#### Risk Analysis
1. **Lagging risk**: EMA is calculated based on historical data and may cause a large retracement in a rapid reversal of the market.  
   - *Solution*: Combine with a momentum indicator (such as RSI) to filter out extreme swings.  
2. **Loss in a volatile market**: In a trendless market, cross signals may frequently trigger invalid transactions.  
   - *Solution*: Introduce a volatility indicator (such as ATR) to suspend trading.  
3. **Parameter overfitting**: The fixed EMA period may not be suitable for all market states.  
   - *Solution*: Use an adaptive period algorithm or multiple timeframe verification.
#### Optimization direction
1. **Composite Signal Enhancement**:
   - Increase trading volume confirmation (such as increasing volume when breaking through) to improve signal reliability.  
2. **Dynamic position management**:
   - Adjust position size based on volatility (ATR value) to reduce exposure during high-risk periods.  
3. **Machine Learning Optimization**:
   - Use historical data to train the model and dynamically optimize the EMA cycle combination.  
4. **Multiple Time Frame Verification**:
   - The weekly level EMA direction is required to be consistent with the daily signal to increase the winning rate.
#### Summary
This strategy achieves a balance between trend tracking and risk control through the combination of EMA double crossover and dynamic stop loss. Its core advantage lies in its clear logical structure and intuitive visual design, which is suitable for medium and low-frequency trading scenarios. In the future, the robustness can be further improved by introducing more dimensions of market data (such as volatility, trading volume).
||  

#### Overview  
This strategy is designed based on the dual crossover principle of Exponential Moving Averages (EMA) combined with a dynamic stop-loss mechanism. It uses the golden/death cross of 10-day and 20-day EMAs as primary trading signals, with the 50-day EMA as a trend filter and the 10-day EMA as a dynamic stop-loss line. A buy signal is generated when the price is above the 50-day EMA and the 10-day EMA crosses above the 20-day EMA; a sell signal occurs when the price is below the 50-day EMA and the 10-day EMA crosses below the 20-day EMA. Positions are exited if the price reversely breaks the 10-day EMA.  

#### Strategy Logic  
1. **Bullish/Bearish Conditions**:  
   - Bullish: When 10-day EMA crosses above 20-day EMA (golden cross) and closing price is above 50-day EMA.  
   - Bearish: When 10-day EMA crosses below 20-day EMA (death cross) and closing price is below 50-day EMA.  
2. **Dynamic Stop-Loss**:  
   - Long positions are closed if price falls below 10-day EMA.  
   - Short positions are closed if price rises above 10-day EMA.  
3. **Trend Filtering**: The 50-day EMA acts as a long-term trend filter to avoid overtrading in ranging markets.  

#### Advantages  
1. **Trend-Following Capability**: Dual EMA crossover effectively captures medium-term trends, while the 50-day EMA reduces false signals.  
2. **Dynamic Risk Management**: The 10-day EMA serves as an adaptive stop-loss, protecting profits during trend movements.  
3. **Visual Clarity**: Distinct colors and line widths differentiate the three EMAs, with annotated signals for real-time monitoring.  
4. **Parameter Flexibility**: Adjustable EMA periods adapt to varying market volatilities.  

#### Risks  
1. **Lagging Risk**: EMAs rely on historical data, potentially causing significant drawdowns during rapid reversals.  
   - *Solution*: Incorporate momentum indicators (e.g., RSI) to filter extreme volatility.  
2. **Range Market Losses**: Frequent whipsaws may occur in trendless conditions.  
   - *Solution*: Add volatility filters (e.g., ATR) to pause trading.  
3. **Overfitting Risk**: Fixed EMA periods may not suit all market regimes.  
   - *Solution*: Implement adaptive period algorithms or multi-timeframe confirmation.  

#### Optimization Directions  
1. **Composite Signals**:  
   - Add volume confirmation (e.g., breakout with high volume) to enhance signal reliability.  
2. **Dynamic Position Sizing**:  
   - Adjust position size based on volatility (ATR values) to reduce exposure in high-risk periods.  
3. **Machine Learning**:  
   - Train models on historical data to dynamically optimize EMA period combinations.  
4. **Multi-Timeframe Validation**:  
   - Require weekly EMA alignment with daily signals to improve win rates.  

#### Conclusion  
This strategy balances trend-following and risk control through EMA dual crossover and dynamic stop-loss. Its core strengths lie in clear logic and intuitive visualization, making it suitable for medium-low frequency trading. Future enhancements could integrate multidimensional data (e.g., volatility, volume) for greater robustness.  
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-24 00:00:00
end: 2025-04-23 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"DOGE_USDT"}]
*/

//@version=5
//@description Ovtlyer EMA Crossover  price over 50 Indicator
//@author YourName

strategy("EMA Crossover Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// Input EMA lengths
length10 = input.int(10, minval=1, title="10 EMA Length")
length20 = input.int(20, minval=1, title="20 EMA Length")
length50 = input.int(50, minval=1, title="50 EMA Length")

// Calculate EMAs
ema10 = ta.ema(close, length10)
ema20 = ta.ema(close, length20)
ema50 = ta.ema(close, length50)

// Bullish Condition: 10 EMA crosses above 20 EMA AND price is above 50 EMA
bullishCondition = ta.crossover(ema10, ema20) and close > ema50

// Bearish Condition: 10 EMA crosses below 20 EMA AND price is below 50 EMA
bearishCondition = ta.crossunder(ema10, ema20) and close < ema50

// Track the current market state
var isBullish = false
var isBearish = false

if (bullishCondition)
    isBullish := true
    isBearish := false

if (bearishCondition)
    isBearish := true
    isBullish := false

// Exit conditions
bullishExit = isBullish and close < ema10
bearishExit = isBearish and close > ema10

// Plot EMAs
plot(ema10, title="10 EMA", color=color.rgb(0, 255, 0), linewidth=3) // Thick green line for 10 EMA
plot(ema20, title="20 EMA", color=color.rgb(0, 150, 255), linewidth=2) // Medium blue line for 20 EMA
plot(ema50, title="50 EMA", color=color.rgb(255, 165, 0), linewidth=1) // Thin orange line for 50 EMA

// Strategy Entry and Exit
if (bullishCondition)
    strategy.entry("Long", strategy.long)

if (bearishCondition)
    strategy.entry("Short", strategy.short)

if (bullishExit)
    strategy.close("Long")

if (bearishExit)
    strategy.close("Short")

// Plot Entry Signals (for visualization)
plotshape(bullishCondition, title="Bullish Signal", 
          location=location.belowbar, style=shape.triangleup, 
          size=size.small, color=color.green)
plotshape(bearishCondition, title="Bearish Signal", 
          location=location.abovebar, style=shape.triangledown, 
          size=size.small, color=color.red)

// Plot Exit Signals (for visualization)
plotshape(bullishExit, title="Bullish Exit", 
          location=location.abovebar, style=shape.xcross, 
          size=size.small, color=color.orange)
plotshape(bearishExit, title="Bearish Exit", 
          location=location.belowbar, style=shape.xcross, 
          size=size.small, color=color.purple)
```

> Detail

https://www.fmz.com/strategy/491892

> Last Modified

2025-04-24 16:59:03
