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
# <a name="net-sdk-release-notes"></a>.NET SDK sürüm notları

Microsoft İş Ortağı Merkezi [.NET SDK'sı yeni](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)sürümleri için aşağıdaki sürüm notları kullanılabilir. [.NET SDK örneklerini GitHub.](https://github.com/Microsoft/Partner-Center-DotNet-Samples) [.NET API İş Ortağı Merkezi .NET API Browser'da](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) bulabilirsiniz.

## <a name="version-201"></a>Sürüm 2.0.1

[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 genel kullanılabilirlik özelliğine sahip. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir. Bu sürüme aşağıdaki değişiklikler dahildir:

> [!NOTE]
> Şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesinde yer alan iş ortaklarının daveti temel alınarak kullanılabilen Yeni Ticaret Deneyimleri ("NCE") kapsamında yapılan bazı değişiklikler. Yeni ticari özel önizleme kapsamında yer alan iş ortakları, etkileri fark etmez ve geriye dönük uyumlu olmalıdır.

### <a name="common"></a>Common
* Kimlik doğrulama kitaplığı başvurusunda değişiklik – Başvuru, Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)olan başvuru, Microsoft Kimlik Doğrulama Kitaplığı ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)) olarak değiştirildi

  MSAL'nin uygulamanıza veya .NET örneğinde doğru şekilde çalıştırılana kadar aşağıdaki değişiklikler gerçekleştirin:

  * Mobil `https://login.microsoftonline.com/common/oauth2/nativeclient` ve masaüstü uygulamaları için RedirectUrl olarak ekleme
  * Uygulama **yapılandırma** dosyanız içinde UserAuthentication bölümüne Etki Alanı ekleyin. 

    Etki alanı, Azure Active Directory Azure AD uygulamasının oluşturularak oluşturulan etki alanı veya kiracı kimliğidir

* [Hata kodları](error-codes.md) – Yeni hata kodu eklendi 
  * 408: İstek zaman aşımı
  * 504: Ağ geçidi zaman aşımı 

### <a name="manage-billing"></a>Faturalandırmayı yönetme

* [Fatura satırı öğeleri](get-invoiceline-items.md) - aşağıdaki API'lere yeni öznitelikler eklendi:
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  Yeni öznitelikler: 
  * productQualifiers
  * subscriptionStartDate
  * subscriptionEndDate
  * referenceId
  * creditReasonCode (Yalnızca NCE için geçerlidir)
  * promotionId 


* [Günlük olarak derecelendirilmiş kullanım Satır öğeleri](get-invoice-billed-consumption-lineitems.md) – aşağıdaki API'ye yeni öznitelikler eklendi: 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  Yeni öznitelikler: 
  * hasPartnerEarnedCredit (Yalnızca NCE için geçerlidir)
  * creditType (Yalnızca NCE için geçerlidir)
  * rateOfCredit (Yalnızca NCE için geçerlidir)


### <a name="manage-orders"></a>Siparişleri yönetme

* [Abonelik Kaynakları](subscription-resources.md) – Yeni özellik eklendi. 
  * CancellationAllowedUntilDate - (Yalnızca NCE için geçerlidir)

* Geçiş Kaynakları (Yalnızca NCE için geçerlidir) – Yeni özellik eklendi 
  * FromSubscriptionId

### <a name="manage-customer-accounts"></a>Müşteri hesaplarını yönetme

* [Adresi doğrulama](validate-an-address.md) – Yanıt Boolean'dan API için yeni bir modele değiştirilir:
  * `POST /validations/address`
  
  Yeni yanıt modeli: 
  * AddressValidationResponse

* Müşterinin nitele zaman uyumlu API'si kullanım dışıdır.  


## <a name="version-1170"></a>Sürüm 1.17.0

[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 genel kullanılabilirlik özelliğine sahip. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir. Bu sürüme aşağıdaki değişiklikler dahildir:

* Denetim Güncelleştirildi - Müşterinin DAP'ı ne zaman onayla ve sonlandırdı olduğunu bilmek için yeni işlem türleri eklendi
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Denetim Güncelleştirildi – Müşteri dizini rolü senaryosunu desteklemek için yeni kaynak ve işlem türleri eklendi
  * Kaynak türü : "[CustomerDirectoryRole](auditing-resources.md)"
  * İşlem türleri : "[AddUserMember](auditing-resources.md)" ve "[RemoveUserMember](auditing-resources.md)"

* Müşteri Hesabında SDK Güncelleştirmeleri - Aşağıdaki API'ler için destek
  * GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * GET /customers/{customer-tenant-id}/qualifications 
  * POST /customers/{customer_id}/qualifications?code={validationCode}

* **Şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortaklarının daveti temel alarak kullanılabilen Yeni Ticaret kapsamında yapılan değişikliklerden sonra.** Yeni ticari özel önizleme kapsamında yer alan iş ortakları, etkileri fark etmez ve geriye dönük uyumlu olmalıdır.
  * Katalog Değişiklikleri:
    * GET /products/{product-id}/skus/{sku-id}
  * Satın Alma ve Yönetme:
    * GET /customers/{customerId}/subscriptions
    * GET /customers/{customerId}/subscriptions/{subscriptionId}
    * PATCH /customers/{customerId}/subscriptions/{subscriptionId}
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions


## <a name="version-1163"></a>Sürüm 1.16.3

[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 artık genel kullanılabilirlik özelliğidir. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir. Bu sürüme aşağıdaki değişiklikler dahildir:

* SelfServePolicies - yeni işlevsellik eklendi
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Müşteriler Şirket Profili
  * [OrganizationRegistrationNumber eklendi](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * MiddleName eklendi

## <a name="version-1162"></a>Sürüm 1.16.2

[Microsoft İş Ortağı Merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 genel kullanılabilirlik özelliğine sahip. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de kullanılabilir. Bu sürüme aşağıdaki değişiklikler dahildir:

* Denetim Kaydı için desteklenen işlem türlerini güncelleştirin. Yeni eklenenler:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Hizmet isteği oluşturma artık kullanım dışı
* Destek konuları artık kullanım dışıdır


## <a name="version-1161"></a>Sürüm 1.16.1

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 artık genel kullanıma sunulmuştur. güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

mevcut Microsoft iş ortağı merkezi SDK 'sını .NET Framework 'den .NET Standard 2,0 platformuna geçirdik. bu, SDK 'nın .NET Framework 4.6.1 ve üstünü kullanarak var olan uygulamalarla uyumlu hale getirir. SDK, .NET Core 2,0 ve üstünü destekleyecektir. Mevcut uygulamalara geçmeden önce [.NET uygulama desteğini](/dotnet/standard/net-standard) kontrol edin.   


## <a name="version-1153"></a>Sürüm 1.15.3
[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 artık genel kullanıma sunulmuştur. güncelleştirilmiş REST apı 'leri ve [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

* İş ortağı sözleşmesi
  * Dolaylı sağlayıcıların, [dolaylı satıcıların Microsoft Iş ortağı sözleşmesi durumunu doğrulama](verify-indirect-reseller-mpa-status.md)özelliği eklenmiştir.
* Ürünler
  * Aşağıdaki iki arabirim Microsoft. Store. PartnerCenter. Products ad alanı altına yanlış yerleştirildi. Şimdi, Microsoft. Store. PartnerCenter. Customers. Products ad alanı altında bulunur.
    * Icustomerproductbyrezervationscope
    * Icustomerskubyırezervationscope
