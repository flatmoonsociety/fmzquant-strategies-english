
> Name

Multi-SMA-and-RSI-Crossover-Strategy-with-Dynamic-ATR-based-Take-Profit-and-Stop-Loss
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d95af172f4220b6ddfb3.png)
![IMG](https://www.fmz.com/upload/asset/2d8ac84fc6fd79d3fa072.png)


[trans]
#### Strategy Overview
This strategy is an automated trading system based on multiple moving average (SMA) and relative strength indicator (RSI) crossover signals. It combines the multiple verification mechanism of short-term and medium-term moving averages, and uses the RSI indicator for trend confirmation, while using dynamic ATR stop loss to control risks, establishing a complete trading decision-making framework. This strategy is mainly used to capture market trend turning points and improve the accuracy of transactions through cross-confirmation of multiple technical indicators.
#### Strategy Principle
The core logic of the strategy is based on the comprehensive judgment of five key conditions:
1. Price breaks above the 20-period high moving average
2. Price breaks above the 20-period moving average of lows
3. Price breaks above the 50-period high moving average
4. Price breaks above the 50-period moving average of lows
5. The RSI(7) indicator breaks above the 50 level upwards
Only when these five conditions are met simultaneously will the strategy generate a buy signal. After entry, the strategy uses dynamic stop loss and take profit levels based on ATR, where stop loss is set to 1.5 times ATR and take profit is set to 2.5 times ATR. This design can automatically adjust risk management parameters based on market volatility.
#### Strategic Advantages
1. The multiple verification mechanism significantly improves the reliability of trading signals and reduces the impact of false signals by requiring simultaneous confirmation of multiple technical indicators.
2. The dynamic risk management system can automatically adjust stop loss and take profit levels according to market volatility, making the strategy highly adaptable.
3. It combines the characteristics of trend following and momentum reversal, which can not only capture strong breakthroughs, but also stop losses in time to protect profits.
4. The strategy parameters are highly adjustable, and traders can adjust various parameters according to different market environments and personal risk preferences.
#### Strategy Risk
1. The requirement to meet multiple conditions at the same time may result in missing some potential trading opportunities.
2. In a volatile market, frequent price crossings of the moving average may trigger too many trading signals.
3. Fixed ATR multiples may not be flexible enough under extreme market conditions.
4. The strategy does not consider market fundamentals, and pure technical analysis may fail in the face of major news.
#### Strategy optimization direction
1. Introduce a market volatility filter to adjust trading frequency and position size during periods of high volatility.
2. Add a trading volume confirmation mechanism to improve the reliability of breakthrough signals.
3. Develop an adaptive ATR multiple adjustment mechanism to dynamically adjust stop loss and take profit levels based on historical volatility.
4. Add a trend strength filter to avoid overtrading in weak markets.
#### Summary
This is a well-designed technical trading strategy that improves trading accuracy through cross-confirmation of multiple technical indicators and uses a dynamic risk management system to protect profits. Although the strategy has certain limitations, its performance can be further improved through the suggested optimization directions. This strategy is suitable for traders with strong risk tolerance and willingness to optimize long-term strategies. ||
#### Strategy Overview
This strategy is an automated trading system based on multiple Simple Moving Average (SMA) crossovers combined with Relative Strength Index (RSI) signals. It incorporates a multi-validation mechanism using both short-term and medium-term moving averages, confirms trends through RSI indicators, and implements dynamic ATR-based stop losses for risk control, establishing a comprehensive trading decision framework. The strategy primarily aims to capture market trend reversal points while improving trading accuracy through multiple technical indicator confirmations.

#### Strategy Principles
The core logic is built on five key conditions:
1. Price breaks above the 20-period high SMA
2. Price breaks above the 20-period low SMA
3. Price breaks above the 50-period high SMA
4. Price breaks above the 50-period low SMA
5. RSI(7) crosses above level 50

A buy signal is generated only when all five conditions are simultaneously satisfied. After entry, the strategy employs dynamic stop-loss and take-profit levels based on ATR, with stop-loss set at 1.5x ATR and take-profit at 2.5x ATR, allowing risk management parameters to automatically adjust based on market volatility.

#### Strategy Advantages
1. The multiple validation mechanism significantly improves the reliability of trading signals by requiring confirmation from multiple technical indicators to reduce false signals.
2. The dynamic risk management system automatically adjusts stop-loss and take-profit levels based on market volatility, providing good adaptability.
3. Combines trend-following and momentum reversal characteristics, capable of capturing strong breakouts while protecting profits through timely stops.
4. Highly adjustable parameters allow traders to modify settings according to different market environments and personal risk preferences.

#### Strategy Risks
1. The requirement for multiple conditions to be simultaneously satisfied may result in missing potential trading opportunities.
2. In ranging markets, frequent price crossovers of moving averages may trigger excessive trading signals.
3. Fixed ATR multipliers may not be flexible enough under extreme market conditions.
4. The strategy doesn't consider fundamental factors, making it potentially vulnerable during significant news events.

#### Optimization Directions
1. Introduce a market volatility filter to adjust trading frequency and position sizing during high volatility periods.
2. Add volume confirmation mechanisms to improve breakout signal reliability.
3. Develop adaptive ATR multiplier adjustment mechanisms to dynamically modify stop-loss and take-profit levels based on historical volatility.
4. Implement trend strength filters to avoid overtrading in weak market conditions.

#### Conclusion
This is a well-designed technical trading strategy that improves trading accuracy through multiple technical indicator confirmations and employs a dynamic risk management system to protect profits. While the strategy has certain limitations, its performance can be further enhanced through the suggested optimization directions. It is suitable for traders with higher risk tolerance who are willing to engage in long-term strategy optimization.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-22 00:00:00
end: 2025-02-19 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=5
strategy("Virat Bharat Auto Trade", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// **User-Defined Inputs for Customization**
smaLength20 = input(20, title="SMA High/Low 20 Length")
smaLength50 = input(50, title="SMA High/Low 50 Length")
rsiLength = input(7, title="RSI Length")
rsiLevel = input(50, title="RSI Crossover Level")
atrMultiplierSL = input(1.5, title="ATR Multiplier for Stop Loss")
atrMultiplierTP = input(2.5, title="ATR Multiplier for Target")

// **Defining the Indicators with Custom Inputs**
smaHigh20 = ta.sma(high, smaLength20)
smaLow20 = ta.sma(low, smaLength20)
smaHigh50 = ta.sma(high, smaLength50)
smaLow50 = ta.sma(low, smaLength50)
rsiValue = ta.rsi(close, rsiLength)
atrValue = ta.atr(14)  // ATR for Dynamic Stop Loss & Target

// **Conditions for Buy Signal**
condition1 = ta.crossover(close, smaHigh20)
condition2 = ta.crossover(close, smaLow20)
condition3 = ta.crossover(close, smaHigh50)
condition4 = ta.crossover(close, smaLow50)
condition5 = ta.crossover(rsiValue, rsiLevel)

// **Final Buy Signal (Only when all conditions match)**
buySignal = condition1 and condition2 and condition3 and condition4 and condition5

// **Buy Price, Stop Loss & Target**
buyPrice = close
stopLoss = buyPrice - (atrValue * atrMultiplierSL)  // Dynamic Stop Loss
target = buyPrice + (atrValue * atrMultiplierTP)  // Dynamic Target

// **Plot Buy Signal on Chart**
plotshape(buySignal, location=location.belowbar, color=color.green, style=shape.labelup, title="BUY", size=size.small, text="BUY")

// **Plot Labels for Buy, Stop Loss & Target**
if buySignal
    label.new(x=bar_index, y=buyPrice, text="BUY @ " + str.tostring(buyPrice, format="#.##"), color=color.green, textcolor=color.white, size=size.small, style=label.style_label_down, yloc=yloc.price)
    label.new(x=bar_index, y=stopLoss, text="STOP LOSS @ " + str.tostring(stopLoss, format="#.##"), color=color.red, textcolor=color.white, size=size.small, style=label.style_label_down, yloc=yloc.price)
    label.new(x=bar_index, y=target, text="TARGET @ " + str.tostring(target, format="#.##"), color=color.blue, textcolor=color.white, size=size.small, style=label.style_label_up, yloc=yloc.price)

// **Strategy Trading Logic - Automated Entry & Exit**
if buySignal
    strategy.entry("BUY", strategy.long)
    strategy.exit("SELL", from_entry="BUY", loss=atrValue * atrMultiplierSL, profit=atrValue * atrMultiplierTP)

```

> Detail

https://www.fmz.com/strategy/483104

> Last Modified

2025-02-21 13:44:39
