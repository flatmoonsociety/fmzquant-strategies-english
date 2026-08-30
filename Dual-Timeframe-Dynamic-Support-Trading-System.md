
> Name

Dual-Timeframe-Dynamic-Support-Trading-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fed6dbf68c21720800.png)

[trans]
#### Overview
This strategy is a dynamic support level trading system based on dual time frames, trading by combining the crossover signals of the SMA and EMA moving averages on the weekly and daily time frames. The system uses the support band formed between moving averages to identify market trends and trading opportunities, and improves the accuracy of trading through signal confirmation in two different time periods. The strategy adopts a percentage position management method and takes into account transaction costs and slippage factors.
#### Strategy Principle
The core principle of the strategy is to determine trading signals by monitoring the intersection and position relationship of moving averages in two time periods:
1. The long cycle (weekly) uses the 20-week SMA and the 21-week EMA, and the short cycle (daily) uses the 50-day SMA and the 51-day EMA.
2. In a long period, when the EMA crosses the SMA upward, a long signal is generated, and when the EMA crosses downward, a closing signal is generated.
3. In the short period, a long signal is generated when the EMA crosses the SMA upward and the short period EMA is above the long period EMA.
4. When a short-selling signal appears in a short period or the long-term moving average crosses downward, the system will close all long orders.
5. The strategy runs within the specified time range, and positions will be automatically closed if they exceed the range.
#### Strategic Advantages
1. Multiple confirmation mechanism: reduce the impact of false signals through signal confirmation in two time periods
2. Dynamic support band: The support band formed between moving averages can dynamically adapt to market changes.
3. Improved risk management: including consideration of transaction costs and slippage, using percentage position management
4. Strong adaptability: the support band will automatically adjust its position according to market fluctuations
5. Clear operating rules: clear entry and exit conditions, easy to execute and backtest
#### Strategy Risk
1. Volatile market risk: Frequent false signals may occur in a volatile market.
2. Lagging risk: The moving average indicator itself has a certain lag and may miss the best entry point.
3. Parameter sensitivity: The choice of moving average period has a greater impact on strategy performance
4. Market environment dependence: The strategy performs better in trending markets, but may perform poorly in violently volatile markets.
5. Fund management risk: Fixed percentage positions may be too risky under certain market conditions
#### Strategy optimization direction
1. Introduce volatility indicators: Consider adding volatility indicators such as ATR to dynamically adjust position sizes
2. Optimize parameter selection: You can optimize system performance by backtesting moving average parameters in different time periods.
3. Add market environment filtering: add trend strength indicator to filter unsuitable market environment
4. Improve the stop loss mechanism: Consider adding a trailing stop or fixed stop to further control risks
5. Optimize position management: position size can be dynamically adjusted based on signal strength and market fluctuations
#### Summary
This strategy builds a relatively robust trading system by combining moving average crossover signals of different time periods. Identify market trends through the concept of support bands, and use multiple confirmation mechanisms to improve the accuracy of transactions. The design of the strategy takes into account various factors in actual trading, including transaction costs, slippage and time management. Although there are some inherent risks, the stability and profitability of the strategy can be further improved through the optimization directions provided. ||
#### Overview
This strategy is a dual timeframe dynamic support trading system that combines SMA and EMA crossover signals on weekly and daily timeframes. The system utilizes support bands formed between moving averages to identify market trends and trading opportunities, enhancing trading accuracy through signal confirmation from two different time periods. The strategy employs percentage-based position management and accounts for trading costs and slippage.

#### Strategy Principles
The core principle revolves around monitoring moving average crossovers and relative positions across two timeframes:
1. Long timeframe (weekly) uses 20-week SMA and 21-week EMA, short timeframe (daily) uses 50-day SMA and 51-day EMA
2. In the long timeframe, long signals are generated when EMA crosses above SMA, and positions are closed on downward crosses
3. In the short timeframe, long signals occur when EMA crosses above SMA and short-term EMA is above long-term EMA
4. All long positions are closed when short timeframe generates short signals or long timeframe shows downward crosses
5. The strategy operates within specified time ranges with automatic position closure outside these ranges

#### Strategy Advantages
1. Multiple confirmation mechanism: Reduces false signals through dual timeframe confirmation
2. Dynamic support band: Support bands between moving averages adapt to market changes
3. Comprehensive risk management: Includes consideration of trading costs and slippage with percentage-based position sizing
4. Strong adaptability: Support bands automatically adjust to market volatility
5. Clear operational rules: Well-defined entry and exit conditions, easy to implement and backtest

#### Strategy Risks
1. Choppy market risk: May generate frequent false signals in sideways markets
2. Lag risk: Moving averages have inherent lag, potentially missing optimal entry points
3. Parameter sensitivity: Strategy performance heavily depends on moving average period selection
4. Market environment dependency: Performs better in trending markets but may struggle in highly volatile conditions
5. Position sizing risk: Fixed percentage positioning may present excessive risk in certain market conditions

