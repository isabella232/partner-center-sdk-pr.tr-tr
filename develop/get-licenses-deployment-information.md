---
title: Lisans dağıtım bilgilerini alma
description: Office ve Dynamics lisanslarıyla ilgili dağıtım bilgilerini alma.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769436"
---
# <a name="get-licenses-deployment-information"></a>Lisans dağıtım bilgilerini alma

**Uygulama hedefi**

- İş Ortağı Merkezi

Office ve Dynamics lisanslarıyla ilgili dağıtım bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Analtics/, CIAL/Deployment/License/http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="uri-parameters"></a>URI parametreleri

| Parametre         | Tür     | Açıklama | Gerekli |
|-------------------|----------|-------------|----------|
| top               | string   | İstekte döndürülecek veri satır sayısı. Belirtilen en büyük değer ve varsayılan değer 10000 ' dir. Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir. | No |
| Atla              | int      | Sorgudaki atlanacak satır sayısı. Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın. Örneğin, top = 10000 ve Skip = 0 verilerin ilk 10000 satırını alır, top = 10000 ve Skip = 10000 sonraki 10000 satırlık verileri alır ve bu şekilde devam eder. | No |
| filtre            | string   | İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor. Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir `eq` `ne` ve deyimler or kullanılarak birleştirilebilir `and` `or` . Aşağıda bazı örnek *filtre* parametreleri verilmiştir:<br/><br/> *Filter = serviceCode EQ ' O365 '*<br/> *Filter = serviceCode EQ ' O365 '* veya (*Channel EQ ' Bayi '*)<br/><br/> Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**serviceCode**<br/>**HizmetAdı**<br/>**kanalla**<br/>**Customertenantıd**<br/>**customerName**<br/>**ProductID**<br/>**productName**  | No |
| ölçütü           | string   | Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**serviceCode**<br/>**HizmetAdı**<br/>**kanalla**<br/>**Customertenantıd**<br/>**customerName**<br/>**ProductID**<br/>**productName**<br/><br/> Döndürülen veri satırları, *GroupBy* parametresinde belirtilen alanları ve aşağıdakileri içerir:<br/><br/>**Licensesdağıtıldı**<br/>**Lisanssesseski**  | No |
| processedDateTime | DateTime | Bunlardan biri, kullanım verilerinin işlendiği tarihi belirtebilir. Verilerin işlendiği tarih varsayılan olarak en geç | No |

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi dağıtılan lisanslar hakkında veri içeren aşağıdaki alanları içerir.

| Alan             | Tür     | Description                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | string   | Hizmet kodu                          |
| HizmetAdı       | string   | Hizmet adı                          |
| kanalla           | string   | Kanal adı, satıcı                |
| Customertenantıd  | string   | Müşteri için benzersiz tanımlayıcı    |
| customerName      | string   | Müşteri adı                         |
| productId         | string   | Ürün için benzersiz tanımlayıcı     |
| productName       | string   | Ürün adı                          |
| Licensesdağıtıldı  | long     | Dağıtılan lisansların sayısı           |
| Lisanssesseski      | long     | Satılan lisansların sayısı               |
| processedDateTime | DateTime | Verilerin son işlendiği tarih |

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT
{
  "Value": [

{
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
