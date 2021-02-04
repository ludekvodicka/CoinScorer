# Exchange Realtime Data

## Candle Ticker start/stop

- Type: `Message`
- Start: `MessageType::ExchangeDataOnline::cmdCandleTickerStart`
- Stop: `MessageType::ExchangeDataOnline::cmdCandleTickerStop`
- Params: `XString strExchange, const stSymbolPair& symbol, timeframe_t timeframe`

``` cpp tab="Send"
SendMessage<XString, stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerStart::id(),
  "binance",
  stSymbolPair("bnb","btc"),
  timeframe_t(EnmTimeframe::Min1)
);

SendMessage<XString, stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerStop::id(),
  "binance",
  stSymbolPair("bnb","btc"),
  timeframe_t(EnmTimeframe::Min1)
);
```

``` cpp tab="Register"  
RegisterMessageCallback<XString, Currencies::stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerStart::id(),
  boost::bind(&method, this, _1, _2, _3)
);

RegisterMessageCallback<XString, Currencies::stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerStop::id(),
  boost::bind(&method, this, _1, _2, _3)
);
```

## HighRes Candle Ticker start/stop

- Type: `Message`
- Start: `MessageType::ExchangeDataOnline::cmdCandleTickerHigResolutionStart`
- Stop: `MessageType::ExchangeDataOnline::cmdCandleTickerHigResolutionStop`
- Params: `XString strExchange, const stSymbolPair& symbol, timeframe_t timeframe`

``` cpp tab="Send"
SendMessage<XString, stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerHigResolutionStart::id(),
  "binance",
  stSymbolPair("bnb","btc"),
  timeframe_t(EnmTimeframe::Min1)
);

SendMessage<XString, stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerHigResolutionStop::id(),
  "binance",
  stSymbolPair("bnb","btc"),
  timeframe_t(EnmTimeframe::Min1)
);
```

``` cpp tab="Register"
RegisterMessageCallback<XString, Currencies::stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerHigResolutionStart::id(),
  boost::bind(&method, this, _1, _2, _3)
);

RegisterMessageCallback<XString, Currencies::stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdCandleTickerHigResolutionStop::id(),
  boost::bind(&method, this, _1, _2, _3)
);
```

## Candle ticker

Ticker message for normal and high-resolution ticker.

- Type: `Message`
- Message: `MessageType::ExchangeDataOnline::onCandleTickerTick(exchange, symbol, timeframe)`
- Params: `tradeData:stTimeCandleStick`

``` cpp tab="Register"
RegisterMessageCallback<stTimeCandleStick>(
  MessageType::ExchangeDataOnline::onCandleTickerTick(exchange, pair, timeframe),
  boost::bind(&method, this, _1)
);
```

``` cpp tab="Send"
SendMessage<stTimeCandleStick>(
  MessageType::ExchangeDataOnline::onCandleTickerTick(exchange, symbol, timeframe),
  dataCandleStick
);
```

## Trade Ticker start/stop

- Type: `Message`
- Start: `MessageType::ExchangeDataOnline::cmdTradeTickerStart`
- Stop: `MessageType::ExchangeDataOnline::cmdTradeTickerStop`
- Params: `XString strExchange, const stSymbolPair& symbol`

``` cpp tab="Send"
SendMessage<XString, stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdTradeTickerStart::id(),
  "binance",
  stSymbolPair("bnb","btc"),
);

SendMessage<XString, stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdTradeTickerStop::id(),
  "binance",
  stSymbolPair("bnb","btc"),
);
```

``` cpp tab="Register"
RegisterMessageCallback<XString, Currencies::stSymbolPair>(
  MessageType::ExchangeDataOnline::cmdTradeTickerStart::id(),
  boost::bind(&method, this, _1, _2)
);

RegisterMessageCallback<XString, Currencies::stSymbolPair>(
  MessageType::ExchangeDataOnline::cmdTradeTickerStop::id(),
  boost::bind(&method, this, _1, _2)
);
```

## Trade ticker

- Type: `Message`
- Message: `MessageType::ExchangeDataOnline::onTradeTick(exchange, symbol)`
- Params: `tradeData:stSymbolTimeTradeData`

``` cpp tab="Register"
RegisterMessageCallback<stSymbolTimeTradeData>(
  MessageType::ExchangeDataOnline::onTradeTick(exchange, pair),
  boost::bind(&method, this, _1)
);
```

``` cpp tab="Send"
SendMessage<stSymbolTimeTradeData>(
  MessageType::ExchangeDataOnline::onTradeTick(exchange, symbol),
  dataTradeTick
);
```


## Market Ticker start/stop

- Type: `Message`
- Start: `MessageType::ExchangeDataOnline::cmdMarketTickerStart`
- Stop: `MessageType::ExchangeDataOnline::cmdMarketTickerStop`
- Params: `XString strExchange`

``` cpp tab="Send"
SendMessage<XString>(
  MessageType::ExchangeDataOnline::cmdMarketTickerStart::id(),
  "binance"
);

SendMessage<XString, stSymbolPair, timeframe_t>(
  MessageType::ExchangeDataOnline::cmdMarketTickerStop::id(),
  "binance"
);
```

``` cpp tab="Register"  
RegisterMessageCallback<XString>(
  MessageType::ExchangeDataOnline::cmdMarketTickerStart::id(),
  boost::bind(&method, this, _1)
);

RegisterMessageCallback<XString>(
  MessageType::ExchangeDataOnline::cmdMarketTickerStop::id(),
  boost::bind(&method, this, _1)
);
```

## Market ticker

- Type: `Message`
- Message: `MessageType::ExchangeDataOnline::onMarketTick(exchange)`
- Params: `tradeData:TlstMarketTickers`

``` cpp tab="Register"
RegisterMessageCallback<TlstMarketTickers>(
  MessageType::ExchangeDataOnline::onMarketTick(exchange),
  boost::bind(&method, this, _1)
);
```

``` cpp tab="Send"
SendMessage<TlstMarketTickers>(
  MessageType::ExchangeDataOnline::onMarketTick(exchange ),
  lstMarketTicks
);
```