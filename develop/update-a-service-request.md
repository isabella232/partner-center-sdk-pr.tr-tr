---
title: Bir hizmet isteğini güncelleştirme
description: Bir bulut çözümü sağlayıcısı 'nın müşterinin adına Microsoft ile dosyalandığı mevcut bir müşteri hizmeti isteğini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769742"
---
# <a name="update-a-service-request"></a>Bir hizmet isteğini güncelleştirme

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir bulut çözümü sağlayıcısı 'nın müşterinin adına Microsoft ile dosyalandığı mevcut bir müşteri hizmeti isteğini güncelleştirme.

Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir. Sonra sol kenar çubuğundan **hizmet yönetimi** ' ni seçin. **Destek istekleri** üst bilgisi altında, söz konusu hizmet isteğini seçin. Son olarak, hizmet isteğinde istenen değişiklikleri yapıp Gönder ' i seçin **.**

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir hizmet isteği KIMLIĞI.

## <a name="c"></a>C\#

Bir müşterinin hizmet isteğini güncelleştirmek için, hizmet isteği arabirimini tanımlamak ve döndürmek üzere hizmet isteği kimliğiyle [**ıvicerequestcollection. Byıd**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) yöntemini çağırın. Ardından, hizmet isteğini güncelleştirmek için [**ıvicerequest. Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) veya [**patchasync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) metodunu çağırın. Güncelleştirilmiş değerleri sağlamak için yeni ve boş bir [**servicerequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) nesnesi oluşturun ve yalnızca değiştirmek istediğiniz özellik değerlerini ayarlayın. Sonra bu nesneyi düzeltme ekine veya PatchAsync metoduna çağrı içinde geçirin.

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdatePartnerServiceRequest.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem    | İstek URI'si                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **DÜZELTMESI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-ID} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Hizmet isteğini güncelleştirmek için aşağıdaki URI parametresini kullanın.

| Ad                  | Tür     | Gerekli | Açıklama                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **servicerequest kimliği** | **guid** | Y        | Hizmet isteğini tanımlayan bir GUID. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi bir [servicerequest](service-request-resources.md) kaynağı içermelidir. Yalnızca gerekli değerler güncellenmelidir.

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş özelliklerle bir **hizmet isteği** kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
