
> Name

Dual-Moving-Average-Crossover-Trend-Following-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d7f8217bee21b959c121.png)
![IMG](https://www.fmz.com/upload/asset/2d89150618c146f9a938b.png)



[trans]

#### Overview
This strategy is a trend following system based on a double moving average crossover, which uses the crossover of two simple moving averages (SMA) in the short and long term to generate clear long and short trading signals. This strategy is designed to be simple and clear, easy to understand and implement, and is especially suitable for traders who want to master the basic principles of moving average crossovers. The core idea of ​​the strategy is that when the short-term moving average crosses the long-term moving average from bottom to top, the system generates a long signal; when the short-term moving average crosses the long-term moving average from top to bottom, the system generates a short signal. This trading method automatically reverses positions at the closing price when the signal occurs, ensuring that traders can adjust the market direction in a timely manner.
#### Strategy Principle
The core of the strategy is based on the interaction of two simple moving averages (SMA):
1. Short-term moving average: The default setting is 9 periods, reflecting the more recent price trends
2. Long-term moving average: The default setting is 21 periods, reflecting longer-term price trends
Trading signal generation logic:
- Long condition: When the short-term moving average crosses the long-term moving average upward (ta.crossover function), the system generates a long signal
- Short selling conditions: When the short-term moving average crosses the long-term moving average downward (ta.crossunder function), the system generates a short selling signal
Transaction execution process:
- When a long signal is triggered, the system first immediately closes any existing short positions and then opens a new long position
- When the short signal is triggered, the system first immediately closes any existing long positions and then opens new short positions.
- The system clearly marks the entry price through labels on the chart. The long label is displayed above the K line and the short label is displayed below the K line.
The strategy also allows users to customize the price source (the default is the opening price) and the moving average period length to adapt to different market environments or trading styles.
#### Strategic Advantages
By in-depth analysis of the strategy code, we can summarize the following obvious advantages:
1. Simple and clear: The strategy logic is clear and there are no complicated indicator combinations or conditional judgments, making it easy for traders to understand and apply
2. Visually intuitive: The system draws two moving averages on the chart and distinguishes them by color (short-term moving average is red, long-term moving average is blue), and at the same time, the entry point and price are visually displayed in the form of labels.
3. Automatic reversal mechanism: When a new signal appears, the strategy will automatically close the reverse position and establish a new position to ensure that traders always follow the current trend direction.
4. Highly customizable: users can adjust the price source and moving average period according to their own preferences to adapt to different market environments or trading time frames.
5. Real-time calculation: The strategy sets the calc_on_every_tick=true parameter to ensure calculations are performed every time the price changes and provide the most timely signals.
6. No parameter overfitting: The strategy only uses two moving average parameters, which reduces the risk of overfitting and enhances the robustness of the strategy under different market conditions.
7. Clear label prompts: By placing labels in advance at the next K-line position, traders can clearly see the entry price, which facilitates risk management.
#### Strategy Risk
Although this strategy is designed to be simple and effective, it still has the following potential risks:
1. Frequent trading in volatile markets: In sideways or volatile markets, short-term and long-term moving averages may cross frequently, resulting in excessive trading signals and unnecessary transaction costs.
   - Solution: You can add additional filter conditions, such as the ADX indicator to confirm trend strength, or set a minimum holding time   
2. Lagging problem: The moving average is essentially a lagging indicator, and the signal may not be generated until the trend has developed or is about to end.
   - Solution: Combine with other leading indicators such as RSI or MACD, or use shorter moving average periods to reduce lag
3. Risk of false breakthrough: The price may briefly cross the moving average and then return to the original trend, resulting in a false signal
   - Solution: Add a confirmation mechanism, such as requiring the price to maintain a certain time or range after crossing before triggering the transaction.
4. Lack of stop-loss mechanism: The current strategy does not have a clear stop-loss setting, which may result in larger losses in a strong reversal market.
   - Solution: Implement a fixed stop loss or a volatility-based dynamic stop loss strategy
5. Parameter sensitivity: Strategy performance is more sensitive to the choice of moving average cycle length. Improper parameters may lead to significant changes in strategy effects.
   - Solution: Perform backtest optimization to find parameter combinations that perform stably under a variety of market conditions
#### Strategy optimization direction
Based on an in-depth analysis of the code, I propose the following optimization directions:
1. Add trend filter: Introduce ADX, trend strength indicator or relative position judgment between price and moving average to only generate signals in a confirmed trend environment to avoid frequent transactions that shock the market
   - Explanation: This will reduce false signals, improve trading success rate and capital efficiency
2. Implement a dynamic stop-loss mechanism: Set dynamic stop-loss levels based on ATR or other volatility indicators to protect profits and limit the maximum risk of a single trade
   - Explanation: Effective risk management is key to long-term trading success
3. Optimize entry timing: Consider using a small period confirmation after the signal is generated or waiting for a callback before entering to obtain a better execution price
   - Explanation: Optimizing entry prices can significantly improve long-term returns
4. Add volume filtering: Add volume confirmation based on cross signals, and execute trades only when volume also supports directional changes.
   - Explanation: Trading volume is an important confirmation factor of the effectiveness of price changes
5. Implement adaptive moving average period: automatically adjust the moving average period length according to market volatility, using a longer period in a high-volatility environment and a shorter period in a low-volatility environment.
   - Explanation: This allows the strategy to better adapt to different market states and cycles
6. Add a batch opening and closing mechanism: Instead of establishing all positions at once, positions are opened and closed in steps to reduce the risk of time point selection.
   - Explanation: This method can smooth the trading results and reduce the luck factor caused by the selection of a single entry point
#### Summary
The Double Moving Average Cross Trend Following Strategy is a simple yet powerful quantitative trading system that generates clear trading signals through the intersection of short-term and long-term moving averages. Its main advantages are simple operation, visual intuitiveness and automatic reversal mechanism, allowing traders to objectively follow market trends. However, this strategy also has inherent risks such as frequent trading in volatile markets and signal lags.
This basic strategy can be significantly enhanced by adding trend filters, implementing dynamic stops, optimizing entry timing, and increasing volume confirmations. In particular, combining other technical indicators to filter signals and optimize risk management will help improve the performance of strategies in various market environments.
It's an ideal starting point for newbies looking to start quantitative trading; for experienced traders, it provides a solid foundation that can be further customized and optimized. It is important that whatever improvements are adopted should be evaluated through rigorous backtesting and forward validation to ensure that the strategy improvements truly add long-term value. ||
#### Overview
This strategy is a trend following system based on the crossover of dual moving averages, utilizing the intersection of short-term and long-term simple moving averages (SMA) to generate clear long and short trading signals. The design is concise and easy to understand and implement, particularly suitable for traders seeking to master the basic principles of moving average crossovers. The core idea is that when the short-term moving average crosses above the long-term moving average, the system generates a long signal; when the short-term moving average crosses below the long-term moving average, the system generates a short signal. This trading method automatically reverses positions at the closing price when signals appear, ensuring traders can adjust market direction in a timely manner.

#### Strategy Principles
The core of the strategy is based on the interaction of two simple moving averages (SMA):
1. Short-term moving average: Default setting is 9 periods, reflecting more recent price movements
2. Long-term moving average: Default setting is 21 periods, reflecting longer-term price trends

Trade signal generation logic:
- Long condition: When the short-term MA crosses above the long-term MA (ta.crossover function), the system generates a long signal
- Short condition: When the short-term MA crosses below the long-term MA (ta.crossunder function), the system generates a short signal

Trading execution process:
- When a long signal is triggered, the system first immediately closes any existing short positions, then opens a new long position
- When a short signal is triggered, the system first immediately closes any existing long positions, then opens a new short position
- The system clearly labels entry prices on the chart, with long labels displayed above the candlesticks and short labels below

The strategy also allows users to customize the price source (default is opening price) and moving average period lengths to adapt to different market environments or trading styles.

#### Strategy Advantages
Through in-depth analysis of the strategy code, we can summarize the following distinct advantages:

1. Simplicity and clarity: The strategy logic is clear, without complex indicator combinations or conditional judgments, making it easy for traders to understand and apply
2. Visual intuitiveness: The system draws two moving averages on the chart, distinguished by color (short-term MA in red, long-term MA in blue), while visually displaying entry points and prices in label form
3. Automatic reversal mechanism: When a new signal appears, the strategy automatically closes opposite positions and establishes new positions, ensuring traders always follow the current trend direction
4. Strong customizability: Users can adjust the price source and moving average periods according to their preferences to adapt to different market environments or trading timeframes
5. Real-time calculation: The strategy is set with calc_on_every_tick=true parameter, ensuring calculations are performed at each price movement, providing the most timely signals
6. No parameter overfitting: The strategy uses only two moving average parameters, reducing the risk of overfitting and enhancing strategy robustness under different market conditions
7. Clear label prompts: By pre-placing labels at the next candlestick position, traders can clearly see entry prices, facilitating risk management

#### Strategy Risks
Despite the strategy's concise and effective design, there are still the following potential risks:

1. Frequent trading in oscillating markets: In sideways consolidation or oscillating markets, short-term and long-term moving averages may frequently cross, leading to excessive trading signals and unnecessary trading costs
   - Solution: Add additional filtering conditions, such as ADX indicator to confirm trend strength, or set a minimum holding time
   
2. Lag issues: Moving averages are inherently lagging indicators, signals may be generated only after trends have developed or are about to end
   - Solution: Combine with other leading indicators, such as RSI or MACD, or use shorter moving average periods to reduce lag

3. False breakout risk: Prices may briefly cross the moving average and then return to the original trend, causing false signals
   - Solution: Add confirmation mechanisms, such as requiring prices to maintain a certain time or amplitude after crossing before triggering a trade

4. Lack of stop-loss mechanism: The current strategy has no explicit stop-loss settings, which may lead to significant losses in strong reversal markets
   - Solution: Implement fixed stop-loss or volatility-based dynamic stop-loss strategies

5. Parameter sensitivity: Strategy performance is relatively sensitive to the choice of moving average period lengths, inappropriate parameters may cause significant changes in strategy effectiveness
   - Solution: Conduct backtest optimization to find parameter combinations that perform stably under various market conditions

#### Strategy Optimization Directions
Based on an in-depth analysis of the code, I propose the following optimization directions:

1. Add trend filters: Introduce ADX, trend strength indicators, or relative position judgments of price and moving averages, generating signals only in confirmed trend environments to avoid frequent trading in oscillating markets
   - Explanation: This will reduce false signals, improving trade success rates and capital efficiency

2. Implement dynamic stop-loss mechanisms: Set dynamic stop-loss levels based on ATR or other volatility indicators to protect profits and limit maximum risk per trade
   - Explanation: Effective risk management is key to long-term trading success

3. Optimize entry timing: Consider using smaller timeframes for confirmation after signal generation or waiting for pullbacks before entering, to obtain better execution prices
   - Explanation: Optimizing entry prices can significantly improve long-term returns

4. Add volume filtering: Add volume confirmation on top of crossover signals, executing trades only when volume also supports directional changes
   - Explanation: Volume is an important confirming factor for the validity of price movements

5. Implement adaptive moving average periods: Automatically adjust moving average period lengths based on market volatility, using longer periods in high-volatility environments and shorter periods in low-volatility environments
   - Explanation: This can make the strategy better adapt to different market states and cycles

6. Add phased position building and closing mechanisms: Instead of establishing full positions at once, build and close positions in steps to reduce timing risk
   - Explanation: This approach can smooth trading results and reduce luck factors brought by single entry point selection

#### Summary
The Dual Moving Average Crossover Trend Following Strategy is a concise yet powerful quantitative trading system that generates clear trading signals through the crossover of short-term and long-term moving averages. Its main advantages lie in simple operation, visual intuitiveness, and automatic reversal mechanisms, allowing traders to objectively follow market trends. However, the strategy also has inherent risks such as frequent trading in oscillating markets and signal lag.

This basic strategy can be significantly enhanced by adding trend filters, implementing dynamic stop-loss mechanisms, optimizing entry timing, and adding volume confirmation. Particularly, combining other technical indicators to filter signals and optimize risk management will help improve strategy performance across various market environments.

For beginners hoping to start quantitative trading, this is an ideal starting point; for experienced traders, it provides a solid foundation that can be further customized and optimized. Importantly, whatever improvements are adopted should be evaluated through rigorous backtesting and forward validation to ensure strategy improvements truly add long-term value.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-01 00:00:00
end: 2025-03-24 00:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//
//@version=6
//
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// @author = Da_mENIZ
// © denis_zvegelj
// last change	20.Mar.2025
//
// Simple MA Crossover strategy that shows on the chart with Long/Short indicators. Feel free to use it to suit 
// your needs
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////
strategy("DZ Simple MA Crossover Strategy", shorttitle="DZ_MACross", overlay=true, calc_on_every_tick=true)

// Define the moving average lengths
i_src_price = input.source  (open, "Price source",                                                                                                                     group="Main Settings")
i_shMA_len  = input.int		(9, 	"Short MA Length", 		minval=1,																									group="Main Settings")
i_loMA_len  = input.int		(21,	"Long MA Length", 		minval=6,																									group="Main Settings")

// Calculate the moving averages
short_MA = ta.sma(i_src_price, i_shMA_len)
long_MA = ta.sma(i_src_price, i_loMA_len)

// Plot the moving averages on the chart
plot(short_MA, color=color.red, linewidth=2, title="Short MA")
plot(long_MA, color=color.blue, linewidth=2, title="Long MA")

// Generate the buy and sell signals
long_Cond = ta.crossover(short_MA, long_MA)
short_Cond = ta.crossunder(short_MA, long_MA)

// Place the orders based on conditions
if (long_Cond)
    strategy.close("Short", immediately = true, comment = "Close")
    strategy.entry("Long", strategy.long, comment = "Enter")
    label.new(bar_index+1, open, "Long\n" + str.tostring(open), style=label.style_label_down, color=color.blue, textcolor=color.white, yloc=yloc.abovebar)



if (short_Cond)
    strategy.close("Long", immediately = true, comment = "Close")
//    strategy.entry("Short", strategy.short, comment = "Short\n" + str.tostring(open))
    strategy.entry("Short", strategy.short, comment = "Enter")
    label.new(bar_index+1, open, "Short\n" + str.tostring(open), style=label.style_label_up, color=color.red, textcolor=color.white, yloc=yloc.belowbar)


```

> Detail

https://www.fmz.com/strategy/488153

> Last Modified

2025-03-25 14:58:39
