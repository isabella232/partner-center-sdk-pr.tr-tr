---
title: Lisans kullanım bilgilerini alma
description: Office ve Dynamics için iş yükü düzeyinde lisans kullanım bilgileri alma.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769430"
---
# <a name="get-licenses-usage-information"></a>Lisans kullanım bilgilerini alma

**Uygulama hedefi**

- İş Ortağı Merkezi

Office ve Dynamics için iş yükü düzeyinde lisans kullanım bilgileri alma.

## <a name="prerequisites"></a>Önkoşullar

[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Analtics/, CIAL/Usage/License/http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="uri-parameters"></a>URI parametreleri

| Parametre         | Tür     | Açıklama | Gerekli |
|-------------------|----------|-------------|----------|
| top               | string   | İstekte döndürülecek veri satır sayısı. Belirtilen en büyük değer ve varsayılan değer 10000 ' dir. Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir. | No |
| Atla              | int      | Sorgudaki atlanacak satır sayısı. Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın. Örneğin, top = 10000 ve Skip = 0 verilerin ilk 10000 satırını alır, top = 10000 ve Skip = 10000 sonraki 10000 satırlık verileri alır ve bu şekilde devam eder. | No |
| filtre            | string   | İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor. Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir **`eq`** **`ne`** ve deyimler or kullanılarak birleştirilebilir **`and`** **`or`** . Aşağıda bazı örnek *filtre* parametreleri verilmiştir:<br/><br/>*Filter = workloadCode EQ ' SFB '*<br/><br/>*Filter = workloadCode EQ ' SFB '* veya (*Channel EQ ' Bayi '*)<br/><br/>Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**HizmetAdı**<br/>**kanalla**<br/>**Customertenantıd**<br/>**customerName**<br/>**ProductID**<br/>**productName** | No |
| ölçütü           | string   | Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**HizmetAdı**<br/>**Channelcustomertenantıd**<br/>**customerName**<br/>**ProductID**<br/>**productName**<br/><br/>Döndürülen veri satırları, *GroupBy* parametresinde belirtilen alanları ve aşağıdakileri içerir:<br/><br/>**licensesActive**<br/>**Lisans nitelikli** | No |
| processedDateTime | DateTime | Bunlardan biri, kullanım verilerinin işlendiği tarihi belirtebilir. Verilerin işlendiği tarih varsayılan olarak en geç | No |

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi, lisans kullanımı hakkında veri içeren aşağıdaki alanları içerir.

| Alan             | Tür     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | string   | İş yükü kodu                                 |
| workloadName      | string   | İş yükü adı                                 |
| serviceCode       | string   | Hizmet kodu                                  |
| HizmetAdı       | string   | Hizmet adı                                  |
| kanalla           | string   | Kanal adı, satıcı                        |
| Customertenantıd  | string   | Müşteri için benzersiz tanımlayıcı            |
| customerName      | string   | Müşteri adı                                 |
| productId         | string   | Ürün için benzersiz tanımlayıcı             |
| productName       | string   | Ürün adı                                  |
| licensesActive    | long     | İş yükü başına etkin lisans sayısı        |
| Lisans nitelikli | long     | İş yükü için uygun lisans sayısı |
| processedDateTime | DateTime | Verilerin son işlendiği tarih         |

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
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
