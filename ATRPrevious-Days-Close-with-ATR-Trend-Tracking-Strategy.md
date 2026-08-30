
> Name

Trend following strategy Previous-Days-Close-with-ATR-Trend-Tracking-Strategy based on previous day's closing price and ATR indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1767cffa0bc8a78a8d2.png)
[trans]

### Overview
This strategy sets the long and short opening price and stop loss price based on the previous day's closing price and the ATR indicator to track the trend. When the price breaks through the opening price, open a long or short position, then clear the position after stopping loss or taking profit.
### Strategy Principles
This strategy uses the previous day's closing price, highest price, lowest price and ATR indicator to calculate the entry price and stop loss price. The specific calculation formula is as follows:
Long position opening price TPup = previous day's closing price + ATR \* 0.8
Short position opening price TPdown = previous day's closing price - ATR \* 0.8
Long stop loss price slup = previous day’s closing price + ATR \* 0.2
Short stop loss price sldown = previous day's closing price - ATR \* 0.2
Long position profit level profitlevelup = previous day’s lowest price + ATR \* 1.7
Short take profit price profitleveldown = the highest price of the previous day - ATR \* 1.7
When the price breaks through the long opening price TPup, the number of lots is 10 to go long; when the price breaks through the short position opening price TPdown, the number of lots is 10 lots to go short. Then set stop loss and take profit. Stop loss and clear the position when the price hits the stop loss price, and take profit and clear the position after the price hits the take profit price.
### Advantage Analysis
The main advantages of this strategy are:
1. Use the ATR indicator to set dynamic opening prices and stop-loss prices, which can be adjusted according to market volatility to make transactions more adaptable to the market environment.
2. Use the closing price of the previous day to determine the direction, and then combine it with the ATR indicator to determine the specific transaction price to avoid being misled by real-time prices with too much noise.
3. By setting up stop-loss and take-profit mechanisms at the same time, the risk of a single transaction can be well controlled.
### Risk Analysis
The main risks of this strategy are:
1. The price set by the ATR indicator may be too ideal and cannot truly reflect the market situation, resulting in frequent stop losses. You can adjust the ATR parameters appropriately or increase the stop loss range.
2. The previous day's closing price cannot determine the future trend. If there is a sharp reversal, it will mislead the choice of trading direction. Consider combining it with other indicators to confirm the trend.
3. The stop loss and take profit positions may be triggered by manipulation and the loss cannot be truly stopped. You can set stop losses in batches to avoid being trapped.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize ATR parameters to make the transaction price more consistent with market volatility.
2. Add a trend judgment mechanism to avoid transaction reversal. For example, combined with indicators such as MA.
3. Adjust the take-profit range to reduce the probability of the profit point being triggered while maintaining profitability.
4. Set stop loss and take profit in batches to reduce the probability of being trapped and losing money.
5. Adding a position management mechanism can increase the position in the trend stage.
### Summarize
This strategy sets dynamic trading prices based on the previous day's closing price and ATR indicator to achieve effective tracking of trends. At the same time, set up stop-loss and take-profit mechanisms to control the risk of a single transaction. Optimization directions include parameter optimization, addition of judgment mechanism, profit-taking adjustment and position management, etc. Generally speaking, this strategy achieves the effect of trend-chasing trading well.
||

### Overview  

This strategy sets long and short entry price levels and stop loss price levels based on previous day's close price and ATR indicator to track the trend. It goes long or short when price breaks through the entry price levels, and flattens positions on stop loss or take profit.

### Strategy Logic  

This strategy uses previous day's close price, high price, low price and ATR indicator to calculate entry price levels and stop loss levels. The specific formulas are as follows:

Long entry price level TPup = Previous day's close + ATR * 0.8  
Short entry price level TPdown = Previous day's close - ATR * 0.8

Long stop loss level slup = Previous day's close + ATR * 0.2  
Short stop loss level sldown = Previous day's close - ATR * 0.2  

Long take profit level profitlevelup = Previous day's low + ATR * 1.7   
Short take profit level profitleveldown = Previous day's high - ATR * 1.7  

When price breaks through TPup, go long 10 lots. When price breaks through TPdown, go short 10 lots. Then set stop loss and take profit. Exit positions on stop loss trigger or take profit trigger.

