
> Name

A-Long-Short-Adaptive-Dynamic-Grid-Strategy-Based
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/fae844b19d036faeb58781a76db2c1b661d4a87768242b64f0b9e2b41b2f035e.png)
[trans]
## Overview
This is a long-short adaptive dynamic grid trading strategy written based on Pine Script. The core idea of ​​this strategy is to automatically calculate the upper and lower bounds of a grid based on recent price highs and lows or a simple moving average, and then divide the range into multiple grid lines. When the price touches a certain grid line, a long position will be opened or closed at that position. In this way, the strategy can continuously open and close positions in volatile market conditions and obtain spread profits. At the same time, by dynamically adjusting the grid boundaries, it can also adapt to different market trends.
## Strategy Principle
1. Calculate the upper and lower bounds of the grid. According to the user's choice, the upper and lower bounds can be based on the highest and lowest points of the most recent N K lines, and the expansion or reduction percentage can be set; it can also be based on the simple moving average of the closing prices of the most recent N K lines, and the upper and lower deviation ratios can be set.
2. Generate grid line array. According to the set number of grid lines, the grid range is evenly divided to generate a grid line array corresponding to the price.
3. Enter/Add a position. Traverse the grid lines from bottom to top. If the current closing price is less than the price of a certain grid line and there is no position in that grid line, open a long order at that position. This way, positions will continue to be added when the price hits the higher grid line.
4. Exit/reduce positions. Traverse the grid lines from top to bottom. If the current closing price is greater than a certain grid line price and there is a position one grid line lower, then the long order one grid line lower will be closed. In this way, positions will continue to be reduced when prices fall back.
5. Dynamic adjustment. If you select the dynamic grid function, each K line will recalculate the upper and lower bounds of the grid and the grid line array, so that the grid can continuously adapt as the market changes.
## Advantage Analysis
1. Strong adaptability. Grid trading strategies can adapt to both volatile and trending conditions. In a volatile market, the grid strategy can continue to open and close positions and earn price differences; in a trending market, because the grid follows the price movement, it can also maintain a certain position and obtain trend profits.
2. Risks are controllable. The size of each position opened is determined by the number of grids set, and the single risk exposure is small and controllable. At the same time, since the position will be closed to make a profit when the price hits the upper grid line, potential losses are also hedged to a certain extent.
3. High degree of automation. This strategy can basically run fully automatically and does not require manual intervention. It is suitable for investors who require long-term stable returns.
4. Flexible parameters. Users can flexibly set the number of grid lines, dynamic grid parameters, etc. according to market characteristics to optimize strategy performance.
## Risk Analysis
1. Black swan risk. If there is an extreme market drop and the price jumps directly below the lowest grid line, the strategy will be full and face a large retracement. To reduce this risk, you can set stop loss conditions and close all positions once the loss reaches the threshold.
2. Improper grid parameter settings. If the grid density is too large, the price difference between each opening and closing of a position will be very small, and handling fees may erode most of the income. If the grid width is too large, the proportion of one-time openings will be high and the risk exposure will be large. It is necessary to carefully evaluate the characteristics of the underlying assets and select appropriate grid parameters.
3. Basis risk. This strategy sets the opening and closing conditions based on the current price. In futures and other markets, if the contract price is significantly different from the underlying price, the actual opening and closing price may deviate more from expectations.
## Optimization direction
1. Add trend filtering. The grid strategy performs poorly in unilateral trend markets. Trend indicators can be added as filters. For example, the grid is only enabled when ADX is lower than a certain threshold, and the grid is turned off when the trend is obvious, and only unilateral positions are held.
2. Signal optimization. Other signals can be superimposed on the grid, such as grid + moving average, that is, the grid mainly determines the opening and closing of positions, but the position will be opened when the price crosses a certain moving average, otherwise the position will not be opened. This can reduce the costs caused by frequent opening and closing positions.
3. Position management. The current strategy's position per square is fixed. It can be set to appropriately reduce the position per square when the price is far from the market average price, and increase the position when it is close to the market average price to improve capital utilization efficiency.
4. Adaptive grid density. The grid density is dynamically adjusted according to the price volatility. When the volatility is high, the number of grids can be appropriately increased, and when the volatility is low, the number of grids can be reduced. This can optimize the grid width and improve fund utilization.
## Summarize
Through the adaptive dynamic grid, this strategy can frequently open and close positions in volatile markets to earn price differences, and can also maintain a certain exposure direction in trend markets to obtain trend returns. It is a medium and long-term quantitative strategy with strong adaptability. By properly setting the grid trigger logic and position management, you can achieve steady returns. However, attention should be paid to extreme market conditions and price gap risks, which need to be controlled by setting appropriate stop loss conditions. In addition, there is room for further optimization in parameter settings and risk management. The robustness and profitability of the strategy can be improved by introducing trend filtering, signal overlay, position management, adaptive grid density and other means. In summary, this strategy is based on the basic logic of the grid and adds a dynamic adaptive mechanism, which can provide new ideas and references for medium and long-term quantitative investors.
||

