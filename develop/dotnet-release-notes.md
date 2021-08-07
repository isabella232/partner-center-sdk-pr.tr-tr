---
title: İş Ortağı Merkezi .NET SDK sürüm notları
description: Iş ortağı merkezi .NET SDK 'sının en son sürümü için sürüm notları.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6fc6182638cb2cc5457bdfada37b928c88e1ca786e401f7eb8d5309a0abd9310
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991233"
---
# <a name="net-sdk-release-notes"></a>.NET SDK sürüm notları

Aşağıdaki sürüm notları, [Microsoft Iş ortağı merkezi .NET SDK 'sının](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)yeni sürümlerinde kullanılabilir. GitHub için [.NET SDK örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) bulabilirsiniz. .NET API tarayıcısında [Iş ortağı merkezi .NET API başvurusunu](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) bulabilirsiniz.

## <a name="version-201"></a>Sürüm 2.0.1

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v 2.0.1 artık genel kullanıma sunulmuştur. güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

> [!NOTE]
> Yeni ticari deneyimler ("NCE") kapsamında tanıtılan bazı değişiklikler, yalnızca M365/D365 yeni ticaret deneyimi Technical Preview 'ın parçası olan iş ortakları için davet temel alınarak kullanılabilir. Yeni ticaret özel önizlemesinin parçası olmayan iş ortakları, etkileri fark etmez ve geriye dönük olarak uyumlu olmalıdır.

### <a name="common"></a>Common
* kimlik doğrulama kitaplığı başvurusunda değişiklik – başvuru, Azure Active Directory kimlik doğrulaması kitaplığı ([ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)) ile Microsoft kimlik doğrulama kitaplığı ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)) olarak değiştirilir

  MSAL uygulamasının uygulamanızda veya .NET örneğinde düzgün çalışmasını sağlamak için aşağıdaki değişiklikler yapılmalıdır:

  * `https://login.microsoftonline.com/common/oauth2/nativeclient`Mobil ve Masaüstü uygulamaları Için RedirectUrl olarak ekleyin
  * Uygulama yapılandırma dosyanızdaki UserAuthentication bölümüne **etki alanı** ekleyin. 

    etki alanı, Azure AD uygulamasının oluşturulduğu Azure Active Directory etki alanı veya kiracı kimliğidir

* [Hata kodları](error-codes.md) – yeni hata kodu eklendi 
  * 408: istek zaman aşımı
  * 504: ağ geçidi zaman aşımı 

### <a name="manage-billing"></a>Faturalandırmayı yönetme

* [Fatura satırı-öğeler](get-invoiceline-items.md) -aşağıdaki API 'lere eklenen yeni öznitelikler:
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  Yeni öznitelikler: 
  * Productniteleyiciler
  * subscriptionStartDate
  * subscriptionEndDate
  * Referenceıd
  * creditReasonCode (yalnızca NCE için geçerlidir)
  * Promotionıd 


* [Günlük dereceli kullanım satırı-öğeler](get-invoice-billed-consumption-lineitems.md) – aşağıdaki API 'ye eklenen yeni öznitelikler: 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  Yeni öznitelikler: 
  * Haspartnerearnedkredisi (yalnızca NCE için geçerlidir)
  * creditType (yalnızca NCE için geçerlidir)
  * Rateofkredisi (yalnızca NCE için geçerlidir)


### <a name="manage-orders"></a>Siparişleri yönetme

* [Abonelik kaynakları](subscription-resources.md) – yeni özellik eklendi. 
  * CancellationAllowedUntilDate-(yalnızca NCE için geçerlidir)

* Geçiş kaynakları (yalnızca NCE için geçerlidir) – yeni özellik eklendi 
  * Fromsubscriptionıd

### <a name="manage-customer-accounts"></a>Müşteri hesaplarını yönetme

* [Adresi doğrulama](validate-an-address.md) – yanıt, Boole değerinden API için yeni bir modele değiştirilir:
  * `POST /validations/address`
  
  Yeni yanıt modeli: 
  * AddressValidationResponse

* Müşterinin nitelik zaman uyumlu API 'SI kullanım dışıdır.  


## <a name="version-1170"></a>Sürüm 1.17.0

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v 1.17.0 artık genel kullanıma sunulmuştur. güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

* Denetim güncelleştirildi-müşterinin ne zaman onayladığı ve sonlandırıldığı hakkında yeni işlem türleri eklendi
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [Dapadminrelationshipsonlandırılan](auditing-resources.md)

* Denetim güncelleştirildi – müşteri dizin rolü senaryosunu desteklemek için yeni kaynak ve işlem türleri eklendi
  * Kaynak türü "[Customerdirectoryrole](auditing-resources.md)"
  * "[Addusermember](auditing-resources.md)" ve "[removeusermember](auditing-resources.md)" işlem türleri

* Müşteriler için SDK güncelleştirmeleri hesabı-aşağıdaki API 'leri destekler
  * /Customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus al
  * /Customers/{Customer-Tenant-ID}/nitelikler al 
  * /Customers/{customer_id}/nitelikler SONRASı? Code = {validationCode}

* **Şu anda, yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinin parçası olan iş ortakları için yapılan davet temelinde mevcut olan yeni ticaretin bir parçası olarak tanıtılan değişiklikler.** Yeni ticaret özel önizlemesinin parçası olmayan iş ortakları, etkileri fark etmez ve geriye dönük olarak uyumlu olmalıdır.
  * Katalog değişiklikleri:
    * /Products/{product-id}/SKUs/{SKU-id} al
  * Satın alın ve yönetin:
    * /Customers/{CustomerID}/abonelikleri al
    * /Customers/{CustomerID}/Subscriptions/{SubscriptionID} al
    * PATCH/Customers/{CustomerID}/Subscriptions/{SubscriptionID}
    * /Customers/{CustomerID}/Subscriptions/{SubscriptionID}/geçişli tioneligılıklara al
    * /Customers/{CustomerID}/Subscriptions/{SubscriptionID}/geçişlerini al
    * POST/Customers/{CustomerID}/Subscriptions/{SubscriptionID}/geçişlerin


## <a name="version-1163"></a>Sürüm 1.16.3

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v 1.16.3 artık genel kullanıma sunulmuştur. güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

* SelfServePolicies-yeni işlevsellik eklendi
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [Getlıfselfservicepolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Müşteriler şirket profili
  * [Organizationregistrationnumber](create-a-customer.md) eklendi

* CustomerBillingProfile. DefaultAddress
  * MiddleName eklendi

## <a name="version-1162"></a>Sürüm 1.16.2

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 artık genel kullanıma sunulmuştur. güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

* Denetim kaydı için desteklenen işlem türlerini güncelleştirin. Yeni eklenen olanlar şunlardır:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * Createrelatedbaşvurunun
  * Updaterelatedbaşvurunun

* Hizmet isteği oluşturma artık kullanım dışıdır
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
