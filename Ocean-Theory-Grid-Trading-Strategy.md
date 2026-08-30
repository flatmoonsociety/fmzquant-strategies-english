
> Name

Ocean-Theory-Grid-Trading-StrategyOcean-Theory-Grid-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy uses the grid trading method in ocean theory to evenly distribute grid lines within a set price range, and perform buying and selling operations based on the relationship between price and grid lines. The strategy has the characteristics of automatically calculating grid price ranges and evenly distributing grid lines, which can effectively control risks.
## Strategy Principle
The strategy first calculates the upper and lower limits of the price grid based on user selection or default settings, that is, the highest and lowest prices of the grid. There are two calculation methods, one is to find the highest price and lowest price within the backtest period, and the other is to calculate the moving average of a certain period. Then the grid lines are evenly distributed according to the number of grids set by the user.
The generation of trading signals depends on the relationship between price and grid lines. When the price is lower than the lower grid line, open a long position with a fixed quantity at the grid line; when the price is higher than the upper grid line, close the position with a fixed quantity at the grid line. In this way, as the price fluctuates, the position also fluctuates within the grid, achieving profits.
Specifically, the strategy maintains a grid line price array and a bool array indicating whether there is a pending order for each grid line. When the price is lower than a certain grid line and there is no pending order on this line, go long at the price of this line; when the price is higher than a certain grid line and there are pending orders on the lower grid line, close the position at the lower grid line. In this way, grid transactions are realized.
## Strategic Advantages
1. Automatically calculate the grid interval to avoid the difficulty of manual setting. Different calculation methods can be selected.
2. Distribute grid lines evenly to avoid excessive trading caused by dense grids. The number of grid lines is adjustable.
3. Using the grid trading method, risks can be effectively controlled, and profits can always be made if the price fluctuates within the grid.
4. There is no direction expectation for the price, so it is suitable for volatile market conditions.
5. The handling rate and number of positions can be customized to adapt to different trading varieties.
6. Visual display of grid lines makes it easy to grasp the transaction situation.
## Strategy Risk
1. Risk of breaking through the grid interval. If the price breaks through the upper and lower limits of the grid, losses will expand.
2. Risk of too loose grid spacing. If the grid is too wide, it will be difficult to make a profit, but if it is too narrow, handling fees will increase. Need to weigh.
3. Risk of holding positions for too long. It is difficult to make a profit if you hold a position for a long time, yet it will increase the handling fee loss.
4. Risk of improper parameter setting. If parameters such as backtest period or moving average period are set improperly, the grid interval calculation will be affected.
5. Market systemic risk. This strategy is more suitable for volatile market conditions and is not suitable for long-term unilateral market conditions.
## Strategy optimization
1. Optimize grid parameter settings. Comprehensively consider market characteristics, transaction costs and other factors, and optimize parameters such as the number of grids and backtesting cycles.
2. Dynamically adjust the grid interval. When major changes occur in the market, a mechanism for dynamically adjusting the grid interval can be introduced.
3. Add a stop loss mechanism. Set a reasonable stop loss line to avoid excessive losses. Stop loss lines can also be adjusted dynamically.
4. Filter transactions in combination with other indicators. Such as Bollinger Bands, trend indicators, etc., to avoid inappropriate transactions.
5. Optimize capital utilization efficiency. Add hot and cold analysis to reduce trading when volatility is low.
## Summarize
This strategy uses the principle of grid trading to achieve volatile market trading with controllable risks. The strategy has the advantages of automatically calculating the grid and uniformly distributing the grid, and can adapt to different market environments by adjusting parameters. Risks are controllable and easy to operate. However, the strategy also has certain limitations and requires continuous optimization to adapt to market changes. Overall, this strategy provides a relatively standardized and parameterizable implementation idea for grid trading.
||

## Overview

This strategy utilizes the grid trading method in ocean theory to place buy and sell orders within a preset price range. The strategy features automatic calculation of grid price range and uniform distribution of grid lines, which helps effectively manage risks.

## Strategy Logic

The strategy first calculates the upper and lower bounds of the price grid based on user's choice or default settings. There are two ways of calculation: getting the highest and lowest prices in the backtesting period, or computing moving averages over a timeframe. Then grid lines are uniformly distributed according to the number of grids set by user. 

