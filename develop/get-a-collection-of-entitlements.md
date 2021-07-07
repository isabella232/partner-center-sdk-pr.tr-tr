---
title: Yetkilendirme koleksiyonu alma
description: Yetkilendirme koleksiyonunu elde etmek.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7bb8d3aefb11fae0af4bce790b41598d935de57c
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906421"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="e0f29-103">Yetkilendirme koleksiyonu alma</span><span class="sxs-lookup"><span data-stu-id="e0f29-103">Get a collection of entitlements</span></span>

<span data-ttu-id="e0f29-104">Yetkilendirme koleksiyonunu elde etmek.</span><span class="sxs-lookup"><span data-stu-id="e0f29-104">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0f29-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e0f29-105">Prerequisites</span></span>

- <span data-ttu-id="e0f29-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e0f29-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e0f29-107">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e0f29-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="e0f29-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e0f29-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e0f29-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e0f29-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e0f29-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="e0f29-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e0f29-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="e0f29-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e0f29-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="e0f29-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e0f29-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="e0f29-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e0f29-114">C\#</span><span class="sxs-lookup"><span data-stu-id="e0f29-114">C\#</span></span>

<span data-ttu-id="e0f29-115">Müşterinin yetkilendirme koleksiyonunu almak için, müşteri kimliğini kullanarak [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak [**Yetkilendirme**](entitlement-resources.md#entitlement) işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="e0f29-115">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="e0f29-116">Ardından **Entitlements** özelliğinden arabirimini alın ve yetkilendirme koleksiyonunu almak için **Get()** veya **GetAsync()** yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f29-116">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="e0f29-117">Alınacak yetkilendirmelerin süre sonu tarihlerini doldurmak için yukarıdaki aynı yöntemleri çağırarak isteğe bağlı **showExpiry** boole parametresini true **Get(true)** veya **GetAsync(true)** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e0f29-117">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="e0f29-118">Bu, yetkilendirme süre sonu tarihlerinin gerekli olduğunu gösterir (uygun olduğunda).</span><span class="sxs-lookup"><span data-stu-id="e0f29-118">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0f29-119">Şirket içi yetkilendirme türlerinin süre sonu tarihleri yok.</span><span class="sxs-lookup"><span data-stu-id="e0f29-119">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e0f29-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e0f29-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e0f29-121">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="e0f29-121">Request syntax</span></span>

| <span data-ttu-id="e0f29-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e0f29-122">Method</span></span> | <span data-ttu-id="e0f29-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e0f29-123">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="e0f29-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="e0f29-124">**GET**</span></span> | <span data-ttu-id="e0f29-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/yetkilendirmeLER HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e0f29-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="e0f29-126">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="e0f29-126">URI parameters</span></span>

<span data-ttu-id="e0f29-127">İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0f29-127">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="e0f29-128">Ad</span><span class="sxs-lookup"><span data-stu-id="e0f29-128">Name</span></span> | <span data-ttu-id="e0f29-129">Tür</span><span class="sxs-lookup"><span data-stu-id="e0f29-129">Type</span></span> | <span data-ttu-id="e0f29-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e0f29-130">Required</span></span> | <span data-ttu-id="e0f29-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e0f29-131">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="e0f29-132">customerId</span><span class="sxs-lookup"><span data-stu-id="e0f29-132">customerId</span></span> | <span data-ttu-id="e0f29-133">string</span><span class="sxs-lookup"><span data-stu-id="e0f29-133">string</span></span> | <span data-ttu-id="e0f29-134">Yes</span><span class="sxs-lookup"><span data-stu-id="e0f29-134">Yes</span></span> | <span data-ttu-id="e0f29-135">Müşteriyi tanımlayan GUID biçimli customerId.</span><span class="sxs-lookup"><span data-stu-id="e0f29-135">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="e0f29-136">entitlementType</span><span class="sxs-lookup"><span data-stu-id="e0f29-136">entitlementType</span></span> | <span data-ttu-id="e0f29-137">dize</span><span class="sxs-lookup"><span data-stu-id="e0f29-137">string</span></span> | <span data-ttu-id="e0f29-138">No</span><span class="sxs-lookup"><span data-stu-id="e0f29-138">No</span></span> | <span data-ttu-id="e0f29-139">Alınacak yetkilendirmelerin türünü belirtmek için kullanılabilir ( yazılım **veya** **reservedInstance** ).</span><span class="sxs-lookup"><span data-stu-id="e0f29-139">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="e0f29-140">Ayarlanmazsa, tüm türler alınır</span><span class="sxs-lookup"><span data-stu-id="e0f29-140">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="e0f29-141">showExpiry</span><span class="sxs-lookup"><span data-stu-id="e0f29-141">showExpiry</span></span> | <span data-ttu-id="e0f29-142">boolean</span><span class="sxs-lookup"><span data-stu-id="e0f29-142">boolean</span></span> | <span data-ttu-id="e0f29-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="e0f29-143">No</span></span> | <span data-ttu-id="e0f29-144">Yetkilendirme süre sonu tarihleri gerekip gerekip gereklğerlğerlerini gösteren isteğe bağlı bayrağı.</span><span class="sxs-lookup"><span data-stu-id="e0f29-144">Optional flag that indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e0f29-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e0f29-145">Request headers</span></span>

<span data-ttu-id="e0f29-146">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e0f29-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e0f29-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e0f29-147">Request body</span></span>

<span data-ttu-id="e0f29-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="e0f29-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e0f29-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e0f29-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e0f29-150">REST response</span></span>

<span data-ttu-id="e0f29-151">Başarılı olursa, yanıt gövdesi yetkilendirme [kaynaklarının bir koleksiyonunu](entitlement-resources.md#entitlement) içerir.</span><span class="sxs-lookup"><span data-stu-id="e0f29-151">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e0f29-152">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e0f29-152">Response success and error codes</span></span>

<span data-ttu-id="e0f29-153">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="e0f29-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e0f29-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0f29-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e0f29-155">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e0f29-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e0f29-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-156">Response example</span></span>

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

## <a name="additional-examples"></a><span data-ttu-id="e0f29-157">Ek Örnekler</span><span class="sxs-lookup"><span data-stu-id="e0f29-157">Additional Examples</span></span>

<span data-ttu-id="e0f29-158">Aşağıdaki örnek, süre sonu tarihleriyle birlikte belirli bir yetkilendirme türünü (uygun olduğunda) nasıl alacazlanı gösterir</span><span class="sxs-lookup"><span data-stu-id="e0f29-158">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="e0f29-159">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-159">C\# example</span></span>

<span data-ttu-id="e0f29-160">Belirli bir yetkilendirme türünü almak için **Entitlements** arabiriminden **ByEntitlementType** arabirimini alın ve **Get()** veya **GetAsync()** yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0f29-160">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="e0f29-161">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-161">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="e0f29-162">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-162">Response example</span></span>

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

<span data-ttu-id="e0f29-163">Aşağıdaki örneklerde, bir yetkilendirmeden ürünler ve rezervasyonlar hakkında bilgileri nasıl alasiniz?</span><span class="sxs-lookup"><span data-stu-id="e0f29-163">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="e0f29-164">SDK V1.8 kullanarak yetkilendirmeden sanal makine rezervasyon ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="e0f29-164">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="e0f29-165">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-165">C\# example</span></span>

<span data-ttu-id="e0f29-166">Bir yetkilendirmeden sanal makine ayırmaları ile ilgili daha fazla ayrıntı almak için artifactType = entitledArtifacts.link altında ortaya virtual_machine_reserved_instance.</span><span class="sxs-lookup"><span data-stu-id="e0f29-166">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="e0f29-167">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-167">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="e0f29-168">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-168">Response example</span></span>

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

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="e0f29-169">SDK V1.9 kullanarak yetkilendirmeden rezervasyon ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="e0f29-169">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="e0f29-170">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-170">C\# example</span></span>

<span data-ttu-id="e0f29-171">Ayrılmış örnek yetkilendirmeden rezervasyonlarla ilgili daha fazla ayrıntı almak için ile altında ortaya konulan URI'yi ```entitledArtifacts.link``` ```artifactType = reservedinstance``` çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f29-171">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="e0f29-172">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="e0f29-173">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e0f29-173">Response example</span></span>

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

### <a name="api-consumers"></a><span data-ttu-id="e0f29-174">API Tüketicileri</span><span class="sxs-lookup"><span data-stu-id="e0f29-174">API Consumers</span></span>

<span data-ttu-id="e0f29-175">Sanal makine ayrılmış örnek yetkilendirmelerini sorgulamak için API'yi kullanan iş ortakları - Geriye dönük uyumluluğu korumak için **/customers/{customerId}/yetkilendirmelerinden gelen istek URI'sini /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** olarak güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e0f29-175">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="e0f29-176">Sanal makineyi veya Azure SQL gelişmiş sözleşmeyle tüketmek için istek URI'sini **/customers/{customerId}/entitlements?entitlementType=reservedinstance olarak güncelleştirin.**</span><span class="sxs-lookup"><span data-stu-id="e0f29-176">To consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
