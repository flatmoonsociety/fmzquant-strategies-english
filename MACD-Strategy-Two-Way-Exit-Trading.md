
> Name

Oscillator Trading Indicator Strategy MACD-Strategy-Two-Way-Exit-Trading
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b40a5649698bbeb882.png)
[trans]

### Overview
This strategy uses the moving average indicator (MACD) to construct long and short signals, conducts reversal transactions under good trend conditions, and obtains profits by dynamically setting exit positions.
### Strategy Principles
This strategy is mainly based on the golden cross long signal and the dead cross short signal of the MACD indicator. Specifically, when the MACD line crosses the signal line from bottom to top, a golden cross long signal is generated; when the MACD line crosses the signal line from top to bottom, a dead cross short signal is generated.
When the golden cross signal comes, if the closing price is higher than the EMA moving average, go long; when the dead cross signal comes, if the closing price is lower than the EMA moving average, go short. This ensures reversal trading under the general trend.
After entering the market, the strategy uses stop loss and take profit levels to dynamically take profit and stop loss. Specifically, the stop-loss position for long orders is set to the entry price*(1-maximum decline); the stop-profit position is set to the entry price*(1+TARGET_STOP_RATIO*maximum decline). The short order settings are opposite. The maximum drop is dynamically calculated, indicating the percentage drop space from swing low to the closing price; TARGET_STOP_RATIO defaults to 2, which means the profit-loss ratio is 2.
The advantage of setting the exit position in this way is that the profit-loss ratio and stop-loss position can be dynamically adjusted according to market fluctuations. Leave the market quickly to stop losses in large fluctuations, and track and take profits in small fluctuations.
### Strategic Advantages
1. Using the MACD indicator to construct long and short signals can effectively determine the timing of price reversal.
2. Use EMA as a filter and choose an upward trend when entering the market to avoid counter-trend trading.
3. The dynamic exit control system can adjust the profit-loss ratio and stop-loss point in real time to pursue high profits while controlling risks.
4. Due to the consideration of market fluctuations, the exit speed is fast, which can reduce the market-marking time and is more suitable for busy investors.

### Strategic risks and solutions
1. The MACD indicator frequently causes false signals in sideways markets. The solution is to add the moving average as a filter to avoid trading against the trend.
2. In extremely volatile markets, DYNAMIC STOP will cause too loose a stop loss, but it performs well in most scenarios. If you encounter extreme market conditions, you can consider a fixed profit-loss ratio.
3. The profit margin is limited and frequent transactions are required to pursue profits. This requires investors to have a certain amount of psychological endurance and time investment. If you have no time to operate, you can consider adjusting to a high cycle.

### Optimization direction
1. According to the characteristics of specific varieties, adjust MACD parameters to optimize the trading effect of golden cross and dead cross.
2. Test different moving averages as trend judgment indicators to find better filters.
3. Test the TARGET_STOP_RATIO and maximum drop calculation methods, and optimize the stop-profit and stop-loss strategies.
4. Add other conditional judgments, such as changes in trading volume, volatility, etc., to improve signal quality.
5. Try machine learning algorithms to extract more features, establish a dynamic multi-factor model, and achieve more intelligent stop-profit and stop-loss.

### Summarize
This strategy overall has strong practicality. Taking MACD as the core trading signal and adding two auxiliary modules such as trend judgment and dynamic exit control can significantly improve the trading effect of MACD itself. The stop-profit and stop-loss strategy is the key direction of strategy optimization. This strategy has made a lot of innovations in this aspect and is worthy of further research and application.

||

### Overview

This strategy uses the Moving Average Convergence Divergence (MACD) indicator to generate long and short signals and makes reversal trades under good trend conditions by dynamically setting exit points to capture profits.

### Strategy Principles 

The core of this strategy is based on the MACD golden cross for long signals and death cross for short signals. Specifically, when the MACD line crosses above the signal line from below, a golden cross is generated as a long signal; when the MACD line crosses below the signal line from above, a death cross is generated as a short signal.  

On golden cross signals, go long if the close price is above the EMA; on death cross signals, go short if the close price is below the EMA. This ensures reversal trades under an upward trend.

After entering positions, the strategy utilizes stop loss and take profit to dynamically control exits. Specifically, the stop loss for long positions is set at entry price * (1 - max drawdown); take profit is set at entry price * (1 + TARGET_STOP_RATIO * max drawdown). Vice versa for short positions. Here max drawdown is dynamically calculated as the percentage of price decline from swing low to close; TARGET_STOP_RATIO is default to 2, meaning a risk/reward ratio of 2.

The advantage of this dynamic stop strategy is that it can adjust stop loss and risk/reward ratio based on market volatility. It exits fast with a tight stop loss during high volatility while tracks profit with loose stop during low volatility environments. 

### Advantages

1. MACD is an effective indicator for identifying reversal opportunities.

2. The EMA filter ensures long trades happen only in an upward trend market. 

3. The dynamic exit control system maximizes profit while effectively manages risk.

4. Fast exist speed reduces required monitoring time, making it suitable for busy investors.

### Risks and Solutions

1. MACD oscillates frequently during sideways markets, generating fake signals. This is solved by adding EMA filter to avoid counter-trend trades.  

2. Extreme volatility can cause DYNAMIC STOP to be too loose. Consider fixed risk/reward ratio when facing extreme market moves.

3. Limited profit margin per trade requires frequent trading. Investors need certain psychological endurance and time commitment. Can switch to higher time frames if too busy.

### Optimization Directions 

1. Fine tune MACD parameters based on symbol characteristics to optimize signal quality.  

2. Test different moving averages as trend filter to find the optimal one. 

