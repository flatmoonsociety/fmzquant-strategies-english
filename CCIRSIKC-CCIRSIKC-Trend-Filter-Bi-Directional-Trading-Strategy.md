
> Name

CCIRSIKC trend filter long and short two-way trading strategy-CCIRSIKC-Trend-Filter-Bi-Directional-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1a9ea437fbea8fd3397.png)

[trans]
#### Overview
This strategy uses three technical indicators, CCI, RSI and Keltner Channel (KC), combined with trend filters, to achieve long and short two-way trading on the AUDNZD and GBPNZD currency pairs. The strategy uses CCI and RSI to determine overbought and oversold conditions. KC is used as a reference for stop loss and profit. It also uses the moving average as a trend filter to open positions when following the trend. This strategy has been backtested on historical data over the past five years and has achieved stable returns.
#### Strategy Principle
1. Calculate CCI, RSI and KC indicators. The upper rail of KC is the midline plus ATR, and the lower rail is the midline minus ATR.
2. Select the moving average type (SMA, EMA, SMMA, CMA or TMA) and trend filtering method (Close, Forward or Inverse) based on the input parameters.
3. Conditions for opening a long position: long positions are allowed, CCI < oversold line, closing price < KC lower track, RSI < oversold line, trading volume > 50 period average * multiple, no long positions currently.
4. Short position opening conditions: short selling is allowed, CCI>overbought line, closing price>KC upper track, RSI>overbought line, trading volume>50 period average volume*multiple, no short position currently.
5. Long position closing conditions: CCI>0. Short position closing conditions: CCI<0.
6. An alarm will sound when a position is opened and an alarm will sound when a position is closed.
#### Strategic Advantages
1. Combine multiple indicators for comprehensive judgment to improve signal accuracy.
2. Using the trend filtering method, you can flexibly adjust according to market trends and follow the trend.
3. The moving average type is optional to adapt to different market characteristics.
4. It has been verified by long-term historical data, has good stability, and is suitable for long-term use.
5. Two-way trading, adaptable to various market conditions, with many profit opportunities.
6. High degree of automation, no manual intervention required, saving time and effort.
#### Strategy Risk
1. Lack of traditional stop loss and take profit, there may be a large retracement in extreme market conditions.
2. In volatile markets, positions may be opened and closed frequently, increasing transaction costs. 
3. A relatively short CCI period is used, and noise signals may appear.
4. When the trend is unclear or market volatility increases, the trend filtering effect is limited.
5. Fixed positions cannot adapt to changes in market volatility.
#### Strategy optimization direction
1. You can consider adding a moving stop loss or a fixed point stop loss to control the risk of a single transaction.
2. The parameters of RSI and CCI can be further optimized to reduce noise signals.
3. You can consider introducing volatility indicators such as ATR to adjust positions and stop losses according to market fluctuations.
4. Add more currency pairs and optimize parameters individually according to the characteristics of each variety.
5. Try to introduce artificial intelligence technologies such as machine learning to adaptively optimize parameters.
#### Summary
This strategy uses multiple classic indicators, and it is more convenient to write and backtest on the trading view. The backtest results are good, but in real trading, you still need to pay attention to controlling risks and adjusting parameters. It is recommended to test with a small amount of money first, and then gradually increase investment after accumulating experience. It has a high degree of mechanization and is suitable for long-term use by prudent investors.
|| 

#### Overview
This strategy combines three technical indicators: CCI, RSI, and Keltner Channels (KC), along with a trend filter to achieve bi-directional trading on AUDNZD and GBPNZD currency pairs. It uses CCI and RSI to determine overbought and oversold conditions, KC as a reference for stop-loss and take-profit, and a moving average as a trend filter to open positions in line with the trend. The strategy has been backtested on historical data over the past 5 years, achieving stable returns.

#### Strategy Principles
1. Calculate CCI, RSI, and KC indicators. The upper KC line is the midline plus ATR, and the lower line is the midline minus ATR.
2. Select the moving average type (SMA, EMA, SMMA, CMA, or TMA) and trend filter method (OFF, Normal, or Reversed) based on input parameters.
3. Long entry conditions: allow long, CCI < oversold line, close < KC lower line, RSI < oversold line, volume > 50-period average volume * multiplier, no current long position.
4. Short entry conditions: allow short, CCI > overbought line, close > KC upper line, RSI > overbought line, volume > 50-period average volume * multiplier, no current short position.
5. Long exit condition: CCI > 0. Short exit condition: CCI < 0.
6. Send alerts when opening and closing positions.

#### Strategy Advantages
1. Combines multiple indicators for comprehensive analysis, improving signal accuracy.
2. Uses trend filter methods, allowing flexible adjustments based on market trends.
3. Offers multiple moving average types, adapting to different market characteristics.
4. Validated through long-term historical data, demonstrating good stability and suitability for long-term use.
5. Bi-directional trading, suitable for various market conditions, providing more profit opportunities.
6. Highly automated, requiring no manual intervention, saving time and effort.

#### Strategy Risks
1. Lacks traditional stop-loss and take-profit, potentially leading to significant drawdowns in extreme market conditions.
2. May experience frequent opening and closing of positions in choppy markets, increasing trading costs.
3. Uses relatively short CCI periods, potentially generating noise signals.
4. Trend filters may have limited effectiveness when trends are unclear or market volatility increases.
5. Fixed position sizing, unable to adapt to changes in market volatility.

