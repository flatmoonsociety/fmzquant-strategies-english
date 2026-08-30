
> Name

Grid management tools
> Author

program

> Strategy Description

**GridPriceManager is used to create and manage grid lists and store grid orders**
### Initialization
| Parameters | Required | Description |
| ----------- | -------- | ----------------------------------------------- |
| upper_price | NO | Grid upper boundary price |
| lower_price | NO | Grid lower boundary price |
| grid_num | NO | Number of grids (equal difference) |
| interval | NO | Grid interval (equal ratio) |
| side | NO | Supports passing in `long`, `short`, if not filled in, the default is `long` |
| Data | NO | Already have grid information, type is dictionary |
```python
# 创建了一个价格1000-800，数量为10的等差网格
GridPriceManager(upper_price=1000, lower_price=800, grid_num=10)

# 创建了一个价格1000-800，间隔为1%的等比网格
GridPriceManager(upper_price=1000, lower_price=800, interval=1)

# 传入已有网格信息
data = {
	"grid_list":    {99:None,100:None,101:None,102:None,103:None,104:None},
	"interval":     None,
	"upper_price":  104,
	"lower_price":  99,
	"grid_num":     6,
	"side":         "long",
	"grid_diff":    1,
	"type":         "等差",
}
GridPriceManager(Data=data)
```

### Data structure
| Parameters | Required | Description |
| ----------- | -------- | --------------------------------------------------------------- |
| grid_list | YES | Grid price and order information are stored as key-value pairs, where key is the price and value is the order id |
| interval | YES | |
| upper_price | YES | |
| lower_price | YES | |
| grid_num | YES | |
| side | YES | |
| grid_diff | YES | |
| type | YES | equal difference or equal ratio |
### Function
+ get_nearest_buy_price(current_price)

**Get the latest grid buying price**
| Parameters | Required | Description |
  | ------------- | -------- | ------------------------------------ |
  | current_price | YES | Pass in the price and find the nearest buying price at this price |
+ get_nearest_sell_price(current_price)

**Get the latest grid selling price**
| Parameters | Required | Description |
  | ------------- | -------- | ------------------------------------ |
  | current_price | YES | Pass in the price and find the nearest selling price at this price |
+ base_position(ticker)

**Bottom warehouse**
| Parameters | Required | Description |
  | ------ | -------- | --------------------------------------------------------------- |
  | ticker | YES | Open a bottom position to open the grid. This function will execute the callback function `event` event `base_position` |
+ add_order(order_id)

**Add grid upper and lower pending orders**
| Parameters | Required | Description |
  | -------- | -------- | --------------------------------------------------------------- |
  | order_id | YES | Add the upper and lower grid pending orders. The id function passed in the bottom position or transaction order will find the upper and lower grids of this id. This function will execute the callback function `event` event `add_order` |
+ cancel_order(order_id)

**Cancel order**
| Parameters | Required | Description |
  | -------- | -------- | --------------------------------------------------------------- |
  | order_id | YES | Cancel the specified order, this function will execute the callback function `event` event `cancel_order` |
### event
Event refers to the specified callback function called during function execution. Here, the event function is always used to pass in the specified event. Decorator mode
```python
gm = GridPriceManager(1000, 800, 10)

# 底仓事件，在调用base_position方法时会触发此事件
@gm.event('base_position')
def base_position(price):
    # 传入最近的网格价格，以此价格作为买入价格参考
    print(price)
    return 123456	# 返回底仓订单，manger将订单记录
```

| Event | Is it required | Pass in | Return |
| ------------- | -------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| base_position | YES | price, buying price, float type | bottom position order id |
| add_order | NO | price, buy grid price, dict type, {"up": upper grid price, "down": lower grid price} | A dict with the same format as the one passed in, corresponding to the upper grid transaction id and the lower grid transaction id |
| cancel_order | NO | order_id, specifies the canceled order id, int or str type | bool, whether the cancellation is successful |
| change | NO | grid_list | This event is triggered when the grid information changes |




> Source (python)

