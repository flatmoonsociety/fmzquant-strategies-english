
> Name

Multi-Zone-MA100-Price-Retracement-Smart-Grid-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1dadedd08563f9320ef6c1a817f168ebb9e4416268e01a96d836459f854f7125.png)

[trans]
#### Overview
This strategy is a multi-range grid trading system based on the MA100 moving average. It sets different price retracement ranges (-8%, -15%, -20%) to build positions in batches, gradually buys when the market drops significantly, and takes profits when the price rebounds by 3%. The strategy adopts the idea of ​​​​intelligent grid to control risks by limiting the maximum number of positions and trading intervals in each interval.
#### Strategy Principle
The core logic of the strategy includes the following aspects:
1. Use the 100-period simple moving average (SMA) as the base price for the strategy
2. Set three buying intervals:
   - Interval 2: Price retracement 8%, maximum 2 transactions allowed
   - Interval 3: Price retracement 15%, maximum 3 transactions allowed
   - Interval 4: Price retracement 20%, maximum 4 transactions allowed
3. Unified closing conditions: when the price rebounds by more than 3% of MA100
4. Each interval is set with a minimum trading interval of 50 K-line cycles to avoid too frequent trading.
#### Strategic Advantages
1. Multi-interval hierarchical warehouse building reduces the cost of building a warehouse
2. Adopt grid trading ideas to capture opportunities in violent fluctuations
3. Set maximum position limits and trading intervals to effectively control risks
4. The strategy logic is simple and easy to understand and maintain.
5. Suitable for high volatility market environments
6. Can be executed automatically without manual intervention
#### Strategy Risk
1. A large retracement may occur in a sustained downward trend
2. A larger capital scale is required to support multi-range position building.
3. The closing conditions are relatively simple and you may miss out on greater room for growth.
4. Failure to consider the overall market trend may result in poor performance in trending markets.
5. Fixed percentage parameters may not be suitable for all market environments
#### Strategy optimization direction
1. Introduce trend judgment indicators and adjust strategy parameters in strong trends
2. Optimize the position closing mechanism and dynamically adjust profit targets according to market fluctuations
3. Add a risk control module and set overall position limits and stop-loss conditions
4. Introduce volatility indicators (such as ATR) and dynamically adjust the position opening range
5. Optimize the transaction interval mechanism, which can be dynamically adjusted according to market conditions
#### Summary
This strategy uses multi-range grid trading to build positions in batches when the market has a sharp correction, and has good risk resistance. Although there are some potential risks, stable trading results can be achieved through reasonable parameter settings and risk control measures. The main room for further optimization lies in adding more market adaptability indicators and improving the risk control mechanism. ||
#### Overview
This strategy is a multi-zone grid trading system based on the MA100 moving average. It implements batch position building through different price retracement zones (-8%, -15%, -20%), buying gradually during significant market drops and taking profits when prices bounce back by 3%. The strategy adopts a smart grid approach, controlling risk by limiting the maximum number of positions and trading intervals in each zone.

#### Strategy Principles
The core logic includes the following aspects:
1. Uses 100-period Simple Moving Average (SMA) as the strategy's reference price
2. Sets three buying zones:
   - Zone 2: 8% price retracement, maximum 2 trades allowed
   - Zone 3: 15% price retracement, maximum 3 trades allowed
   - Zone 4: 20% price retracement, maximum 4 trades allowed
3. Unified closing condition: when price bounces back above 3% of MA100
4. Each zone has a minimum trading interval of 50 candle periods to avoid excessive trading

#### Strategy Advantages
1. Multi-zone layered position building reduces entry cost
2. Adopts grid trading concept, capable of capturing opportunities in volatile markets
3. Maximum position limits and trading intervals effectively control risk
4. Simple strategy logic, easy to understand and maintain
5. Suitable for high-volatility market environments
6. Can be executed automatically without manual intervention

