
> Name

The first time placing orders for new coins on the exchange
> Author

grass
> Strategy Description

Pending orders will be placed at fixed intervals, and will be used as a robot to place orders as soon as new coins are listed on the exchange. Not tested due to simple logic
## Principle:
Start running after adding the trading pair, and try to obtain the market quotations without interruption. If the quotations can be obtained, it means that the transaction has started, and the strategy will place an order. If it cannot be obtained, it means that it is not open. Continue to try again and wait.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Type|0|Order type: Buy order|Sell order|
|Start_Price|7000|Start Price|
|Spread|5|Interval|
|N|5|Single number|
|Amount|0.1|Pending order amount per order|
|Amount_Step|false|Pending order increment amount|

> Source (javascript)

``` javascript

function main() {
    exchange.SetTimeout(500) //保证较快的返回null,继续重试获取行情
    while(true){
        var ticker = exchange.GetTicker()
        if(!ticker){
            continue
        }else{
            Log('获取到行情,开始下单')
            for(var i=0;i<N;i++){
               if(Type == 0){
                    exchange.Buy(Start_Price-i*Spread,Amount+i*Amount_Step)
               }else{
                    exchange.Sell(Start_Price+i*Spread,Amount+i*Amount_Step)
               }
            }
            Log('完成挂单,退出程序')
            return
        }
    }
}

```

> Detail

https://www.fmz.com/strategy/194206

> Last Modified

2020-10-16 10:20:29
