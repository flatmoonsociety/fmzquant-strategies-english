
> Name

Momentum-Capture-Channel-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/651191a78692be312c.png)
 [trans]

### Overview
The Momentum Capture Channel strategy is a variation based on the Donchian channel. It consists of the highest price band, the lowest price band and the baseline which is the average of the highest price band and the lowest price band. This strategy is very useful on weekly and daily time frames of trending instruments. This is the implementation used in the QuantCT application.
You can set the operating mode to long-short or long only.
You can also set a fixed stop loss or ignore it so that the strategy only operates based on entry and exit signals.
### Strategy Principles
The core logic of this strategy is based on the Donchian Channel indicator. The Donchian channel consists of the average of the highest, lowest and closing prices over a 20-day period. Determine the trend direction and possible reversal based on the price breaking through the upper and lower rails of the channel.
This strategy is a variation of the Donchian channel. It consists of the highest price band, the lowest price band and the baseline which is the average of the highest price band and the lowest price band. The specific logic is as follows:
1. Calculate the highest price and lowest price within a certain period as the upper and lower rails of the channel
2. Calculate the average of the upper and lower rails as the baseline
3. When the price breaks through the upper track, go long
4. Close long positions when the price falls below the baseline
5. When the price falls below the lower band, go short (if short positions are allowed)
6. When the price regains the baseline, close the short position
The advantage of this strategy is that it can effectively capture the trend momentum of prices. By waiting for the price to break through the upper and lower rails to judge the start of the real trend, you can avoid unnecessary losses caused by being talked about.
### Advantage Analysis
1. Capture price trend momentum and achieve profitable growth
2. Avoid being trapped by false breakthroughs and reduce unnecessary losses
3. Parameters can be adjusted flexibly, suitable for different varieties
4. You can choose to do only long or full positions to meet different needs.
5. Integrated stop-loss mechanism can effectively control single losses
### Risk Analysis
1. While capturing the trend, it will also amplify the losses caused by failed breakthroughs.
2. If the stop loss setting is too loose, a single loss may increase
3. Improper parameter settings may lead to frequent transactions and increase transaction costs.
4. There is a certain lag in the judgment of breakthrough signals, and the optimal entry point may be missed.
Solution:
1. Choose the stop loss ratio carefully, not only to control losses, but also to give enough space to the trend
2. Increase the parameter period value and reduce the transaction frequency
3. Combine with other indicators to judge the reliability of trend signals and choose better entry opportunities.
### Optimization direction
1. Integrate other indicators to determine the timing of entry
2. Dynamically adjust the stop loss position
3. Optimize parameter settings according to variety characteristics
4. Combined with machine learning to determine the success rate of breakthroughs
5. Add position management logic
### Summarize
The Momentum Capture Channel strategy offers considerable profit opportunities by capturing price trends. At the same time, it also has certain risks, and parameters need to be appropriately adjusted for risk control. By continuously optimizing entry timing and stop loss logic, this strategy can become an excellent trend following system. Its simple trading rules and clear signal judgment make it easy to understand and implement, making it very suitable for novice traders.
|| 

### Overview

The Momentum Capture Channel Strategy is a variation of the Donchian Channel trading strategy. It consists of a highest-high band, a lowest-low band, and a baseline which averages the highest-high and lowest-low bands. This strategy works very well on trending instruments across weekly and daily timeframes. This is the implementation used in the QuantCT app.  

You can set the operation mode to Long/Short or Long-only.

You can also set a fixed stop-loss or ignore it so the strategy acts solely based on entry and exit signals.

### Strategy Logic

The core logic of this strategy is based on the Donchian Channel indicator. The Donchian Channel consists of the highest high, lowest low, and closing price average over the past 20 days. Trend direction and potential reversals are judged by price breaking through the upper and lower bands of the channel.

This strategy is a variation on the Donchian Channel. It consists of a highest-high band, a lowest-low band, and a baseline which averages the highest-high and lowest-low bands. The specific logic is:

