---
title: Fatura ekstresini alma
description: Fatura KIMLIĞINI kullanarak bir fatura ekstresi alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f0324916eb2efd9244530a53b1d7bb4abc0c8e6e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549136"
---
# <a name="get-invoice-statement"></a>Fatura ekstresini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Geçerli bir fatura KIMLIĞI.

## <a name="c"></a>C\#

Bir fatura ekstresini KIMLIĞE göre almak için, **ıpartner.** Invoice koleksiyonunuzu kullanın ve fatura kimliğini kullanarak **byıd (** ) yöntemini çağırın, sonra fatura ekstresini erişmek için **Belgeler ()** ve **Ekstre ()** yöntemlerini çağırın. Son olarak **Get ()** veya **GetAsync ()** yöntemlerini çağırın.

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: partnersdk. featuresample **sınıfı**: getfaturalarestatement. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{INVOICE-ID}/Documents/deyimin http/1.1  |

### <a name="uri-parameter"></a>URI parametresi

Fatura ekstresini almak için aşağıdaki sorgu parametresini kullanın.

| Ad       | Tür       | Gerekli | Açıklama                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| Fatura kimliği | string     | Yes      | Değer, satıcının belirli bir faturaya ait sonuçları filtrelemesine olanak tanıyan bir fatura kimliğidir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir [Faturalarestatement](invoice-resources.md#invoicestatement) kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
