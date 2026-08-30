
> Name

A strategy for buying cryptocurrencies on a regular basis Simple-Holder-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1a87d169e146cedd76d1827a2fea65ae9f7c36d3159ff1da4ebc84b23a73c086.png)
[trans]

## Overview
The hold naive strategy is a strategy of regularly purchasing cryptocurrencies to achieve asset appreciation through repeated purchases and holdings of cryptocurrencies. The strategy mainly consists of three main components: regular buy signals, hold signals and exit signals.
## Strategy Principle
The basic logic of this strategy is:
1. At launch, send a buy signal to make your first purchase.
2. Every certain number of candles, send a buy signal to buy more Base currency with Quote currency.
3. When the candle count reaches the preset value, send an exit instruction to close the position.
4. When the exit time arrives, send an exit signal, stop the strategy, and close all positions.
By repeatedly buying and holding cryptocurrencies, you can achieve cost averaging and continuous accumulation effects.
## Advantage Analysis
This strategy has the following advantages:
1. Cryptocurrencies can be purchased regularly to reduce the time risk of purchases.
2. Through repeated purchases, the average holding cost of cryptocurrency can be reduced.
3. By continuing to increase positions, you can obtain portfolio growth returns.
4. You can customize the timing of purchase and exit to achieve automated operations.
5. Simple operation, easy to master and use.
## Risk Analysis
This strategy also has the following risks:
1. Systemic risks in the cryptocurrency market, and prices may fluctuate significantly.
2. Improper exit timing may result in failure to stop losses in time.
3. Improper fund management can also lead to unbearable losses.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Dynamically adjust the purchase time interval and amount according to market conditions.
2. Add a stop loss signal to close the position when the price falls below the support level.
3. Combine more factors to judge the market situation and choose the best time to enter and exit the market.
## Summarize
The holding naive strategy achieves cost averaging and portfolio appreciation by regularly purchasing and holding cryptocurrencies. It is a relatively simple quantitative strategy provided that you know how to use it. By introducing more optimizations, the strategy can be made more intelligent and adaptable to changes in the market environment.
||

## Overview

The Simple Holder strategy is a strategy that periodically buys cryptocurrencies and holds them to achieve asset appreciation. The strategy mainly includes three parts: periodic buying signals, holding signals and exit signals.

## Strategy Principle 

The basic logic of the strategy is:

1. Send a buy signal at start to make the first purchase.  

2. Send a buy signal every certain number of candles to purchase more base currency using the quote currency.

3. When candle count reaches preset value, send exit order to close position.  

4. When exit time is reached, send exit signal to stop strategy and close all positions.

Through repetitive buying and holding of cryptocurrencies, the effects of cost averaging and continuous increasing of positions can be achieved.

## Advantage Analysis

The advantages of this strategy are:

1. Can periodically buy cryptocurrencies to reduce timing risk of purchases.

2. Can reduce average holding cost of cryptocurrencies through repetitive buying. 

3. Can obtain growth profit of portfolio through continuously increasing positions.

4. Customizable purchase and exit timing enables automation.

5. Simple to operate and easy to master.

## Risk Analysis  

Risks of this strategy include:

1. Systematic risk of cryptocurrency market with potentially huge price swings.

2. Inappropriate exit timing may fail to timely stop loss.

3. Inadequate capital management may also lead to failure in bearing losses.

## Optimization Suggestions

The following aspects of the strategy can be optimized:

1. Dynamically adjust buying amount and intervals according to market conditions.

2. Add stop loss signals to close positions when price falls below support level.  

3. Incorporate more factors to determine the optimal entry and exit timing.

## Summary  

The Simple Holder strategy achieves the effect of cost averaging and portfolio growth through periodic buying and holding of cryptocurrencies. It is a relatively simple quantitative strategy once the usage is mastered. Incorporating further optimizations can enhance the strategy's intelligence and adaptability to changing market environments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|7|(?Trade Range)Close at Candle Count:|
|v_input_1|timestamp(2023-09-21 16:30)|Start Date/Time|
|v_input_2|timestamp(2023-09-21 23:05)|End Date/Time|
|v_input_3|paste your message here|(?3Commas)Message to start bot and deal|
|v_input_4|paste your message here|Message for deal add funds signal in the quote currency|
|v_input_5|paste your message here|Message to cancel the deal|
|v_input_6|paste your message here|Message to cancel all bot deals and stop the bot|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2024-01-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Merdoc390

