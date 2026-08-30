
> Name

Bitcoin-Momentum-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14b59777f9bf5d971ca.png)
[trans]

## Strategy Overview
The Bitcoin Momentum Trailing Stop Strategy is a momentum-based long position strategy designed to capture the upward trend of Bitcoin while avoiding downside risk by dynamically adjusting the stop loss. This strategy uses a simple yet clever momentum trailing stop technique, tightening the stop during periods of highly bearish volatility to protect exposed profits, and loosening the stop to let profits run during periods of sustained bullish momentum. This strategy will hold the position as long as the price of Bitcoin is above the 20-week moving average (EMA), and will close the position with a stop loss when the price falls below the 20-week moving average. This strategy only trades one position, not shorting, but if you know what you're doing, you can easily adjust it to do anything you like.
## Strategy Principle
1. The current price of Bitcoin must be above the EMA of the high-level time frame (20-week EMA)
2. Bitcoin cannot be in an "alert" state, that is, the latest peak of Bitcoin minus the lowest price of the current K-line is greater than 1.5 times ATR, or the closing price of the day is lower than the 20EMA of the day.
3. The stop loss is set to the latest wave peak minus 1 ATR. If it is in the alert state, minus 20% of the ATR (i.e. 0.2 ATR)
4. When the price closes below the stop loss price, close the position at the opening of the next K-line
This strategy uses the weekly chart and the 20-week EMA as a trend filter, only entering when the price is above the 20-week EMA. The 5-period ATR is used to dynamically adjust the distance of the trailing stop loss, and will tighten the stop loss in the alert state. The alert state is defined by two conditions: the distance from the recent wave peak to the current lowest price is greater than 1.5 times ATR, or the closing price of the day is lower than the 20EMA of the day. This dynamic stop-loss adjustment method can give greater retracement space when the trend is strong and quickly lock in profits when the trend weakens.
## Strategic Advantages
1. Simple and effective: The logic of this strategy is simple and clear, easy to understand and implement, and it can effectively capture the main upward trend of Bitcoin.
2. Dynamic stop loss: Dynamically adjust the stop loss position according to market fluctuations, which can not only control the retracement, but also allow profits to run. It is a more balanced and stable stop loss method.
3. Trend filtering: Through high-level moving average (20-week EMA) filtering, only enter the market during a clear upward trend, which greatly improves the strategy winning rate and profit-loss ratio.
4. Position management: The default is full position trading, which can maximize the use of funds and improve the efficiency of fund utilization. At the same time, the position size can also be adjusted flexibly.
5. Wide applicability: The strategy logic can be easily transplanted to other targets and markets, and has good versatility.
## Strategy Risk
1. Parameter applicability: The parameters of this strategy are set based on the characteristics of the Bitcoin market. The applicability to other markets needs to be verified, and parameter optimization may be required for different targets.
2. Trend identification: This strategy mainly relies on technical indicators such as high-level EMA and ATR to judge trends. The grasp of the market is not as comprehensive as fundamental analysis, and mistakes are prone to occur at market turning points.
3. Stop loss risk: Although dynamic stop loss can control risks to a certain extent, under extreme market conditions (such as plummets or rapid and deep shocks), large retracements may still occur. Moreover, the stop loss position is relatively close, and the loss may be stopped frequently in the volatile market.
4. Profit space: The strategy performs well in a unilateral upward trend, but in volatile markets it is more likely to fall into the dilemma of frequent stop losses, and the overall profit space may be limited.
5. Real offer performance: This strategy performed well in backtesting, but the actual offer is affected by slippage, handling fees and other factors, and there may be a certain gap with theoretical returns, so it needs to be evaluated carefully.
## Optimization direction
1. Trend judgment: You can try to introduce more high-level moving averages, volatility indicators and even fundamental data to improve the accuracy and reliability of trend identification.
2. Dynamic parameters: Stop loss levels and ATR parameters can be further optimized and dynamic adjustment mechanisms related to price or volatility introduced to adapt to different market conditions.
3. Position management: You can dynamically adjust the position size based on indicators such as trend strength and volatility. Increase the position when the trend is strong, reduce the position when the volatility is high, and improve the return-to-risk ratio.
4. Long-short mechanism: Introduce a short-selling mechanism in a bear market to expand the scope of application and potential profit potential of the strategy. However, rules such as entry and stop loss need to be redesigned.
5. Combination strategy: Combine this strategy with other strategies (such as reversal, mean reversion, etc.) to complement each other's advantages and improve strategy stability and profitability.
## Strategy summary
The Bitcoin momentum tracking stop loss strategy is a simple and effective momentum strategy that uses high-level moving averages and ATR indicators to capture Bitcoin's strong upward trend and control downside risks by dynamically adjusting stop losses. This strategy has clear logic, is easy to implement and optimize, and is suitable for medium and long-term investors who pursue stable returns. However, its performance is average in a volatile market, and its overall profit potential is limited.
This strategy can be used as a basic template. Investors can further improve it in terms of trend judgment, parameter optimization, position management, long-short mechanism, etc. based on their own needs and experience, or combine it with other strategies in order to obtain a higher return-to-risk ratio. However, it should be noted that the performance of this strategy in real trading may be different from the backtest results, and risks need to be carefully evaluated and controlled. Any strategy needs to be fully backtested with historical data and simulated trading before use, and dynamically adjusted according to market changes.
|| 

