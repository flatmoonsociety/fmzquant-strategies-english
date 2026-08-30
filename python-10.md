
> Name

python-status bar table-display button example
> Author

Inventor Quantification-Little Dream




> Source (python)

``` python
import json

def main():
    tab = {
        "type" : "table", 
        "title" : "demo", 
        "cols" : ["a", "b", "c"], 
        "rows" : [["1", "2", {"type" : "button", "cmd" : "coverAll", "name" : "平仓"}]]    # 在状态栏表格 第一行，第三列上配置一个按钮 名字是平仓
    }
    
    LogStatus("`" + json.dumps(tab) + "`")

```

> Detail

https://www.fmz.com/strategy/147155

> Last Modified

2019-05-10 11:35:13
