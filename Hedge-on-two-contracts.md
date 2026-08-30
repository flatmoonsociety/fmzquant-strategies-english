
> Name

One-click futures hedging plug-in Hedge-on-two-contracts
> Author

grass
> Strategy Description

Two contracts can be automatically and immediately hedged. Be careful to add appropriate price slippage, as the transaction may not be completed. If you have a large number of positions, you can click multiple times.
The plug-in can be launched with one click on the trading terminal, free of charge, and convenient for manual trading. Detailed introduction: https://www.fmz.com/digest-topic/5051
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Contract_A|this_week|Trading Contract A|Contract A|
|Contract_B|quarter|Transaction Contract B|Contract B|
|Amount|10|Open Amount|
|Slip|2|Slip Price|
|Reverse|false|Reverse trading|Reverse Direction|

> Source (javascript)

``` javascript

function main(){
    exchange.SetContractType(Reverse ? Contract_B : Contract_A)
    var ticker_A = exchange.GetTicker()
    if(!ticker_A){return 'Unable to get quotes'}
    exchange.SetDirection('buy')
    var id_A = exchange.Buy(ticker_A.Sell+Slip, Amount)
    exchange.SetContractType(Reverse ? Contract_B : Contract_A)
    var ticker_B = exchange.GetTicker()
    if(!ticker_B){return 'Unable to get quotes'}
    exchange.SetDirection('sell')
    var id_B = exchange.Sell(ticker_B.Buy-Slip, Amount)
    if(id_A){
        exchange.SetContractType(Reverse ? Contract_B : Contract_A)
        exchange.CancelOrder(id_A)
    }
    if(id_B){
        exchange.SetContractType(Reverse ? Contract_B : Contract_A)
        exchange.CancelOrder(id_B)
    }
    return 'Position: ' + JSON.stringify(exchange.GetPosition())
}

```

> Detail

https://www.fmz.com/strategy/191348

> Last Modified

2020-03-24 10:52:08
