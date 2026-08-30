
> Name

Quantitative-Trading-Strategy-Based-on-Ichimoku-Cloud-Breakout-and-ADX-Index
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1d1bbce4d14765ebaee.png)
[trans]
## Overview
The name of this strategy is called "Quantitative Trading Strategy Based on Yiyun Breakthrough and ADX Indicator". It combines One Cloud graphical technical analysis with the Average Trend Index (ADX) indicator to decide when to enter a long or short position. Specifically, it takes a position when price breaks out of a key area of ​​the cloud chart and the ADX indicator shows a strong trend.
## Strategy Principle
This strategy uses the "one cloud pattern" in the Black Band indicator to identify key support and resistance areas. It also combines with the ADX indicator to determine trend strength. The specific trading strategy rules are as follows:
Signals for opening a long position:
- The antenna line is turned upward and crosses the reference line
- The late line turns and crosses the 0 axis
- The price is higher than the upper edge of the cloud chart
- ADX value below 45 (indicating the trend is not overextended)
- +DI value is higher than -DI value (indicating an uptrend)
Signals for opening a short position:
- The antenna line is turned to cross the baseline
- The late line turns and crosses the 0 axis
- The price is below the lower edge of the cloud graph
- ADX value above 45 (indicating possible trend reversal)
- +DI value is lower than -DI value (indicating a downtrend)
## Advantage Analysis
This strategy combines graphic technical analysis and trend analysis indicators to effectively determine market trends and strong areas. The specific advantages are as follows:
1. Use Yiyun graphics to determine key support and resistance areas and capture strong trends.
2. Combine with ADX index to determine the true trend strength and avoid wrong transactions
3. The rules are clear and easy to operate, and it is easy to confirm the offer.
## Risks and workarounds
This strategy also has some risks, mainly focusing on the instability of the ADX index determination. Specific risks and solutions are as follows:
1. There is a lag in ADX calculation and rapid reversal may be missed. ADX parameters can be appropriately reduced to make them more sensitive
2. ADX does not work well in volatile market conditions. Other indicator filters can be added, such as BOLL channel, etc.
3. Yiyun graphics may also fail. Parameters can be adjusted appropriately or other indicators can be added to assist
## Strategy optimization suggestions
This strategy can also be optimized from the following aspects:
1. Adjust Yiyun graphics parameters to adapt to more varieties
2. Add stop loss strategy to control single loss
3. Combine more indicators to form an indicator combination to filter signals
4. Add a model prediction module and use machine learning to further determine the trend signal effector
## Summarize
This strategy combines Yiyun graphic technical analysis and ADX trend judgment indicators to form a clear and complete set of quantitative trading strategies. It determines key support and resistance areas while taking into account trend judgment, and can effectively seize market opportunities. This strategy is easy to implement and there is room for optimization. Overall, it is a high-quality quantitative strategy.
||

## Overview  

The name of this strategy is “Quantitative Trading Strategy Based on Ichimoku Cloud Breakout and ADX Index”. It combines Ichimoku cloud charting with Average Directional Movement Index (ADX) to determine when to take long or short positions. Specifically, it enters positions when price breaks through key areas of the cloud chart and ADX shows strong trend.   

## Strategy Logic   

The strategy uses “Ichimoku Cloud” from Ichimoku Kinko Hyo indicators to identify key support and resistance areas. It also incorporates ADX index to judge trend strength. The specific trading rules are:  

Long entry signals:   
- Conversion line crosses above base line  
- Lagging line crosses above 0 axis 
- Price above cloud top 
- ADX below 45 (indicating trend not overextended)   
- +DI above -DI (indicating uptrend)   

Short entry signals:
- Conversion line crosses below base line
- Lagging line crosses below 0 axis  
- Price below cloud bottom   
- ADX above 45 (indicating possible trend reversal)  
- +DI below -DI (indicating downtrend)  

## Advantage Analysis   

The strategy combines chart pattern analysis and trend analysis indicators, which can effectively determine market trends and strong areas. The main advantages are:  

1. Using Ichimoku cloud to determine key support/resistance levels to catch strong trends  
2. Incorporating ADX index to gauge true trend strength, avoiding false trades   
3. Clear rules easy to follow for live trading  

## Risks and Solutions  

There are some risks with this strategy, mainly around instability in ADX trend determination. The risks and solutions are:  

