
> Name

Triple-Bollinger-Band-Standard-Deviation-Trend-Following-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8d5b9821f00f02b8d66.png)
![IMG](https://www.fmz.com/upload/asset/2d8718abd8ace9b720631.png)




[trans]
#### Overview
This strategy is a trend following trading system based on Bollinger Bands standard deviation. The strategy determines the strength of the trend by observing the position of three consecutive candle lines relative to the upper and lower Bollinger Bands, and trades when the trend is established. The system uses a fixed risk-benefit ratio to manage the risk of each transaction.
#### Strategy Principle
The core logic of the strategy is based on the following points:
1. Use the 20-period moving average as the middle track of the Bollinger Bands, and use 2 times the standard deviation to calculate the upper and lower tracks.
2. When the closing prices of three consecutive candle lines are above the upper track, the system believes that the upward trend has been established, and enters the long position when the third candle line closes.
3. When the closing prices of three consecutive candle lines are below the lower track, the system believes that the downward trend has been established, and enters the market to go short when the third candle line closes.
4. The stop loss is set at the extreme value of the earliest candlestick with the entry signal.
5. The target price is set with a risk-return ratio of 1:1, that is, the profit target distance is equal to the stop loss distance.
#### Strategic Advantages
1. The signal confirmation mechanism is robust - it requires three consecutive candle lines to break through the Bollinger Bands, effectively reducing the risk of false breakthroughs.
2. Reasonable risk management - Use a fixed risk-return ratio for transaction management to avoid excessive losses in a single transaction.
3. The trend following effect is significant - the standard deviation characteristics of Bollinger Bands enable the strategy to adapt to changes in market volatility.
4. Clear execution rules - There are clear quantitative standards for setting entry, stop loss and profit targets, and no subjective judgment is required.
#### Strategy Risk
1. Poor performance in sideways markets - Frequent false signals may occur in markets with no clear trend.
2. The timing of entry is slightly delayed - you need to wait for three candle lines to be confirmed before entering, and you may miss some early stages of the market.
3. Limitations of a fixed risk-to-return ratio - A risk-to-return ratio of 1:1 may result in premature closing of profitable positions in a strong trend.
4. Lack of trend strength filtering - only rely on the relationship between price and Bollinger Bands to judge, without considering other trend confirmation indicators.
#### Strategy optimization direction
1. Add trend strength filter - trend indicators such as ADX or MACD can be introduced to improve signal quality.
2. Optimize the risk-return ratio setting - the risk-return ratio can be dynamically adjusted based on market volatility.
3. Improve the take-profit mechanism - Consider adding a trailing stop-loss or batch profit-taking mechanism to better grasp the general trend.
4. Add volume confirmation - Add volume breakthrough confirmation when the signal is generated to improve signal reliability.
#### Summary
This is a well-designed trend following strategy that uses Bollinger Bands and multiple confirmation mechanisms to capture market trends. The risk management framework of the strategy is complete and the implementation standards are clear. Although there is a certain lag, the stability and profitability of the strategy can be further improved through the suggested optimization direction. For traders who prefer trend tracking and focus on risk control, this is a strategic framework worth referring to. ||
#### Overview
This strategy is a trend following trading system based on Bollinger Band standard deviation. It determines trend strength by observing the relationship between three consecutive candles and the Bollinger Bands, executing trades when trends are confirmed. The system employs a fixed risk-reward ratio for managing trade risk.

#### Strategy Principle
The core logic is based on the following points:
1. Uses a 20-period moving average as the middle band, with 2 standard deviations for upper and lower bands.
2. When three consecutive candles close above the upper band, an uptrend is confirmed, entering long at the close of the third candle.
3. When three consecutive candles close below the lower band, a downtrend is confirmed, entering short at the close of the third candle.
4. Stop loss is set at the extreme value of the earliest candle in the entry signal.
5. Target price is set with a 1:1 risk-reward ratio, meaning the profit target distance equals the stop loss distance.

#### Strategy Advantages
1. Robust Signal Confirmation - Requires three consecutive candles breaking the Bollinger Bands, effectively reducing false breakout risks.
2. Rational Risk Management - Uses fixed risk-reward ratio for trade management, preventing excessive losses in single trades.
3. Effective Trend Following - Bollinger Band's standard deviation characteristics allow the strategy to adapt to market volatility changes.
4. Clear Execution Rules - Entry, stop loss, and profit targets all have clear quantitative standards, requiring no subjective judgment.

#### Strategy Risks
1. Poor Performance in Ranging Markets - May generate frequent false signals in markets without clear trends.
2. Delayed Entry Timing - Waiting for three-candle confirmation may miss early stages of price movements.
3. Fixed Risk-Reward Ratio Limitations - 1:1 risk-reward ratio may close profitable positions too early in strong trends.
4. Lack of Trend Strength Filtering - Relies solely on price-band relationships without considering other trend confirmation indicators.

#### Strategy Optimization Directions
1. Add Trend Strength Filter - Incorporate ADX or MACD for improved signal quality.
2. Optimize Risk-Reward Ratio Setting - Dynamically adjust risk-reward ratio based on market volatility.
3. Enhance Profit-Taking Mechanism - Consider adding trailing stops or partial profit-taking mechanisms for better trend capture.
4. Include Volume Confirmation - Add volume breakout confirmation when generating signals to improve reliability.

#### Summary
This is a well-designed trend following strategy that captures market trends through Bollinger Bands and multiple confirmation mechanisms. The strategy features a comprehensive risk management framework with clear execution standards. While there is some inherent lag, the suggested optimization directions can further enhance strategy stability and profitability. For traders who prefer trend following and emphasize risk control, this provides a valuable strategic framework.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-01 00:00:00
end: 2025-02-18 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("Bollinger Band Buy and Sell Strategy (Entry at Close of 3rd Candle)", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10, pyramiding=0)

// Bollinger Band settings
length = input.int(20, "Bollinger Band Length")
mult = input.float(2.0, "Standard Deviation Multiplier")
basis = ta.sma(close, length)
dev = mult * ta.stdev(close, length)
upper_band = basis + dev
lower_band = basis - dev

// Plot Bollinger Bands
plot(upper_band, "Upper Band", color.blue)
plot(lower_band, "Lower Band", color.red)

// Initialize variables
var float buyEntryPrice = na
var float buyStopLoss = na
var float buyTargetPrice = na

var float sellEntryPrice = na
var float sellStopLoss = na
var float sellTargetPrice = na

// Buy Condition: Last 3 candles closed above upper band
buyCondition = close[2] > upper_band[2] and 
               close[1] > upper_band[1] and 
               close > upper_band

// Sell Condition: Last 3 candles closed below lower band
sellCondition = close[2] < lower_band[2] and   close[1] < lower_band[1] and   close < lower_band

// Buy Logic
if buyCondition and strategy.position_size == 0
    buyEntryPrice := close  // Entry at the close of the 3rd candle
    buyStopLoss := low[2]   // Low of the earliest candle in the 3-candle sequence
    buyTargetPrice := buyEntryPrice + (buyEntryPrice - buyStopLoss)
    
    strategy.entry("Buy", strategy.long)
    strategy.exit("Buy Exit", "Buy", stop=buyStopLoss, limit=buyTargetPrice)
    
    // Plot buy signal arrow on the entry candle
    label.new(bar_index, low, "▲", color=color.green, style=label.style_label_up, yloc=yloc.belowbar)

// Sell Logic
if sellCondition and strategy.position_size == 0
    sellEntryPrice := close  // Entry at the close of the 3rd candle
    sellStopLoss := high[2]  // High of the earliest candle in the 3-candle sequence
    sellTargetPrice := sellEntryPrice - (sellStopLoss - sellEntryPrice)
    
    strategy.entry("Sell", strategy.short)
    strategy.exit("Sell Exit", "Sell", stop=sellStopLoss, limit=sellTargetPrice)
    
    // Plot sell signal arrow on the entry candle
    label.new(bar_index, high, "▼", color=color.red, style=label.style_label_down, yloc=yloc.abovebar)

// Plot stop loss and target levels for buy trades
plot(strategy.position_size > 0 ? buyStopLoss : na, "Buy Stop Loss", color.red, 2, plot.style_linebr)
plot(strategy.position_size > 0 ? buyTargetPrice : na, "Buy Target", color.green, 2, plot.style_linebr)

// Plot stop loss and target levels for sell trades
plot(strategy.position_size < 0 ? sellStopLoss : na, "Sell Stop Loss", color.red, 2, plot.style_linebr)
plot(strategy.position_size < 0 ? sellTargetPrice : na, "Sell Target", color.green, 2, plot.style_linebr)
```

> Detail

https://www.fmz.com/strategy/482878

> Last Modified

2025-02-20 16:16:14
