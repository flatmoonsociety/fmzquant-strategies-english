
> Name

Bollinger Bands High-Frequency Quantitative-Strategy-Combined-with-High-Low-Breakout-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/182c575fd28d467c195.png)

[trans]
#### Overview
This strategy is a high-frequency trading system that combines the Bollinger Bands indicator with price breakouts. The strategy monitors the relationship between price and Bollinger Bands and combines the previous high and low point breakthrough signals to conduct reversal transactions when the market appears overbought and oversold. The system uses a risk-benefit ratio of 1:1 to set take-profit and stop-loss, and displays each key price in a visual way to help traders intuitively understand market trends.
#### Strategy Principle
The core logic of the strategy is based on two main judgment conditions: when the price breaks through the previous high and the previous high is below the lower Bollinger Band, a long signal is triggered; when the price falls below the previous low and the previous low is above the Bollinger Band, a short signal is triggered. Bollinger Bands parameters use a 20-period moving average and 2 times the standard deviation to determine the market's fluctuation range and overbought and oversold areas. After the system triggers the trading signal, it will automatically set the corresponding stop loss level and target level, and display them visually through different styles of lines.
#### Strategic Advantages
1. It combines two trading ideas, trend breakthrough and mean reversion, to maintain stability in different market environments.
2. Using a fixed risk-return ratio for position management is conducive to long-term stable profits.
3. Improve the operability of the strategy by visually displaying entry, stop loss and target levels.
4. The use of Bollinger Bands indicators helps identify overbought and oversold conditions in the market and improves the accuracy of transactions.
5. The strategy logic is simple and clear, easy to understand and implement
#### Strategy Risk
1. High-frequency trading may face higher transaction costs, and the impact of handling fees needs to be considered.
2. Frequent false breakthrough signals may occur in sideways and volatile markets.
3. A fixed risk-benefit ratio may not be able to fully grasp the general trend.
4. Fixed Bollinger Band parameters may not be suitable for all market environments
5. The market needs to be monitored in real time to ensure timely execution of signals
#### Strategy optimization direction
1. Introduce trading volume indicators as signal confirmation to improve the reliability of breakthroughs
2. Dynamically adjust Bollinger Band parameters based on market volatility
3. Add trend filter to avoid frequent trading in sideways market
4. Consider adding time filtering to avoid trading during inactive periods
5. Develop an adaptive risk-benefit ratio setting mechanism
#### Summary
This is a complete trading system that integrates multiple technical analysis concepts. By combining the Bollinger Bands indicator with price breakouts, the strategy can capture reversal opportunities in overbought and oversold areas of the market. Although there is some room for optimization, the basic framework of the system has good scalability and practical value. Through reasonable risk management and parameter optimization, this strategy is expected to achieve stable returns in actual transactions. ||
#### Overview
This strategy is a high-frequency trading system that combines Bollinger Bands indicators with price breakout signals. The strategy monitors the relationship between price and Bollinger Bands, combined with previous high and low point breakout signals, to execute reversal trades during market overbought and oversold conditions. The system implements a 1:1 risk-reward ratio for profit and loss targets, and visualizes key price levels to help traders intuitively understand market trends.

#### Strategy Principles
The core logic of the strategy is based on two main conditions: a buy signal is triggered when the price breaks above the previous high and that high is below the lower Bollinger Band; a sell signal is triggered when the price breaks below the previous low and that low is above the upper Bollinger Band. The Bollinger Bands parameters use a 20-period moving average with 2 standard deviations to determine market volatility range and overbought/oversold areas. After triggering trading signals, the system automatically sets corresponding stop-loss and target levels, visualizing them through different line styles.

#### Strategy Advantages
1. Combines both trend breakout and mean reversion trading approaches, maintaining stability across different market conditions
2. Uses fixed risk-reward ratio for position management, beneficial for long-term profitable trading
3. Visualizes entry, stop-loss, and target levels, improving strategy operability
4. Utilizes Bollinger Bands to identify market overbought/oversold conditions, enhancing trading accuracy
5. Simple and clear strategy logic, easy to understand and execute

