
> Name

Dual-Indicator-Trading-Strategy-Combining-Trend-Following-and-Momentum
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/bac42fc1d476462b5c4fdb37838f1275bb2999e05eb4323c338a6e35b45684a6.png)

[trans]
#### Overview
This strategy combines two methods, trend following and momentum analysis, using the Simple Moving Average (SMA) and Moving Average Convergence Divergence (MACD) indicators to identify potential trading opportunities. The strategy determines the overall market trend through the Trendilo indicator, an SMA-based trend indicator, while using the MACD's zero line crossover to capture short-term momentum changes. In addition, the strategy uses the Average True Range (ATR) to dynamically set stop loss and take profit levels to adapt to changes in market volatility.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Trendilo indicator: Uses a 50-period simple moving average to determine the medium- and long-term trend direction.
2. MACD zero line crossover: used to capture changes in short-term momentum as an entry signal.
3. ATR stop loss/profit setting: Use the 14-period ATR to dynamically adjust risk management parameters.
Specifically, when the MACD line crosses the zero line from below (crossing above), and the closing price is higher than the Trendilo line, a long signal is triggered. On the contrary, when the MACD line crosses the zero line from above (crosses below), and the closing price is below the Trendilo line, a short signal is triggered. Once entered, the strategy uses ATR-based stop-loss and take-profit levels to manage risk and lock in profits.
#### Strategic Advantages
1. Trend confirmation: By combining Trendilo and MACD, the strategy can capture short-term momentum changes while confirming the overall trend, effectively reducing false signals.
2. Dynamic risk management: Using ATR to set stop loss and profit levels enables the strategy to automatically adjust according to market volatility, improving the adaptability of the strategy.
3. Multi-cycle analysis: combines medium- and long-term (Trendilo) and short-term (MACD) indicators to provide a more comprehensive market perspective.
4. Visual support: The strategy marks buying and selling signals and trend lines on the chart to facilitate traders to intuitively understand market conditions.
#### Strategy Risk
1. Trend reversal risk: Perform well in strong trending markets, but may incur losses in sideways or rapidly reversing markets.
2. Parameter sensitivity: Strategy performance may be highly sensitive to the choice of input parameters (such as Trendilo period, ATR multiplier, etc.).
3. Excessive trading: In a volatile market, frequent trading signals may be generated, increasing transaction costs.
4. Hysteresis: Due to the use of moving averages, the strategy may miss some opportunities in the early stages of the trend.
#### Strategy optimization direction
1. Introduce filters: Additional technical indicators or market sentiment indicators can be added to filter out low-quality trading signals.
2. Optimize parameter selection: Find the optimal combination of Trendilo cycle and ATR multiplier through historical data backtesting.
3. Add volatility adjustment: dynamically adjust the strategy parameters according to the current market volatility to improve the adaptability of the strategy.
4. Implement partial position management: Consider adjusting the position size of each trade based on signal strength or market conditions.
5. Add time filtering: Add trading time window restrictions to avoid periods of greater volatility or poor liquidity.
#### Summarize
This strategy cleverly combines trend following and momentum analysis, providing traders with a relatively comprehensive market analysis framework through the synergy of Trendilo and MACD. A dynamic risk management approach enhances the adaptability of the strategy, allowing it to maintain stability in different market environments. However, traders still need to be cautious when using this strategy, especially in terms of parameter optimization and risk control. With continuous monitoring and optimization, this strategy has the potential to become a reliable trading tool, especially for investors who want to capture opportunities in trending markets.
|| 

#### Overview

This strategy combines trend following and momentum analysis methods, utilizing Simple Moving Average (SMA) and Moving Average Convergence Divergence (MACD) indicators to identify potential trading opportunities. The strategy uses the Trendilo indicator (a trend indicator based on SMA) to determine the overall market trend, while employing MACD zero line crossovers to capture short-term momentum changes. Additionally, the strategy incorporates Average True Range (ATR) to dynamically set stop-loss and take-profit levels, adapting to changes in market volatility.

#### Strategy Principles

The core logic of the strategy is based on the following key elements:

1. Trendilo Indicator: Uses a 50-period simple moving average to determine medium to long-term trend direction.
2. MACD Zero Line Crossover: Used to capture changes in short-term momentum as entry signals.
3. ATR Stop-Loss/Take-Profit Setting: Utilizes a 14-period ATR to dynamically adjust risk management parameters.

