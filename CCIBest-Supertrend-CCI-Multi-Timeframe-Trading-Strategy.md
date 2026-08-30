
> Name

Best-Supertrend-CCI-Multi-Timeframe-Trading-Strategy Multi-Timeframe Trading Strategy Based on Supertrend and CCI Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/9b82d1ae785ac6d33e353884d20f301487686ef17ad023db5507d46371ad48d1.png)
[trans]
## Overview
This strategy combines the Super Trend indicator and the Commodity Channel Index (CCI) indicator to achieve a multi-time frame trend tracking and trading signal generation. The main idea of ​​this strategy is to use the CCI indicator to determine the short-term trend direction, and at the same time combine the super trend indicator to determine the medium and long-term trend direction. When the short-term and medium- and long-term trends are consistent, a trading signal is generated.
## Strategy Principle
### CCI indicator determines short-term trends
The CCI indicator can determine overbought and oversold phenomena. When the CCI indicator crosses the 0 axis from bottom to top, it is a long signal, and vice versa, it is a short signal. This strategy uses this characteristic to determine the short-term trend direction.
```
cci_period = input(28, "CCI Period")  
cci = cci(source, cci_period)
ML = input(0, "CCI Mid Line pivot")
```

The above code defines the period and central axis position of the CCI indicator.
```
TrendUp := cci[1] > ML ? max(Up,TrendUp[1]) : Up 
TrendDown := cci[1]< ML ? min(Dn,TrendDown[1]) : Dn
```

This part of the code determines whether cci crosses above the 0 axis. If so, it updates the upper track of the super trend. If it crosses below, it updates the lower track.
### Super trend indicator determines medium and long-term trends
The super trend indicator can determine the direction of the mid- to long-term trend by combining the ATR indicator with price. When the price breaks through the upper track of the super trend, it is a long signal, and when the price breaks through the lower track, it is a short signal.
The calculation formula of the super trend indicator in this strategy is as follows:
```
Up=hl2-(Factor*atr(Pd)) 
Dn=hl2+(Factor*atr(Pd))
```

Among them, Factor and Pd are adjustable parameters.
The Trend variable determines the current direction of the super trend:
```
Trend := cci > ML ? 1: cci < ML ? -1: nz(Trend[1],1)
```

### Integrate CCI and super trends
By integrating the CCI indicator and the super trend indicator, this strategy realizes trend judgment in multiple time frames. The CCI indicator captures short-term trends, and the super trend indicator determines medium- and long-term trends.
When the two directions are consistent, a more reliable trading signal is generated.
```
isLong  = st_trend == 1
isShort = st_trend == -1
```

The entry time is in the same direction as short-term and mid- to long-term, and the exit time is in the opposite direction of short-term and mid- to long-term.
## Strategic Advantages
### Multiple time frame judgment
This strategy integrates both short-term and medium- and long-term trend judgment indicators to make trading signals more reliable.
### Parameters adjustable
The Factor parameter in the super trend indicator and the cci_period of the CCI indicator can be adjusted according to the market, making the strategy more flexible.
### Simple and clear
The strategy structure is simple and clear, easy to understand and implement, and is very suitable for beginners in quantitative trading.
### Wide range of application
It can be applied to stocks, foreign exchange, cryptocurrency and other markets, and can also be adapted to different varieties according to parameter settings.
## Strategic risks and solutions
### Prices fluctuate greatly
When prices fluctuate wildly, many false signals can appear. The Factor parameters of the super trend can be appropriately adjusted to reduce the trading frequency of the strategy.
### Following the strong is not enough
The super trend itself is not enough to follow the strong trend. You can consider combining it with the momentum indicator to track the trend during the trend acceleration stage.
### Stop loss strategy
This strategy does not set a stop loss. Trails stop loss can be set based on the size of the ATR indicator.
## Strategy optimization direction
### Market Relevance
According to the characteristics of different markets, adjust the parameters of super trend and CCI to improve the stability of the strategy.
### Momentum indicator combination
Combined with momentum indicators such as MACD and KDJ, you can track the trend during the trend acceleration stage and obtain higher returns.
### Integrated Learning
Optimize strategy parameters and trading rules using machine learning and ensemble learning methods.
## Summarize
This strategy successfully combines the super trend and CCI indicators to achieve trend judgment under multiple time frames. The strategy is simple and easy to understand, the parameters are adjustable, and the profit potential is large. It can be further optimized through parameter adjustment, stop loss and integrated learning to make it a reliable, stable and efficient trading strategy.
|| 

## Overview

This strategy integrates the Supertrend indicator and the Commodity Channel Index (CCI) to realize a multi timeframe trend tracking and trade signal generation. The main idea is to use the CCI indicator to judge short-term trend direction while combining the Supertrend indicator to determine medium-to-long term trend direction. Trading signals are generated when the short-term and medium-to-long term trends align.

## Strategy Logic  

### CCI Indicator for Short-term Trend

The CCI indicator can identify overbought and oversold scenarios. An upward crossover of the 0 line is a bullish signal while a downward one is a bearish signal. This strategy utilizes this feature to determine short-term trend direction.

```
cci_period = input(28, "CCI Period")
cci = cci(source, cci_period)  
ML = input(0, "CCI Mid Line pivot")
```

The above code defines the CCI period and mid line position.

``` 
TrendUp := cci[1] > ML ? max(Up,TrendUp[1]) : Up
TrendDown := cci[1]< ML ? min(Dn,TrendDown[1]) : Dn  
```

