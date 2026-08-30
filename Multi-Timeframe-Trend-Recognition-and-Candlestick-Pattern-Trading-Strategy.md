
> Name

Multi-Timeframe-Trend-Recognition-and-Candlestick-Pattern-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/72ffd072930a83d9ce25253a3da608060b399cb4812fc3b0c87b83bf002eb56b.png)
![IMG](assets/images/ef7c98599db68ed9368c41876b6fac8ecd53ed6f7aa12794a666c6a44fa1d62d.png)

[trans]
#### Overview
The multi-time frame trend identification and candlestick pattern trading strategy is a quantitative trading method that combines long- and short-term market analysis. This strategy cleverly incorporates multi-time frame analysis techniques to time entries by confirming the overall market trend on the 15-minute time frame and identifying specific candlestick patterns (such as the bullish engulfing pattern) on the 1-minute time frame. In addition, this strategy also integrates a strict time filtering mechanism to avoid trading during high-volatility periods at the beginning of the market opening and early closing, and ensure that positions are not held overnight, thereby effectively managing trading risks.
#### Strategy Principle
The core logic of this quantitative trading strategy is based on multi-time frame analysis and strict trading time management. Specifically:
1. **Trend identification**: Obtain the price data of the 15-minute time frame through the `request.security` function to determine the medium and long-term trend direction. The strategy confirms the existence of an uptrend by comparing the current closing price to the previous period's closing price (`trend_15m > trend_15m[1]`).
2. **Pattern Recognition**: On the 1-minute time frame, the strategy identifies a bullish engulfing pattern, that is, the closing price of the current K line is higher than the opening price (positive line), and the opening price of the previous K line is higher than the closing price (yin line), and the closing price of the current K line is higher than the opening price of the previous K line. This condition is achieved through `bullish_engulfing = close > open and open[1] > close[1] and close > open[1]`.
3. **Time filter**: The policy sets two important time filter conditions:
   - Avoid the high volatility period in the first 45 minutes (9:00-9:45) after the market opens
   - Avoid the uncertainty period 60 minutes before the close (15:00-16:00)   
