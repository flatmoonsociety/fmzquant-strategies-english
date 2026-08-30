
> Name

Trend-Following-Channel-Breakout-Strategy-with-Moving-Average-and-Trailing-Stop
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3a736596fbb53627e4aa523fc11c9757a0288b38f5a4ac58423d10d08519cc2c.png)

[trans]

### Overview
This strategy is a price channel-based breakout strategy that combines moving average indicators and trailing stop loss/take profit for entry and exit. It uses the moving average of high and low prices to construct a price channel, enters the market to go long/short when the price breaks through the channel, and uses fixed stop loss or trailing stop to control risks.
### Strategy Principles
This strategy forms a price channel by calculating the moving average of high and low prices. Specifically, the high-price and low-price SMA moving averages with a length of 10 are calculated to form the upper and lower rails of the Channel. When the price breaks through from the lower rail to the upper rail, enter the market with a long position; when the price breaks through from the upper rail rail with the lower rail, enter the market with a short position.
After entering the market, the strategy uses fixed stop loss or trailing stop to exit the position. Trailing stop includes two parameters: fixed profit level and activating offset. When the price reaches the activation offset, the take profit level will be trailed by the price. This locks in profits while maintaining margins.
This strategy also combines time period filtering and only performs backtesting within specified historical dates, allowing you to test the performance of different market stages.
### Advantage Analysis
This strategy uses price channel and trend tracking stop loss, which can capture the direction of medium and long-term trends. Compared with a simple moving average strategy, it reduces invalid transactions caused by price fluctuations. By trailing stop, you can dynamically trail the price to lock in profits.
Overall, this strategy has clear logic, uses fewer indicators and parameters, is easy to backtest, is suitable for medium and long-term trend trading, and can make profits in strong market conditions.
### Risk Analysis
This strategy is easy to be trapped and exited in volatile market conditions, and cannot make lasting profits. In addition, in extreme market conditions, the price may directly break through the stop loss level, causing large losses.
Parameter settings are relatively subjective, and parameters need to be adjusted at different market stages. The fixed take-profit level and activation offset cannot be adjusted according to the degree of market fluctuations.
### Optimization direction
You can consider combining other indicators to filter entry signals, such as trading volume, Bollinger Bands, etc., to avoid being trapped. Or use dynamic stop loss to set stop loss based on ATR or price fluctuation.
Exit rules can be optimized to Trailing Stop or Chandelier Exit. A partial exit can also be considered when price re-enters the channel. Optimization of entry filtering and exit rules can greatly improve strategy stability.
### Summarize
This strategy as a whole is a quantitative strategy based on price channel, trend tracking, and stop loss/take profit management. It has a clear logical structure and simple parameter structure, which is easy to understand and backtest, and is suitable for learning quantitative trading. This strategy can be optimized in a variety of ways to improve stability and profitability. The core idea is to capture the direction of the price trend and control risks through stop loss and take profit, which can be applied to a variety of varieties and time periods.
||

### Overview

This is a breakout strategy based on price Channel, combined with moving average indicators and trailing stop/take profit for entry and exit. It uses moving average of high/low prices to construct the price Channel, and enter long/short when price breaks out of the Channel, with fixed stop loss or trailing stop to control risks.

### Strategy Logic

The strategy calculates moving averages of high/low prices to form a price Channel. Specifically, it computes length 10 SMA of high/low prices to plot the upper and lower band of the Channel. When price breaks out above the lower band into the upper band, it enters long. When price breaks down from the upper band into the lower band, it enters short.  

After entry, the strategy uses either fixed stop loss or trailing stop for exit. The trailing stop consists of two parameters: fixed take profit level, and activating offset. When price reaches the activating offset, the take profit level starts to trail the price. This allows locking in profits while keeping some open space.

The strategy also combines time range filter, only running backtest within specified historical timeframe, to test performance across different market stages.

### Advantage Analysis

The strategy exploits price Channel and trend following with trailing stop, which allows it to capture mid-to-long term trend directions. Compared to simple moving average strategies, it avoids ineffective trades due to price fluctuations. With trailing stops, it can dynamically trail prices to lock in profits.

Overall, the strategy has clear logic, minimal indicators and parameters, easy to backtest, suitable for mid-to-long term trend trading, and can profit from strong trends. 

### Risk Analysis  

The strategy tends to get stopped out easily during ranging, choppy markets, unable to sustain profits. Also during extreme moves, price may break out the stop loss aggressively leading to large losses.

The parameter tuning is quite subjective, requiring adjustments across different market stages. The fixed take profit and activating offset fails to adapt to varying market volatility.

### Enhancement Opportunities

Other indicators such as volume, Bollinger Bands can be incorporated to filter entry signals, avoiding traps. Or dynamic stops can be used based on ATR or price volatility.

