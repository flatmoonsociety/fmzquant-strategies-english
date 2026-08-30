
> Name

Simple Martingale long and short position increase ratio modification
> Author

Zer3192

> Strategy Description

! ! ! ! ! ! ! Warm reminder, this strategy is for learning purposes only, if used for real trading, your position will definitely be liquidated! ! ! ! ! ! ! ! ! !
! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! ! !
Simple martingale
The principle is to double your losses until you win the expected profit.
Because it is for backtesting, all orders placed are market orders, and the real price has not been exceeded! !
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|LongAmount|150|Initial order amount for long orders|
|ShortAmount|100|Initial order amount of short order|
|MarginLevel|50|Set Leverage|
|profit|0.5|Expected profit for long orders|
|profits|0.4|Expected profit of short order|
|longbet|1.1|Open multiple times|
|shortbet|true|short opening ratio|
|SetContractType|swap|Perpetual Contract|
|short|true|Short|
|long|false|Go long|
|StopProfit|5|Stop Profit Percent|
|StopLoss|6|Stop loss percentage|

> Source (javascript)

``` javascript
/*backtest
start: 2017-06-26 00:00:00
end: 2022-02-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/
var m =LongAmount //初始下单数
var n = ShortAmount //初始下单数
var MarginLevel1 =MarginLevel  //合约杠杆
var SetContractType1=SetContractType // 合约类型
var longprofit = profit //期望收益 ，多单不能小于手续费
var shortprofits = profits//期望收益 ，空单不能小于手续费
var longbet1 =longbet //开多倍率
var shortbet2=shortbet //开空倍率
StopProfit /=StopProfit ;
StopLoss /=StopLoss ;
//取随机数 
function sum(m, n) {　　
    var num = Math.floor(Math.random() * (m - n) + n);　　
    return num;
}

function main(){
    while(true){
LogProfit(exchange.GetAccount().Balance)
        Sleep(2000)
    }
}
function main() {
    exchange.SetContractType(SetContractType1)
    exchange.SetMarginLevel(MarginLevel1)
    var position = []
    while (true) { 
         position = exchange.GetPosition()
        if (position.length == 0) {
            //取随机数0、1作为方向
            var redom = sum(2, 0)
            Log(redom)
            redom=0==short //做空
            if (redom == 0) {
                n=ShortAmount
                exchange.SetDirection("sell")
                exchange.Sell(-1, n, "开空")
            }
            redom=1==long //做多
            if (redom == 1) {
                m=LongAmount
                exchange.SetDirection("buy")
                exchange.Buy(-1, m, "开多")
            }
        }
        if (position.length > 0) {

            if (position[0].Type == 0) {
                //多头盈利大于期望 
                if (position[0].Profit >profit) {
                    exchange.SetDirection("closebuy")
                    exchange.Sell(-1, position[0].Amount)
                    let redom = Math.random()
                    if (redom < 0.5) { 
                     m=LongAmount
                    exchange.SetDirection("buy")
                    exchange.Buy(-1, m, "平多头开多头头寸")    
                }
             }  
                //多头负盈利大于保证金 则加仓

                if (position[0].Profit <position[0].Margin * -1) {
                    longbet1=longbet
                    m=m*longbet
                    exchange.SetDirection("buy")
                    exchange.Buy(-1, position[0].Amount=m)
               }
            }
                  //空头盈利大于期望 
            if (position[0].Type == 1) {
                if (position[0].Profit > profits) {
                    exchange.SetDirection("closesell")
                    exchange.Buy(-1, position[0].Amount)
                    let redom = Math.random()
                   if (redom > 0.5) {  
                     n=ShortAmount
                    exchange.SetDirection("sell")
                    exchange.Sell(-1, n, "平空头开空头头寸")  
              }
          }
                  //空头负盈利大于保证金 则加仓
                if (position[0].Profit <position[0].Margin * -1 ) {
                    shortbet2=shortbet
                    n=n*shortbet
                    exchange.SetDirection("sell")
                    exchange.Sell(-1, position[0].Amount=n)
                }
            }
            Sleep(60000)
        }
    }
}


```

> Detail

https://www.fmz.com/strategy/356471

> Last Modified

2022-06-19 12:12:05
