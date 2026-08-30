
> Name

Comprehensive-Futures-Automated-Trading-Strategy-for-Both-Long-and-Short
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/65bf54e6de61b39d0b4e69b173d0d7939c8efa27ad110a08ee0845fdea710cd7.png)
[trans]

This strategy is an innovative **comprehensive long and short automatic futures trading strategy** that integrates multiple indicators such as SuperTrend, QQE and Trend Indicator A-V2 to automatically discover trading signals and conduct long and short transactions. This strategy aims to explore the main trends of the market and obtain stable returns while controlling risks.
**Strategy Principle**
This strategy is mainly based on three parts:
1. The SuperTrend indicator is responsible for determining the main trend direction of the market. When the price crosses the upper turning line, it is bullish, and when it breaks below the lower turning line, it is bearish.
2. The QQE indicator combines with RSI to determine overbought and oversold conditions. The dynamic upper and lower limits are calculated based on the average and standard deviation of RSI. When RSI is higher than the upper limit, it is an overbought signal, and when RSI is lower than the lower limit, it is an oversold signal.
3. The Trend Indicator A-V2 indicator determines the trend by calculating the position of the EMA fast and slow lines. If the fast line is higher than the slow line, it is a bullish signal.
When judging the market direction, when SuperTrend is bullish, and QQE is judged not to be oversold, and A-V2 is bullish, a long signal is issued to enter the market; when SuperTrend is bearish, and QQE is judged not to be overbought, and A-V2 is bearish, a short signal is issued to enter the market.
**Strategic Advantages**
1. Use multiple indicators comprehensively to make trading decisions more reliable and reduce false signals.
2. It can realize automatic discovery of trading signals without manual intervention and judgment, reducing human errors.
3. Use the organic combination of indicators to discover signals while controlling risks to achieve stable profits.
4. Parameters are adjustable and users can personalize strategies according to their own preferences.
5. Support unilateral, multiple or bilateral transactions, and the transaction is flexible.
**Risks and Solutions**
1. Under special market conditions, the indicator may send out wrong signals, which can be reduced by optimizing the indicator parameters.
2. Transaction costs and slippage may affect the profit margin of the strategy, which can be optimized by implementing a stop-loss and stop-profit mechanism.
3. Improper setting of indicator parameters may lead to poor strategy performance. You can try different parameters to find the best configuration.
**Optimization direction**
1. Add machine learning algorithms to automatically optimize indicator parameters based on historical data to make the strategy more intelligent.
2. Combine more market microstructure factors, such as trading volume, external market data and other data to discover more effective trading signals.
3. Apply high-frequency trading technology and automatically submit orders through algorithm models for transaction execution.
**Summarize**
This strategy integrates multiple indicators to judge the market structure and achieve stable profits while controlling risks. It takes into account both the trend direction and overbought and oversold conditions, making trading decisions more detailed. There is still a lot of room for optimization, and strategy performance can be further improved from aspects such as parameter optimization, structure optimization, and execution optimization.
||

This strategy is an innovative **Comprehensive Futures Automated Trading Strategy for Both Long and Short**. It integrates SuperTrend, QQE and Trend Indicator A-V2 to automatically discover trading signals and make long/short trades. This strategy aims to identify main market trends and achieve steady profits with good risk control.  

**Strategy Principle**   

The strategy consists of three main parts:  

1. SuperTrend indicator determines the main market trend. When price breaks above the up trendline, it indicates an uptrend. When price breaks below the down trendline, it indicates a downtrend.   

2. QQE indicator combines RSI to identify overbought/oversold status. Dynamic overbought/oversold levels are calculated based on RSI average and standard deviation. RSI above upper level indicates overbought signal and RSI below lower level indicates oversold signal.   

3. Trend Indicator A-V2 judges the trend by comparing fast and slow EMA lines. When fast EMA is higher than slow EMA, it sends a buy signal.  

When judging market direction, long signals are triggered when SuperTrend shows uptrend, QQE not oversold and A-V2 buy signal occurs. Short signals are triggered when opposite conditions occur.   

**Advantages**  

1. Using multiple indicators improves reliability and reduces false signals. 

2. Automated signal discovery without manual interference reduces human errors.   

3. Organic combination of indicators provides effective risk control while discovering trading opportunities.  

4. Customizable parameters to meet users' needs.   

5. Support both long-only and long/short trading for flexibility.  

**Risks and Solutions**

1. Indicators may generate false signals under extreme market conditions. Fine-tune parameters to minimize such cases.  

2. Transaction costs and slippage could erode profits. Optimize with stop loss/take profit.