## Overview

This is a long-short adaptive dynamic grid trading strategy based on Pine Script. The core idea of this strategy is to automatically calculate the upper and lower bounds of a grid based on the recent price highs and lows or a simple moving average, and then divide this range evenly into multiple grid lines. When the price reaches a certain grid line, it will open a long position or close a position at that level. In this way, the strategy can continuously open and close positions in a rangebound market to capture the price spread. At the same time, by dynamically adjusting the grid boundaries, it can also adapt to different market trends.

## Strategy Principles

1. Calculate grid boundaries. Based on user choice, the boundaries can be calculated from the highest and lowest points of the recent N candles, with an option to widen or narrow the range by a percentage; or they can be based on the simple moving average of the closing prices of the recent N candles, with an option to set the upward and downward deviation ratios.

2. Generate grid line array. According to the set number of grid lines, divide the grid range evenly to generate an array of grid line prices.

3. Entry/Add position. Traverse the grid lines from bottom to top. If the current closing price is less than a grid line price and there is no position on that grid line, then open a long position at that level. In this way, when the price reaches higher grid lines, it will continue to add positions.

4. Exit/Reduce position. Traverse the grid lines from top to bottom. If the current closing price is greater than a grid line price and there is a position on the grid line below, then close the long position on the lower grid line. In this way, when the price falls back, it will continue to reduce positions.

5. Dynamic adjustment. If the dynamic grid function is selected, the upper and lower bounds of the grid and the grid line array will be recalculated on each candle, so that the grid can constantly adapt as the market changes.

## Advantage Analysis

1. Strong adaptability. The grid trading strategy can adapt to both rangebound and trending markets. In a rangebound market, the grid strategy can continuously open and close positions to earn the price spread; in a trending market, because the grid follows the price movement, it can also maintain a certain position to obtain trend gains.

2. Controllable risk. The position size of each opening is determined by the set number of grids, so the single risk exposure is small and controllable. At the same time, since reaching the upper grid lines will close positions for profit, it also hedges potential losses to a certain extent.

3. High degree of automation. This strategy can basically run fully automatically without manual intervention, which is suitable for investors who need long-term steady returns.

4. Flexible parameters. Users can flexibly set the number of grid lines, dynamic grid parameters, etc. according to market characteristics to optimize strategy performance.

## Risk Analysis

1. Black swan risk. In case of an extreme market crash, if the price directly gaps down below the lowest grid line, the strategy will be fully positions and face a larger drawdown. To reduce this risk, a stop-loss condition can be set to close all positions once the loss reaches a threshold.

2. Improper grid parameter setting. If the grid density is too high, the spread of each open and close will be very small, and transaction costs may erode most of the gains. If the grid width is too large, the one-time opening ratio is high and the risk exposure is large. The characteristics of the underlying asset need to be carefully evaluated to select appropriate grid parameters. 