#### Strategy Risks
1. High-frequency trading may face higher transaction costs, requiring consideration of commission impacts
2. May generate frequent false breakout signals in ranging markets
3. Fixed risk-reward ratio might not fully capture strong trend movements
4. Fixed Bollinger Bands parameters may not adapt to all market conditions
5. Requires real-time market monitoring to ensure timely signal execution

#### Strategy Optimization Directions
1. Incorporate volume indicators for signal confirmation, improving breakout reliability
2. Dynamically adjust Bollinger Bands parameters based on market volatility
3. Add trend filters to avoid frequent trading in ranging markets
4. Consider adding time filters to avoid trading during inactive periods
5. Develop adaptive risk-reward ratio setting mechanisms

#### Summary
This is a comprehensive trading system integrating multiple technical analysis concepts. Through the combination of Bollinger Bands indicators and price breakouts, the strategy can capture reversal opportunities in market overbought and oversold areas. While there is room for optimization, the system's basic framework has good extensibility and practical value. Through proper risk management and parameter optimization, this strategy has the potential to achieve stable returns in actual trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-03 00:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Band Scalping", overlay=true)

// Input for Bollinger Bands length and standard deviation
bbLength = input(20, title="Bollinger Bands Length")
stdDev = input(2.0, title="Bollinger Bands Std Dev")

// Calculate and plot the Bollinger Bands
basis = ta.sma(close, bbLength)
deviation = stdDev * ta.stdev(close, bbLength)
upperBB = basis + deviation
lowerBB = basis - deviation

// Get previous candle's values
prevHigh = high[1]   // Previous candle high
prevLow = low[1]     // Previous candle low

// Buy Signal Condition: Current high crossed above previous high and previous high is below the lower Bollinger Band
buyCondition = ta.crossover(high, prevHigh) and (prevHigh < lowerBB[1])

// Sell Signal Condition: Current low crossed below previous low and previous low is above the upper Bollinger Band
sellCondition = ta.crossunder(low, prevLow) and (prevLow > upperBB[1])

// Entry and exit for Buy signals
if (buyCondition)
    strategy.entry("Buy", strategy.long)
    // Calculate target and stop loss
    stopLossPrice = prevLow
    targetPrice = prevHigh + (prevHigh - stopLossPrice)  // 1:1 RR target

    // Set stop loss and target orders
    strategy.exit("Sell", "Buy", limit=targetPrice, stop=stopLossPrice)

    // // Plot entry line
    // line.new(x1=bar_index, y1=prevHigh, x2=bar_index + 12, y2=prevHigh, color=color.green, width=2, style=line.style_solid)
    // // Plot stop loss line
    // line.new(x1=bar_index, y1=stopLossPrice, x2=bar_index + 12, y2=stopLossPrice, color=color.red, width=1, style=line.style_dashed)
    // // Plot target line
    // line.new(x1=bar_index, y1=targetPrice, x2=bar_index + 12, y2=targetPrice, color=color.blue, width=2, style=line.style_solid)

// Entry and exit for Sell signals
if (sellCondition)
    strategy.entry("Sell", strategy.short)
    // Calculate target and stop loss
    stopLossPriceSell = prevHigh
    targetPriceSell = prevLow - (stopLossPriceSell - prevLow)  // 1:1 RR target

    // Set stop loss and target orders
    strategy.exit("Cover", "Sell", limit=targetPriceSell, stop=stopLossPriceSell)

    // // Plot entry line
    // line.new(x1=bar_index, y1=prevLow, x2=bar_index + 12, y2=prevLow, color=color.red, width=2, style=line.style_solid)
    // // Plot stop loss line
    // line.new(x1=bar_index, y1=stopLossPriceSell, x2=bar_index + 12, y2=stopLossPriceSell, color=color.green, width=1, style=line.style_dashed)
    // // Plot target line
    // line.new(x1=bar_index, y1=targetPriceSell, x2=bar_index + 12, y2=targetPriceSell, color=color.blue, width=2, style=line.style_solid)

// Plotting Bollinger Bands with 70% transparency
plot(upperBB, color=color.red, title="Upper Bollinger Band", transp=70)
plot(lowerBB, color=color.green, title="Lower Bollinger Band", transp=70)
plot(basis, color=color.blue, title="Middle Band", transp=70)

```

> Detail

https://www.fmz.com/strategy/473936

> Last Modified

2024-12-04 15:15:50
