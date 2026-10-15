<div align="center">

<img src="https://download.alianblank.com/gameframex/gameframex_logo_320.png" alt="Game Frame X Logo" width="160" />

# Game Frame X Payment (DouYin Mini Game)

[![License](https://img.shields.io/github/license/GameFrameX/com.gameframex.unity.payment.douyinminigame)](https://github.com/GameFrameX/com.gameframex.unity.payment.douyinminigame/blob/main/LICENSE.md)
[![Version](https://img.shields.io/github/v/release/GameFrameX/com.gameframex.unity.payment.douyinminigame)](https://github.com/GameFrameX/com.gameframex.unity.payment.douyinminigame/releases)
[![Unity Version](https://img.shields.io/badge/Unity-2019.4-black?logo=unity)](https://unity.com/)
[![Documentation](https://img.shields.io/badge/Documentation-docs-blue)](https://gameframex.doc.alianblank.com)

独立游戏前后端一体化解决方案 · 独立游戏开发者的圆梦大使

<br />

[文档](https://gameframex.doc.alianblank.com) · [快速开始](#快速开始) · QQ群: 467608841 / 233840761

<br />

[English](README.md) | **简体中文** | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

</div>

## 语言

[English](README.md) | **简体中文** | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

---

## 项目简介

本包为 GameFrameX.Payment 的「抖音小游戏支付」适配器，实现了一个 `BasePaymentManager`（`DouYinMiniGamePaymentManager`），用于在抖音小游戏环境下通过 TTSDK 发起游戏内商品支付请求。

## 支持范围

- 支付发起：一次性商品（通过统一的 `Buy(PurchaseParams)` 接口配合 `DouYinMiniGamePurchaseParams`）。
- iOS：调用 `TTSDK.TT.OpenAwemeCustomerService(...)`（DIAMOND 币种，需 `CanIUse.OpenAwemeCustomerServiceParams.GoodType` 为 true，否则不发起支付）。
- 其余平台（Android/开发者工具）：调用 `TTSDK.TT.RequestGamePayment(...)`。
- 商品名称按 `商品ID_商品名称`（`ProductId_GoodName`）拼接上送。

## 不支持/空实现

- `BuyInApp(...)`：抛出异常（请使用 `Buy(PurchaseParams)`）。
- `BuySubs(...)`：抛出异常（抖音支付不支持订阅商品）。
- `QueryPurchases(...)` / `ConsumePurchase(...)`：仅输出警告日志，不执行实际逻辑。
- `SetPredefinedProductIds(...)`：空实现。
- `Init(...)`：仅输出警告日志（抖音支付不需要初始化）。

## 快速开始

### 安装

选择以下任一方式：

1. 编辑 Unity 项目的 `Packages/manifest.json`，添加 `scopedRegistries` 部分：
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

   `scopes` 控制哪些包通过此注册表解析。只有以 `com.gameframex` 开头的包才会从这个注册表获取。

2. 直接在 `manifest.json` 的 `dependencies` 节点下添加以下内容：
   ```json
   {
      "com.gameframex.unity.payment.douyinminigame": "https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame.git"
   }
   ```
3. 在 Unity 的 `Package Manager` 中使用 `Git URL` 的方式添加库，地址为：`https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame.git`
4. 直接下载仓库放置到 Unity 项目的 `Packages` 目录下，会自动加载识别。
## Buy 参数映射

`DouYinMiniGamePaymentManager.Buy(purchaseParams)` 要求传入 `DouYinMiniGamePurchaseParams`，字段映射如下：

- `ProductId`：作为 `goodName` 的 `商品ID_商品名称`（`ProductId_GoodName`）前缀上送。
- `OrderId`：传入 `customId`。
- `Money`：直接作为 `orderAmount` 传入（单位：分；本包不会对金额做 `* 100`）。
- `GoodName`：作为 `goodName` 的 `商品ID_商品名称`（`ProductId_GoodName`）后半段上送（不做长度截断）。
- `ExtraInfo`：传入 `extraInfo`。

## 支付结果处理说明

本包当前只负责发起抖音支付请求，未在包内封装 TTSDK 的支付结果回调与 GameFrameX.Payment 的结果事件桥接。如需在客户端获知结果，请使用抖音 TTSDK 提供的回调/事件机制，或以服务端订单回调为准完成发货与校验。

## 平台支持

| 平台         | 支持 |
|--------------|------|
| 抖音小游戏   | 是   |

## 更新日志

详见 [CHANGELOG.md](CHANGELOG.md)。


## 依赖

| 包 | 说明 |
|----|------|
| `com.gameframex.unity` | 3.0.0 |
| `com.gameframex.unity.payment` | 2.0.0 |

## 文档与资源

- [官方文档](https://gameframex.doc.alianblank.com)

## 社区与支持

- QQ群: 467608841 / 233840761
## 开源协议

该项目根据 Apache-2.0 许可证授权 - 有关详细信息，请参阅 [LICENSE.md](LICENSE.md) 文件。
