---
title: Bir kullanıcıya lisans atama
description: C veya REST API 'lerinin kullanımı gibi Iş Ortağı Merkezi API 'Leri aracılığıyla bir müşteri kullanıcısına lisans atamayı öğrenin \# .
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770007"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="8a052-103">Iş Ortağı Merkezi API 'Leri aracılığıyla bir kullanıcıya lisans atama</span><span class="sxs-lookup"><span data-stu-id="8a052-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="8a052-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="8a052-104">**Applies to:**</span></span>

- <span data-ttu-id="8a052-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8a052-105">Partner Center</span></span>

<span data-ttu-id="8a052-106">Bir müşteri kullanıcısına lisans atama.</span><span class="sxs-lookup"><span data-stu-id="8a052-106">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a052-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8a052-107">Prerequisites</span></span>

- <span data-ttu-id="8a052-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8a052-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8a052-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="8a052-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8a052-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8a052-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8a052-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a052-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8a052-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8a052-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8a052-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="8a052-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8a052-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="8a052-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8a052-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="8a052-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8a052-116">Bir müşteri Kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8a052-116">A customer user identifier.</span></span> <span data-ttu-id="8a052-117">Bu KIMLIK, lisansın atanacağı kullanıcıyı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8a052-117">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="8a052-118">Lisansın ürününü tanımlayan bir Ürün SKU tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8a052-118">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="8a052-119">Kod aracılığıyla lisans atama</span><span class="sxs-lookup"><span data-stu-id="8a052-119">Assigning licenses through code</span></span>

<span data-ttu-id="8a052-120">Bir kullanıcıya lisans atadığınızda, müşterinin abone olunan SKU 'ların koleksiyonundan seçim yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a052-120">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="8a052-121">Daha sonra, atamak istediğiniz ürünleri tanımladıktan sonra, atamaları yapabilmek için her bir ürün için Ürün SKU 'su KIMLIĞINI edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a052-121">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="8a052-122">Her [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) örneği, [**productsku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) nesnesine başvuralabileceğiniz ve [**kimliği**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)alabileceğiniz bir [**productsku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="8a052-122">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="8a052-123">Lisans atama isteğinin tek bir lisans grubundan lisans içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a052-123">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="8a052-124">Örneğin, aynı istekte [**grup1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) ve **grup2** 'tan lisans atayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="8a052-124">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="8a052-125">Tek bir istekte birden fazla gruptan lisans atama girişimi uygun bir hata ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8a052-125">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="8a052-126">Lisans grubuna göre hangi lisansların kullanılabildiğini öğrenmek için bkz. [lisans grubuna göre kullanılabilir lisansların listesini alma](get-a-list-of-available-licenses-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="8a052-126">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="8a052-127">Şu kod aracılığıyla lisans atama adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8a052-127">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="8a052-128">[**Licenseatama**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a052-128">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="8a052-129">Atanacak Ürün SKU 'sunu ve hizmet planlarını belirtmek için bu nesneyi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="8a052-129">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="8a052-130">Nesne özelliklerini aşağıda gösterildiği gibi doldurun.</span><span class="sxs-lookup"><span data-stu-id="8a052-130">Populate the object properties as shown below.</span></span> <span data-ttu-id="8a052-131">Bu kod, zaten Ürün SKU KIMLIĞINIZ olduğunu ve kullanılabilir tüm hizmet planlarının atanacağını (yani, hiçbirinin dışlanmayacağını) varsayar.</span><span class="sxs-lookup"><span data-stu-id="8a052-131">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="8a052-132">Ürün SKU KIMLIĞINIZ yoksa, abone olunan SKU 'ların koleksiyonunu almanız ve Ürün SKU 'su kimliğini bunlardan birine almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a052-132">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="8a052-133">Ürün SKU 'SU adını biliyorsanız bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8a052-133">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="8a052-134">Sonra, [**Licenseatama**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)türünde yeni bir liste oluşturun ve lisans nesnesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8a052-134">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="8a052-135">Her birini listeye ayrı ekleyerek birden fazla lisans atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a052-135">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="8a052-136">Bu listeye dahil edilen lisanslar aynı lisans grubundan olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8a052-136">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="8a052-137">[**Licenseupdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) örneği oluşturun ve lisans atamalarının listesini [**licensestoassign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) özelliğine atayın.</span><span class="sxs-lookup"><span data-stu-id="8a052-137">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="8a052-138">Lisansları atamak için [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metodunu çağırın ve lisans güncelleştirme nesnesini aşağıda gösterildiği gibi geçirin.</span><span class="sxs-lookup"><span data-stu-id="8a052-138">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="8a052-139">C\#</span><span class="sxs-lookup"><span data-stu-id="8a052-139">C\#</span></span>

