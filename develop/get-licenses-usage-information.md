---
title: Lisans kullanım bilgilerini alma
description: Office dynamics için iş yükü düzeyinde lisans kullanım bilgilerini alın.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445995"
---
# <a name="get-licenses-usage-information"></a>Lisans kullanım bilgilerini alma

Office dynamics için iş yükü düzeyinde lisans kullanım bilgilerini alın.

## <a name="prerequisites"></a>Önkoşullar

kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="uri-parameters"></a>URI parametreleri

| Parametre         | Tür     | Açıklama | Gerekli |
|-------------------|----------|-------------|----------|
| top               | string   | İstekte geri dönecek veri satırlarının sayısı. Belirtilmezse en büyük değer ve varsayılan değer 10000'tir. Sorguda daha fazla satır varsa yanıt gövdesi, sonraki veri sayfasını talep etmek için kullanabileceğiniz bir sonraki bağlantı içerir. | Hayır |
| Atla              | int      | Sorguda atlana satır sayısı. Büyük veri kümelerini sayfalara yapmak için bu parametreyi kullanın. Örneğin, top=10000 ve skip=0 ilk 10000 veri satırlarını, top=10000 ve skip=10000 sonraki 10000 satırı ve bu şekilde devam ediyor. | Hayır |
| filtre            | string   | *İsteğin* filtre parametresi, yanıtta satırları filtreleen bir veya daha fazla deyim içerir. Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir ve **`eq`** **`ne`** deyimleri veya kullanılarak bir **`and`** araya **`or`** olabilir. Bazı örnek filtre *parametreleri şu* şekildedir:<br/><br/>*filter=workloadCode eq 'SFB'*<br/><br/>*filter=workloadCode eq 'SFB'* veya (*channel eq 'Reseller'*)<br/><br/>Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**Hizmetadı**<br/>**Kanal**<br/>**customerTenantId**<br/>**Müşteriadı**<br/>**Productıd**<br/>**Productname** | Hayır |
| Groupby           | string   | Yalnızca belirtilen alanlara veri toplaması uygulanan bir deyim. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**Hizmetadı**<br/>**channelcustomerTenantId**<br/>**Müşteriadı**<br/>**Productıd**<br/>**Productname**<br/><br/>Döndürülen veri satırları *groupby* parametresinde belirtilen alanları ve şunları içerir:<br/><br/>**licensesActive**<br/>**licensesQualified** | Hayır |
| processedDateTime | DateTime | Kullanım verileri işlenme tarihini belirtebilirsiniz. Verilerin işlenme tarihi varsayılan olarak en son tarihtir | Hayır |

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

Başarılı olursa, yanıt gövdesi lisans kullanımıyla ilgili verileri içeren aşağıdaki alanları içerir.

| Alan             | Tür     | Açıklama                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | string   | İş yükü kodu                                 |
| workloadName      | string   | İş yükü adı                                 |
| serviceCode       | string   | Hizmet kodu                                  |
| Hizmetadı       | string   | Hizmet adı                                  |
| Kanal           | string   | Kanal adı, kurumsal bayi                        |
| customerTenantId  | string   | Müşterinin benzersiz tanımlayıcısı            |
| Müşteriadı      | string   | Müşteri adı                                 |
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
