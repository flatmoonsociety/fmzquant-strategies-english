
> Name

Trend-Following-Average-True-Range-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/bd08661a998133129e914a5cc5f2ef8d1d1d945275772fbd559f94f16f36e4ec.png)

[trans]
#### Overview
This strategy uses the average true range (ATR) as the basis for the trailing stop (TS), and achieves the purpose of tracking the trend by dynamically adjusting the stop loss position. When the price moves in a favorable direction, the stop loss position will also be adjusted accordingly, thereby locking in the profits obtained; when the price moves in an unfavorable direction, the stop loss position remains unchanged, and once the price hits the stop loss price, the position will be closed and the stop loss will be closed. The key to this strategy lies in the dynamic adjustment of the stop loss position, which can not only protect the profits obtained, but also allow the profits to continue to expand as the trend continues.
#### Strategy Principle
1. Calculate ATR as the basis for trailing stop loss. ATR reflects market volatility and is used to measure the average magnitude of price changes.
2. Calculate the stop loss distance nLoss based on the ATR and KeyValue parameters. KeyValue is a user-defined multiple, and nLoss is the product of KeyValue and ATR, indicating how many times the stop loss distance is ATR.
3. Calculate the dynamic trailing stop position xATRTrailingStop. When holding a long position, set it to "the larger value of the highest price of the previous K line and (closing price - nLoss)"; when holding a short position, set it to "the smaller value of the lowest price of the previous K line and (closing price + nLoss)".
4. Generate a signal to open a position. When the closing price crosses xATRTrailingStop, go long; when the closing price crosses xATRTrailingStop, go short.
#### Advantage Analysis
1. The stop loss position is dynamically adjusted with price fluctuations, which can not only lock in profits, but also allow profits to expand as the trend continues.
2. The stop loss position is calculated based on ATR, which can objectively reflect market volatility and is more flexible and effective than a subjectively set fixed stop loss.
3. By enlarging the ATR through the KeyValue parameter, you can set an appropriate stop loss distance according to your own risk preference. A larger KeyValue will bring wider stop loss space and less stop loss frequency.
#### Risk Analysis
1. Trend-based strategies perform poorly in volatile markets. When the unilateral trend is not obvious, losses will be stopped frequently, resulting in rapid loss of funds.
2. The timing of entry depends on the cross signal between the closing price and the dynamic stop loss line. Continuous small stop losses may occur in volatile market conditions.
3. The trailing stop loss strategy cannot avoid gaps caused by huge negative or positive results, and the adjustment speed of the stop loss position cannot keep up with the speed of price changes, resulting in actual losses far greater than the expected controllable losses.
#### Optimization direction
1. Trend judgment indicators can be added to the strategy, such as moving average systems, momentum indicators, etc. Only enter the market when the trend is clear to avoid frequent trading in volatile markets.
2. You can consider introducing a take-profit strategy, such as calculating positions based on the Kelly formula, setting a fixed profit point to retrace take-profit, etc., to reduce the possibility of potential profit taking at the end of the trend.
3. For gap openings, you can set a maximum stop loss limit, such as a fixed amount or a fixed percentage. Once this limit is reached, the loss will be stopped immediately no matter where the dynamic stop loss price is.
#### Summary
The ATR tracking stop loss strategy can dynamically adjust the stop loss position according to the price fluctuation range, and can achieve good results in trending markets. However, this strategy also has risks such as being unable to cope with volatile markets, stopping losses too frequently, and being unable to avoid gaps. In view of the above defects, the strategy can be optimized and improved from the aspects of trend judgment, profit-taking strategy, maximum stop-loss limit, etc. Through these adjustments, it is expected to enhance the adaptability and profitability of the strategy.
|| 

#### Overview
This strategy uses the Average True Range (ATR) as the basis for a Trailing Stop (TS), dynamically adjusting the stop-loss position to follow the trend. When the price moves in a favorable direction, the stop-loss position is adjusted accordingly to lock in profits; when the price moves in an adverse direction, the stop-loss position remains unchanged, and once the price reaches the stop-loss price, the position is closed. The key to this strategy lies in the dynamic adjustment of the stop-loss position, which can both protect profits and allow profits to expand as the trend continues.

#### Strategy Principle
1. Calculate the ATR as the basis for the trailing stop. ATR reflects market volatility and is used to measure the average magnitude of price changes.
2. Calculate the stop-loss distance nLoss based on the ATR and the KeyValue parameter. KeyValue is a user-defined multiplier, and nLoss is the product of KeyValue and ATR, indicating that the stop-loss distance is several times the ATR.
3. Calculate the dynamic trailing stop position xATRTrailingStop. For a long position, it is set to the greater of "the highest price of the previous candle and (close - nLoss)"; for a short position, it is set to the lesser of "the lowest price of the previous candle and (close + nLoss)".
4. Generate entry signals. When the closing price crosses above xATRTrailingStop, go long; when the closing price crosses below xATRTrailingStop, go short.