3. Test TARGET_STOP_RATIO calculation and max drawdown definition to optimize the exit strategy.  

4. Add other factors like volume, volatility etc. to improve signal quality.  

5. Explore machine learning models to extract more features and build adaptive multifactor models for smarter exits.  

### Conclusion
This strategy has strong practical value overall. With MACD as core trading signal, the add-on modules of trend filter and dynamic exit control can significantly improve MACD performance itself. Exit control is essential for strategy optimization and this strategy innovates substantially in this area. Well worth further research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|Risk/Reward|
|v_input_float_2|2|Risk per Trade %|
|v_input_bool_1|true|(?Backtest Time Period)Filter Date Range of Backtest|
|v_input_2|timestamp(5 June 2022)|Start Date|
|v_input_3|timestamp(5 July 2022)|End Date|
|v_input_int_1|200|(?EMA)Length|
|v_input_int_2|7|(?number of past candles)Swing High|
|v_input_int_3|7|Swing Low|
|v_input_4|12|(?MACD)Fast Length|
|v_input_5|26|Slow Length|
|v_input_int_4|9|Signal Smoothing|
|v_input_string_1|0|Oscillator MA Type: EMA|SMA|
|v_input_string_2|0|Signal Line MA Type: EMA|SMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-05 00:00:00
end: 2023-12-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © maxencetajet

//@version=5
strategy("MACD Strategy", overlay=true, initial_capital=1000, slippage=25)

src = input(title="Source", defval=close)
target_stop_ratio = input.float(title='Risk/Reward', defval=2, minval=0.5, maxval=100)
risk = input.float(2, title="Risk per Trade %")

riskt = risk / 100 + 1

useDateFilter = input.bool(true, title="Filter Date Range of Backtest",
     group="Backtest Time Period")
backtestStartDate = input(timestamp("5 June 2022"), 
     title="Start Date", group="Backtest Time Period",
     tooltip="This start date is in the time zone of the exchange " + 
     "where the chart's instrument trades. It doesn't use the time " + 
     "zone of the chart or of your computer.")
backtestEndDate = input(timestamp("5 July 2022"),
     title="End Date", group="Backtest Time Period",
     tooltip="This end date is in the time zone of the exchange " + 
     "where the chart's instrument trades. It doesn't use the time " + 
     "zone of the chart or of your computer.")

inTradeWindow =  true
emaV = input.int(200, title="Length", group="EMA")
swingHighV = input.int(7, title="Swing High", group="number of past candles")
swingLowV = input.int(7, title="Swing Low", group="number of past candles")

ema = ta.ema(src, emaV)

fast_length = input(title="Fast Length", defval=12, group="MACD")
slow_length = input(title="Slow Length", defval=26, group="MACD")
signal_length = input.int(title="Signal Smoothing",  minval = 1, maxval = 50, defval = 9, group="MACD")
sma_source = input.string(title="Oscillator MA Type",  defval="EMA", options=["SMA", "EMA"], group="MACD")
sma_signal = input.string(title="Signal Line MA Type", defval="EMA", options=["SMA", "EMA"], group="MACD")

fast_ma = sma_source == "SMA" ? ta.sma(src, fast_length) : ta.ema(src, fast_length)
slow_ma = sma_source == "SMA" ? ta.sma(src, slow_length) : ta.ema(src, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal == "SMA" ? ta.sma(macd, signal_length) : ta.ema(macd, signal_length)
hist = macd - signal

longcondition = close > ema and ta.crossover(macd, signal) and macd < 0
shortcondition = close < ema and ta.crossunder(macd, signal) and macd > 0

float risk_long = na
float risk_short = na
float stopLoss = na
float takeProfit = na
float entry_price = na

risk_long := risk_long[1]
risk_short := risk_short[1]

swingHigh = ta.highest(high, swingHighV)
swingLow = ta.lowest(low, swingLowV)

lotB = (strategy.equity*riskt-strategy.equity)/(close - swingLow)
lotS = (strategy.equity*riskt-strategy.equity)/(swingHigh - close)

if strategy.position_size == 0 and longcondition and inTradeWindow
    risk_long := (close - swingLow) / close
    strategy.entry("long", strategy.long, qty=lotB)
    
if strategy.position_size == 0 and shortcondition and inTradeWindow
    risk_short := (swingHigh - close) / close  
    strategy.entry("short", strategy.short, qty=lotS)

if strategy.position_size > 0

    stopLoss := strategy.position_avg_price * (1 - risk_long)
    takeProfit := strategy.position_avg_price * (1 + target_stop_ratio * risk_long)
    entry_price := strategy.position_avg_price
    strategy.exit("long exit", "long", stop = stopLoss, limit = takeProfit)
    
if strategy.position_size < 0

    stopLoss := strategy.position_avg_price * (1 + risk_short)
    takeProfit := strategy.position_avg_price * (1 - target_stop_ratio * risk_short)
    entry_price := strategy.position_avg_price
    strategy.exit("short exit", "short", stop = stopLoss, limit = takeProfit)
    
plot(ema, color=color.white, linewidth=2, title="EMA")
p_ep = plot(entry_price, color=color.new(color.white, 0), linewidth=2, style=plot.style_linebr, title='entry price')
p_sl = plot(stopLoss, color=color.new(color.red, 0), linewidth=2, style=plot.style_linebr, title='stopLoss')
p_tp = plot(takeProfit, color=color.new(color.green, 0), linewidth=2, style=plot.style_linebr, title='takeProfit')
fill(p_sl, p_ep, color.new(color.red, transp=85))
fill(p_tp, p_ep, color.new(color.green, transp=85))


```

> Detail

https://www.fmz.com/strategy/435106

> Last Modified

2023-12-12 12:44:50
