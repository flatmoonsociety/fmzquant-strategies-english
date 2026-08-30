
> Name

Double-Reversal-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](https://www.fmz.com/upload/asset/12a2094b9f28b5cd3e2.png)
[trans]
### Overview
The double-turn tracking strategy generates trading signals by tracking double turning points in price. When the price makes a new high, the strategy will enter a short position; when the price makes a new low, the strategy will enter a long position. This real-time tracking of price turning points can capture reversals in market momentum in real time.
### Strategy Principles
The dual turn tracking strategy uses two pattern judgments to generate trading signals, including the buy high turn pattern (HHS) and the sell low turn pattern (LLB). The judgment formula is as follows:
1. HHS form: close[0] \< close[1] and high[0] \> high[1]
2. LLB form: close[0] \> close[1] and low[0] \< low[1]
If the above conditions are met, the bar index and price of HHS and LLB will be formulated respectively. The strategy then monitors in real time whether the price breaks through the recorded turning price. When the price breaks through the HHS turning high point, it indicates that the price pattern has reversed into a downward trend, and this strategy will open a short position; conversely, when the price breaks through the LLB turning low point, it indicates that the price pattern has reversed into an upward trend, and this strategy will open a long position. In this way, the dual turn tracking strategy can dynamically capture price reversal opportunities.
When this strategy is running, it will also visually display HHS, LLB patterns and price breakthroughs by drawing marks and background colors. This is very helpful for intuitively judging the market structure and verifying the operation of strategies. In general, the dual turning tracking strategy realizes transactions by dynamically tracking price turning points, and can effectively capture price reversal opportunities.
### Advantage Analysis
The double turn tracking strategy has the following advantages:
1. Track price changes in real time and quickly capture market reversal opportunities. This strategy is more responsive than other strategies that track indicators such as moving averages.
2. Use the turning characteristics of the price itself to generate trading signals. There are not too many parameters that need to be optimized and adjusted, and the implementation is simple and direct.
3. Draw pattern marks and breakthrough marks to intuitively visualize the strategy operation process, making it easy to verify the strategy effect.
4. The amount of strategy implementation code is small and easy to understand and secondary development. It can be learned as an introductory strategy for quantitative trading.
In general, the double turn tracking strategy is relatively simple, but it can effectively capture price reversals and is worth using as a fast tracking strategy.
### Risk Analysis
There are also certain risks in the double-turn tracking strategy, which are mainly reflected in:
1. The judgment of price reversal relies on a single point of information, and there may be a high probability of misjudgment. You can set an effective tracking threshold after a price breakthrough to reduce the probability of misjudgment.
2. Without considering the large-scale price trend, wrong short position signals may still be generated during the main rise. Trend filtering can be added to avoid such risks.
3. There is no stop-loss mechanism to control single losses. In real trading, it is necessary to set up a reasonable stop loss strategy and control the single loss within the tolerable range.
4. There is optimization bias in the backtest data, and the real performance may be weaker than the backtest results. Real offer verification is crucial.
Generally speaking, as a fast tracking reversal strategy, this strategy is simple to implement, but there is also a certain probability of misjudgment risk. By adding modules such as trend filtering and stop-loss strategies, risks can be effectively reduced, making it a stable and reliable real-time strategy.
### Optimization direction
In order to reduce the probability of misjudgment and improve stability, this strategy can be optimized from the following aspects:
1. Add effective price breakthrough determination, such as requiring the price to fall below a certain percentage of the turning high before opening a position.
2. Add a large-level trend judgment module to avoid mistaken short selling during the main rising wave. Trends can be determined using indicators such as exponential moving averages.
3. Add stop-loss strategies, such as trailing stop-loss, interval stop-loss, etc., to control single losses within a certain limit.
4. Optimize the position algorithm, which can adjust the position size according to market volatility and reduce single positions when volatility is high.
5. Test real-time data over a longer period of time, evaluate parameter stability, and perform multiple iterative optimizations.
Through optimization and adjustment in the above directions, the real performance and stability of this strategy can be significantly improved.
### Summarize
The Double Turn Tracking strategy captures reversal opportunities by monitoring price turning points in real time. It has simple judgment and direct implementation, and can quickly open positions that reverse the trend. However, this strategy also has a certain probability of misjudgment risk. By adding modules such as trend judgment and stop-loss strategy, and optimizing parameters, the probability of misjudgment can be effectively reduced, making it a stable and efficient real trading strategy. This strategy is ideal for use as a fast tracking reversal type strategy.
||


### Overview  

The Double Reversal Tracking strategy generates trading signals by tracking the double reversal points of prices. It will open a short position when the price forms a new high point and will open a long position when the price forms a new low point. This real-time tracking of price reversals can capture changes in market momentum in a timely manner.   

### Strategy Logic

The Double Reversal Tracking strategy uses two pattern judgments to generate trading signals, including the high buy reversal pattern (HHS) and the low sell reversal pattern (LLB). The judgment formulas are as follows:

1. HHS pattern: close[0] \< close[1] and high[0] \> high[1]  
2. LLB pattern: close[0] \> close[1] and low[0] \< low[1]

When the above conditions are met, the bar index and price of HHS and LLB will be recorded respectively. After that, the strategy will monitor in real time whether the price breaks through the recorded reversal price. When the price breaks through the HHS reversal high point, it indicates the price pattern has reversed to a downward trend and the strategy will open a short position. On the contrary, when the price breaks through the LLB reversal low point, it indicates the price pattern has reversed to an upward trend and the strategy will open a long position. In this way, the Double Reversal Tracking strategy can dynamically capture price reversal opportunities.

When the strategy is running, it will also visually display the HHS, LLB patterns and breakout situations through markings and background colors. This is very helpful for intuitively judging market conditions and verifying the strategy. In summary, the Double Reversal Tracking strategy realizes trading by dynamically tracking price reversal points, which can effectively capture price reversal opportunities.  

### Advantage Analysis  

The Double Reversal Tracking strategy has the following advantages:

1. Real-time tracking of price reversals allows quick capturing of market reversal opportunities. Compared with other strategies tracking moving average and other technical indicators, this strategy has more agile responses.  

2. It generates trading signals directly from the price reversal features, without too many parameters to optimize. The implementation is simple and straightforward.

3. The markings of patterns and breakouts make the strategy operation visualization possible, making verification of strategy performance very easy.  

4. The code base of the strategy is small and easy to understand and customize. It can serve as an introductory quantitative trading strategy for learning.  

In summary, although simple, the Double Reversal Tracking strategy can effectively capture price reversals and is worth using as a fast-tracking reversal strategy.

### Risk Analysis

The Double Reversal Tracking strategy also has some risks, mainly:  

1. The price reversal judgment relies on single-point information, which has higher probability of misjudgments. The misjudgment probability can be reduced by setting a valid tracking threshold after price breakouts.

2. It does not consider the major trend, and may still generate incorrect short signals during major up trends. Trend filtering can be introduced to avoid such risks.

3. There is no stop loss mechanism to control single trade loss. Reasonable stop loss strategies need to be set for live trading to control losses to acceptable levels.  

4. Backtest data may have optimization bias, and live performance may underperform backtests. Live verification is crucial.  

In general, as a fast-tracking reversal strategy, this strategy has simple implementations but also has some probability of misjudgments. By introducing trend filtering, stop loss and other modules, the risks can be effectively reduced to make it a stable and reliable live trading strategy.  

### Enhancement Areas  

To reduce misjudgment probability and improve stability, the strategy can be enhanced from the following aspects:

1. Add effective breakout validation, such as requiring the price to break the reversal point by some percentage before opening positions.  

2. Add major trend judgment module to avoid incorrect short signals during major up trends. Moving average indicators can be used to determine the trend.

3. Implement stop loss strategies like trailing stop loss and zone stop loss to control single trade loss under certain limits.

4. Optimize position sizing algorithms to adjust position size based on market volatility, reducing single position size under high volatility environments.  

5. Test longer timeframes of live data to evaluate parameter stability and conduct multi-round optimization iterations.  

With adjustments through the above aspects, significant improvements can be achieved on live performance and stability of this strategy.

### Conclusion  

The Double Reversal Tracking strategy captures reversal opportunities by real-time monitoring of price reversal points. It has simple logic, straightforward execution, and can quickly open positions along reversal trends. But it also has some probability of misjudgments. By introducing trend filtering, stop loss strategies and parameter optimization, the misjudgment risk can be effectively reduced to make it a stable and efficient strategy for live trading. It is especially suitable as a fast-tracking reversal strategy.  
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-31 00:00:00
end: 2023-11-30 00:00:00
period: 6h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Rev. FO", shorttitle="Rev. FO", overlay=true, pyramiding=0,calc_on_order_fills=true,calc_on_every_tick=true,default_qty_type=strategy.percent_of_equity,default_qty_value=50,initial_capital=1000,currency="USD",commission_type=strategy.commission.percent,commission_value=0.2,process_orders_on_close=false)

HHS = close[0] < close[1] and high[0] > high[1]
LLB = close[0] > close[1] and low[0] < low[1]

var trade_long = false
var text_status = "Awaiting Trade..."
var index_hhs = 0
var index_llb = 0
var price_hhs = 0.0
var price_llb = 0.0

if (HHS)
    trade_long := false
    text_status := "Trade in Short"
    index_hhs := bar_index
    price_hhs := high
if (LLB)
    trade_long := true
    text_status := "Trade in Long"
    index_llb := bar_index
    price_llb := low

plotshape(HHS, style=shape.labeldown, title="HHS", location=location.abovebar, color=color.red, text="HHS", textcolor=color.white,size=size.tiny)
plotshape(LLB, style=shape.labelup, title="LLB", location=location.belowbar, color=color.white, text="LLB", textcolor=color.white,size=size.tiny)

// HHS_top = line.new(index_hhs-1,price_hhs,bar_index,price_hhs,extend=extend.right,style=line.style_solid,width=1,color=color.red)
// LLB_bot = line.new(index_llb-1,price_llb,bar_index,price_llb,extend=extend.right,style=line.style_solid,width=1,color=color.white)
// line.delete(HHS_top[1])
// line.delete(LLB_bot[1])

//Calculates how far the signal is painted to right. 
hours = 5
lapos_x = timenow+1000*60*60*hours
lapos_y = highest(20)

// lb = label.new(lapos_x, lapos_y, text=text_status,color=trade_long?color.white:color.red,xloc = xloc.bar_time,style=label.style_diamond,textcolor=trade_long?color.white:color.red,size=size.small)
// label.delete(lb[1])

breakout_hhs = crossover(high,price_hhs)
breakout_llb = crossunder(low,price_llb)

bgcolor(breakout_hhs?color.lime:na,transp=50,title="BO HHS")
bgcolor(breakout_llb?color.maroon:na,transp=50,title="BO LLB")

long_condition = breakout_hhs
long_close = close < price_hhs or breakout_llb
short_condition = breakout_llb
short_close = close > price_llb or breakout_hhs

strategy.entry(id="long",long=true,comment="L",when=long_condition)
strategy.close(id="long",when=long_close)
strategy.entry(id="short",long=false,comment="S",when=short_condition)
strategy.close(id="short",when=short_close)


```

> Detail

https://www.fmz.com/strategy/433938

> Last Modified

2023-12-01 15:36:34
