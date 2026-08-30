
> Name

websocket-version OKEX intertemporal hedging strategy tutorial
> Author

Inventor Quantification-Little Dream
> Strategy Description

## Minimalist version of OKEX intertemporal hedging strategy (tutorial)   
- Screenshot of real offer:
     ![IMG](https://www.fmz.com/upload/asset/16f45ddc33e43f3248db.png)
- Only the positive move is done, the reverse move can be modified, and the contract is exchanged to achieve the reverse move.
- Add two exchange objects, the first one is the quarter, the second one is the current week.
- All the code that can be simplified has been streamlined, and there is still a lot of room for optimization. The teaching strategy is prudent and firm, and there are certain risks in the inter-period period.
- Place an order using the counterparty price.
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
|_Instrument_id_A|LTC-USD-190628|A Exchange Quarterly Contract ID|
|_Instrument_id_B|LTC-USD-190426|B exchange’s current week’s contract ID|

> Source (javascript)

``` javascript
function Hedge (isOpen, retSetA, retSetB) {
    exchanges[0].SetDirection(isOpen ? "sell" : "closesell")
    exchanges[1].SetDirection(isOpen ? "buy" : "closebuy");
    (function (routineA, routineB) {
        Log(routineA.wait(), routineB.wait(), retSetA, retSetB)
    })(exchanges[0].Go(isOpen ? "Sell" : "Buy", -1, _ContractNum), exchanges[1].Go(isOpen ? "Buy" : "Sell", -1, _ContractNum))
}

function main () {
    var param = {"op": "subscribe", "args": ["futures/ticker:" + _Instrument_id_A, "futures/ticker:" + _Instrument_id_B]}
    var client = Dial("wss://real.okex.com:8443/ws/v3|compress=gzip_raw&mode=recv&reconnect=true&payload=" + JSON.stringify(param))
    client.write(JSON.stringify(param))
    var tickerA, tickerB 
    var arr = []
    for (var i = 0 ; i < _Count ; i++) {
        arr.push({open: _Begin + i * _Add, cover: _Begin + i * _Add - _Profit, isHold: false})
    }
    while (1) {
        var tab = {type: "table", title: "状态", cols: ["节点信息"], rows: []}
        Sleep(10) 
        var ret = client.read(-2)
        if (!ret || ret == "") {
            continue
        }

        var obj = null
        try {
            obj = JSON.parse(ret)
        } catch (e) {
            Log(e)
            continue
        }

        if (obj.table == "futures/ticker" && obj.data[0].instrument_id == _Instrument_id_A) {   
            tickerA = obj.data[0]
        } else if (obj.table == "futures/ticker" && obj.data[0].instrument_id == _Instrument_id_B) {
            tickerB = obj.data[0]
        }

        if (tickerA && tickerB) {
            $.PlotLine(tickerA.instrument_id + "-" + tickerB.instrument_id, tickerA.last - tickerB.last)
            for (var j = 0 ; j < arr.length; j++) {
                if (tickerA.best_bid - tickerB.best_ask > arr[j].open && !arr[j].isHold) {   
                    Hedge(true, exchanges[0].SetContractType("quarter"), exchanges[1].SetContractType("this_week"))
                    arr[j].isHold = true
                }
                if (tickerA.best_ask - tickerB.best_bid < arr[j].cover && arr[j].isHold) {
                    Hedge(false, exchanges[0].SetContractType("quarter"), exchanges[1].SetContractType("this_week"))
                    arr[j].isHold = false 
                }
                tab.rows.push([JSON.stringify(arr[j])])
            }
        }
        LogStatus(_D(), "\n `" + JSON.stringify(tab) + "`")
    }
}
```

> Detail

https://www.fmz.com/strategy/144378

> Last Modified

2020-04-27 16:58:34