### Advantage Analysis   

The main advantages of this strategy are:  

1. Using ATR indicator to set dynamic entry price levels and stop loss levels based on market volatility, making trades more adaptive to market conditions.  

2. Using previous day's close to determine direction and combining with ATR indicator to identify specific trade levels, avoiding being misled by too much real-time price noise.

3. Setting both stop loss and take profit mechanisms to effectively control the risk of each trade.  

### Risk Analysis

The main risks of this strategy are:

1. The price levels set by ATR may be too idealistic to truly reflect market conditions, leading to frequent stop loss triggers. Parameters of ATR can be adjusted or stop loss range can be widened.  

2. Previous day's close cannot determine future trends. Drastic reversals may mislead directional choices. Other indicators can be combined to confirm trends.

3. Stop loss and take profit may be manipulated to trigger, failing to truly stop loss. Batch stop loss can be used to avoid being trapped.  

### Optimization Directions   

This strategy can be optimized in the following aspects:

1. Optimize ATR parameters to make trade levels fit better with market volatility.  

2. Add trend judging mechanisms to avoid trading reversals, e.g. combining with MA indicators.

3. Adjust take profit range, keeping profitability while reducing probability of profit taking triggers.   

4. Set batch stop loss and profit taking to reduce probability of being trapped or losing.

5. Add position sizing mechanism to increase positions in trending phases.  

### Conclusion  

This strategy sets dynamic trade levels based on previous day's close and ATR to effectively track trends. It also uses stop loss and take profit to control single trade risks. Optimization directions include parameter tuning, judging mechanism enhancement, take profit adjustment and position sizing etc. In general, this strategy achieves good trend following effects.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|lookback length of ATR|
|v_input_2|0.8|Entry level for ATR|
|v_input_3|1.7|Exit level for ATR|
|v_input_4|0.2|Stop loss level for ATR|
|v_input_5|2014|Backtest Starting year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("PC with ATR Strategy (by Zhipengcfel)", shorttitle="PC_ATR", pyramiding=1, overlay=true)

// Zhipengcfel's Previous day's close with ATR Strategy
//
// Version 1.0
// @copyright Idea by Zhipengcfel on June 29, 2017.

//Previous day's close plus ATR strategy. 
//Buy (if breaking PC+ATR*0.8) or sell (if breaking PC-0.8*ATR). 

//This is just a demo vision and can not be used for real auto trading



///////////// ATR value
ATRlength = input(14, minval=1, title="lookback length of ATR")
//ATR = atr(ATRlength)
ATR = request.security(syminfo.tickerid, 'D', atr(ATRlength))

///////////// Entry levels and target levels
entr = input(0.8, minval=0.1, step = 0.05, title="Entry level for ATR")
tplevel = input(1.7, minval=0.1, step = 0.05, title="Exit level for ATR")
yesterday = request.security(syminfo.tickerid, 'D', close[1])
dl = request.security(syminfo.tickerid, 'D', low[1])
dh = request.security(syminfo.tickerid, 'D', high[1])
TPup = yesterday+entr*ATR
TPdown = yesterday-entr*ATR
profitlevelup = dl+tplevel*ATR
profitleveldown = dh-tplevel*ATR

///////////// Stop loss level
sl = input( 0.2  ,minval=0.01, step = 0.05, title="Stop loss level for ATR") //82 for 2, 83 for 3 and more positions
slup = yesterday+sl*ATR
sldown = yesterday-sl*ATR

///////////// Starting year to backtest
yer = input( 2014  , title="Backtest Starting year")


///////////// strategy: PC + ATR
if (close > TPup) and (close < profitlevelup)
    strategy.entry("LONG", strategy.long, 10, comment="Buy", when = year > yer, oca_name="My oca")
    strategy.exit("Stopped", "LONG",  stop = slup, limit= profitlevelup, oca_name="My oca")
            

if (close < TPdown) and (close > profitleveldown)
    strategy.entry("SHORT", strategy.short, 10, comment="Sell", when = year > yer, oca_name="My oca")
    strategy.exit("Stopped", "SHORT", stop = sldown, limit= profitleveldown, oca_name="My oca")
 
```

> Detail

https://www.fmz.com/strategy/440536

> Last Modified

2024-01-31 14:39:09