1. ADX has lagging effect, may miss fast reversals. Can lower ADX parameters to make it more sensitive  
2. ADX does not work well in ranging markets. Can add filters like BOLL channel  
3. Ichimoku cloud can also fail. Can adjust parameters or add auxiliary indicators  

## Optimization Suggestions   

The strategy can be further optimized in the following ways:  

1. Adjust Ichimoku parameters to suit more instruments   
2. Add stop loss to control single trade loss  
3. Incorporate more indicators to filter signals  
4. Add machine learning prediction to further determine trend signals  

## Conclusion  

This strategy combines Ichimoku cloud charting and ADX trend index to form a complete quantitative trading system. It identifies key support/resistance levels while also judging trend. It can effectively capture market opportunities. The strategy is easy to implement in live trading and also has room for optimization. Overall it is a quality quantitative strategy.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_2|true|Stop_loss|
|v_input_3|5|Take_profit|
|v_input_int_1|9|Tenkan-Sen Bars|
|v_input_int_2|26|Kijun-Sen Bars|
|v_input_int_3|52|Senkou-Span B Bars|
|v_input_int_4|26|Chikou-Span Offset|
|v_input_int_5|26|Senkou-Span Offset|
|v_input_4|true|Long Entry|
|v_input_5|true|Short Entry|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-26 00:00:00
end: 2024-02-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=5
strategy('Ichimoku Cloud with ADX (By Coinrule)',
         overlay=true,
         initial_capital=1000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=30,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 1, 1, 0, 0)


// Stop Loss and Take Profit for Shorting
Stop_loss = input(1) / 100
Take_profit = input(5) / 100
longStopPrice = strategy.position_avg_price * (1 - Stop_loss)
longTakeProfit = strategy.position_avg_price * (1 + Take_profit)


// Inputs
ts_bars = input.int(9, minval=1, title='Tenkan-Sen Bars')
ks_bars = input.int(26, minval=1, title='Kijun-Sen Bars')
ssb_bars = input.int(52, minval=1, title='Senkou-Span B Bars')
cs_offset = input.int(26, minval=1, title='Chikou-Span Offset')
ss_offset = input.int(26, minval=1, title='Senkou-Span Offset')
long_entry = input(true, title='Long Entry')
short_entry = input(true, title='Short Entry')

middle(len) => math.avg(ta.lowest(len), ta.highest(len))

// Ichimoku Components
tenkan = middle(ts_bars)
kijun = middle(ks_bars)
senkouA = math.avg(tenkan, kijun)
senkouB = middle(ssb_bars)

// Plot Ichimoku Kinko Hyo
plot(tenkan, color=color.new(#0496ff, 0), title='Tenkan-Sen')
plot(kijun, color=color.new(#991515, 0), title='Kijun-Sen')
plot(close, offset=-cs_offset + 1, color=color.new(#459915, 0), title='Chikou-Span')
sa = plot(senkouA, offset=ss_offset - 1, color=color.new(color.green, 0), title='Senkou-Span A')
sb = plot(senkouB, offset=ss_offset - 1, color=color.new(color.red, 0), title='Senkou-Span B')
fill(sa, sb, color=senkouA > senkouB ? color.green : color.red, title='Cloud color', transp=90)

ss_high = math.max(senkouA[ss_offset - 1], senkouB[ss_offset - 1])
ss_low = math.min(senkouA[ss_offset - 1], senkouB[ss_offset - 1])


// ADX
[pos_dm, neg_dm, avg_dm] = ta.dmi(14, 14)


// Entry/Exit Signals
tk_cross_bull = tenkan > kijun
tk_cross_bear = tenkan < kijun
cs_cross_bull = ta.mom(close, cs_offset - 1) > 0
cs_cross_bear = ta.mom(close, cs_offset - 1) < 0
price_above_kumo = close > ss_high
price_below_kumo = close < ss_low

bullish = tk_cross_bull and cs_cross_bull and price_above_kumo and avg_dm < 45 and pos_dm > neg_dm
bearish = tk_cross_bear and cs_cross_bear and price_below_kumo and avg_dm > 45 and pos_dm < neg_dm

strategy.entry('Long', strategy.long, when=bullish and long_entry and timePeriod)
strategy.close('Long', when=bearish and not short_entry)

strategy.entry('Short', strategy.short, when=bearish and short_entry and timePeriod)
strategy.close('Short', when=bullish and not long_entry)



```

> Detail

https://www.fmz.com/strategy/440872

> Last Modified

2024-02-02 17:50:30