## Strategy Overview

The Bitcoin Momentum Trailing Stop Strategy is a long-only momentum-based strategy designed to capture Bitcoin's uptrends while mitigating downside risk through dynamically adjusted stop-losses. The strategy employs a simple yet clever momentum trailing stop technique, which tightens the stop-loss during highly bearish volatility to protect open profits and loosens the stop-loss during sustained bullish momentum to let profits run. The strategy remains invested as long as the Bitcoin price is above the 20-week exponential moving average (EMA) and exits when the price closes below it. It trades only one position and does not short, but it can be easily tweaked to do whatever you like if you know what you're doing.

## Strategy Principle

1. Bitcoin's current price must be trading above the higher-timeframe EMA (20-week EMA).
2. Bitcoin must not be in a "caution" state, defined as the recent swing high minus the current bar's low being greater than 1.5 times the ATR, or the daily close being lower than the daily 20 EMA.
3. The stop-loss is set at the recent swing high minus 1 ATR, or minus 20% of the ATR (i.e., 0.2 ATR) if in the caution state.
4. Exit on the next bar's open when the price closes below the stop-loss.

The strategy uses the weekly chart and the 20-week EMA as a trend filter, only entering when the price is above the 20-week EMA. A 5-period ATR is used to dynamically adjust the distance of the trailing stop, which tightens in the caution state. The caution state is defined by two conditions: the distance from the recent swing high to the current low being greater than 1.5 times the ATR, or the daily close being below the daily 20 EMA. This dynamic stop-loss adjustment approach allows for greater pullback room when the trend is strong and quickly locks in profits when the trend weakens.

## Strategy Advantages

1. Simplicity and effectiveness: The strategy logic is simple, clear, easy to understand and implement, while effectively capturing Bitcoin's major uptrends.

2. Dynamic stop-loss: The stop-loss position is dynamically adjusted based on market volatility conditions, controlling drawdowns while letting profits run, which is a relatively balanced and robust approach to stop-loss management.

3. Trend filtering: By filtering with a higher-level moving average (20-week EMA), the strategy only enters during clear uptrends, greatly improving the strategy's win rate and risk-reward ratio.

4. Position sizing: The default is to trade with a full position, maximizing capital utilization and improving capital efficiency. Position size can also be flexibly adjusted.

5. Wide applicability: The strategy logic can be easily ported to other assets and markets, having good generalizability.

## Strategy Risks

