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
# <a name="net-sdk-release-notes"></a>.NET SDK sürüm notları

Aşağıdaki sürüm notları, [Microsoft Iş ortağı merkezi .NET SDK 'sının](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)yeni sürümlerinde kullanılabilir. GitHub 'da [.NET SDK örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) bulabilirsiniz. .NET API tarayıcısında [Iş ortağı merkezi .NET API başvurusunu](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) bulabilirsiniz.

## <a name="version-1170"></a>Sürüm 1.17.0

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v 1.17.0 artık genel kullanıma sunulmuştur. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

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

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v 1.16.3 artık genel kullanıma sunulmuştur. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

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

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 artık genel kullanıma sunulmuştur. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

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

[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 artık genel kullanıma sunulmuştur. Güncelleştirilmiş [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

Mevcut Microsoft Iş Ortağı Merkezi SDK 'sını .NET Framework 'den .NET Standard 2,0 platformuna geçirdik. Bu, SDK 'nın .NET Framework 4.6.1 ve üstünü kullanarak var olan uygulamalarla uyumlu hale getirir. SDK, .NET Core 2,0 ve üstünü destekleyecektir. Mevcut uygulamalara geçmeden önce [.NET uygulama desteğini](/dotnet/standard/net-standard) kontrol edin.   


## <a name="version-1153"></a>Sürüm 1.15.3
[Microsoft Iş ortağı merkezi .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 artık genel kullanıma sunulmuştur. Güncelleştirilmiş REST API 'Leri ve [GitHub örnekleri](https://github.com/Microsoft/Partner-Center-DotNet-Samples) de mevcuttur. Bu sürüme aşağıdaki değişiklikler dahildir:

* İş ortağı sözleşmesi
  * Dolaylı sağlayıcıların, [dolaylı satıcıların Microsoft Iş ortağı sözleşmesi durumunu doğrulama](verify-indirect-reseller-mpa-status.md)özelliği eklenmiştir.
* Ürünler
  * Aşağıdaki iki arabirim Microsoft. Store. PartnerCenter. Products ad alanı altına yanlış yerleştirildi. Şimdi, Microsoft. Store. PartnerCenter. Customers. Products ad alanı altında bulunur.
    * Icustomerproductbyrezervationscope
    * Icustomerskubyırezervationscope
