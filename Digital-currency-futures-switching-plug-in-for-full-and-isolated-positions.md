
> Name

Digital currency futures switching plug-in for full and isolated positions
> Author

Inventor Quantification-Little Dream


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|type|0|Cross Margin/Isolated Margin Mode: Isolated Margin|Cross Margin|

> Source (javascript)

``` javascript
function main() {
    var posType = [false, true][type]
    var name = exchange.GetName()
    if (name == "Futures_Binance") {
        exchange.IO("cross", posType)
    } else if (name == "Futures_HuobiDM") {
        exchange.IO("cross", posType)    
    } else if (name == "Futures_Bibox") {
        exchange.IO("cross", posType)        
    } else if (name == "Futures_Bitget") {
        exchange.IO("cross", posType)        
    } else if (name == "Futures_AOFEX") {
        exchange.IO("cross", posType)      
    } else if (name == "Futures_Pionex") {
        exchange.IO("cross", posType)      
    } else {
        throw "not support!"
    }
    return name + "切换 cross :" + posType
}
```

> Detail

https://www.fmz.com/strategy/351758

> Last Modified

2023-09-06 10:36:47
