---
ms.assetid: 038903d6-efab-4da6-96b5-046c7431e6e7
description: アプリのレビューに返信を送るには、Microsoft Store レビュー API の以下のメソッドを使います。
title: レビューに対する返信の送信
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, Store サービス, Microsoft Store レビュー API, アドオンの入手数
ms.localizationpriority: medium
ms.openlocfilehash: c08dcda52940f0218b6fdb5be147f058eca7479a
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57623837"
---
# <a name="submit-responses-to-reviews"></a>レビューに対する返信の送信


アプリのレビューにプログラムで返信するには、Microsoft Store レビュー API の以下のメソッドを使います。 このメソッドを呼び出すときは、返信するレビューの ID を指定する必要があります。 レビュー ID は、Microsoft Store 分析 API の[アプリのレビューの取得](get-app-reviews.md)メソッドの応答データ、および[レビュー レポート](../publish/reviews-report.md)の[オフライン ダウンロード](../publish/download-analytic-reports.md)で取得できます。

顧客はレビューを送信するときに、レビューへの返信を受け取らないことを選択できます。 顧客が返信を受け取らないように指定しているレビューに返信すると、このメソッドの返信の本文には、返信ができなかったことが示されます。 このメソッドを呼び出す前に、任意で、[アプリのレビューへの返信情報の取得](get-response-info-for-app-reviews.md)メソッドを使用して、特定のレビューへの返信が許可されているかどうかを確認できます。

> [!NOTE]
> に加えて、このメソッドを使用してプログラムでのレビューに応答する、またはに対応できるレビュー[パートナー センターを使用して](../publish/respond-to-customer-reviews.md)します。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store レビュー API に関するすべての[前提条件](respond-to-reviews-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](respond-to-reviews-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。
* 返信するレビューの ID を取得します。 レビュー ID は、Microsoft Store 分析 API の[アプリのレビューの取得](get-app-reviews.md)メソッドの応答データ、および[レビュー レポート](../publish/reviews-report.md)の[オフライン ダウンロード](../publish/download-analytic-reports.md)で取得できます。

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| POST    | ```https://manage.devcenter.microsoft.com/v1.0/my/reviews/responses``` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

このメソッドには要求パラメーターはありません。


### <a name="request-body"></a>要求本文

要求本文には次の値が含まれます。

| 値        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------|
| Responses | array | 提出する返信を含むオブジェクトの配列です。 各オブジェクトのデータの詳細については、以下の表を参照してください。 |


*Responses* 配列内の各オブジェクトには、次の値が保持されています。

| 値        | 種類   | 説明           |  必須  |
|---------------|--------|-----------------------------|-----|
| ApplicationId | string |  返信対象のレビューがあるアプリのストア ID です。 Store ID は、[アプリ id のページ](../publish/view-app-identity-details.md)パートナー センターの。 ストア ID は、たとえば 9WZDNCRFJ3Q8 のような文字列です。   |  〇  |
| ReviewId | string |  返信するレビューの ID です (これは GUID です)。 レビュー ID は、Microsoft Store 分析 API の[アプリのレビューの取得](get-app-reviews.md)メソッドの応答データ、および[レビュー レポート](../publish/reviews-report.md)の[オフライン ダウンロード](../publish/download-analytic-reports.md)で取得できます。   |  〇  |
| ResponseText | string | 提出する返信です。 返信は、[こちらのガイドライン](../publish/respond-to-customer-reviews.md#guidelines-for-responses)に従う必要があります。   |  〇  |
| SupportEmail | string | アプリのサポート メール アドレスです。顧客はこのアドレスを使用して、直接連絡できます。 したがって、有効なメール アドレスである必要があります。     |  〇  |
| IsPublic | ブール値 |  指定した場合**true**応答、アプリのストアの一覧から、顧客のレビューのすぐ下に表示され、は、すべてのお客様に表示されます。 指定した場合**false**と、ユーザーが電子メールの応答を受信しないことを選択、応答は、電子メールや顧客に送信され、アプリのストアの一覧で他のユーザーに表示されません。 指定した場合**false**され、ユーザーが電子メールの応答を受信しないことを選択、エラーが返されます。   |  〇  |


### <a name="request-example"></a>要求の例

次の例は、このメソッドを使用して、いくつかのレビューに返信を提出する方法を示しています。

```json
POST https://manage.devcenter.microsoft.com/v1.0/my/reviews/responses HTTP/1.1
Authorization: Bearer <your access token>
Content-Type: application/json
{
  "Responses": [
    {
      "ApplicationId": "9WZDNCRFJ3Q8",
      "ReviewId": "6be543ff-1c9c-4534-aced-af8b4fbe0316",
      "ResponseText": "Thank you for pointing out this bug. I fixed it and published an update, you should have the fix soon",
      "SupportEmail": "support@contoso.com",
      "IsPublic": "true"
    },
    {
      "ApplicationId": "9NBLGGH1RP08",
      "ReviewId": "80c9671a-96c2-4278-bcbc-be0ce5a32a7c",
      "ResponseText": "Thank you for submitting your review. Can you tell more about what you were doing in the app when it froze? Thanks very much for your help.",
      "SupportEmail": "support@contoso.com",
      "IsPublic": "false"
    }
  ]
}
```

## <a name="response"></a>応答

### <a name="response-body"></a>応答本文

| Value        | 種類   | 説明            |
|---------------|--------|---------------------|
| 結果 | array | 提出した各返信についてのデータを保持するオブジェクトの配列です。 各オブジェクトのデータの詳細については、以下の表を参照してください。  |


*Result* 配列内の各オブジェクトには、次の値が保持されています。

| Value        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------|
| ApplicationId | string |  返信対象のレビューがあるアプリのストア ID です。 ストア ID は、たとえば 9WZDNCRFJ3Q8 のような文字列です。   |
| ReviewId | string |  返信するレビューの ID です。 これは GUID です。   |
| Successful | string | 値が **true** の場合、返信が正常に送信されたことを示します。 値が **false** の場合、返信は提出できなかったことを示します。    |
| FailureReason | string | **Successful** が **false** の場合、この値には失敗の理由が含まれます。 **Successful** が **true** の場合、この値は空です。      |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Result": [
    {
      "ApplicationId": "9WZDNCRFJ3Q8",
      "ReviewId": "6be543ff-1c9c-4534-aced-af8b4fbe0316",
      "Successful": "true",
      "FailureReason": ""
    },
    {
      "ApplicationId": "9NBLGGH1RP08",
      "ReviewId": "80c9671a-96c2-4278-bcbc-be0ce5a32a7c",
      "Successful": "false",
      "FailureReason": "No Permission"
    }
  ]
}
```

## <a name="related-topics"></a>関連トピック

* [パートナー センターを使用して顧客レビューに応答します。](../publish/respond-to-customer-reviews.md)
* [Microsoft Store サービスを使用してレビューに応答します。](respond-to-reviews-using-windows-store-services.md)
* [アプリのレビューの応答情報を取得します。](get-response-info-for-app-reviews.md)
* [アプリのレビューを取得します。](get-app-reviews.md)
