
> Name

Marubozu-Candle-Range-Balance-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1b9c5af1a3a724570cc.png)
[trans]
## Overview
The Marubo Candlestick Equilibrium Strategy is a quantitative trading strategy based on intraday periods. This strategy determines the market trend and looks for trading opportunities by identifying the Marubo candle pattern and examining the equilibrium situation of the candle line segments.
## Strategy Principle
The core logic of this strategy is based on the following points:
1. Identify the Marubo white long and black short candles. Marubo candle is a special candlestick pattern, which refers to a long candle with no shadow line between the opening price and the closing price. It is divided into two types: white long and black short.
2. Calculate the average line segment length of the candle body and compare it with the current candle body length to determine whether the line segment is long or short.
3. Determine whether the candle line segments are balanced, that is, the lengths of the upper shadow line and lower shadow line are approximately equal.
4. Go long when the white long Marubo candle is identified; go short when the black short candle of Marubo is identified.
5. Determine trend reversal by examining the closing conditions of the previous two candles as a closing signal.
This strategy mainly relies on the strong unilateral trend signals provided by the Marubo candle itself and the line segment equilibrium conditions to determine the timing of long and short positions. When the Marubo candle is identified, it indicates that there is a strong unilateral trend in the market; and the line segment equilibrium also confirms the reliability of this trend. Close positions promptly when a strong trend reverses to capture the trend and make profits.
## Advantage Analysis
Marubo candle line equilibrium strategy has the following advantages:
1. Identify high-probability strong trends. Marubo candles themselves provide extremely explosive unilateral market signals.
2. Line segment balancing effectively filters out false breakthroughs and avoids being trapped. When the line segments are unbalanced, it indicates that there may be a risk of false breakthrough, and the trading signal will be skipped.
3. Use the previous two candles to determine trend reversal, and you can capture the trend in time to obtain higher profits.
4. The strategy is simple and clear, easy to understand and implement, and is suitable for beginners to learn.
5. Can be used in any variety and at any time, with strong applicability.
## Risk Analysis
This strategy also has the following risks:
1. Unable to effectively filter the shock trend, there may be more virtual signals and the risk of hold-up in the shock market. It can be alleviated by shortening the position period or increasing the stop loss through parameter adjustment.
2. Depends on parameter settings. Different parameters may cause large differences in results. Parameters can be optimized through backtesting.
3. If you are unable to judge the sub-strong trend and only rely on extreme Marubo candles for judgment, you will miss the sub-strong opportunity. This can be improved by relaxing the line segment equilibrium conditions.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Optimize the line segment ratio threshold for Marubo candle judgment and adjust the recognition sensitivity.
2. Optimize the equilibrium threshold parameters and identify more balanced or unbalanced equilibrium types.
3. Add the comparison between the closing price and the moving average as an auxiliary judgment indicator.
4. Judgment of sudden indicators that increase trading volume.
5. Relax the line segment equilibrium requirements and identify more opportunities for strong Marubo candles.
## Summarize
Marubo's candle line equilibrium strategy explores high-probability unilateral trend opportunities by identifying specific candle patterns and supplementing them with equilibrium judgment. The strategy is simple and easy to understand, with a high winning rate. It is suitable for both novices to learn and advanced traders looking for potential opportunities. Better results can be obtained through some parameter and signal optimization. Overall, it is a very practical daytime quantitative strategy.
||

## Overview

The Marubozu candle range balance strategy is an intraday quantitative trading strategy. It identifies Marubozu candle patterns and examines the balance of candle ranges to determine market trends and find trading opportunities.

## Strategy Principle  

The core logic of this strategy is based on the following points:

1. Identify Marubozu white bullish and black bearish candles. Marubozu candles are special candlestick patterns with no shadows between the open and close prices, divided into white bullish and black bearish types.

2. Calculate the average candle body range and compare it with the current candle body range to determine whether the range is long or short.

3. Determine whether the candle ranges are balanced, that is, whether the upper shadow and lower shadow lengths are roughly equal.

4. Go long when a Marubozu white bullish candle is identified; Go short when a Marubozu black bearish candle is identified.  

5. Use the closing prices of the previous two candles to determine trend reversal as the exit signal.

The strategy relies mainly on the strong one-sided trend signals provided by the Marubozu candles themselves and the balanced range conditions to determine long and short opportunities. When a Marubozu candle is identified, it indicates that the market has a strong one-sided trend. The balanced range situation also confirms the reliability of this trend. Exit positions in a timely manner when the strong trend reverses to capture the trend profit.

## Advantage Analysis   

The Marubozu candle range balance strategy has the following advantages:

1. Identify high-probability strong trends. Marubozu candles themselves provide extremely explosive one-sided price signals.  

2. Balanced range effectively filters false breakouts and avoids traps. When the range is imbalanced, it indicates potential risks of false breakout and will skip the trading signal.

3. Using the previous two candles to determine trend reversal can capture profits from the trend in a timely manner.  

4. The strategy is simple and clear, easy to understand and implement, suitable for beginners.

5. Can be used on any products and timeframes, with strong applicability.

## Risk Analysis   

The strategy also has the following risks:

1. Inability to effectively filter whipsaw markets, with higher risks of false signals and traps in range-bound trends. Can be mitigated by adjusting parameters to shorten holding period or increase stop loss.  

2. Reliance on parameter settings. Different parameters can lead to significantly different results. Parameters can be optimized through backtesting.

3. Inability to identify secondary strong trends, relying solely on extreme Marubozu candles for judgements, thus missing secondary opportunity. Can be improved by relaxing balanced range requirements. 

