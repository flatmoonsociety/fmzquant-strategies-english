
> Name

Pivot-Reversal-Strategy-with-Pivot-Exit - Trading strategy based on pivot point reversal and exit
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/09d9f357919841aa3996a3d5617b42c6d604460d733c381986d50a40066034a5.png)

[trans]
#### Overview
This strategy is based on pivot points (Pivot Points) to identify market reversal points and trade based on them. When the market appears a pivot point high (Pivot High) within the 4 K lines on the left, the strategy opens a long position; when the market appears a pivot point low (Pivot Low) within the 4 K lines on the left, the strategy opens a short position. The stop loss of the strategy is set at the minimum price change unit (syminfo.mintick) above and below the opening price. There are two exit conditions for the strategy: 1) Close the position when the next pivot point in the opposite direction appears; 2) Close the position when the floating loss reaches 30%.
#### Strategy Principle
1. Use the ta.pivothigh() and ta.pivotlow() functions to calculate the pivot point high point (swh) and low point (swl) within the range of 4 K lines on the left and 2 K lines on the right.
2. When the pivot point high exists (swh_cond), update the highest price (hprice), and when the current highest price is higher than the previous highest price, open the long entry condition (le).
3. When the long entry condition (le) is established, open a long position at the position of one minimum change unit (syminfo.mintick) above the pivot point high.
4. Similar to long, when the pivot point low exists (swl_cond), the lowest price (lprice) is updated, and when the current lowest price is lower than the previous lowest price, the short entry condition (se) is enabled.
5. When the short entry condition (se) is established, open a short position at the position of one minimum change unit (syminfo.mintick) below the pivot point low.
6. In the exitAtNextPivot() function, if you hold a long position, the stop loss will be one minimum unit of movement below the low of the next pivot point; if you hold a short position, the stop loss will be one minimum unit of movement above the high of the next pivot point.
7. In the exitIfProfitLessThanThirtyPercent() function, calculate the profit and loss percentage of long and short positions. If the loss exceeds 30%, the position will be closed.
#### Strategic Advantages
1. The pivot point can better reflect the support and pressure position of the market. It is a commonly used technical analysis indicator and has a certain degree of market recognition.
2. Entering the market when the pivot point breaks through can capture the opportunity of market reversal.
3. Two exit conditions are set, one is a technical exit based on the next pivot point in the opposite direction, and the other is a risk-controlled exit based on the loss percentage, which can control the strategy retracement to a certain extent.
#### Strategy Risk
1. The pivot point indicator itself also has certain hysteresis and frequent signal problems, and may perform poorly in volatile markets.
2. The fixed calculation parameters of 4 K lines and 2 K lines may not be suitable for all market conditions and lack certain adaptability and flexibility.
3. The stop loss position is close to the entry price (one minimum unit of change) and may be thrown away when the market fluctuates violently.
4. The setting of stop loss after 30% loss may be too loose, and the retracement range is too large.
#### Strategy optimization direction
1. You can try to use other types of pivot point indicators, such as factor-type pivot points, weighted pivot points, etc., to improve the sensitivity and real-time performance of the indicator.
2. The number of left and right K lines can be used as input parameters, and the best value can be found through parameter optimization.
3. The stop loss position can be optimized to ATR or percentage stop loss. The former can be adaptively adjusted as market volatility changes, while the latter can limit risks within a controllable range.
4. The 30% loss closing conditions can be tightened to reduce strategy retracement. In addition, you can also increase the profit percentage closing conditions to manage floating profits and losses at the same time.
5. Other filtering conditions can be superimposed on the pivot point breakthrough, such as trend filtering, volatility filtering, etc., to improve signal quality.
#### Summary
This strategy builds a two-way trading system based on the pivot point indicator, and captures market reversal opportunities by going long at the high point and short at the low point of the pivot point. The strategy has a certain theoretical basis and practical value, but due to the limitations of the pivot point indicator itself, the strategy may face some risks and challenges in actual operation. By optimizing the pivot point indicator type, parameters, filter conditions, take profit and stop loss, etc., it is expected to further improve the robustness and profitability of this strategy.
|| 

#### Overview
This strategy uses Pivot Points to identify market reversal points and make trading decisions based on them. When a Pivot High is formed within the last 4 candles on the left, the strategy enters a long position; when a Pivot Low is formed within the last 4 candles on the left, the strategy enters a short position. The stop loss is set at one tick size (syminfo.mintick) above or below the entry price. There are two exit conditions: 1) exit when the next opposite pivot point appears; 2) exit when the floating loss reaches 30%.

#### Strategy Principles
1. Use ta.pivothigh() and ta.pivotlow() functions to calculate the Pivot High (swh) and Pivot Low (swl) within the range of 4 candles on the left and 2 candles on the right.
2. When a Pivot High exists (swh_cond), update the highest price (hprice), and when the current high is higher than the previous high, enable the long entry condition (le).
3. When the long entry condition (le) is met, enter a long position at one tick size (syminfo.mintick) above the Pivot High.
4. Similarly, when a Pivot Low exists (swl_cond), update the lowest price (lprice), and when the current low is lower than the previous low, enable the short entry condition (se).
5. When the short entry condition (se) is met, enter a short position at one tick size (syminfo.mintick) below the Pivot Low.
6. In the exitAtNextPivot() function, if holding a long position, set the stop loss at one tick size below the next Pivot Low; if holding a short position, set the stop loss at one tick size above the next Pivot High.
7. In the exitIfProfitLessThanThirtyPercent() function, calculate the profit and loss percentage for long and short positions, and close the position if the loss exceeds 30%.

