
> Name

Time-based-ATR-Stop-Loss-Buy-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d21064b565fc14ad9a.png)
[trans]

### Overview
The core idea of ​​this strategy is to combine time and ATR indicators to set buying timing and stop loss points. The strategy sends a timed buy signal at a specified time point, uses the closing price at that time as the buying price, and then uses the buying price plus the ATR value as the stop loss point. This can filter out some inappropriate buying opportunities and use ATR to control risks.
### Strategy Principles
This strategy mainly consists of the following parts:
1. Input parameters: including buying time timeTrade and ATR parameter atrLength. timeTrade determines the buying time, and atrLength determines the cycle parameters of ATR.
2. Calculate the ATR indicator: calculate the value of the ATR indicator atrValue based on the atrLength parameter.
3. Define the buy condition: a buy signal is generated when the combination of hours and minutes equals timeTrade.
4. Issue a buy order: go long when the buy conditions are met, and record the buy price buyprice.
5. Set the stop loss point: the stop loss point is the purchase price plus the ATR value. Stop loss and exit when the price breaks through the stop loss point.
6. Drawing: Draw stop-loss horizontal lines.
### Advantage Analysis
The biggest advantage of this strategy is to use time and ATR indicators to double confirm the buying timing and stop loss point. This avoids blindly following the market buying and effectively controls risks. Secondly, the stop loss point set by ATR changes dynamically, and a reasonable stop loss range can be set according to the degree of market volatility. Finally, the strategy logic is simple and easy to understand and track.
### Risk Analysis
This strategy mainly has the following risks:
1. If the buying time is not set properly, you may miss a better buying opportunity or buy in an unsatisfactory market.
2. Improper setting of ATR parameters and too large or too small stop loss point will affect the strategy effect.
3. It cannot effectively track long-term trends and is more suitable for short-term operations.
4. Failure to consider fundamental analysis factors.
### Optimization direction
This strategy can be further optimized from the following aspects:
1. Combine with multi-factor model to determine a more scientific buying time.
2. Optimize ATR parameter settings based on the volatility model.
3. Add a trend tracking mechanism to adapt to longer holding periods.
4. Integrate fundamental analysis to determine the rationality of the buying opportunity.
### Summarize
Overall, this strategy is a relatively simple and intuitive high-frequency intraday trading strategy. The core idea is to use the double confirmation of time and ATR indicators to lock in the buying opportunity and stop loss point. The advantage is that the risks are controllable and relatively easy to implement. However, there are also problems such as purchase timing selection and insufficient parameter optimization. In the future, further optimization can be carried out by introducing more factors, dynamic parameter optimization, trend tracking, etc.
||

### Overview  

The core idea of this strategy is to combine time and ATR indicators to set the buy-in timing and stop loss points. The strategy issues a timed buy signal at the specified time point, uses the closing price at that time as the purchase price, and then sets the stop loss point at the purchase price plus the ATR value. This can filter out some unsuitable buy-in timings while using ATR to control risks.

### Strategy Principle   

The strategy consists of the following main parts:  

1. Input parameters: including buy-in time timeTrade and ATR parameter atrLength. timeTrade determines the buy-in time, and atrLength determines the period parameter of ATR.

2. Calculate ATR indicator: calculate the ATR value atrValue based on the atrLength parameter.  

3. Define buy conditions: generate buy signals when the combination of hours and minutes equals timeTrade.  

4. Issue buy order: go long when the buy condition is met, and record the purchase price buyprice.

5. Set stop loss point: the stop loss point is set at purchase price plus ATR value. Stop loss exit when price breaks this point.  

6. Plotting: plot the stop loss level line.

### Advantage Analysis   

The biggest advantage of this strategy is the double confirmation of buy-in timing and stop loss point by time and ATR indicator. This avoids blindly following the market to buy in, and effectively controls risks. Secondly, the stop loss point set by ATR is dynamically changing, which can set a reasonable stop loss range according to market fluctuation. Finally, the strategy logic is simple and easy to understand and track.  

### Risk Analysis  

The main risks of this strategy include:  

1. Improper setting of buy-in time may miss better buy-in opportunities or buy in undesirable markets.  

2. Improper parameter settings of ATR will affect strategy performance if stop loss point is too large or too small.   

3. Unable to track long-term trends effectively, more suitable for short-term operations.  

4. Fundamental analysis factors are not considered.

### Optimization Directions   

This strategy can be further optimized in the following aspects:  

1. Determine a more scientific buy-in time by combining multi-factor models.  

2. Optimize ATR parameter settings by combining volatility models.  

3. Increase trend tracking mechanism to adapt to longer holding periods.   

4. Incorporate fundamental analysis to judge the reasonableness of buy-in timing.  

### Conclusion  

Overall, this is a relatively simple and intuitive high frequency intraday trading strategy. The core idea is to use the double confirmation of time and ATR indicators to determine the buy-in timing and stop loss points. The advantages are controllable risks and relatively easy to implement. But there are also problems like insufficient selection of buy-in timing and inadequate parameter optimization. Future optimizations can be made from introducing more factors, dynamic parameter optimization, trend tracking etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|700|(?Time Settings)Trade Execution Time (HHMM)|
|v_input_2|14|(?ATR Settings)ATR Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Time-based Strategy with ATR Take Profit", overlay=true)

// Initialize take profit levels
var float takeProfitLevel = na
var float takeProfitLevelForSell = na
var float buyprice = na
var float sellprice = na



// Input for the time when the trade should be executed
tradeTime = input(0700, "Trade Execution Time (HHMM)", "Specify the time in HHMM format", group="Time Settings")

// Calculate ATR for the last 5 minutes
atrLength = input(14, "ATR Length", "Specify ATR length", group="ATR Settings")
atrValue = request.security(syminfo.tickerid, "5", ta.atr(atrLength))

// Define conditions for buy and sell
buyCondition = hour * 100 + minute == tradeTime // and strategy.position_size == 0
sellCondition = hour * 100 + minute == tradeTime // and strategy.position_size > 0
// Execute Buy and Sell orders


if (buyCondition)
    strategy.entry("Buy", strategy.long)
    buyprice := close
    takeProfitLevel := buyprice + atrValue
strategy.exit("Take Profit BUY", from_entry="Buy", limit =takeProfitLevel) 
    

  

// if (sellCondition)
//     strategy.entry("Sell", strategy.short)
//     sellprice := close
//     takeProfitLevelForSell := sellprice -atrValue
// strategy.exit("Take Profit Sell", from_entry="Sell", limit=takeProfitLevelForSell)


// Plot horizontal lines for take profit levels


plot(takeProfitLevel, color=color.green, title="Take Profit Level (Buy)")
plot(takeProfitLevelForSell, color=color.red, title="Take Profit Level (Sell)")

```

> Detail

https://www.fmz.com/strategy/443038

> Last Modified

2024-02-28 17:36:50
