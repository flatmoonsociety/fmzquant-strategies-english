
> Name

Scalping-Trading-Strategy-Based-on-Double-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/bda41c552e9953a3667a1ee4dced31775644440d917f8f25d7ce5a38f993ee5c.png)
[trans]
## Overview
This strategy is a swing trading strategy based on double moving averages. It uses the crossover of the fast and slow moving averages as buy and sell signals. A buy signal is generated when the fast moving average crosses above the slow moving average from below; a sell signal is generated when the fast moving average crosses below the slow moving average from above. This strategy is suitable for volatile market conditions and can capture short-term price fluctuations to make profits.
## Strategy Principle
This strategy uses an RMA of length 6 as the fast moving average and an HMA of length 4 as the slow moving average. The strategy determines price trends and generates trading signals through the intersection of fast and slow lines.
When the fast line crosses the slow line from below, it means that the price has turned from falling to rising in the short term, which is the opportunity for chip switching, so the strategy generates a buy signal at this time; when the fast line crosses the slow line from above, it means that the price has turned from rising to falling in the short term, which is the time for chip switching, so the strategy generates a sell signal at this time.
In addition, the strategy also detects long-term trend judgments to avoid contrarian trades. Actual buy and sell signals are generated only when long-term trend judgment also favors the signal.
## Strategic Advantages
This strategy has the following advantages:
1. Use double moving average crossover judgment to effectively identify short-term price reversal points.
2. The lengths of fast lines and slow lines are properly matched to produce more accurate trading signals.
3. Combined with long-term and short-term trend judgment, most noise trading signals can be filtered out.
4. The stop-profit and stop-loss logic has been implemented to proactively avoid risks.
5. Easy to understand and implement, suitable for beginners in quantitative trading.
## Risks and Solutions
There are also some risks with this strategy:
1. The double moving average strategy is prone to multiple small profits but a large loss. The solution is to appropriately adjust the take profit and stop loss levels.
2. Frequent trading signals in volatile market conditions may lead to over-trading. The solution is to appropriately relax transaction conditions and reduce transactions.
3. Strategy parameters are easy to be over-optimized, and the actual effect may be poor. The solution is parameter robustness testing.
4. The strategy performs poorly in trending markets. The solution is to add a trend judgment module or use it in combination with a trend strategy.
## Optimization direction
Directions in which this strategy can be further optimized include:
1. Update the moving average indicator and use adaptive filters such as Kalman.
2. Add a machine learning module and use AI training to determine buying and selling points.
3. Add a fund management module to make risk control more automated.
4. Combine with high-frequency factors to find stronger trading signals.
5. Multi-species and cross-market arbitrage.
## Summarize
Overall, this double moving average oscillation strategy is a typical and practical quantitative trading strategy. It has strong adaptability, and beginners can learn a lot about strategy development from it. At the same time, it also has a lot of room for improvement, and can be further optimized by combining more quantitative techniques to obtain better strategic effects.
|| 

## Overview

This is an oscillation trading strategy based on double moving averages. It uses the crossover of fast and slow moving averages as buy and sell signals. When the fast MA crosses above the slow MA, a buy signal is generated. When the fast MA crosses below the slow MA, a sell signal is generated. This strategy is suitable for range-bound markets and capturing short-term price fluctuations.

## Strategy Logic

The strategy uses a 6-period RMA as the fast MA and a 4-period HMA as the slow MA. It judges price trends and generates trading signals based on the crossover between the fast and slow lines. 

When the fast line crosses above the slow line, it indicates a short-term trend change from decline to rise, which is a timing of chip transfer. Hence a buy signal is generated. Conversely, when the fast line crosses below the slow line, a sell signal is generated.

In addition, long-term trend judgments are made to avoid trading against the trend. Actual buy/sell signals are only generated when the long-term trend aligns with the signal.

## Advantages

The advantages of this strategy include:

1. The double MA crossover effectively identifies short-term reversal points. 

2. The fast and slow MA lengths are reasonably combined to produce accurate signals.

3. Long/short-term trend filtering removes most false signals.  

4. Take profit and stop loss logic actively manages risks.

5. It is easy to understand and implement, suitable for beginners.

## Risks and Solutions

There are also some risks:

1. Prone to multiple small profits but one huge loss. Fine tune TP/SL levels.

2. Frequent trading under range-bound markets. Relax trading conditions.

3. Overfitting parameters. Robustness test needed.  

4. Underperforms under trending markets. Add trend module or combine with trend strategies.

## Optimization Directions 

Some directions to optimize the strategy:

1. Upgrade MAs with adaptive Kalman filters etc. 

2. Add ML model to improve signal accuracy.

3. Add capital management module to automate risk control.

4. Combine with high-frequency factors for stronger signals. 

5. Cross-market arbitrage across products. 

## Conclusion

In conclusion, this double MA strategy is a typical and practical quant strategy. It has good adaptivity for beginners to learn from, meanwhile has great potential to optimize further with more quant techniques for better results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|(?⚙ Settings)Bar Color|
|v_input_2|true|Show Alerts|
|v_input_timeframe_1|0|? Timeframe: 60|5|15|30|1|120|240|360|720|D|W|
|v_input_3|true|Show Take Profit/Stop Loss|
|v_input_string_1|0|(?⚙ D-Panel Settings️)⚙ D-Panel Location: Bottom Center|Top Right|Bottom Right|
|v_input_string_2|0|⚙ D-Painel Size: Big|Small|Tiny|
|v_input_float_1|4500|(?⚙ Risk Management)Take Profit:|
|v_input_float_2|2500|Stop Loss:|
|v_input_int_1|20|(?⚙️ Scanner Market Makers Settings)Period Volume|
|v_input_float_3|1.85|Proportion to the mean: (1.25 = 125% of the mean)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-31 00:00:00
end: 2024-01-07 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © dc_analytics
// https://datacryptoanalytics.com/


//@version=5
strategy("Scalping Trading", overlay=true)

//  INPUTS  //
bar_color       = input(true, title='Bar Color', group='⚙ Settings',tooltip='Color chart bars.', inline = "1")
mostrar         = input(true, 'Show Alerts', group='⚙ Settings', inline = "1")
tempo           = input.timeframe('60', group='⚙ Settings', title='? Timeframe', options=['1', '5', '15', '30', '60', '120', '240', '360', '720', 'D', 'W'])

i_position      = input.string("Bottom Center", title = "⚙ D-Panel Location", 
 options = ["Top Right", "Bottom Center", "Bottom Right"], group='⚙ D-Panel Settings️',
 tooltip='Choose the location of the information table on the chart.(D-Panel) ')

position        = i_position == "Top Right" ? position.top_right : i_position == "Bottom Center" ? position.bottom_center : position.bottom_right

i_tam           = input.string('Big', title = '⚙ D-Painel Size', 
 options = ["Tiny", "Small", "Big"], group='⚙ D-Panel Settings️',tooltip='Choose the size of the information panel (D-Panel).')

tamanho         = i_tam == "Tiny" ? size.tiny : i_tam == "Small" ? size.small : size.normal

show_tp_sl      = input(true, title='Show Take Profit/Stop Loss', group='⚙ Settings',tooltip='Show Take Profit/Stop Loss.')
TP              = input.float(defval=4500, title='Take Profit:',group='⚙ Risk Management',tooltip='Choose amount of profit')
SL              = input.float(defval=2500, title='Stop Loss:', group='⚙ Risk Management',tooltip='Choose amount of loss') 
//  END INPUTS  //


//  DECLARATIONS  //
t_up    = '?'
t_down  = '?'

c_buy   = 'Long ⇡'
c_sell  = 'Short ⇣'

// _DECLARATION TREND
t_sma       = ta.hma(close, 200)
tend_sma    = ta.sma(close, 12)

tendencia   = request.security(syminfo.tickerid, timeframe.period, t_sma, barmerge.gaps_off, barmerge.lookahead_off)
tend_tabela = request.security(syminfo.tickerid, timeframe.period, tend_sma, barmerge.gaps_off, barmerge.lookahead_off)
// _END DECLARATION TREND

circle = plot.style_circles
//  END DECLARATIONS  //


