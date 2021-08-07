---
title: Konsol test uygulaması
description: Bu konsol test uygulaması, uygulama api'leri tarafından desteklenen tüm senaryolar için İş Ortağı Merkezi sağlar. Test için de kullanabilirsiniz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 53a014608303e432be251de0845857547170a5464a1952bb4fde9ff7beb8ae95
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991965"
---
# <a name="console-test-app"></a>Konsol test uygulaması

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Konsol test uygulaması C# ve Java ile sağlanmıştır ve uygulama api'leri tarafından desteklenen tüm senaryolar için İş Ortağı Merkezi sağlar. Test için de kullanabilirsiniz.

## <a name="get-the-code"></a>Kodu alma

Konsol test uygulaması için örnek kodu indirin.

## <a name="net"></a>.NET

[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=746682) ve gerekli şekilde değiştirin.

> [!IMPORTANT]
> Uygulamayı derlemeden önce,App.configdosyasındaki değerleri, kimlik doğrulamasında oluşturduğunuz Azure AD kimlik doğrulaması [bilgilerini İş Ortağı Merkezi güncelleştirin.](partner-center-authentication.md)  Özellikle, erken geliştirme sırasında veya üretimde test etmek için tümleştirme korumalı alan hesabı ayarlarınızı kullansanız iyi olur.

App.config *dosyasındaki* **ScenarioSettings** altında, çalıştırdınız senaryolara otomatik olarak geçirilir parametreleri ayarlayın.

Çalıştırilen senaryoların listesini değiştirmek için **IPartnerScenario \[ \] mainScenarios** veya *Program.cs* dosyasında bulunan tek bir **Senaryo Al** yönteminde satırları açıklama satırı olarak ekleyin.

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=2026887) ve gerekli şekilde değiştirin.

> [!IMPORTANT]
> Uygulamayı derlemeden önce, dosyada yer *alanSamplesConfigurations.js,* kimlik doğrulamasında oluşturduğunuz Azure AD kimlik doğrulama bilgilerini [yansıtacak İş Ortağı Merkezi güncelleştirin.](partner-center-authentication.md) Özellikle, erken geliştirme sırasında veya üretimde test etmek için tümleştirme korumalı alan hesabı ayarlarınızı kullansanız iyi olur.

Dosyanın dosya *SamplesConfiguration.js* **ScenarioSettings** altında, çalıştırdınız senaryolara otomatik olarak geçirilir parametreleri ayarlayın.

Çalıştırilen senaryoların listesini değiştirmek için **IPartnerScenario \[ \] mainScenarios** veya *Program.java* dosyasında bulunan tek bir **Senaryo Al** yönteminde satırları açıklama satırı olarak ekleyin.

## <a name="what-to-change"></a>Nelerin değişmesi gerekenler

Örnek kodda neyi değiştireceklerini veya değiştirmeyeceklerini belirlemek için aşağıdaki listeleri kullanın.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

**PartnerServiceSettings** için şunları değiştirme:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Örnek API çağrılarının düzgün çalışması için bu ayarların hepsi gereklidir.

### <a name="userauthentication"></a>UserAuthentication

**UserAuthentication** için şunları değiştirmelisiniz:

- **ApplicationId** (oturum Azure Active Directory kullanılan uygulama kimliğiniz)
- **UserName** (active directory kullanıcı adınız)
- **Parola** (active directory parolanız).

Şunları değiştirme:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

**AppAuthentication** için şunları değiştirmelisiniz:

- **ApplicationId** (uygulama oturum açma için kullanılan Active Directory uygulama kimliğiniz)
- **ApplicationSecret** (uygulama oturum açma için kullanılan Active Directory uygulama gizli dizininiz)
- **Etki** alanı (uygulamanın barındırıldı olduğu Active Directory etki alanınız)

### <a name="scenariosettings"></a>ScenarioSettings

**ScenarioSettings** için, şunları değiştirme:

- **CustomerDomainSuffix** (yeni müşteri oluştururken kullanılan etki alanı soneki)

İsteğe bağlı ayarlar. Boş bırakılırsa, gerektiğinde bir senaryo çalıştırılabilirken bu bilgilerin gir olması gerekir:

- **CustomerIdToDelete** (silme için kullanılan müşterinin kimliği)
- **DefaultCustomerId** (müşteriyle ilgili senaryolarda kullanmak için müşteri kimliği)
- **DefaultInvoiceID** (fatura senaryolarında kullanmak için fatura kimliği)
- **PartnerMpnId** (dolaylı iş ortağı senaryolarında kullanmak için iş ortağı MPN kimliği)
- **DefaultServiceRequestId** (hizmet isteği senaryolarında kullanmak için hizmet isteği kimliği)
- **DefaultSupportTopicID** (hizmet isteği senaryolarında kullanmak için destek konusu kimliği)
- **DefaultOfferID** (teklif senaryolarında kullanmak için teklif kimliği)
- **DefaultOrderID** (sipariş senaryolarında kullanmak için sipariş kimliği)
- **DefaultSubscriptionID** (abonelik senaryolarında kullanmak için abonelik kimliği)

Değiştirmek için isteğe bağlı. Bu ayarların hepsi, sayfalamalı içerik alınırken sayfa başına giriş miktarını belirtir:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
