---
title: İş Ortağı Merkezi web kancaları
description: Web kancaları, iş ortaklarının kaynak değişiklik olayları kaydetmesine izin verir.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 74d5981436ba29ea4f6f93a5693ec6da82777eb4
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547759"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="3cbe6-103">İş Ortağı Merkezi web kancaları</span><span class="sxs-lookup"><span data-stu-id="3cbe6-103">Partner Center webhooks</span></span>

<span data-ttu-id="3cbe6-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3cbe6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3cbe6-105">Iş Ortağı Merkezi Web kancası API 'Leri, iş ortaklarının kaynak değişiklik olayları kaydetmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-105">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="3cbe6-106">Bu olaylar, ortağın kayıtlı URL 'sine HTTP yayınları biçiminde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-106">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="3cbe6-107">İş Ortağı Merkezi 'nden bir olay almak için iş ortakları, Iş Ortağı Merkezi 'nin kaynak değişiklik olayını nakledebileceği bir geri çağırma işlemini barındıracaktır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-107">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="3cbe6-108">Bu olay, iş ortağının Iş Ortağı Merkezi 'nden gönderildiğini doğrulayabilmesi için dijital olarak imzalanacaktır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-108">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="3cbe6-109">İş ortakları, Iş Ortağı Merkezi tarafından desteklenen aşağıdaki örneklerde olduğu gibi Web kancası olayları arasından seçim yapabilir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-109">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="3cbe6-110">**Test olayı ("test-Created")**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-110">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="3cbe6-111">Bu olay, bir test olayı isteyerek ve sonra ilerleme durumunu izleyerek kaydınızı kendi kendinize ekleme ve test etmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-111">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="3cbe6-112">Olayı sunmaya çalışırken Microsoft 'tan alınmakta olan hata iletilerini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-112">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="3cbe6-113">Bu kısıtlama yalnızca "test tarafından oluşturulan" olaylar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-113">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="3cbe6-114">Yedi günden daha eski veriler temizlenir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-114">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="3cbe6-115">**Abonelik güncelleştirildi olayı ("abonelik-güncelleştirildi")**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-115">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="3cbe6-116">Bu olay, abonelik değiştiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-116">This event is raised when the subscription changes.</span></span> <span data-ttu-id="3cbe6-117">Bu olaylar, Iş Ortağı Merkezi API 'SI aracılığıyla değişikliklerin yapılmesinin yanı sıra bir iç değişiklik yapıldığında oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-117">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3cbe6-118">Abonelik değişikliği sırasında ve aboneliğin güncelleştirildiği olay tetiklendiğinde 48 saate kadar bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-118">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="3cbe6-119">**Eşik aşıldı olayı ("usagerecords-Thresholdexcembaşında")**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-119">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="3cbe6-120">bu olay, herhangi bir müşterinin Microsoft Azure kullanım miktarı kullanım harcama bütçesini (bunların eşiğini) aştığında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-120">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="3cbe6-121">Daha fazla bilgi için bkz. [müşterileriniz için Azure harcama bütçesi ayarlama/iş ortağı-merkezi/set-a-Azure-harcama-bütçe-for-Customers).</span><span class="sxs-lookup"><span data-stu-id="3cbe6-121">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="3cbe6-122">**Başvuru oluşturulan olay ("başvuru-oluşturuldu")**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-122">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="3cbe6-123">Bu olay, başvuru oluşturulduğunda tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-123">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="3cbe6-124">**Başvuru güncelleştirildi olayı ("başvuru-güncelleştirildi")**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-124">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="3cbe6-125">Bu olay, başvuru güncelleştirilirken tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-125">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="3cbe6-126">**Faturaya ready olayı ("Invoice-Ready")**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-126">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="3cbe6-127">Bu olay, yeni fatura hazırlandığınızda tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-127">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="3cbe6-128">Gelecekteki Web kancası olayları, iş ortağının denetiminde olmadığı sistemde değişen kaynaklar için eklenir ve bu olayları mümkün olduğunca "gerçek zamanlı" olarak almak için daha fazla güncelleştirme yapılır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-128">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="3cbe6-129">Olaylara değer ekleyen olayların iş ortaklarının geri bildirimi, hangi yeni olayların ekleneceğini belirlemede yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-129">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="3cbe6-130">Iş Ortağı Merkezi tarafından desteklenen Web kancası olaylarının tüm listesi için bkz. [Partner Center Web kancası olayları](partner-center-webhook-events.md).</span><span class="sxs-lookup"><span data-stu-id="3cbe6-130">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cbe6-131">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3cbe6-131">Prerequisites</span></span>

