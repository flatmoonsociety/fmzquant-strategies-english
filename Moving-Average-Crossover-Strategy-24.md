
> Name

Moving Average Golden Cross and Dead Cross Trend Following Strategy Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14ae8a20deb3418743a.png)

[trans]

### 

This strategy uses the moving average crossover of the 20-day line and the 60-day line to form a buy and sell signal. When the price rises and breaks through the 20-day line, go long; when the price falls and breaks through the 20-day line, close the position. In the same way, a buy and sell signal is also formed when the price breaks through the 60-day line. This strategy is a typical trend following strategy.
### Strategy Principles
1. Calculate the 20-day simple moving average and the 60-day simple moving average
2. When the closing price rises and breaks through the 20-day line, go long
3. When the closing price falls and breaks through the 20-day line, close the position
4. When the closing price rises and breaks through the 60-day line, go long
5. When the closing price falls and breaks through the 60-day line, close the position
The above form the trading signals and rules of this strategy. When the price breaks through the average line, it indicates that the trend has begun, and you can follow the trend to go long; when the price falls below the average line, it indicates that the trend has ended, and closing the position is the right choice at this time.
### Strategic Advantages
1. Use a combination of double moving averages to make the strategy more stable. The 20-day line can capture short-term trend opportunities more quickly; the 60-day line filters out some short-term market noise and locks in mid- to long-term trends.  
2. The strategy backtest started in 2018, and the Taiwan stock market was chosen. Compared with mainland A-shares, the trading system of Taiwan stocks is more complete and can better reflect the strategy effect.
3. Set up reasonable stop loss and position control to control risks to the greatest extent.
### Strategy Risk
1. The strategy is only based on the moving average indicator. When the market does not have an obvious trend, it will produce more Whirlaway and spread.
2. The strategy does not optimize the buying/selling quantity and positions, and cannot maximize the use of funds.
3. This strategy responds symmetrically to price increases and decreases and cannot respond to different market conditions.
Risk resolution:
1. You can add other indicator combinations, such as KDJ, MACD, etc., to form multiple verifications and avoid mistaken transactions.  
2. The utilization efficiency of positions and trading funds can be optimized based on market value, volatility and other factors.
3. Asymmetric operations can be adopted according to different stages of the market index, reducing transactions during shock adjustments and increasing positions during clear trends.
### Strategy optimization direction
1. Optimize the buying and selling quantities. The position quantity can be dynamically adjusted based on stop loss information.
2. Optimize the days parameter of the moving average. Step optimization, stochastic optimization and other methods can be used to find better parameters.  
3. Add a stop loss strategy. Trailing stop loss or pending order stop loss can better protect profits.
4. Increase position management. Dynamically adjust the position of a single transaction according to the size of funds and market value.
### Summarize
This strategy as a whole is a typical double moving average crossover strategy. The core idea is to follow the trend and establish a trend position when the price breaks through the average line. The strategy is simple, practical and easy to implement. At the same time, there is also some room for optimization. Through parameter optimization, stop loss avoidance, position management and other means, better strategic effects can be obtained.
||

This strategy adopts the crossover of 20-day moving average and 60-day moving average to generate trading signals. It goes long when price breaks above 20-day MA and closes position when price breaks below 20-day MA. Similarly, it forms trading signals when price crosses 60-day MA. This strategy belongs to a typical trend following system.  

### Strategy Logic

1. Calculate 20-day simple moving average and 60-day simple moving average  
2. Go long when closing price breaks above 20-day MA
3. Close position when closing price breaks below 20-day MA 
4. Go long when closing price breaks above 60-day MA
5. Close position when closing price breaks below 60-day MA

The above rules define the trading signals and logic for this strategy. When price crosses over the MA line, it shows a new trend is emerging and we can follow the trend to go long. When price drops below the MA line, it shows the trend is ending so we close position.  

### Advantages

1. Adopting double MAs makes the strategy more steady. The 20-day MA captures short-term opportunities faster while the 60-day MA filters out some market noises and locks in medium-long term trend.
2. The backtest starts from 2018 and selects Taiwan stock market, which has more developed trading system compared to China A-share market, better reflecting the strategy efficacy. 
3. It sets proper stop loss and position sizing, maximally controlling the risk.

### Risks

1. The strategy solely relies on MA indicator. It may generate more whipsaws when there is no obvious trend in the market.
2. The strategy does not optimize the buy/sell size and position, failing to maximize the capital usage.  
3. The strategy reacts symmetrically to price ups and downs, unable to adapt to different market conditions.

Risk Solutions:
1. Add other indicators like KDJ, MACD to form multiple confirmation, avoiding wrong trades.
2. Optimize position sizing and capital usage efficiency according to market cap, volatility etc. 
3. Adopt asymmetric moves based on market stages, reduce trading during range-bound market and increase position size during obvious trend.
 

### Optimization Directions 

1. Optimize buy/sell quantity. Dynamically adjust position size based on stop loss.
2. Optimize MA parameters. Find better parameters through walk forward optimization and random optimization.
3. Add stop loss strategy. Moving stop loss or stop limit order better protects profits. 
4. Add position sizing management. Dynamically adjust position size per trade based on capital size, market cap etc.

### Summary

This is a typical dual moving average crossover strategy. The core idea is to follow trends by establishing position when price crosses over MA line. The strategy is simple and practical to implement. Meanwhile, there is room for further optimization, by parameter tuning, stop loss, position sizing etc. to achieve better results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2018|backtest_year|
|v_input_int_1|true|backtest_month|
|v_input_int_2|true|backtest_day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-01 00:00:00
end: 2023-12-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Astorhsu

//@version=5
strategy("Astor SMA20/60 TW", overlay=true, margin_long=100, margin_short=100)
backtest_year = input(2018, title='backtest_year') //回測開始年分
backtest_month = input.int(01, title='backtest_month', minval=1, maxval=12) //回測開始月份
backtest_day = input.int(01, title='backtest_day', minval=1, maxval=31)  //回測開始日期
start_time = timestamp(backtest_year, backtest_month, backtest_day, 00, 00)  //回測開始的時間函數

//Indicators
sma20 = ta.sma(close,20)
sma60 = ta.sma(close,60)
plot(sma20, color=color.green, title="sma(20)")
plot(sma60, color=color.red, title="sma(60)")

//進場條件
longCondition = ta.crossover(close, ta.sma(close, 20))
if (longCondition) and time >= start_time
    strategy.entry("open long20", strategy.long, qty=1, comment="站上m20做多")


shortCondition = ta.crossunder(close, ta.sma(close, 20))
if (shortCondition) and time >= start_time
    strategy.close("open long20",comment="跌破m20平倉", qty=1)     
    
longCondition1 = ta.crossover(close, ta.sma(close, 60))
if (longCondition1) and time >= start_time
    strategy.entry("open long60", strategy.long, qty=1, comment="站上m60做多")


shortCondition1 = ta.crossunder(close, ta.sma(close, 60))
if (shortCondition1) and time >= start_time
    strategy.close("open long60",comment="跌破m60平倉", qty=1)     
```

> Detail

https://www.fmz.com/strategy/434701

> Last Modified

2023-12-08 15:23:33