## Strategy Optimization

The strategy can be optimized in the following aspects:

1. Optimize the threshold percentage of Marubozu determination to adjust identification sensitivity.

2. Optimize balanced threshold parameters to identify more balanced or imbalanced balanced patterns. 

3. Add close price vs moving average comparison as an auxiliary judgement indicator.  

4. Add indicators to determine surges in trading volume.

5. Relax balanced range requirements to identify more secondary strong Marubozu opportunities.   

## Conclusion  

The Marubozu candle range balance strategy identifies high-probability one-sided trend opportunities by recognizing specific candle patterns coupled with balanced judgements. The strategy is simple and clear with high win rate. It is suitable for both beginners to learn and advanced traders to find potential opportunities. Further improvements can be made through signal and parameter optimizations. Overall it is a very practical intraday quantitative strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

strategy(title="Marubozu", shorttitle="Marubozu", overlay=true, initial_capital = 1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent , commission_value=0 )

C_Len = 14 // ema depth for bodyAvg
C_ShadowPercent = 5.0 // size of shadows
C_ShadowEqualsPercent = 100.0
C_DojiBodyPercent = 5.0
C_Factor = 2.0 // shows the number of times the shadow dominates the candlestick body

C_BodyHi = max(close, open)
C_BodyLo = min(close, open)
C_Body = C_BodyHi - C_BodyLo
C_BodyAvg = ema(C_Body, C_Len)
C_SmallBody = C_Body < C_BodyAvg
C_LongBody = C_Body > C_BodyAvg
C_UpShadow = high - C_BodyHi
C_DnShadow = C_BodyLo - low
C_HasUpShadow = C_UpShadow > C_ShadowPercent / 100 * C_Body
C_HasDnShadow = C_DnShadow > C_ShadowPercent / 100 * C_Body
C_WhiteBody = open < close
C_BlackBody = open > close
C_Range = high-low
C_IsInsideBar = C_BodyHi[1] > C_BodyHi and C_BodyLo[1] < C_BodyLo
C_BodyMiddle = C_Body / 2 + C_BodyLo
C_ShadowEquals = C_UpShadow == C_DnShadow or (abs(C_UpShadow - C_DnShadow) / C_DnShadow * 100) < C_ShadowEqualsPercent and (abs(C_DnShadow - C_UpShadow) / C_UpShadow * 100) < C_ShadowEqualsPercent
C_IsDojiBody = C_Range > 0 and C_Body <= C_Range * C_DojiBodyPercent / 100
C_Doji = C_IsDojiBody and C_ShadowEquals

patternLabelPosLow = low - (atr(30) * 0.6)
patternLabelPosHigh = high + (atr(30) * 0.6)

C_MarubozuWhiteBullishNumberOfCandles = 1
C_MarubozuShadowPercentWhite = 5.0
C_MarubozuWhiteBullish = C_WhiteBody and C_LongBody and C_UpShadow <= C_MarubozuShadowPercentWhite/100*C_Body and C_DnShadow <= C_MarubozuShadowPercentWhite/100*C_Body and C_WhiteBody
alertcondition(C_MarubozuWhiteBullish, title = "Marubozu White", message = "New Marubozu White - Bullish pattern detected.")
if C_MarubozuWhiteBullish
    var ttBullishMarubozuWhite = "Marubozu White\nA Marubozu White Candle is a candlestick that does not have a shadow that extends from its candle body at either the open or the close. Marubozu is Japanese for “close-cropped” or “close-cut.” Other sources may call it a Bald or Shaven Head Candle."
    label.new(bar_index, patternLabelPosLow, text="MW", style=label.style_label_up, color = color.blue, textcolor=color.white, tooltip = ttBullishMarubozuWhite)
bgcolor(highest(C_MarubozuWhiteBullish?1:0, C_MarubozuWhiteBullishNumberOfCandles)!=0 ? color.blue : na, offset=-(C_MarubozuWhiteBullishNumberOfCandles-1))

C_MarubozuBlackBearishNumberOfCandles = 1
C_MarubozuShadowPercentBearish = 5.0
C_MarubozuBlackBearish = C_BlackBody and C_LongBody and C_UpShadow <= C_MarubozuShadowPercentBearish/100*C_Body and C_DnShadow <= C_MarubozuShadowPercentBearish/100*C_Body and C_BlackBody
alertcondition(C_MarubozuBlackBearish, title = "Marubozu Black", message = "New Marubozu Black - Bearish pattern detected.")
if C_MarubozuBlackBearish
    var ttBearishMarubozuBlack = "Marubozu Black\nThis is a candlestick that has no shadow, which extends from the red-bodied candle at the open, the close, or even at both. In Japanese, the name means “close-cropped” or “close-cut.” The candlestick can also be referred to as Bald or Shaven Head."
    label.new(bar_index, patternLabelPosHigh, text="MB", style=label.style_label_down, color = color.red, textcolor=color.white, tooltip = ttBearishMarubozuBlack)
bgcolor(highest(C_MarubozuBlackBearish?1:0, C_MarubozuBlackBearishNumberOfCandles)!=0 ? color.red : na, offset=-(C_MarubozuBlackBearishNumberOfCandles-1))

strategy.entry("short",1,when= C_MarubozuBlackBearish)

strategy.entry("long",0,when=C_MarubozuWhiteBullish)

strategy.close("long",when= close[1] < open[1]and close[2] < open[2] and close > open)
strategy.close("short",when= close[1] > open[1]and close[2] > open[2] and close < open)
```

> Detail

https://www.fmz.com/strategy/442641

> Last Modified

2024-02-23 14:23:41
