
> Name

Buy-Strategy-Based-on-Close-Price-Breakthrough
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/0cebe520e97fb6147d95df44d612610cded0c2e387cafca3346b7f994b91c363.png)
[trans]
## Overview
The core idea of ​​this strategy is to buy when the closing price of the stock is higher than the opening price. When the buying conditions are met, the strategy will enter a long position at the closing price when the K-line closes. Then set the stop loss price and take profit price, and the position will be closed when the price touches these two prices.
## Strategy Principle
The closing price of the day's K-line is higher than the opening price, indicating that the stock price of the day is rising. This is a buy signal. The closing price exceeds the opening price of the day, indicating that the buyer's power is relatively strong and the stock price is expected to continue to rise.
Therefore, the trading signal of this strategy is: the closing price of the K-line on the day > the opening price of the K-line on the day. When this condition is met, buy at the closing price when the K-line closes and hold it daily.
This strategy uses two parameters:
1. Entry Price: Buying price, the default is 0, which means buying at the closing price
2. Take Profit Parameter: Take Profit Parameter, the take profit price calculation formula is: Entry Price * (1 + Take Profit Parameter), the default value is 0.5%, which is equivalent to 0.5% of the purchase price
The specific transaction process is as follows:
1. Wait for the K-line to close and check the closing price of the day > the opening price of the day
2. When the conditions are met, buy at the closing price
3. Set stop loss price and take profit price after opening a position
4. When the price rises to the take profit price, close the position and take profit
5. When the price drops to the lowest point of the next K line, close the position and stop the loss.
6. Repeat steps 1-5 every day
## Strategic Advantages
This strategy has the following advantages:
1. Simple idea, easy to understand and implement
2. To judge trading signals, you only need to use the opening price and closing price of the K line, which requires little data.
3. The risk of retracement is small, and the stop-loss and stop-profit mechanism is used to control losses.
## Risk Analysis
This strategy also has some risks:
1. Multiple buying opportunities may appear on the day, but the strategy only buys once at the close, which may result in missing some opportunities.
2. The price may retrace after the market closes, resulting in a higher probability of the stop loss being triggered.
In this regard, the risk can be reduced by:
1. After triggering the buy condition, track the highest price of the day and use AdjustAmount functions to dynamically adjust the position.
2. Delay for a certain period of time after the market closes before setting the stop-loss and take-profit prices to avoid the stop-loss being triggered directly.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Add volume and price confirmation, such as increased trading volume or market heat, as confirmation of buying signals
2. Use dynamic stop-profit and stop-loss after buying, and adjust the stop-loss and stop-profit prices in real time
3. Set parameters for individual stocks and use machine learning methods to automatically optimize parameters
4. Add a position management mechanism to avoid retracement risks by adjusting positions
## Summarize
This strategy generates a buy signal based on the closing price breakthrough. The idea is simple and the risk of retracement is small. By adding confirmation indicators, dynamic stop-profit and stop-loss, parameter optimization and other means, the stability and profitability of the strategy can be further improved. Generally speaking, this strategy is suitable for investors who are interested in opening breakthrough strategies to use and optimize, and has good practicality.
||

## Overview

The core idea of this strategy is to buy when the closing price of the stock is higher than the opening price of the day. When the buy condition is met, the strategy will go long at the close of that candlestick at the closing price. Stop loss price and take profit price will then be set. When the price reaches these two prices, the position will be closed.

## Strategy Principle  

If the closing price of the daily candlestick is higher than the opening price, it means that the stock price rose on that day. This is a buy signal. The breakthrough of the closing price from the opening price indicates that the buying power is quite strong and the stock price is likely to continue rising.

Therefore, the trading signal for this strategy is: Daily Candlestick Close Price > Daily Candlestick Open Price. When this condition is met, buy at the closing price at the close of that candlestick and hold daily.

This strategy uses two parameters:

1. Entry Price: The buying price, the default is 0, which means buying at the closing price  

2. Take Profit Parameter: Take profit parameter, the take profit price formula is: Entry Price * (1 + Take Profit Parameter), the default value is 0.5%, equivalent to 0.5% of the entry price

The specific trading process is as follows:  

1. Wait for candlestick to close and check if close price > open price of the day
2. When the condition is met, buy at the closing price
3. After opening a position, set stop loss and take profit price 
4. When the price rises to take profit price, close position for profit
5. When the price falls to the lowest point of the next candlestick, close position for stop loss
6. Repeat steps 1-5 every day

## Advantage Analysis   

This strategy has the following advantages:

1. The idea is simple and easy to understand and implement  
2. It only requires the open and close prices of candlestick for trade signal judgment, with small data requirements
3. The risk of drawdown is small, using stop loss and take profit mechanism to control losses

## Risk Analysis

There are also some risks with this strategy:   

1. There may be multiple buy opportunities during the day, but the strategy only buys once at close, possibly missing some opportunities  
2. Price may callback after close, increasing the probability of stop loss trigger

The risks can be reduced by:

1. After buy signal triggered, track the highest price of the day and use AdjustAmount functions to dynamically adjust position 
2. Delay setting stop loss and take profit price for a period after close to avoid stop loss trigger immediately  

## Optimization Directions   

This strategy can be optimized in the following aspects:

1. Add volume confirmation, for example add volume or market heat indicators as confirmation for buy signal
2. Use dynamic stop loss and take profit after buying, adjust stop loss and take profit price in real time
3. Set parameters specifically for individual stocks, use machine learning methods to automatically optimize the parameters
4. Add position management mechanism, adjust position size to avoid drawdown risk

## Conclusion  

This strategy generates buy signals based on close price breakthrough. The idea is simple with small drawdown risk. By adding confirmation indicators, dynamic stop loss/take profit, parameter optimization etc., the stability and profitability of the strategy can be further improved. Overall speaking, this strategy is suitable for investors who are interested in opening price breakthrough strategies to use and optimize, and has very good practicality.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|false|Entry Price|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2024-02-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Buy on Close Strategy", overlay=true)

// Входные параметры
var float entry_price = na
if (na(entry_price))
    entry_price := input.float(title="Entry Price", defval=0)

// Функция для расчета Take Profit
calc_take_profit(price) =>
    price * 1.005 // 0.5% от суммы сделки

// Проверяем условие для открытия позиции на покупку
buy_condition = close > open

// Переменная для отслеживания открытой позиции
var bool open_position = na

// Реализация стратегии
if (buy_condition)
    // Открываем сделку на покупку
    strategy.entry("Buy", strategy.long)
    open_position := true

// Закрываем позицию по Take Profit или при закрытии свечи
if (open_position)
    // Рассчитываем уровень Take Profit
    take_profit_level = calc_take_profit(entry_price)

    // Закрываем сделку по Take Profit
    strategy.exit("Take Profit", "Buy", limit=take_profit_level)

    // Закрываем сделку при закрытии свечи
    if (close < open)
        strategy.close("Close Candle", "Buy")

```

> Detail

https://www.fmz.com/strategy/442378

> Last Modified

2024-02-21 14:48:59