- <span data-ttu-id="3cbe6-132">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-132">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3cbe6-133">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-133">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="3cbe6-134">Iş Ortağı Merkezi 'nden olay alma</span><span class="sxs-lookup"><span data-stu-id="3cbe6-134">Receiving events from Partner Center</span></span>

<span data-ttu-id="3cbe6-135">Iş Ortağı Merkezi 'nden olay almak için, herkese açık bir uç nokta kullanıma sunmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-135">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="3cbe6-136">Bu uç nokta sunulduğundan, iletişimin Iş Ortağı Merkezi 'nden olduğunu doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-136">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="3cbe6-137">Aldığınız tüm Web kancası olayları Microsoft köküne zincirsiz bir sertifikayla dijital olarak imzalanır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-137">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="3cbe6-138">Olayı imzalamak için kullanılan sertifikaya bir bağlantı da sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-138">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="3cbe6-139">Bu, hizmetinizi yeniden dağıtmak veya yeniden yapılandırmak zorunda kalmadan sertifikanın yenilenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-139">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="3cbe6-140">İş Ortağı Merkezi, olayı teslim etmek için 10 deneme yapar.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-140">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="3cbe6-141">Etkinlik yine 10 denemeden sonra teslim edilmezse, bu, çevrimdışı bir kuyruğa taşınır ve teslim sırasında başka bir girişim yapılmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-141">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="3cbe6-142">Aşağıdaki örnekte, Iş ortağı merkezinden gönderilen bir olay gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-142">The following sample shows an event posted from Partner Center.</span></span>

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
><span data-ttu-id="3cbe6-143">Yetkilendirme üst bilgisinde bir "Signature" düzeni vardır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-143">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="3cbe6-144">Bu, içeriğin Base64 olarak kodlanmış bir imzasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-144">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="3cbe6-145">Geri aramanın kimliğini doğrulama</span><span class="sxs-lookup"><span data-stu-id="3cbe6-145">How to authenticate the callback</span></span>

<span data-ttu-id="3cbe6-146">Iş Ortağı Merkezi 'nden alınan geri çağırma olayının kimliğini doğrulamak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3cbe6-146">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="3cbe6-147">Gerekli üstbilgilerin mevcut olduğunu doğrulayın (yetkilendirme, x-MS-Certificate-URL, x-MS-Signature-algoritma).</span><span class="sxs-lookup"><span data-stu-id="3cbe6-147">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="3cbe6-148">İçeriği imzalamak için kullanılan sertifikayı indirin (x-MS-Certificate-URL).</span><span class="sxs-lookup"><span data-stu-id="3cbe6-148">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="3cbe6-149">Sertifika zincirini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-149">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="3cbe6-150">Sertifikanın "organizasyonunu" doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-150">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="3cbe6-151">UTF8 kodlamalı içeriği bir arabelleğe okur.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-151">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="3cbe6-152">Bir RSA şifreleme sağlayıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-152">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="3cbe6-153">Verilerin belirtilen karma algoritmayla imzalandıklarla eşleştiğini doğrulayın (örneğin, SHA256).</span><span class="sxs-lookup"><span data-stu-id="3cbe6-153">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="3cbe6-154">Doğrulama başarılı olursa, iletiyi işleyin.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-154">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="3cbe6-155">Varsayılan olarak, imza belirteci bir yetkilendirme üst bilgisinde gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-155">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="3cbe6-156">Kaydınızın **Signaturetokentomssignatureheader** değerini true olarak ayarlarsanız, imza belirteci x-MS-Signature üst bilgisine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-156">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="3cbe6-157">Olay modeli</span><span class="sxs-lookup"><span data-stu-id="3cbe6-157">Event model</span></span>

