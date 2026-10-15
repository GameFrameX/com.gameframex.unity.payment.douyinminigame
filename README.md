<div align="center">

<img src="https://download.alianblank.com/gameframex/gameframex_logo_320.png" alt="Game Frame X Logo" width="160" />

# Game Frame X Payment (DouYin Mini Game)

[![License](https://img.shields.io/github/license/GameFrameX/com.gameframex.unity.payment.douyinminigame)](https://github.com/GameFrameX/com.gameframex.unity.payment.douyinminigame/blob/main/LICENSE.md)
[![Version](https://img.shields.io/github/v/release/GameFrameX/com.gameframex.unity.payment.douyinminigame)](https://github.com/GameFrameX/com.gameframex.unity.payment.douyinminigame/releases)
[![Unity Version](https://img.shields.io/badge/Unity-2019.4-black?logo=unity)](https://unity.com/)
[![Documentation](https://img.shields.io/badge/Documentation-docs-blue)](https://gameframex.doc.alianblank.com)

All-in-One Solution for Indie Game Development · Empowering Indie Developers' Dreams

<br />

[Documentation](https://gameframex.doc.alianblank.com) · [Quick Start](#quick-start) · QQ Group: 467608841 / 233840761

<br />

**English** | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

</div>

## Language

**English** | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

---

## Project Overview

This package is the Douyin Mini Game payment adapter for GameFrameX.Payment. It implements a `BasePaymentManager` (`DouYinMiniGamePaymentManager`) for initiating in-game product payment requests through TTSDK in the Douyin Mini Game environment.

## Supported Features

- Payment initiation: One-time products (via the unified `Buy(PurchaseParams)` interface with `DouYinMiniGamePurchaseParams`).
- iOS: Calls `TTSDK.TT.OpenAwemeCustomerService(...)` (DIAMOND currency, requires `CanIUse.OpenAwemeCustomerServiceParams.GoodType` to be true; otherwise does nothing).
- Other platforms (Android / developer tools): Calls `TTSDK.TT.RequestGamePayment(...)`.
- `goodName` is sent as `ProductId_GoodName`.

## Unsupported / Stub Implementations

- `BuyInApp(...)`: Throws an exception (use `Buy(PurchaseParams)` instead).
- `BuySubs(...)`: Throws an exception (Douyin payment does not support subscription products).
- `QueryPurchases(...)` / `ConsumePurchase(...)`: Only outputs warning logs, no actual logic.
- `SetPredefinedProductIds(...)`: Empty implementation.
- `Init(...)`: Only outputs a warning log (Douyin payment does not require initialization).

## Quick Start

### Installation

Choose one of the following methods:

1. Edit your Unity project's `Packages/manifest.json` and add the `scopedRegistries` section:
   ```json
   {
     "scopedRegistries": [
       {
         "name": "GameFrameX",
         "url": "https://gameframex.upm.alianblank.uk",
         "scopes": [
           "com.gameframex"
         ]
       }
     ],
     "dependencies": {
       "com.gameframex.unity.payment.douyinminigame": "2.0.0"
     }
   }
   ```

   `scopes` controls which packages are resolved through this registry. Only packages whose names start with `com.gameframex` will be fetched from it.

2. Add to `manifest.json` dependencies:
   ```json
   {
      "com.gameframex.unity.payment.douyinminigame": "https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame.git"
   }
   ```
3. Use **Package Manager** in Unity with **Git URL**: `https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame.git`
4. Clone the repository into your Unity project's `Packages` directory. It will be loaded automatically.
## Buy Parameter Mapping

`DouYinMiniGamePaymentManager.Buy(purchaseParams)` requires a `DouYinMiniGamePurchaseParams` and maps its fields as follows:

- `ProductId`: Sent as the `ProductId` prefix of `goodName` (`ProductId_GoodName`).
- `OrderId`: Passed to `customId`.
- `Money`: Passed directly as `orderAmount` (unit: fen/cents; this package does not multiply by 100).
- `GoodName`: Sent as the `GoodName` part of `goodName` (`ProductId_GoodName`, no length truncation).
- `ExtraInfo`: Passed to `extraInfo`.

## Payment Result Handling

This package only initiates the Douyin payment request. It does not encapsulate TTSDK payment result callbacks or bridge them with GameFrameX.Payment result events. To receive results on the client side, use the callbacks/events provided by the Douyin TTSDK, or rely on server-side order callbacks for fulfillment and verification.

## Platform Support

| Platform        | Supported |
|-----------------|-----------|
| Douyin MiniGame | Yes       |

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for details.


## Dependencies

| Package | Description |
|---------|-------------|
| `com.gameframex.unity` | 3.0.0 |
| `com.gameframex.unity.payment` | 2.0.0 |

## Documentation & Resources

- [Documentation](https://gameframex.doc.alianblank.com)

## Community & Support

- QQ Group: 467608841 / 233840761
## License

See [LICENSE.md](LICENSE.md) for license information.
