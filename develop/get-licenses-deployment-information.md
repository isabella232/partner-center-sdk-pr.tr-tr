---
title: Lisans dağıtım bilgilerini alma
description: Office ve Dynamics lisansları için dağıtım bilgilerini alın.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c47ab4f839c102c7a7bcab0169bf13955ab49beb97c48800e882598714347e67
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990724"
---
# <a name="get-licenses-deployment-information"></a>Lisans dağıtım bilgilerini alma

Office ve Dynamics lisansları için dağıtım bilgilerini alın.

## <a name="prerequisites"></a>Önkoşullar

kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="uri-parameters"></a>URI parametreleri

| Parametre         | Tür     | Açıklama | Gerekli |
|-------------------|----------|-------------|----------|
| top               | string   | İstekte geri dönecek veri satırlarının sayısı. Belirtilmezse en büyük değer ve varsayılan değer 10000'tir. Sorguda daha fazla satır varsa yanıt gövdesi, sonraki veri sayfasını talep etmek için kullanabileceğiniz bir sonraki bağlantı içerir. | No |
| Atla              | int      | Sorguda atlana satır sayısı. Büyük veri kümelerini sayfalara yapmak için bu parametreyi kullanın. Örneğin, top=10000 ve skip=0 ilk 10000 veri satırlarını, top=10000 ve skip=10000 sonraki 10000 satırı ve bu şekilde devam ediyor. | No |
| filtre            | string   | *İsteğin* filtre parametresi, yanıtta satırları filtreleen bir veya daha fazla deyim içerir. Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir ve `eq` `ne` deyimleri veya kullanılarak bir `and` araya `or` olabilir. Bazı örnek filtre *parametreleri şu* şekildedir:<br/><br/> *filter=serviceCode eq 'O365'*<br/> *filter=serviceCode eq 'O365'* veya (*channel eq 'Reseller'*)<br/><br/> Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**serviceCode**<br/>**Hizmetadı**<br/>**Kanal**<br/>**customerTenantId**<br/>**Müşteriadı**<br/>**Productıd**<br/>**Productname**  | No |
| Groupby           | string   | Yalnızca belirtilen alanlara veri toplaması uygulanan bir deyim. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>**serviceCode**<br/>**Hizmetadı**<br/>**Kanal**<br/>**customerTenantId**<br/>**Müşteriadı**<br/>**Productıd**<br/>**Productname**<br/><br/> Döndürülen veri satırları *groupby* parametresinde belirtilen alanları ve şunları içerir:<br/><br/>**dağıtılan lisanslar**<br/>**licensesSold**  | No |
| processedDateTime | DateTime | Kullanım verileri işlenme tarihini belirtebilirsiniz. Verilerin işlenme tarihi varsayılan olarak en son tarihtir | No |

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

Başarılı olursa, yanıt gövdesi dağıtılan lisanslar hakkında verileri içeren aşağıdaki alanları içerir.

| Alan             | Tür     | Description                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | string   | Hizmet kodu                          |
| Hizmetadı       | string   | Hizmet adı                          |
| Kanal           | string   | Kanal adı, kurumsal bayi                |
| customerTenantId  | string   | Müşterinin benzersiz tanımlayıcısı    |
| Müşteriadı      | string   | Müşteri adı                         |
| productId         | string   | Ürün için benzersiz tanımlayıcı     |
| Productname       | string   | Ürün adı                          |
| dağıtılan lisanslar  | long     | Dağıtılan lisans sayısı           |
| licensesSold      | long     | Satılan lisans sayısı               |
| processedDateTime | DateTime | Verilerin son işlenme tarihi |

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
