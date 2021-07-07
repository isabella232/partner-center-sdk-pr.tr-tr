---
title: Sandbox 'de dolaylı satıcı oluşturma
description: API 'Leri kullanarak uçtan uca teste olanak sağlayan korumalı alan dolaylı sağlayıcıları için bilgi sağlar.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973443"
---
# <a name="create-indirect-reseller-in-sandbox"></a>Sandbox 'de dolaylı satıcı oluşturma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi

Bu belgede, korumalı alan dolaylı sağlayıcılarının nasıl oluşturulacağı ve API 'Ler kullanılarak uçtan uca testlerin nasıl etkinleştirileceği gösterilmektedir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="csp-indirect-provider"></a>CSP Indirect Provider

| Üretim özellikleri             | Korumalı alan özellikleri                            |
|-------------------------------------|-------------------------------------------------|
| Son müşteriye dolaylı satıcı üzerinden satış yapın | Desteklenir |
| Tüm satış, faturalandırma, sağlama ve yönetim/destek sahibi | Desteklenir |
| Satıcılarla iş ortaklığı isteme | Desteklenir |
| Müşterileri satıcıya göre görüntüleme | Desteklenir |
| Satıcılara göre yeni müşteriler ekleyin | Desteklenir |
| Müşterileri davet et | Korumalı alanda müşteri ilişkisi isteği desteklenmiyor |
| Korumalı alan dolaylı sağlayıcısı, işlem sırasında g veya s olarak korumalı alan IR (MPN ID) seçebilir | Desteklenir |
| Üretimde desteklenmez | Korumalı alan dolaylı sağlayıcısı, korumalı alan dolaylı satıcısı oluşturabilir |
| Korumalı alan MPN KIMLIĞI girilmelidir, ürün MPN KIMLIĞI çalışmayacak | Üretimde desteklenmez |
| Üretimde desteklenmez | Korumalı alan dolaylı sağlayıcısı, korumalı alan dolaylı Bayi silebilir |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a>Korumalı alan dolaylı sağlayıcısı – korumalı alan dolaylı satıcısı oluşturma

Bu özellik yalnızca korumalı alanda kullanılabilir ve Sandbox dolaylı sağlayıcılarına korumalı alan dolaylı satıcıları oluşturma olanağı sağlar.

1. Sandbox dolaylı sağlayıcısı başına beş korumalı alan dolaylı satıcıların izin verdiği sınır
2. Korumalı alan dolaylı sağlayıcıları, `associatedPartnerId` korumalı alan dolaylı satıcısı olan müşteriler oluşturabilir
3. Korumalı alan dolaylı satıcısı oluştururken belirli bir bölgenin [MPN](/partner-center/mpn-create-a-partner-center-account) kimliğini girin. Aynı korumalı alan MPN KIMLIĞIYLE birden çok korumalı alan dolaylı satıcıları oluşturulabilir.
4. Sandbox dolaylı sağlayıcısı başına yalnızca 75 müşteriye izin verilir

## <a name="sandbox-indirect-resellers--view-customers"></a>Korumalı alan dolaylı satıcıları – müşterileri görüntüleyin

1. Korumalı alan dolaylı satıcıları, korumalı alan müşterilerinin listesini Sandbox dolaylı sağlayıcılarına göre görüntüleyebilir.
2. Korumalı alan dolaylı satıcıları, yönetici temsilcisi izinlerini kullanarak müşteri hesabını yönetebilir.

## <a name="create-sandbox-indirect-reseller-through-api"></a>API aracılığıyla korumalı alan dolaylı satıcısı oluşturma

### <a name="rest-request"></a>REST isteği

#### <a name="request-syntax"></a>İstek sözdizimi

| **Yöntem** | **İstek URI'si**                                                        |
|------------|------------------------------------------------------------------------|
| **Yayınla**   | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/sandboxındirectbayi |

#### <a name="request-headers"></a>İstek üst bilgileri

- Bu API, ıdempotent (birden çok kez çağırırsanız farklı bir sonuç vermez).
- İstek KIMLIĞI ve bağıntı KIMLIĞI gereklidir.
- Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

#### <a name="request-body"></a>İstek gövdesi

Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.

| Özellik             | Tür           | Açıklama                                      |
|----------------------|----------------|--------------------------------------------------|
| Mpnıd                | string         | Belirli bir bölgedeki IR için MPN KIMLIĞI         |
| Kiracı               | Sözlük &lt; dizesi, dize&gt; | Oluşturulacak bir hesabı tanımlayan temel bilgilerin toplanması |
| legalBusinessProfile | Sözlük &lt; dizesi, dize&gt; | Kişi, adres ve ad gibi yasal iş varlığını temsil eden bilgilerin toplanması |
| organizationProfileLanguage | Sözlük &lt; dizesi, dize&gt; | Kuruluş dil tanımlayıcısı |

Bu tabloda, **kiracı** özniteliğinde gereken özellikler açıklanmaktadır.

| Özellik           | Tür           | Açıklama                         |
|--------------------|----------------|-------------------------------------|
| domainPrefix       | Dizisinde eşi | Kiracı hesabı için etki alanı       |
| name               | string         | Kiracının kolay adı         |
| displayName        | string         | Hesabın görünen adı        |
| adminUserName      | string         | Oturum açma hesabının Kullanıcı adı |
| adminfirstname     | string         | Yönetici Kullanıcı adı       |
| adminlastname      | string         | Yönetici Kullanıcı için Soyadı        |
| adminAlernateEmail | string         | Yönetici Kullanıcı için e-posta            |
| ülke            | string         | Hesabın ülkesi              |
| kültür            | string         | Hesap için dil tercihi     |

Bu tabloda, **legalBusinessProfile** özniteliğinde gerekli özellikler açıklanmaktadır.

| Özellik       | Tür                             | Açıklama                          |
|----------------|----------------------------------|--------------------------------------|
| Tadı    | string                           | Yasal varlık için şirket adı        |
| adres        | Sözlük &lt; dizesi, dize&gt; | Yasal varlık konumunun adresi |
| primaryContact | Sözlük &lt; dizesi, dize&gt; | Şirketin iletişim ayrıntıları       |
| kültür        | string                           | Şirket tarafından tercih edilen dil    |

### <a name="request-example"></a>İstek örneği

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş korumalı alan IR kaynağını döndürür.

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
