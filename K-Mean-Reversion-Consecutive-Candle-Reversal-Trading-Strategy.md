
> Name

Mean-Reversion-Consecutive-Candle-Reversal-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1dae1d30727352e93d1.png)

[trans]
#### Overview
This is a trading strategy based on the principle of mean reversion, which captures short-term price reversal opportunities by identifying continuous falling and rising K-line patterns. The core logic of the strategy is to enter long positions after the appearance of three consecutive falling K lines, and to exit the position after the appearance of three consecutive rising K lines. Strategies can also optionally incorporate EMA filters to improve trade quality.
#### Strategy Principles
The strategy is mainly based on the following core elements:
1. Continuous K-line counter: Count the number of consecutive rising and falling K-lines respectively.
2. Entry conditions: A long signal is triggered when a specified number (default 3) of closing price falling K lines appear continuously.
3. Exit conditions: The closing signal is triggered when the closing price of a specified number (default 3) of rising K lines appears continuously.
4. EMA filter: Optionally add 200-period exponential moving average as a trend filter condition
5. Trading time window: Specific trading start and end times can be set to limit the trading range.
#### Strategic Advantages
1. The logic is simple and clear: the strategy uses a simple K-line counting method, which is easy to understand and implement.
2. Strong adaptability: can be applied to different time periods and trading varieties
3. Flexible parameters: parameters such as the number of consecutive K lines and EMA period can be adjusted as needed
4. Improved risk control: control risks through multiple mechanisms such as time windows and trend filtering
5. High computational efficiency: the core logic only needs to compare the closing prices of adjacent K lines, so the computational burden is small
#### Strategy Risk
1. Trend market risk: False breakthroughs may occur frequently in strong trending markets
2. Parameter sensitivity: The setting of the number of consecutive K lines has a greater impact on strategy performance
3. Impact of slippage: You may face greater risk of slippage in a volatile market
4. False signal risk: The continuous K-line pattern may be disturbed by market noise
5. Lack of stop loss: The strategy does not set a clear stop loss mechanism, which may lead to larger retracements.
#### Strategy optimization direction
1. Add a stop loss mechanism: It is recommended to add a fixed stop loss or trailing stop loss to control risks
2. Optimize filtering conditions: indicators such as trading volume and volatility can be introduced as auxiliary filtering
3. Dynamic parameter adjustment: Consider dynamically adjusting the number of consecutive K lines according to market conditions.
4. Increase position management: you can design a batch opening and reduction mechanism to increase profits
5. Improve time management: set different trading parameters for different time periods
#### Summary
This is a well-designed mean reversion strategy that captures short-term price oversold rebound opportunities to gain profits. The main advantages of the strategy are simple logic and strong adaptability, but in actual application, attention needs to be paid to controlling risks. It is recommended to improve the stability of the strategy by adding a stop-loss mechanism, optimizing filter conditions, etc. ||
#### Overview
This is a mean reversion trading strategy that captures short-term price reversal opportunities by identifying consecutive bearish and bullish candle patterns. The core logic enters a long position after three consecutive bearish candles and exits after three consecutive bullish candles. The strategy can optionally incorporate an EMA filter to enhance trade quality.

#### Strategy Principles
The strategy is based on the following core elements:
1. Consecutive candle counter: Tracks the number of consecutive bullish and bearish candles
2. Entry condition: Triggers a long signal when specified number (default 3) of consecutive lower closing prices occurs
3. Exit condition: Triggers a closing signal when specified number (default 3) of consecutive higher closing prices occurs
4. EMA filter: Optional 200-period exponential moving average as trend filter
5. Trading time window: Can set specific trading start and end times to limit trading periods

#### Strategy Advantages
1. Simple and clear logic: Strategy uses simple candle counting method, easy to understand and implement
2. High adaptability: Can be applied to different timeframes and trading instruments
3. Flexible parameters: Consecutive candle counts, EMA period and other parameters can be adjusted as needed
4. Comprehensive risk control: Multiple mechanisms including time window and trend filter to control risk
5. High computational efficiency: Core logic only requires comparing adjacent candle closing prices, low computational load

#### Strategy Risks
1. Trend market risk: May encounter frequent false breakouts in strong trending markets
2. Parameter sensitivity: Number of consecutive candles setting significantly impacts strategy performance
3. Slippage impact: May face significant slippage risk in volatile markets
4. False signal risk: Consecutive candle patterns may be affected by market noise
5. Lack of stop loss: Strategy lacks explicit stop loss mechanism, may lead to large drawdowns

#### Strategy Optimization Directions
1. Add stop loss mechanism: Recommend adding fixed or trailing stop loss to control risk
2. Optimize filter conditions: Can introduce volume, volatility and other indicators as auxiliary filters
3. Dynamic parameter adjustment: Consider dynamically adjusting consecutive candle count requirements based on market conditions
4. Enhance position management: Can design partial position building and reduction mechanisms to improve returns
5. Improve time management: Set different trading parameters for different time periods

#### Summary
This is a well-designed mean reversion strategy that generates returns by capturing short-term oversold bounce opportunities. The strategy's main advantages are simple logic and high adaptability, but risk control needs attention in practical application. It is recommended to enhance strategy stability through adding stop loss mechanisms, optimizing filter conditions and other improvements.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-19 00:00:00
end: 2025-02-18 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("3 Down, 3 Up Strategy", overlay=true, initial_capital = 1000000, default_qty_value = 200, default_qty_type = strategy.percent_of_equity, process_orders_on_close = true, margin_long = 5, margin_short = 5, calc_on_every_tick = true)


//#region INPUTS SECTION
// ============================================
// Time Settings
// ============================================
startTimeInput = input(timestamp("1 Jan 2014"), "Start Time", group = "Time Settings")
endTimeInput = input(timestamp("1 Jan 2099"), "End Time", group = "Time Settings")
isWithinTradingWindow = true

// ============================================
// Strategy Settings
// ============================================
buyTriggerInput = input.int(3, "Consecutive Down Closes for Entry", minval = 1, group = "Strategy Settings")
sellTriggerInput = input.int(3, "Consecutive Up Closes for Exit", minval = 1, group = "Strategy Settings")

// ============================================
// EMA Filter Settings
// ============================================
useEmaFilter = input.bool(false, "Use EMA Filter", group = "Trend Filter")
emaPeriodInput = input.int(200, "EMA Period", minval = 1, group = "Trend Filter")
//#endregion

//#region INDICATOR CALCULATIONS
// ============================================
// Consecutive Close Counter
// ============================================
var int aboveCount = na
var int belowCount = na

aboveCount := close > close[1] ? (na(aboveCount) ? 1 : aboveCount + 1) : 0
belowCount := close < close[1] ? (na(belowCount) ? 1 : belowCount + 1) : 0

// ============================================
// Trend Filter Calculation
// ============================================
emaValue = ta.ema(close, emaPeriodInput)
//#endregion

//#region TRADING CONDITIONS
// ============================================
// Entry/Exit Logic
// ============================================
longCondition = belowCount >= buyTriggerInput and isWithinTradingWindow
exitCondition = aboveCount >= sellTriggerInput

// Apply EMA Filter if enabled
if useEmaFilter
    longCondition := longCondition and close > emaValue
//#endregion

//#region STRATEGY EXECUTION
// ============================================
// Order Management
// ============================================
if longCondition
    strategy.entry("Long", strategy.long)
    
if exitCondition
    strategy.close_all()
//#endregion
```

> Detail

https://www.fmz.com/strategy/482589

> Last Modified

2025-02-19 10:51:35
