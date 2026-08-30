
> Name

Moving-Average-Crossover-Strategy based on different period moving average crossover strategies
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/0b18e1f10d053052609d1593457088fff4003e34af05fe18591efd3805ca2a47.png)
[trans]

### Overview
This strategy generates trading signals by calculating moving averages of two different periods and plotting their intersection points. When the short-term moving average crosses the long-term moving average, go long; when the short-term moving average crosses below the long-term moving average, go short.
### Strategy Principles
This strategy is based on the advantages of the moving average - it can remove the randomness in the price sequence and extract the main trend. The strategy uses the 7-day line and the 20-day line to construct a double moving average system. These two periods are more commonly used and clear.
When the short-term moving average crosses the long-term moving average, it means that the price has entered an upward trend; when the short-term moving average crosses below the long-term moving average, it means that the price has entered a downward trend. Based on this principle, we buy long or sell short.
Specifically, the strategy calculates the 7-day simple moving average and the 20-day simple moving average. When the two average lines cross, it determines the trend turning point and sends a trading signal. In order to distinguish the crossover types, it is defined that the short-term line is greater than the long-term line as a price upward trend, and vice versa as a price downward trend. When the short-term line crosses the long-term line, that is, when the price upward trend begins, enter the market with a long position; when the short-term line crosses below the long-term line, that is, when the price decline trend begins, enter the market with a short position.
### Advantage Analysis
(1) The strategic ideas are clear and simple, easy to understand and implement.
(2) As a trend tracking indicator, the moving average can effectively filter out some of the noise contained in the price. The use of a double moving average system can further improve stability.
(3) The parameter configuration is flexible and the parameter combination of the cycle can be adjusted to meet the trading requirements of different market environments.
(4) Using the two more commonly used moving average periods, it is easy to judge clear trading signals.
(5) Visual auxiliary analysis is relatively powerful, and trends, important points, etc. can be intuitively judged through visual effects.
(6) After the strategy is backtested, parameters can be adjusted based on the optimization results to improve the strategy’s return rate.
### Risk Analysis
(1) The double moving average strategy is more sensitive to market fluctuations and is prone to frequent trading losses in volatile markets.
(2) Relying only on moving average crossovers may not accurately determine the turning point of the trend, and may cause false signals.
(3) The rules are relatively rigid. When emergencies affect the market, the strategy cannot be adjusted and may cause large losses.
(4) Improper parameters can also cause false signals or missed trading opportunities, and careful testing and optimization are required.
In order to mitigate these risks, the parameter combination can be appropriately adjusted; other indicators can be added for assistance; stop-loss strategies can be set to control losses; parameters can be adjusted or strategies closed according to the market environment, etc.
### Optimization direction
(1) Combined with other technical indicators to form a combination strategy, the accuracy of the signal can be improved. For example, adding a trading volume indicator to determine the amplification of trading volume when the moving average crosses can increase the Entry chance.
(2) Adding a stop-loss strategy can effectively control single losses. For example, when the price breaks through a certain range of the moving average, exit the current Head position.
(3) Test the period parameter combination of optimized moving average. You can try different fast and slow cycle matching to find the best parameter combination. In addition, you can also test the use of other moving average indicators such as exponential moving averages and weighted moving averages.
(4) Carry out parameter tuning according to different varieties and market environments. For products with high volatility, the moving average period can be shortened and the frequency of transactions can be reduced. For market environments with strong trends, the time span gap between the two moving averages can be increased.
### Summarize
The moving average double crossover strategy is overall a very typical and basic trend following strategy. It determines changes in price trends by calculating moving averages for two different periods and observing their intersections. A trading signal is generated when the short-term moving average crosses above or below the long-term moving average. This simple trading idea is easy to implement and has flexible parameter adjustment. It is an entry-level strategy for quantitative trading. However, there are also some shortcomings, such as being sensitive to fluctuations in the market environment and the signals may be inaccurate. By combining it with other technical indicators or setting stop losses and parameter optimization, this strategy can be strengthened and become a very practical quantitative trading strategy.
||

### Overview  

The strategy generates trading signals by calculating two moving averages of different periods and plotting their crossover points. It goes long when the shorter-term moving average crosses above the longer-term moving average, and goes short when the shorter-term moving average crosses below the longer-term moving average.

### Strategy Logic  

The strategy is based on the advantage of moving averages - they eliminate the randomness in price sequences and extract the main trend. The strategy employs a dual moving average system consisting of 7-day and 20-day lines, two commonly used and quite definitive periods.  

When the shorter-term moving average crosses above the longer-term moving average, it signals that prices are entering an uptrend. When it crosses below, it signals prices are entering a downtrend. According to this logic, we go long or short respectively.  

