
> Name

Momentum-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/cbc31164b6ab705b657003a8f8e25f0998bf5f5813ce4bbf185b901cf884b269.png)
[trans]

### Overview
This strategy is based on momentum indicators and combined with moving averages to achieve the purpose of tracking market trends. Going long when the price has a strong upward momentum and going short when the price has a strong downward momentum is a trend following strategy.
### Strategy Principles
1. Calculate the momentum value of price, the formula is: (current price - price before N periods) / price before N periods
2. Calculate the moving average mid of the price, and the parameter is the N-period moving average.
3. Normalize the momentum value and map it to the 0-1 interval
4. Go long when the normalized momentum value is greater than 0.5 and the price is above the moving average.
5. Go short when the normalized momentum value is less than 0.5 and the price is below the moving average.
6. Adopt a trailing stop loss mechanism and set a reasonable stop loss position
The above is the basic trading logic of the strategy. When the market is trending, prices will rise and fall continuously, creating a large momentum value. The strategy will judge the strength of the trend based on the momentum value and decide to enter the market based on the direction of the moving average. In addition, stop loss setting is also very important to effectively control risks.
### Advantage Analysis
This strategy has the following advantages:
1. Track market trends and have greater profit potential
2. Momentum indicators are sensitive to price changes and can respond quickly to trends
3. The moving average filters out random fluctuations and works well when combined with the momentum indicator.
4. Adopting a stop-loss strategy can limit the losses of individual transactions.
5. The transaction logic is simple and clear, easy to implement and backtest
6. Parameters can be flexibly adjusted to adapt to different cycles and market environments.
Generally speaking, this is a strategy that is very suitable for tracking trending markets. In some markets with obvious direction, its profitability will be very strong.
### Risk Analysis
Despite its many advantages, this strategy also has some risks to be aware of:
1. In the long market, there is a risk of falling back again after breaking through the upper track, and the trailing stop may be killed instantly.
2. In the short market, there is a risk of rebounding after falling below the lower track, and there is also the possibility of being trapped by the trailing stop.
3. When the market fluctuates around the moving average, multiple unnecessary trading signals will be generated.
4. When parameters are set improperly, momentum values ​​and moving averages may send wrong signals.
5. This strategy relies more on trends and performs poorly in volatile sideways markets.
6. The stop loss ratio and movement range must be strictly controlled to prevent the stop loss from being too small or being breached too quickly.
To address these risks, it is necessary to optimize stop loss strategies, loosen parameters to filter out unnecessary signals, adjust parameters to suit different cycles, and control position size, etc.
### Optimization direction
This strategy also has the following points that can be further optimized:
1. You can test the impact of different parameters on the backtest results and select the best parameter combination
2. You can add the turtle trading rule, clear the position when the loss reaches 2N, and clear the position when the profit reaches 1N.
3. The stop loss position can be optimized in combination with the volatility indicator, and the stop loss range can be adjusted according to market volatility.
4. You can add a position management module to adjust the position size based on factors such as retracement and time.
5. You can experiment with different momentum calculation methods, such as the exponential smoothing moving average momentum indicator
6. You can add candlestick graphic filtering to filter some robust trading signals
7. You can try machine learning algorithms for parameter optimization, feature selection, etc.
8. Certain artificial experience can be introduced to assist strategic decision-making at key points.
Through the above methods, we can expect to further enhance the stability, adaptability and SUFFIX of the strategy. However, any optimization requires strict statistical verification to avoid over-optimization.
### Summarize
The momentum following strategy is a simple and practical trend strategy. It can keenly capture market trends and obtain huge profits while chasing ups and downs. However, we also need to pay attention to prevent the backtest curve from being too beautified, strictly control risks, and maintain the robustness of the strategy. Through optimization such as parameter tuning and function expansion, the strategy can achieve stable returns in more market environments.
||

### Overview

This strategy is based on momentum indicators combined with moving averages to track market trends. It goes long when there is strong upside momentum and goes short when there is strong downside momentum. It belongs to the category of trend following strategies.

