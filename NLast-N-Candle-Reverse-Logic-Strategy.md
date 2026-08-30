
> Name

Last-N-Candle-Reverse-Logic-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/e8cd6044600f408ec26523c7253ce01e898decb5792bfe3aca34944fcfa0b653.png)
[trans]

## Overview
The main idea of this strategy is to decide whether to go long or short based on the colors of the last N K lines. If the last N K-lines are all green, go long; if the last N K-lines are all red, go short. Its uniqueness lies in the addition of a "reverse logic" parameter, which can invert the original logic. When the "reverse logic" parameter is true, the last N green K lines will go short, and the last N red K lines will go long.
## Strategy Principle
This strategy mainly relies on the following important parameters:
1. numCandlesToCheck: used to specify the number of K lines to be checked
2. numCandlesToExit: Specify the number of K lines that need to be exited after holding a position.
3. inverseLogic: parameter of inverse logic, when true, the original long-short logic will be inverted.
The key logic is to traverse the latest numCandlesToCheck K-lines through a for loop, and count the number of consecutive green K-lines and red K-lines in real time. If the continuous red K lines ≥ numCandlesToCheck, mark lastNCandlesRed as true. If the continuous green K lines ≥ numCandlesToCheck, mark lastNCandlesGreen as true.
When lastNCandlesGreen is true, if the inverseLogic parameter is false, go long; if it is true, go short. On the contrary, when lastNCandlesRed is true, if the inverseLogic parameter is false, go short; if it is true, go long.
Regardless of whether you are long or short, the counter barsSinceEntry will be reset to 0 after opening a position. When barsSinceEntry is greater than or equal to numCandlesToExit, the current position will be closed.
## Advantage Analysis
This is an interesting strategy that uses K-line color decision-making. It adds a "reverse logic" parameter and can flexibly adjust the logic of long and short positions. The main advantages are:
1. The idea is novel and can form an investment in the opposite direction to the general logic of the market.
2. The code is clear and concise, easy to understand and modify
3. You can find the optimal parameter combination by adjusting parameters
4. No matter what the market situation is, this strategy can continue to run and generate signals.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. The color of the K line does not completely represent the market, and there is a possibility of tracking wrong signals.
2. Unable to determine the optimal value of the parameter numCandlesToCheck
3. Unable to determine the optimal value of the parameter numCandlesToExit
4. Improper setting of reverse logic parameters may lead to increased losses
5. The problem of being unable to effectively control a single stop loss
In response to the above risks, the following measures can be taken to control and optimize:
1. Add other filters to avoid false signals, such as increasing the level of trend judgment
2. Traverse different parameter values and find the optimal parameter combination
3. Add a stop-loss mechanism to control single losses
4. Verify the validity of reverse logic parameters
## Optimization direction
This strategy can be optimized mainly from the following directions:
1. Add handicap parameter determination to avoid being cheated
2. Optimize the values of parameters numCandlesToCheck and numCandlesToExit
3. Combine with large cycle trend indicators to filter out false signals
4. Add stop loss and take profit strategies
5. Backtest different varieties to verify the effectiveness of the strategy
6. Compare the returns of original logic and reverse logic
## Summary
The overall idea of this strategy is clear and easy to understand, and it uses simple K-line color judgment to form trading signals. Adjustment of strategy parameters can form rich combination changes, thereby optimizing adjustments for different market environments and varieties. At the same time, we also need to pay attention to some potential risks and take necessary measures to control the risks. By continuously enriching the content of the strategy, the strategy can become a valuable strategy worthy of long-term practice and continuous optimization and improvement.
|| 

## Overview
The main idea of this strategy is to determine long or short based on the color of the last N candles. If the last N candles are green, go long; if the last N candles are red, go short. The unique part is the addition of an "inverse logic" parameter that can reverse the original logic. When the "inverse logic" parameter is true, the last N green candles will go short, and the last N red candles will go long.

## Strategy Principle  
This strategy mainly relies on the following important parameters:

1. numCandlesToCheck: Used to specify the number of candles to check
2. numCandlesToExit: Specifies the number of candles after opening position that needs to exit 
3. inverseLogic: The inverse logic parameter. When true, the original long and short logic is reversed

The key logic is to traverse the last numCandlesToCheck candles through a for loop, and count the consecutive green and red candles in real time. If consecutive red candles ≥numCandlesToCheck, mark lastNCandlesRed as true. If consecutive green candles ≥numCandlesToCheck, mark lastNCandlesGreen as true.

When lastNCandlesGreen is true, go long if inverseLogic is false, otherwise go short. On the contrary, when lastNCandlesRed is true, go short if inverseLogic is false, otherwise go long.

