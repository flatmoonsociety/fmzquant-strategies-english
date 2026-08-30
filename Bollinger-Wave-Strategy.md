
> Name

Bollinger-Wave-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b759641f0ba4e3f836.png)
 [trans]

## Overview
Bollinger Wave Strategy is a quantitative trading strategy that combines Bollinger Wave Bands and moving averages. This strategy determines the market trend and overbought and oversold areas by calculating the standard deviation of the Bohr wave band and the crossover signal of the moving average, and generates trading signals.
## Strategy Principle
The strategy first calculates the exponential moving average (EMA) for the specified period as a baseline. Then calculate the upper trajectory (EMA + n times the standard deviation) and the lower trajectory (EMA - n times the standard deviation) based on this EMA. When the price breaks above the upper track, it is an overbought signal, and when the price falls below the lower track, it is an oversold signal.
When the price is between the upper track and the lower track, it is the normal price fluctuation range of the stock. In addition, this strategy combines RSI indicators and other indicators to filter trading signals, reduce trading frequency, and reduce unnecessary losses.
Specifically, the trading signal judgment rules of this strategy are as follows:
1. Bull signal: closing price > upper track and RSI (14) > 60
2. Short signal: closing price < lower track and RSI (14) < 40
When the above trading signals appear, enter the market according to a fixed amount or account ratio. When the price returns to the wave band range or when the opposite signal appears, exit the position.
## Strategic Advantages
This strategy combines trend judgment and overbought and oversold judgment to avoid erroneous transactions during volatile consolidation. Compared with a single indicator strategy, unnecessary position openings can be reduced and risks can be effectively controlled.
Compared with the simple moving average strategy, Bohr wave bands can better reflect the current market volatility and risk level. When the wave band width is small, the trading signal is more reliable; when the wave band width is large, the trading frequency will automatically decrease. This adaptive adjustment can control strategic risks according to different market conditions.
In addition, this strategy uses RSI and other indicators for double confirmation, which can filter out some false signals and avoid wrong transactions at trend turning points. This also improves the strategy win rate.
## Risk Analysis
This strategy mainly faces the following risks:
1. Parameter optimization risks. If the moving average parameters or standard deviation multiples are set improperly, more noise trading or missed trading opportunities will occur. These parameters require repeated testing and optimization.
2. Break through the risk of false signals. When the price breaks through the upper and lower rails in the short term and then falls back soon, it will generate a wrong signal. If you trade rashly at this time, your losses will increase. This risk can be controlled by increasing the moving average period or setting a stop loss.
3. Transaction frequency risk. If the gap between the upper and lower tracks is too small, the number of transactions and handling fees will increase. This will have a certain impact on final profits. This risk can be controlled by appropriately increasing the moving average period.
## Optimization direction
There is room for further optimization of this strategy:
1. Add a stop loss mechanism. Establishing a trailing stop loss or time stop loss can help stop losses in time and control single losses.
2. Increase position management. For example, establish rules for adding and reducing positions so that profits can be increased and losses can be reduced. This can improve strategy profitability.
3. Filter signals in combination with other indicators. Indicators such as KDJ and MACD can be used as indicators to assist in judging signals. This helps further improve strategy profitability.
4. Optimize parameter settings. Parameter combinations can be tested through more systematic methods such as genetic algorithms to find better parameter settings.
## Summarize
The Bohr band fluctuation signal strategy integrates the trend judgment of the moving average and the judgment of overbought and oversold. It adjusts the trading frequency according to changes in the wave band range and can adapt to different states of the market. At the same time, it is combined with RSI and other indicators to filter signals to avoid erroneous transactions. This strategy not only takes into account the need to track market trends, but also controls risks. Through continuous optimization, this strategy can become a stable and profitable quantitative trading strategy.
|| 

## Overview

The Bollinger Wave Strategy is a quantitative trading strategy that combines Bollinger Bands and moving averages. It generates trading signals by calculating the standard deviation of Bollinger Bands and crossovers of moving averages to determine market trends and overbought/oversold areas.

## Strategy Logic