<span data-ttu-id="3cbe6-158">Aşağıdaki tabloda bir Iş Ortağı Merkezi olayının özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-158">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="3cbe6-159">Özellikler</span><span class="sxs-lookup"><span data-stu-id="3cbe6-159">Properties</span></span>

| <span data-ttu-id="3cbe6-160">Ad</span><span class="sxs-lookup"><span data-stu-id="3cbe6-160">Name</span></span>                      | <span data-ttu-id="3cbe6-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3cbe6-161">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="3cbe6-162">**EventName**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-162">**EventName**</span></span>             | <span data-ttu-id="3cbe6-163">Olayın adı.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-163">The name of the event.</span></span> <span data-ttu-id="3cbe6-164">{Resource}-{Action} biçiminde.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-164">In the form {resource}-{action}.</span></span> <span data-ttu-id="3cbe6-165">Örneğin, "test oluşturma".</span><span class="sxs-lookup"><span data-stu-id="3cbe6-165">For example, "test-created".</span></span>  |
| <span data-ttu-id="3cbe6-166">**ResourceUri**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-166">**ResourceUri**</span></span>           | <span data-ttu-id="3cbe6-167">Değiştirilen kaynağın URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-167">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="3cbe6-168">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-168">**ResourceName**</span></span>          | <span data-ttu-id="3cbe6-169">Değiştirilen kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-169">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="3cbe6-170">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-170">**AuditUrl**</span></span>              | <span data-ttu-id="3cbe6-171">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-171">Optional.</span></span> <span data-ttu-id="3cbe6-172">Denetim kaydının URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-172">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="3cbe6-173">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="3cbe6-173">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="3cbe6-174">Kaynak değişikliği oluştuğunda UTC biçimindeki tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-174">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="3cbe6-175">Örnek</span><span class="sxs-lookup"><span data-stu-id="3cbe6-175">Sample</span></span>

<span data-ttu-id="3cbe6-176">Aşağıdaki örnek, bir Iş Ortağı Merkezi olayının yapısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-176">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="3cbe6-177">Web kancası API 'Leri</span><span class="sxs-lookup"><span data-stu-id="3cbe6-177">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="3cbe6-178">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3cbe6-178">Authentication</span></span>

<span data-ttu-id="3cbe6-179">Web kancası API 'Lerine yapılan tüm çağrılar, yetkilendirme üstbilgisindeki taşıyıcı belirteci kullanılarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-179">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="3cbe6-180">Erişim için bir erişim belirteci alın `https://api.partnercenter.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="3cbe6-180">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="3cbe6-181">Bu belirteç, Iş Ortağı Merkezi API 'lerinin geri kalanına erişmek için kullanılan belirteçtir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-181">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="3cbe6-182">Olayların bir listesini alın</span><span class="sxs-lookup"><span data-stu-id="3cbe6-182">Get a list of events</span></span>

<span data-ttu-id="3cbe6-183">Web kancası API 'Leri tarafından şu anda desteklenen olayların bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-183">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="3cbe6-184">Kaynak URL'si</span><span class="sxs-lookup"><span data-stu-id="3cbe6-184">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="3cbe6-185">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-185">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="3cbe6-186">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-186">Response example</span></span>

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

### <a name="register-to-receive-events"></a><span data-ttu-id="3cbe6-187">Olayları almak için kaydolun</span><span class="sxs-lookup"><span data-stu-id="3cbe6-187">Register to receive events</span></span>

