
> Name

Multi-MA-Trend-Following-with-RSI-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11549e253ad10783ca4.png)

[trans]
#### Overview
This strategy is a trend following strategy based on a multiple moving average system and the RSI indicator. The strategy uses a combination of 20, 50 and 200-period moving averages to determine the market trend by analyzing the positional relationship between different moving averages, and combines the RSI indicator to confirm trading signals. The strategy sets dynamic stop loss and profit targets, and protects the profits obtained by trailing the stop loss.
#### Strategy Principle
The core of the strategy is to determine the market trend by analyzing the relative position relationship between the three moving averages (MA20, MA50, MA200). The strategy defines 18 different moving average combination scenarios, focusing on moving average crossovers and position relationships. When the short-term moving average is above the long-term moving average, it tends to go long; otherwise, it tends to go short. In order to avoid over-trading, the strategy introduces the RSI indicator as a filter condition. When the RSI is below 70, it is allowed to go long, and when it is above 30, it is allowed to go short. The strategy adopts a risk-reward ratio setting of 1:10 and uses a 25-point trailing stop to protect profits.
#### Strategic Advantages
1. Multi-dimensional trend confirmation: By analyzing the relationship between multiple moving averages, the strength and direction of the market trend can be judged more accurately
2. Dynamic risk management: The use of a trailing stop-loss mechanism can protect already-earned profits while allowing profits to continue to grow.
3. Improved filtering mechanism: combine the RSI indicator for signal filtering to effectively reduce false signals
4. Risk-benefit ratio optimization: Use a risk-benefit ratio setting of 1:10 to pursue the benefits brought by the general trend.
5. Adaptable: the strategy can be applied to different markets and time periods
#### Strategy Risk
1. Risk of volatile market: Frequent false breakthrough signals may occur in a volatile market.
2. Slippage risk: In fast markets, the 25-point trailing stop may not be executed accurately due to slippage.
3. Trend reversal risk: When the trend reverses, the strategy may respond slowly, resulting in profit taking
4. Parameter dependence: The strategy effect depends largely on the selection of moving average period and RSI parameters.
#### Strategy optimization direction
1. Introducing trading volume indicators: You can improve the accuracy of trend judgment by adding trading volume analysis
2. Optimize scenario definition: It can simplify some repetitive scenario definitions and improve the efficiency of strategy operation.
3. Dynamic parameter adjustment: the trailing stop loss point can be dynamically adjusted according to market volatility
4. Add time filtering: Add trading time period filtering to avoid volatile market opening and closing periods
5. Optimize signal confirmation: you can add trend strength confirmation indicators to improve the reliability of trading signals
#### Summary
This is a trend following strategy with complete structure and clear logic. Through the combined use of multiple moving average systems and the filtering of RSI indicators, a relatively reliable trading system is formed. The risk management mechanism of the strategy is reasonably designed, and the trailing stop loss method protects profits without leaving the market prematurely. Although there is still some room for optimization in the strategy, the overall framework design is more scientific and has practical application value. ||
#### Overview
This strategy is a trend-following system based on multiple moving averages and RSI indicator. It utilizes a combination of 20, 50, and 200-period moving averages to analyze market trends through their relative positions, combined with RSI confirmation for trade signals. The strategy incorporates dynamic stop-loss and profit targets with trailing stops to protect profits.

#### Strategy Principles
The core of the strategy lies in analyzing the relative positions of three moving averages (MA20, MA50, MA200) to determine market trends. The strategy defines 18 different moving average combination scenarios, focusing on crossovers and relative positions. Long positions are preferred when shorter-term MAs are above longer-term MAs, and vice versa. To avoid overtrading, RSI is introduced as a filter, allowing long entries when RSI is below 70 and short entries above 30. The strategy employs a 1:10 risk-reward ratio with a 25-point trailing stop to protect profits.

#### Strategy Advantages
1. Multi-dimensional trend confirmation: More accurate trend strength and direction determination through analysis of multiple MA relationships
2. Dynamic risk management: Trailing stop mechanism protects profits while allowing for continued growth
3. Comprehensive filtering: RSI indicator integration effectively reduces false signals
4. Optimized risk-reward ratio: 1:10 setting targets profits from major trends
5. High adaptability: Strategy applicable across different markets and timeframes

#### Strategy Risks
1. Choppy market risk: May generate frequent false breakout signals in ranging markets
2. Slippage risk: 25-point trailing stop may not execute accurately in fast markets due to slippage
3. Trend reversal risk: Strategy may react slowly to trend reversals, leading to profit giveback
4. Parameter dependency: Strategy effectiveness heavily relies on MA period and RSI parameter selection

#### Optimization Directions
1. Volume indicator integration: Add volume analysis to improve trend identification accuracy
2. Scenario definition optimization: Simplify redundant scenario definitions to improve strategy efficiency
3. Dynamic parameter adjustment: Adjust trailing stop levels based on market volatility
4. Time filtering addition: Add trading session filters to avoid high volatility market opens and closes
5. Signal confirmation enhancement: Add trend strength confirmation indicators to improve signal reliability

#### Summary
This is a well-structured trend-following strategy with clear logic. The combination of multiple moving average systems with RSI filtering creates a relatively reliable trading system. The risk management mechanism is well-designed, protecting profits through trailing stops without premature exits. While there is room for optimization, the overall framework is scientifically designed with practical application value.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Refined MA Strategy with Trailing Stop for 30m", overlay=true)

// Define the moving averages
TR20 = ta.sma(close, 20)
TR50 = ta.sma(close, 50)
TR200 = ta.sma(close, 200)

// Define the RSI for additional filtering
rsi = ta.rsi(close, 14)

// Define the scenarios
scenario1 = TR20 > TR50 and TR50 > TR200
scenario2 = TR50 > TR20 and TR20 > TR200
scenario3 = TR200 > TR50 and TR50 > TR20
scenario4 = TR50 > TR200 and TR200 > TR20
scenario5 = TR20 > TR200 and TR200 > TR50
scenario6 = TR200 > TR20 and TR20 > TR50
scenario7 = TR20 == TR50 and TR50 > TR200
scenario8 = TR50 == TR20 and TR20 > TR200
scenario9 = TR200 == TR50 and TR50 > TR20
scenario10 = TR20 > TR50 and TR50 == TR200
scenario11 = TR50 > TR20 and TR20 == TR200
scenario12 = TR20 > TR50 and TR50 == TR200
scenario13 = TR20 == TR50 and TR50 == TR200
scenario14 = TR20 > TR50 and TR200 == TR50
scenario15 = TR50 > TR20 and TR200 == TR50
scenario16 = TR20 > TR50 and TR50 == TR200
scenario17 = TR20 > TR50 and TR50 == TR200
scenario18 = TR20 > TR50 and TR50 == TR200

// Entry conditions
longCondition = (scenario1 or scenario2 or scenario5) and rsi < 70
shortCondition = (scenario3 or scenario4 or scenario6) and rsi > 30

// Execute trades based on scenarios with 50 points stop loss and 1:10 RR, using a trailing stop of 25 points
if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit("Take Profit", from_entry="Long", limit=close + 250, trail_offset=25)

if (shortCondition)
    strategy.entry("Short", strategy.short)
    strategy.exit("Take Profit", from_entry="Short", limit=close - 250, trail_offset=25)

```

> Detail

https://www.fmz.com/strategy/473360

> Last Modified

2024-11-29 15:20:30