Specifically, the strategy calculates the 7-day simple moving average (SMA) and 20-day simple moving average. When the two averages cross, it judges a trend reversal and triggers a trade signal. To differentiate between crossover types, we define the short term line being above the long term line as an upward price trend, and vice versa for a downward trend. When the short term line crosses above the long term line, i.e. the onset of an upward trend, a long position is entered. When the short term line crosses below, i.e. the onset of a downward trend, a short position is entered.

### Advantage Analysis   

(1) The strategy logic is simple and easy to understand and implement.  

(2) Moving averages as trend tracking indicators can effectively filter out some noise in prices. The dual moving average system further enhances stability.

(3) Flexible parameter configurations to meet different market conditions and trading requirements.  

(4) Use of two commonly used moving average periods makes it easy to determine clear trading signals.
   
(5) Powerful visualization for intuitive trend, key levels identification etc.
   
(6) Parameters can be optimized via backtesting to improve strategy return.

### Risk Analysis  

(1) The strategy is quite sensitive to market fluctuation. Whipsaws can lead to frequent losses in ranging periods.  

(2) Crossovers may not accurately pinpoint trend reversal levels and could trigger wrong signals.

(3) Rigid rules cannot adapt to drastic events affecting markets, potentially causing huge losses.  

(4) Improper parameters could also lead to inaccurate signals and missed trades. Careful testing is needed.

To mitigate these risks, parameters could be adjusted accordingly. Other indicators can be added for confirmation. Stop loss strategies could control losses. Parameters or strategies could be adjusted per market regimes.  

### Enhancement Directions

(1) Incorporating other technical indicators to form a combined strategy could increase signal accuracy. E.g. adding volume to confirm expansion on moving average crossover.  

(2) Adding stop loss strategies to effectively control single trade loss. E.g. exiting positions if prices breach moving averages by some threshold.

(3) Testing and optimizing moving average periods. Trying different fast and slow combinations to find best parameters. Other moving averages like EMA, WMA can also be tested.  

(4) Parameter tuning based on different products and market conditions. Using shorter moving averages and smaller cross-term difference for more volatile products. 

### Conclusion  

The moving average crossover strategy is a very typical and basic trend following strategy. By calculating two moving averages of different periods and observing their crossovers, it judges changes in price trend. Trading signals are generated when the shorter period moving average crosses above or below the longer one. This simple logic is easy to implement and flexible to adjust, making it an introductory quant strategy. But it also has defects like sensitivity to market fluctuations and potential inaccurate signals. By combining with other indicators, adding stops, and parameter optimization, the strategy can be enhanced into a very practical one for quantitative trading.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Price Source For The Moving Averages: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|true|Use Current Timeframe As Resolution?|
|v_input_3|W|Use Different Timeframe? Then Uncheck The Box Above|
|v_input_4|7|Short Period Moving Average|
|v_input_5|20|Long Period Moving Average|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-01 00:00:00
end: 2023-12-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Ma stratégie", overlay=true)

// Multi-timeframe and price input
pricetype = input(close, title="Price Source For The Moving Averages")
useCurrentRes = input(true, title="Use Current Timeframe As Resolution?")
resCustom = input(title="Use Different Timeframe? Then Uncheck The Box Above",  defval="W")
res = useCurrentRes ? timeframe.period : resCustom
price = request.security(syminfo.tickerid, res, pricetype)

// MA period input
shortperiod = input(7, title="Short Period Moving Average")
longperiod = input(20, title="Long Period Moving Average")



short = ema(price, shortperiod) 
long = ema(price, longperiod) 
   
// MA trend direction color
shortcolor = short > short[1] ? lime : short < short[1] ? red : blue
longcolor = long > long[1] ? lime : long < long[1] ? red : blue

// MA output
MA1 = plot(short, title="Short Period Moving Average", style=linebr, linewidth=2, color=shortcolor)
MA2 = plot(long, title="Long Period Moving Average", style=linebr, linewidth=4, color=longcolor)
fill(MA1, MA2, color=silver, transp=50)

// MA trend bar color
TrendingUp() => short > long 
TrendingDown() => short < long 
barcolor(TrendingUp() ? green : TrendingDown() ? red : blue)

// MA cross alert
MAcrossing = cross(short, long) ? short : na
plot(MAcrossing, style = cross, linewidth = 4,color=black)

// MA cross background color alert
Uptrend() => TrendingUp() and TrendingDown()[1]
Downtrend() => TrendingDown() and TrendingUp()[1]
bgcolor(Uptrend() ? green : Downtrend() ? red : na,transp=50)

// Buy and sell alert
Buy = Uptrend() and close > close[1]
Sell = Downtrend() and close < close[1]
plotshape(Buy, color=black, style=shape.arrowup, text="Buy", location=location.bottom)
plotshape(Sell, color=black, style=shape.arrowdown, text="Sell", location=location.top)



if (Buy)
    strategy.entry("My Long Entry Id", strategy.long)


if (Sell)
    strategy.entry("My Short Entry Id", strategy.short)
```

> Detail

https://www.fmz.com/strategy/434691

> Last Modified

2023-12-08 12:20:42