The trading signals are generated based on the relationship between price and grid lines. When the price is below a grid line, a long position is opened at the grid line price with fixed quantity; when the price goes above a grid line, the position is closed at the grid line below. As price fluctuates within the grid, the positions change accordingly to gain profit.

Specifically, the strategy maintains a grid line price array and a bool array indicating whether orders are placed at each line. When price is below a line with no orders, long position is opened at the line; when price is above a line while orders exist at the line below, positions are closed at the lower line. Grid trading is implemented this way.

## Advantages

1. Grid range is calculated automatically, avoiding manual setting difficulty. Different calculation options are available.

2. Grid lines are distributed evenly to avoid overtrading due to dense grids. Number of grids can be adjusted. 

3. Grid trading method effectively controls risks. Profit can be gained as long as price fluctuates within the grid.

4. No price direction assumption, suitable for range-bound market.

5. Customizable commission and position size settings for different trading instruments.

6. Visualization of grid lines helps understand trading situation.

## Risks

1. Price breakout risks. Breaking the upper or lower grid limits can lead to greater losses.

2. Excessive grid space risks. Grids too loose cannot profit easily while too narrow increases costs. Balance is needed.

3. Prolonged holding risks. Long holding makes profit difficult yet increases costs.

4. Improper parameter setting risks. Backtesting period or moving average period can affect grid range calculation if set inappropriately.  

5. Systemic market risks. More suitable for range-bound instead of long-term trended markets.

## Enhancement

1. Optimize grid parameters. Comprehensively consider market conditions, costs etc. to optimize number of grids, lookback period etc.

2. Introduce dynamic grid range adjustment. Adapt grid ranges when significant market change occurs.

3. Incorporate stop loss mechanisms. Set proper stop loss lines to limit losses. Can be adjusted dynamically.

4. Add filters using other indicators. Such as Bollinger Bands, trend indicators etc. to avoid improper trading.

5. Improve capital usage efficiency. Introduce volatility analysis to reduce trading during steady periods.

## Conclusion

The strategy realizes risk-controllable range trading by leveraging grid trading principles. The automatic grid calculation and uniform distribution offer advantages that suit various markets through parameter tuning. Risks are limited and easy to operate. However, limitations exist and continuous improvements are needed to adapt to evolving markets. Overall, the strategy provides a standardized and parametric approach to implementing grid trading.

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
/*backtest
start: 2023-09-12 00:00:00
end: 2023-10-12 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("(IK) Grid Script", overlay=true, pyramiding=14, close_entries_rule="ANY", default_qty_type=strategy.cash, initial_capital=100.0, currency="USD", commission_type=strategy.commission.percent, commission_value=0.1)
i_autoBounds    = input(group="Grid Bounds", title="Use Auto Bounds?", defval=true, type=input.bool)                             // calculate upper and lower bound of the grid automatically? This will theorhetically be less profitable, but will certainly require less attention
i_boundSrc      = input(group="Grid Bounds", title="(Auto) Bound Source", defval="Hi & Low", options=["Hi & Low", "Average"])     // should bounds of the auto grid be calculated from recent High & Low, or from a Simple Moving Average
i_boundLookback = input(group="Grid Bounds", title="(Auto) Bound Lookback", defval=250, type=input.integer, maxval=500, minval=0) // when calculating auto grid bounds, how far back should we look for a High & Low, or what should the length be of our sma
i_boundDev      = input(group="Grid Bounds", title="(Auto) Bound Deviation", defval=0.10, type=input.float, maxval=1, minval=-1)  // if sourcing auto bounds from High & Low, this percentage will (positive) widen or (negative) narrow the bound limits. If sourcing from Average, this is the deviation (up and down) from the sma, and CANNOT be negative.
i_upperBound    = input(group="Grid Bounds", title="(Manual) Upper Boundry", defval=0.285, type=input.float)                      // for manual grid bounds only. The upperbound price of your grid
i_lowerBound    = input(group="Grid Bounds", title="(Manual) Lower Boundry", defval=0.225, type=input.float)                      // for manual grid bounds only. The lowerbound price of your grid.
i_gridQty       = input(group="Grid Lines",  title="Grid Line Quantity", defval=8, maxval=15, minval=3, type=input.integer)       // how many grid lines are in your grid
strategy.initial_capital = 50000
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

https://www.fmz.com/strategy/429163

> Last Modified

2023-10-13 17:07:39
