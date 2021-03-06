# ccxt-task
Using CCXT public API and creating a backend service

# Task Overview:
**Step 0 - Create a new branch: eng/public-API-bittrex-poloniex**

**Step 1 - Pull in external data from an exchange "bittrex" and "poloniex"- Data: Coin prices.**

https://www.npmjs.com/package/ccxt

**Step 2 - Save it in database**
- Use MySQL
https://www.npmjs.com/package/mysql

Things to store:
DB Table: MarketData
- Last Updated - Timestamp
- Coin pair - USD/BTC
- Exchange - bittrex, poloniex (all small)
- Price - float.

**Step 3 - Use: https://www.npmjs.com/package/node-schedule to have this data pulled every 5 minutes and saved in the DB.**

This value can be changed from 1 sec to 1 day. We can have a configuration file to change this value. The value can be picked up on config file change. (use file watcher, or something).

**Step 4 - Develop APIs using Node.js for fetching data from Db.**

- Exchange: bittrex, poloniex
- APIs:

+ A - GET a specific coin information :
```
Input: GET /coin-price?pair=USD-BTC
Output: { "status":"OK",
        "info":[
        {
            "exchange": "bittrex",
            "coin":"USD-BTC",
            "value": 50.5,
            "updated": "",//timestamps (you can decide on the format thats the most suited)
        },
        {
            "exchange": "poloniex",
            "coin":"USD-BTC",
            "value": 50.5,
            "updated": "",//timestamps (you can decide on the format thats the most suited)
        }]
}
```
+ B - GET all coins from an exchange :
```
Input: GET /exchange-info?name=bittrex
Output: {
    "status":"OK",
    "info": [
    {
        "coin":"USD-BTC",
        "value": 5700
    },
    {
        "coin":"USD-ETH",
        "value": 234
    },
    {
        "coin":"USD-LTC",
        "value": 50.5
    }]
}
```
+ ERROR situations:
```
{
    "status": "NOTOK",
        "errorcode":1001,
        "errormessage" : "Coin pair not found",
        "messagedetail": "Provide more info if needed"
}
{
    "status": "NOTOK",
        "errorcode":1002,
        "errormessage" : "Invalid exchange not found",
        "messagedetail": "Provide more info if needed"
}
```

**Step 5 - Deploy on AWS**
- Deploy it on AWS. Credentials shared by email.

Other things:
- Use async-await.
- Make this as Modular, readable, extensible as possible.
- We might want to add a caching layer down the line, so please plan accordingly.

