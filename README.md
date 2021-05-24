# DevCartelGateway64
![GitHub release](https://img.shields.io/github/release/devcartel/devcartelgateway64.svg)
![platform](https://img.shields.io/badge/platform-win-lightgray.svg)
[![GitHub](https://img.shields.io/github/license/devcartel/devcartelgateway64.svg)](https://github.com/devcartel/devcartelgateway64/blob/master/LICENSE.txt)
[![downloads](https://img.shields.io/github/downloads/devcartel/devcartelgateway64/total.svg)](https://github.com/devcartel/devcartelgateway64/releases)
[![Enterprise Support](https://img.shields.io/badge/DevCartelGateway64%20Enterprise%20Support-%24249%2Fmonth-orange.svg?style=social&logo=paypal)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=EKWFY7M7APA5E)

Built with MT5 gateway API, DevCartelGateway64 accepts connection from MT5 platform and connects to a remote PyMT5 application. It accepts various data types from PyMT5. For complete protocol and documentation, visit [PyMT5 GitHub](https://github.com/devcartel/pymt5).

<p align="center">
    <img src="http://media.virbcdn.com/cdn_images/resize_1024x1365/5b/ac5a58aa5703cc1b-ScreenShot2018-09-08at103035.png" alt="application" width="800"/>
</p>

## Installation
* Download a gateway package from our [releases](https://github.com/devcartel/devcartelgateway64/releases)
* Unzip the package and put the whole folder in MT5 platform's gateway directory e.g. `D:\MetaTrader 5 Platform\History\Gateway`

## Launching
* On MT5 Administrator, add a gateway by choosing *DevCartelGateway64*
* *Trading server* should be an IP address and port of a [PyMT5](https://github.com/devcartel/pymt5) server application <br /><br /><img width="584" alt="Launching gateway" src="https://user-images.githubusercontent.com/3415706/39416673-04c8d3aa-4c79-11e8-903a-a3121e864f65.png"><br /><br />
* Click OK and the gateway will establish connection to your PyMT5 application

## Gateway Network Protocol
TCP socket.

## Message Format
Message is composed of `Header+Body+<LF>` where each field in `Body` is demilited using ASCII SOH (`\x01`) and must be prefixed by the `Header`. Each message is ended with ASCII LF (`\x0A`), for example:

```python
ver=3<SOH>type=3<SOH>tag1=value1<SOH>tag2=value2<SOH>...<SOH>tagN=valueN<LF>
```

In this documentation, light vertical bar character (`❘`) represents the delimiter ASCII SOH.

## Message Type
### Login
| Tag<img width=200/> | Comments<img width=520/> |
| ------------------- | ------------------------ |
| _Header_            | `ver=3❘type=1`           |
| _Body_              |                          |
| `login`             |                          |
| `password`          |                          |
| `res`               | `0` - ok<br/>`2` - error |

### Logout
| Tag<img width=200/> | Comments<img width=520/> |
| ------------------- | ------------------------ |
| _Header_            | `ver=3❘type=2`           |
| _Body_              | _None_                   |



### Symbol
| Tag<img width=200/>  | Comments<img width=520/>                                                                                                                                                     |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Header_             | `ver=3❘type=3`                                                                                                                                                               |
| _Body_               |                                                                                                                                                                              |
| `index`              | Symbol index                                                                                                                                                                 |
| `symbol`             |                                                                                                                                                                              |
| `path`               |                                                                                                                                                                              |
| `description`        |                                                                                                                                                                              |
| `page`               |                                                                                                                                                                              |
| `currency_base`      |                                                                                                                                                                              |
| `currency_profit`    |                                                                                                                                                                              |
| `currency_margin`    |                                                                                                                                                                              |
| `digits`             |                                                                                                                                                                              |
| `tick_flags`         |                                                                                                                                                                              |
| `calc_mode`          |                                                                                                                                                                              |
| `exec_mode`          |                                                                                                                                                                              |
| `chart_mode`         |                                                                                                                                                                              |
| `fill_flags`         |                                                                                                                                                                              |
| `expir_flags`        |                                                                                                                                                                              |
| `tick_value`         |                                                                                                                                                                              |
| `tick_size`          |                                                                                                                                                                              |
| `contract_size`      |                                                                                                                                                                              |
| `volume_min`         |                                                                                                                                                                              |
| `volume_max`         |                                                                                                                                                                              |
| `volume_step`        |                                                                                                                                                                              |
| `market_depth`       |                                                                                                                                                                              |
| `margin_flags`       |                                                                                                                                                                              |
| `margin_initial`     |                                                                                                                                                                              |
| `margin_maintenance` |                                                                                                                                                                              |
| `margin_long`        |                                                                                                                                                                              |
| `margin_short`       |                                                                                                                                                                              |
| `margin_limit`       |                                                                                                                                                                              |
| `margin_stop`        |                                                                                                                                                                              |
| `margin_stop_limit`  |                                                                                                                                                                              |
| `settlement_price`   |                                                                                                                                                                              |
| `price_limit_max`    |                                                                                                                                                                              |
| `price_limit_min`    |                                                                                                                                                                              |
| `time_start`         | Trading start date                                                                                                                                                           |
| `time_expiration`    | Trading expiration date                                                                                                                                                      |
| `trade_mode`         | `0` - trade disabled<br/>`1` - only long positions allowed<br/>`2` - only short positions allowed<br/>`3` - only position closure<br/>`4` - all trade operations are allowed |

### Tick
| Tag<img width=200/> | Comments<img width=520/>             |
| ------------------- | ------------------------------------ |
| _Header_            | `ver=3❘type=4`                       |
| _Body_              |                                      |
| `symbol`            |                                      |
| `bank`              |                                      |
| `bid`               |                                      |
| `ask`               |                                      |
| `last`              |                                      |
| `volume`            |                                      |
| `datetime`          | POSIX timestamp e.g. `1523278796000` |


### Order
| Tag<img width=200/> | Comments<img width=520/>                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Header_            | `ver=3❘type=5`                                                                                                                                                                                                                                                                                                                                                                                                        |
| _Body_              |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `symbol`            |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `bank`              |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `bid`               |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `ask`               |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `last`              |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `volume`            |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `datetime`          | POSIX timestamp e.g. `1523278796000`                                                                                                                                                                                                                                                                                                                                                                                  |
| `order_action`      | `1` - new<br/>`2` - modify<br/>`3` - cancel                                                                                                                                                                                                                                                                                                                                                                           |
| `state`             | `0` - unkonwn<br/>`1` - confirmed<br/>`2` - placed<br/>`3` - new<br/>`4` - rejected<br/>`5` - deal<br/>`6` - modification received<br/>`7` - modified<br/>`8` - modification rejected<br/>`9` - cancelation received<br/>`10` - canceled<br/>`11` - cancelation rejected<br/>`20` - complete                                                                                                                          |
| `order`             | MT order ticket                                                                                                                                                                                                                                                                                                                                                                                                       |
| `exchange_id`       | Exchange order ID                                                                                                                                                                                                                                                                                                                                                                                                     |
| `custom_data`       |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `request_id`        |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `symbol`            |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `login`             | MT client login                                                                                                                                                                                                                                                                                                                                                                                                       |
| `type_order`        | `0` - buy market<br/>`1` - sell<br/>`2` - buy limit<br/>`3` - sell limit<br/>`4` - buy stop<br/>`5` - sell stop<br/>`6` - buy stop limit<br/>`7` - sell stop limit                                                                                                                                                                                                                                                    |
| `type_time`         | `0` - good till cancel<br/>`1` - good till day<br/>`2` - good till specified<br/>`3` - good till specified day                                                                                                                                                                                                                                                                                                        |
| `action`            | Client action:<br/>`0` - prices for<br/>`1` - request<br/>`2` - instant<br/>`3` - market<br/>`4` - exchange<br/>`5` - pending<br/>`6` - stop loss/taking profit<br/>`7` - modify<br/>`8` - cancel<br/>`100` - activate<br/>`101` - activate stop loss<br/>`102` - activate take profit<br/>`103` - activate stop-limit order<br/>`104` - delete stop-out order<br/>`105` - close stop-out position<br/>`106` - expire |
| `price_order`       |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `price_sl`          | Stop Loss level                                                                                                                                                                                                                                                                                                                                                                                                       |
| `price_tp`          | Take Profit level                                                                                                                                                                                                                                                                                                                                                                                                     |
| `price_tick_bid`    | Symbol bid price in external trading system                                                                                                                                                                                                                                                                                                                                                                           |
| `price_tick_ask`    | Symbol ask price in external trading system                                                                                                                                                                                                                                                                                                                                                                           |
| `volume`            |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `expiration_time`   |                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `result`            | Result of order processing:<br/>`1` - ok<br/>`10006` - rejected<br/>`10007` - canceled<br/>`10008` - placed<br/>`10009` - complete<br/>                                                                                                                                                                                                                                                                               |

### Heartbeat
| Tag<img width=200/> | Comments<img width=520/> |
| ------------------- | ------------------------ |
| _Header_            | `ver=3❘type=6`           |
| _Body_              | _None_                   |

### Deal
| Tag<img width=200/> | Comments<img width=520/> |
| ------------------- | ------------------------ |
| _Header_            | `ver=3❘type=8`           |
| _Body_              |                          |
| `exchange_id`       | Exchange order ID        |
| `order`             | Order exchange ticket    |
| `symbol`            |                          |
| `login`             | MT client's login        |
| `type_deal`         | `0` - buy<br/>`1` - sell |
| `volume`            | Deal volume              |
| `volume_rem`        | Non-filled volume        |
| `price`             | Lot price                |
| _Optional_          |                          |
| `datetime`          | Deal timestamp           |
| `comment`           |                          |
| `position`          | Position ID              |

### External Deal
| Tag<img width=200/> | Comments<img width=520/> |
| ------------------- | ------------------------ |
| _Header_            | `ver=3❘type=50`          |
| _Body_              |                          |
| `exchange_id`       | Exchange order ID        |
| `order`             | Order exchange ticket    |
| `symbol`            |                          |
| `login`             | MT client's login        |
| `type_deal`         | `0` - buy<br/>`1` - sell |
| `volume`            | Deal volume              |
| `volume_rem`        | Non-filled volume        |
| `price`             | Lot price                |
| _Optional_          |                          |
| `datetime`          | Deal timestamp           |
| `comment`           |                          |

## Support
* Report an issue [here](https://github.com/devcartel/devcartelgateway64/issues)

## Changelog
1.3.0
* 22 January 2021
* Make `datetime` in deal message optional
* Make `comment` in deal message optional

1.2.0
* 6 August 2020
* Supports comment field in external deal

1.1.0
* 26 April 2018
* Supports external deal DatetimeMsc

1.0.0
* 13 April 2018
* Supports login, logout, order, confirm, deal
* Supports external deal submission to MT5
