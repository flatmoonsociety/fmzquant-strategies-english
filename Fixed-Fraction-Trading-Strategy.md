
> Name

Fixed-Fraction-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The core idea of ​​this strategy is that investors always maintain a fixed investment share of a certain asset in the asset. When the value of assets rises, investors will sell part to maintain their investment shares; when the value of assets falls, investors will buy to replenish their investment shares. This strategy is suitable for relatively stable assets.
## Strategy Principle
This strategy first needs to set the investment share parameter percentage_invested, which is the share of assets in the investment portfolio. Then adjust the position according to the following logic:
1. When the position is 0, calculate the number of contracts to be purchased based on the set investment share percentage_invested and initial capital initial_capital.
2. When holding a position, compare the ratio of the invested amount to the total equity of the account invested and the set investment share percent_invested. If the proportion of the invested amount is too low, buy the contract to supplement the investment share; if the proportion of the invested amount is too high, sell the contract to maintain the investment share.
3. Repeat step 2 to maintain the investment share at a fixed level.
## Strategic Advantages
- You can hold relatively stable assets for a long time without frequent transactions.
- Adjust positions regularly to profit from asset fluctuations.
- Can diversify investments into multiple non-correlated assets to reduce portfolio risk.
- Can prevent full position losses and avoid losing the entire investment when the bubble bursts.
## Risk Analysis
- For assets with greater volatility, the risk of loss is greater.
- Frequent transactions are required to pay handling fees.
- There may be a time lag in position adjustment and the best buying and selling point may be missed.
- Improper percentage settings can lead to overtrading.
Risks can be reduced in the following ways:
1. Choose assets carefully and avoid highly volatile assets.
2. Optimize position adjustment logic and reduce transaction frequency.
3. Set the minimum unit for position change to avoid over-trading.
4. Optimize percentage settings to prevent excessive concentration of funds.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Add stop loss logic to automatically stop loss when the asset price drops to a certain level.
2. Increase the verification of trading signals for position adjustment to avoid adjusting positions at non-trend change points.
3. Set different investment percentages, stop loss ratios and other parameters for different assets.
4. Add a parameter optimization module to automatically optimize parameters based on historical data.
5. Support closing positions and reinvesting in other assets for dynamic asset allocation.
## Summarize
This strategy achieves the effects of diversified investment and risk control through fixed investment shares, and is suitable for long-term holding of stable assets. However, this strategy has problems such as lag in position adjustment and investment risks in risky assets. In the future, the stability of the strategy can be further improved by optimizing stop loss logic, signal verification and other means.
||

## Overview

The core idea of this strategy is to keep the investment percentage of an asset in the portfolio fixed. When the asset value rises, the investor sells some to maintain the percentage. When it falls, the investor buys more to replenish the percentage. The strategy is suitable for relatively stable assets.

## Strategy Logic

The strategy first sets the investment percentage parameter percent_invested, i.e. the percentage of the asset in the portfolio. It then adjusts positions based on:

1. When position is 0, calculate contracts to buy based on percent_invested and initial capital. 

2. When holding, compare invested amount percentage invested to equity percent_invested. If too low, buy more contracts. If too high, sell contracts.

3. Repeat step 2 to keep investment percentage fixed.

## Advantages

- Allows long-term holding of stable assets without frequent trading.

- Periodic rebalancing profits from asset fluctuations.

- Investment diversification across uncorrelated assets reduces portfolio risk.

- Prevents full losses by avoiding full investment before bubble bursts.

## Risk Analysis

- Higher loss risk for volatile assets.

- Frequent trading means more fees.

- Rebalancing may lag, missing best entry/exit points. 

- Improper percentage settings may cause overtrading.

Risks can be reduced by:

1. Selecting assets carefully to avoid high volatility.

2. Optimizing rebalancing logic to reduce trade frequency.

3. Setting minimum position change units to prevent overtrading.

4. Optimizing percentage settings to prevent overconcentration.

## Optimization Directions

The strategy can be improved by:

1. Adding stop loss logic to cut losses at certain threshold.

2. Adding signal validation before rebalancing to avoid non-trend spots.

3. Customizing percentages, stop loss ratios per asset.

4. Adding parameter optimization module to find optimal parameters. 

5. Support closing positions to reinvest in other assets for dynamic allocation.

## Summary

The fixed percentage strategy provides diversification and risk control. But it has risks like lagging rebalancing and volatile asset losses. Further improvements to stop loss logic and signal validation can enhance stability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Percent Invested|
|v_input_2|true|From Day|
|v_input_3|true|From Month|
|v_input_4|2017|From Year|
|v_input_5|true|To Day|
|v_input_6|true|To Month|
|v_input_7|2018|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-21 00:00:00
end: 2022-11-22 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
// strategy("Fixed Fractioning", overlay=true, initial_capital=100000.0)

percent_invested=input(50.0,title="Percent Invested",maxval=100.0,minval=0.0)
fraction_invested=percent_invested/100

from_day=input(1,title="From Day",maxval=31,minval=1)
from_month=input(1,title="From Month",maxval=12,minval=1)
from_year=input(2017,title="From Year",maxval=2018,minval=1900)

to_day=input(1,title="To Day",maxval=31,minval=1)
to_month=input(1,title="To Month",maxval=12,minval=1)
to_year=input(2018,title="To Year",maxval=2018,minval=1900)

// === FUNCTION EXAMPLE === from: https://www.tradingview.com/script/62hUcP6O-How-To-Set-Backtest-Date-Range/
start     = timestamp(from_year, from_month, from_day, 00, 00)  // backtest start window
finish    = timestamp(to_year, to_month, to_day, 23, 59)        // backtest finish window
window()  => true // create function "within window of time"
strategy.initial_capital = 50000
if strategy.position_size==0 and window()
    contracts_to_buy=(fraction_invested*strategy.initial_capital)/close
    strategy.entry("long",long=true,qty=contracts_to_buy,limit=close,when=contracts_to_buy>1)

invested=(strategy.position_size*close)/strategy.equity
if invested<fraction_invested and window()
    contracts_to_buy=((fraction_invested-invested)*strategy.equity)/close
    strategy.order("long",long=true,qty=contracts_to_buy,limit=close,when=contracts_to_buy>1)

else 
    if invested>fraction_invested and window()
        contracts_to_sell=((invested-fraction_invested)*strategy.equity)/close
        strategy.order("sell",long=false,qty=contracts_to_sell,limit=close,when=contracts_to_sell>1)



```

> Detail

https://www.fmz.com/strategy/427612

> Last Modified

2023-09-22 16:51:25
