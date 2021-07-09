---
title: İş Ortağı Merkezi .NET SDK sürüm notları
description: .NET SDK'sı için en son İş Ortağı Merkezi sürüm notları.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1532d48c00550f5eb437ed0164d6a1f7bb340dd
ms.sourcegitcommit: 53c94db33b09c30e762b842c4275b2b531dba932
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113522643"
---
# <a name="net-sdk-release-notes"></a><span data-ttu-id="a08a7-103">.NET SDK sürüm notları</span><span class="sxs-lookup"><span data-stu-id="a08a7-103">.NET SDK release notes</span></span>

<span data-ttu-id="a08a7-104">Microsoft İş Ortağı Merkezi [.NET SDK'sı yeni](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)sürümleri için aşağıdaki sürüm notları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="a08a7-105">[.NET SDK örneklerini GitHub.](https://github.com/Microsoft/Partner-Center-DotNet-Samples)</span><span class="sxs-lookup"><span data-stu-id="a08a7-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="a08a7-106">[.NET API İş Ortağı Merkezi .NET API Browser'da](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a08a7-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-201"></a><span data-ttu-id="a08a7-107">Sürüm 2.0.1</span><span class="sxs-lookup"><span data-stu-id="a08a7-107">Version 2.0.1</span></span>

<span data-ttu-id="a08a7-108">[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 genel kullanılabilirlik özelliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="a08a7-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 is now general availability.</span></span> <span data-ttu-id="a08a7-109">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a08a7-110">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="a08a7-110">The following changes are included in this version:</span></span>

> [!NOTE]
> <span data-ttu-id="a08a7-111">Şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesinde yer alan iş ortaklarının daveti temel alınarak kullanılabilen Yeni Ticaret Deneyimleri ("NCE") kapsamında yapılan bazı değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="a08a7-111">Some of changes introduced as part of New Commerce Experiences (“NCE”) which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span> <span data-ttu-id="a08a7-112">Yeni ticari özel önizleme kapsamında yer alan iş ortakları, etkileri fark etmez ve geriye dönük uyumlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a08a7-112">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>

### <a name="common"></a><span data-ttu-id="a08a7-113">Common</span><span class="sxs-lookup"><span data-stu-id="a08a7-113">Common</span></span>
* <span data-ttu-id="a08a7-114">Kimlik doğrulama kitaplığı başvurusunda değişiklik – Başvuru, Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)olan başvuru, Microsoft Kimlik Doğrulama Kitaplığı ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)) olarak değiştirildi</span><span class="sxs-lookup"><span data-stu-id="a08a7-114">Change on the reference to authentication library – The reference is changed from Azure Active Directory Authentication Library ([ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)) to Microsoft Authentication Library ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet))</span></span>

  <span data-ttu-id="a08a7-115">MSAL'nin uygulamanıza veya .NET örneğinde doğru şekilde çalıştırılana kadar aşağıdaki değişiklikler gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a08a7-115">Following changes should be made to ensure MSAL runs correctly on your application or .NET sample:</span></span>

  * <span data-ttu-id="a08a7-116">Mobil `https://login.microsoftonline.com/common/oauth2/nativeclient` ve masaüstü uygulamaları için RedirectUrl olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="a08a7-116">Add `https://login.microsoftonline.com/common/oauth2/nativeclient` as RedirectUrl for Mobile and desktop applications</span></span>
  * <span data-ttu-id="a08a7-117">Uygulama **yapılandırma** dosyanız içinde UserAuthentication bölümüne Etki Alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a08a7-117">Add **Domain** into UserAuthentication section in your application configuration file.</span></span> 

    <span data-ttu-id="a08a7-118">Etki alanı, Azure Active Directory Azure AD uygulamasının oluşturularak oluşturulan etki alanı veya kiracı kimliğidir</span><span class="sxs-lookup"><span data-stu-id="a08a7-118">Domain is the Azure Active Directory domain or tenant ID where the Azure AD application was created</span></span>

* <span data-ttu-id="a08a7-119">[Hata kodları](error-codes.md) – Yeni hata kodu eklendi</span><span class="sxs-lookup"><span data-stu-id="a08a7-119">[Error codes](error-codes.md) – New error code added</span></span> 
  * <span data-ttu-id="a08a7-120">408: İstek zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="a08a7-120">408: Request timeout</span></span>
  * <span data-ttu-id="a08a7-121">504: Ağ geçidi zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="a08a7-121">504: Gateway timeout</span></span> 

### <a name="manage-billing"></a><span data-ttu-id="a08a7-122">Faturalandırmayı yönetme</span><span class="sxs-lookup"><span data-stu-id="a08a7-122">Manage billing</span></span>

