---
title: Korumalı Alanda Dolaylı Kurumsal Bayi oluşturma
description: KORUMALı Alan Dolaylı Sağlayıcıları için API'leri kullanarak 1.5 00.000 testi etkinleştirme hakkında bilgi sağlar.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 970b7ba49f6bb4b842f0f7d96e689856b0362c03949e14c9cf5a0e205573277b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991455"
---
# <a name="create-indirect-reseller-in-sandbox"></a>Korumalı Alanda Dolaylı Kurumsal Bayi oluşturma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Bu belgede, Korumalı Alan Dolaylı Sağlayıcılarının nasıl oluşturularak API'ler kullanılarak uzlamlı testlerin nasıl etkinleştirildikleri anlatılıyor.

## <a name="prerequisites"></a>Önkoşullar

- Kimlik Doğrulaması altında açıklandığı [gibi İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="csp-indirect-provider"></a>CSP Indirect Provider

| Üretim özellikleri             | Korumalı alan özellikleri                            |
|-------------------------------------|-------------------------------------------------|
| Dolaylı kurumsal bayi aracılığıyla son müşteriye satış | Desteklenir |
| Tüm satış, faturalama, sağlama ve yönetim/destek sahip olur | Desteklenir |
| Kurumsal bayilerle iş ortaklığı isteği | Desteklenir |
| Kurumsal Bayiye göre müşterileri görüntüleme | Desteklenir |
| Kurumsal bayilere göre yeni müşteriler ekleme | Desteklenir |
| Müşterileri davet etme | Korumalı Alanda müşteri ilişkisi isteği desteklenmiyor |
| Korumalı Alan Dolaylı Sağlayıcısı, işlemi yaparken SANDBOX IR (MPN ID) öğesini (SANDBOX IR) (MPN ID) olarak seçerek IŞLEMI tamamlar | Desteklenir |
| Üretimde desteklenmiyor | Korumalı Alan Dolaylı Sağlayıcısı Korumalı Alan Dolaylı Kurumsal Bayi oluşturabilir |
| Korumalı Alan MPN Kimliği girilir, ürün MPN kimliği çalışmaz | Üretimde desteklenmiyor |
| Üretimde desteklenmiyor | Korumalı Alan Dolaylı Sağlayıcısı, Korumalı Alan Dolaylı Kurumsal Bayi'lerini silebilir |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a>Korumalı Alan Dolaylı Sağlayıcısı – Korumalı Alan Dolaylı Kurumsal Bayi oluşturma

Bu özellik yalnızca Korumalı Alanda kullanılabilir ve Korumalı Alan Dolaylı Sağlayıcılarına Korumalı Alan Dolaylı Kurumsal Bayileri oluşturma olanağı sağlar.

1. Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen beş Korumalı Alan Dolaylı Kurumsal Bayi sınırı
2. Korumalı Alan Dolaylı Sağlayıcıları, Korumalı Alan Dolaylı `associatedPartnerId` Kurumsal Bayi ile müşteri oluşturabilir
3. Korumalı Alan Dolaylı Kurumsal Bayi oluştururken belirli bir bölgenin [MPN](/partner-center/mpn-create-a-partner-center-account) kimliğini girin. Aynı Korumalı Alan MPN Kimliği ile birden çok Korumalı Alan Dolaylı Kurumsal Bayisi oluşturulabilir.
4. Korumalı Alan Dolaylı Sağlayıcısı başına yalnızca 75 müşteriye izin verilir

## <a name="sandbox-indirect-resellers--view-customers"></a>Korumalı Alan Dolaylı Kurumsal Bayileri – Müşterileri görüntüleme

1. Korumalı Alan Dolaylı Kurumsal Bayileri, Korumalı Alan Dolaylı sağlayıcılarına göre korumalı alan müşterilerinin listesini ekleyebilirsiniz.
2. Korumalı Alan Dolaylı Kurumsal Bayileri, yönetici temsilcisi izinlerini kullanarak müşteri hesabını yönetebilir.

## <a name="create-sandbox-indirect-reseller-through-api"></a>API aracılığıyla Korumalı Alan Dolaylı Kurumsal Bayi oluşturma

### <a name="rest-request"></a>REST isteği

#### <a name="request-syntax"></a>İstek söz dizimi

| **Yöntem** | **İstek URI'si**                                                        |
|------------|------------------------------------------------------------------------|
| **Yayınla**   | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller |

#### <a name="request-headers"></a>İstek üst bilgileri

- Bu API bir kez etkilidir (birden çok kez çağırsanız farklı bir sonuç ortayalanmaz).
- İstek kimliği ve bağıntı kimliği gereklidir.
- Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

#### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde gerekli özellikleri açıklar.

| Özellik             | Tür           | Description                                      |
|----------------------|----------------|--------------------------------------------------|
| mpnId                | string         | Belirli bir bölgedeki IR için MPN Kimliği         |
| Kiracı               | Sözlük &lt; dizesi, dize&gt; | Oluşturulacak hesabı tanımlayan temel bilgi koleksiyonu |
| legalBusinessProfile | Sözlük &lt; dizesi, dize&gt; | İletişim, adres ve ad gibi yasal iş varlığını temsil eden bilgilerin toplanması |
| organizationProfileLanguage | Sözlük &lt; dizesi, dize&gt; | Kuruluş dili tanımlayıcısı |

Bu tablo, kiracı özniteliğinde gerekli **özellikleri** açıklar.

| Özellik           | Tür           | Description                         |
|--------------------|----------------|-------------------------------------|
| domainPrefix       | Dize; Benzer -siz | Kiracı hesabı için etki alanı       |
| name               | string         | Kiracının kolay adı         |
| displayName        | string         | Hesabın görünen adı        |
| adminUserName      | string         | Oturum açma hesabı için kullanıcı adı |
| adminfirstname     | string         | Yönetici kullanıcı için Ad       |
| adminlastname      | string         | Yönetici kullanıcının soyadı        |
| adminAlernateEmail | string         | yönetici kullanıcı için e-posta            |
| ülke            | string         | Hesabın ülkesi              |
| kültür            | string         | Hesap için dil tercihi     |

Bu tabloda **legalBusinessProfile özniteliğinde gerekli özellikler açıklanır.**

| Özellik       | Tür                             | Description                          |
|----------------|----------------------------------|--------------------------------------|
| Şirketadı    | string                           | Yasal varlık için şirket adı        |
| adres        | Sözlük &lt; dizesi, dize&gt; | Yasal varlık konumunun adresi |
| primaryContact | Sözlük &lt; dizesi, dize&gt; | Şirketin iletişim ayrıntıları       |
| kültür        | string                           | Şirket tarafından tercih edilen dil    |

### <a name="request-example"></a>İstek Örneği

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

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş Korumalı Alan IR kaynağını döndürür.

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
