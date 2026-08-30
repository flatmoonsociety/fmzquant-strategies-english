
> Name

RSI-Moving-Average-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

This strategy integrates RSI indicators and moving averages to determine trends and generate trading signals, and uses moving stop-loss and take-profit methods to lock in profits and control risks. It is a typical trend following trading strategy.
Strategy principle:
1. Calculate the RSI indicator to determine overbought and oversold conditions. RSI above 50 is a bullish signal.
2. Calculate the fast and slow moving average, and the golden cross pattern is a long signal.
3. The continuous rise of RSI can also be used as a trading signal to track long positions.
4. After entering the market, set a moving stop loss line and a take profit line.
5. The stop-loss line is fixed to track below the price, and the take-profit line is fixed to track above the price.
6. The position will be closed when the price hits the stop-loss and take-profit lines.
Advantages of this strategy:
1. The RSI indicator determines overbought and oversold, and avoids chasing highs and selling lows.
2. Moving averages identify trend direction. The combination improves judgment accuracy.
3. Moving stop loss and take profit method, the stop loss position can be adjusted according to real-time price changes.
Risks of this strategy:
1. RSI indicators and moving averages are prone to produce false signals in volatile markets.
2. The range of trailing stop loss and take profit needs to be set carefully. There will be problems if it is too large or too small.
3. There is no way to limit the size of a single loss, and there is a risk of large losses.
In short, this strategy brings together the advantages of RSI and moving average indicators, and uses a moving stop-loss and take-profit method for risk management. Improvements in parameter optimization and risk control can achieve better results.
||

This strategy combines RSI and moving averages for trend bias and adds trailing stops for risk management. It aims to follow trends with adaptive exits.

Strategy Logic:

1. Calculate RSI to judge overbought/oversold levels. RSI above 50 signals bullishness. 

2. Compute fast and slow moving averages, golden cross signals bull trend.

3. Consistent RSI rise also signals long entry.

4. After entry, set trailing stop loss and take profit lines.

5. Stop loss trail below price, take profit trail above.

6. Exit when price hits stop or take profit.

Advantages:

1. RSI avoids chasing tops and bottoms.

2. Moving averages identify trend direction. Combination improves accuracy.

3. Trailing stops/profits adjust dynamically to price.

Risks:

1. RSI and MAs prone to false signals in ranging markets.

2. Trailing stop width requires prudent calibration, too wide or too narrow problematic.

3. Unable to limit loss size, risks large losing trades. 

In summary, this strategy combines RSI and MAs then uses trailing stops for risk management. With robust optimization and risk controls, it can achieve good results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_2|14|length|
|v_input_float_1|2|Trail Long Loss (%)|
|v_input_float_2|true|Trail Short Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-06 00:00:00
end: 2023-09-12 00:00:00
period: 4d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("RSI and MA Strategy with Trailing Stop Loss and Take Profit",
         overlay=true,
         initial_capital=1000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=100,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 1, 1, 0, 0)
notInTrade = strategy.position_size <= 0

//==================================Buy Conditions============================================

//RSI
length = input(14)
rsi = ta.rsi(close, length)
buyCondition1 = rsi > 50

//MA
SMA9 = ta.sma(close, 9)
SMA50 = ta.sma(close, 50)
SMA100 = ta.sma(close, 100)
plot(SMA9, color = color.green)
plot(SMA50, color = color.orange)
plot(SMA100, color = color.blue)
buyCondition2 = SMA9 > SMA50//ta.crossover(SMA9, SMA100)

//RSI Increase
increase = 5
buyCondition3 = (rsi > rsi[1] + increase)


if (buyCondition1 and buyCondition2 and buyCondition3 and timePeriod) //and buyCondition
    strategy.entry("Long", strategy.long)

//==================================Sell Conditions============================================

//Trailing Stop Loss and Take Profit
longTrailPerc = input.float(title='Trail Long Loss (%)', minval=0.0, step=0.1, defval=2) * 0.01
shortTrailPerc = input.float(title='Trail Short Loss (%)', minval=0.0, step=0.1, defval=1) * 0.01

longStopPrice = 0.0
shortStopPrice = 0.0

longStopPrice := if strategy.position_size > 0
    stopValue = close * (1 - longTrailPerc)
    math.max(stopValue, longStopPrice[1])
else
    0

shortStopPrice := if strategy.position_size < 0
    stopValue = close * (1 + shortTrailPerc)
    math.min(stopValue, shortStopPrice[1])
else
    999999


strategy.exit(id="Exit", stop = longStopPrice, limit = shortStopPrice)
```

> Detail

https://www.fmz.com/strategy/426576

> Last Modified

2023-09-13 14:26:43
