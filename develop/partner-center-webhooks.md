---
title: İş Ortağı Merkezi web kancaları
description: Web kancaları, iş ortaklarının kaynak değişiklik olayları kaydetmesine izin verir.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8225623ade7e922ac23ebf0ed9215686b0601244
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769226"
---
# <a name="partner-center-webhooks"></a>İş Ortağı Merkezi web kancaları

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Iş Ortağı Merkezi Web kancası API 'Leri, iş ortaklarının kaynak değişiklik olayları kaydetmesine izin verir. Bu olaylar, ortağın kayıtlı URL 'sine HTTP yayınları biçiminde dağıtılır. İş Ortağı Merkezi 'nden bir olay almak için iş ortakları, Iş Ortağı Merkezi 'nin kaynak değişiklik olayını nakledebileceği bir geri çağırma işlemini barındıracaktır. Bu olay, iş ortağının Iş Ortağı Merkezi 'nden gönderildiğini doğrulayabilmesi için dijital olarak imzalanacaktır.

İş ortakları, Iş Ortağı Merkezi tarafından desteklenen aşağıdaki örneklerde olduğu gibi Web kancası olayları arasından seçim yapabilir.

- **Test olayı ("test-Created")**

    Bu olay, bir test olayı isteyerek ve sonra ilerleme durumunu izleyerek kaydınızı kendi kendinize ekleme ve test etmenize olanak tanır. Olayı sunmaya çalışırken Microsoft 'tan alınmakta olan hata iletilerini görebilirsiniz. Bu kısıtlama yalnızca "test tarafından oluşturulan" olaylar için geçerlidir. Yedi günden daha eski veriler temizlenir.

- **Abonelik güncelleştirildi olayı ("abonelik-güncelleştirildi")**

    Bu olay, abonelik değiştiğinde tetiklenir. Bu olaylar, Iş Ortağı Merkezi API 'SI aracılığıyla değişikliklerin yapılmesinin yanı sıra bir iç değişiklik yapıldığında oluşturulacaktır.

    >[!NOTE]
    >Abonelik değişikliği sırasında ve aboneliğin güncelleştirildiği olay tetiklendiğinde 48 saate kadar bir gecikme vardır.

- **Eşik aşıldı olayı ("usagerecords-Thresholdexcembaşında")**

    Bu olay, herhangi bir müşterinin Microsoft Azure kullanım miktarı kullanım harcama bütçesini (bunların eşiğini) aştığında tetiklenir. Daha fazla bilgi için bkz. [müşterileriniz için Azure harcama bütçesi ayarlama/iş ortağı-merkezi/set-a-Azure-harcama-bütçe-for-Customers).

- **Başvuru oluşturulan olay ("başvuru-oluşturuldu")**

    Bu olay, başvuru oluşturulduğunda tetiklenir.

- **Başvuru güncelleştirildi olayı ("başvuru-güncelleştirildi")**

    Bu olay, başvuru güncelleştirilirken tetiklenir.

- **Faturaya ready olayı ("Invoice-Ready")**

    Bu olay, yeni fatura hazırlandığınızda tetiklenir.

Gelecekteki Web kancası olayları, iş ortağının denetiminde olmadığı sistemde değişen kaynaklar için eklenir ve bu olayları mümkün olduğunca "gerçek zamanlı" olarak almak için daha fazla güncelleştirme yapılır. Olaylara değer ekleyen olayların iş ortaklarının geri bildirimi, hangi yeni olayların ekleneceğini belirlemede yararlı olacaktır.

Iş Ortağı Merkezi tarafından desteklenen Web kancası olaylarının tüm listesi için bkz. [Partner Center Web kancası olayları](partner-center-webhook-events.md).

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="receiving-events-from-partner-center"></a>Iş Ortağı Merkezi 'nden olay alma

Iş Ortağı Merkezi 'nden olay almak için, herkese açık bir uç nokta kullanıma sunmanız gerekir. Bu uç nokta sunulduğundan, iletişimin Iş Ortağı Merkezi 'nden olduğunu doğrulamanız gerekir. Aldığınız tüm Web kancası olayları Microsoft köküne zincirsiz bir sertifikayla dijital olarak imzalanır. Olayı imzalamak için kullanılan sertifikaya bir bağlantı da sunulacaktır. Bu, hizmetinizi yeniden dağıtmak veya yeniden yapılandırmak zorunda kalmadan sertifikanın yenilenmesini sağlar. İş Ortağı Merkezi, olayı teslim etmek için 10 deneme yapar. Etkinlik yine 10 denemeden sonra teslim edilmezse, bu, çevrimdışı bir kuyruğa taşınır ve teslim sırasında başka bir girişim yapılmayacaktır.

Aşağıdaki örnekte, Iş ortağı merkezinden gönderilen bir olay gösterilmektedir.

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

>[!NOTE]
>Yetkilendirme üst bilgisinde bir "Signature" düzeni vardır. Bu, içeriğin Base64 olarak kodlanmış bir imzasına sahiptir.

## <a name="how-to-authenticate-the-callback"></a>Geri aramanın kimliğini doğrulama