* <span data-ttu-id="a08a7-123">[Fatura satırı öğeleri](get-invoiceline-items.md) - aşağıdaki API'lere yeni öznitelikler eklendi:</span><span class="sxs-lookup"><span data-stu-id="a08a7-123">[Invoice line-items](get-invoiceline-items.md) - new attributes added to following APIs:</span></span>
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  <span data-ttu-id="a08a7-124">Yeni öznitelikler:</span><span class="sxs-lookup"><span data-stu-id="a08a7-124">New attributes:</span></span> 
  * <span data-ttu-id="a08a7-125">productQualifiers</span><span class="sxs-lookup"><span data-stu-id="a08a7-125">productQualifiers</span></span>
  * <span data-ttu-id="a08a7-126">subscriptionStartDate</span><span class="sxs-lookup"><span data-stu-id="a08a7-126">subscriptionStartDate</span></span>
  * <span data-ttu-id="a08a7-127">subscriptionEndDate</span><span class="sxs-lookup"><span data-stu-id="a08a7-127">subscriptionEndDate</span></span>
  * <span data-ttu-id="a08a7-128">referenceId</span><span class="sxs-lookup"><span data-stu-id="a08a7-128">referenceId</span></span>
  * <span data-ttu-id="a08a7-129">creditReasonCode (Yalnızca NCE için geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="a08a7-129">creditReasonCode  (Only applicable to NCE)</span></span>
  * <span data-ttu-id="a08a7-130">promotionId</span><span class="sxs-lookup"><span data-stu-id="a08a7-130">promotionId</span></span> 


* <span data-ttu-id="a08a7-131">[Günlük olarak derecelendirilmiş kullanım Satır öğeleri](get-invoice-billed-consumption-lineitems.md) – aşağıdaki API'ye yeni öznitelikler eklendi:</span><span class="sxs-lookup"><span data-stu-id="a08a7-131">[Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – new attributes added to following API:</span></span> 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  <span data-ttu-id="a08a7-132">Yeni öznitelikler:</span><span class="sxs-lookup"><span data-stu-id="a08a7-132">New attributes:</span></span> 
  * <span data-ttu-id="a08a7-133">hasPartnerEarnedCredit (Yalnızca NCE için geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="a08a7-133">hasPartnerEarnedCredit (Only applicable to NCE)</span></span>
  * <span data-ttu-id="a08a7-134">creditType (Yalnızca NCE için geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="a08a7-134">creditType (Only applicable to NCE)</span></span>
  * <span data-ttu-id="a08a7-135">rateOfCredit (Yalnızca NCE için geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="a08a7-135">rateOfCredit (Only applicable to NCE)</span></span>


### <a name="manage-orders"></a><span data-ttu-id="a08a7-136">Siparişleri yönetme</span><span class="sxs-lookup"><span data-stu-id="a08a7-136">Manage orders</span></span>

* <span data-ttu-id="a08a7-137">[Abonelik Kaynakları](subscription-resources.md) – Yeni özellik eklendi.</span><span class="sxs-lookup"><span data-stu-id="a08a7-137">[Subscription Resources](subscription-resources.md) – New property added.</span></span> 
  * <span data-ttu-id="a08a7-138">CancellationAllowedUntilDate - (Yalnızca NCE için geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="a08a7-138">CancellationAllowedUntilDate  - (Only applicable to NCE)</span></span>

* <span data-ttu-id="a08a7-139">Geçiş Kaynakları (Yalnızca NCE için geçerlidir) – Yeni özellik eklendi</span><span class="sxs-lookup"><span data-stu-id="a08a7-139">Transition Resources (Only applicable to NCE) – New property added</span></span> 
  * <span data-ttu-id="a08a7-140">FromSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a08a7-140">FromSubscriptionId</span></span>

### <a name="manage-customer-accounts"></a><span data-ttu-id="a08a7-141">Müşteri hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="a08a7-141">Manage customer accounts</span></span>

* <span data-ttu-id="a08a7-142">[Adresi doğrulama](validate-an-address.md) – Yanıt Boolean'dan API için yeni bir modele değiştirilir:</span><span class="sxs-lookup"><span data-stu-id="a08a7-142">[Validate an address](validate-an-address.md) – Response is changed from a Boolean to a new model for API:</span></span>
  * `POST /validations/address`
  
  <span data-ttu-id="a08a7-143">Yeni yanıt modeli:</span><span class="sxs-lookup"><span data-stu-id="a08a7-143">New response model:</span></span> 
  * <span data-ttu-id="a08a7-144">AddressValidationResponse</span><span class="sxs-lookup"><span data-stu-id="a08a7-144">AddressValidationResponse</span></span>

* <span data-ttu-id="a08a7-145">Müşterinin nitele zaman uyumlu API'si kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="a08a7-145">Customer’s qualification synchronous API is deprecated.</span></span>  


## <a name="version-1170"></a><span data-ttu-id="a08a7-146">Sürüm 1.17.0</span><span class="sxs-lookup"><span data-stu-id="a08a7-146">Version 1.17.0</span></span>

<span data-ttu-id="a08a7-147">[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 genel kullanılabilirlik özelliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="a08a7-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="a08a7-148">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a08a7-149">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="a08a7-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="a08a7-150">Denetim Güncelleştirildi - Müşterinin DAP'ı ne zaman onayla ve sonlandırdı olduğunu bilmek için yeni işlem türleri eklendi</span><span class="sxs-lookup"><span data-stu-id="a08a7-150">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="a08a7-151">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="a08a7-151">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="a08a7-152">DapAdminRelationshipTerminated</span><span class="sxs-lookup"><span data-stu-id="a08a7-152">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="a08a7-153">Denetim Güncelleştirildi – Müşteri dizini rolü senaryosunu desteklemek için yeni kaynak ve işlem türleri eklendi</span><span class="sxs-lookup"><span data-stu-id="a08a7-153">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="a08a7-154">Kaynak türü : "[CustomerDirectoryRole](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="a08a7-154">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="a08a7-155">İşlem türleri : "[AddUserMember](auditing-resources.md)" ve "[RemoveUserMember](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="a08a7-155">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="a08a7-156">Müşteri Hesabında SDK Güncelleştirmeleri - Aşağıdaki API'ler için destek</span><span class="sxs-lookup"><span data-stu-id="a08a7-156">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="a08a7-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="a08a7-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="a08a7-158">GET /customers/{customer-tenant-id}/qualifications</span><span class="sxs-lookup"><span data-stu-id="a08a7-158">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="a08a7-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span><span class="sxs-lookup"><span data-stu-id="a08a7-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="a08a7-160">**Şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortaklarının daveti temel alarak kullanılabilen Yeni Ticaret kapsamında yapılan değişikliklerden sonra.**</span><span class="sxs-lookup"><span data-stu-id="a08a7-160">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="a08a7-161">Yeni ticari özel önizleme kapsamında yer alan iş ortakları, etkileri fark etmez ve geriye dönük uyumlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a08a7-161">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="a08a7-162">Katalog Değişiklikleri:</span><span class="sxs-lookup"><span data-stu-id="a08a7-162">Catalog Changes:</span></span>
    * <span data-ttu-id="a08a7-163">GET /products/{product-id}/skus/{sku-id}</span><span class="sxs-lookup"><span data-stu-id="a08a7-163">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="a08a7-164">Satın Alma ve Yönetme:</span><span class="sxs-lookup"><span data-stu-id="a08a7-164">Purchase and Manage:</span></span>
    * <span data-ttu-id="a08a7-165">GET /customers/{customerId}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="a08a7-165">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="a08a7-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="a08a7-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="a08a7-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="a08a7-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="a08a7-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span><span class="sxs-lookup"><span data-stu-id="a08a7-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="a08a7-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="a08a7-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="a08a7-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="a08a7-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="a08a7-171">Sürüm 1.16.3</span><span class="sxs-lookup"><span data-stu-id="a08a7-171">Version 1.16.3</span></span>

<span data-ttu-id="a08a7-172">[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 artık genel kullanılabilirlik özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-172">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="a08a7-173">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-173">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a08a7-174">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="a08a7-174">The following changes are included in this version:</span></span>

* <span data-ttu-id="a08a7-175">SelfServePolicies - yeni işlevsellik eklendi</span><span class="sxs-lookup"><span data-stu-id="a08a7-175">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="a08a7-176">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a08a7-176">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="a08a7-177">GetListOfSelfServicePolicies</span><span class="sxs-lookup"><span data-stu-id="a08a7-177">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="a08a7-178">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a08a7-178">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="a08a7-179">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a08a7-179">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="a08a7-180">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a08a7-180">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="a08a7-181">Müşteriler Şirket Profili</span><span class="sxs-lookup"><span data-stu-id="a08a7-181">Customers Company Profile</span></span>
  * <span data-ttu-id="a08a7-182">[OrganizationRegistrationNumber eklendi](create-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="a08a7-182">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="a08a7-183">CustomerBillingProfile.DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="a08a7-183">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="a08a7-184">MiddleName eklendi</span><span class="sxs-lookup"><span data-stu-id="a08a7-184">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="a08a7-185">Sürüm 1.16.2</span><span class="sxs-lookup"><span data-stu-id="a08a7-185">Version 1.16.2</span></span>

<span data-ttu-id="a08a7-186">[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 genel kullanılabilirlik özelliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="a08a7-186">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="a08a7-187">Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-187">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a08a7-188">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="a08a7-188">The following changes are included in this version:</span></span>

* <span data-ttu-id="a08a7-189">Denetim Kaydı için desteklenen işlem türlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a08a7-189">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="a08a7-190">Yeni eklenenler:</span><span class="sxs-lookup"><span data-stu-id="a08a7-190">The newly added ones are:</span></span>
  * <span data-ttu-id="a08a7-191">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a08a7-191">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="a08a7-192">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a08a7-192">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="a08a7-193">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a08a7-193">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="a08a7-194">RemovePartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="a08a7-194">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="a08a7-195">DeleteTipCustomer</span><span class="sxs-lookup"><span data-stu-id="a08a7-195">DeleteTipCustomer</span></span>
  * <span data-ttu-id="a08a7-196">CreateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="a08a7-196">CreateRelatedReferral</span></span>
  * <span data-ttu-id="a08a7-197">UpdateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="a08a7-197">UpdateRelatedReferral</span></span>

* <span data-ttu-id="a08a7-198">Hizmet isteği oluşturma artık kullanım dışı</span><span class="sxs-lookup"><span data-stu-id="a08a7-198">Service request creation is now deprecated</span></span>
* <span data-ttu-id="a08a7-199">Destek konuları artık kullanım dışıdır</span><span class="sxs-lookup"><span data-stu-id="a08a7-199">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="a08a7-200">Sürüm 1.16.1</span><span class="sxs-lookup"><span data-stu-id="a08a7-200">Version 1.16.1</span></span>

<span data-ttu-id="a08a7-201">[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 artık genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a08a7-201">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="a08a7-202">güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="a08a7-202">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a08a7-203">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="a08a7-203">The following changes are included in this version:</span></span>

<span data-ttu-id="a08a7-204">mevcut Microsoft iş ortağı merkezi SDK 'sını .NET Framework 'den .NET Standard 2,0 platformuna geçirdik.</span><span class="sxs-lookup"><span data-stu-id="a08a7-204">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="a08a7-205">bu, SDK 'nın .NET Framework 4.6.1 ve üstünü kullanarak var olan uygulamalarla uyumlu hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-205">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="a08a7-206">SDK, .NET Core 2,0 ve üstünü destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-206">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="a08a7-207">Mevcut uygulamalara geçmeden önce [.NET uygulama desteğini](/dotnet/standard/net-standard) kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a08a7-207">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="a08a7-208">Sürüm 1.15.3</span><span class="sxs-lookup"><span data-stu-id="a08a7-208">Version 1.15.3</span></span>
<span data-ttu-id="a08a7-209">[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 artık genel kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a08a7-209">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="a08a7-210">güncelleştirilmiş REST apı 'leri ve [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="a08a7-210">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a08a7-211">Bu sürüme aşağıdaki değişiklikler dahildir:</span><span class="sxs-lookup"><span data-stu-id="a08a7-211">The following changes are included in this version:</span></span>

* <span data-ttu-id="a08a7-212">İş ortağı sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="a08a7-212">Partner Agreement</span></span>
  * <span data-ttu-id="a08a7-213">Dolaylı sağlayıcıların, [dolaylı satıcıların Microsoft Iş ortağı sözleşmesi durumunu doğrulama](verify-indirect-reseller-mpa-status.md)özelliği eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="a08a7-213">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="a08a7-214">Ürünler</span><span class="sxs-lookup"><span data-stu-id="a08a7-214">Products</span></span>
  * <span data-ttu-id="a08a7-215">Aşağıdaki iki arabirim Microsoft. Store. PartnerCenter. Products ad alanı altına yanlış yerleştirildi.</span><span class="sxs-lookup"><span data-stu-id="a08a7-215">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="a08a7-216">Şimdi, Microsoft. Store. PartnerCenter. Customers. Products ad alanı altında bulunur.</span><span class="sxs-lookup"><span data-stu-id="a08a7-216">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="a08a7-217">Icustomerproductbyrezervationscope</span><span class="sxs-lookup"><span data-stu-id="a08a7-217">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="a08a7-218">Icustomerskubyırezervationscope</span><span class="sxs-lookup"><span data-stu-id="a08a7-218">ICustomerSkuByReservationScope</span></span>