#### Strategy Risks
1. May experience significant drawdowns in persistent downtrends
2. Requires substantial capital to support multi-zone position building
3. Simple closing conditions might miss larger upward movements
4. Doesn't consider overall market trends, may underperform in trending markets
5. Fixed percentage parameters may not suit all market conditions

#### Strategy Optimization Directions
1. Introduce trend indicators to adjust strategy parameters in strong trends
2. Optimize closing mechanism to dynamically adjust profit targets based on market volatility
3. Add risk control module with overall position limits and stop-loss conditions
4. Incorporate volatility indicators (like ATR) to dynamically adjust entry zones
5. Optimize trading interval mechanism to adjust dynamically based on market conditions

#### Summary
This strategy achieves batch position building during significant market corrections through multi-zone grid trading, demonstrating good risk resistance. While there are potential risks, stable trading results can be achieved through appropriate parameter settings and risk control measures. Further optimization opportunities mainly lie in incorporating more market-adaptive indicators and improving risk control mechanisms.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-20 00:00:00
end: 2025-02-17 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// BTC SOL ETH BNB XMR RNDR AKT OM ONDO IO

strategy("MA100 crash buy 3 Zone // 15 min", overlay=true, calc_on_every_tick=true)

// Définition des MA
maH1 = ta.sma(close, 100)
maB2 = ta.sma(close, 100)
maB3 = ta.sma(close, 100)
maB4 = ta.sma(close, 100)

// Définition du niveau d'achat et de vente
sellLevel1 = maH1 * 1.03 //+3%
buyLevel2 = maB2 * 0.92 //-8%
buyLevel3 = maB2 * 0.85 //-15%
buyLevel4 = maB2 * 0.80 //-20%



// Nombre max de trades simultanés
maxTrades2 = 2
maxTrades3 = 3
maxTrades4 = 4

// Délais entre deux ordres (en bougies)
tradeDelay = 50
var float lastTradeTime = na
var float lastSellTime = na
tradeDelay2 = 50
var float lastTradeTime2 = na
tradeDelay3 = 50
var float lastTradeTime3 = na
tradeDelay4 = 50
var float lastTradeTime4 = na

// Condition d'achat et de vente
buyCondition2 = low <= buyLevel2 and strategy.opentrades < maxTrades2 and (na(lastTradeTime2) or bar_index - lastTradeTime2 > tradeDelay2)
buyCondition3 = low <= buyLevel3 and strategy.opentrades < maxTrades3 and (na(lastTradeTime3) or bar_index - lastTradeTime3 > tradeDelay3)
buyCondition4 = low <= buyLevel4 and strategy.opentrades < maxTrades4 and (na(lastTradeTime4) or bar_index - lastTradeTime4 > tradeDelay4)
sellCondition = strategy.position_size > 0 and high >= sellLevel1 and (na(lastSellTime) or bar_index - lastSellTime > tradeDelay)

if buyCondition2
    strategy.entry("Buy", strategy.long)
    lastTradeTime2 := bar_index  // Enregistre le moment du trade

if buyCondition3
    strategy.entry("Buy", strategy.long)
    lastTradeTime3 := bar_index  // Enregistre le moment du trade

if buyCondition4
    strategy.entry("Buy", strategy.long)
    lastTradeTime4 := bar_index  // Enregistre le moment du trade

if sellCondition
    strategy.close("Buy")  // Ferme 50% de toutes les positions ouvertes // , qty_percent=30
    lastSellTime := bar_index  // Enregistre le moment du trade


// Affichage des niveaux
plot(sellLevel1, color=#fa930d, title="Sell Level")
plot(buyLevel2, color=#15bbfd, title="Buy Level")
plot(buyLevel3, color=#1229aa, title="Buy Level")
plot(buyLevel4, color=#9812aa, title="Buy Level")
```

> Detail

https://www.fmz.com/strategy/482598

> Last Modified

2025-02-19 11:12:51
