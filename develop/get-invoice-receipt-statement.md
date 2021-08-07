---
title: Fatura makbuz ekstresi alma
description: Fatura kimliğini ve makbuz kimliğini kullanarak bir fatura makbuzu deyimini alınır.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed47eadb377a94363b46cbc5508e5377cee005007698df9077d085705c7b9d08
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990741"
---
# <a name="get-invoice-receipt-statement"></a>Fatura makbuz ekstresi alma

Fatura kimliğini ve makbuz kimliğini kullanarak bir fatura makbuzu deyimini alınır.

> [!IMPORTANT]
> Bu özellik yalnızca Tayvan vergi makbuzları için geçerlidir.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Geçerli bir Fatura Kimliği ve karşılık gelen makbuz kimliği.

## <a name="c"></a>C\#

İş Ortağı Merkezi SDK'sı v1.12.0 ile başlayarak, id ile bir fatura makbuzu deyimi almak için **IPartner.Invoices** koleksiyonu kullanın ve fatura kimliğini kullanarak **ById()** yöntemini arayın, ardından **Makbuzlar** koleksiyonunu çağırarak **ById()** çağrısında bulundurarak **Documents()** ve **Statement()** yöntemlerini fatura makbuzu deyimine erişin. Son olarak **Get() veya** **GetAsync() yöntemlerini** arayın.

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** PartnerSDK.FeatureSample **Sınıfı:** GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Fatura makbuzu deyimini almak için aşağıdaki sorgu parametresini kullanın.

| Ad       | Tür   | Gerekli | Açıklama                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| invoice-id | string | Yes      | Değer, kurumsal bayinin belirli bir faturanın sonuçlarını filtrelemesini sağlayan bir invoice-id değeridir. |
| receipt-id | string | Yes      | Değer, kurumsal bayinin belirli bir fatura için makbuzları filtrelemesini sağlayan bir makbuz kimliğidir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir pdf akışı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
