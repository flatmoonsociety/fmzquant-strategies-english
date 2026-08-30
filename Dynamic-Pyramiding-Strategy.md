
> Name

Dynamic-Pyramiding-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1868726b948a33b1dd7.png)

[trans]

## Overview
The dynamic position-adding strategy reduces the average cost price by adding positions when losing money, thereby achieving the purpose of stopping losses and covering losses. When the price triggers the conditions for adding positions, this strategy will add positions one after another at a certain amount and interval. At the same time, the maximum number of positions is set to avoid the risk of unlimited positions.
## Strategy Principle
The core logic of this strategy is:
1. Open a position to buy: If the position is 0, place an order to open a position at the specified price.
2. Conditions for adding positions: If the current number of positions added is less than the maximum number of positions added, and the price is lower than a preset decline of the previous position price, the position added will be triggered.
3. Adding method: The adding quantity increases by a scaling factor of the previous quantity, and the adding interval decreases by a scaling factor of the previous interval.
4. Take profit condition: If a preset profit range of the average price of the position is triggered, all positions will be closed and take profit will be taken.
In this way, when the market is unfavorable, this strategy can reduce the cost of holding positions by adding positions, and obtain additional income while pulling back to stop losses. When the market turns upward, the take profit condition is triggered and all positions are closed for profit.
## Advantage Analysis
The biggest advantage of this strategy is that by adding positions, the average cost price can be reduced, and greater profits can be obtained while tolerating a certain loss, which is especially obvious in a bull market. Specifically, it has the following main advantages:
1. It can significantly reduce the cost of holding positions and enhance the ability to stop losses. When there is a price correction, the strategy will increase the position, thereby "diluting" orders with a higher purchase price and reducing the total cost.
2. Increase profit margins. After reducing costs, as long as the price rebounds, the profit margin will be expanded, which will give way to profit-taking.
3. Flexibly set up the position adding logic and can be customized. The strategy allows you to set parameters such as the margin, quantity, and interval of positions, and users can adjust them according to their own preferences.
4. The risk is controllable and the upper limit for adding positions is set. The limit on the maximum number of positions prevents the strategy from unlimited positions and can control risks.
## Risk Analysis
Although this strategy obtains greater profit potential by adding positions, there are also certain risks that require vigilance:
1. Risk of loss. The strategy is to increase positions on the premise of bearing a certain loss. If the market continues to be unfavorable, losses may expand.
2. Risk of plunge. Under extreme market conditions, prices may plummet, exceeding the affordability of the strategy. This requires reasonable setting of position adding parameters and stop loss points.
3. The rebound is not timely. A price rebound may not necessarily trigger profit taking, and the inability to take profit in time is a shortcoming of the strategy.
4. Parameter setting risks. Improper settings of parameters such as the position increase coefficient and the take-profit range may lead to strategy failure.
These risks can be mitigated by:
1. Appropriately reduce the amount of added positions and control single losses.
2. Reduce the interval between positions and quickly reduce costs.
3. Set stop loss levels appropriately. If the stop loss point is set too wide, the loss will easily expand.
## Optimization direction
Considering that this strategy uses the method of adding positions to obtain greater returns, its optimization direction mainly focuses on better controlling risks and obtaining returns. Specifically, there are the following main optimization directions:
1. Improve the logic algorithm of adding positions to make adding positions more intelligent and responsive to market trends. You can consider triggering additional positions based on indicators such as volatility and price gaps.
2. Optimize the profit-taking method to achieve more efficient profit-taking. It can be combined with moving take-profit, batch take-profit and other methods to reduce the situation where rebound cannot take profit.
3. Introduce machine learning algorithms to achieve adaptive optimization of parameters. Key parameters are no longer static, but dynamically adjusted based on real-time market conditions and feedback.
4. Add a stop-loss mechanism to control the maximum loss. Stop loss methods can consider trailing stop loss, pending order stop loss, etc. to avoid the expansion of losses caused by extreme market conditions.
## Summarize
The dynamic position-adding strategy reduces the average cost by adding positions, and obtains greater returns while appropriately controlling risks. This strategy, which is premised on bearing a certain loss, is especially popular among investors with a strong ability to tolerate losses. The future optimization direction will focus on more intelligent methods of adding positions, more efficient profit-taking mechanisms, etc.
||

## Overview

The dynamic pyramiding strategy aims to lower the average holding cost through pyramiding additional positions when the price drops. It can help to mitigate losses and gain additional profits when the price bounces back. The strategy will open additional positions with certain quantity and interval when the pyramiding conditions are triggered. Meanwhile, the maximum number of pyramiding is set to limit the risk.

## Strategy Logic  

The core logic of this strategy includes:

1. Open position: Open long position with specified price if current position is 0.  

2. Pyramiding condition: Trigger pyramiding if current pyramiding times is less than maximum value, and price drops below last entry price at a preset percentage.

3. Pyramiding way: Increase pyramiding quantity at a scaling factor of previous one, and reduce interval at a scaling factor.  

4. Take profit condition: Close all positions if the profit target based on average holding price is triggered.

