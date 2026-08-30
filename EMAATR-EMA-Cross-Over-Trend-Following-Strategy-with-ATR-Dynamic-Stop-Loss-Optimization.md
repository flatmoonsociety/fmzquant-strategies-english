
> Name

EMA-Cross-Over-Trend-Following-Strategy-with-ATR-Dynamic-Stop-Loss-Optimization
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d87fb46a3c5c58760515.png)
![IMG](https://www.fmz.com/upload/asset/2d8310f9e5be05625826c.png)




[trans]
#### Overview
This strategy is a trend following system based on moving average crossovers and dynamic stops. The core logic is to capture the starting point of the upward trend through the golden cross of the fast moving average (EMA5) and the slow moving average (EMA200), and combine it with ATR dynamic stop loss to protect profits. The strategy also sets a fixed percentage take-profit target to achieve a balance between risk and return.
#### Strategy Principle
Strategy operation is based on the following core mechanisms:
1. The entry signal is triggered by EMA5 crossing EMA200, indicating that short-term momentum breaks through the long-term trend
2. Dynamic stop loss is calculated based on the ATR indicator, and the stop loss price is set to the closing price minus the ATR value multiplied by the multiple
3. The take profit target is set as a fixed percentage of the entry price (default 5%)
4. During the position holding period, the ATR stop loss price will move upward as the price rises, forming a trailing stop loss.
5. When the price hits the stop loss line or reaches the take profit target, the strategy automatically closes the position
#### Strategic Advantages
1. Strong trend capturing ability - EMA crossover system can effectively identify the early stage of the trend
2. Flexible risk management - ATR dynamic stop loss can be adaptively adjusted according to market volatility
3. Stable execution - systematic entry and exit rules to avoid artificial emotional interference
4. The parameters are highly adjustable - the moving average period, ATR multiple and take-profit ratio can all be optimized according to needs
5. Clear operational logic - the policy rules are simple and clear, easy to understand and execute
#### Strategy Risk
1. False breakout risk - sideways markets may produce multiple invalid cross signals
2. Retracement risk - you may be exposed to a larger retracement when the trend suddenly reverses
3. Slippage risk – stop-loss or take-profit orders may face slippage in rapidly volatile markets
4. Parameter sensitivity - there may be large differences in optimal parameters under different market environments
5. Money management risk - fixed position ratios may be too risky in some circumstances
#### Strategy optimization direction
1. Add trend filter - trend strength indicators such as ADX can be introduced to filter out weak market conditions
2. Optimize the stop loss mechanism - consider setting a stop loss based on support levels or volatility percentages
3. Dynamically adjust the take profit target - dynamically adjust the take profit target based on market volatility or trend strength
4. Add time filtering - avoid time periods with high volatility
5. Improve position management - introduce a dynamic position management mechanism and adjust it according to market risk
#### Summary
This is a trend following strategy that combines classic technical indicators with modern risk management. Capture the trend through moving average crossovers, use ATR dynamic stop loss to protect profits, and perform well in trending markets. Although there is a certain risk of false signals, the stability of the strategy can be significantly improved through parameter optimization and adding filters. The core advantage of the strategy lies in its systematic operating logic and flexible risk management mechanism, which is suitable as the basic strategy framework for medium and long-term trend trading. ||


#### Overview
This strategy is a trend-following system based on moving average crossovers and dynamic stop-loss management. The core logic is to capture the beginning of uptrends through the golden cross of fast moving average (EMA5) and slow moving average (EMA200), combined with ATR-based dynamic stop-loss for profit protection. The strategy also incorporates a fixed percentage take-profit target to balance risk and reward.

#### Strategy Principles
The strategy operates on the following core mechanisms:
1. Entry signals are triggered when EMA5 crosses above EMA200, indicating short-term momentum breakthrough
2. Dynamic stop-loss is calculated based on the ATR indicator, set at close price minus ATR value multiplied by a factor
3. Take-profit target is set at a fixed percentage (default 5%) above entry price
4. During position holding, ATR stop-loss moves up with price movement, forming a trailing stop
5. The strategy automatically closes positions when price hits either stop-loss or take-profit levels

#### Strategy Advantages
1. Strong trend capture capability - EMA crossover system effectively identifies early trend stages
2. Flexible risk management - ATR dynamic stop-loss adapts to market volatility
3. Stable execution - Systematic entry and exit rules avoid emotional interference
4. High parameter adaptability - Moving average periods, ATR multiplier, and take-profit percentage can be optimized
5. Clear operational logic - Strategy rules are simple and easy to understand and execute

#### Strategy Risks
1. False breakout risk - Ranging markets may produce multiple invalid cross signals
2. Drawdown risk - Sudden trend reversals may lead to significant drawdowns
3. Slippage risk - Stop-loss or take-profit orders may face slippage in volatile markets
4. Parameter sensitivity - Optimal parameters may vary significantly across different market conditions
5. Money management risk - Fixed position sizing may be too risky in certain situations

#### Strategy Optimization Directions
1. Add trend filters - Incorporate trend strength indicators like ADX to filter weak trends
2. Optimize stop-loss mechanism - Consider combining support levels or volatility percentages
3. Dynamic take-profit adjustment - Adjust take-profit targets based on market volatility or trend strength
4. Add time filters - Avoid highly volatile time periods
5. Improve position management - Introduce dynamic position sizing based on market risk levels

#### Summary
This is a trend-following strategy combining classic technical indicators with modern risk management. It captures trends through moving average crossovers and protects profits using ATR dynamic stop-loss, performing well in trending markets. While there are risks of false signals, strategy stability can be significantly improved through parameter optimization and additional filters. The core advantages lie in its systematic operational logic and flexible risk management mechanism, making it suitable as a foundation framework for medium to long-term trend trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-21 00:00:00
end: 2025-02-18 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

// -----------------------------------------------------------
//  Title:    EMA5 Cross-Up EMA200 with ATR Trailing Stop & Take-Profit
//  Author:   ChatGPT
//  Version:  1.1 (Pine Script v6)
//  Notes:    Enter Long when EMA(5) crosses above EMA(200).
//            Exit on either ATR-based trailing stop or
//            specified % Take-Profit.
// -----------------------------------------------------------

//@version=6
strategy(title="EMA5 Cross-Up EMA200 ATR Stop", shorttitle="EMA5x200_ATRStop_v6", overlay=true, initial_capital=100000, default_qty_type=strategy.percent_of_equity,default_qty_value=100)

// -- 1) Inputs
emaFastLength   = input.int(5,    "Fast EMA Length")
emaSlowLength   = input.int(200,  "Slow EMA Length")
atrPeriod       = input.int(14,   "ATR Period")
atrMult         = input.float(2.0,"ATR Multiplier", step=0.1)
takeProfitPerc  = input.float(5.0,"Take-Profit %", step=0.1)

// -- 2) Indicator Calculations
emaFast   = ta.ema(close, emaFastLength)
emaSlow   = ta.ema(close, emaSlowLength)
atrValue  = ta.atr(atrPeriod)

// -- 3) Entry Condition: EMA5 crosses above EMA200
emaCrossUp = ta.crossover(emaFast, emaSlow)

// -- 4) Determine a dynamic ATR-based stop loss (for trailing)
longStopPrice = close - (atrValue * atrMult)

// -- 5) Take-Profit Price
//    We store it in a variable so we can update it when in position.
var float takeProfitPrice = na
var float avgEntryPrice   = na

if strategy.position_size > 0
    // If there is an open long, get the average fill price:
    avgEntryPrice   := strategy.position_avg_price
    takeProfitPrice := avgEntryPrice * (1 + takeProfitPerc / 100)
else
    // If no open position, reset
    takeProfitPrice := na
    avgEntryPrice   := na

// -- 6) Submit Entry Order
if emaCrossUp
    strategy.entry(id="Long", direction=strategy.long)

// -- 7) Submit Exit Orders (Stop or Take-Profit)
strategy.exit(id         = "Exit Long",stop       = longStopPrice,limit      = takeProfitPrice)

// -- 8) (Optional) Plotting for Visuals
plot(emaFast, color=color.new(color.yellow, 0), linewidth=2, title="EMA Fast")
plot(emaSlow, color=color.new(color.blue,   0), linewidth=2, title="EMA Slow")
plot(longStopPrice, color=color.red, linewidth=2, title="ATR Trailing Stop")
```

> Detail

https://www.fmz.com/strategy/482774

> Last Modified

2025-02-27 17:51:17
