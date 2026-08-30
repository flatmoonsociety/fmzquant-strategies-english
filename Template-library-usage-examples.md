
> Name

Template library usage examples
> Author

Zero

> Strategy Description

Template library usage examples
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|OType|0|Buy or Sell: Buy|Sell|
|Amount|0.5|Order amount|

> Source (javascript)

``` javascript

function main() {
    Log(OType === 0 ? $.Buy(Amount) : $.Sell(Amount));
}
```

> Detail

https://www.fmz.com/strategy/10991

> Last Modified

2016-02-20 22:13:47