No matter long or short, the barsSinceEntry counter will be reset to 0 after opening position. When barsSinceEntry is greater than or equal to numCandlesToExit, the current position will be closed.

## Advantage Analysis
This is an interesting strategy that uses candle color to make decisions, with an “inverse logic” parameter that can flexibly adjust the long and short logic. The main advantages are:

1. The idea is novel and can form reverse investment against market common logic  
2. The code is clear and concise, easy to understand and modify
3. Can find the optimal parameter combination by adjusting parameters  
4. No matter the market condition, this strategy can continue to run and generate signals

## Risk Analysis
There are also some risks to note for this strategy:

1. Candle color cannot fully represent market condition, risk of tracking incorrect signal exists
2. Unable to determine optimal value for numCandlesToCheck
3. Unable to determine optimal value for numCandlesToExit 
4. Improper inverse logic parameter may amplify losses
5. Unable to effectively control single stop loss

To address these risks, the following measures can be adopted for control and optimization:

1. Increase other filters to avoid incorrect signals, e.g. determine trend on higher timeframe
2. Traverse different parameter values to find optimal parameter combination  
3. Add stop loss mechanism to control single loss
4. Verify effectiveness of inverse logic parameter

## Optimization Directions
The main optimization directions for this strategy are:  

1. Increase orderbook condition to avoid being trapped
2. Optimize the values of numCandlesToCheck and numCandlesToExit
3. Add trend indicator on higher timeframe to filter false signal  
4. Add stop loss and take profit
5. Backtest on different products to verify effectiveness  
6. Compare return between original and inverted logic

## Conclusion
The overall idea of this strategy is clear and easy to understand, generating trading signals simply based on candle color determination. Adjusting parameters can form rich combination variations for optimization targeting different market environments and products. Also need to pay attention to some potential risks and take necessary measures to control them. By continuously enriching strategy content, this strategy can become a valuable one to keep optimizing for long term trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Number of Candles to Check|
|v_input_2|2|Number of Candles To Exit|
|v_input_3|10000|Investment Value|
|v_input_4|false|inverseLogic|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-25 00:00:00
end: 2023-12-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Last Number of  Candles", overlay=true)

// Define the condition for a green candle
isGreenCandle(candle) =>
    close[candle] > open[candle]

// Define the condition for a red candle
isRedCandle(candle) =>
    close[candle] < open[candle]

// Input to specify the number of candles to check
numCandlesToCheck = input(5, title="Number of Candles to Check")
numCandlesToExit = input(2, title="Number of Candles To Exit")  // Corrected the input title

// Initialize variables to count consecutive green and red candles
var int consecutiveGreenCandles = 0
var int consecutiveRedCandles = 0

// Initialize barsSinceEntry outside the loop
var int barsSinceEntry = 0

// Loop through the last "numCandlesToCheck" candles
for i = 0 to numCandlesToCheck - 1
    if isGreenCandle(i)
        consecutiveGreenCandles := consecutiveGreenCandles + 1
        consecutiveRedCandles := 0 // Reset the count for consecutive red candles
    else if isRedCandle(i)
        consecutiveRedCandles := consecutiveRedCandles + 1
        consecutiveGreenCandles := 0 // Reset the count for consecutive green candles

// Check if the last "numCandlesToCheck" candles are green or red
lastNCandlesGreen = consecutiveGreenCandles >= numCandlesToCheck
lastNCandlesRed = consecutiveRedCandles >= numCandlesToCheck

// Calculate the quantity based on the investment value and current asset price
investmentValue = input(10000, title="Investment Value")
var assetPrice = close
var quantity = investmentValue / assetPrice


inverseLogic = input(false, title="inverseLogic")

// Entry condition: Open a buy order if the last "numCandlesToCheck" candles are green
if lastNCandlesGreen
    if inverseLogic
        strategy.entry("Short", strategy.long, qty = quantity)
    else 
        strategy.entry("Buy", strategy.long, qty = quantity)// Reset barsSinceEntry when entering a trade
    barsSinceEntry := 0

// Entry condition: Open a short order if the last "numCandlesToCheck" candles are red
if lastNCandlesRed
    if inverseLogic
        strategy.entry("Buy", strategy.long, qty = quantity)

    else 
        strategy.entry("Short", strategy.short, qty = quantity)
    // Reset barsSinceEntry when entering a trade
    barsSinceEntry := 0

// Increment barsSinceEntry
barsSinceEntry := barsSinceEntry + 1

// Exit condition: Close the position after 2 bars
if barsSinceEntry >= numCandlesToExit
    strategy.close("Buy")
    strategy.close("Short")

```

> Detail

https://www.fmz.com/strategy/436604

> Last Modified

2023-12-26 11:00:29