3. Basis risk. This strategy sets the opening and closing conditions based on the current price. In markets such as futures, if the contract price differs greatly from the underlying price, the actual opening and closing prices may deviate significantly from expectations.

## Optimization Directions

1. Add trend filter. Grid strategies do not perform well in unilateral trending markets. Trend indicators can be added as a filter, such as only enabling the grid when ADX is below a threshold, and closing the grid when the trend is obvious, only holding unilateral positions.

2. Signal optimization. Other signals can be superimposed on the basis of the grid, such as grid + moving average, that is, the opening and closing are mainly determined by the grid, but only open positions when the price crosses a certain moving average, otherwise do not open positions. This can reduce the cost of frequent opening and closing. 

3. Position management. Currently, the position of each grid in the strategy is fixed. It can be set to appropriately reduce the position of each grid when the price is far from the market average price, and increase the position when it is close to the market average price to improve the efficiency of capital utilization.

4. Adaptive grid density. Dynamically adjust the grid density according to price volatility. When volatility is high, the number of grids can be appropriately increased; when volatility is low, the number of grids can be reduced. This can optimize the grid width and improve capital utilization.

## Summary

Through adaptive dynamic grids, this strategy can frequently open and close positions to earn price spreads in rangebound markets, and can also maintain a certain degree of exposure direction in trending markets to obtain trend gains. It is a mid-to-long-term quantitative strategy with strong adaptability. By reasonably setting the grid triggering logic and position management, steady returns can be achieved. However, it is necessary to pay attention to the risks of extreme market conditions and price gaps, which requires setting appropriate stop-loss conditions to control. In addition, there is further room for optimization in parameter setting and risk management. The robustness and profitability of the strategy can be improved by introducing trend filtering, signal superposition, position management, adaptive grid density and other means. In summary, based on the basic logic of grids, this strategy incorporates a dynamic adaptive mechanism, which can provide new ideas and references for mid-to-long-term quantitative investors.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|(?Grid Bounds)Use Auto Bounds?|
|v_input_2|0|(Auto) Bound Source: Hi & Low|Average|
|v_input_3|250|(Auto) Bound Lookback|
|v_input_4|0.1|(Auto) Bound Deviation|
|v_input_5|0.285|(Manual) Upper Boundry|
|v_input_6|0.225|(Manual) Lower Boundry|
|v_input_7|8|(?Grid Lines)Grid Line Quantity|


> Source (PineScript)