### Strategy Logic

1. Calculate the momentum of price as: (Current Price - Price N periods ago) / Price N periods ago

2. Calculate the moving average mid of price over N periods

3. Normalize the momentum value to the range of 0-1

4. When the normalized momentum is greater than 0.5 and price is above moving average, go long

5. When the normalized momentum is less than 0.5 and price is below moving average, go short  

6. Use a moving stop loss mechanism with proper stop loss levels

The above covers the basic trading logic. When the market is trending, price will move persistently in one direction, generating large momentum values. The strategy judges the strength of the trend using the momentum and the direction using the moving average to decide on entry. Also, the stop loss is critical for controlling risks.

### Advantage Analysis 

This strategy has the following advantages:

1. Tracks market trends, with potentially large gains

2. Momentum is sensitive to price changes and responds quickly to trends

3. Moving averages filter out random noise and combine well with momentum

4. Stop loss mechanism limits loss on individual trades

5. Simple and clear logic, easy to implement and backtest

6. Flexible parameters can adapt to different periods and market regimes

Overall, this is a great strategy for trending markets. It can profit significantly from directional trends.

### Risk Analysis

Despite the advantages, some risks need to be noted:

1. Breakout risk in uptrends when price reverses after breaking out

2. Reversal risk in downtrends when price bounces after breaking down

3. Whipsaw signals when price oscillates around moving average

4. Wrong signals if parameters are not properly set

5. Underperforms in rangebound choppy markets  

6. Strict stop loss and movement required to prevent premature exit

To address these risks, stop loss strategy needs optimization, filter unnecessary signals with loose parameters, adjust parameters for different periods, and control position sizing.

### Optimization Directions

Here are some ways the strategy can be further optimized:

1. Test different parameter combinations for best backtest results

2. Incorporate the Turtle Trading rules of exiting at 2N loss and 1N profit

3. Optimize stop loss with volatility indicators for adaptive stop loss

4. Add position sizing rules based on drawdown, time, etc

5. Test different momentum calculation methods like exponential moving average momentum

6. Add candlestick pattern filters for more robust signals

7. Utilize machine learning for parameter optimization, feature selection, etc

8. Incorporate some discretionary human input at key points

With these enhancements, the strategy may achieve better stability, adaptability, and profitability. But any optimization needs strict statistical validation to avoid overfitting. 

### Conclusion

The momentum tracking strategy is a simple and practical trend following approach. It can nimbly capture market trends and profit from riding bubbles and crashes. But curve fitting risks need to be managed with disciplined risk controls to maintain robustness. With parameter tuning and functionality extensions, the strategy can yield steady profits in more market regimes.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|src: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|20|lookback|
|v_input_3|0|Bar color scheme: 1|2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-02 00:00:00
end: 2023-11-09 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Momentum Strategy, rev.2", overlay=true)

//
// Data
//
src = input(close)
lookback = input(20)
cscheme=input(1, title="Bar color scheme", options=[1,2])

//
// Functions
//
momentum(ts, p) => (ts - ts[p]) / ts[p]

normalize(src, len) =>
    hi  = highest(src, len)
    lo  = lowest(src, len)
    res = (src - lo)/(hi - lo)

//
// Main
//
price = close
mid = sma(src, lookback)
mom = normalize(momentum(price, lookback),100)

//
// Bar Colors
//
clr1 = cscheme==1?black: red
clr2 = cscheme==1?white: green
barcolor(close < open ? clr1 : clr2)

//
// Strategy
//
if (mom > .5 and price > mid )
    strategy.entry("MomLE", strategy.long, stop=high+syminfo.mintick, comment="MomLE")
else
    strategy.cancel("MomLE")

if (mom < .5 and price < mid )
    strategy.entry("MomSE", strategy.short, stop=low-syminfo.mintick, comment="MomSE")
else
    strategy.cancel("MomSE")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/431672

> Last Modified

2023-11-10 12:12:44
