
> Name

Elevated-Touch-Short-Triangle-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1dcfd6a06c0e8ed2eb7.png)
[trans]

### Overview
This strategy is a breakout trading strategy based on the EMA indicator. When the price breaks through the EMA, it is regarded as an entry signal. A triangle stop-loss method is used to set the stop-loss and take-profit levels, which has a high possibility of profit.
### Strategy Principles
This strategy calculates the 5-day EMA as an indicator, and when the closing price touches the 5-day EMA from above, it is used as a short-selling signal; then the entry price is set to the high point of the signal generation bar, the stop-loss position is the highest point of the previous K line, and the take-profit position is 3 times the entry price minus the risk value (assuming that the take-profit and stop-loss ratio is 2:1). In this way, when the price breaks through the EMA downward, we go short; if the price rises again, the stop loss point can control the loss within a certain range; and the triangle take profit can obtain a better risk-reward ratio.
### Advantage Analysis
This is a simpler strategy to break through the EMA, with the following advantages:
1. The rules are simple, clear and easy to implement;
2. EMA can well describe the price trend, and it is easy to make profits by using breakthrough signals;
3. Using triangle stop-profit and stop-loss, you can get a higher profit-loss ratio;
4. Visual stop-loss and stop-profit levels help risk control.
### Risk Analysis
There are also some risks with this strategy:
1. The market suddenly undergoes huge changes, and stop loss may not be effective;
2. The EMA indicator lags behind and you may miss the best entry opportunity;
3. The triangle set may be stuck and unable to stop the loss.
In order to control risks, you can combine other indicators to determine the general trend and avoid counter-trend trading; you can also adjust the stop loss range according to the degree of market volatility.
### Optimization direction
This is a relatively simple strategy, and it can be optimized in the following directions:
1. Optimize EMA cycle parameters to adapt to different cycles;
2. Add other indicator judgments to improve strategy stability;
3. Adopt dynamic stop loss method and adjust the stop loss range according to the degree of market fluctuation;
4. Combine trading volume and other indicators to avoid false breakthroughs.
### Summarize
The overall strategy is a simple and practical short-term breakthrough EMA strategy. It has the advantages of clear rules, easy implementation, complete stop-profit and stop-loss, etc., and can obtain a better risk-reward ratio. But there are also issues such as the risk of being trapped. Subsequent optimization can be done by adjusting parameters, adding indicators, dynamic stop loss, etc. to make the strategy more stable and reliable.
||

### Overview  

This is a breakout trading strategy based on the EMA indicator. When the price breaks through the EMA, it is considered as an entry signal. It adopts triangle stop loss to set the stop loss and take profit, with high profit potential.  

### Principles

The strategy calculates the 5-day EMA as an indicator. When the close price touches the 5-day EMA from above, it is a signal for going short. Then the entry price is set to the high of the signal bar, the stop loss is set to the highest point of the previous bar, and the take profit is set to the entry price minus 3 times the risk value (assuming a 2:1 risk-reward ratio for TP calculation). So when the price breaks through the EMA downward, we go short; if the price rebounds again, the stop loss point can keep the loss within a certain range; and the triangle take profit can achieve a good risk-reward ratio.

### Advantages

This is a relatively simple breakout EMA strategy with the following strengths:
1. Simple and clear rules, easy to implement;  
2. EMA depicts price trends well, easy to profit from breakout signals;
3. Triangle stop loss for better risk-reward ratio; 
4. Visual SL and TP for better risk control.

### Risks 

The strategy also has some risks:
1. Sudden huge market change may make SL invalid;
2. EMA lag may miss best entry point; 
3. Triangle trap.  

To control risks, we can combine other indicators to determine the major trend, avoid trading against trends; we can also adjust the stop loss range based on market volatility.

### Improvements

This is a simple strategy, and can be improved in the following aspects:
1. Optimize EMA parameters for different cycles;
2. Add other indicators to improve stability; 
3. Adopt dynamic SL based on market volatility;  
4. Combine trading volumes to avoid false breakout.   

### Conclusion   

In summary, this is a simple and practical short-term EMA breakout strategy. It has advantages like clear rules, easy to implement, complete SL and TP. But it also has risks like being trapped. Going forward it can be improved by adjusting parameters, adding indicators, dynamic stops etc., to make the strategy more stable and reliable.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|5|EMA Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-30 00:00:00
end: 2024-02-29 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Short Entry EMA Strategy with Visual SL and TP", shorttitle="SE-EMA-SL-TP-Viz", overlay=true)

// Customization Inputs
emaPeriod = input.int(5, title="EMA Period", minval=1)

// EMA Calculation
emaValue = ta.ema(close, emaPeriod)
plot(emaValue, title="5 EMA", color=color.blue)

// Detecting Short Entry Conditions
shortEntryCondition = close > emaValue and low <= emaValue and low[1] > emaValue[1] and close[1] > emaValue[1]

// Entry, SL, and TP Logic
if (shortEntryCondition)
    entryPrice = open[1]
    slLevel = high[1]
    risk = slLevel - entryPrice
    tpLevel = entryPrice - risk * 3  // Assuming a 2:1 risk-reward ratio for TP calculation

    // Execute short trade
    strategy.entry("Short", strategy.short)
    strategy.exit("Exit", "Short", stop=slLevel, limit=tpLevel)

    // Visualizing SL and TP levels
    // line.new(bar_index, slLevel, bar_index + 20, slLevel, color=color.red, width=2)
    // line.new(bar_index, tpLevel, bar_index + 20, tpLevel, color=color.green, width=2)

// Plotting Short Entry Signal
plotshape(series=shortEntryCondition, style=shape.triangledown, location=location.abovebar, color=color.red, title="Short Signal")

```

> Detail

https://www.fmz.com/strategy/443231

> Last Modified

2024-03-01 11:02:49
