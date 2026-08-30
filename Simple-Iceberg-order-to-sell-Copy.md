
> Name

Spot Iceberg order to sell plug-in Simple-Iceberg-order-to-sell-Copy
> Author

grass
> Strategy Description

Very simple, just for learn.
Code is best annotation.

Iceberg entrusted selling, which divides orders into small sales to avoid impacting the market, is a good and simple learning strategy for getting started with Bitcoin quantitative trading.
The plug-in can be launched with one click on the trading terminal, free of charge, and convenient for manual trading. Detailed introduction: https://www.fmz.com/digest-topic/5051
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|SELLAMOUNT|2|amount to sell|
|SELLSIZE|0.1|sell orders size|
|INTERVAL|3|order exist time(second)|


> Source (javascript)

``` javascript
function main(){
    var initAccount = _C(exchange.GetAccount)
    if (initAccount.Stocks < SELLAMOUNT){
        throw 'check your account amount to sell'
    }
    while(true){
        var account = _C(exchange.GetAccount)
        var dealAmount =  initAccount.Stocks - account.Stocks
        var ticker = _C(exchange.GetTicker)
        if(SELLAMOUNT - dealAmount >= SELLSIZE){
            var id = exchange.Sell(ticker.Buy, SELLSIZE)
            Sleep(INTERVAL*1000)
            if(id){
                exchange.CancelOrder(id) // May cause error log when the order is completed, which is all right.
            }else{
                throw 'sell error'
            }
        }else{
            account = _C(exchange.GetAccount)
            var avgCost = (account.Balance - initAccount.Balance)/(initAccount.Stocks - account.Stocks)
            return 'Iceberg order to sell is done, avg price is ' + avgCost
            
        }
    }
}
```

> Detail

https://www.fmz.com/strategy/191772

> Last Modified

2020-03-24 10:50:43
