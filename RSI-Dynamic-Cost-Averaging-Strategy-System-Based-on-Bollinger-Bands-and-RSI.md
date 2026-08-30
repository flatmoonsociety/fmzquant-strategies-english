
> Name

Dynamic-Cost-Averaging-Strategy-System-Based-on-Bollinger-Bands-and-RSI
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/98b336242069c30f54a5cb08752a8f0784db13834466862bc61c0378ea932e2e.png)

[trans]
#### Overview
This strategy is a quantitative trading system that combines Bollinger Bands, Relative Strength Index (RSI) and Dynamic Cost Average (DCA). By setting fund management rules, the strategy automatically executes batch opening operations in market fluctuations, and combines technical indicators to judge buying and selling signals to achieve risk-controllable transaction execution. The system also includes take-profit logic and cumulative profit tracking functions, which can effectively monitor and manage trading performance.
#### Strategy Principle
The strategy mainly operates based on the following core components:
1. The Bollinger Bands indicator is used to determine the price fluctuation range. When the price touches the lower track, consider buying, and when the price hits the upper track, consider selling.
2. The RSI indicator is used to confirm the overbought and oversold status of the market. When the RSI is lower than 25, it is confirmed to be oversold, and when it is higher than 75, it is confirmed to be oversold.
3. The DCA module dynamically calculates the amount of each position based on account equity to achieve adaptive management of funds.
4. The take-profit module sets a profit target of 5% and automatically closes positions when the target is reached to protect profits.
5. The market status monitoring module calculates the range of market changes in 90 days to help determine the overall trend.
6. The cumulative profit tracking module records the profit and loss status of each transaction to facilitate the evaluation of strategy performance.
#### Strategic Advantages
1. Combined with cross-validation of multiple technical indicators to improve signal reliability
2. Adopt dynamic position management to avoid risks caused by fixed positions
3. Set reasonable profit-taking conditions and lock in profits in a timely manner
4. Equipped with market trend monitoring function to facilitate grasping the overall situation
5. Complete profit tracking system to facilitate analysis of strategy performance
6. The alarm function is well configured and can remind trading opportunities in real time
#### Strategy Risk
1. Volatile markets may frequently trigger signals, leading to increased transaction costs.
2. The RSI indicator may lag in trending markets.
3. Fixed percentage take-profit may exit prematurely in a strong trending market
4. The DCA strategy may cause a large retracement in a unilateral falling market.
The following measures are recommended to manage risk:
-Set maximum position limit
- Dynamically adjust parameters based on market volatility
- Add trend filter
- Implement a hierarchical take-profit strategy
#### Strategy optimization direction
1. Dynamic optimization of parameters:
- Bollinger Band parameters can be adaptively adjusted according to volatility
- RSI thresholds can change with market cycles
- The DCA capital ratio can be adjusted according to the account size
2. Signal system enhancement:
- Increased volume confirmation
- Add trend line analysis
- Combined with more technical indicators for cross-validation
3. Improved risk control:
- Implement dynamic stop loss
-Add maximum retracement control
- Set daily loss limit
#### Summary
This strategy builds a relatively complete trading system by comprehensively using technical analysis and fund management methods. The advantage of the strategy lies in multiple signal confirmations and perfect risk management, but it still needs to be fully tested and optimized in real trading. By continuously improving parameter settings and adding auxiliary indicators, this strategy is expected to achieve stable performance in actual transactions.
|| 

#### Overview
This strategy is a quantitative trading system that combines Bollinger Bands, Relative Strength Index (RSI), and Dynamic Cost Averaging (DCA). The strategy implements automatic position building through established money management rules during market fluctuations, while integrating technical indicators for buy/sell signal determination to achieve controlled risk execution. The system also includes take-profit logic and cumulative profit tracking functionality for effective monitoring and management of trading performance.

#### Strategy Principles
The strategy operates based on the following core components:
1. Bollinger Bands for determining price volatility ranges, considering buying at lower band and selling at upper band
2. RSI for confirming overbought/oversold conditions, confirming oversold below 25 and overbought above 75
3. DCA module dynamically calculates position sizes based on account equity for adaptive capital management
4. Take-profit module sets 5% profit target for automatic position closing
5. Market state monitoring calculates 90-day market changes to assess overall trends
6. Cumulative profit tracking records each trade's profit/loss for strategy performance evaluation

#### Strategy Advantages
1. Multiple technical indicator cross-validation improves signal reliability
2. Dynamic position management avoids fixed-position risks
3. Reasonable take-profit conditions secure timely profits
4. Market trend monitoring capabilities aid in big-picture understanding
5. Comprehensive profit tracking system facilitates strategy analysis
6. Well-configured alert system provides real-time trading opportunities

#### Strategy Risks
1. Choppy markets may trigger frequent signals increasing trading costs
2. RSI indicators may lag in trending markets
3. Fixed percentage take-profit may exit too early in strong trends
4. DCA strategy may cause significant drawdowns in prolonged downtrends
Risk management recommendations:
- Set maximum position limits
- Dynamically adjust parameters based on market volatility
- Add trend filters
- Implement tiered take-profit strategy

#### Strategy Optimization Directions
1. Parameter Dynamic Optimization:
- Bollinger Bands parameters adapt to volatility
- RSI thresholds vary with market cycles
- DCA allocation adjusts with account size

2. Signal System Enhancement:
- Add volume confirmation
- Include trendline analysis
- Integrate additional technical indicator cross-validation