``` python
class GridPriceManager:
    def __init__(self, Data=None, upper_price=None, lower_price=None, interval=None, grid_num=None, side: Literal['long','short']='long') -> dict:
        self.interval = interval
        self.upper_price = upper_price
        self.lower_price = lower_price
        self.grid_num = grid_num
        self.side = side
        self.grid_diff = None
        self.type = None    # 网格类型
        if self.grid_num is not None:
            self.grid_diff = (self.upper_price - self.lower_price) / (self.grid_num - 1)
        if Data is None: 
            if self.interval is None:
                self.grid_list = self._generate_grid_list_difference()
                self.type = "等差"
            else:
                self.grid_list = self._generate_grids_list_ratio()
                self.type = "等比"
        else:
            self.grid_list = Data["grid_list"]
            self.interval = Data["interval"]
            self.upper_price = Data["upper_price"]
            self.lower_price = Data["lower_price"]
            self.grid_num = Data["grid_num"]
            self.side = Data["side"]
            self.grid_diff = Data["grid_diff"]
            self.type = Data["type"]
        self.data = f"网格类型: {self.type}, 网格数量: {len(self.grid_list)}, 上下区间: [{self.upper_price}-{self.lower_price}, 方向: {self.side}]"
        self.callback = {}

    def event(self, event_name):
        """事件"""
        def decorator(func):
            self.callback[event_name] = func
            return func
        return decorator

    def _generate_grid_list_difference(self) -> dict:
        """等差网格生成"""
        grid_list = {}
        price = self.lower_price
        for _ in range(self.grid_num):
            grid_list[price] = None
            price += self.grid_diff
        grid_list[self.upper_price] = None
        return grid_list

    def _generate_grids_list_ratio(self) -> dict:
        """等比网格生成"""
        ratio = 1 + self.interval / 100
        grid = [self.lower_price * (ratio ** i) for i in range(-100, 101)]
        return {round(g, 8): None for g in grid if self.lower_price <= g <= self.upper_price}


    def get_nearest_buy_price(self, current_price) -> float:
        """获取最近网格买入价格"""
        nearest_price = None
        for price in sorted(self.grid_list.keys()):
            if price > current_price:
                break
            nearest_price = price
        return nearest_price

    def get_nearest_sell_price(self, current_price) -> float:
        """获取最近网格卖出价格"""
        nearest_price = None
        for price in sorted(self.grid_list.keys(), reverse=True):
            if price < current_price:
                break
            nearest_price = price
        return nearest_price
    
    def base_position(self, ticker) -> Union[str, int]:
        """底仓"""
        if self.side == "short":
            t = self.get_nearest_sell_price(ticker)
        else:
            t = self.get_nearest_buy_price(ticker)
        order_id = self.callback["base_position"](t)
        self.grid_list[t] = order_id
        self.callback["change"](self.grid_list)
        return order_id
    
    def add_order(self, order_id) -> Union[Dict, bool]:
        """增加网格上下挂单"""
        up_price = None
        down_price = None
        ticker = None
        keys = list(self.grid_list.keys())
        for i in range(len(keys)-1):
            if self.grid_list[keys[i]] == order_id:
                ticker = keys[i]
                try:
                    if self.side is None or self.side == "long":
                        up_price = keys[i+1]
                        down_price = keys[i-1]
                    else:
                        up_price = keys[i-1]
                        down_price = keys[i+1]
                except IndexError:
                    return False
                break

        PriceDict = {"up": up_price, "down": down_price}
        d = self.callback["add_order"](PriceDict)
        d = {"up": d["up"], "down": d["down"]}
        self.grid_list[up_price] = d["up"]
        self.grid_list[down_price] = d["down"]
        self.grid_list[ticker] = None
        self.callback["change"](self.grid_list)
        return d
    
    def cancel_order(self, order_id):
        """撤销订单"""
        result = self.callback["cancel_order"](order_id)
        if result == True:
            for items in self.grid_list.items():
                if items[1] == order_id:
                    self.grid_list[items[0]] = None
                    self.callback["change"](self.grid_list)
                    break

def main():
    gm = GridPriceManager(1000, 500, 10)

    @gm.event('add_order')
    def add_order(price):
        print(price)
        return {
            'up': 36543,
            'down': 87957,
        }

    @gm.event('cancel_order')
    def cancel_order(order_id):
        return True

    @gm.event('base_position')
    def base_position(price):
        print(price)
        return 123456

    a = gm.base_position(600)
    print(a)
    a = gm.add_order(123456)
    print(gm.grid_list)
    gm.cancel_order(87957)
    print(gm.grid_list)
```

> Detail

https://www.fmz.com/strategy/411935

> Last Modified

2023-05-01 12:32:46
