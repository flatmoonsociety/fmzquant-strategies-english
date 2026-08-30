
> Name

Momentum-Breakthrough-TTM-Strategy Momentum-Breakthrough-TTM-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9d0aadc6b199f6fb6b.png)


[trans]

## Overview
This strategy is a binary options breakout trading strategy that uses the momentum indicator RSI combined with the Bollinger Bands indicator BB. In terms of time, the TTM indicator is used to determine whether the market is in a consolidation state, thereby improving the reliability of entry.
## Strategy Principle
The basic logic of the strategy is to determine the price breakthrough direction based on the TTM indicator set forming a breakthrough, combined with the Bollinger Bands and RSI indicators. Specifically, the strategy uses a 20-period BB and a 30-period RSI. When the market breaks through and shrinks, determine the opening direction when RSI is in a certain fluctuation range (30-70) and BB has a large breakthrough (0.15 times the fluctuation range). In addition, the strategy also checks the opening direction of the K line before opening a position to avoid unnecessary repeated openings.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Use the TTM indicator to judge the trading status of the market and avoid meaningless transactions in the consolidating market. The collective compression and expansion of TTMS indicators can better judge the main trend direction and provide reference for opening positions.
2. The combined use of RSI and BB can make position opening more reliable. The RSI indicator determines whether the price is overbought or oversold; the BB indicator determines whether the price has experienced a major breakthrough. The combination of the two allows the strategy to make profits in stronger directional markets.
3. The strategy logic takes into account certain optimizations, such as avoiding repeated opening of positions, etc. This can reduce unnecessary switching back and forth between profits and losses to a certain extent.
## Risk Analysis
This strategy mainly involves the following risks:
1. Risk of breakthrough failure. When the TTM indicator is not accurate in judging the trend, RSI and BB may still have false breakthroughs. At this time, the strategy opens a position based on the indicator list, and may eventually be trapped. To control this risk, you can consider reducing the position size.
2. When the market fluctuates, it is easy to cause losses. When the market is in a state of shock, the performance of the TTM indicator is not ideal. The RSI and BB indicators can also produce multiple false signals. At this time, it is very easy to cause losses. To control this risk, avoid using this strategy in obviously volatile markets.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize TTM indicator parameters and adjust the length and factor of the indicator. This can improve the TTM indicator's judgment of consolidation and breakthroughs.
2. Optimize the parameters of RSI and BB. Appropriately shortening the number of cycles may lead to more timely and accurate breakthrough signals. At the same time, the channel bandwidth of BB can also be tested with different values.
3. Add stop loss logic. This strategy does not set a stop loss level. To prevent a single loss from being too large, you can consider adding a trailing stop loss or an expected stop loss.
4. Can test different variety parameters. The current strategy runs on the 1-minute line. For other parameters (such as 5 minutes), the indicator parameters can be retested and optimized to obtain better parameter combinations.
## Summarize
This strategy is a binary option strategy that uses TTM to determine the accuracy of the trend, and combines RSI and BB to determine the breakthrough direction. Compared with simple breakthrough strategies, its entry timing and indicator parameter optimization have more advantages and can increase the probability of profit. However, this strategy also has certain risks of failure and adaptability to market shocks. This requires us to adjust the position size during use and avoid using it in volatile markets. With further parameter and stop loss optimization, this strategy can become a reliable options trading strategy.
||

## Overview  

This is a binary option breakthrough trading strategy that utilizes the momentum indicator RSI combined with the Bollinger Bands indicator BB. In terms of timeliness, the TTM indicator is used to determine whether the market is in a consolidation state, thereby improving the reliability of entry.

## Principle  

The basic logic of the strategy is to determine the breakthrough direction based on Bollinger Bands and the RSI indicator under the condition that the TTM indicator set forms a breakthrough. Specifically, the strategy uses 20 periods of BB and 30 periods of RSI. When the market breaks through the squeeze, it determines the opening direction when the RSI is within a certain fluctuation range (30-70) and the BB has a large breakthrough (0.15 times the fluctuation range). In addition, the strategy also checks the opening direction of the previous K-line before opening a position to avoid unnecessary repeated opening.

## Advantages  

The main advantages of this strategy are:  

1. Using the TTM indicator to judge the trading state of the market and avoid meaningless trading in the consolidating market. The compression and expansion of the TTMS indicator can better determine the main trend direction and provide a reference for opening positions.

2. The combination of RSI and BB can make opening positions more reliable. The RSI indicator judges whether prices are overbought or oversold; while the BB indicator judges whether prices have occurred a major breakthrough. The combination of the two makes the strategy profit from strong directional trends.

3. The strategy logic considers certain optimizations such as avoiding repeated opening. This can reduce unnecessary profit and loss switching to some extent.

## Risk Analysis   

The main risks of this strategy are:

1. Breakdown failure risk. When the TTM indicator does not accurately judge the trend, RSI and BB may still have false breakouts. At this time, the strategy opens positions based on the indicators, and may eventually be trapped. To control this risk, consider reducing the size of the position.

2. It is easy to lose when the market oscillates. When the market is in an oscillating state, the performance of the TTM indicator is not ideal. RSI and BB indicators may also give multiple false signals. At this time it is very easy to form losses. To control this risk, avoid using this strategy in obvious oscillating markets.

## Optimization  

The strategy can be optimized in the following aspects:  

1. Optimize the parameters of the TTM indicator to adjust the length and factors of the indicator. This can improve TTM's judgment on consolidation and breakthrough.

2. Optimize RSI and BB parameters. Appropriately shortening cycle numbers may obtain more timely and precise breakthrough signals. At the same time, the bandwidth of the BB channel can also test different values.  

3. Increase stop loss logic. Since the strategy does not set a stop loss, to prevent a single loss from being too large, consider adding a moving stop loss or expected stop loss.

4. Different varieties of parameters can be tested. The current strategy runs on 1 minute charts. For other varieties of parameters (such as 5 minutes), indicator parameters can be retested and optimized to obtain better parameter combinations.  

## Conclusion   

This strategy utilizes TTM to determine trend accuracy and uses RSI and BB to determine breakthrough directions. Compared with simple breakthrough strategies, its entry timing and indicator parameter optimization are more advantageous, which can increase profitability. But this strategy also poses certain risks of failure and adaptability issues in oscillating markets. This requires us to adjust position sizing during use and avoid using it in oscillating markets. With further parameter and stop loss optimization, this strategy can become a reliable option trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Length|
|v_input_2|50|length|
|v_input_3|0.2|Mult Factor|
|v_input_4|0.1|alertLevel|
|v_input_5|0.75|impulseLevel|
|v_input_6|false|showRange|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-14 00:00:00
end: 2023-11-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy (title="EA_Binary Option Spfrat Strategy", shorttitle="Spyfrate_Binary Option 5min", overlay=false, pyramiding=1999, initial_capital=60000, currency=currency.USD)

// TTM Squeeze code
lengthttm = input(title="Length",  defval=20, minval=0) 
bband(lengthttm, mult) =>
	sma(close, lengthttm) + mult * stdev(close, lengthttm)
keltner(length, mult) =>
	ema(close, lengthttm) + mult * ema(tr, lengthttm)

e1 = (highest(high, lengthttm) + lowest(low, lengthttm)) / 2 + sma(close, lengthttm)
osc = linreg(close - e1 / 2, lengthttm, 0)
diff = bband(lengthttm, 2) - keltner(lengthttm, 1)
osc_color = osc[1] < osc[0] ? osc[0] >= 0 ? #00ffff : #cc00cc : osc[0] >= 0 ? #009b9b : #ff9bff
mid_color = diff >= 0 ? green : red
conso = diff >= 0?1:0

//plot(osc, color=osc_color, style=histogram, linewidth=2)
//plot(0, color=mid_color, style=circles, linewidth=3)

// BB Init
source = close
length = input(50, minval=1)
mult = input(0.2, title="Mult Factor", minval=0.001, maxval=50)
alertLevel=input(0.1)
impulseLevel=input(0.75)
showRange = input(false, type=bool)

//RSI CODE
src = close, 
up = rma(max(change(src), 0), 30)
down = rma(-min(change(src), 0), 30)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))

//BB CODE
basis = sma(source, length)
dev = mult * stdev(source, length)
upper = basis + dev
lower = basis - dev
bbr = source>upper?(((source-upper)/(upper-lower))/10): source<lower?(((source-lower)/(upper-lower))/10) : 0.05
bbi = bbr - nz(bbr[1]) 
//Rule
long1 = rsi>50.5 and rsi<70 and  bbi>0.15  and osc>0.00100 and conso>0
short1 = rsi<49.5 and rsi>30 and  bbi<-0.15 and osc<-0.00100 and conso>0
//
long = long1[1] == 0 and long1 == 1
short = short1[1] == 0 and short1 == 1
longclose = long[5] == 1
shortclose = short[5] == 1

//Alert

strategy.entry("short", strategy.short, when=short)
strategy.entry("long", strategy.long, when=long)
plot(long,"long",color=green,linewidth=1)
plot(short,"short",color=red,linewidth=1)
strategy.close("long",when=longclose)
strategy.close("short",when=shortclose)

//strategy.exit(id="long",qty = 100000,when=longclose)
//strategy.exit(id="short",qty = 100000,when=shortclose)
plot(longclose,"close",color=blue,linewidth=1)
plot(shortclose,"close",color=orange,linewidth=1)
//strategy.exit(id="Stop", profit = 20, loss = 100)
```

> Detail

https://www.fmz.com/strategy/432788

> Last Modified

2023-11-21 15:07:38