The strategy first calculates an exponential moving average (EMA) over a specified period as the baseline. The upper band (EMA + n times standard deviation) and lower band (EMA - n times standard deviation) are then calculated based on this EMA. A break above the upper band indicates an overbought signal, while a break below the lower band indicates an oversold signal.  

When prices are between the upper and lower bands, it is the normal price fluctuation range of the stock. In addition, the strategy combines other indicators like RSI to filter trade signals and reduce trading frequency to minimize unnecessary losses.

Specifically, the trading signal rules are:

1. Long signal: Close > Upper band and RSI(14) > 60 
2. Short signal: Close < Lower band and RSI(14) < 40

When the above trading signals appear, take positions with fixed quantity or account percentage. Exit positions when prices move back into bands or opposite signals appear.

## Advantages

The strategy combines trend determination and overbought/oversold judgement to avoid incorrect trades in range-bound markets. Compared to single indicator strategies, it can reduce unnecessary position opening and effectively control risks.

Compared to simple moving average strategies, Bollinger Bands better reflect current market volatility and risk levels. When band width is small, trade signals are more reliable. When band width is large, trade frequency will be reduced automatically. Such adaptive adjustment can control strategy risks based on different market conditions.

In addition, the double confirmation from RSI and other indicators helps filter out some false signals and avoid incorrect trades around trend turning points. This also improves the strategy's win rate.

## Risk Analysis

The main risks of this strategy are:

1. Parameter optimization risk. If moving average or standard deviation parameters are set inappropriately, it may generate more noisy trades or miss trade opportunities. These parameters need iterative testing and optimization.

2. False breakout signal risk. When prices briefly break above or below the bands then quickly reverse, it may generate incorrect signals. Blindly trading on those would increase losses. This can be controlled by increasing moving average period or setting stop loss.  

3. High trading frequency risk. If the bands have very narrow gaps, it may increase trade counts and commissions paid, thus affecting final profitability. This can be mitigated by moderately increasing the moving average period.

## Optimization Directions

There is room for further optimization of the strategy:

1. Add stop loss mechanism. Using trailing stop loss or time stop loss helps realize losses in time and control single trade loss amount.

2. Add position sizing rules. For example, pyramiding into winning trades and reducing losers. This can improve strategy return.

3. Combine with other indicators for signal filtering. Indicators like KDJ and MACD can serve as auxiliary judgement tools. This helps further improve strategy profitability. 

4. Optimize parameter settings. More systematic methods like genetic algorithms can be used to test different parameter combinations and find better settings.

## Conclusion

The Bollinger Wave Strategy integrates trend determination of moving averages and overbought/oversold judgement. It adjusts trade frequency based on band width changes to adapt to different market conditions. Meanwhile, signal filtering by RSI and other indicators avoids incorrect trades. The strategy considers both tracking market trends and controlling risks. With continuous optimization, it can become a steady profitable quantitative trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|55|EMA length|
|v_input_float_1|true|Standard Deviation|
|v_input_string_1|0|Trade Type: Both|Shorts Only|Longs Only|
|v_input_2|true|Color Bars|
|v_input_3|true|╔═══ Time Range to BackTest ═══╗|
|v_input_int_2|true|From Month|
|v_input_int_3|true|From Day|
|v_input_int_4|2018|From Year|
|v_input_int_5|true|To Month|
|v_input_int_6|true|To Day|
|v_input_int_7|9999|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-08 00:00:00
end: 2024-01-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
//@FiboBuLL