Iş Ortağı Merkezi 'nden alınan geri çağırma olayının kimliğini doğrulamak için şu adımları izleyin:

1. Gerekli üstbilgilerin mevcut olduğunu doğrulayın (yetkilendirme, x-MS-Certificate-URL, x-MS-Signature-algoritma).

2. İçeriği imzalamak için kullanılan sertifikayı indirin (x-MS-Certificate-URL).

3. Sertifika zincirini doğrulayın.

4. Sertifikanın "organizasyonunu" doğrulayın.

5. UTF8 kodlamalı içeriği bir arabelleğe okur.

6. Bir RSA şifreleme sağlayıcısı oluşturun.

7. Verilerin belirtilen karma algoritmayla imzalandıklarla eşleştiğini doğrulayın (örneğin, SHA256).

8. Doğrulama başarılı olursa, iletiyi işleyin.

> [!NOTE]
> Varsayılan olarak, imza belirteci bir yetkilendirme üst bilgisinde gönderilir. Kaydınızın **Signaturetokentomssignatureheader** değerini true olarak ayarlarsanız, imza belirteci x-MS-Signature üst bilgisine gönderilir.

## <a name="event-model"></a>Olay modeli

Aşağıdaki tabloda bir Iş Ortağı Merkezi olayının özellikleri açıklanmaktadır.

### <a name="properties"></a>Özellikler

| Ad                      | Açıklama                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | Olayın adı. {Resource}-{Action} biçiminde. Örneğin, "test oluşturma".  |
| **ResourceUri**           | Değiştirilen kaynağın URI 'SI.                                                 |
| **Kaynak**          | Değiştirilen kaynağın adı.                                                |
| **AuditUrl**              | İsteğe bağlı. Denetim kaydının URI 'SI.                                                |
| **ResourceChangeUtcDate** | Kaynak değişikliği oluştuğunda UTC biçimindeki tarih ve saat.                  |

### <a name="sample"></a>Örnek

Aşağıdaki örnek, bir Iş Ortağı Merkezi olayının yapısını gösterir.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a>Web kancası API 'Leri

### <a name="authentication"></a>Kimlik Doğrulaması

Web kancası API 'Lerine yapılan tüm çağrılar, yetkilendirme üstbilgisindeki taşıyıcı belirteci kullanılarak doğrulanır. Erişim için bir erişim belirteci alın `https://api.partnercenter.microsoft.com` . Bu belirteç, Iş Ortağı Merkezi API 'lerinin geri kalanına erişmek için kullanılan belirteçtir.

### <a name="get-a-list-of-events"></a>Olayların bir listesini alın

Web kancası API 'Leri tarafından şu anda desteklenen olayların bir listesini döndürür.

### <a name="resource-url"></a>Kaynak URL'si

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a>İstek örneği

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US

[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```

### <a name="register-to-receive-events"></a>Olayları almak için kaydolun

Belirtilen olayları almak için bir kiracı kaydeder.

#### <a name="resource-url"></a>Kaynak URL'si

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>İstek örneği

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="view-a-registration"></a>Kayıt görüntüleme

Bir kiracının Web kancaları olay kaydını döndürür.

#### <a name="resource-url"></a>Kaynak URL'si

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>İstek örneği

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="update-an-event-registration"></a>Olay kaydını güncelleştirme

Var olan bir olay kaydını güncelleştirir.

#### <a name="resource-url"></a>Kaynak URL'si

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>İstek örneği

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="send-a-test-event-to-validate-your-registration"></a>Kaydınızı doğrulamak için bir test olayı gönderin

Web kancaları kaydını doğrulamak için bir test olayı oluşturur. Bu test, Iş Ortağı Merkezi 'nden olay alacağınızı doğrulamaya yöneliktir. Bu olayların verileri, ilk olay oluşturulduktan sonra yedi gün sonra silinecektir. Doğrulama olayını göndermeden önce, kayıt API 'sini kullanarak "test tarafından oluşturulan" olay için kaydolmalısınız.

>[!NOTE]
>Bir doğrulama olayı naklederken dakikada 2 istekten oluşan bir kısıtlama sınırı vardır.

#### <a name="resource-url"></a>Kaynak URL'si

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a>İstek örneği

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```

### <a name="verify-that-the-event-was-delivered"></a>Olayın teslim edildiğini doğrulama

Doğrulama olayının geçerli durumunu döndürür. Bu doğrulama, olay teslimi sorunlarını gidermek için yararlı olabilir. Yanıt, olayı teslim etmek için yapılan her girişimde bir sonuç içerir.

#### <a name="resource-url"></a>Kaynak URL'si

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a>İstek örneği

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```

## <a name="example-for-signature-validation"></a>Imza doğrulama örneği

### <a name="sample-callback-controller-signature-aspnet"></a>Örnek geri çağırma denetleyicisi imzası (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>İmza doğrulama

Aşağıdaki örnek, Web kancası olaylarından geri çağırmaları alan denetleyiciye bir yetkilendirme özniteliğinin nasıl ekleneceğini gösterir.

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // for example RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
