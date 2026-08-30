
> Name

Black-Swan-Volatility-and-Moving-Average-Crossover-Momentum-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13fa94a39de0470476e.png)

[trans]
#### Overview
This strategy is a momentum tracking trading system based on price fluctuations and moving average crossovers. The strategy mainly triggers signals by monitoring abnormal fluctuations in price volatility exceeding 1.91% (black swan events), and combines the intersection of EMA144 and EMA169 to confirm the trend direction and exit timing. The strategy is particularly suitable for short-cycle trading of 1-3 minutes, and can quickly capture opportunities for violent market fluctuations.
#### Strategy Principle
The core logic of the strategy consists of two main parts:
1. Volatility monitoring: Measure price fluctuations by calculating the ratio of the absolute difference between the closing price and the opening price relative to the closing price. When the ratio exceeds 1.91%, a trading signal is triggered.
2. Trend confirmation: Use the cross of EMA144 and EMA169 to confirm the trend direction. If the cross crosses upward, go long, and if the cross crosses downward, go short. SMA60 and SMA20 are also introduced as auxiliary indicators.
The strategy goes long when it detects upward fluctuations greater than 1.91%, and goes short when it detects downward fluctuations. When the moving average crosses in reverse, the strategy will automatically close positions to control risks.
#### Strategic Advantages
1. Quick response: The strategy can capture the violent fluctuations of the market in a timely manner and is especially suitable for short-cycle trading.
2. Risk control: Use moving average crossover as a closing signal to effectively control position risks.
3. High flexibility: The strategy allows setting the backtest time range and parameter adjustment, and can be optimized according to different market conditions.
4. Perfect position management: Use the account net value percentage for position control, and support pyramid positions up to 3 times.
#### Strategy Risk
1. False breakthrough risk: False signals may appear in highly volatile markets, leading to unnecessary transactions.
2. Slippage risk: Since the strategy operates in a short period, it may face larger slippage losses.
3. Trend reversal risk: A rapid trend reversal may occur after severe fluctuations.
4. Parameter sensitivity: The strategy effect is more sensitive to parameter settings and may require frequent adjustments under different market conditions.
#### Strategy optimization direction
1. Introducing volatility filtering: It is recommended to add the ATR indicator to filter market noise and improve signal quality.
2. Optimize entry timing: You can consider increasing transaction volume confirmation to improve entry accuracy.
3. Dynamically adjust parameters: It is recommended to develop an adaptive parameter system to automatically adjust the trigger threshold according to market conditions.
4. Improve the stop loss mechanism: It is recommended to add a trailing stop loss function to better protect existing profits.
#### Summary
This strategy achieves rapid response to abnormal market fluctuations and trend following by combining volatility monitoring and moving average crossovers. The strategy design is reasonable and has a good risk control mechanism, but traders still need to optimize parameters and manage risks based on actual market conditions. It is recommended to start with small positions in real trading and gradually verify the performance of the strategy in different market environments. ||
#### Overview
This strategy is a momentum tracking trading system based on price volatility and moving average crossovers. It triggers signals by monitoring price volatility exceeding 1.91% (Black Swan events) and combines EMA144 and EMA169 crossovers to confirm trend direction and exit timing. The strategy is particularly suitable for short-term trading on 1-3 minute timeframes, capable of quickly capturing significant market volatility opportunities.

#### Strategy Principle
The core logic consists of two main components:
1. Volatility Monitoring: Calculates the absolute difference between closing and opening prices relative to the closing price, triggering trading signals when this ratio exceeds 1.91%.
2. Trend Confirmation: Uses EMA144 and EMA169 crossovers to confirm trend direction, going long on upward crosses and short on downward crosses. SMA60 and SMA20 are also incorporated as auxiliary indicators.

The strategy enters long positions when detecting upward volatility above 1.91% and short positions for downward volatility. Positions are automatically closed when moving averages cross in the opposite direction to manage risk.

