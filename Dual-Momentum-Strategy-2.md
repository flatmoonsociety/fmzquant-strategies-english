
> Name

Dual-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
The dual momentum strategy achieves the purpose of buying low and selling high by identifying the K-line pattern of continuous rising or falling stocks. It uses simple indicator judgments, is easy to implement, and is suitable for medium and short-term transactions.
### Strategy Principles
This strategy is mainly based on two indicators: **number of rising K lines** and **number of falling K lines**.
- When close rises more than LongEnterAfter K lines, go long; when close falls more than LongExitAfter K lines, close the long position.
- When close falls more than ShortEnterAfter K lines, go short; when close rises more than ShortExitAfter K lines, close the short position.
The above parameters can be adjusted to determine the specific trading rules by adjusting LongEnterAfter, LongExitAfter, ShortEnterAfter and ShortExitAfter.
This strategy captures changes in stock price momentum and determines the timing of entry and exit by continuously monitoring the rise and fall of daily closing prices. When the K-line pattern set by the indicator parameters appears, perform the corresponding buy opening or sell closing operation.
To sum up, the core of the dual momentum strategy is to identify the short-term rising and falling trends of stock prices to determine the trading direction and timing. It is simple and direct, and the aggressiveness of the strategy can be adjusted through parameter settings.
### Advantage Analysis
The dual momentum strategy offers the following advantages:
- The idea is simple and direct, easy to understand and implement.
- Configurable parameters to adjust the aggressiveness of the strategy.
- Paying attention to the short-term trend of stock prices will help capture stock momentum.
- Combined with stop loss, risk can be effectively controlled.
- Suitable for stocks that are sensitive to stock price fluctuations, especially small and medium-capitalization stocks.
Generally speaking, the dual momentum strategy is suitable for investors who are more sensitive to stock price changes and pursue high operating frequency. It can seize the short-term operation of individual stocks and obtain excess returns. The frequency and risk of the strategy can be controlled by adjusting parameters.
### Risk Analysis
Dual momentum strategies also have the following risks:
- Too much reliance on parameter settings. Different parameters may lead to large differences in transaction frequency and income.
- Only focusing on the short-term trend of stock prices may miss long-term opportunities.
- Higher trading frequency increases transaction costs and slippage risk.
- Improper stop loss setting may result in losses exceeding what is tolerated.
- Not suitable for stocks with volatile prices or long-term consolidation.
- There is a risk of arbitrage, so you need to pay attention to changes in trading volume.
To control risks, the following measures can be considered:
- Adjust parameters, reduce transaction frequency, and control the risk of over-optimization caused by frequent switching of buying and selling points.
- Properly extend the holding period and pay attention to the medium and long-term trends.
-Set stop loss points and strictly control single losses.
- Prefer stocks with sustained breakthroughs and avoid choosing volatile stocks.
- Increase the importance of trading volume to avoid arbitrage risks when volume decreases.
### Optimization direction
This strategy can be optimized by considering the following points:
- Add trend judgment indicators to avoid wrong trades at the end of the trend. Indicators such as MACD and KDJ can be introduced to determine the general trend.
- Increase the judgment of trading volume and avoid opening a position when the volume decreases.
- Set a trailing stop to lock in profits, and you can use ATR at least N times to trail the stop.
- Add backtest parameter combination optimization to find optimal parameters to improve stability.
- Add algorithmic trading module to achieve more intelligent order management.
- Use machine learning technology to discover more effective trading signals.
Generally speaking, the main optimization direction is to improve strategy stability, control risks, and explore more effective alpha. At the same time, it is also important to enhance algorithmic trading capabilities.
### Summarize
The dual momentum strategy implements stock timing trading through simple continuous rise and fall K-line judgments. It is easy to implement and parameters can be adjusted to control the aggressiveness. It is mainly suitable for investors who pursue short-term profits, especially for small and medium-sized market capitalization stocks. At the same time, you also need to pay attention to risks such as parameter over-optimization, stop loss settings, and changes in trading volume. Optimization can improve the stability of the strategy. Overall, the dual momentum strategy is an efficient and flexible quantitative strategy and is worth exploring its application value.
||

### Overview

The dual momentum strategy aims to buy low and sell high by identifying consecutive up or down candlestick patterns in stock prices. It uses simple indicators for decision making and is easy to implement for mid-to-short term trading.

### Strategy Logic

The strategy is based on two metrics: **number of rising bars** and **number of falling bars**. 