4. **Risk Management**: After confirming the entry signal, the strategy automatically sets the stop loss at the lowest point of the previous K line (`stop_loss := low[1]`), and calculates the profit target (`take_profit := close + 2 * (close - stop_loss)`) based on a risk-reward ratio of 2:1.
5. **Intraday trading restrictions**: The strategy forces all positions to be closed at the end of each trading day (16:00) to ensure that no positions are held overnight. This is implemented through the `strategy.close_all()` function.
#### Strategic Advantages
1. **Multi-level market analysis**: By combining the analysis of 15-minute and 1-minute time frames, the strategy can simultaneously grasp the mid-term trend and short-term entry opportunities, significantly improving the accuracy of trading. Medium-term trends provide guidance on overall market direction, while short-term patterns provide precise entry timing.
2. **Effective time filtering mechanism**: Avoiding periods of high volatility and low liquidity before the market opens and closes. These periods usually have more noise and poor signal quality, which may lead to false breakthroughs or expanded slippage.
3. **Automated risk management**: The strategy has built-in clear stop loss and profit target settings, and adopts a risk-reward ratio of 2:1. This is a risk control standard commonly used by professional traders and helps to make long-term profits.
4. **Intraday trading strategy**: By forcing positions to be closed before the market closes, the strategy avoids the risks of holding positions overnight, including uncontrollable losses that may be caused by emergencies, overnight gaps, etc.
5. **Code is concise and efficient**: The strategy code has a clear structure and tight logic. It uses built-in functions of the PineScript language such as `request.security` and `strategy.exit` to improve execution efficiency.
#### Strategy Risk
1. **Multiple time frame lag**: Using the `request.security` function to obtain larger time frame data may introduce a certain degree of lag, which may lead to missed entry points or delayed exits in rapidly changing markets. The solution is to consider using dynamic time frames or adding instant trend confirmation indicators.
2. **Single Pattern Dependence**: The strategy only uses bullish engulfing patterns as entry signals, which may result in missing other effective trading opportunities. Expanding the identification of other high-probability patterns (such as cross stars, hammers, etc.) can increase trading frequency.
3. **Fixed risk-reward setting**: Using a fixed 2:1 risk-reward ratio may not be flexible enough in different volatility environments. The solution is to consider dynamically adjusting stop loss and take profit levels based on ATR (Average True Range).
4. **Time filtering restrictions**: Although time filtering can avoid high-risk periods, it may also miss some high-quality trading opportunities, especially on strong trend days caused by opening gaps. Consider adding additional confirmation conditions rather than avoiding these periods entirely.
5. **Lack of adaptability to market conditions**: The strategy does not differentiate between different market conditions (such as oscillating markets and trending markets) and may perform poorly in certain market environments. Introducing a market status recognition mechanism can improve the adaptability of the strategy.
#### Strategy optimization direction
1. **Trend confirmation indicator enhancement**: Technical indicators such as MACD, RSI or moving average system can be added on the 15-minute frame to provide more reliable trend confirmation. For example, adding a MACD indicator crossover or RSI directional confirmation can reduce false signals.
2. **Dynamic Risk Management**: Dynamically adjust stop loss and profit targets based on market volatility (such as ATR) instead of using a fixed risk-reward ratio. Set looser stops in high-volatility markets and tighter stops in low-volatility markets.
3. **Add more entry patterns**: In addition to bullish engulfing patterns, you can add the recognition of other high-probability candlestick patterns, such as bullish star patterns, hammer lines, etc., to increase trading frequency and diversity.
4. **Introduction of trading volume confirmation**: Incorporating trading volume analysis into the strategy logic, and only confirming the engulfing pattern when the trading volume is amplified, can improve signal quality.
5. **Market Environment Adaptation**: Add market environment identification functions, such as distinguishing trending markets and oscillating markets through volatility indicators (such as ATR) or trend strength indicators (such as ADX), and adjust strategy parameters accordingly.
6. **Optimize time filter**: You can consider using a more refined time filtering mechanism, such as determining the best trading period based on historical data analysis, rather than simply excluding fixed time periods.
#### Summarize
The multi-time frame trend identification and candlestick pattern trading strategy is a comprehensive trading system that combines medium and long-term trend analysis with short-term entry techniques. This strategy improves entry accuracy by confirming the overall market trend direction on the larger time frame (15 minutes) and executing trades by identifying high-probability bullish engulfing patterns on the smaller time frame (1 minute).
Another major feature of this strategy is that it integrates a strict time filtering mechanism and risk management system to avoid periods of high market volatility, and controls risks through a fixed risk-return ratio and forced liquidation before closing. These features make this strategy particularly suitable for day traders looking for solid gains.
Although the strategy has clear logic and strict risk control, there is still room for optimization, including enhancing the trend confirmation mechanism, introducing dynamic risk management, adding more entry pattern recognition, integrating trading volume analysis, and developing market environment adaptive functions. Through these optimizations, the strategy is expected to achieve more stable performance in different market environments.
|| 

#### Overview

The Multi-Timeframe Trend Recognition and Candlestick Pattern Trading Strategy is a quantitative trading approach that combines long and short-term market analysis. This strategy cleverly integrates multi-timeframe analysis techniques by confirming the overall market trend on a 15-minute timeframe while identifying specific candlestick patterns (such as bullish engulfing patterns) on a 1-minute timeframe to determine entry points. Additionally, the strategy incorporates strict time filtering mechanisms to avoid trading during highly volatile periods immediately after market open and before market close, while ensuring no positions are held overnight, effectively managing trading risk.

#### Strategy Principles

The core logic of this quantitative trading strategy is built on multi-timeframe analysis and strict trading time management. Specifically:

