
> Name

rest-version OKEX intertemporal hedging strategy tutorial
> Author

Inventor Quantification-Little Dream
> Strategy Description

## Minimalist version of OKEX intertemporal hedging strategy (tutorial)   
  ![IMG](assets/images/2445c2e3f54c207feeb922d08a05d6b3be9609fd7c45a354bf7230c066417dbf.png)

- Only the positive move is done, the reverse move can be modified, and the contract is exchanged to achieve the reverse move.
- Add two exchange objects, the first one is the quarter, the second one is the current week.
- All the code that can be simplified has been streamlined, and there is still a lot of room for optimization. The teaching strategy is prudent and firm, and there are certain risks in the inter-period period.
- Welcome to report bugs.

### Teaching strategies, use with caution in real-life situations.
  ### Teaching strategies, use with caution in real-life situations.
  ### Teaching strategies, use with caution in real-life situations.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|_Begin|true|Starting spread|
|_Add|true|Spread distance|
|_Profit|true|Close the difference profit|
|_Count|10|Number of nodes|
|_ContractNum|true|Node order quantity|

> Source (javascript)

``` javascript
function Hedge (isOpen, priceA, priceB) {
    exchanges[0].SetDirection(isOpen ? "sell" : "closesell")
    exchanges[1].SetDirection(isOpen ? "buy" : "closebuy");
    (function (routineA, routineB) {
        Log(routineA.wait(), routineB.wait(), priceA, priceB)
    })(exchanges[0].Go(isOpen ? "Sell" : "Buy", priceA, _ContractNum), exchanges[1].Go(isOpen ? "Buy" : "Sell", priceB, _ContractNum));
}

var slidePrice = 5
function main () {
    var tickerA, tickerB 
    var arr = []
    for (var i = 0 ; i < _Count ; i++) {
        arr.push({open: _Begin + i * _Add, cover: _Begin + i * _Add - _Profit, isHold: false})
    }
    exchanges[0].SetContractType("quarter")
    exchanges[1].SetContractType("this_week")
    while (1) {
        var tab = {type: "table", title: "状态", cols: ["节点信息"], rows: []}
        tickerA = exchanges[0].GetTicker()
        tickerB = exchanges[1].GetTicker()

        if (tickerA && tickerB) {
            $.PlotLine("差价:A所-B所", tickerA.Last - tickerB.Last)
            for (var j = 0 ; j < arr.length; j++) {
                if (tickerA.Buy - tickerB.Sell > arr[j].open && !arr[j].isHold) {
                    Hedge(true, tickerA.Buy - slidePrice, tickerB.Sell + slidePrice)
                    arr[j].isHold = true
                }
                if (tickerA.Sell - tickerB.Buy < arr[j].cover && arr[j].isHold) {
                    Hedge(false, tickerA.Sell + slidePrice, tickerB.Buy - slidePrice)
                    arr[j].isHold = false 
                }
                tab.rows.push([JSON.stringify(arr[j])])
            }
        }
        LogStatus(_D(), "\n `" + JSON.stringify(tab) + "`")
        Sleep(500)
    }
}
```

> Detail

https://www.fmz.com/strategy/144406

> Last Modified

2019-04-17 16:58:51
