# [2.0.0](https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame/compare/1.0.2...2.0.0) (2026-10-15)


### Build System

* **package:** 包更名并升级依赖至 2.0.0 ([82c896f](https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame/commit/82c896fe9a7725c00819ef54316cf33691b07ac0))


### Features

* **runtime:** 包与程序集更名并对齐抖音支付流程 ([5ab760b](https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame/commit/5ab760b5d50050a21d1b3c9f5007c82aa4425d6b))


### BREAKING CHANGES

* **package:** UPM 包名变更，manifest.json 需改用新包名引用。
* **runtime:** 程序集名、命名空间、管理器与参数类名全部变更，旧引用需按新名称迁移。

## [2.0.0](https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame/compare/1.0.2...2.0.0) (2026-10-15)


### ⚠ BREAKING CHANGES

* 包名由 `com.gameframex.unity.payment.minigame.douyin` 更名为 `com.gameframex.unity.payment.douyinminigame`（`minigame.douyin` 整合为一段，与 advertisement/setting 等 douyinminigame 包对齐）；程序集更名为 `GameFrameX.Payment.DouYinMiniGame.Runtime`，命名空间变更为 `GameFrameX.Payment.DouYinMiniGame.Runtime`，`MiniGameDouYinPaymentManager` 更名为 `DouYinMiniGamePaymentManager`，`DouyinPurchaseParams` 更名为 `DouYinMiniGamePurchaseParams`

### Features

* 支付流程对齐 Client_Android_DEV DummyLocalizationSdkInterface.Pay：改为 iOS 平台优先判断（platform 为 ios 或包含 ios 时走 `OpenAwemeCustomerService` DIAMOND 币种客服支付，CanIUse 不支持时静默不发起），其余平台（Android/开发者工具）走 `RequestGamePayment` 道具直购；商品名称按 `商品ID_商品名称` 拼接上送，移除 10 字符截断逻辑

## [1.0.2](https://github.com/gameframex/com.gameframex.unity.payment.minigame.douyin/compare/1.0.1...1.0.2) (2026-07-30)


### Bug Fixes

* 更新依赖项版本至 com.gameframex.unity 2.5.1 和 com.gameframex.unity.payment 1.1.0 ([328f912](https://github.com/gameframex/com.gameframex.unity.payment.minigame.douyin/commit/328f91283ccffe31aa2da4cfe76282c9f9493455))

## [1.0.1](https://github.com/gameframex/com.gameframex.unity.payment.minigame.douyin/compare/1.0.0...1.0.1) (2026-06-07)


### Bug Fixes

* 补全包规范文件（LICENSE/CHANGELOG/URL 字段/unity 字段） ([5a19ee8](https://github.com/gameframex/com.gameframex.unity.payment.minigame.douyin/commit/5a19ee860477b450a4d394f50540bea821ece1fc))

# 1.0.0 (2026-03-11)


### Bug Fixes

* 截取抖音支付商品名称超长部分避免错误 ([89a5049](https://github.com/gameframex/com.gameframex.unity.payment.minigame.douyin/commit/89a50493532177199b5fedf6997125200b285d99))


### Features

* **payment:** 添加抖音小游戏支付管理器实现 ([335efa3](https://github.com/gameframex/com.gameframex.unity.payment.minigame.douyin/commit/335efa305f417ae2da3aa1de29903634bae1e60f))