1. **Trend Identification**: The strategy obtains 15-minute timeframe price data through the `request.security` function to determine the medium to long-term trend direction. It confirms the existence of an uptrend by comparing the current closing price with the previous closing price (`trend_15m > trend_15m[1]`).

2. **Pattern Recognition**: On the 1-minute timeframe, the strategy identifies bullish engulfing patterns, where the current candle's closing price is higher than its opening price (bullish candle), the previous candle's opening price is higher than its closing price (bearish candle), and the current candle's closing price is higher than the previous candle's opening price. This condition is implemented through `bullish_engulfing = close > open and open[1] > close[1] and close > open[1]`.

3. **Time Filtering**: The strategy establishes two important time filters:
   - Avoiding the first 45 minutes after market open (9:00-9:45) which is typically highly volatile
   - Avoiding the last 60 minutes before market close (15:00-16:00) which often has high uncertainty

4. **Risk Management**: After confirming an entry signal, the strategy automatically sets a stop loss at the lowest point of the previous candle (`stop_loss := low[1]`) and calculates a profit target based on a 2:1 risk-reward ratio (`take_profit := close + 2 * (close - stop_loss)`).

5. **Intraday Trading Restriction**: The strategy forces the closure of all positions at the end of each trading day (16:00), ensuring no overnight positions, implemented through the `strategy.close_all()` function.

#### Strategy Advantages

1. **Multi-level Market Analysis**: By combining 15-minute and 1-minute timeframe analyses, the strategy can simultaneously capture medium-term trends and short-term entry opportunities, significantly improving trading accuracy. The medium-term trend provides guidance on overall market direction, while short-term patterns provide precise entry timing.

2. **Effective Time Filtering Mechanism**: The strategy avoids high volatility and low liquidity periods around market open and close, which typically have more noise and lower quality signals that could lead to false breakouts or increased slippage.

3. **Automated Risk Management**: The strategy incorporates clear stop-loss and profit target settings, adopting a 2:1 risk-reward ratio, which is a risk control standard commonly used by professional traders and contributes to long-term profitability.

4. **Intraday Trading Approach**: By forcing position closure before market close, the strategy avoids overnight holding risks, including unexpected events and overnight gaps that could lead to uncontrollable losses.

5. **Clean and Efficient Code**: The strategy code has a clear structure and tight logic, utilizing PineScript language's built-in functions such as `request.security` and `strategy.exit`, which enhances execution efficiency.

#### Strategy Risks

1. **Multi-Timeframe Lag**: Using the `request.security` function to obtain data from larger timeframes may introduce some lag, potentially causing missed entry points or delayed exits in rapidly changing markets. A solution is to consider using dynamic timeframes or adding real-time trend confirmation indicators.

2. **Single Pattern Dependency**: The strategy relies solely on bullish engulfing patterns as entry signals, which may cause it to miss other effective trading opportunities. Expanding to recognize other high-probability patterns (such as doji stars, hammer lines, etc.) could increase trading frequency.

3. **Fixed Risk-Reward Settings**: Using a fixed 2:1 risk-reward ratio may not be flexible enough in different volatility environments. A solution is to consider dynamically adjusting stop-loss and profit levels based on ATR (Average True Range).

4. **Time Filter Limitations**: While time filtering can avoid high-risk periods, it may also miss some high-quality trading opportunities, especially on strong trend days following opening gaps. Consider adding additional confirmation conditions rather than completely avoiding these periods.

5. **Lack of Market State Adaptability**: The strategy doesn't differentiate between different market states (such as ranging or trending markets) and may perform poorly in certain market environments. Introducing market state recognition mechanisms could improve strategy adaptability.

#### Strategy Optimization Directions

1. **Enhanced Trend Confirmation Indicators**: Technical indicators such as MACD, RSI, or moving average systems could be added to the 15-minute timeframe to provide more reliable trend confirmation. For example, adding MACD crossovers or RSI directional confirmation could reduce false signals.

