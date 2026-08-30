
> Name

ChatGPT handles new announcements on exchanges
> Author

ChaoZhang

> Strategy Description

An effective way to solve the problem of inconsistent listing time on exchanges is to use ChatGPT for processing and avoid using regular expressions for cumbersome matching. Handing announcements directly to ChatGPT, allowing it to identify and process the time formats of various exchanges, has become a convenient and efficient application scenario.
By passing the announcement text to the openaiCompletions function, you can leverage the power of ChatGPT to extract key information from listing announcements on various exchanges. This approach not only improves processing efficiency, but also enhances compatibility with different time formats.
Before using this function, you need to set the policy parameter OPENAI_API_KEY, which provides your OpenAI API key. You can use your own key to access the gpt-3.5-turbo API.
Function name: openaiCompletions
Function introduction: This function determines whether the input announcement content is an announcement of a new trading pair on the exchange's spot by calling OpenAI's gpt-3.5-turbo model. If the announcement meets the conditions, the function will return a JSON object, including the success ID, trading pair and Beijing time; if the announcement does not meet the conditions, only a failure ID will be returned.
Input parameters:
content: Announcement content that needs to be judged.
Output result:
JSON object containing the following key-value pairs:
success: Boolean value, indicating whether the judgment result is successful.
pair: (only present when success is true) Array of strings representing trading pairs.
time: (only exists when success is true) A string indicating the announcement release time, which has been converted to Beijing time (UTC+8).
Function execution flow:
Define the URL, request headers and request data for requesting gpt-3.5-turbo API.
Call the HttpQuery method to send the request data to the gpt-3.5-turbo API in JSON format.
Parse the JSON data returned by the gpt-3.5-turbo API and extract the required information.
Returns the processed JSON object.
Usage example:
```
var content = "某交易所宣布，将于2023年3月22日12:00（UTC+8）上线ID/USDT交易对。";
var result = openaiCompletions(content);
Log(result);
```

Output result:
```
{
  "success": true,
  "pair": ["ID_USDT"],
  "time": "2023-03-22 12:00:00"
}

```

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|OPENAI_API_KEY|xxxx|API KEY|


> Source (javascript)

``` javascript

// 封装的函数
function openaiCompletions(content) {
    var url = 'https://api.openai.com/v1/chat/completions';
    var headers = 'Content-Type: application/json\nAuthorization: Bearer ' + OPENAI_API_KEY;
    var data = {
        model: 'gpt-4',//如果api没有gpt-4的权限,这里可以修改为gpt-3.5-turbo
        messages: [
          {role: "system", "content": '判断公告内容,是交易所现货上新交易对的公告吗?如果是你只需要以json的{"success":true,"pair":["ID_USDT"],"time":"2023-03-22 12:00:00"}格式,时间转换为北京时间utc+8,如果不是返回{"success":false}'},
          {role: 'user', content: content}
          ]
    };

    var response = HttpQuery(url, JSON.stringify(data),null,headers,false);
    response = JSON.parse(response)
    return JSON.parse(response.choices[0].message.content);
}

// 使用示例
function main() {
    let announcement = `Fellow Binancians,
Binance will list Radiant Capital (RDNT) in the Innovation Zone and will open trading for these spot trading pairs at 2023-03-30 07:30 (UTC):
New Spot Trading Pairs: RDNT/BTC, RDNT/USDT, RDNT/TUSD
Users can now start depositing RDNT in preparation for trading
Withdrawals for RDNT will open at 2023-03-31 07:30 (UTC)
RDNT Listing Fee: 0 BNB
Users will enjoy zero maker fees on the RDNT/TUSD trading pairs until further notice
Note: The withdrawal open time is an estimated time for users’ reference. Users can view the actual status of withdrawals on the withdrawal page.
In addition, Binance will add RDNT as a new borrowable asset with these new margin pairs on Isolated Margin, within 48 hours from 2023-03-30 07:30 (UTC):
New Isolated Margin Pairs: RDNT/USDT
Please refer to Margin Data for a list of the most updated marginable assets and further information on specific limits and rates.
What is Radiant Capital (RDNT)?
Radiant Capital is a decentralized omnichain money market protocol. Users can stake their collateral on one of the major chains and borrow from another chain. RDNT is the utility token for liquidity mining and governance.
Reminder:
The Innovation Zone is a dedicated trading zone where users are able to trade new, innovative tokens that are likely to have higher volatility and pose a higher risk than other tokens.
Before being able to trade in the Innovation Zone, all users are required to visit the web version of the Innovation Zone trading page to carefully read the Binance Terms of Use and complete a questionnaire as part of the Initial Disclaimer. Please note that there will not be any trading restrictions on trading pairs in the Innovation Zone.
RDNT is a relatively new token that poses a higher than normal risk, and as such will likely be subject to high price volatility. Please ensure that you exercise sufficient risk management, have done your own research in regards to RDNT’s fundamentals, and fully understand the project before opting to trade the token.
Details:
Radiant Capital Website
RDNT Token Contract Addresses - Arbitrum, BNB Chain
Fees
Rules
Thanks for your support!
Binance Team
2023-03-30`
Log(openaiCompletions(announcement))

}

```

> Detail

https://www.fmz.com/strategy/407636

> Last Modified

2023-04-03 14:03:09
