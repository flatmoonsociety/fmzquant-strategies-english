
> Name

Linear-Regression-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1bdbc5242543b5629d9.png)

[trans]

## Overview
The moving average reversion trading strategy determines buy and sell signals by calculating the intersection of the linear regression line of the stock price and the moving average. This strategy combines moving average and linear regression analysis, taking into account both the stock price trend and statistical characteristics, which can effectively determine the stock price reversal point and achieve buying low and selling high.
## Strategy Principle
This strategy first calculates the linear regression line of the n-day stock price and the m-day moving average. The linear regression line reflects the long-term statistical trend of the stock price, and the moving average reflects the short-term trend of the stock price.
When the moving average crosses the linear regression line, it indicates that the rising momentum of the stock price is increasing, generating a buy signal. When the moving average crosses the linear regression line, it indicates that the stock price is weak and a sell signal is generated.
Specifically, the strategy determines trading signals through the following steps:
1. Calculate the n-day stock price linear regression line lrLine
2. Calculate the m-day simple moving average lrMA of the linear regression line
3. Calculate the m-day exponential moving average EMA of the stock price
4. When ema crosses lrMA, a buy signal longEntry is generated
5. When ema crosses lrMA, a sell signal longExit is generated
6. At the same time, combined with the judgment of the market, the buying signal will only be considered when the market is bullish.
7. Execute buy and sell transactions based on signals
Determining the buying and selling timing through the intersection of the moving average and the regression line can effectively filter out false breaks and capture reversal points, allowing you to buy low and sell high.
## Strategic Advantages
- The regression line reflects the long-term trend, and the moving average reflects the short-term trend. Combining the dual indicators can accurately determine the buying and selling point.
- The regression line calculation is simple and easy to implement
- Use market judgment to filter out inappropriate trading signals
- Customizable parameters to adjust buying and selling strategies
- Achieved buying low and selling high, resulting in larger profit space
## Strategy Risk
- When the stock price fluctuates violently, the moving average and the regression line cross frequently, which may produce false signals.
- When the market judgment is inaccurate, the trading timing will also be misjudged.
- Improper parameter settings will also affect the strategy effect
- Frequent transactions and high transaction costs
Parameter adjustments that need attention include appropriately increasing the moving average and regression line cycle parameters and reducing the trading frequency. Set up a reasonable stop-loss strategy to control risks. Optimize market judgment rules and improve accuracy.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Moving average indicator optimization: Try different types of moving averages, such as weighted moving averages, etc., to find the best moving average suitable for the stock.
2. Regression line optimization: adjust the regression line calculation period and find the period parameters that best reflect the long-term trend of the stock.
3. Market judgment optimization: Test different market judgment indicators and find the market signals that are most suitable for the strategy.
4. Parameter optimization: Repeated backtesting through different parameter combinations to find the best parameter configuration.
5. Stop loss strategy optimization: test different stop loss methods and set the best stop loss logic to control risks.
6. Transaction cost optimization: According to different transaction fee models, adjust transaction frequency to reduce transaction costs.
Through the above optimization points, the stability and profitability of the strategy can be further improved.
## Summarize
This moving average regression trading strategy integrates the advantages of moving average analysis and linear regression analysis, and can effectively identify stock price reversal points and guide buying low and selling high. The strategy is relatively simple and reliable, and is suitable for medium and long-term stock selection transactions. Strategy stability can be further improved through parameter optimization and risk control. This strategy provides a feasible technical trading solution for stock market analysis.
||


## Overview

The Linear Regression Moving Average trading strategy generates buy and sell signals based on the crossovers between a linear regression line and moving average of the stock price. This strategy combines trend following with linear regression analysis to identify potential reversals and achieve buying low and selling high.

## Strategy Logic

The strategy first calculates a n-day linear regression line and m-day moving average of the stock price. The regression line captures long term statistical trends while the moving average reflects short term momentum. 

When the moving average crosses above the regression line, it signals strengthening upside momentum and generates a buy signal. When the moving average crosses below, it signals weakening upside and produces a sell signal.

Specifically, the strategy follows these steps to determine trade signals:

1. Calculate n-day linear regression line of prices lrLine

2. Calculate m-day simple moving average of lrLine called lrMA 

3. Calculate m-day exponential moving average of prices called ema

4. When ema crosses above lrMA, generate buy signal longEntry

5. When ema crosses below lrMA, generate sell signal longExit

6. Only consider buy signals when market is bullish

7. Execute trades based on the signals

By using crossover between regression and moving averages to determine entries, the strategy can effectively filter out false breaks and identify reversals for buying low and selling high.

## Advantages

- Combines trend and regression analysis for accurate signal identification 
- Regression line is simple to calculate and implement
- Uses market filtering to avoid unfavorable trades
- Customizable parameters for adjusting strategy
- Achieves buying low and selling high for profit

## Risks

- Frequent crossovers during volatility may generate false signals
- Inaccurate market filters lead to mistimed entries
- Poor parameter tuning impacts strategy performance 
- High trading frequency leads to higher costs

Parameters should be tuned to increase moving average and regression line periods and reduce trade frequency. Reasonable stop losses should be implemented to control risks. Market filters can be enhanced to improve accuracy.

