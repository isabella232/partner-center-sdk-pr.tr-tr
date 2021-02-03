---
title: İş Ortağı Merkezi Web kancası olayları
description: Iş Ortağı Merkezi tarafından desteklenen tüm Web kancası olayları için belgeler.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 5358aab8efdd68ad52c583936304f99ffae12708
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769250"
---
# <a name="partner-center-webhook-events"></a>İş Ortağı Merkezi Web kancası olayları

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

İş Ortağı Merkezi Web kancası olayları, kayıtlı bir URL 'ye HTTP gönderimleri biçiminde teslim edilen kaynak değişiklik olaylardır. Iş Ortağı Merkezi 'nden bir olay almak için, Iş Ortağı Merkezi 'nin olayı NAKLEDEBILECEĞI bir geri çağırma barındırmanız gerekir. Etkinlik, Iş Ortağı Merkezi 'nden gönderildiğini doğrulayabilmeniz için dijital olarak imzalanır.

Olayları alma, geri çağırma kimlik doğrulaması ve bir olay kaydı oluşturmak, görüntülemek ve güncelleştirmek için Iş Ortağı Merkezi Web kancası API 'Lerini kullanma hakkında bilgi için bkz. [Partner Center Web kancaları](partner-center-webhooks.md).

## <a name="supported-events"></a>Desteklenen olaylar

Aşağıdaki Web kancası olayları Iş Ortağı Merkezi tarafından desteklenir.

### <a name="test-event"></a>Test olayı

Bu olay, bir test olayı isteyerek ve sonra ilerleme durumunu izleyerek kaydınızı kendi kendinize ekleme ve test etmenize olanak tanır. Olayı sunmaya çalışırken Microsoft 'tan alınmakta olan hata iletilerini görebileceksiniz. Bu, yalnızca "test tarafından oluşturulan" olaylar ve 7 günden eski olan veriler temizlenir.

>[!NOTE]
>Test tarafından oluşturulan bir olay nakledilirken dakikada 2 istekten oluşan bir kısıtlama sınırı vardır.

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {Resource}-{Action} biçiminde. Bu olay için, değer "test tarafından oluşturuldu" olarak ayarlanır.                                          |
| ResourceUri               | URI                                | Kaynağı almak için URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Webkancas/v1/Registration/validationevents/{{CorrelationId}}" |
| ResourceName              | string                             | Olayı tetikleyecek kaynağın adı. Bu olay için değer "test" dir.                                  |
| Sesturi                  | URI                                | Seçim Varsa, denetim kaydının alınacağı URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Auditactivity/v1/auditrecords/{{auditıd}}" |
| ResourceChangeUtcDate     | UTC Tarih-saat biçiminde dize | Kaynak değişikliğinin gerçekleştiği tarih ve saat.                                                         |

#### <a name="example"></a>Örnek

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>Abonelik güncelleştirildi olayı

Bu olay, belirtilen abonelik değiştiğinde tetiklenir. Iş Ortağı Merkezi API 'SI aracılığıyla değişiklik yapıldığında bir iç değişiklik olduğunda, abonelik güncelleştirilmiş bir olay oluşturulur.  Bu olay yalnızca, ticaret düzeyi değişiklikler olduğunda (örneğin, lisansların sayısı değiştirildiğinde ve aboneliğin durumu değiştiğinde) oluşturulacaktır. Bu işlem, abonelik içinde kaynaklar oluşturulduğunda oluşturulmaz.

>[!NOTE]
>Abonelik değişikliği sırasında ve aboneliğin güncelleştirildiği olay tetiklendiğinde 48 saate kadar bir gecikme vardır.

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {Resource}-{Action} biçiminde. Bu olay için, değer "abonelik-güncelleştirildi" dır.                                  |
| ResourceUri               | URI                                | Kaynağı almak için URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Webkancas/v1/Customers/{{CustomerID}}/Subscriptions/{{SubscriptionID}}" |
| ResourceName              | string                             | Olayı tetikleyecek kaynağın adı. Bu olay için değer "Subscription" dır.                          |
| Sesturi                  | URI                                | Seçim Varsa, denetim kaydının alınacağı URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Auditactivity/v1/auditrecords/{{auditıd}}" |
| ResourceChangeUtcDate     | UTC Tarih-saat biçiminde dize | Kaynak değişikliğinin gerçekleştiği tarih ve saat.                                                         |