1. Parameter applicability: The strategy parameters are set based on the characteristics of the Bitcoin market, and their applicability to other markets needs to be validated and may require parameter optimization for different assets.

2. Trend identification: The strategy mainly relies on technical indicators such as higher-level EMAs and ATRs to judge trends, which is not as comprehensive as fundamental analysis in grasping market conditions and is prone to errors at market turning points.

3. Stop-loss risk: Although dynamic stop-losses can control risk to a certain extent, significant drawdowns may still occur in extreme market conditions (such as sharp drops or rapid deep fluctuations). Moreover, the stop-loss position is relatively tight, which may lead to frequent stop-outs in choppy markets.

4. Profit potential: The strategy performs well in unidirectional uptrends but is more likely to fall into the dilemma of frequent stop-losses in rangebound markets, potentially limiting overall profit potential.

5. Live performance: While the strategy performs well in backtesting, live trading is affected by factors such as slippage and commissions, and actual results may differ from theoretical returns, requiring careful evaluation.

## Optimization Directions

1. Trend determination: Consider introducing more higher-level moving averages, volatility indicators, or even fundamental data to improve the accuracy and reliability of trend identification.

2. Dynamic parameters: Stop-loss positions and ATR parameters can be further optimized by introducing dynamic adjustment mechanisms related to price or volatility to adapt to different market states.

3. Position sizing: Dynamically adjust position size based on indicators such as trend strength and volatility, increasing position size when the trend is strong and reducing position size during high volatility to improve the risk-reward ratio.

4. Long/short mechanism: Introduce a short-selling mechanism in bear markets to expand the strategy's applicability and potential profitability. However, entry and stop-loss rules need to be redesigned.

5. Strategy combination: Combine this strategy with other strategies (such as mean reversion) to complement each other's strengths and improve strategy stability and profitability.

## Strategy Summary

The Bitcoin Momentum Trailing Stop Strategy is a simple and effective momentum strategy that captures Bitcoin's strong uptrends using higher-level moving averages and ATR indicators while controlling downside risk through dynamically adjusted stop-losses. The strategy logic is clear, easy to implement and optimize, and suitable for medium to long-term investors seeking steady returns. However, it performs averagely in rangebound markets with limited overall profit potential.
This strategy can serve as a basic template, and investors can further refine it based on their own needs and experience in areas such as trend determination, parameter optimization, position management, and long/short mechanisms, or combine it with other strategies to achieve a higher risk-reward ratio. However, it should be noted that the live performance of the strategy may differ from backtesting results, requiring careful risk assessment and control. Any strategy should be thoroughly backtested on historical data and forward tested before use, and dynamically adjusted based on market changes.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_timeframe_1|W|(?G_STRATEGY)Higher Timeframe|
|v_input_int_1|20|EMA Length|
|v_input_int_2|5|ATR Length|
|v_input_source_1_low|0|(?G_EXIT)Trail Stop Source: low|high|close|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_3|7|Trail Stop Lookback|
|v_input_float_1|0.2|Trailing Stop Ratchet Multiplier|
|v_input_1|timestamp(01 Jan 2000 13:30 +0000)|(?G_FILTER)Start Filter|
|v_input_2|timestamp(1 Jan 2099 19:30 +0000)|End Filter|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-08 00:00:00
end: 2024-03-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ZenAndTheArtOfTrading
// ------------------------------------------------------------------------------------------------------
// System Concept: Capture as much Bitcoin upside volatility as possible while side-stepping downside volatility.
//  Entry Rule #1: Bitcoin must be trading above higher-timeframe EMA (Weekly 20 EMA)
//  Entry Rule #2: Bitcoin must not be in 'caution' condition
//      -> Caution: True if BTC's recent swing high minus its current low is > 1.5x ATR OR close < Daily EMA
//  Trailing Stop: Stop is trailed 1 ATR from recent swing high, OR 20% of ATR if in caution condition
// ------------------------------------------------------------------------------------------------------
// @version=5
strategy("Bitcoin Momentum Strategy", 
     overlay=true)

