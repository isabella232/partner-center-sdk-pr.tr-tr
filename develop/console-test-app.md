---
title: Konsol test uygulaması
description: Bu konsol test uygulaması, Iş Ortağı Merkezi API 'Leri tarafından desteklenen tüm senaryolar için örnek kod sağlar. Test etmek için de kullanabilirsiniz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769179"
---
# <a name="console-test-app"></a>Konsol test uygulaması

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Konsol test uygulaması C# ve Java 'da sağlanır, Iş Ortağı Merkezi API 'Leri tarafından desteklenen tüm senaryolar için örnek kodlar sağlar. Test etmek için de kullanabilirsiniz.

## <a name="get-the-code"></a>Kodu alma

Konsol test uygulaması için örnek kodu indirin.

## <a name="net"></a>.NET

[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=746682) ve gereken şekilde değiştirin.

> [!IMPORTANT]
> Uygulamayı oluşturmadan önce, *App.config* dosyadaki değerleri, [iş ortağı merkezi kimlik doğrulaması](partner-center-authentication.md)' nda oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtacak şekilde güncelleştirin. Özellikle, tümleştirme korumalı alanı hesap ayarlarınızı erken geliştirme sırasında veya üretimde test etmek için kullanmanız gerekir.

*App.config* dosyasında **ScenarioSettings** altında, çalıştırdığınız senaryolara otomatik olarak geçirilecek parametreleri ayarlayabilirsiniz.

Çalıştırılan senaryoların listesini değiştirmek için, **ıpartnerscenario \[ \] mainsenaryolarında** ya da *program.cs* dosyasında bulunan tek bir **Get senaryolar** yönteminde bulunan satırları açıklama satırı yapın.

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=2026887) ve gereken şekilde değiştirin.

> [!IMPORTANT]
> Uygulamayı oluşturmadan önce, dosyadaki *SamplesConfigurations.js* , [iş ortağı merkezi kimlik DOĞRULAMASıNDA](partner-center-authentication.md)oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtacak şekilde güncelleştirin. Özellikle, tümleştirme korumalı alanı hesap ayarlarınızı erken geliştirme sırasında veya üretimde test etmek için kullanmanız gerekir.

*SamplesConfiguration.js* dosyadaki **ScenarioSettings** altında, çalıştırdığınız senaryolara otomatik olarak geçirilecek parametreleri ayarlayabilirsiniz.

Çalıştırılan senaryoların listesini değiştirmek için, **ıpartnerscenario \[ \] Mainsenaryolarında** ya da *program. Java* dosyasında bulunan tek bir **Get senaryolar** yönteminde bulunan satırları açıklama satırı yapın.

## <a name="what-to-change"></a>Ne değiştirilebilir

Örnek kodda nelerin değişiklik yapılacağını veya değişdiklerinizi belirlemek için aşağıdaki listeleri kullanın.

### <a name="partnerservicesettings"></a>Partnerservice ayarları

**Partnerservicesettings** için şu değişikliği yapmayın:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Bu ayarların tümü, örnek API çağrılarının düzgün çalışması için gereklidir.

### <a name="userauthentication"></a>UserAuthentication

**Userauthentication** için şunları değiştirmeniz gerekir:

- **ApplicationId** (Azure Active Directory oturum açma için kullanılan uygulama kimliği)
- **Kullanıcı adı** (Active Directory Kullanıcı adınız)
- **Parola** (Active Directory parolanız).

Değiştirme:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

**Appauthentication** için şunları değiştirmeniz gerekir:

- **ApplicationId** (uygulama oturum açması için kullanılan Active DIRECTORY uygulama kimliğiniz)
- **Applicationsecret** (uygulama oturum açması için kullanılan Active Directory uygulama gizli anahtarı)
- **Etki alanı** (uygulamanın barındırıldığı Active Directory etki alanı)

### <a name="scenariosettings"></a>ScenarioSettings

**ScenarioSettings** için şunu değiştirmeyin:

- **Customerdomainsuffix** (yeni müşteri oluşturulurken kullanılan etki alanı soneki)

İsteğe bağlı ayarlar. Boş bırakılırsa, gereken yerde bir senaryo çalıştırılırken bu bilgilerin oluşturulması gerekir):

- **Customerıdtodelete** (silinmek üzere kullanılan müşterinin kimliği)
- **Defaultcustomerıd** (müşteriyle ilgili senaryolarda kullanılacak müşteri kimliği)
- **Defaultınvoiceıd** (fatura senaryolarında kullanılacak fatura kimliği)
- **Partnermpnıd** (dolaylı iş ortağı senaryolarında kullanılacak iş ortağı MPN kimliği)
- **DefaultServiceRequestId** (hizmet isteği senaryolarında kullanılacak HIZMET isteği kimliği)
- **Defaultsupporttopicıd** (hizmet isteği senaryolarında kullanılacak destek konusu kimliği)
- **Defaultofferıd** (teklif senaryolarında kullanılacak teklif kimliği)
- **DefaultOrderID** (sipariş senaryolarında kullanılacak sıra kimliği)
- **Defaultsubscriptionıd** (abonelik senaryolarında kullanılacak abonelik kimliği)

Değişiklik için isteğe bağlı. Bu ayarların tümü, disk belleği içeriğini alırken sayfa başına giriş miktarını belirtir:

- **CustomerPageSize**
- **Invoicepagesize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
