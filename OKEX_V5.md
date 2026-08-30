
> Name

Switch to OKEX_V5 simulated trading terminal plug-in
> Author

Inventor Quantification-Little Dream
> Strategy Description

## Trading terminal OKEX_V5 simulation disk switching plug-in
When the OKEX V5 exchange object is configured (using OKEX V5's simulated disk API KEY configuration), because the simulated disk environment is not switched, the following error will be reported:
```
{"msg":"Broker id of APIKey does not match current environment.","code":"50101"}
```

You can use this plug-in to switch, as shown in the figure:
- #### Click the Add button:
  ![IMG](https://www.fmz.com/upload/asset/1789d89b0004425112f5.png) 

- #### Select plugin:
  ![IMG](https://www.fmz.com/upload/asset/1714b6edacde6828eba2.png) 

- #### Execute plugin
  ![IMG](https://www.fmz.com/upload/asset/169ace291c5d0da6e210.png) 

- #### Execute immediately
  ![IMG](https://www.fmz.com/upload/asset/170bac2eacc494c2eba3.png)  

- #### The simulated disk assets are read out
  ![IMG](https://www.fmz.com/upload/asset/168a45cf491f249d7189.png) 

If you want to switch back to the real disk environment, just uncheck the option and execute it again.


> Source (javascript)

``` javascript
function main() {    
    exchange.IO("simulate", true)
    return "已经切换为OKEX V5模拟盘"
}
```

> Detail

https://www.fmz.com/strategy/288769

> Last Modified

2021-06-08 15:08:47
