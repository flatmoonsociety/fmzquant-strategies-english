
> Name

Oscillation-Strategy-of-High-and-Low-TEMA-Average
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/187d54c57fe7604338a.png)

[trans]

## Overview
This strategy uses three indicators: TEMA, VWMACD and HMA to capture the falling trend of Bitcoin. Its main logic is to go short when VWMACD crosses the 0 axis, the price is lower than the HMA moving average, and the fast line TEMA is lower than the slow line TEMA. The position is closed when VWMACD crosses the 0 axis, the price is higher than the HMA moving average, or the fast TEMA crosses the slow TEMA.
## Principle
First calculate VWMACD (the only difference from ordinary MACD is the way to calculate the moving average) and draw it as a histogram. Then add HMA as a trend filter. Then create and add fast line TEMA (5 periods) and slow line TEMA (8 periods), and calculate the difference between the two and draw it near the 0 axis. This is the key to short selling decisions.
The specific entry rules are: go short when VWMACD is lower than the 0 axis, the price is lower than the HMA moving average, and the fast TEMA is lower than the slow TEMA.
The specific exit rules are: close the position when VWMACD crosses the 0 axis, the price is higher than the HMA moving average, or the fast TEMA crosses the slow TEMA.
## Advantage Analysis
- Used a combination of three indicators to improve the reliability of trading signals
- VWMACD can identify divergences and provide more accurate trend judgments
- HMAfilt acts as a trend filter to avoid being misled by noise
- Fast and slow TEMA combination to capture short-term reversal points
- Using short-cycle parameters, it is suitable for high-frequency trading and captures short-term falling prices.
## Risk Analysis
- Multiple indicator combinations, parameter settings are complex and require experience for tuning
- Although there is an HMA filter, it still needs to prevent false breakthroughs that shake the market
- Short-period parameters are easily disturbed by market noise, resulting in false signals.
- Stop loss needs to be strictly controlled to avoid larger losses than expected.
- Need to pay attention to transaction cost control, high-frequency transactions are easily damaged by handling fees
## Optimization direction
- Can test parameter combinations of different periods to find the best parameters
- You can add other indicators, such as RSI, KD and other auxiliary judgments
- Adaptive parameters can be used according to different market conditions
- Stop loss strategies can be optimized, such as moving the stop loss with the price
- Can be combined with quantity and energy indicators to avoid false breakthroughs due to insufficient quantity and energy
## Summarize
This strategy uses a combination of VWMACD, HMA and fast and slow TEMA. Ziel captures the short-term decline of Bitcoin. Its advantage is that the signal is more reliable and suitable for high-frequency trading. However, there are also risks such as complicated parameter tuning and easy interference by noise. By continuing to optimize parameter combinations and adding auxiliary indicators, the strategy can be made more stable and reliable. Generally speaking, this strategy uses the characteristics of multi-indicator confirmation and short-cycle parameters to make a more accurate judgment on Bitcoin's short-term decline. It is an effective high-frequency short-selling strategy.
||


## Overview

This strategy uses TEMA, VWMACD and HMA indicators to capture the downtrend of Bitcoin. Its main logic is to go short when VWMACD crosses below 0, price is below HMA and fast TEMA is below slow TEMA. It will exit the position when VWMACD crosses above 0, price is above HMA or fast TEMA crosses above slow TEMA.

## Principle 

First calculate VWMACD (the only difference from regular MACD is the way to calculate moving average) and plot it as histogram. Then add HMA as a trend filter. After that create and add fast TEMA (5 periods) and slow TEMA (8 periods), and calculate the difference between them to plot around 0. This is the key decision for going short.  

The specific entry rule is: when VWMACD is below 0, price is below HMA and fast TEMA is below slow TEMA, go short.

The specific exit rule is: when VWMACD crosses above 0, price is above HMA or fast TEMA crosses above slow TEMA, close position.

## Advantage Analysis

- Uses a combination of three indicators, improves reliability of trading signals.
- VWMACD can identify divergences and provide accurate trend judgements.  
- HMAfilt as a trend filter, avoids noise interference.
- Fast and slow TEMA combo catches short-term reversal points.
- Adopts short-period parameters, suitable for high frequency trading, catches short-term downtrends.

