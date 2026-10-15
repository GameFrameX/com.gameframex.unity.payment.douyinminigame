<div align="center">

<img src="https://download.alianblank.com/gameframex/gameframex_logo_320.png" alt="Game Frame X Logo" width="160" />

# Game Frame X Payment (DouYin Mini Game)

[![License](https://img.shields.io/github/license/GameFrameX/com.gameframex.unity.payment.douyinminigame)](https://github.com/GameFrameX/com.gameframex.unity.payment.douyinminigame/blob/main/LICENSE.md)
[![Version](https://img.shields.io/github/v/release/GameFrameX/com.gameframex.unity.payment.douyinminigame)](https://github.com/GameFrameX/com.gameframex.unity.payment.douyinminigame/releases)
[![Unity Version](https://img.shields.io/badge/Unity-2019.4-black?logo=unity)](https://unity.com/)
[![Documentation](https://img.shields.io/badge/Documentation-docs-blue)](https://gameframex.doc.alianblank.com)

인디 게임 개발자를 위한 올인원 솔루션 · 인디 개발자의 꿈을 실현

<br />

[문서](https://gameframex.doc.alianblank.com) · [빠른 시작](#빠른-시작) · QQ 그룹: 467608841 / 233840761

<br />

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | **한국어**

</div>

## 언어

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | **한국어**

---

## 프로젝트 개요

이 패키지는 GameFrameX.Payment의 '抖音 미니게임 결제' 어댑터입니다. `BasePaymentManager`(`DouYinMiniGamePaymentManager`)를 구현하여, 抖音 미니게임 환경에서 TTSDK를 통해 게임 내 상품 결제 요청을 시작합니다.

## 지원 범위

- 결제 시작: 일회성 상품 (통합된 `Buy(PurchaseParams)` 인터페이스와 `DouYinMiniGamePurchaseParams` 사용).
- iOS: `TTSDK.TT.OpenAwemeCustomerService(...)` 호출 (DIAMOND 통화, `CanIUse.OpenAwemeCustomerServiceParams.GoodType`이 true여야 함; false이면 결제를 시작하지 않음).
- 기타 플랫폼 (Android / 개발자 도구): `TTSDK.TT.RequestGamePayment(...)` 호출.
- 상품명은 `상품ID_상품명`(`ProductId_GoodName`)으로 연결하여 전송합니다.

## 미지원 / 스텁 구현

- `BuyInApp(...)`: 예외 발생 (`Buy(PurchaseParams)`를 사용하세요).
- `BuySubs(...)`: 예외 발생 (抖音 결제는 구독 상품을 지원하지 않음).
- `QueryPurchases(...)` / `ConsumePurchase(...)`: 경고 로그만 출력, 실제 로직 없음.
- `SetPredefinedProductIds(...)`: 빈 구현.
- `Init(...)`: 경고 로그만 출력 (抖音 결제는 초기화가 필요하지 않음).

## 빠른 시작

### 설치

다음 방법 중 하나를 선택하세요:

1. Unity 프로젝트의 `Packages/manifest.json`을 편집하여 `scopedRegistries` 섹션을 추가하세요:
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

   `scopes`는 이 레지스트리를 통해 어떤 패키지를 해석할지 제어합니다. `com.gameframex`로 시작하는 패키지만 이 레지스트리에서 가져옵니다.

2. `manifest.json`의 `dependencies`에 직접 추가:
   ```json
   {
      "com.gameframex.unity.payment.douyinminigame": "https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame.git"
   }
   ```
3. Unity의 **Package Manager**에서 **Git URL**을 사용하여 추가: `https://github.com/gameframex/com.gameframex.unity.payment.douyinminigame.git`
4. 리포지토리를 Unity 프로젝트의 `Packages` 디렉토리에 클론하세요. 자동으로 로드됩니다.
## Buy 매개변수 매핑

`DouYinMiniGamePaymentManager.Buy(purchaseParams)`는 `DouYinMiniGamePurchaseParams`를 요구하며, 필드는 다음과 같이 매핑됩니다:

- `ProductId`: `goodName`의 `상품ID_상품명`(`ProductId_GoodName`) 접두사로 전송됩니다.
- `OrderId`: `customId`로 전달됩니다.
- `Money`: 그대로 `orderAmount`로 전달됩니다 (단위: 분; 이 패키지는 금액에 * 100을 하지 않습니다).
- `GoodName`: `goodName`의 `상품ID_상품명`(`ProductId_GoodName`) 후반부로 전송됩니다 (길이 잘라내기 없음).
- `ExtraInfo`: `extraInfo`로 전달됩니다.

## 결제 결과 처리

이 패키지는 抖音 결제 요청 시작만 담당합니다. TTSDK 결제 결과 콜백과 GameFrameX.Payment 결과 이벤트 브리징은 패키지 내에 캡슐화되어 있지 않습니다. 클라이언트 측에서 결과를 받으려면 抖音 TTSDK에서 제공하는 콜백/이벤트 메커니즘을 사용하거나, 서버 측 주문 콜백에 의존하여 배송 및 검증을 완료하세요.

## 플랫폼 지원

| 플랫폼          | 지원 |
|-----------------|------|
| 抖音 미니게임   | 예   |

## 변경 로그

자세한 내용은 [CHANGELOG.md](CHANGELOG.md)를 참조하세요.


## 의존성

| 패키지 | 설명 |
|--------|------|
| `com.gameframex.unity` | 3.0.0 |
| `com.gameframex.unity.payment` | 2.0.0 |

## 문서 및 자료

- [문서](https://gameframex.doc.alianblank.com)

## 커뮤니티 및 지원

- QQ 그룹: 467608841 / 233840761
## 라이선스

이 프로젝트는 Apache-2.0 라이선스에 따라 배포됩니다. 자세한 내용은 [LICENSE.md](LICENSE.md) 파일을 참조하세요.
