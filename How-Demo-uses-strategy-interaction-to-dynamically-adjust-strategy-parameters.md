
> Name

How Demo uses strategy interaction to dynamically adjust strategy parameters
> Author

momox

> Strategy Description

The strategy requires constant testing and adjustment, and the parameters are often changed. Stopping and restarting each time is laborious and laborious, and the original profit progress will be lost (although it can also be restored through global parameters). In fact, botvs has provided a way to dynamically adjust parameters-"Strategy Interaction"
> Strategy Arguments





|Button|Default|Description|
|----|----|----|
|A3|999|AAA parameters|
|B3|Botvs|BBB parameters|

> Source (javascript)

``` javascript
var Interval=2000;

//AAA，BBB为策略中希望动态调整的参数
var AAA=0;
var BBB="hello world";

function main() {
    while(true){
        onTick();
        Sleep(Interval);
    }
}

function onTick(){
    set_command();
    Log("AAA="+AAA,"       BBB="+BBB);
}

//获取动态参数（策略交互内容）
 function set_command() {

     var get_command = GetCommand();//  GetCommand方法是获取参数方法，获取的参数是字符串形式 格式为 "参数名:参数值" 参见BotVS API文档
     if (get_command != null) {
         if (get_command.indexOf("A3:") == 0) {  //如果传入的参数名为A3（以“A3:”打头，即表明是A3参数）

             AAA = (get_command.replace("A3:", "")); //赋值给策略里面的AAA（将打头字符串替换为空，剩下就是我们的参数值）

             Log("AAA变成:" + AAA);
         }
         
          if (get_command.indexOf("B3:") == 0) {  //如果传入的参数名为B3（以“B3:”打头，即表明是B3参数）

             BBB = (get_command.replace("B3:", "")); //赋值给策略里面的BBB（将打头字符串替换为空，剩下就是我们的参数值）

             Log("BBB变成:" + BBB);
         }

     }
 }
```

> Detail

https://www.fmz.com/strategy/8379

> Last Modified

2016-01-09 21:18:07