## Risk Analysis

- Multiple indicators combo, complex parameter tuning needed.
- Although having HMA filter, still need to prevent false breakouts in ranging markets.
- Short periods prone to market noise interference, wrong signals may occur.  
- Need strict stop loss to prevent unexpected large losses.
- Need to focus on transaction cost control, high frequency trading easily hurt by friction.

## Optimization Directions

- Can test different parameter combinations to find optimal parameters.
- Can add other indicators like RSI, KD for assistance.
- Can use adaptive parameters according to different market conditions.
- Can optimize stop loss strategy, like trailing stop loss.
- Can combine with volume indicators to avoid insufficient thrust.

## Conclusion

This strategy uses the combination of VWMACD, HMA and fast/slow TEMA to capture short-term downtrends of Bitcoin. Its advantages are relatively reliable signals and suitability for high frequency trading. But it also has risks like complex parameter tuning, prone to noise interference. Further optimizing parameter combos and adding auxiliary indicators can make the strategy more stable and reliable. Overall, by utilizing multiple indicator confirmation and short period parameters, this strategy can make relatively accurate judgements on Bitcoin's short-term downtrends, and is an effective high frequency short strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2017|Start Year|
|v_input_2|12|Month|
|v_input_3|17|Day|
|v_input_4|13|Short period|
|v_input_5|21|Long period|
|v_input_6|5|Smoothing period|
|v_input_7|400|HMA|
|v_input_8|5|Fast moving TEMA|
|v_input_9|8|Slow moving TEMA|
|v_input_10|true|Take Profit (%)|
|v_input_11|4|Stop Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-08 00:00:00
end: 2023-11-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="TEMA_HMA_VWMACD short strategy", shorttitle="Short strategy", overlay=false, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.018, currency='USD')
startP = timestamp(input(2017, "Start Year"), input(12, "Month"), input(17, "Day"), 0, 0)
end   = timestamp(9999,1,1,0,0)
_testPeriod() =>
    iff(time >= startP and time <= end, true, false)
    

slow = input(13, "Short period")
fast = input(21, "Long period")
signal = input(5, "Smoothing period")

Fast = ema( volume * close, fast ) / ema( volume, fast ) 
Slow = ema( volume * close, slow ) / ema( volume, slow ) 
Macd = Slow - Fast 
Signal = ema(Macd, signal) 
Hist=Macd-Signal
plot(Hist, color=color.silver, linewidth=1, style=plot.style_histogram)
plot(0, color=color.red)

length = input(400, minval=1, title = "HMA")
hullma = wma(2*wma(close, length/2)-wma(close, length), floor(sqrt(length)))

tema_length_1 = input(5, "Fast moving TEMA")
tema_length_2 = input(8, "Slow moving TEMA")


tema(sec, length)=>
    tema1= ema(sec, length)
    tema2= ema(tema1, length)
    tema3= ema(tema2, length)
    tema = 3*tema1-3*tema2+tema3

tema1 = tema(hlc3, tema_length_1)
tema2 = tema(hlc3, tema_length_2)

threshold  = 0
tm = tema1 - tema2
plot_fast = plot(tm, color = tm > 0 ? color.green : color.red)
plot(threshold, color=color.purple)

up =  crossover(tm, 0) 
down = crossunder(tm, 0)

longCondition =  (Hist < 0) and hullma > close and (tema1 < tema2)  and _testPeriod() 
strategy.entry('BUY', strategy.short, when=longCondition)  
 
shortCondition =  (Hist > 0) or hullma < close or up
strategy.close('BUY', when=shortCondition)


// Take profit  
tp = input(1, type=input.float, title='Take Profit (%)')  
sl = input(4, type=input.float, title='Stop Loss (%)')  
strategy.exit('XLong', from_entry='BUY', profit=(close * (tp/100) * (1/syminfo.mintick)), loss=(close * (sl/100) * (1/syminfo.mintick)))
```

> Detail

https://www.fmz.com/strategy/432239

> Last Modified

2023-11-15 17:49:52
