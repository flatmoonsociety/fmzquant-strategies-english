
> Name

CTA Strategy Commodity Futures Simple Martingale
> Author

Zer3192

> Strategy Description

#### 1. Summary
The Martingale strategy first originated in France in the 18th century, but at that time it was mostly used on gambling tables, and it did not take long to become well-known in Europe. In theory, this is a strategy with a winning rate close to 100%. It has been used in many trading markets until now, such as foreign exchange, futures and digital currency markets. But is it really reliable? Is it really the legendary invincible? This article demonstrates the creation of a simple Martingale strategy for commodity futures.
#### 2. Principle of Martingale Strategy
Martingale is neither a trading strategy nor a trading mechanism, but a money management method. The principle is simple: every time a trader loses a certain amount, he will double the next order volume until he returns to the initial value when he makes a profit. In this way, you only need to make a profit once, not only to recover the previous losses, but also to obtain the profit from the first order amount. Obviously, this is a fund management method of doubling the position against the trend.
Suppose there is a coin with the same weight on both sides. We keep tossing the coin. The probability of heads and tails is about 50%. Next, we make a bet by tossing the coin. The initial bet amount is 1 yuan. If it comes up heads, we win 1 yuan. If it comes up tails, we lose 1 yuan. Theoretically, the probability of a coin coming up heads or tails is the same, because the results of each occurrence are independent of each other, that is, 50%.
According to the principle of Martin strategy, every time you lose money, adjust the bet amount to twice the last bet amount. You only need to win once to recover all previous losses. But when you lose money continuously, you will lose everything. If the principal is only 10 yuan, the first bet is 1 yuan, and the loss is 1 yuan, and the account balance is 9 yuan; the second bet is 2 yuan, and the loss is 2 yuan, and the account balance is 7 yuan; the third bet is 4 yuan, and the loss is 4 yuan, and the account balance is 3 yuan; at this time, there is not enough funds to bet.
#### 3. Strategy backtesting
- Backtest start date: 2015-06-01
- Backtest end date: 2021-04-01
- Data type: Rapeseed meal index
- Data period: daily line
- Slippage: 2 ticks each for opening and closing positions
**Backtest configuration**
 ![IMG](https://www.fmz.com/upload/asset/39df3d9ffd96e830c2f4.png)
**Backtest Performance**
 ![IMG](https://www.fmz.com/upload/asset/3a0b9d36caf93df156c0.png)
**Funding Curve**
 ![IMG](https://www.fmz.com/upload/asset/3992048c1b248823b8e0.png)
**Log information**
 ![IMG](https://www.fmz.com/upload/asset/3979363f6bf790113495.png)
#### 4. Martingale strategy upgrade
The biggest risk of Martingale's strategy is that the market has always been in a unilateral trend. If the trader's position direction runs counter to the market direction, the accumulated positions will be very scary. If a trader's initial capital is 10,000 yuan and he increases his position by 2 times when he loses, he will only need to lose 7 times in a row before his position will be liquidated. But if the multiplier is changed to 1.5, the situation will be much better. It will take 12 consecutive losses before the position is liquidated. If the multiplier is changed to 1.1, the position will be liquidated after 49 consecutive losses. Because the amount of funds occupied is relatively small, the risk of operation is relatively small.
 ![IMG](https://www.fmz.com/upload/asset/390720a08054ffca4d39.png) 

The above picture is a chart of investment multiples and capital investment ratios. It can be seen that using a lower investment multiples will occupy very small funds, and the strategy will have stronger risk resistance. Therefore, in order to ensure the safety of funds, it is recommended to use low investment multiples for real offers. It is recommended to calculate the multiple investment multiples before the actual offer. It is best to have a multiple investment multiple that can withstand more than ten consecutive losses.

#### 5. Summary
Since trading probability is the essence of trading, no one can guarantee that every order will be 100% profitable. It can be said that when you place an order with the perfect reason and timing, the risk actually already exists. The Martingale strategy is especially suitable for trending markets. As long as traders can reasonably judge the trend, open positions in the direction of the trend, and set a good risk-reward ratio, they can also obtain very stable returns.


> Source (javascript)

``` javascript
/*backtest
start: 2015-06-01 00:00:00
end: 2022-04-01 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_usdt"}]
*/

MarginLevel =20//合约杠杆 
unit =0.015//初始下单量
profits =1//盈亏间距
bei =1//倍率



function main() {
    exchange.SetContractType("swap")
    exchange.SetMarginLevel(MarginLevel)
    while (true) {
        let depth = exchange.GetDepth();
        if (!depth) return;
        let ask = depth.Asks[0].Price==-1;
        let bid = depth.Bids[0].Price==-1;
        let position = exchange.GetPosition()
        if (position.length == 0) {
            let redom = Math.random()
            unit =0.015
            if (redom > 0.5) {
                exchange.SetDirection("sell")
                exchange.Sell(-1, unit, "开空")
            }
            if (redom < 0.5 ) {
                exchange.SetDirection("buy")
                exchange.Buy(-1, unit, "开多")
            }
        }
        if (position.length > 0) {
            let type = position[0].Type;
            let profit = position[0].Profit;
            let amount = position[0].Amount;
            if (type == 0) {
                if (profit > profits) {
                    exchange.SetDirection("closebuy")
                    exchange.Sell(-1, amount, "多头止盈，当前盈利：" + profit)
                      unit = 0.015
                }       
            
                if (profit <-profits ) {
                    unit = unit * bei
                    exchange.SetDirection("buy")
                    exchange.Buy(-1, unit, "多头加仓，当前盈利：" + profit)
                }
            }
        
        
            if (type == 1) {
                if (profit > profits) {
                    exchange.SetDirection("closesell")
                    exchange.Buy(-1, amount, "空头止盈，当前盈利：" + profit)
                    unit = 0.015
            }
                    
                
                if (profit < -profits) {
                    unit = unit * bei
                    exchange.SetDirection("sell")
                    exchange.Sell(-1, unit, "空头加仓，当前盈利：" + profit)
                }
            
              }
          } 

        Sleep(1000 )
    }
}



```

> Detail

https://www.fmz.com/strategy/275287

> Last Modified

2022-04-05 07:47:26