This code checks if cci crosses above/below the 0 line to update Supertrend's upper/lower band.

### Supertrend for Medium-to-long Term Trend  

The Supertrend indicator combines ATR with price to determine mid-to-long term trends. An upward penetration of the upper band signals an uptrend while a downward one signals downtrend.

Supertrend is calculated as:  

```
Up=hl2-(Factor*atr(Pd))
Dn=hl2+(Factor*atr(Pd)) 
```

Where Factor and Pd are adjustable parameters.

The Trend variable determines current Supertrend direction:

```
Trend := cci > ML ? 1: cci < ML ? -1: nz(Trend[1],1)  
```

### Integrate CCI and Supertrend

By integrating CCI and Supertrend, this strategy realizes multi timeframe trend judgment. CCI captures short-term swings while Supertrend focuses on bigger moves. 

When directions agree, more reliable trading signals are generated.

```  
isLong = st_trend == 1 
isShort = st_trend == -1
```

Entries when short and medium-term align, exits when directions disagree.


## Advantages

### Multi Timeframe Judgment  

Integrates short-term and mid-term indicators for more reliable signals.


### Customizable Parameters

Supertrend's Factor and CCI Period can be adjusted for market conditions.   


### Simple and Clear  

Simple logic and easy to understand, great for beginners.

 
### Wide Applicability

Applicable to stocks, forex, crypto by parameter tuning.


## Risks and Solutions

### Price Whipsaw

Many false signals may occur when prices fluctuate violently. Increase Supertrend's Factor to lower frequency.


### Lagging Strong Moves  

Supertrend has some lagging. Combine momentum indicators to track accelerating trends. 


### No Stop Loss

Add stop loss based on ATR for risk control.


## Optimization Directions   

### Market Correlation

Adjust parameters for different markets.

### Momentum Combination  

Combine with MACD, KDJ etc. to catch strong momentum moves.

### Machine Learning  

Utilize AI and ensemble methods to optimize parameters and rules.


## Conclusion  

This strategy successfully combines Supertrend and CCI for multi timeframe trend tracking. Simple logic, good reward potential and customizability. Can further improve via parameter tuning, stop loss, and machine learning to become a solid trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|28|CCI Period|
|v_input_3|false|CCI Mid Line pivot|
|v_input_4|3|[ST] Factor|
|v_input_5|3|[ST] PD|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-10 00:00:00
end: 2024-01-17 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
//@author=Daveatt

StrategyName = "Best Supertrend CCI Strategy"
ShortStrategyName = "Best Supertrend CCI Strategy"

strategy(title=StrategyName, shorttitle=ShortStrategyName, overlay=true )

//////////////////////////
//* COLOR CONSTANTS *//
//////////////////////////

AQUA = #00FFFFFF
BLUE = #0000FFFF
RED  = #FF0000FF
LIME = #00FF00FF
GRAY = #808080FF
DARKRED   = #8B0000FF
DARKGREEN = #006400FF
GOLD = #FFD700
WHITE = color.white

// Plots
GREEN_LIGHT     = color.new(color.green, 40)
RED_LIGHT       = color.new(color.red, 40) 
BLUE_LIGHT      = color.new(color.aqua, 40)
PURPLE_LIGHT    = color.new(color.purple, 40) 

source = input(close)

///////////////////////////////////////////////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////
/////////////////////////////////// CCI /////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////

cci_period = input(28, "CCI Period")
cci = cci(source, cci_period)
//UL = input(80, "Upper level")
//LL = input(20, "Lower Level")
ML = input(0, "CCI Mid Line pivot")

///////////////////////////////////////////////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////
///////////////////////////// SUPERTREND /////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////

Factor=input(3,title="[ST] Factor", minval=1,maxval = 100, type=input.float)
Pd=input(3, title="[ST] PD", minval=1,maxval = 100)

///////////////////////////////////////////////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////
/////////////////////// SUPERTREND DETECTION //////////////////////////////////
///////////////////////////////////////////////////////////////////////////////
///////////////////////////////////////////////////////////////////////////////

f_supertrend(Factor, Pd) =>

    Up=hl2-(Factor*atr(Pd))
    Dn=hl2+(Factor*atr(Pd))
    
    TrendUp = 0.0
    TrendUp := cci[1] > ML ? max(Up,TrendUp[1]) : Up
    TrendDown = 0.0
    TrendDown := cci[1]< ML ? min(Dn,TrendDown[1]) : Dn
    Trend = 0.0
    Trend := cci > ML ? 1: cci < ML ? -1: nz(Trend[1],1)
    Tsl = Trend==1? TrendUp: TrendDown

    [Trend, Tsl]

[st_trend, st_tsl] = f_supertrend(Factor, Pd)

// Plot the ST
linecolor = close >= st_tsl ? color.green : color.red
plot(st_tsl, color = linecolor , linewidth = 3,title = "SuperTrend", transp=0)

isLong  = st_trend == 1
isShort = st_trend == -1

longClose   = isLong[1] and isShort
shortClose  = isShort[1] and isLong

strategy.entry("Long", 1, when=isLong)
strategy.close("Long", when=longClose )

strategy.entry("Short", 0,  when=isShort)
strategy.close("Short", when=shortClose )

```

> Detail

https://www.fmz.com/strategy/439227

> Last Modified

2024-01-18 15:09:33