//  COLORS  //
color gray   = color.gray
color red    = color.new(#ff8c05, 0)
color orange = color.new(#ff8c05, 0)
color silver = color.silver
color up_vol = color.new(color.green, 0)
color dn_vol = color.new(color.purple, 0)

color orange_tranp  = color.new(#ff8c05, 95)
// END COLORS //

//  SCANNER MARKET MAKERS  //
periodo  = input.int(20, 'Period Volume', group='⚙️ Scanner Market Makers Settings')
fator    = input.float(1.85, 'Proportion to the mean: (1.25 = 125% of the mean)', minval=0, group='⚙️ Scanner Market Makers Settings')
vol_up   = close > open
vol_down = open > close
vol      = volume
pesado   = volume > ta.ema(volume, periodo) * fator

palette  = pesado and vol_up ? gray : pesado and vol_down ? orange : vol_up ? silver : gray
//  END SCANNER MARKET MAKERS  //


//  LOGIC ONE  //
s = ta.rma(close, 6)
v = ta.hma(close, 4)

//  TREND  
t_baixa     = tendencia > tendencia[1]
t_alta      = tendencia < tendencia[1]

te_d        = tend_tabela > tend_tabela[1]
trend       = te_d ? t_up : t_down
//  END TREND  

a = request.security(syminfo.tickerid, tempo, s)
b = request.security(syminfo.tickerid, tempo, ohlc4)

c_dn   = a > b and a[1] < b[1]
c_up   = b > a and b[1] < a[1]

compra = mostrar and c_up ? a : na
venda  = mostrar and c_dn ? a : na

s_sell = venda and t_alta
s_buy  = compra and t_baixa
c_vela = b > a and te_d ? gray : orange

s_up = false
s_dw = false

b_sinal = not s_up and s_buy
s_sinal = not s_dw and s_sell

if b_sinal
    s_dw := false
    s_up := true
    s_up

if s_sinal
    s_dw := true
    s_up := false
    s_up

// END LOGIC ONE //


//  DATA TABLE  //
c = b > a ? orange : gray 
c_sinal = b > a ? c_buy : c_sell
//  END DATA TABLE  //


//  PLOT/BARCOLOR  //
c_barcolor = pesado and vol_up ? up_vol : pesado and vol_down ? dn_vol : vol_up ? c : c

barcolor(bar_color ? c_barcolor : na)
plot(a, color=orange_tranp, style=circle)
//  END PLOT/BARCOLOR  //


//  TABLE  //
var dash = table.new(position=position, columns=2, rows=3, border_width=1)
if barstate.islast
    table.cell(table_id=dash, column=1, row=2, text='Scalping DCA', bgcolor=orange)
    table.cell(table_id=dash, column=1, row=0, text='Trade: ' + c_sinal)
    table.cell(table_id=dash, column=1, row=1, text='Trend: ' + trend)
//  END TABLE  //


//  SETTINGS STRATEGY  //
exitPrice = strategy.closedtrades.exit_price(strategy.closedtrades - 1)

// OPEN ORDER
if (b_sinal)
    strategy.order("Long", strategy.long , comment = "Entry: " + str.tostring(close, "#.####"))
//    strategy.exit("EXIT", trail_points = 1000, trail_offset = 0, comment_trailing = "Close with Profit: " + str.tostring(close, "#.####"))
//    strategy.entry("long", strategy.long)

if (s_sinal)
    strategy.order("Short", strategy.short , comment = "Entry: " + str.tostring(close, "#.####"))
//    strategy.exit("EXIT", trail_points = 1000, trail_offset = 0, comment_trailing = "Close with Profit: " + str.tostring(close, "#.####"))
//    strategy.entry("short", strategy.short)

//  TP/SL ORDERS
if strategy.position_size > 0
    strategy.exit('Long_Close', 'Long',profit = TP , loss=SL, qty_percent=100, comment_profit = "Profit Long: " + str.tostring(exitPrice, "#.####"), comment_loss = "Stop Long: " + str.tostring(exitPrice, "#.####"))
//if  strategy.position_size > 0
//    strategy.exit("Long", "Long", stop = longSL, limit = longTP, comment_profit = "Profit Long: " + str.tostring(exitPrice, "#.####"), comment_loss = "Stop Long: " + str.tostring(exitPrice, "#.####"))
    
if strategy.position_size < 0
    strategy.exit('Short_Close', 'Short',profit = TP, loss=SL, qty_percent=100, comment_profit = "Profit Short: " + str.tostring(exitPrice, "#.####"), comment_loss = "Stop Short: " + str.tostring(exitPrice, "#.####"))
//if strategy.position_size < 0
//    strategy.exit("Short", "Short", stop = shortSL, limit = shortTP, comment_profit = "Profit Short: "+ str.tostring(exitPrice, "#.####"), comment_loss = "Stop Short: " + str.tostring(exitPrice, "#.####")) 

//  END SETTINGS STRATEGY  //

// LOGS 
// if strategy.opentrades > 10
//     log.warning("{0} positions opened in the same direction in a row. Try adjusting `bracketTickSizeInput`", strategy.opentrades)

// last10Perc = strategy.initial_capital / 10 > strategy.equity
// if (last10Perc and not last10Perc[1])
//     log.error("The strategy has lost 90% of the initial capital!")
```

> Detail

https://www.fmz.com/strategy/438056

> Last Modified

2024-01-08 16:29:21
