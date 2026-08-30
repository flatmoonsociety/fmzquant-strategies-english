
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
  ![IMG](assets/images/f926a39d3bba29202a73c4bf86c620d6a0e8c267297fd677d2e84150d520ae32.png) 

- #### Select plugin:
  ![IMG](assets/images/3468ee8a03eaa7165771ab66cceefd9d414200941297d5e65ac7131f5668afbd.png) 

- #### Execute plugin
  ![IMG](assets/images/f0bc729e1e86fdd29448b4d5cfb3201f98c472c4925a26993d8914936dbea7dd.png) 

- #### Execute immediately
  ![IMG](assets/images/bb9e0e5c3541d7835a968e2a26272ee26b13e6c94f0e9f985f5c1a576c445459.png)  

- #### The simulated disk assets are read out
  ![IMG](assets/images/b1262d5d0481e50724a21de5ac784beb23b6bbcaea4b90c21bfb9fb609a92c76.png) 

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