<span data-ttu-id="8a052-140">Bir müşteri kullanıcısına lisans atamak için, önce bir [**Licenseatama**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) nesnesi örneği oluşturun ve [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) ve [**excludedplanlar**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) özelliklerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="8a052-140">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="8a052-141">Atanacak Ürün SKU 'sunu belirtmek için bu nesneyi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="8a052-141">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="8a052-142">Sonra, **Licenseatama** türünde yeni bir liste oluşturun ve lisans nesnesini listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8a052-142">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="8a052-143">Sonra bir [**Licenseupdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) örneği oluşturun ve lisans atamalarının listesini [**licensestoassign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) özelliğine atayın.</span><span class="sxs-lookup"><span data-stu-id="8a052-143">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="8a052-144">Ardından, müşteriyi tanımlamak için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve kullanıcıyı tanımlamak IÇIN Kullanıcı kimliği ile [**Users. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a052-144">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="8a052-145">Daha sonra [**Licenseupdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) özelliğinden müşteri Kullanıcı Lisansı güncelleştirme işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="8a052-145">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="8a052-146">Son olarak, [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metodunu çağırın ve lisansı atamak için lisans güncelleştirme nesnesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="8a052-146">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

<span data-ttu-id="8a052-147">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8a052-147">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8a052-148">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CustomerUserAssignLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="8a052-148">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8a052-149">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8a052-149">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8a052-150">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8a052-150">Request syntax</span></span>

| <span data-ttu-id="8a052-151">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8a052-151">Method</span></span>   | <span data-ttu-id="8a052-152">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8a052-152">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8a052-153">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="8a052-153">**POST**</span></span> | <span data-ttu-id="8a052-154">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="8a052-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8a052-155">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="8a052-155">URI parameters</span></span>

<span data-ttu-id="8a052-156">Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a052-156">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="8a052-157">Ad</span><span class="sxs-lookup"><span data-stu-id="8a052-157">Name</span></span>        | <span data-ttu-id="8a052-158">Tür</span><span class="sxs-lookup"><span data-stu-id="8a052-158">Type</span></span>   | <span data-ttu-id="8a052-159">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8a052-159">Required</span></span> | <span data-ttu-id="8a052-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a052-160">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="8a052-161">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="8a052-161">customer-id</span></span> | <span data-ttu-id="8a052-162">string</span><span class="sxs-lookup"><span data-stu-id="8a052-162">string</span></span> | <span data-ttu-id="8a052-163">Yes</span><span class="sxs-lookup"><span data-stu-id="8a052-163">Yes</span></span>      | <span data-ttu-id="8a052-164">Müşteriyi tanımlayan GUID biçimli bir KIMLIK.</span><span class="sxs-lookup"><span data-stu-id="8a052-164">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="8a052-165">user-id</span><span class="sxs-lookup"><span data-stu-id="8a052-165">user-id</span></span>     | <span data-ttu-id="8a052-166">string</span><span class="sxs-lookup"><span data-stu-id="8a052-166">string</span></span> | <span data-ttu-id="8a052-167">Yes</span><span class="sxs-lookup"><span data-stu-id="8a052-167">Yes</span></span>      | <span data-ttu-id="8a052-168">Kullanıcıyı tanımlayan GUID biçimli bir KIMLIK.</span><span class="sxs-lookup"><span data-stu-id="8a052-168">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="8a052-169">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8a052-169">Request headers</span></span>

<span data-ttu-id="8a052-170">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8a052-170">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8a052-171">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="8a052-171">Request body</span></span>

<span data-ttu-id="8a052-172">Atanacak lisansları belirten istek gövdesine bir [Licenseupdate](license-resources.md#licenseupdate) kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8a052-172">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="8a052-173">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8a052-173">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="8a052-174">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8a052-174">REST response</span></span>

<span data-ttu-id="8a052-175">Başarılı olursa, HTTP yanıt durum kodu 201 döndürülür ve yanıt gövdesi lisans bilgilerine sahip bir [Licenseupdate](license-resources.md#licenseupdate) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="8a052-175">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8a052-176">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8a052-176">Response success and error codes</span></span>

<span data-ttu-id="8a052-177">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="8a052-177">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8a052-178">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a052-178">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8a052-179">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8a052-179">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="8a052-180">Yanıt örneği (başarılı)</span><span class="sxs-lookup"><span data-stu-id="8a052-180">Response example (success)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="8a052-181">Yanıt örneği (lisans kullanılamıyor)</span><span class="sxs-lookup"><span data-stu-id="8a052-181">Response example (license isn't available)</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