#### Advantage Analysis
1. The stop-loss position is dynamically adjusted with price fluctuations, allowing profits to be locked in while also allowing profits to expand as the trend continues.
2. The stop-loss position is based on the ATR calculation, which can objectively reflect market volatility and is more flexible and effective compared to subjectively set fixed stop-losses.
3. By amplifying the ATR with the KeyValue parameter, you can set an appropriate stop-loss distance based on your risk preference. A larger KeyValue will result in a wider stop-loss space and fewer stop-loss occurrences.

#### Risk Analysis
1. Trend-following strategies perform poorly in choppy markets, and when the unilateral trend is not clear, frequent stop-losses can lead to rapid loss of funds.
2. The entry timing relies on the cross signal between the closing price and the dynamic stop-loss line, which may result in consecutive small stop-losses in a choppy market.
3. Trailing stop strategies cannot avoid gaps caused by significant bearish or bullish news, and the adjustment speed of the stop-loss position cannot keep up with the price change speed, resulting in actual losses far greater than expected controllable losses.

#### Optimization Direction
1. Trend judgment indicators, such as moving average systems and momentum indicators, can be added to the strategy to only enter the market when the trend is clear, avoiding frequent trading in choppy markets.
2. A take-profit strategy can be considered, such as calculating position sizes based on the Kelly formula, setting fixed profit points for retracement stop-profits, etc., to reduce the possibility of potential profit givebacks at the end of a trend.
3. For gap openings, a maximum stop-loss limit can be set, such as a fixed amount or a fixed percentage. Once this limit is reached, the position is immediately stopped out regardless of where the dynamic stop-loss price is.

#### Summary
The ATR trailing stop strategy can dynamically adjust the stop-loss position based on the magnitude of price fluctuations and can achieve good results in trending markets. However, this strategy also has risks such as inability to cope with choppy markets, excessive stop-loss frequency, and difficulty in avoiding gap openings. To address these shortcomings, the strategy can be optimized and improved in terms of trend judgment, take-profit strategies, and maximum stop-loss limits. With these adjustments, the strategy's adaptability and profitability can hopefully be enhanced.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-01 00:00:00
end: 2024-04-30 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Long TAP", overlay=true)

// Constants
keyValueDefault = 3.0
keyValueStep = 0.5
atrPeriodDefault = 10

// Inputs
keyValue = input.float(keyValueDefault, title="Key Value")
atrPeriod = input.int(atrPeriodDefault, title="ATR Period")

// Calculations
xATR = ta.atr(atrPeriod)
nLoss = keyValue * xATR

// Trailing Stop Calculation
var float xATRTrailingStop = 0.0
xATRTrailingStop := ta.highest(math.max(nz(xATRTrailingStop[1], 0), close - nLoss), 1)
xATRTrailingStop := ta.lowest(math.min(nz(xATRTrailingStop, 0), close + nLoss), 1)

// Position Calculation
var int pos = 0
pos := nz(pos[1], 0)
if (close[1] < nz(xATRTrailingStop, 0) and close > nz(xATRTrailingStop, 0))
    pos := 1
else if (close[1] > nz(xATRTrailingStop, 0) and close < nz(xATRTrailingStop, 0))
    pos := -1

// Plotting Trailing Stop
var color xcolor = na
if (pos == -1)
    xcolor := color.red
else if (pos == 1)
    xcolor := color.green
plot(xATRTrailingStop, color=xcolor, title="Trailing Stop")

// Buy/Sell Signals
buySignal = ta.crossover(close, xATRTrailingStop)
sellSignal = ta.crossunder(close, xATRTrailingStop)

// Strategy
if (buySignal)
    strategy.entry("Long", strategy.long)
    label.new(bar_index, xATRTrailingStop, text="Buy Signal", color=color.green, style=label.style_label_up, yloc=yloc.belowbar)
if (sellSignal)
    strategy.entry("Short", strategy.short)
    label.new(bar_index, xATRTrailingStop, text="Sell Signal", color=color.red, style=label.style_label_down, yloc=yloc.abovebar)

// Alerts
alertcondition(buySignal, title='UT BOT Buy', message='UT BOT Buy')
alertcondition(sellSignal, title='UT BOT Sell', message='UT BOT Sell')

```

> Detail

https://www.fmz.com/strategy/452364

> Last Modified

2024-05-24 18:12:01
