
> Name

Example of fund transfer between Huobi futures currency accounts
> Author

Inventor Quantification-Little Dream




> Source (javascript)

``` javascript
function main() {
    // API 接口描述：
    // https://api.huobi.pro
    // POST /v1/futures/transfer
    // params    currency e.g. btc
    //           amount
    //           type futures-to-pro
    
    Log(exchange.GetAccount())
    var ret = exchange.IO("api", "POST", "/v1/futures/transfer", "currency=ltc&amount=0.1&type=pro-to-futures")   // 测试的是LTC ， 币币转期货
    Log("ret", ret)
    
    /* ret
    ret {"status":"ok","data":25669845}
    */
}
```

> Detail

https://www.fmz.com/strategy/148532

> Last Modified

2019-05-20 18:19:53