``` pinescript
// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © jcloyd

//@version=4
strategy("(IK) Grid Script", overlay=true, pyramiding=14, close_entries_rule="ANY", default_qty_type=strategy.cash, initial_capital=100.0, currency="USD", commission_type=strategy.commission.percent, commission_value=0.1)
i_autoBounds    = input(group="Grid Bounds", title="Use Auto Bounds?", defval=true, type=input.bool)                             // calculate upper and lower bound of the grid automatically? This will theorhetically be less profitable, but will certainly require less attention
i_boundSrc      = input(group="Grid Bounds", title="(Auto) Bound Source", defval="Hi & Low", options=["Hi & Low", "Average"])     // should bounds of the auto grid be calculated from recent High & Low, or from a Simple Moving Average
i_boundLookback = input(group="Grid Bounds", title="(Auto) Bound Lookback", defval=250, type=input.integer, maxval=500, minval=0) // when calculating auto grid bounds, how far back should we look for a High & Low, or what should the length be of our sma
i_boundDev      = input(group="Grid Bounds", title="(Auto) Bound Deviation", defval=0.10, type=input.float, maxval=1, minval=-1)  // if sourcing auto bounds from High & Low, this percentage will (positive) widen or (negative) narrow the bound limits. If sourcing from Average, this is the deviation (up and down) from the sma, and CANNOT be negative.
i_upperBound    = input(group="Grid Bounds", title="(Manual) Upper Boundry", defval=0.285, type=input.float)                      // for manual grid bounds only. The upperbound price of your grid
i_lowerBound    = input(group="Grid Bounds", title="(Manual) Lower Boundry", defval=0.225, type=input.float)                      // for manual grid bounds only. The lowerbound price of your grid.
i_gridQty       = input(group="Grid Lines",  title="Grid Line Quantity", defval=8, maxval=15, minval=3, type=input.integer)       // how many grid lines are in your grid

f_getGridBounds(_bs, _bl, _bd, _up) =>
    if _bs == "Hi & Low"
        _up ? highest(close, _bl) * (1 + _bd) : lowest(close, _bl)  * (1 - _bd)
    else
        avg = sma(close, _bl)
        _up ? avg * (1 + _bd) : avg * (1 - _bd)

f_buildGrid(_lb, _gw, _gq) =>
    gridArr = array.new_float(0)
    for i=0 to _gq-1
        array.push(gridArr, _lb+(_gw*i))
    gridArr

f_getNearGridLines(_gridArr, _price) =>
    arr = array.new_int(3)
    for i = 0 to array.size(_gridArr)-1
        if array.get(_gridArr, i) > _price
            array.set(arr, 0, i == array.size(_gridArr)-1 ? i : i+1)
            array.set(arr, 1, i == 0 ? i : i-1)
            break
    arr

var upperBound      = i_autoBounds ? f_getGridBounds(i_boundSrc, i_boundLookback, i_boundDev, true) : i_upperBound  // upperbound of our grid
var lowerBound      = i_autoBounds ? f_getGridBounds(i_boundSrc, i_boundLookback, i_boundDev, false) : i_lowerBound // lowerbound of our grid
var gridWidth       = (upperBound - lowerBound)/(i_gridQty-1)                                                       // space between lines in our grid
var gridLineArr     = f_buildGrid(lowerBound, gridWidth, i_gridQty)                                                 // an array of prices that correspond to our grid lines
var orderArr        = array.new_bool(i_gridQty, false)                                                              // a boolean array that indicates if there is an open order corresponding to each grid line

var closeLineArr    = f_getNearGridLines(gridLineArr, close)                                                        // for plotting purposes - an array of 2 indices that correspond to grid lines near price
var nearTopGridLine = array.get(closeLineArr, 0)                                                                    // for plotting purposes - the index (in our grid line array) of the closest grid line above current price
var nearBotGridLine = array.get(closeLineArr, 1)                                                                    // for plotting purposes - the index (in our grid line array) of the closest grid line below current price
strategy.initial_capital = 50000
for i = 0 to (array.size(gridLineArr) - 1)
    if close < array.get(gridLineArr, i) and not array.get(orderArr, i) and i < (array.size(gridLineArr) - 1)
        buyId = i
        array.set(orderArr, buyId, true)
        strategy.entry(id=tostring(buyId), long=true, qty=(strategy.initial_capital/(i_gridQty-1))/close, comment="#"+tostring(buyId))
    if close > array.get(gridLineArr, i) and i != 0
        if array.get(orderArr, i-1)
            sellId = i-1
            array.set(orderArr, sellId, false)
            strategy.close(id=tostring(sellId), comment="#"+tostring(sellId))

if i_autoBounds
    upperBound  := f_getGridBounds(i_boundSrc, i_boundLookback, i_boundDev, true)
    lowerBound  := f_getGridBounds(i_boundSrc, i_boundLookback, i_boundDev, false)
    gridWidth   := (upperBound - lowerBound)/(i_gridQty-1)
    gridLineArr := f_buildGrid(lowerBound, gridWidth, i_gridQty)

closeLineArr    := f_getNearGridLines(gridLineArr, close)
nearTopGridLine := array.get(closeLineArr, 0)
nearBotGridLine := array.get(closeLineArr, 1)
```

> Detail

https://www.fmz.com/strategy/445440

> Last Modified

2024-03-19 14:19:28