Exit rules may be upgraded to trailing stop or Chandelier Exit. Partial profit targets can be considered when price re-enters Channel. Optimizing entry filters and exit rules can greatly improve stability of the strategy.

### Conclusion

In summary, this is a quantitative strategy based on price Channel, trend following, stop loss/profit taking management. It has clear logic flow, simple parameter structure, easy to understand and backtest. It is suitable to learn algorithmic trading concepts. The strategy can be enhanced in various aspects to improve stability and profitability. The core idea is to capture trend direction, and manage risks via stop loss and take profit. It can be applied to various products over different timeframes.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Lb|
|v_input_2|0|MA Type: SMA|EMA|HMA|McG|WMA|Tenkan|
|v_input_3|300|SL Activation|
|v_input_4|true|SL Trigger|
|v_input_5|150|TP Activation|
|v_input_6|true|TP Trigger|
|v_input_7|true|From Month|
|v_input_8|true|From Day|
|v_input_9|2019|From Year|
|v_input_10|6|To Month|
|v_input_11|19|To Day|
|v_input_12|2020|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-21 23:59:59
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Generalized SSL Backtest w/ TSSL", shorttitle="GSSL Backtest", overlay=true )
// Generalized SSL:
//  This is the very first time the SSL indicator, whose acronym I ignore, is on Tradingview. 
//  It is based on moving averages of the highs and lows. 
//  Similar channel indicators can be found, whereas 
//  this one implements the persistency inside the channel, which is rather tricky.
//  The green line is the base line which decides entries and exits, possibly with trailing stops.
//  With respect to the original version, here one can play with different moving averages.
//  The default settings are (10,SMA)
//
// Vitelot/Yanez/Vts March 2019

lb = input(10, title="Lb", minval=1)
maType = input( defval="SMA", title="MA Type", options=["SMA","EMA","HMA","McG","WMA","Tenkan"])

fixedSL = input(title="SL Activation", defval=300)
trailSL = input(title="SL Trigger", defval=1)
fixedTP = input(title="TP Activation", defval=150)
trailTP = input(title="TP Trigger", defval=1)

FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
FromYear  = input(defval = 2019, title = "From Year", minval = 2017)
ToMonth   = input(defval = 6, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 19, title = "To Day", minval = 1, maxval = 31)
ToYear    = input(defval = 2020, title = "To Year", minval = 2017)
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
startTimeOk()  => true // create function "within window of time" if statement true
// QUANDL:BCHAIN/ETRVU is USD-denominated daily transaction value on BTC blockchain
// QUANDL:BCHAIN/MKTCP is USD-denominated Bitcoin marketcap

hma(sig, n) => // Hull moving average definition
    wma( 2*wma(sig,round(n/2))-wma(sig,n), round(sqrt(n)))

mcg(sig,length) => // Mc Ginley MA definition
    mg = 0.0
    mg := na(mg[1]) ? ema(sig, length) : mg[1] + (sig - mg[1]) / (length * pow(sig/mg[1], 4))

tenkan(sig,len) =>
    0.5*(highest(sig,len)+lowest(sig,len))

ma(t,sig,len) =>
    sss=na
    if t =="SMA"
        sss := sma(sig,len)
    if t == "EMA"
        sss := ema(sig,len)
    if t == "HMA"
        sss := hma(sig,len)
    if t == "McG" // Mc Ginley
        sss := mcg(sig,len)
    if t == "Tenkan"
        sss := tenkan(sig,len)
    if t == "WMA"
        sss := wma(sig,len)
    sss

base(mah, mal) =>
    bbb = na
    inChannel = close<mah and close>mal
    belowChannel = close<mah and close<mal
    bbb := inChannel? bbb[1]: belowChannel? -1: 1
    uuu = bbb==1? mal: mah
    ddd = bbb==1? mah: mal
    [uuu, ddd]

maH = ma(maType, high, lb)
maL = ma(maType, low, lb)

[up, dn] = base(maH,maL)

plot(up, title="High MA", color=lime, linewidth=3)
plot(dn, title="Low MA", color=orange, linewidth=3)

long = crossover(dn,up)
short = crossover(up,dn)

// === STRATEGY - LONG POSITION EXECUTION ===
strategy.entry("Long", strategy.long, when= long and startTimeOk())
strategy.exit("Exit", qty_percent = 100, loss=fixedSL, trail_offset=trailTP, trail_points=fixedTP) 
strategy.exit("Exit", when= short)
// === STRATEGY - SHORT POSITION EXECUTION ===
strategy.entry("Short", strategy.short, when= short and startTimeOk())
strategy.exit("Exit", qty_percent = 100, loss=fixedSL, trail_offset=trailTP, trail_points=fixedTP)
strategy.exit("Exit", when= long)
```

> Detail

https://www.fmz.com/strategy/438782

> Last Modified

2024-01-15 12:25:26
