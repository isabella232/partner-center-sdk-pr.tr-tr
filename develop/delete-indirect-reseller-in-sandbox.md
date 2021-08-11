---
title: Korumalı Alanda Dolaylı Kurumsal Bayiyi Silme
description: Korumalı Alan Dolaylı Kurumsal Bayilerini silme ve API'leri kullanarak 2.00.000 testi etkinleştirme hakkında bilgi sağlar.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 708fedd4e34b2242aae6e6e0ac673ce77524d448dcee4a05877d37b5266e44c8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994940"
---
# <a name="delete-indirect-reseller-in-sandbox"></a>Korumalı Alanda Dolaylı Kurumsal Bayiyi Silme

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Bu belgede, Korumalı Alan Dolaylı Sağlayıcılarının nasıl silinecek ve API'ler kullanılarak esn nasıl testlerin etkinleştirildi?

> [!Important]
> Bu belgede, Dolaylı Model deneyimleri için yalnızca Korumalı Alan ortamında izin verilen özellikler açıkmaktadır.

## <a name="prerequisites"></a>Önkoşullar

- Kimlik Doğrulaması altında açıklandığı [gibi İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a>Korumalı Alan Dolaylı Sağlayıcısı – Korumalı Alan Dolaylı Kurumsal Bayiyi Silme 

Bu özellik yalnızca Korumalı Alanda kullanılabilir ve Korumalı Alan Dolaylı Sağlayıcılarına Korumalı Alan Dolaylı Kurumsal Bayileri oluşturma olanağı sağlar.

1. Korumalı Alan Dolaylı Kurumsal Bayiyi Silme Önkoşulları
    1. Korumalı Alan Dolaylı Kurumsal Bayinin her müşterisi için abonelikleri askıya alma
    2. Dolaylı Kurumsal Bayinin tüm müşterilerini silme
2. Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen beş Korumalı Alan Dolaylı Kurumsal Bayi sınırı. Korumalı Alan Dolaylı kurumsal bayisi silindikten sonra kota sıfırlanır.

## <a name="delete-sandbox-indirect-reseller-through-api"></a>API aracılığıyla Korumalı Alan Dolaylı Kurumsal Bayisini silme

### <a name="rest-request"></a>REST isteği

#### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si                                                                             |
|------------|-------------------------------------------------------------------------------------|
| **Silmek** | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId} |

#### <a name="request-headers"></a>İstek üst bilgileri

- Bu API bir kez etkilidir (birden çok kez çağırsanız farklı bir sonuç ortayalanmaz)
- İstek kimliği ve bağıntı kimliği gereklidir
- Daha fazla bilgi için [bkz. İŞ ORTAĞı MERKEZI REST üst bilgileri](headers.md)

### <a name="request-example"></a>İstek Örneği

Silmek https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu ve diğer hata ayıklama bilgilerini gösteren bir HTTP durum koduyla birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

Bu yöntem aşağıdaki durum başarısını ve hata kodlarını döndürür:

| HTTP Durum Kodu                     | Hata kodu     | Description                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| 401                                  | 6002           | Yetkisiz belirteç veya İpucu Sağlayıcısı Hesabı Değil |
| 403                                  | 6003           | Korumalı Alanı Silme IR'ye izin verilmiyor                 |
| 403                                  | 6004           | Korumalı Alan IR oluşturma işlemi izin verilmiyor          |
| 409                                  | 1003           | Kiracı oluşturulurken çakışma                   |