Specifically, a long signal is triggered when the MACD line crosses above zero and the closing price is above the Trendilo line. Conversely, a short signal is triggered when the MACD line crosses below zero and the closing price is below the Trendilo line. After entry, the strategy uses ATR-based stop-loss and take-profit levels to manage risk and lock in profits.

#### Strategy Advantages

1. Trend Confirmation: By combining Trendilo and MACD, the strategy can capture short-term momentum changes while confirming the overall trend, effectively reducing false signals.
2. Dynamic Risk Management: Using ATR to set stop-loss and take-profit levels allows the strategy to automatically adjust to market volatility, enhancing its adaptability.
3. Multi-timeframe Analysis: Combines medium to long-term (Trendilo) and short-term (MACD) indicators, providing a more comprehensive market perspective.
4. Visual Support: The strategy marks buy and sell signals and trend lines on the chart, facilitating intuitive understanding of market conditions for traders.

#### Strategy Risks

1. Trend Reversal Risk: Performs well in strong trending markets but may generate losses in ranging or rapidly reversing markets.
2. Parameter Sensitivity: Strategy performance may be highly sensitive to the choice of input parameters (such as Trendilo period, ATR multipliers, etc.).
3. Overtrading: In highly volatile markets, frequent trading signals may be generated, increasing transaction costs.
4. Lagging Nature: Due to the use of moving averages, the strategy may miss some opportunities at the beginning of trends.

#### Strategy Optimization Directions

1. Introduce Filters: Additional technical indicators or market sentiment indicators can be added to filter out low-quality trading signals.
2. Optimize Parameter Selection: Through historical data backtesting, find the optimal combination of Trendilo period and ATR multipliers.
3. Incorporate Volatility Adjustment: Dynamically adjust strategy parameters based on current market volatility to improve strategy adaptability.
4. Implement Partial Position Management: Consider adjusting the size of each trade based on signal strength or market conditions.
5. Add Time Filtering: Implement trading time window restrictions to avoid periods of high volatility or poor liquidity.

#### Conclusion

This strategy cleverly combines trend following and momentum analysis, providing traders with a relatively comprehensive market analysis framework through the synergy of Trendilo and MACD. The dynamic risk management approach enhances the strategy's adaptability, allowing it to maintain stability in different market environments. However, traders should still exercise caution when using this strategy, especially in terms of parameter optimization and risk control. Through continuous monitoring and optimization, this strategy has the potential to become a reliable trading tool, particularly suitable for investors looking to capture opportunities in trending markets.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-09-24 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("NNFX Trendilo + Zero MACD Strategy", overlay=true)

// --- Inputs ---
atrPeriod = input.int(14, title="ATR Period")
stopLossMultiplier = input.float(1.5, minval=0.0, maxval = 20.0, step = 0.1 ,title="Stop Loss Multiplier")
takeProfitMultiplier = input.float(2.0, minval=0.0 , maxval = 20.0, step = 0.1,title="Take Profit Multiplier")

// --- Trendilo ---
trendiloPeriod = input.int(50, title="Trendilo Period")
trendilo = ta.sma(close, trendiloPeriod)

// --- MACD ---
[macdLine, signalLine, _] = ta.macd(close, 12, 26, 9)
macdZeroCrossUp = ta.crossover(macdLine, 0)
macdZeroCrossDown = ta.crossunder(macdLine, 0)

// --- ATR for Stop Loss and Take Profit ---
atr = ta.atr(atrPeriod)
stopLoss = atr * stopLossMultiplier
takeProfit = atr * takeProfitMultiplier

// --- Trading Logic ---
longCondition = macdZeroCrossUp and close > trendilo
shortCondition = macdZeroCrossDown and close < trendilo

// --- Execute Long Trades ---
if (longCondition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit/Stop Loss", "Buy", limit=close + takeProfit, stop=close - stopLoss)

// --- Execute Short Trades ---
if (shortCondition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit/Stop Loss", "Sell", limit=close - takeProfit, stop=close + stopLoss)

// --- Plot Signals ---
plotshape(series=longCondition, location=location.belowbar, color=color.green, style=shape.labelup, text="Buy")
plotshape(series=shortCondition, location=location.abovebar, color=color.red, style=shape.labeldown, text="Sell")

// --- Plot Trendilo ---
plot(trendilo, color=color.blue, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/468334

> Last Modified

2024-09-26 16:14:22
