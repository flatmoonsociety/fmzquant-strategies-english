
> Name

Intelligent-Time-Based-Long-Short-Rotation-Balanced-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1bee661f5e30ac09fb0.png)

[trans]
#### Overview
This is an intelligent rotation strategy based on time periods, which achieves profits by conducting long and short rotation transactions within a specified time period. The strategy adopts a flexible position management mechanism, which can automatically adjust the trading direction according to the market environment, and also has risk control functions. This strategy supports long-short two-way trading and can selectively enable swing trading mode, making it highly adaptable.
#### Strategy Principle
The strategy mainly controls transactions through time periods and position status. First, determine whether it is within the effective trading range of the last 500 K lines through the inActivePeriod() function. Within the effective range, the strategy determines trading behavior based on variables such as position status (positionHeld), held position time (barsHeld), and pause time (barsPaused). When the swing trading mode is enabled, the strategy will quickly rotate between the long and short directions; when the swing trading mode is disabled, the strategy will close the position after 3 periods and wait for new trading opportunities.
#### Strategic Advantages
1. Strong flexibility: supports pure long, pure short or long-short two-way trading modes
2. Risk controllable: Limit the holding time through time periods to avoid long-term position risks
3. Good adaptability: able to automatically adjust the trading direction according to the market environment
4. Simple operation: clear transaction logic, easy to understand and execute
5. High capital efficiency: improve capital utilization efficiency through frequent rotation
6. Adjustable parameters: all key parameters can be flexibly adjusted according to actual needs
#### Strategy Risk
1. Frequent transactions may result in higher handling fees.
2. Frequent false signals may occur in volatile markets
3. A fixed holding period may miss important market opportunities
4. Failure to consider market trends, which may be contrary to the main trend
5. Lack of stop-loss mechanism, which may cause large losses in extreme market conditions
#### Strategy optimization direction
1. Introduce volatility indicators (such as ATR) to dynamically adjust the holding time
2. Add trend judgment indicators to improve the accuracy of trading direction
3. Add a stop-loss and stop-profit mechanism to improve risk control capabilities
4. Optimize entry timing and avoid trading during unfavorable time periods
5. Introduce a fund management system and optimize the size of positions
6. Add market sentiment indicators to improve trading accuracy
#### Summary
This strategy obtains market returns through time cycle control and long-short rotation, and has strong flexibility and adaptability. Although there are some risks, the stability and profitability of the strategy can be significantly improved through reasonable optimization and risk control measures. The core advantage of the strategy lies in its simple and effective trading logic, which is suitable for further optimization and expansion as a basic strategy.
||

#### Overview
This is an intelligent rotation strategy based on time periods that seeks to generate returns through long-short rotation trading within specified time periods. The strategy employs a flexible position management mechanism that can automatically adjust trading direction according to market conditions while incorporating risk control functions. It supports bi-directional trading and optional swing trading mode, demonstrating strong adaptability.

#### Strategy Principle
The strategy primarily controls trading through time periods and position status. First, the inActivePeriod() function determines whether trading is within the effective trading interval of the last 500 bars. Within the effective interval, the strategy decides trading actions based on variables such as position status (positionHeld), holding time (barsHeld), and pause time (barsPaused). When swing trading mode is enabled, the strategy rotates quickly between long and short directions; when disabled, positions are closed after 3 periods and wait for new trading opportunities.

#### Strategy Advantages
1. High Flexibility: Supports pure long, pure short, or bi-directional trading modes
2. Controlled Risk: Limits position holding time through time periods to avoid long-term position risks
3. Good Adaptability: Automatically adjusts trading direction based on market conditions
4. Simple Operation: Clear trading logic, easy to understand and execute
5. High Capital Efficiency: Improves capital utilization through frequent rotation
6. Adjustable Parameters: Key parameters can be flexibly adjusted according to actual needs

#### Strategy Risks
1. Frequent trading may lead to high commission costs
2. May generate frequent false signals in oscillating markets
3. Fixed holding periods might miss important market opportunities
4. Market trends not considered, may trade against primary trends
5. Lack of stop-loss mechanism may cause significant losses in extreme market conditions

#### Strategy Optimization Directions
1. Introduce volatility indicators (like ATR) to dynamically adjust holding periods
2. Add trend judgment indicators to improve trading direction accuracy
3. Include stop-loss and take-profit mechanisms to enhance risk control
4. Optimize entry timing to avoid unfavorable trading periods
5. Introduce money management system to optimize position sizing
6. Add market sentiment indicators to improve trading accuracy

#### Summary
This strategy achieves market returns through time period control and long-short rotation, demonstrating strong flexibility and adaptability. While certain risks exist, the strategy's stability and profitability can be significantly improved through reasonable optimization and risk control measures. The core advantage lies in its simple yet effective trading logic, making it suitable as a foundation strategy for further optimization and expansion.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-12 00:00:00
end: 2024-11-11 00:00:00
period: 4h
basePeriod: 4h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Tickerly Test Strategy", overlay=true)

// Inputs
longEnabled = input.bool(true, "Enable Long Trades")
shortEnabled = input.bool(true, "Enable Short Trades")
swingEnabled = input.bool(false, "Enable Swing Trading")

// Variables
var positionHeld = 0
var barsHeld = 0
var barsPaused = 0
var lastAction = "none"

// Function to determine if we're in the last 500 bars
inActivePeriod() => 
    barIndex = bar_index
    lastBarIndex = last_bar_index
    barIndex >= (lastBarIndex - 499)

// Main strategy logic
if inActivePeriod()
    if swingEnabled
        if positionHeld == 0 and barstate.isconfirmed
            if lastAction != "long"
                strategy.entry("Long", strategy.long)
                positionHeld := 1
                barsHeld := 0
                lastAction := "long"
            else
                strategy.entry("Short", strategy.short)
                positionHeld := -1
                barsHeld := 0
                lastAction := "short"
        
        if positionHeld != 0
            barsHeld += 1
            if barsHeld >= 2
                if positionHeld == 1
                    strategy.entry("Short", strategy.short)
                    positionHeld := -1
                    barsHeld := 0
                    lastAction := "short"
                else
                    strategy.entry("Long", strategy.long)
                    positionHeld := 1
                    barsHeld := 0
                    lastAction := "long"
    else
        if positionHeld == 0 and barsPaused >= 1 and barstate.isconfirmed
            if longEnabled and shortEnabled
                if lastAction != "long"
                    strategy.entry("Long", strategy.long)
                    positionHeld := 1
                    barsHeld := 0
                    barsPaused := 0
                    lastAction := "long"
                else
                    strategy.entry("Short", strategy.short)
                    positionHeld := -1
                    barsHeld := 0
                    barsPaused := 0
                    lastAction := "short"
            else if longEnabled
                strategy.entry("Long", strategy.long)
                positionHeld := 1
                barsHeld := 0
                barsPaused := 0
                lastAction := "long"
            else if shortEnabled
                strategy.entry("Short", strategy.short)
                positionHeld := -1
                barsHeld := 0
                barsPaused := 0
                lastAction := "short"
        
        if positionHeld != 0
            barsHeld += 1
            if barsHeld >= 3
                strategy.close_all()
                positionHeld := 0
                barsHeld := 0
                barsPaused := 0  // Reset pause counter when exiting a position
        else
            barsPaused += 1

// Plotting active period for visual confirmation
plot(inActivePeriod() ? 1 : 0, "Active Period", color=color.new(color.blue, 80), style=plot.style_areabr)
```

> Detail

https://www.fmz.com/strategy/471718

> Last Modified

2024-11-12 16:33:43
