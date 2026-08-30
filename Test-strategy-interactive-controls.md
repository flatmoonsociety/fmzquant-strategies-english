
> Name

Test strategy interactive controls
> Author

Inventor Quantification-Little Dream
> Strategy Description

This strategy is used to test the interactive control function in the strategy design of the inventor's quantitative trading platform.
> Strategy Arguments





|Button|Default|Description|
|----|----|----|
|cmdNum1|Remarks of interactive control cmdNum1|Description of (?numeric type) interactive control cmdNum1|
|cmdNum2|Remarks of interactive control cmdNum2|Description of interactive control cmdNum2|
|cmdNum3|Remarks of interactive control cmdNum3|Description of interactive control cmdNum3|
|cmdBool1|Remarks of interactive control cmdBool1|(?Boolean type) Description of interactive control cmdBool1|
|cmdStr1|Remarks of interactive control cmdStr1|(?String type) Description of interactive control cmdStr1|
|cmdStr2|Remarks of interactive control cmdStr2|Description of interactive control cmdStr2|
|cmdStr3|Remarks of interactive control cmdStr3|Description of interactive control cmdStr3|
|cmdStr4|Remarks of interactive control cmdStr4|Description of interactive control cmdStr4|
|cmdCombox1|Remarks of interactive control cmdCombox1|(?Drop-down box type) Description of interactive control cmdCombox1|
|cmdCombox2|Remarks on interactive control cmdCombox2|Description of interactive control cmdCombox2|
|cmdCombox3|Remarks on the interactive control cmdCombox3|Description of the interactive control cmdCombox3|
|cmdBtn|Remarks on interactive control cmdBtn|(?Button type) Description of interactive control cmdBtn|

> Source (javascript)

``` javascript
function main() {
    var lastCmd = ""
    while (true) {
        var cmd = GetCommand()
        if (cmd) {
            Log(cmd)
            lastCmd = cmd
        }
        LogStatus(_D(), lastCmd)
        Sleep(500)
    }
}
```

> Detail

https://www.fmz.com/strategy/455231

> Last Modified

2024-06-27 15:06:27