1. Calculate the highest high and lowest low over a certain period as the upper and lower bands of the channel
2. Calculate the average of the upper and lower bands as the baseline
3. Go long when price breaks above the upper band 
4. Close long position when price breaks below the baseline
5. Go short when price breaks below the lower band (if shorting is allowed)
6. Close short position when price reclaims the baseline

The advantage of this strategy is it can effectively capture the momentum of price trends. By waiting for price to break the upper/lower bands to determine the real start of a trend, unnecessary losses from fakeouts can be avoided.  

### Advantage Analysis

1. Captures price trend momentum for profit growth
2. Avoids unnecessary losses from being trapped by fake breakouts
3. Flexible parameter adjustment makes it suitable for different products  
4. Can choose Long-only or fully traded to suit different needs
5. Integrated stop-loss mechanism effectively controls per trade loss

### Risk Analysis  

1. While capturing trends, failed breakouts also amplify losses
2. Stop-loss set too wide could lead to enlarged per trade loss
3. Improper parameter settings may lead to overtrading and increased transaction costs  
4. Breakout signal judgement has some lag, could miss best entry points  

Solutions:

1. Choose stop-loss percentage carefully to control loss yet give trend enough room
2. Increase parameter period values to reduce trading frequency  
3. Incorporate other indicators to judge signal reliability, select better entry timing

### Optimization Directions

1. Incorporate other indicators to determine entry timing
2. Dynamically adjust stop-loss placement  
3. Optimize parameter settings based on instrument characteristics 
4. Incorporate machine learning to judge breakout success rate
5. Add position sizing logic

### Conclusion

The Momentum Capture Channel strategy provides considerable profit opportunities by capturing price trends. At the same time, it also has certain risks that need to be controlled by properly adjusting parameters. By continually optimizing entry timing selection and stop-loss logic, this strategy can become an excellent trend following system. Its simple trading rules and clear signal judgement make it easy to understand and implement, highly suitable for novice traders.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|High Period|
|v_input_2|10|Low Period|
|v_input_3|false|Long Only|
|v_input_4|5|Stop-loss (%)|
|v_input_5|false|Use Stop-Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-19 00:00:00
end: 2023-12-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © QuantCT

//@version=4
strategy("Donchian Channel Strategy Idea",
         shorttitle="Donchian", 
         overlay=true,
         pyramiding=0,     
         default_qty_type=strategy.percent_of_equity, 
         default_qty_value=100, 
         initial_capital=1000,           
         commission_type=strategy.commission.percent, 
         commission_value=0.075)

// ____ Inputs

high_period = input(title="High Period", defval=10) 
low_period = input(title="Low Period", defval=10)
long_only = input(title="Long Only", defval=false)
slp = input(title="Stop-loss (%)", minval=1.0, maxval=25.0, defval=5.0)
use_sl = input(title="Use Stop-Loss", defval=false)

// ____ Logic

highest_high = highest(high, high_period)
lowest_low = lowest(low, low_period)
base_line = (highest_high + lowest_low) / 2
    
enter_long = (close > highest_high[1])
exit_long = (close < base_line)
enter_short = (close < lowest_low[1])
exit_short = (close > base_line)

strategy.entry("Long", strategy.long, when=enter_long)
strategy.close("Long", when=exit_long) 
if (not long_only)
    strategy.entry("Short", strategy.short, when=enter_short)
    strategy.close("Short", when=exit_short) 
   
// ____ SL

sl_long = strategy.position_avg_price * (1- (slp/100))
sl_short = strategy.position_avg_price * (1 + (slp/100))
if (use_sl)
    strategy.exit(id="SL", from_entry="Long", stop=sl_long)
    strategy.exit(id="SL", from_entry="Short", stop=sl_short)
    
// ____ Plots

colors = 
 strategy.position_size > 0 ? #27D600 :
 strategy.position_size < 0 ? #E30202 :
 color.orange

highest_high_plot = plot(highest_high, color=colors)
lowest_low_plot = plot(lowest_low, color=colors)
plot(base_line, color=color.silver)
fill(highest_high_plot, lowest_low_plot, color=colors, transp=90)







```

> Detail

https://www.fmz.com/strategy/435981

> Last Modified

2023-12-20 15:46:40