## Enhancements

The strategy can be optimized in several aspects:

1. Moving average optimization by testing different types of MAs

2. Regression line optimization by adjusting calculation period 

3. Market filter optimization by testing different indicators

4. Parameter optimization through rigorous backtesting

5. Stop loss optimization by testing different stop loss logics 

6. Cost optimization by adjusting trade frequency based on costs

These optimizations can further improve the stability and profitability of the strategy. 

## Conclusion

The Linear Regression MA strategy integrates strengths of trend analysis and linear regression for effective reversal identification and buying low selling high. The straightforward strategy is suitable for stock picking over medium to long term horizons. With parameter tuning and risk control, the strategy can achieve even higher stability. It provides a viable technical trading framework for market analysis.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|true|Execute Long Trades|
|v_input_bool_2|true|Execute Short Trades|
|v_input_bool_3|true|Execute Stop Loss|
|v_input_float_1|10|Max Profit (%)|
|v_input_float_2|1.75|Stop Loss (%)|
|v_input_1|true|Show Date Range|
|v_input_int_1|true|(?Date Info)Start Month|
|v_input_int_2|true|Start Day|
|v_input_int_3|2022|Start Year|
|v_input_int_4|55|(?Averages)Linear Regression Line|
|v_input_int_5|55|Linear Regression MA|
|v_input_int_6|55|EMA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-18 00:00:00
end: 2023-10-24 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © lazy_capitalist

//@version=5
strategy('Linear Regression MA', overlay=true, initial_capital=10000)
datesGroup = "Date Info"
startMonth = input.int(defval = 1,    title = "Start Month",  minval = 1, maxval = 12,  group=datesGroup)
startDay   = input.int(defval = 1,    title = "Start Day",    minval = 1, maxval = 31,  group=datesGroup)
startYear  = input.int(defval = 2022, title = "Start Year",   minval = 1970,            group=datesGroup)

averagesGroup = "Averages"
lrLineInput     = input.int(title="Linear Regression Line",   defval=55, minval = 1, group=averagesGroup)
lrMAInput       = input.int(title="Linear Regression MA",     defval=55, minval = 1, group=averagesGroup)
emaInput        = input.int(title="EMA Length",               defval=55, minval = 1, group=averagesGroup)


tradesGroup = "Execute Trades"
executeLongInput    = input.bool(title="Execute Long Trades",       defval=true)
executeShortInput   = input.bool(title="Execute Short Trades",      defval=true)
executeStopLoss     = input.bool(title="Execute Stop Loss",         defval=true)

fourHrSMAExpr       = ta.sma(close, 200)
fourHrMA            = request.security(symbol=syminfo.tickerid, timeframe="240", expression=fourHrSMAExpr)

bullish             = close > fourHrMA ? true : false


maxProfitInput              = input.float(  title="Max Profit (%)",         defval=10.0,    minval=0.0)   * 0.01
stopLossPercentageInput     = input.float(  title="Stop Loss (%)",          defval=1.75,    minval=0.0)   * 0.01

start       = timestamp(startYear, startMonth, startDay, 00, 00)            // backtest start  window
window()    => time >= start ? true : false                              // create function "within window of time"
showDate    = input(defval = true, title = "Show Date Range")

lrLine = ta.linreg(close, lrLineInput, 0)
lrMA   = ta.sma(lrLine, lrMAInput)
ema     = ta.ema(close, emaInput)

longEntry   = ema   < lrMA
longExit    = lrMA  < ema

shortEntry  = lrMA  < ema
shortExit   = ema   < lrMA


maxProfitLong   = strategy.opentrades.entry_price(0) * (1 + maxProfitInput)
maxProfitShort  = strategy.opentrades.entry_price(0) * (1 - maxProfitInput)

stopLossPriceShort  = strategy.position_avg_price * (1 + stopLossPercentageInput)
stopLossPriceLong   = strategy.position_avg_price * (1 - stopLossPercentageInput)

if(executeLongInput and bullish)
    strategy.entry( id="long_entry", direction=strategy.long,   when=longEntry and window(),    qty=10,  comment="long_entry")
    strategy.close( id="long_entry", when=longExit,     comment="long_exit")
    // strategy.close( id="long_entry", when=maxProfitLong <= close, comment="long_exit_mp")
    
if(executeShortInput and not bullish)
    strategy.entry( id="short_entry", direction=strategy.short,   when=shortEntry and window(),    qty=10,  comment="short_entry")
    strategy.close( id="short_entry", when=shortExit,     comment="short_exit")
    // strategy.close( id="short_entry", when=maxProfitShort <= close, comment="short_exit_mp")

if(strategy.position_size > 0 and executeStopLoss)
    strategy.exit(  id="long_entry",        stop=stopLossPriceLong,             comment="exit_long_SL")
    strategy.exit(  id="short_entry",       stop=stopLossPriceShort,            comment="exit_short_SL")
    
// plot(series=lrLine,     color=color.green)
plot(series=lrMA,       color=color.red)
plot(series=ema,        color=color.blue)

```

> Detail

https://www.fmz.com/strategy/430113

> Last Modified

2023-10-25 10:58:02