<span data-ttu-id="3cbe6-188">Belirtilen olayları almak için bir kiracı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-188">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3cbe6-189">Kaynak URL'si</span><span class="sxs-lookup"><span data-stu-id="3cbe6-189">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="3cbe6-190">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-190">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="3cbe6-191">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-191">Response example</span></span>

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

### <a name="view-a-registration"></a><span data-ttu-id="3cbe6-192">Kayıt görüntüleme</span><span class="sxs-lookup"><span data-stu-id="3cbe6-192">View a registration</span></span>

<span data-ttu-id="3cbe6-193">Bir kiracının Web kancaları olay kaydını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-193">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3cbe6-194">Kaynak URL'si</span><span class="sxs-lookup"><span data-stu-id="3cbe6-194">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="3cbe6-195">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-195">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="3cbe6-196">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-196">Response example</span></span>

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

### <a name="update-an-event-registration"></a><span data-ttu-id="3cbe6-197">Olay kaydını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3cbe6-197">Update an event registration</span></span>

<span data-ttu-id="3cbe6-198">Var olan bir olay kaydını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-198">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3cbe6-199">Kaynak URL'si</span><span class="sxs-lookup"><span data-stu-id="3cbe6-199">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="3cbe6-200">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-200">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="3cbe6-201">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-201">Response example</span></span>

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

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="3cbe6-202">Kaydınızı doğrulamak için bir test olayı gönderin</span><span class="sxs-lookup"><span data-stu-id="3cbe6-202">Send a test event to validate your registration</span></span>

<span data-ttu-id="3cbe6-203">Web kancaları kaydını doğrulamak için bir test olayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-203">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="3cbe6-204">Bu test, Iş Ortağı Merkezi 'nden olay alacağınızı doğrulamaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-204">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="3cbe6-205">Bu olayların verileri, ilk olay oluşturulduktan sonra yedi gün sonra silinecektir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-205">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="3cbe6-206">Doğrulama olayını göndermeden önce, kayıt API 'sini kullanarak "test tarafından oluşturulan" olay için kaydolmalısınız.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-206">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="3cbe6-207">Bir doğrulama olayı naklederken dakikada 2 istekten oluşan bir kısıtlama sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-207">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3cbe6-208">Kaynak URL'si</span><span class="sxs-lookup"><span data-stu-id="3cbe6-208">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="3cbe6-209">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-209">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="3cbe6-210">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-210">Response example</span></span>

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

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="3cbe6-211">Olayın teslim edildiğini doğrulama</span><span class="sxs-lookup"><span data-stu-id="3cbe6-211">Verify that the event was delivered</span></span>

<span data-ttu-id="3cbe6-212">Doğrulama olayının geçerli durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-212">Returns the current state of the validation event.</span></span> <span data-ttu-id="3cbe6-213">Bu doğrulama, olay teslimi sorunlarını gidermek için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-213">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="3cbe6-214">Yanıt, olayı teslim etmek için yapılan her girişimde bir sonuç içerir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-214">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="3cbe6-215">Kaynak URL'si</span><span class="sxs-lookup"><span data-stu-id="3cbe6-215">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="3cbe6-216">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-216">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="3cbe6-217">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-217">Response example</span></span>

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

## <a name="example-for-signature-validation"></a><span data-ttu-id="3cbe6-218">Imza doğrulama örneği</span><span class="sxs-lookup"><span data-stu-id="3cbe6-218">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="3cbe6-219">Örnek geri çağırma denetleyicisi imzası (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="3cbe6-219">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="3cbe6-220">İmza doğrulama</span><span class="sxs-lookup"><span data-stu-id="3cbe6-220">Signature Validation</span></span>

<span data-ttu-id="3cbe6-221">Aşağıdaki örnek, Web kancası olaylarından geri çağırmaları alan denetleyiciye bir yetkilendirme özniteliğinin nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3cbe6-221">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

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
