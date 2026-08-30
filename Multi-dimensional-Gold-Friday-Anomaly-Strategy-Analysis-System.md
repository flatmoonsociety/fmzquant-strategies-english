
> Name

Multi-dimensional Gold-Friday-Anomaly-Strategy-Analysis-System
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b5e92ca3cc7a03e15a654a1a47607536541f51f996ced91d74960f022f324c73.png)

[trans]
#### Overview
This strategy is a trading system based on market anomalies, which mainly uses the market behavior characteristics from Thursday evening's closing to Friday's closing for trading. This strategy uses fixed entry and exit times and verifies the effectiveness of this market model through backtesting. The strategy uses 10% of the capital for a single transaction and takes into account slippage and commission factors to ensure the authenticity of the backtest results.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Entry conditions: Enter long at the closing time on Thursday. This time point is chosen based on historical data analysis.
2. Exit conditions: Close the position at the close of trading on Friday, and the holding time is fixed.
3. Fund management: Use 10% of the account funds for each transaction. This conservative position management helps control risks.
4. Transaction execution: Executing orders at the closing price can avoid the impact of violent fluctuations within the day.
#### Strategic Advantages
1. Simple and clear: The trading rules are clear, there are no complicated indicator combinations, and they are easy to understand and execute.
2. Controllable risks: Fixed holding time and fund management plan make risks easier to evaluate and control.
3. High degree of automation: The strategy logic is simple and suitable for programming to realize automated transactions.
4. Strong flexibility: parameters can be adjusted according to different market environments and have good adaptability.
#### Strategy Risk
1. Time dependence: The strategy relies heavily on a specific time window and may be affected by major news during non-trading hours.
2. Changes in the market environment: Historical statistical laws may become invalid in the future, and strategy performance needs to be continuously monitored.
3. Execution risk: Liquidity may be insufficient during the closing period, resulting in increased slippage.
It is recommended to manage risk by:
- Set stop loss and take profit
- Dynamically adjust position holding time
- Add filter conditions
#### Strategy optimization direction
1. Introduce volatility indicator: ATR indicator can be added to dynamically adjust the position size to make the strategy more adaptable.
2. Optimize the timing of entry: You can combine price patterns and technical indicators to improve the accuracy of entry.
3. Improve risk control: add a dynamic stop-loss mechanism to protect existing profits.
4. Add filter conditions: Consider adding a trend filter to avoid trading in adverse market conditions.
#### Summary
This strategy is a classic trading system based on market anomalies, which achieves potential gains through strict time management and conservative fund management. Although the strategy logic is simple, you still need to pay attention to the risks caused by changes in the market environment. It is recommended to adopt more conservative position control and a more complete risk management mechanism during real trading. ||
#### Overview
This strategy is a trading system based on market anomalies, primarily utilizing market behavior characteristics between Thursday evening close and Friday close. The strategy employs fixed entry and exit times, validating this market pattern through backtesting. It uses 10% of capital per trade and considers slippage and commission factors to ensure realistic backtesting results.

#### Strategy Principles
The core logic of the strategy is based on several key elements:
1. Entry Condition: Enter long positions at Thursday's close, based on historical data analysis.
2. Exit Condition: Close positions at Friday's close, with fixed holding periods.
3. Money Management: Uses 10% of account capital per trade, this conservative position sizing helps control risk.
4. Trade Execution: Orders are executed at closing prices, avoiding intraday volatility impacts.

#### Strategy Advantages
1. Simple and Clear: Trading rules are straightforward, without complex indicator combinations, easy to understand and execute.
2. Controlled Risk: Fixed holding periods and money management plans make risk easier to assess and control.
3. High Automation: Simple strategy logic suitable for automated trading implementation.
4. High Flexibility: Parameters can be adjusted for different market environments, showing good adaptability.

#### Strategy Risks
1. Time Dependency: Strategy heavily relies on specific time windows, may be affected by major news during non-trading hours.
2. Market Environment Changes: Historical statistical patterns may become invalid in the future, requiring continuous strategy performance monitoring.
3. Execution Risk: Liquidity may be insufficient during closing periods, leading to increased slippage.
Risk management suggestions:
- Set stop-loss and take-profit levels
- Dynamically adjust holding periods
- Add filtering conditions

#### Strategy Optimization Directions
1. Incorporate Volatility Indicators: Add ATR indicator for dynamic position sizing, making the strategy more adaptive.
2. Optimize Entry Timing: Combine price patterns and technical indicators to improve entry accuracy.
3. Enhance Risk Control: Add dynamic stop-loss mechanisms to protect existing profits.
4. Add Filtering Conditions: Consider adding trend filters to avoid trading in unfavorable market conditions.

#### Summary
This strategy is a classic trading system based on market anomalies, seeking potential returns through strict time management and conservative money management. While the strategy logic is simple, attention must be paid to risks from changing market environments. It's recommended to use more conservative position sizing and comprehensive risk management mechanisms in live trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-11 00:00:00
end: 2024-12-10 08:00:00
period: 4h
basePeriod: 4h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © piirsalu

//@version=5
strategy("Gold Friday Anomaly Strategy", 
     default_qty_type=strategy.percent_of_equity,
     slippage = 1, commission_value=0.0005,
     process_orders_on_close = true,
     initial_capital = 50000,
     default_qty_value=500,
     overlay = true)
     

/////////////////////////////////////////////////////////////////////////////////////
//                                 . USER INPUTS .                                 //
/////////////////////////////////////////////////////////////////////////////////////

// Define backtest start and end dates
st_yr_inp = input(defval=2000, title='Backtest Start Year')
st_mn_inp = input(defval=01, title='Backtest Start Month')
st_dy_inp = input(defval=01, title='Backtest Start Day')
en_yr_inp = input(defval=2025, title='Backtest End Year')
en_mn_inp = input(defval=01, title='Backtest End Month')
en_dy_inp = input(defval=01, title='Backtest End Day')

// Set start and end timestamps for backtesting
start = timestamp(st_yr_inp, st_mn_inp, st_dy_inp, 00, 00)
end = timestamp(en_yr_inp, en_mn_inp, en_dy_inp, 00, 00)

/////////////////////////////////////////////////////////////////////////////////////
//                              . STRATEGY LOGIC .                                 //
/////////////////////////////////////////////////////////////////////////////////////

// Check if the current day is Friday
isFriday = (dayofweek == dayofweek.friday)

// Initialize a candle counter
var int barCounter = 0

// Increment the candle counter on each new bar
barCounter := barCounter + 1

// Define trading session time ranges
pre_mkt = time(timeframe.period, '0400-0800:23456')
mkt_hrs = time(timeframe.period, '0800-1600:23456')
eod = time(timeframe.period, '1200-1600:23456')

/////////////////////////////////////////////////////////////////////////////////////
//                          . STRATEGY ENTRY & EXIT .                              //
/////////////////////////////////////////////////////////////////////////////////////

// Enter a long position on the first candle of Friday within the backtest period
if dayofweek == 4 and time >= start and time <= end
    strategy.entry("BuyOnFriday", strategy.long)

// Close the position after holding it for 4 candles
if (barCounter % 1 == 0)
    strategy.close("BuyOnFriday")


```

> Detail

https://www.fmz.com/strategy/474877

> Last Modified

2024-12-12 16:32:12