#### Strategy Advantages
1. Quick Response: The strategy promptly captures sharp market movements, ideal for short-term trading.
2. Risk Control: Uses moving average crossovers as exit signals to effectively manage position risk.
3. High Flexibility: Allows for backtesting period customization and parameter adjustment to optimize for different market conditions.
4. Comprehensive Position Management: Uses account equity percentage for position sizing and supports up to 3x pyramid scaling.

#### Strategy Risks
1. False Breakout Risk: May generate false signals in highly volatile markets leading to unnecessary trades.
2. Slippage Risk: Short-term operations may face significant slippage losses.
3. Trend Reversal Risk: Possibility of rapid trend reversals following extreme volatility.
4. Parameter Sensitivity: Strategy performance is highly dependent on parameter settings, requiring frequent adjustments under different market conditions.

#### Optimization Directions
1. Incorporate Volatility Filtering: Recommend adding ATR indicator to filter market noise and improve signal quality.
2. Optimize Entry Timing: Consider adding volume confirmation to enhance entry accuracy.
3. Dynamic Parameter Adjustment: Suggest developing an adaptive parameter system to automatically adjust trigger thresholds based on market conditions.
4. Enhanced Stop-Loss Mechanism: Recommend adding trailing stop-loss functionality to better protect accumulated profits.

#### Summary
This strategy achieves quick response to market anomalies and trend following by combining volatility monitoring with moving average crossovers. While the strategy design is sound with good risk control mechanisms, traders need to optimize parameters and manage risks according to actual market conditions. It's recommended to start with small positions in live trading and gradually validate strategy performance across different market environments.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-05 00:00:00
end: 2024-12-12 00:00:00
period: 45m
basePeriod: 45m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5

//黑天鹅警报器，作者（）：道格拉斯机器人
//适合1分钟-3分钟的k线，发生波动超过百分之二时，自动报警
strategy('黑天鹅警报', overlay=true, initial_capital=10000, currency='USD', default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.075, pyramiding=3)
//-------------------------------------------
//-------------------------------------------
timecondition = timeframe.period == '480' or timeframe.period == '240' or timeframe.period == 'D' or timeframe.period == '720'
// Make input options that configure backtest date range
startDate = input.int(title='Start Date', defval=1, minval=1, maxval=31)
startMonth = input.int(title='Start Month', defval=11, minval=1, maxval=12)
startYear = input.int(title='Start Year', defval=2018, minval=1800, maxval=2100)
endDate = input.int(title='End Date', defval=1, minval=1, maxval=31)
endMonth = input.int(title='End Month', defval=11, minval=1, maxval=12)
endYear = input.int(title='End Year', defval=2031, minval=1800, maxval=2100)
// Look if the close time of the current bar
// falls inside the date range
inDateRange = time >= timestamp(syminfo.timezone, startYear, startMonth, startDate, 0, 0) and time < timestamp(syminfo.timezone, endYear, endMonth, endDate, 0, 0)



// Inputs
a = input(1, title='Key Vaule. \'This changes the sensitivity\'')
c = input(10, title='ATR Period')
h = input(false, title='Signals from Heikin Ashi Candles')


ma60 = ta.sma(close, 60)
ema144 = ta.ema(close, 144)

ema169 = ta.ema(close, 169)
ma20 = ta.sma(close, 20)


plot(ema144, color=color.new(color.yellow, 0), title='144')
plot(ema169, color=color.new(color.orange, 0), title='169')


heitiane = close - open
heitiane := math.abs(heitiane)
heitiane /= close

if inDateRange and heitiane > 0.0191 and close < open  //  and close>f3
    strategy.entry('botsell20', strategy.short, comment='黑天鹅追空' + str.tostring(heitiane))

if ta.crossover(ema144, ema169)
    strategy.close('botsell20', comment='平空')
if inDateRange and heitiane > 0.0191 and close > open  //  and close>f3
    strategy.entry('botbuy20', strategy.long, comment='白天鹅追多' + str.tostring(heitiane))

if ta.crossunder(ema144, ema169)
    strategy.close('botbuy20', comment='平多')



```

> Detail

https://www.fmz.com/strategy/474981

> Last Modified

2024-12-13 11:52:51
