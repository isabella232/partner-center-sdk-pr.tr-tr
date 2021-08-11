---
title: İş Ortağı Merkezi kancası olaylarını
description: Web kancası olaylarını test etmeyi ve kullanarak aboneliklerde ve diğer olaylarda ne zaman değişiklik olduğunu İş Ortağı Merkezi.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: f329f7aa59ee5127c8275c7c9d8c59e5ea2cf12e9c888419f1ce35e2db3604d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997575"
---
# <a name="partner-center-webhook-events"></a>İş Ortağı Merkezi kancası olaylarını

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

İş Ortağı Merkezi kancası olayları, HTTP POST'leri şeklinde kayıtlı bir URL'ye teslim edilen kaynak değişikliği olaylarıdır. Bir olay İş Ortağı Merkezi almak için, olay gönderenin İş Ortağı Merkezi bir geri çağırma barındırsınız. Olay dijital olarak imzalanır ve bu nedenle bu etkinliğin İş Ortağı Merkezi.

Olayları alma, geri çağırma kimliğini doğrulama ve olay kaydını oluşturmak, görüntülemek ve güncelleştirmek için İş Ortağı Merkezi web kancası API'lerini kullanma hakkında bilgi için [bkz. İş Ortağı Merkezi Web Kancaları.](partner-center-webhooks.md)

## <a name="supported-events"></a>Desteklenen Olaylar

Aşağıdaki web kancası olayları, aşağıdaki web kancası İş Ortağı Merkezi.

### <a name="test-event"></a>Test Olayı

Bu olay, bir test olayı isteğinde bulundurarak ve ardından ilerlemesini takip etmek için kaydınızı kendi kendine eklemenizi ve test etmenizi sağlar. Olayı teslim etmeye çalışırken Microsoft'tan alınan hata iletilerini görebilirsiniz. Bu yalnızca "test tarafından oluşturulan" olaylar için geçerli olur ve yedi günlükten eski veriler temizilir.

>[!NOTE]
>Test tarafından oluşturulan bir olayı gönderdiğinizde dakikada 2 istek kısıtlama sınırı vardır.

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {resource}-{action} formunda. Bu olay için değer "test-created" şeklindedir.                                          |
| ResourceUri               | URI                                | Kaynağı almak için URI. Şu söz dizimlerini kullanır: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | string                             | Olayı tetikleyen kaynağın adı. Bu olay için değer "test" olur.                                  |
| AuditUri                  | URI                                | (İsteğe bağlı) Denetim kaydının (varsa) elde URI'si. Şu söz dizimlerini kullanır: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC tarih-saat biçimindeki dize | Kaynak değişikliğinin meydana geldiği tarih ve saat.                                                         |

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

### <a name="subscription-updated-event"></a>Abonelik Güncelleştirilmiş Olayı

Belirtilen abonelik değişirken bu olay ortaya çıkar. Abonelik Güncelleştirildi olayı, api'sinde değişiklik yapılana ek olarak bir iç değişiklik olduğunda İş Ortağı Merkezi oluşturulur.  Bu olay yalnızca ticari düzeyde değişiklikler olduğunda (örneğin, lisans sayısı değiştirildiğinde ve aboneliğin durumu değiştirildiğinde) oluşturulur. Abonelik içinde kaynaklar oluşturulduğunda oluşturulmaz.

>[!NOTE]
>Bir aboneliğin değişiklik zamanı ile Abonelik Güncelleştirildi olayı tetiklenmesi arasında 48 saate kadar bir gecikme olur.

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {resource}-{action} formunda. Bu olay için değer "subscription-updated" şeklindedir.                                  |
| ResourceUri               | URI                                | Kaynağı almak için URI. Şu söz dizimlerini kullanır: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | string                             | Olayı tetikleyen kaynağın adı. Bu olay için değer "abonelik" olur.                          |
| AuditUri                  | URI                                | (İsteğe bağlı) Denetim kaydının (varsa) elde URI'si. Şu söz dizimlerini kullanır: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC tarih-saat biçimindeki dize | Kaynak değişikliğinin meydana geldiği tarih ve saat.                                                         |

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

### <a name="threshold-exceeded-event"></a>Eşik Aşıldı Olayı

Bu olay, herhangi bir müşterinin Microsoft Azure harcama bütçesini (eşik) aştıklarında ortaya çıkar. Daha fazla bilgi için bkz. [Müşterileriniz için Azure harcama bütçesi ayarlama/iş ortağı-merkezi/set-an-azure-spending-budget-for-your-customers).

#### <a name="properties"></a>Özellikler

| Özellik                  | Tür                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Olayın adı. {resource}-{action} formunda. Bu olay için değer "usagerecords-thresholdExceeded" şeklindedir.                                  |
| ResourceUri               | URI                                | Kaynağı almak için URI. Şu söz dizimlerini kullanır: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | string                             | Olayı tetikleyen kaynağın adı. Bu olay için değer "usagerecords" olur.                          |
| AuditUri                  | URI                                | (İsteğe bağlı) Denetim kaydının (varsa) elde URI'si. Şu söz dizimlerini kullanır: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC tarih-saat biçimindeki dize | Kaynak değişikliğinin meydana geldiği tarih ve saat.                                                         |

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

### <a name="referral-created-event"></a>Referans Oluşturma Olayı

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