3. Inadequate parameter setup leads to poor performance. Try different values to find optimal configuration.  

**Optimization Directions**  

1. Increase machine learning to auto optimize parameters based on historical data.

2. Incorporate more market micro-structure factors like volume to discover better signals.  

3. Implement high frequency trading techniques to auto submit orders.

**Conclusion**  

The strategy combines indicators to assess market structure and achieves steady profits under risk control. It considers both trend direction and overbought/oversold status for nuanced trading decisions. Much room remains for parameter optimization, logic improvements and execution enhancements to further lift strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|One-sided|
|v_input_2|9|ST ATR Period|
|v_input_3|3.9|ST ATR Multiplier|
|v_input_4_hl2|0|ST Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_5|6|QQE RSI Length|
|v_input_6|5|QQE RSI Smoothing|
|v_input_7|3|QQE Fast Factor|
|v_input_8|3|QQE Thresh-hold|
|v_input_9_close|0|QQE RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_10|52|TIA-V2 EMA Period|

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
//author：盧振興 芙蓉中華中學畢業 育達科技大學畢業碩士
//參考資料 : QQE MOD By:Mihkel00 ,SuperTrend By:KivancOzbilgic , TrendIndicator A-V2 By:Dziwne

strategy("綜合交易策略", shorttitle="Comprehensive Strategy", overlay=true)

// 添加單邊或多空參數
OnlyLong = input(true, title="單邊")

// SuperTrend 参数
PeriodsST = input(9, title="ST ATR Period")
MultiplierST = input(3.9, title="ST ATR Multiplier")
srcST = input(hl2, title="ST Source")

atrST = atr(PeriodsST)
upST = srcST - (MultiplierST * atrST)
upST := close[2] > upST[1] ? max(upST, upST[1]) : upST
dnST = srcST + (MultiplierST * atrST)
dnST := close[2] < dnST[1] ? min(dnST, dnST[1]) : dnST
trendST = 1
trendST := nz(trendST[1], trendST)
trendST := trendST == -1 and close[2] > dnST[1] ? 1 : trendST == 1 and close[2] < upST[1] ? -1 : trendST

// QQE 参数
RSI_PeriodQQE = input(6, title='QQE RSI Length')
SFQQE = input(5, title='QQE RSI Smoothing')
QQE = input(3, title='QQE Fast Factor')
ThreshHoldQQE = input(3, title="QQE Thresh-hold")
srcQQE = input(close, title="QQE RSI Source")

Wilders_PeriodQQE = RSI_PeriodQQE * 2 - 1

RsiQQE = rsi(srcQQE, RSI_PeriodQQE)
RsiMaQQE = ema(RsiQQE, SFQQE)
AtrRsiQQE = abs(RsiMaQQE[1] - RsiMaQQE)
MaAtrRsiQQE = ema(AtrRsiQQE, Wilders_PeriodQQE)
darQQE = ema(MaAtrRsiQQE, Wilders_PeriodQQE) * QQE

basisQQE = sma(RsiMaQQE - 50, 50)
devQQE = 0.35 * stdev(RsiMaQQE - 50, 50)
upperQQE = basisQQE + devQQE
lowerQQE = basisQQE - devQQE

qqeCondition = RsiMaQQE[1] - 50 > upperQQE[1] ? true : RsiMaQQE[1] - 50 < lowerQQE[1] ? false : na

// Trend Indicator A-V2 参数
ma_periodA_V2 = input(52, title="TIA-V2 EMA Period")
oA_V2 = ema(open, ma_periodA_V2)
cA_V2 = ema(close, ma_periodA_V2)
trendIndicatorAV2Condition = cA_V2[1] >= oA_V2[1] ? true : false

// 综合交易逻辑
longCondition = trendST == 1 and qqeCondition and trendIndicatorAV2Condition
shortCondition = trendST == -1 and not qqeCondition and not trendIndicatorAV2Condition

// 针对多单的开平仓逻辑
if (OnlyLong)
    if (longCondition)
        strategy.entry("Buy", strategy.long)        
    else
        strategy.close("Buy")

// 多空都做时的逻辑
if (not OnlyLong)
    if (longCondition)
        strategy.entry("Buy", strategy.long)
    else if (shortCondition)
        strategy.entry("Sell",strategy.short)

    // 添加多空平仓逻辑
    if (not longCondition)
        strategy.close("Buy")
    if (not shortCondition)
        strategy.close("Sell")

// 可视化信号
plotshape(series=longCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=shortCondition and not OnlyLong, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

```

> Detail

https://www.fmz.com/strategy/441988

> Last Modified

2024-02-18 14:25:04
