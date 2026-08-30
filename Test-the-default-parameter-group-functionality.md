
> Name

Test the default parameter group functionality
> Author

Inventor Quantification-Little Dream
> Strategy Description

### How to accurately adjust the "backtest system default settings" using code
> In parameter testing of strategies, backtesting in different time periods, backtesting on multiple underlying objects, etc., the parameters need to be adjusted repeatedly during backtesting the strategy and cannot be recorded, so they need to be reset the next time backtesting. In order to facilitate parameter adjustment, the platform has added a new function - using code to accurately adjust the "backtest system default settings".
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|number|9999|Number type|
|bool|true|Boolean type|
|string|Hello World!|String type|
|comboBox|0|Drop-down box: combo1|combo2|combo3|

> Source (javascript)

``` javascript
/*backtest
start: 2017-03-01        
end: 2017-03-02           
period: 15              
mode: 1                 
*/

/*defaults
number : 0
bool: false
string: Hello BotVS！
comboBox : 2
*/

function main(){
    while(true){
        LogStatus("测试默认参数！");
        Sleep(1000);
    }
}
```

> Detail

https://www.fmz.com/strategy/40155

> Last Modified

2021-07-02 16:33:15