strategy(shorttitle='FB Wave', title='FiboBuLL Wave', overlay=true, pyramiding=1, currency=currency.NONE, initial_capital=100000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

src = input(close, title='Source')
length = input.int(55, minval=1, title='EMA length')  // 20 for classis Bollinger Bands SMA line (basis)


mult = input.float(1., minval=0.236, maxval=2, title='Standard Deviation')  //2 for Classic Bollinger Bands //Maxval = 2 as higher the deviation, higher the risk
basis = ta.sma(src, length)
dev = mult * ta.stdev(src, length)

Show = input.string('Both', options=['Longs Only', 'Shorts Only', 'Both'], title='Trade Type')
CC = input(true, 'Color Bars')

upper = basis + dev
lower = basis - dev

//Conditions for Long and Short - Extra filter condition can be used such as RSI or CCI etc.

short = src < lower  // and rsi(close,14)<40
long = src > upper  // and rsi(close,14)>60

L1 = ta.barssince(long)
S1 = ta.barssince(short)

longSignal = L1 < S1 and not (L1 < S1)[1]
shortSignal = S1 < L1 and not (S1 < L1)[1]

//Plots and Fills


////Long/Short shapes with text
// plotshape(S1<L1 and not (S1<L1)[1]?close:na, text = "sᴇʟʟ", textcolor=#ff0100, color=#ff0100, style=shape.triangledown, size=size.small, location=location.abovebar, transp=0, title = "SELL", editable = true)
// plotshape(L1<S1 and not (L1<S1)[1]?close:na, text = "ʙᴜʏ", textcolor = #008000, color=#008000, style=shape.triangleup, size=size.small, location=location.belowbar, transp=0, title = "BUY", editable = true)  

// plotshape(shortSignal?close:na, color=#ff0100, style=shape.triangledown, size=size.small, location=location.abovebar, transp=0, title = "Short Signal", editable = true)
// plotshape(longSignal?close:na, color=#008000, style=shape.triangleup, size=size.small, location=location.belowbar, transp=0, title = "Long Signal", editable = true)  


p1 = plot(upper, color=color.new(#ff0000, 75), display=display.all, title='Upper Band')
p2 = plot(lower, color=color.new(#008000, 75), display=display.all, title='Lower Band')

p = plot(basis, color=L1 < S1 ? #008000 : S1 < L1 ? #ff0000 : na, linewidth=2, editable=false, title='Basis')

fill(p, p1, color=color.new(color.teal, 85), title='Top Fill')  //fill for basis-upper
fill(p, p2, color=color.rgb(217, 161, 161), title='Bottom Fill', transp=85)  //fill for basis-lower

//Barcolor

bcol = src > upper ? color.new(#8ceb07, 0) : src < lower ? color.new(#ff0000, 0) : src > basis ? color.green : src < basis ? color.red : na

barcolor(CC ? bcol : na, editable=false, title='Color Bars')


// //Alerts ----  // Use 'Once per bar close'

// alertcondition(condition=longSignal, title="Long - BB Filter", message='BB Filter Long @ {{close}}') // Use 'Once per bar close'
// alertcondition(condition=shortSignal, title="Short - BB Filter", message='BB Filter Short @ {{close}}')  // Use 'Once per bar close'

Notestart1 = input(true, '╔═══ Time Range to BackTest ═══╗')

// === INPUT BACKTEST RANGE ===
FromMonth = input.int(defval=1, title='From Month', minval=1, maxval=12)
FromDay = input.int(defval=1, title='From Day', minval=1, maxval=31)
FromYear = input.int(defval=2018, title='From Year', minval=2015)
ToMonth = input.int(defval=1, title='To Month', minval=1, maxval=12)
ToDay = input.int(defval=1, title='To Day', minval=1, maxval=31)
ToYear = input.int(defval=9999, title='To Year', minval=2010)

// === FUNCTION EXAMPLE === 
start = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish = timestamp(ToYear, ToMonth, ToDay, 23, 59)  // backtest finish window
window() =>
    time >= start and time <= finish ? true : false

if window() and (Show == 'Longs Only' or Show == 'Both')
    strategy.entry('AL', direction=strategy.long, when=longSignal)
    strategy.close('LongAL', when=shortSignal, comment='AL KAPA')

if window() and (Show == 'Shorts Only' or Show == 'Both')
    strategy.entry('SAT', direction=strategy.short, when=shortSignal)
    strategy.close('SAT', when=longSignal, comment='SAT KAPA')













```

> Detail

https://www.fmz.com/strategy/438821

> Last Modified

2024-01-15 15:16:27