// Get user input
var const string    G_STRATEGY  = "Strategy Entry Settings"
var const string    G_EXIT      = "Strategy Exit Settings"
var const string    G_FILTER    = "Strategy Filters"
i_HigherTimeframe   = input.timeframe("W", "Higher Timeframe", group=G_STRATEGY, tooltip="Higher timeframe MA reference")
i_EmaLength         = input.int(20, "EMA Length", group=G_STRATEGY, tooltip="Moving average period length")
i_AtrLength         = input.int(5, "ATR Length", group=G_STRATEGY, tooltip="ATR period length")
i_TrailStopSource   = input.source(low, "Trail Stop Source", group=G_EXIT, tooltip="Lowest price source for trailing stop")
i_TrailStopLookback = input.int(7, "Trail Stop Lookback", group=G_EXIT, tooltip="How many bars to look back for trailing price source")
i_TrailStopMulti    = input.float(0.2, "Trailing Stop Ratchet Multiplier", group=G_EXIT, tooltip="When momentum is yellow (caution), shrink ATR distance for TS by this much")
i_StartTime         = input(timestamp("01 Jan 2000 13:30 +0000"), "Start Filter", group=G_FILTER, tooltip="Start date & time to begin searching for setups")
i_EndTime           = input(timestamp("1 Jan 2099 19:30 +0000"), "End Filter", group=G_FILTER, tooltip="End date & time to stop searching for setups")

// Define custom security function which does not repaint
RequestSecurity_NonRP(_market, _res, _exp) => request.security(_market, _res, _exp[barstate.isrealtime ? 1 : 0])[barstate.isrealtime ? 0 : 1]

// Define date filter check
DateFilter(int start, int end) => time >= start and time <= end

// Get indicator values
float   atrValue    = ta.atr(i_AtrLength)
float   emaValue    = ta.ema(close, i_EmaLength)
float   htfEmaValue = RequestSecurity_NonRP(syminfo.tickerid, i_HigherTimeframe, emaValue)
float   marketPrice = close

// Check for bullishness / bearish volatility caution
bool    isBullish   = marketPrice > htfEmaValue
bool    isCaution   = isBullish and (ta.highest(high, 7) - low > (atrValue * 1.5) or marketPrice < emaValue) 

// Set momentum color
color bgCol = color.red
if isBullish[1]
    bgCol := color.green
if isCaution[1]
    bgCol := color.orange

// Handle strategy entry, and reset trailing stop
var float trailStop = na
if isBullish and strategy.position_size == 0 and not isCaution
    strategy.entry(id="Buy", direction=strategy.long)
    trailStop := na

// Update trailing stop
float temp_trailStop = ta.highest(i_TrailStopSource, i_TrailStopLookback) - (isCaution[1] ? atrValue * i_TrailStopMulti : atrValue)
if strategy.position_size > 0
    if temp_trailStop > trailStop or na(trailStop)
        trailStop := temp_trailStop

// Handle strategy exit
if (close < trailStop or close < htfEmaValue) and barstate.isconfirmed
    strategy.close("Buy", comment="Sell")

// Draw trailing stop, HTF EMA and color-coded momentum indicator
plotshape(true, color=bgCol, style=shape.square, location=location.bottom, size=size.auto, title="Momentum Strength")
plot(htfEmaValue, color=close > htfEmaValue ? color.green : color.red, linewidth=2, title="HTF EMA")
plot(emaValue, color=close > emaValue ? color.green : color.red, linewidth=1, title="CTF EMA")
plot(strategy.position_size[1] > 0 ? trailStop : na, style=plot.style_linebr, color=color.red, title="Stop Loss")
```

> Detail

https://www.fmz.com/strategy/444020

> Last Modified

2024-03-08 16:20:16