//@version=5

// The idea with this script is to use 3commas DCA bot to keep buying crypto, but not 'close the deal' which sells the crypto. 

// Basic idea is to keep adding funds, which increases the buy. 
// When you cancel the sale, you keep the crypto, thus HODL.
// I use this to build my positions that I short sale on Coinbase.com, so I need to cancel the deal after several candles so I can 
// trade them. 

// 3commas HODL DCA Bot article:
// https://3commas.io/blog/3commas-hodl-dca-bot-strategy
// This article includes the bot setup on 3Commas:
// Basicially you start the trade, then add funds to the trade, buying more crypto, then eventually cancel the deal.
// When you create the bot, you set the take profit really high, like 999%. Since it is unlikey to hit the value, it will never sell


// Credit to Irakli Gun as inspriation
// https://3commas.io/blog/3commas-hodl-dca-bot-strategy

strategy(title='HODL Simple v1', shorttitle="HODL'er", 
 calc_on_every_tick=false, calc_on_order_fills=true, process_orders_on_close =true,
 format=format.price, precision=4, overlay=true, pyramiding=365, 
 currency=currency.USD, default_qty_value=10, default_qty_type=strategy.cash , initial_capital=3650, 
 commission_type=strategy.commission.percent, commission_value=0.1)


var startFirstDeal = true
var done = false
var dealCount = 0
var totalDealCount = 0 


i_closeCount = input.int(defval=7,title="Close at Candle Count:",tooltip="How many buy candles to convert to a buy, otherwise it will remain open until end of timeframe.",group="Trade Range")
Start_date   = input(defval=timestamp('2023-09-21 16:30'),title="Start Date/Time",group="Trade Range")
Finish_date  = input(defval=timestamp('2023-09-21 23:05'),title="End Date/Time",group="Trade Range")

i_startBotAndDealMessage     = input(defval="paste your message here",title="Message to start bot and deal", tooltip="Message for 'start bot and deal",                        group="3Commas",display=display.all) 
i_addFundsMessage            = input(defval="paste your message here",title="Message for deal add funds signal in the quote currency",  tooltip="Using the quote (such as USD), to purchase more.",group="3Commas",display=display.all)
i_cancelTheDealMessage       = input(defval="paste your message here",title="Message to cancel the deal",tooltip="If you paste only cancel the deal, the bot will wait until next candle to add funds.\nOption is to also paste the add funds message to also add a buy position.",       group="3Commas",display=display.all)
i_cancelAndStopMessage       = input(defval="paste your message here",title="Message to cancel all bot deals and stop the bot",tooltip="Paste 3c bot messagage for Cancel all and Stop Bot",     group="3Commas",display=display.all)

time_cond = true

// check exit first
if not startFirstDeal and not done and dealCount < i_closeCount 
    strategy.close("Long")
    alert(i_cancelAndStopMessage)
    // log.info("Time expired, stopping bot, Total Deal Count:{0}",totalDealCount)
    done := true
// check if add funds after first deal
else if time_cond and not startFirstDeal and dealCount < i_closeCount 
    strategy.entry("Long", strategy.long)
    alert(i_addFundsMessage)
    // log.info("Deal Count:{0}, totalDeals:{1}",dealCount,totalDealCount)
    dealCount := dealCount + 1
    totalDealCount := totalDealCount + 1

else if time_cond and startFirstDeal and dealCount <= i_closeCount 
    strategy.entry("Long", strategy.long)
    // log.info("Start deal message, startFirst")
    alert(i_startBotAndDealMessage)
    startFirstDeal := false

else if time_cond and dealCount >= i_closeCount 
    strategy.close("Long")
    alert(i_cancelTheDealMessage)
    // log.info("Over Trades limit of {1}, resetting. Canceling. DealCount: {0}", dealCount, i_closeCount)
    dealCount := 0
    startFirstDeal := true

else if time_cond
    log.error("case not covered")


```

> Detail

https://www.fmz.com/strategy/438066

> Last Modified

2024-01-08 17:05:10