2. **Dynamic Risk Management**: Dynamically adjust stop-loss and profit targets based on market volatility (such as ATR) rather than using a fixed risk-reward ratio. Set wider stops in high-volatility markets and tighter stops in low-volatility markets.

3. **Add More Entry Patterns**: In addition to bullish engulfing patterns, recognize other high-probability candlestick formations, such as bullish star patterns or hammer lines, to increase trading frequency and diversity.

4. **Incorporate Volume Confirmation**: Integrate volume analysis into the strategy logic, confirming engulfing patterns only when accompanied by increased volume, which can improve signal quality.

5. **Market Environment Adaptation**: Add market environment recognition capabilities, for example, by using volatility indicators (such as ATR) or trend strength indicators (such as ADX) to distinguish between trending and ranging markets, and adjust strategy parameters accordingly.

6. **Optimize Time Filters**: Consider using more refined time filtering mechanisms, such as determining optimal trading periods based on historical data analysis, rather than simply excluding fixed time periods.

#### Conclusion

The Multi-Timeframe Trend Recognition and Candlestick Pattern Trading Strategy is a comprehensive trading system that combines medium to long-term trend analysis with short-term entry techniques. By confirming the overall market trend direction on a larger timeframe (15-minute) and identifying high-probability bullish engulfing patterns on a smaller timeframe (1-minute) to execute trades, the strategy can effectively improve entry accuracy.

Another major feature of this strategy is the integration of strict time filtering mechanisms and risk management systems, avoiding high volatility periods in the market, and controlling risk through fixed risk-reward ratios and forced position closure before market close. These features make the strategy particularly suitable for intraday traders seeking stable returns.

Although the strategy has clear logic and strict risk control, there are still multiple areas for optimization, including enhancing trend confirmation mechanisms, introducing dynamic risk management, adding more entry pattern recognition, integrating volume analysis, and developing market environment adaptation capabilities. Through these optimizations, the strategy has the potential to achieve more stable performance across different market environments.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-07 00:00:00
end: 2025-03-05 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Multi-Timeframe Strategy with Time Filters", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// Define the 15-minute trend (long-term trend)
trend_15m = request.security(syminfo.tickerid, "15", close)

// Identify Bullish Engulfing pattern on the 1-minute chart
bullish_engulfing = close > open and open[1] > close[1] and close > open[1]

// Define the entry condition: Bullish Engulfing on the 1-minute chart and uptrend on the 15-minute chart
long_condition = bullish_engulfing and trend_15m > trend_15m[1]

// Define the current time
current_hour = hour
current_minute = minute

// Check if it's within the first 45 minutes or last 60 minutes of the trading day
first_45_minutes = (current_hour == 9 and current_minute < 45) // First 45 minutes of the day (9:00 - 9:45 AM)
last_60_minutes = (current_hour == 15 and current_minute >= 0) or (current_hour == 16 and current_minute < 60) // Last 60 minutes (3:00 - 4:00 PM)

// Block trades if within the restricted time windows
time_restricted = first_45_minutes or last_60_minutes

// Execute the strategy logic for long entry only if not within restricted time window
if (long_condition and not time_restricted)
    strategy.entry("Long", strategy.long)

// Initialize stop loss and take profit variables
var float stop_loss = na
var float take_profit = na

// Update stop loss and take profit values when a long entry is triggered
if (long_condition and not time_restricted)
    stop_loss := low[1]  // Set stop loss to the low of the previous candle
    take_profit := close + 2 * (close - stop_loss)  // Set take profit to 2:1 risk-to-reward ratio

// Set stop loss and take profit for the trade using strategy.exit
strategy.exit("Exit Long", "Long", stop=stop_loss, limit=take_profit)

// Close all positions at the end of the trading day (for example, at 16:00 EST)
end_of_day = (hour == 16 and minute == 0)  // 16:00 EST is the end of the day for most US markets

if (end_of_day)
    strategy.close_all()  // Close all open positions at the end of the day
```

> Detail

https://www.fmz.com/strategy/485292

> Last Modified

2025-03-07 09:57:01
