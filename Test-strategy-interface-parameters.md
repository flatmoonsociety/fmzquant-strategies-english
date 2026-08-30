
> Name

Test strategy interface parameters
> Author

Inventor Quantification-Little Dream
> Strategy Description

This strategy is used to test the interface parameter function in the strategy design of the inventor's quantitative trading platform.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|pNum1|Remarks for parameter pNum1|(? Numeric parameter) Description of parameter pNum1|
|pNum2|Remarks for parameter pNum2|Description of parameter pNum2|
|pNum3|Remarks for parameter pNum3|Description of parameter pNum3|
|pNum4|Remarks for parameter pNum4|Description of parameter pNum4|
|pBool1|Remarks for parameter pBool1|(?Boolean parameter) Description of parameter pBool1|
|pBool2|Remarks for parameter pBool2, used to control whether to display pNum1|Description of parameter pBool2|
|pStr1|Remarks for parameter pStr1|(?String type) Description of parameter pStr1|
|pStr2|Remarks for parameter pStr2|Description of parameter pStr2|
|pStr3|Remarks for parameter pStr3|Description of parameter pStr3|
|pStr4|Remarks for parameter pStr4|Description of parameter pStr4|
|pCombox1|Remarks for parameter pCombox1|(?Drop-down box type) Description of parameter pCombox1|
|pCombox2|Remarks for parameter pCombox2|Description of parameter pCombox2|
|pCombox3|Remarks for parameter pCombox3|Description of parameter pCombox3|
|pSecretStr1|Remarks for parameter pSecretStr1|(?Encrypted string type) Description of parameter pSecretStr1|

> Source (javascript)

``` javascript
/*backtest
start: 2023-06-21 00:00:00
end: 2024-06-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_OKX","currency":"BTC_USD"}]
*/

function main() {
    Log("---------------------------开始测试数字类型参数---------------------------")
    Log("变量pNum1:", pNum1, ", 变量值类型：", typeof(pNum1))
    Log("变量pNum2:", pNum2, ", 变量值类型：", typeof(pNum2))
    Log("变量pNum3:", pNum3, ", 变量值类型：", typeof(pNum3))
    Log("变量pNum4:", pNum4, ", 变量值类型：", typeof(pNum4))
    
    Log("---------------------------开始测试布尔类型参数---------------------------")
    Log("变量pBool1:", pBool1, ", 变量值类型：", typeof(pBool1))
    Log("变量pBool2:", pBool2, ", 变量值类型：", typeof(pBool2))

    Log("---------------------------开始测试字符串类型参数---------------------------")
    Log("变量pStr1:", pStr1, ", 变量值类型：", typeof(pStr1))
    Log("变量pStr2:", pStr2, ", 变量值类型：", typeof(pStr2))
    Log("变量pStr3:", pStr3, ", 变量值类型：", typeof(pStr3))
    Log("变量pStr4:", pStr4, ", 变量值类型：", typeof(pStr4))

    Log("---------------------------开始测试下拉框类型参数---------------------------")
    Log("变量pCombox1:", pCombox1, ", 变量值类型：", typeof(pCombox1))
    Log("变量pCombox2:", pCombox2, ", 变量值类型：", typeof(pCombox2))
    Log("变量pCombox3:", pCombox3, ", 变量值类型：", typeof(pCombox3))

    Log("---------------------------开始测试加密串类型参数---------------------------")
    Log("变量pSecretStr1:", pSecretStr1, ", 变量值类型：", typeof(pSecretStr1))
}
```

> Detail

https://www.fmz.com/strategy/455212

> Last Modified

2024-06-27 15:05:19