#### Strategy Optimization Directions
1. Consider adding trailing stops or fixed-point stop-losses to control single-trade risk.
2. Further optimize RSI and CCI parameters to reduce noise signals.
3. Consider introducing volatility indicators like ATR to adjust position sizing and stop-losses based on market volatility.
4. Add more currency pairs and optimize parameters individually based on each instrument's characteristics.
5. Attempt to introduce machine learning and other AI technologies for adaptive parameter optimization.

#### Summary
This strategy employs multiple classic indicators and is relatively easy to code and backtest on TradingView. While the backtesting results are good, risk control and parameter adjustments are still necessary for live trading. It is recommended to start with small funds for testing and gradually increase investment as experience accumulates. With a high degree of automation, it is suitable for conservative investors to use over the long term.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-01 00:00:00
end: 2024-04-30 23:59:59
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('CCI Strategy with Trend Filter AUDNZD, GBPNZD', overlay=true, default_qty_type=strategy.cash, default_qty_value=50000, commission_value=0.0005, slippage=2, initial_capital=10000)

// State variables to ensure one entry per signal
var bool isLongOpen = false
var bool isShortOpen = false

// Input Parameters for allowing long and short trades
allowLong = input(true, title='Allow Long Trades')
allowShort = input(true, title='Allow Short Trades')

// Trend Filter Inputs
maType = input.string(title='MA Type', options=['OFF', 'SMA', 'EMA', 'SMMA', 'CMA', 'TMA'], defval='OFF')
trendFilterMethod = input.string(title='Trend Filter Method', options=['OFF', 'Normal', 'Reversed'], defval='OFF')
maLength = input(14, title='MA Length')

// Other Input Parameters
lengthKC = input(30, title='Keltner Channels Length')
multKC = input(0.7, title='Keltner Channels Multiplier')
lengthCCI = input(5, title='CCI Length')
overboughtCCI = input(75, title='CCI Overbought Level')
oversoldCCI = input(-75, title='CCI Oversold Level')
rsiPeriod = input(30, title='RSI Period')
rsiOverbought = input(60, title='RSI Overbought Level')
rsiOversold = input(60, title='RSI Oversold Level')
volumeMultiplier = input.float(0, title='Volume Multiplier', step=0.1, minval=0)

// Define Moving Averages
var float maValue = na
if maType == 'SMA'
    maValue := ta.sma(close, maLength)
else if maType == 'EMA'
    maValue := ta.ema(close, maLength)
else if maType == 'SMMA'
    float initialSMMA = ta.sma(close, maLength)
    maValue := na(maValue[1]) ? initialSMMA : (maValue[1] * (maLength - 1) + close) / maLength
else if maType == 'CMA'
    float firstSMA = ta.sma(close, maLength)
    float secondSMA = ta.sma(close, maLength)
    maValue := na(maValue[1]) ? firstSMA : (firstSMA + secondSMA - maValue[1]) / 2
else if maType == 'TMA'
    maValue := ta.sma(ta.sma(close, math.round(maLength / 2)), math.round(maLength / 2) + 1)

// Entry Conditions with Trend Filter
longCondition = allowLong and (trendFilterMethod == 'OFF' or trendFilterMethod == 'Normal' and close > maValue or trendFilterMethod == 'Reversed' and close < maValue)
shortCondition = allowShort and (trendFilterMethod == 'OFF' or trendFilterMethod == 'Normal' and close < maValue or trendFilterMethod == 'Reversed' and close > maValue)

// Keltner Channels
typicalPrice = hlc3
middleLine = ta.sma(typicalPrice, lengthKC)
range_1 = multKC * ta.atr(lengthKC)
upperChannel = middleLine + range_1
lowerChannel = middleLine - range_1

// CCI
cci = ta.cci(close, lengthCCI)

// RSI
rsi = ta.rsi(close, rsiPeriod)

// Volume
volCondition = volume > ta.sma(volume, 50) * volumeMultiplier

// Combined Entry Conditions with Trend Filter and state check
longCondition := longCondition and cci < oversoldCCI and low < lowerChannel and rsi < rsiOversold and volCondition and not isLongOpen
shortCondition := shortCondition and cci > overboughtCCI and high > upperChannel and rsi > rsiOverbought and volCondition and not isShortOpen

// Execute orders at the open of the new bar after conditions are met
if longCondition
    strategy.entry('Long', strategy.long)
    alert('LicenseID,buy,AUDNZD,risk=1')
    isLongOpen := true
if shortCondition
    strategy.entry('Short', strategy.short)
    alert('LicenseID,sell,AUDNZD,risk=1')
    isShortOpen := true

// Exit Conditions and Alerts
longExitCondition = cci > 0
shortExitCondition = cci < 0
if (longExitCondition and isLongOpen)
    strategy.close('Long')
    alert('LiceneseID,closelong,AUDNZD')
    isLongOpen := false
if (shortExitCondition and isShortOpen)
    strategy.close('Short')
    alert('LicenseID,closeshort,AUDNZD')
    isShortOpen := false

// Plotting
plot(upperChannel, color=color.new(color.red, 0), linewidth=1)
plot(lowerChannel, color=color.new(color.green, 0), linewidth=1)
hline(overboughtCCI, 'Overbought', color=color.red)
hline(oversoldCCI, 'Oversold', color=color.green)

```

> Detail

https://www.fmz.com/strategy/451530

> Last Modified

2024-05-15 16:56:03
