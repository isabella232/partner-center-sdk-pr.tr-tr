---
title: Fatura makbuz ekstresi alma
description: Fatura KIMLIĞI ve giriş KIMLIĞI ' ni kullanarak bir fatura alındısı ekstresi alır.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768711"
---
# <a name="get-invoice-receipt-statement"></a>Fatura makbuz ekstresi alma

**Uygulama hedefi**

- İş Ortağı Merkezi

Fatura KIMLIĞI ve giriş KIMLIĞI ' ni kullanarak bir fatura alındısı ekstresi alır.

> [!IMPORTANT]
> Bu özellik yalnızca Tayvan vergi alındıları için geçerlidir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Geçerli bir fatura KIMLIĞI ve buna karşılık gelen bir giriş KIMLIĞI.

## <a name="c"></a>C\#

Iş Ortağı Merkezi SDK v 1.12.0 'den başlayarak, KIMLIĞE göre fatura alındı bilgisi almak için, **ıpartner.** Invoice koleksiyonunuzu kullanın ve fatura kimliğini kullanarak **byıd ()** yöntemini çağırın, ardından **alındılar** koleksiyonunu çağırın ve **Byıd (** ) çağrısı yapın ve ardından **Belgeler ()** ve **Ekstre ()** yöntemlerini çağırarak fatura alındısı bildirimine erişin. Son olarak **Get ()** veya **GetAsync ()** yöntemlerini çağırın.

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Partnersdk. Featuresample **sınıfı**: GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{INVOICE-ID}/POTS/{pot-id}/Documents/deyimin http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Fatura alındısı ekstresini almak için aşağıdaki sorgu parametresini kullanın.

| Ad       | Tür   | Gerekli | Açıklama                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| Fatura kimliği | string | Yes      | Değer, satıcının belirli bir faturaya ait sonuçları filtrelemesine olanak tanıyan bir fatura kimliğidir. |
| makbuz kimliği | string | Yes      | Değer, satıcının belirli bir faturaya ait alındıları filtrelemesine olanak tanıyan bir makbuz kimliğidir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir PDF akışı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

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
