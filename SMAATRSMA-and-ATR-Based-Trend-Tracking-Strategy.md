
> Name

SMA-and-ATR-Based-Trend-Tracking-Strategy based on SMA and ATR
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ee57f3dcfa96c8d894c4b8020ea132f84b9b87ceef62437c697579dc78a46f2b.png)
[trans]
## 1. Strategy name
The name of this strategy is **Trend following strategy based on SMA and ATR**.
## 2. Strategy Overview
This strategy uses the SMA indicator to determine the direction of the price trend, and uses the ATR indicator to set a stop loss position to track the trend. Go short when the price falls below the uptrend, and go long when the price breaks out of the downtrend to achieve trend trading.
## 3. Strategy Principles
### 1. Enter signal
(1) When the closing price rises and is above the SMA, go long
(2) When the closing price falls and is below the SMA, go short
### 2. Stop loss setting
Use the value of the ATR indicator multiplied by the set stop loss multiple as the stop loss position.
### 3. Stop loss update
After each K line closes, the stop loss position is checked and updated to a stop loss value closer to the current price.
### 4. Exit signal
After the price hits the stop loss line, the price will stop and exit.
## 4. Strategic advantages
### 1. Strong trend following ability
Using the dynamic stop loss setting of the ATR indicator can automatically track the trend.
### 2. Good retracement control ability
Strict stop-loss rules help control the maximum drawdown on a single trade.
### 3. Simple parameter setting
There are only 3 parameters, making it easy to adjust and optimize.
## 5. Strategic Risks
### 1. The stop loss may be too loose
If the stop loss multiple is set too large, the stop loss position may be too loose, thereby increasing the retracement.
### 2. Risks caused by false breakthroughs
When a false breakthrough occurs in the price, it may lead to a deviation from the trend direction, and the signal should be filtered in combination with other indicators.
### 3. Parameter optimization risks
Overreliance on parameter optimization can lead to curve optimization. Parameter stability should be assessed carefully.
## 6. Strategy optimization direction
### 1. Optimize stop loss algorithm
You can test other types of stop loss algorithms, such as trailing stop loss, proportional stop loss, etc.
### 2. Add filter signal
Other indicators can be added to filter out false breakthroughs. For example, increasing trading volume conditions, etc.
### 3. Evaluate parameter stability
Evaluate the adaptability of parameters to different varieties and cycles through historical backtesting.
## 7. Summary
The overall idea of this strategy is clear. It uses SMA to determine the trend direction and uses ATR for trend tracking. It has good retracement control capabilities and is suitable for medium and long-term trend trading. However, it is still necessary to adjust parameters appropriately in real trading and prevent the risk of over-optimization.
|| 

## I. Strategy Name
The strategy is named **SMA and ATR Based Trend Tracking Strategy**.  

## II. Strategy Overview  
This strategy uses the SMA indicator to determine the price trend direction and sets stop loss positions with the ATR indicator to track the trend. It goes short when the price breaks down an uptrend and goes long when the price breaks through a downtrend to implement trend trading.

## III. Strategy Principle
### 1. Entry Signals 
(1) Go long when the close price rises and is higher than SMA.  
(2) Go short when the close price falls and is lower than SMA.   

### 2. Stop Loss Setting
Use the ATR indicator's value multiplied by the set stop loss multiple as the stop loss position.

### 3. Stop Loss Updating  
After each bar's close, check the stop loss position and update it to a stop loss value closer to the current price.  

### 4. Exit Signals
Actively stop loss when price touches stop loss line.  

## IV. Advantages of Strategy
### 1. Strong Trend Tracking Ability 
The dynamic stop loss setting of the ATR indicator enables automatic tracking of trends.

### 2. Good Drawdown Control  
Strict stop loss rules help control maximum drawdown per trade.  

### 3. Simple Parameter Setting  
Only 3 parameters make adjustment and optimization easy.  

## V. Risks of Strategy
### 1. Risk of Stop Loss being too Loose  
If the stop loss multiple is set too high, the stop loss position may be too loose, thus increasing drawdown.  

### 2. Risks of False Breakout  
Price false breakouts may lead to missing the trend direction. Other indicators should be used to filter signals.   

### 3. Risks of Parameter Optimization
Excessive reliance on parameter optimization may lead to curve fitting. The stability of parameters should be carefully evaluated.  

## VI. Strategy Optimization Directions  
### 1. Optimizing Stop Loss Algorithm
Other types of stop loss algorithms can be tested, such as moving stop loss, proportional stop loss, etc.  

### 2. Adding Filter Signals  
Other indicators can be added to filter false breakouts. For example, adding trading volume conditions.  

### 3. Evaluating Stability of Parameters  
Back-testing history to evaluate parameters' adaptability to different products and timeframes.  

## VII. Summary  
The overall idea of this strategy is clear. It judges trend direction through SMA and uses ATR to track trends with good drawdown control. It is suitable for medium-long term trend trading. But parameters still need proper adjustment in live trading, and risks of over-optimization should be prevented.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|100|SMA Length|
|v_input_int_2|10|ATR Length|
|v_input_float_1|4|Stop Offset Multiple|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-16 00:00:00
end: 2024-01-16 17:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © omererkan

//@version=5
strategy(title="SMA with ATR", overlay=true)

smaLen = input.int(100, title="SMA Length")

atrLen     = input.int(10, title="ATR Length")
stopOffset = input.float(4, title="Stop Offset Multiple", step=0.25)


smaValue  = ta.sma(close, smaLen)
stopValue = ta.atr(atrLen) * stopOffset


lowerCloses = close < close[1] and 
     close[1] < close[2] and
     close[2] < close[3]

enterLong = close > smaValue and 
     lowerCloses


longStop = 0.0
longStop := if enterLong and strategy.position_size < 1
    close - stopValue
else
    math.max(close - stopValue, longStop[1])


higherCloses = close > close[1] and 
     close[1] > close[2] and
     close[2] > close[3]

enterShort = close < smaValue and 
     higherCloses


shortStop = 0.0
shortStop := if enterShort and strategy.position_size > -1
    close + stopValue
else
    math.min(close + stopValue, shortStop[1])


plot(smaValue, color=#4169e1, linewidth=2, title="SMA")

plot(strategy.position_size > 0 ? longStop : na, color=color.lime,
     style=plot.style_linebr, title="Long stop", linewidth=2)

plot(strategy.position_size < 0 ? shortStop : na, color=color.red,
     style=plot.style_linebr, title="Short stop", linewidth=2)


if enterLong
    strategy.entry("EL", strategy.long)

if enterShort
    strategy.entry("ES", strategy.short)


if strategy.position_size > 0
    strategy.exit("SL Long", from_entry="EL", stop=longStop)

if strategy.position_size < 0
    strategy.exit("SL Short", from_entry="ES", stop=shortStop)


if enterLong
    strategy.cancel("Exit Short")

if enterShort
    strategy.cancel("Exit Long")

```

> Detail

https://www.fmz.com/strategy/439260

> Last Modified

2024-01-18 16:04:51