- Go long when close rises above LongEnterAfter bars, close long when close falls below LongExitAfter bars.

- Go short when close falls below ShortEnterAfter bars, close short when close rises above ShortExitAfter bars.

The exact trading rules are determined by tuning LongEnterAfter, LongExitAfter, ShortEnterAfter and ShortExitAfter. 

The strategy captures momentum shifts in stock prices by monitoring daily closing prices. It triggers entry and exit signals based on the candlestick patterns defined in the parameters.

In summary, the core of the dual momentum strategy is identifying short-term price uptrends and downtrends to determine trade direction and timing. It is simple and direct, and the aggressiveness can be adjusted through parameter tuning.

### Advantage Analysis

The dual momentum strategy has the following advantages:

- Simple and straightforward logic that is easy to understand and implement.

- Configurable parameters to adjust strategy aggressiveness.

- Captures short-term momentum which helps capitalize on stock trends.

- Stop loss can effectively control risks.

- Works well for stocks sensitive to price fluctuations, especially small-cap stocks.

Overall, the dual momentum strategy suits investors who are sensitive to price changes and pursue high trading frequency. It can capitalize on short-term stock moves and achieve alpha. The frequency and risk can be controlled through parameter tuning.

### Risk Analysis

The dual momentum strategy also has the following risks:

- Highly dependent on parameter settings which lead to large performance difference.

- Ignores long-term moves by focusing only on short-term trends.

- High trading frequency increases costs and slippage risks.

- Improper stop loss setting may lead to unacceptable loss.

- Not suitable for range-bound or long-consolidation stocks.

- Risks of being gamed by smart money when volume dries up.

The risks can be mitigated by:

- Adjusting parameters to reduce trading frequency and over-optimization risks.

- Allowing longer holding periods to account for medium-long term trends. 

- Setting stop loss to strictly control single trade loss.

- Selecting stocks with high momentum and avoiding choppy stocks.

- Increasing importance of volume to avoid risks when volume declines.

### Enhancement Opportunities

The strategy can be enhanced in several ways:

- Add trend indicators like MACD and KDJ to avoid trades against major trend.

- Add volume condition to avoid entries when volume declines.

- Add moving stop loss to lock in profits, e.g. xN ATR trailing stop.

- Optimize parameters through backtesting to improve stability.

- Incorporate algorithmic trading models for better order management. 

- Apply machine learning to discover more effective signals.

Overall, the main focus is improving stability, controlling risks, and discovering new alpha factors. Enhancing algorithmic trading capabilities is also important.

### Summary

The dual momentum strategy times the market through simple consecutive up/down bar metrics. It is easy to implement and the aggressiveness is adjustable. It suits short-term traders, especially for small-cap stocks. Risk management against over-optimization, stop loss, volume changes etc. is important. With enhancements, it can become a highly effective and flexible quant strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|enter long after X rising blocks|
|v_input_2|true|exit long after X falling blocks|
|v_input_3|2|enter short after X falling blocks|
|v_input_4|true|exit short after X rising blocks|
|v_input_5|2017|trade since year|
|v_input_6|true|trade since month|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-02 00:00:00
end: 2023-10-08 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
// strategy(title="simple momentum", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// ====================================
// STUDY AND STRATEGY

// Inputs
LongEnterAfter = input(title="enter long after X rising blocks",  defval=2)
LongExitAfter = input(title="exit long after X falling blocks",  defval=1)
ShortEnterAfter = input(title="enter short after X falling blocks",  defval=2)
ShortExitAfter = input(title="exit short after X rising blocks",  defval=1)

// Criteria
Valid = change(time)
LongEnter = Valid and rising(close, LongEnterAfter)
LongExit = Valid and falling(close, LongExitAfter)
ShortEnter = Valid and falling(close, ShortEnterAfter)
ShortExit = Valid and rising(close, ShortExitAfter)

// ====================================
// STRATEGY

TradeSinceYear = input(title="trade since year",  defval=2017)
TradeSinceMonth = input(title="trade since month",  defval=1)

if year > TradeSinceYear or (year == TradeSinceYear and month >= TradeSinceMonth)
    strategy.entry("long", strategy.long, when = LongEnter)
    strategy.close("long", when = LongExit)

    strategy.entry("short", strategy.short, when = ShortEnter)
    strategy.close("short", when = ShortExit)

```

> Detail

https://www.fmz.com/strategy/428785

> Last Modified

2023-10-09 15:03:30
