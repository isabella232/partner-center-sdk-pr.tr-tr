---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünü onaylama
description: Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri Sözleşmesi 'nin müşteri kabulünü onaylama hakkında bilgi edinin.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974021"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Iş Ortağı Merkezi API 'Lerini kullanarak Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama

**Uygulama hedefi**: Iş Ortağı Merkezi

**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

İş ortağı merkezi şu anda Microsoft Müşteri sözleşmesinin yalnızca Microsoft genel bulutundaki müşteri kabulünün onayını desteklemektedir.

Bu makalede, Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylama veya yeniden onaylama işlemlerinin nasıl yapılacağı açıklanır.

## <a name="prerequisites"></a>Önkoşullar

- Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.

- [Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. *Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.*

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde Tarih (**kabul edildi**).

- Müşteri kuruluşundan, Microsoft Müşteri anlaşmasını kabul eden kullanıcı hakkında bilgiler. Şunları içerir:
  - Ad
  - Soyadı
  - E-posta adresi
  - Telefon numarası (isteğe bağlı)
- bir müşteri için aşağıdaki değerler değişiyorsa, iş ortağı merkezi bu müşteri için başka bir sözleşmenin oluşturulmasını sağlayacaktır: ad adı soyadı e-posta adresi Telefon numarası aksi takdirde iş ortakları, oluşturulan yinelenen bir müşteri nedeniyle aşağıdaki hata kodunu alır


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a>.NET

Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak veya yeniden doğrulamak için:

1. Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın. Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir. Daha fazla bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Onayın ayrıntılarını içeren yeni bir **anlaşma** nesnesi oluşturun.

3. **Iagreggatepartner. Customers** koleksiyonunu kullanın ve belirtilen **Müşteri Kiracı kimliği** ile **byıd** yöntemini çağırın.

4. , Ardından **Create** veya **createasync** çağrısı yaparak **anlaşmalar** özelliğini kullanın.

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [createcustomeragreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) sınıfında bir bütün örnek bulunabilir.

## <a name="rest-request"></a>REST isteği

Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak veya yeniden doğrulamak için:

1. Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın. Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir. Daha fazla bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).

2. Müşterinin Microsoft Müşteri anlaşmasını kabul ettiğini onaylamak için yeni bir [ **anlaşma** kaynağı](agreement-resources.md) oluşturun. Aşağıdaki [rest istek sözdizimini](#request-syntax)kullanın.

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Onayladığınız müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.

| Ad               | Tür | Gerekli | Açıklama                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| Müşteri-Kiracı kimliği | GUID | Yes | Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tabloda, REST istek gövdesinde gereken özellikler açıklanmaktadır.

| Ad      | Tür   | Açıklama                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Sözleşme | object | Microsoft Müşteri sözleşmesinin müşteri kabulünü onaylamak için iş ortağı tarafından sunulan ayrıntılar. |

#### <a name="agreement"></a>Sözleşme

Bu tablo, bir [ **anlaşma** kaynağı](agreement-resources.md)oluşturmak için gereken en düşük alanları açıklar.

| Özellik       | Tür   | Açıklama                              |
|----------------|--------|------------------------------------------|
| primaryContact | [İletişim](./utility-resources.md#contact) | Microsoft Müşteri sözleşmesini kabul eden müşteri kuruluşundan Kullanıcı hakkındaki bilgiler:  **FirstName**, **LastName**, **email** ve **PhoneNumber** (isteğe bağlı) |
| Kabul edilen tarih     | UTC Tarih saat biçiminde dize |Müşterinin sözleşmeyi kabul ettiği tarih. |
| TemplateId     | string | Müşteri tarafından kabul edilen sözleşme türünün benzersiz tanımlayıcısı. Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alarak Microsoft Müşteri Sözleşmesi için **TemplateId** 'yi edinebilirsiniz. Ayrıntılar için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](./get-customer-agreement-metadata.md) . |
| tür           | string | Müşteri tarafından kabul edilen anlaşma türü. Müşteri Microsoft Müşteri anlaşmasını kabul ettiğinde "MicrosoftCustomerAgreement" kullanın. |

#### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem bir [ **anlaşma** kaynağı](./agreement-resources.md)döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

#### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