#### Strategy Advantages
1. Pivot Points can well reflect the support and resistance levels in the market, and are a commonly used technical analysis indicator with certain market recognition.
2. Entering at the breakout of Pivot Points can capture market reversal opportunities.
3. Two exit conditions are set, one based on the next opposite pivot point for technical exit, and the other based on loss percentage for risk control exit, which can control the strategy drawdown to a certain extent.

#### Strategy Risks
1. The Pivot Point indicator itself has certain lag and frequent signal issues, and may not perform well in a fluctuating market.
2. The fixed calculation parameters of 4 candles and 2 candles may not be applicable to all market conditions, lacking certain adaptability and flexibility.
3. The stop loss is set close to the entry price (one tick size), which may be thrown away during violent market fluctuations.
4. The 30% loss stop setting may be too loose, with a large drawdown amplitude.

#### Strategy Optimization Directions
1. Try using other types of Pivot Point indicators, such as Factor Pivot Points, Weighted Pivot Points, etc., to improve the sensitivity and timeliness of the indicators.
2. The number of left and right candles can be used as input parameters, and the optimal values can be found through parameter optimization.
3. The stop loss position can be optimized to ATR or percentage stop loss. The former can adaptively adjust with changes in market volatility, while the latter can limit risks within a controllable range.
4. The 30% loss stop condition can be tightened to reduce strategy drawdown. In addition, a profit percentage stop condition can be added to manage both floating profits and losses.
5. Other filtering conditions, such as trend filtering and volatility filtering, can be superimposed on the basis of Pivot Point breakout to improve signal quality.

#### Summary
This strategy builds a bi-directional trading system based on the Pivot Point indicator, capturing market reversal opportunities by going long at Pivot Highs and short at Pivot Lows. The strategy has certain theoretical basis and practical value, but due to the limitations of the Pivot Point indicator itself, the strategy may face some risks and challenges in actual operation. By optimizing the Pivot Point indicator type, parameters, filtering conditions, stop loss and profit taking, etc., it is expected to further improve the robustness and profitability of the strategy.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|leftBars|
|v_input_2|2|rightBars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-04-24 00:00:00
end: 2024-04-29 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Pivot Reversal Strategy with Pivot Exit", overlay=true)

leftBars = input(4)
rightBars = input(2)

var float dailyEquity = na

// Reset equity to $10,000 at the beginning of each day
isNewDay = ta.change(time("D")) != 0
if (isNewDay)
    dailyEquity := 10000

// Calculate pivot highs and lows
swh = ta.pivothigh(leftBars, rightBars)
swl = ta.pivotlow(leftBars, rightBars)

// Define long entry condition
swh_cond = not na(swh)
hprice = 0.0
hprice := swh_cond ? swh : hprice[1]
le = false
le := swh_cond ? true : (le[1] and high > hprice ? false : le[1])

// Enter long position if long entry condition is met
if (le)
    strategy.entry("PivRevLE", strategy.long, comment="EnterLong", stop=hprice + syminfo.mintick)

// Define short entry condition
swl_cond = not na(swl)
lprice = 0.0
lprice := swl_cond ? swl : lprice[1]
se = false
se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])

// Enter short position if short entry condition is met
if (se)
    strategy.entry("PivRevSE", strategy.short, comment="EnterShort", stop=lprice - syminfo.mintick)

// Exit condition: Exit at the next pivot point
exitAtNextPivot() =>
    if strategy.opentrades > 0
        if strategy.position_size > 0
            // Exiting long position at next pivot low
            if not na(swl)
                strategy.exit("ExitLong", "PivRevLE", stop=swl - syminfo.mintick)
        else
            // Exiting short position at next pivot high
            if not na(swh)
                strategy.exit("ExitShort", "PivRevSE", stop=swh + syminfo.mintick)

// Call exitAtNextPivot function
exitAtNextPivot()

// Exit condition: Exit if profit is less than 30%
exitIfProfitLessThanThirtyPercent() =>
    if strategy.opentrades > 0
        if strategy.position_size > 0
            // Calculate profit percentage for long position
            profit_percentage_long = (close - strategy.position_avg_price) / strategy.position_avg_price * 100
            // Exiting long position if profit is less than 30%
            if profit_percentage_long < -30
                strategy.close("PivRevLE")
        else
            // Calculate profit percentage for short position
            profit_percentage_short = (strategy.position_avg_price - close) / strategy.position_avg_price * 100
            // Exiting short position if profit is less than 30%
            if profit_percentage_short < -30
                strategy.close("PivRevSE")

// Call exitIfProfitLessThanThirtyPercent function
exitIfProfitLessThanThirtyPercent()

```

> Detail

https://www.fmz.com/strategy/449944

> Last Modified

2024-04-30 15:57:54