By pyramiding with dropping price, this strategy lowers the average cost dynamically. It stops loss efficiently and leaves more room for profit when trend reverses. When take profit condition is triggered, all positions exit with profit.

## Advantage Analysis

The biggest advantage of this strategy is to gain greater profit potential with acceptable losses by lowering average holding cost using pyramiding. The main benefits are:  

1. Reduce holding cost significantly hence enhances the ability to stop loss. By adding additional buy orders at lower prices when drawdown happens, the strategy "dilutes" previous higher entries and lowers overall cost.

2. Increase profit range after lowering cost. If price bounces back, the profit potential gets expanded and paves the way for take profit.  

3. Flexible customization for pyramiding logic by setting related parameters on increment, quantity and interval etc.  

4. Controllable risk by capping maximum pyramiding times. It prevents unlimited pyramiding.

## Risk Analysis   

While the strategy allows more profit potential with pyramiding, some risks need attention:   

1. Loss risk - The premise is undertaking certain losses from pyramiding. If trend keeps going against holdings, losses may expand.  

2. Cliff dive risk - In extreme cases like cliff dive, losses may exceed acceptable range. Reasonable pyramiding settings and stop loss point are critical.

3. Late or missing take profit - Price rebound may not always trigger take profit condition, which is the shortcoming of the strategy.  

4. Parameter tuning risk - Unsuitable settings on parameters like pyramiding coefficient and take profit percentage may lead to failure.

Below measures can help mitigate the risks:

1. Lower increment scale to control single entry loss amount.   

2. Narrow down pyramiding interval to achieve faster cost reduction.

3. Set stop loss point appropriately rather than too loose.

## Optimization Directions

Considering the nature of gaining higher profit potential with pyramiding, the optimization directions mainly focus on better risk control and profitability enhancement:  

1. Improve pyramiding logic to make entries more intelligent and adaptive to market conditions. Entry signals can rely on volatility, price gap and more metrics.

2. Optimize take profit mechanisms for higher efficiency, such as trailing take profit, partial closing etc., to lower the chance of missing price rebound.  

3. Introduce machine learning algorithms to enable parameter auto-tuning. Key parameters become dynamic instead of static based on real-time feedback.   

4. Add stop loss mechanism to limit maximum losses, such as trailing stop loss and take profit stop orders. It prevents losses running out of control under extreme market events.

## Conclusion

The dynamic pyramiding strategy lowers average holding cost by additional entries, enabling higher profit potential given acceptable loss tolerance. This kind of strategy favors investors with relatively high risk appetite. The future optimization directions will be around more intelligent pyramiding logic, higher efficiency take profit mechanisms and so on.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|true|From Day|
|v_input_3|2021|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|2|Price deviation to open safety orders|
|v_input_8|1.5|Target Take Profit|
|v_input_9|100000|base order|
|v_input_10|200|safe order|
|v_input_11|2|Safety order volume scale|
|v_input_12|true|Safety order step scale|
|v_input_13|10|max safe order|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-14 00:00:00
end: 2023-12-18 19:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

strategy("DCA Bot Emulator", overlay=true, pyramiding=99, default_qty_type=strategy.cash, commission_value = 0.02)

// Date Ranges
from_month = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
from_day   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
from_year  = input(defval = 2021, title = "From Year")
to_month   = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
to_day     = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
to_year    = input(defval = 9999, title = "To Year")
start  = timestamp(from_year, from_month, from_day, 00, 00)  // backtest start window
finish = timestamp(to_year, to_month, to_day, 23, 59)        // backtest finish window
window = time >= start and time <= finish ? true : false // create function "within window of time"

// Strategy Inputs
price_deviation = input(2, title='Price deviation to open safety orders', maxval=0)/100
take_profit = input(1.5, title='Target Take Profit', minval=0)/100

// base order
base_order  = input(100000, title='base order') 
safe_order  = input(200, title='safe order') 
safe_order_volume_scale  = input(2, title='Safety order volume scale') 
safe_order_step_scale  = input(1, title='Safety order step scale') 

max_safe_order = input(10, title='max safe order') 
var current_so = 1
var initial_order = 0.0

// Calculate our key levels
pnl = (close - strategy.position_avg_price) / strategy.position_avg_price

take_profit_level = strategy.position_avg_price * (1 + take_profit)

// First Position
if(strategy.position_size == 0 and window)
    strategy.entry("Long", strategy.long, qty = base_order/close)
    initial_order := close
    current_so := 1

// Average Down!
if current_so > 0 and close  < initial_order * (1 - price_deviation * current_so * safe_order_step_scale) and current_so <= max_safe_order
    so_name = "SO " + tostring(current_so) 
    strategy.entry(so_name, long=strategy.long , qty = safe_order * safe_order_volume_scale /close)
    current_so := current_so + 1
    
// Take Profit!
strategy.close_all(when=take_profit_level <= close  and strategy.position_size > 0)

```

> Detail

https://www.fmz.com/strategy/436245

> Last Modified

2023-12-22 14:36:30
