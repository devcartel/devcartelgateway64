# DevCartelGateway64
Built with MT5 gateway API, DevCartelGateway64 accepts connection from MT5 platform and connects to a remote PyMT5 application. It accepts various data types from PyMT5. For complete protocol and documentation, visit [PyMT5 GitHub](https://github.com/devcartel/pymt5).

## Installation
* Download a gateway package from our [releases](https://github.com/devcartel/devcartelgateway64/releases)
* Unzip the package and put the whole folder in MT5 platform's gateway directory e.g. `D:\MetaTrader 5 Platform\History\Gateway`

## Launching
* On MT5 Administrator, add a gateway by choosing *DevCartelGateway64*
* *Trading server* should be an IP address and port of a [PyMT5](https://github.com/devcartel/pymt5) server application <br /><br /><img width="584" alt="Launching gateway" src="https://user-images.githubusercontent.com/3415706/39416673-04c8d3aa-4c79-11e8-903a-a3121e864f65.png"><br /><br />
* Click OK and the gateway will establish connection to your PyMT5 application

## Message Format
Message is composed of `Header+Body+<LF>` where each field in `Body` is demilited using ASCII SOH (`\x01`). Each message is ended with ASCII LF (`\x0A`) e.g.:

* `key1=value1<SOH>key2=value2<SOH>...<SOH>keyN=valueN<LF>`

In this documentation, pipe character (`|`) represents the delimiter ASCII SOH.

Message type    | Header                          | Body
----------------|---------------------------------|------
Login           | <code>ver=3&#124;type=1</code>  | `login`,`password`,`res`
Logout          | <code>ver=3&#124;type=2</code>  | _None_
Symbol          | <code>ver=3&#124;type=3</code>  | `index`,`symbol`,`path`,`description`,`page`,`currency_base`,<br />`currency_profit`,`currency_margin`,`digits`,`tick_flags`,<br />`calc_mode`,`exec_mode`,`chart_mode`,`fill_flags`,<br />`expir_flags`,`tick_value`,`tick_size`,`contract_size`,<br />`volume_min`,`volume_max`,`volume_step`,`market_depth`,<br />`margin_flags`,`margin_initial`,`margin_maintenance`,<br />`margin_long`,`margin_short`,`margin_limit`,`margin_stop`,<br />`margin_stop_limit`,`settlement_price`,`price_limit_max`,<br />`price_limit_min`,`time_start`,`time_expiration`,`trade_mode`
Tick            | <code>ver=3&#124;type=4</code>  | `symbol`,`bank`,`bid`,`ask`,`last`,`volume`,`datetime`
Order           | <code>ver=3&#124;type=5</code>  | `symbol`,`bank`,`bid`,`ask`,`last`,`volume`,`datetime`,<br />`order_action`,`state`,`order`,`exchange_id`,`custom_data`,<br />`request_id`,`symbol`,`login`,`type_order`,`type_time`,<br />`action`,`price_order`,`price_sl`,`price_tp`,`price_tick_bid`,<br />`price_tick_ask`,`volume`,`expiration_time`,`result`
Heartbeat       | <code>ver=3&#124;type=6</code>  | _None_
Deal            | <code>ver=3&#124;type=8</code>  | `exchange_id`,`order`,`symbol`,`login`,`type_deal`,`volume`,<br />`volume_rem`,`price`
External Deal   | <code>ver=3&#124;type=50</code> | `exchange_id`,`order`,`symbol`,`login`,`type_deal`,`volume`,<br />`volume_rem`,`price`,`datetime`

## Support
* Report an issue [here](https://github.com/devcartel/devcartelgateway64/issues)

## Changelog
1.1.0
* 26 April 2018
* Supports external deal DatetimeMsc

1.0.0
* 13 April 2018
* Supports login, logout, order, confirm, deal
* Supports external deal submission to MT5
