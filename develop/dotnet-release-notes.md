---
title: İş Ortağı Merkezi .NET SDK sürüm notları
description: Iş ortağı merkezi .NET SDK 'sının en son sürümü için sürüm notları.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2fe309500cc80e962c101ad97f0712bef7e11eb3
ms.sourcegitcommit: f7fce0b35ab1579e59136abc357b71cf768b81b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104895542"
---
# <a name="net-sdk-release-notes"></a><span data-ttu-id="ee01a-103">.NET SDK sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ee01a-103">.NET SDK release notes</span></span>

<span data-ttu-id="ee01a-104">Aşağıdaki sürüm notları, [Microsoft Iş ortağı merkezi .NET SDK 'sının](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)yeni sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee01a-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="ee01a-105">GitHub 'da [.NET SDK örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee01a-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="ee01a-106">.NET API tarayıcısında [Iş ortağı merkezi .NET API başvurusunu](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee01a-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-1170"></a><span data-ttu-id="ee01a-107">Sürüm 1.17.0</span><span class="sxs-lookup"><span data-stu-id="ee01a-107">Version 1.17.0</span></span>

<span data-ttu-id="ee01a-108">[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v 1.17.0 artık genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="ee01a-109">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ee01a-110">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="ee01a-110">The following changes are included in this version:</span></span>

* <span data-ttu-id="ee01a-111">Denetim güncelleştirildi-müşterinin ne zaman onayladığı ve sonlandırıldığı hakkında yeni işlem türleri eklendi</span><span class="sxs-lookup"><span data-stu-id="ee01a-111">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="ee01a-112">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="ee01a-112">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="ee01a-113">Dapadminrelationshipsonlandırılan</span><span class="sxs-lookup"><span data-stu-id="ee01a-113">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="ee01a-114">Denetim güncelleştirildi – müşteri dizin rolü senaryosunu desteklemek için yeni kaynak ve işlem türleri eklendi</span><span class="sxs-lookup"><span data-stu-id="ee01a-114">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="ee01a-115">Kaynak türü "[Customerdirectoryrole](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="ee01a-115">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="ee01a-116">"[Addusermember](auditing-resources.md)" ve "[removeusermember](auditing-resources.md)" işlem türleri</span><span class="sxs-lookup"><span data-stu-id="ee01a-116">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="ee01a-117">Müşteriler için SDK güncelleştirmeleri hesabı-aşağıdaki API 'leri destekler</span><span class="sxs-lookup"><span data-stu-id="ee01a-117">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="ee01a-118">/Customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus al</span><span class="sxs-lookup"><span data-stu-id="ee01a-118">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="ee01a-119">/Customers/{Customer-Tenant-ID}/nitelikler al</span><span class="sxs-lookup"><span data-stu-id="ee01a-119">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="ee01a-120">/Customers/{customer_id}/nitelikler SONRASı? Code = {validationCode}</span><span class="sxs-lookup"><span data-stu-id="ee01a-120">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="ee01a-121">**Şu anda, yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinin parçası olan iş ortakları için yapılan davet temelinde mevcut olan yeni ticaretin bir parçası olarak tanıtılan değişiklikler.**</span><span class="sxs-lookup"><span data-stu-id="ee01a-121">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="ee01a-122">Yeni ticaret özel önizlemesinin parçası olmayan iş ortakları, etkileri fark etmez ve geriye dönük olarak uyumlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee01a-122">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="ee01a-123">Katalog değişiklikleri:</span><span class="sxs-lookup"><span data-stu-id="ee01a-123">Catalog Changes:</span></span>
    * <span data-ttu-id="ee01a-124">/Products/{product-id}/SKUs/{SKU-id} al</span><span class="sxs-lookup"><span data-stu-id="ee01a-124">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="ee01a-125">Satın alın ve yönetin:</span><span class="sxs-lookup"><span data-stu-id="ee01a-125">Purchase and Manage:</span></span>
    * <span data-ttu-id="ee01a-126">/Customers/{CustomerID}/abonelikleri al</span><span class="sxs-lookup"><span data-stu-id="ee01a-126">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="ee01a-127">/Customers/{CustomerID}/Subscriptions/{SubscriptionID} al</span><span class="sxs-lookup"><span data-stu-id="ee01a-127">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="ee01a-128">PATCH/Customers/{CustomerID}/Subscriptions/{SubscriptionID}</span><span class="sxs-lookup"><span data-stu-id="ee01a-128">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="ee01a-129">/Customers/{CustomerID}/Subscriptions/{SubscriptionID}/geçişli tioneligılıklara al</span><span class="sxs-lookup"><span data-stu-id="ee01a-129">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="ee01a-130">/Customers/{CustomerID}/Subscriptions/{SubscriptionID}/geçişlerini al</span><span class="sxs-lookup"><span data-stu-id="ee01a-130">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="ee01a-131">POST/Customers/{CustomerID}/Subscriptions/{SubscriptionID}/geçişlerin</span><span class="sxs-lookup"><span data-stu-id="ee01a-131">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="ee01a-132">Sürüm 1.16.3</span><span class="sxs-lookup"><span data-stu-id="ee01a-132">Version 1.16.3</span></span>

<span data-ttu-id="ee01a-133">[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v 1.16.3 artık genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-133">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="ee01a-134">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-134">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ee01a-135">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="ee01a-135">The following changes are included in this version:</span></span>

* <span data-ttu-id="ee01a-136">SelfServePolicies-yeni işlevsellik eklendi</span><span class="sxs-lookup"><span data-stu-id="ee01a-136">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="ee01a-137">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ee01a-137">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="ee01a-138">Getlıfselfservicepolicies</span><span class="sxs-lookup"><span data-stu-id="ee01a-138">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="ee01a-139">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ee01a-139">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="ee01a-140">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ee01a-140">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="ee01a-141">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="ee01a-141">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="ee01a-142">Müşteriler şirket profili</span><span class="sxs-lookup"><span data-stu-id="ee01a-142">Customers Company Profile</span></span>
  * <span data-ttu-id="ee01a-143">[Organizationregistrationnumber](create-a-customer.md) eklendi</span><span class="sxs-lookup"><span data-stu-id="ee01a-143">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="ee01a-144">CustomerBillingProfile. DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="ee01a-144">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="ee01a-145">MiddleName eklendi</span><span class="sxs-lookup"><span data-stu-id="ee01a-145">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="ee01a-146">Sürüm 1.16.2</span><span class="sxs-lookup"><span data-stu-id="ee01a-146">Version 1.16.2</span></span>

<span data-ttu-id="ee01a-147">[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 artık genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="ee01a-148">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ee01a-149">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="ee01a-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="ee01a-150">Denetim kaydı için desteklenen işlem türlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ee01a-150">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="ee01a-151">Yeni eklenen olanlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ee01a-151">The newly added ones are:</span></span>
  * <span data-ttu-id="ee01a-152">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ee01a-152">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="ee01a-153">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ee01a-153">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="ee01a-154">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ee01a-154">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="ee01a-155">RemovePartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="ee01a-155">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="ee01a-156">DeleteTipCustomer</span><span class="sxs-lookup"><span data-stu-id="ee01a-156">DeleteTipCustomer</span></span>
  * <span data-ttu-id="ee01a-157">Createrelatedbaşvurunun</span><span class="sxs-lookup"><span data-stu-id="ee01a-157">CreateRelatedReferral</span></span>
  * <span data-ttu-id="ee01a-158">Updaterelatedbaşvurunun</span><span class="sxs-lookup"><span data-stu-id="ee01a-158">UpdateRelatedReferral</span></span>

* <span data-ttu-id="ee01a-159">Hizmet isteği oluşturma artık kullanım dışıdır</span><span class="sxs-lookup"><span data-stu-id="ee01a-159">Service request creation is now deprecated</span></span>
* <span data-ttu-id="ee01a-160">Destek konuları artık kullanım dışıdır</span><span class="sxs-lookup"><span data-stu-id="ee01a-160">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="ee01a-161">Sürüm 1.16.1</span><span class="sxs-lookup"><span data-stu-id="ee01a-161">Version 1.16.1</span></span>

<span data-ttu-id="ee01a-162">[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 artık genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-162">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="ee01a-163">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-163">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ee01a-164">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="ee01a-164">The following changes are included in this version:</span></span>

<span data-ttu-id="ee01a-165">Mevcut Microsoft Iş Ortağı Merkezi SDK 'sını .NET Framework 'den .NET Standard 2,0 platformuna geçirdik.</span><span class="sxs-lookup"><span data-stu-id="ee01a-165">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="ee01a-166">Bu, SDK 'nın .NET Framework 4.6.1 ve üstünü kullanarak var olan uygulamalarla uyumlu hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ee01a-166">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="ee01a-167">SDK, .NET Core 2,0 ve üstünü destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="ee01a-167">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="ee01a-168">Mevcut uygulamalara geçmeden önce [.NET uygulama desteğini](/dotnet/standard/net-standard) kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="ee01a-168">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="ee01a-169">Sürüm 1.15.3</span><span class="sxs-lookup"><span data-stu-id="ee01a-169">Version 1.15.3</span></span>
<span data-ttu-id="ee01a-170">[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 artık genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-170">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="ee01a-171">Güncelleştirilmiş REST API 'Leri ve [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-171">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="ee01a-172">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="ee01a-172">The following changes are included in this version:</span></span>

* <span data-ttu-id="ee01a-173">İş ortağı sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="ee01a-173">Partner Agreement</span></span>
  * <span data-ttu-id="ee01a-174">Dolaylı sağlayıcıların, [dolaylı satıcıların Microsoft Iş ortağı sözleşmesi durumunu doğrulama](verify-indirect-reseller-mpa-status.md)özelliği eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ee01a-174">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="ee01a-175">Ürünler</span><span class="sxs-lookup"><span data-stu-id="ee01a-175">Products</span></span>
  * <span data-ttu-id="ee01a-176">Aşağıdaki iki arabirim Microsoft. Store. PartnerCenter. Products ad alanı altına yanlış yerleştirildi.</span><span class="sxs-lookup"><span data-stu-id="ee01a-176">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="ee01a-177">Şimdi, Microsoft. Store. PartnerCenter. Customers. Products ad alanı altında bulunur.</span><span class="sxs-lookup"><span data-stu-id="ee01a-177">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="ee01a-178">Icustomerproductbyrezervationscope</span><span class="sxs-lookup"><span data-stu-id="ee01a-178">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="ee01a-179">Icustomerskubyırezervationscope</span><span class="sxs-lookup"><span data-stu-id="ee01a-179">ICustomerSkuByReservationScope</span></span>
