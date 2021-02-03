---
title: Yetkilendirme koleksiyonu alma
description: Yetkilendirmeler koleksiyonu alma.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2cc485429941dd2080bd285553333a01fc0ffd1
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769292"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="e8aeb-103">Yetkilendirme koleksiyonu alma</span><span class="sxs-lookup"><span data-stu-id="e8aeb-103">Get a collection of entitlements</span></span>

<span data-ttu-id="e8aeb-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="e8aeb-104">**Applies To**</span></span>

- <span data-ttu-id="e8aeb-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e8aeb-105">Partner Center</span></span>

<span data-ttu-id="e8aeb-106">Yetkilendirmeler koleksiyonu alma.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-106">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8aeb-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e8aeb-107">Prerequisites</span></span>

- <span data-ttu-id="e8aeb-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e8aeb-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="e8aeb-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e8aeb-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e8aeb-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e8aeb-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e8aeb-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e8aeb-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e8aeb-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="e8aeb-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e8aeb-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e8aeb-116">C\#</span></span>

<span data-ttu-id="e8aeb-117">Bir müşteriye yönelik yetkilendirmeler koleksiyonu almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak [**Yetkilendirme**](entitlement-resources.md#entitlement) işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-117">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="e8aeb-118">Daha sonra, **yetkilendirmeler** özelliğinden arabirimi alın ve yetkilendirme koleksiyonunu almak için **Get ()** veya **GetAsync ()** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-118">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="e8aeb-119">Alınacak yetkilendirmelerin bitiş tarihlerini doldurmak için yukarıdaki aynı yöntemleri çağırın ve **Showsüre sonu** isteğe bağlı Boolean parametresini true **Get (true)** veya **GetAsync (true)** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-119">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="e8aeb-120">Bu, yetkilendirme süre sonu tarihlerinin gerekli olduğunu gösterir (varsa).</span><span class="sxs-lookup"><span data-stu-id="e8aeb-120">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8aeb-121">Şirket içi yetkilendirme türlerinde süre sonu tarihleri yoktur.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-121">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e8aeb-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e8aeb-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e8aeb-123">Request syntax</span></span>

| <span data-ttu-id="e8aeb-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e8aeb-124">Method</span></span> | <span data-ttu-id="e8aeb-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e8aeb-125">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="e8aeb-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="e8aeb-126">**GET**</span></span> | <span data-ttu-id="e8aeb-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{CustomerID}/yetkilendirmeler http/1.1</span><span class="sxs-lookup"><span data-stu-id="e8aeb-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="e8aeb-128">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="e8aeb-128">URI parameters</span></span>

<span data-ttu-id="e8aeb-129">İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="e8aeb-130">Ad</span><span class="sxs-lookup"><span data-stu-id="e8aeb-130">Name</span></span> | <span data-ttu-id="e8aeb-131">Tür</span><span class="sxs-lookup"><span data-stu-id="e8aeb-131">Type</span></span> | <span data-ttu-id="e8aeb-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e8aeb-132">Required</span></span> | <span data-ttu-id="e8aeb-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e8aeb-133">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="e8aeb-134">customerId</span><span class="sxs-lookup"><span data-stu-id="e8aeb-134">customerId</span></span> | <span data-ttu-id="e8aeb-135">string</span><span class="sxs-lookup"><span data-stu-id="e8aeb-135">string</span></span> | <span data-ttu-id="e8aeb-136">Yes</span><span class="sxs-lookup"><span data-stu-id="e8aeb-136">Yes</span></span> | <span data-ttu-id="e8aeb-137">Müşteriyi tanımlayan bir GUID biçimli CustomerID.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-137">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="e8aeb-138">entitlementType</span><span class="sxs-lookup"><span data-stu-id="e8aeb-138">entitlementType</span></span> | <span data-ttu-id="e8aeb-139">dize</span><span class="sxs-lookup"><span data-stu-id="e8aeb-139">string</span></span> | <span data-ttu-id="e8aeb-140">No</span><span class="sxs-lookup"><span data-stu-id="e8aeb-140">No</span></span> | <span data-ttu-id="e8aeb-141">Alınacak yetkilendirmelerin türünü (**yazılım** veya **reservedınstance** ) belirtmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-141">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="e8aeb-142">Ayarlanmamışsa, tüm türler alınır</span><span class="sxs-lookup"><span data-stu-id="e8aeb-142">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="e8aeb-143">Showsüre sonu</span><span class="sxs-lookup"><span data-stu-id="e8aeb-143">showExpiry</span></span> | <span data-ttu-id="e8aeb-144">boolean</span><span class="sxs-lookup"><span data-stu-id="e8aeb-144">boolean</span></span> | <span data-ttu-id="e8aeb-145">No</span><span class="sxs-lookup"><span data-stu-id="e8aeb-145">No</span></span> | <span data-ttu-id="e8aeb-146">Yetkilendirmelerin süre sonu tarihlerinin gerekip gerekmediğini belirten isteğe bağlı bayrak.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-146">Optional flag which indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e8aeb-147">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e8aeb-147">Request headers</span></span>

<span data-ttu-id="e8aeb-148">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e8aeb-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e8aeb-149">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e8aeb-149">Request body</span></span>

<span data-ttu-id="e8aeb-150">Yok.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e8aeb-151">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e8aeb-152">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e8aeb-152">REST response</span></span>

<span data-ttu-id="e8aeb-153">Başarılı olursa, yanıt gövdesi bir [Yetkilendirme](entitlement-resources.md#entitlement) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-153">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e8aeb-154">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e8aeb-154">Response success and error codes</span></span>

<span data-ttu-id="e8aeb-155">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e8aeb-156">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e8aeb-157">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e8aeb-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e8aeb-158">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
    },
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <a name="additional-examples"></a><span data-ttu-id="e8aeb-159">Ek Örnekler</span><span class="sxs-lookup"><span data-stu-id="e8aeb-159">Additional Examples</span></span>

<span data-ttu-id="e8aeb-160">Aşağıdaki örnek, belirli bir yetkilendirmelerin, süre sonu tarihleriyle birlikte nasıl alınacağını gösterir (uygun olduğunda)</span><span class="sxs-lookup"><span data-stu-id="e8aeb-160">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="e8aeb-161">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-161">C\# example</span></span>

<span data-ttu-id="e8aeb-162">Belirli bir hak türünü almak için, **yetkilendirmeler** arabiriminden **Byentitlementtype** arabirimini alın ve **Get ()** veya **GetAsync ()** yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-162">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="e8aeb-163">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="e8aeb-164">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="e8aeb-165">Aşağıdaki örneklerde, bir yetkilendirkarşı ürün ve rezervasyonlar hakkındaki bilgilerin nasıl alınacağını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-165">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="e8aeb-166">SDK V 1.8 kullanarak bir yetkilendirkarşı sanal makine ayırma ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="e8aeb-166">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="e8aeb-167">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-167">C\# example</span></span>

<span data-ttu-id="e8aeb-168">Yetkilendirmeli sanal makine ayırmaları hakkında daha fazla ayrıntı almak için, entitledArtifacts. LINK altında sunulan URI 'yi artifactType = virtual_machine_reserved_instance ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-168">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance .</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="e8aeb-169">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="e8aeb-170">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-170">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="e8aeb-171">SDK V 1.9 kullanarak bir yetkilendirkarşı rezervasyon ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="e8aeb-171">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="e8aeb-172">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-172">C\# example</span></span>

<span data-ttu-id="e8aeb-173">Ayrılmış bir örnek yetkilendirmeli rezervasyonlar ile ilgili daha fazla ayrıntı almak için, altında sunulan URI 'yi çağırın ```entitledArtifacts.link``` ```artifactType = reservedinstance``` .</span><span class="sxs-lookup"><span data-stu-id="e8aeb-173">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="e8aeb-174">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="e8aeb-175">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e8aeb-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "reservedinstance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="api-consumers"></a><span data-ttu-id="e8aeb-176">API tüketicileri</span><span class="sxs-lookup"><span data-stu-id="e8aeb-176">API Consumers</span></span>

<span data-ttu-id="e8aeb-177">Sanal makine ayrılmış örnek yetkilendirmelerini sorgulamak için API kullanan iş ortakları-geriye dönük uyumluluğu sürdürmek için **/Customers/{CustomerID}/yetkilendirmeler ' den/Customers/{CustomerID}/yetkilendirmeler? entitlementType = virtualmachinereservedınstance** ' a YÖNELIK istek URI 'sini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-177">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="e8aeb-178">Sanal makineyi veya Azure SQL 'i gelişmiş sözleşmeyle kullanmak için, istek URI 'sini **/Customers/{CustomerID}/yetkilendirmeler? entitlementType = reservedınstance** olarak güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8aeb-178">In order to consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