#### <a name="example"></a>Örnek

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>Eşik aşıldı olayı

Bu olay, herhangi bir müşterinin Microsoft Azure kullanım miktarı kullanım harcama bütçesini (bunların eşiğini) aştığında tetiklenir. Daha fazla bilgi için bkz. [müşterileriniz için Azure harcama bütçesi ayarlama/iş ortağı-merkezi/set-a-Azure-harcama-bütçe-for-Customers).

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {Resource}-{Action} biçiminde. Bu olay için, değer "usagerecords-Thresholdexcebaşında" olur.                                  |
| ResourceUri               | URI                                | Kaynağı almak için URI. "[*{BaseUrl}*](partner-center-rest-urls.md)/webhooks/v1/Customers/usagerecords" sözdizimini kullanır. |
| ResourceName              | string                             | Olayı tetikleyecek kaynağın adı. Bu olay için, değer "usagerecords" olur.                          |
| Sesturi                  | URI                                | Seçim Varsa, denetim kaydının alınacağı URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Auditactivity/v1/auditrecords/{{auditıd}}" |
| ResourceChangeUtcDate     | UTC Tarih-saat biçiminde dize | Kaynak değişikliğinin gerçekleştiği tarih ve saat.                                                         |

#### <a name="example"></a>Örnek

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>Başvuru oluşturulan olay

Bu olay, başvuru oluşturulduğunda tetiklenir.

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {Resource}-{Action} biçiminde. Bu olay için, değer "başvuru oluşturuldu" değeridir.                                  |
| ResourceUri               | URI                                | Kaynağı almak için URI. "[*{BaseUrl}*](partner-center-rest-urls.md)/Engagements/v1/referrals/{{ReferralID}}" sözdizimini kullanır. |
| ResourceName              | string                             | Olayı tetikleyecek kaynağın adı. Bu olay için, değer "başvuru" olur.                          |
| Sesturi                  | URI                                | Seçim Varsa, denetim kaydının alınacağı URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Auditactivity/v1/auditrecords/{{auditıd}}" |
| ResourceChangeUtcDate     | UTC Tarih-saat biçiminde dize | Kaynak değişikliğinin gerçekleştiği tarih ve saat.                                                         |

#### <a name="example"></a>Örnek

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>Başvuru güncelleştirildi olayı

Bu olay, başvuru güncelleştirilirken tetiklenir.

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {Resource}-{Action} biçiminde. Bu olay için, değer "başvuru-güncelleştirildi" olur.                                  |
| ResourceUri               | URI                                | Kaynağı almak için URI. "[*{BaseUrl}*](partner-center-rest-urls.md)/Engagements/v1/referrals/{{ReferralID}}" sözdizimini kullanır. |
| ResourceName              | string                             | Olayı tetikleyecek kaynağın adı. Bu olay için, değer "başvuru" olur.                          |
| Sesturi                  | URI                                | Seçim Varsa, denetim kaydının alınacağı URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Auditactivity/v1/auditrecords/{{auditıd}}" |
| ResourceChangeUtcDate     | UTC Tarih-saat biçiminde dize | Kaynak değişikliğinin gerçekleştiği tarih ve saat.                                                         |

#### <a name="example"></a>Örnek

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>Faturaya ready olayı

Bu olay, yeni fatura hazırlandığınızda tetiklenir.

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | string | Olayın adı. {Resource}-{Action} biçiminde. Bu olay için, değer "Invoice-Ready" olur. |
| ResourceUri | URI | Kaynağı almak için URI. Şu sözdizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{{ınvoed}}" |
| ResourceName | string | Olayı tetikleyecek kaynağın adı. Bu olay için değer "Invoice" dır. |
| Sesturi |  URI | Seçim Varsa, denetim kaydının alınacağı URI. Söz dizimini kullanır: "[*{BaseUrl}*](partner-center-rest-urls.md)/Auditactivity/v1/auditrecords/{{sestid}}") |
| ResourceChangeUtcDate | UTC Tarih-saat biçiminde dize | Kaynak değişikliğinin gerçekleştiği tarih ve saat. |

#### <a name="example"></a>Örnek

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