#### Optimization Directions
1. Incorporate volatility indicators: Consider adding ATR for dynamic position sizing
2. Optimize parameter selection: Backtest different moving average periods to optimize system performance
3. Add market environment filters: Implement trend strength indicators to filter unsuitable market conditions
4. Enhance stop-loss mechanisms: Consider adding trailing or fixed stops for better risk control
5. Improve position management: Dynamically adjust position sizes based on signal strength and market volatility

#### Conclusion
This strategy builds a relatively robust trading system by combining moving average crossover signals from different timeframes. It identifies market trends through the support band concept and uses multiple confirmation mechanisms to improve trading accuracy. The strategy design considers various practical trading factors, including trading costs, slippage, and time management. While inherent risks exist, the suggested optimization directions can further enhance the strategy's stability and profitability.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-04 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Demo GPT - Bull Market Support Band", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_value=0.1, slippage=3)

start_date = input(timestamp("2018-01-01 00:00 +0000"), title="Start Date")
end_date = input(timestamp("2069-12-31 00:00 +0000"), title="End Date")

lsmaLength = input.int(20, title="Long SMA Length", minval=1)
lemaLength = input.int(21, title="Long EMA Length", minval=1)
customLongTimeframe = input.timeframe("W", title="Long Timeframe")  // Khung thời gian dài
ssmaLength = input.int(50, title="Short SMA Length", minval=1)
semaLength = input.int(51, title="Short EMA Length", minval=1)
customShortTimeframe = input.timeframe("D", title="Short Timeframe")  // Khung thời gian ngắn

source = close

// Tính toán SMA và EMA cho khung thời gian dài
smaLong = ta.sma(source, lsmaLength)
emaLong = ta.ema(source, lemaLength)
outSmaLong = request.security(syminfo.tickerid, customLongTimeframe, smaLong)
outEmaLong = request.security(syminfo.tickerid, customLongTimeframe, emaLong)

// Tính toán SMA và EMA cho khung thời gian ngắn
smaShort = ta.sma(source, ssmaLength)
emaShort = ta.ema(source, semaLength)
outSmaShort = request.security(syminfo.tickerid, customShortTimeframe, smaShort)
outEmaShort = request.security(syminfo.tickerid, customShortTimeframe, emaShort)

// Plot các chỉ báo trên biểu đồ
smaPlotLong = plot(outSmaLong, color=color.new(color.red, 0), title='20w SMA (Long)')
emaPlotLong = plot(outEmaLong, color=color.new(color.green, 0), title='21w EMA (Long)')
smaPlotShort = plot(outSmaShort, color=color.new(color.red, 0), title='20d SMA (Short)')
emaPlotShort = plot(outEmaShort, color=color.new(color.green, 0), title='21d EMA (Short)')

// Fill vùng giữa các đường SMA và EMA
fill(smaPlotLong, emaPlotLong, color=color.new(color.orange, 75), fillgaps=true)
fill(smaPlotShort, emaPlotShort, color=color.new(color.orange, 75), fillgaps=true)

// Điều kiện long và short cho khung thời gian dài
longConditionLong = ta.crossover(outEmaLong, outSmaLong)
shortConditionLong = ta.crossunder(outEmaLong, outSmaLong)

// Điều kiện long và short cho khung thời gian ngắn
longConditionShort = ta.crossover(outEmaShort, outSmaShort) and (outEmaShort > outEmaLong)
shortConditionShort = ta.crossunder(outEmaShort, outSmaShort) and (outEmaShort > outEmaLong) // Điều kiện short khi EMA ngắn hạn cắt xuống dưới SMA ngắn hạn và EMA ngắn hạn cao hơn EMA dài hạn

// Kiểm tra điều kiện trong khoảng thời gian được chỉ định
inDateRange = true

// Nếu khung ngắn hạn xuất hiện tín hiệu short, ưu tiên đóng tất cả các lệnh Long
if shortConditionShort and inDateRange
    strategy.close_all()

// Nếu khung dài có tín hiệu short, đóng tất cả các lệnh Long
if shortConditionLong and inDateRange
    strategy.close_all()

// Nếu khung ngắn hạn có tín hiệu long và không có tín hiệu short từ khung dài, vào lệnh Long
if longConditionShort and not shortConditionLong and not shortConditionShort and inDateRange
    strategy.entry("Long", strategy.long)

// Đóng tất cả các lệnh khi không trong khoảng thời gian được chọn
if not inDateRange
    strategy.close_all()

```

> Detail

https://www.fmz.com/strategy/474062

> Last Modified

2024-12-05 16:44:56