3. Risk Control Improvement:
- Implement dynamic stop-loss
- Add maximum drawdown control
- Set daily loss limits

#### Summary
The strategy builds a comprehensive trading system through combined technical analysis and money management methods. Its strengths lie in multiple signal confirmation and thorough risk management, though it still requires extensive testing and optimization in live trading. Through continuous improvement in parameter settings and additional auxiliary indicators, the strategy shows promise for stable performance in actual trading.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-27 00:00:00
end: 2024-11-26 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Combined BB RSI with Cumulative Profit, Market Change, and Futures Strategy (DCA)", shorttitle="BB RSI Combined DCA Strategy", overlay=true)

// Input Parameters
length = input.int(20, title="BB Length")  // Adjusted BB length
mult = input.float(2.5, title="BB Multiplier")  // Adjusted BB multiplier
rsiLength = input.int(14, title="RSI Length")  // Adjusted RSI length
rsiBuyLevel = input.int(25, title="RSI Buy Level")  // Adjusted RSI Buy Level
rsiSellLevel = input.int(75, title="RSI Sell Level")  // Adjusted RSI Sell Level
dcaPositionSizePercent = input.float(1, title="DCA Position Size (%)", tooltip="Percentage of equity to use in each DCA step")
takeProfitPercentage = input.float(5, title="Take Profit (%)", tooltip="Take profit percentage for DCA strategy")

// Calculate DCA position size
equity = strategy.equity  // Account equity
dcaPositionSize = (equity * dcaPositionSizePercent) / 100  // DCA position size as percentage of equity

// Bollinger Bands Calculation
basis = ta.sma(close, length)
dev = mult * ta.stdev(close, length)
upper = basis + dev
lower = basis - dev

// RSI Calculation
rsi = ta.rsi(close, rsiLength)

// Plotting Bollinger Bands and RSI levels
plot(upper, color=color.red, title="Bollinger Upper")
plot(lower, color=color.green, title="Bollinger Lower")
hline(rsiBuyLevel, "RSI Buy Level", color=color.green)
hline(rsiSellLevel, "RSI Sell Level", color=color.red)

// Buy and Sell Signals
buySignal = (rsi < rsiBuyLevel and close <= lower)
sellSignal = (rsi > rsiSellLevel and close >= upper)

// DCA Strategy: Enter Long or Short based on signals with calculated position size
if (buySignal)
    strategy.entry("DCA Buy", strategy.long)

if (sellSignal)
    strategy.entry("DCA Sell", strategy.short)

// Take Profit Logic
if (strategy.position_size > 0)  // If long
    strategy.exit("Take Profit Long", from_entry="DCA Buy", limit=close * (1 + takeProfitPercentage / 100))

if (strategy.position_size < 0)  // If short
    strategy.exit("Take Profit Short", from_entry="DCA Sell", limit=close * (1 - takeProfitPercentage / 100))

// Plot Buy/Sell Signals on the chart
plotshape(buySignal, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY", textcolor=color.white)
plotshape(sellSignal, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL", textcolor=color.white)

// Alerts for Buy/Sell Signals
alertcondition(buySignal, title="Buy Alert", message="Buy Signal Detected")
alertcondition(sellSignal, title="Sell Alert", message="Sell Signal Detected")

// Cumulative Profit Calculation
var float buyPrice = na
var float profit = na
var float cumulativeProfit = 0.0  // Cumulative profit tracker

if (buySignal)
    buyPrice := close
if (sellSignal and not na(buyPrice))
    profit := (close - buyPrice) / buyPrice * 100
    cumulativeProfit := cumulativeProfit + profit  // Update cumulative profit
    label.new(bar_index, high, text="P: " + str.tostring(profit, "#.##") + "%", color=color.blue, style=label.style_label_down)
    buyPrice := na  // Reset buyPrice after sell

// Plot cumulative profit on the chart
var label cumulativeLabel = na
if (not na(cumulativeProfit))
    if not na(cumulativeLabel)
        label.delete(cumulativeLabel)
    cumulativeLabel := label.new(bar_index, high + 10, text="Cumulative Profit: " + str.tostring(cumulativeProfit, "#.##") + "%", color=color.purple, style=label.style_label_up)

// Market Change over 3 months Calculation
threeMonthsBars = 3 * 30 * 24  // Approximation of 3 months in bars (assuming 1 hour per bar)
priceThreeMonthsAgo = request.security(syminfo.tickerid, "D", close[threeMonthsBars])
marketChange = (close - priceThreeMonthsAgo) / priceThreeMonthsAgo * 100

// Plot market change over 3 months
var label marketChangeLabel = na
if (not na(marketChange))
    if not na(marketChangeLabel)
        label.delete(marketChangeLabel)
    marketChangeLabel := label.new(bar_index, high + 20, text="Market Change (3 months): " + str.tostring(marketChange, "#.##") + "%", color=color.orange, style=label.style_label_up)

// Both labels (cumulative profit and market change) are displayed simultaneously
var label infoLabel = na
if (not na(cumulativeProfit) and not na(marketChange))
    if not na(infoLabel)
        label.delete(infoLabel)
    infoLabel := label.new(bar_index, high + 30, text="Cumulative Profit: " + str.tostring(cumulativeProfit, "#.##") + "% | Market Change (3 months): " + str.tostring(marketChange, "#.##") + "%", color=color.purple, style=label.style_label_upper_right)

```

> Detail

https://www.fmz.com/strategy/473153

> Last Modified

2024-11-27 16:37:12
