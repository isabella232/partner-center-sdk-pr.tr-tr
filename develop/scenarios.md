---
title: İş Ortağı Merkezi API senaryoları
description: Bulut çözümü sağlayıcısı program iş ortaklarının, müşteri hesaplarını, siparişleri, desteği ve faturalandırmayı programlı bir şekilde yönetmek için Iş Ortağı Merkezi API 'sini nasıl kullanabileceğinizi öğrenin.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14dbd501e3d075c3880fae6f362feef797cba133
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769958"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>Müşteri hesaplarını programlı bir şekilde yönetmenize olanak sağlayan iş ortağı merkezi API senaryoları

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, bulut çözümü sağlayıcısı programındaki iş ortaklarının bazıları, aşağıdaki gibi alanlarda programlı bir şekilde yönetim sağlamak için Iş Ortağı Merkezi API 'sini kullanabilir.

- Müşteri hesapları
- Siparişler
- Abonelikler
- Destek
- Faturalandırma

Farklı yetenekler içeren farklı Iş ortağı merkezi sürümleri mevcuttur. Tüm senaryolar Iş Ortağı Merkezi sürümlerinde desteklenmez. Daha fazla bilgi için bkz. [Microsoft Ulusal bulut Için Iş Ortağı Merkezi Için geliştirme](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>Iş Ortağı Merkezi SDK 'Sı tarafından desteklenen senaryolar

Aşağıdaki senaryoların hepsi üç farklı şekilde tamamlanabilir:

- [Iş Ortağı Merkezi](https://partner.microsoft.com/dashboard) panosunda el ile.

- Program aracılığıyla Iş Ortağı Merkezi tarafından yönetilen API 'YI kullanma.

- Program aracılığıyla Iş Ortağı Merkezi REST API.

| Desteklenen bu senaryolar hakkında bilgi edinmek için:  | Şu kaynağa bakın:     |
|----------------------------------|--------------------------|
| **Analiz:** Azure kullanımı, abonelikleri, lisansları veya başvurularıyla ilgili analiz verilerini almayı öğrenin.         | [Analiz](usage-analytics.md)  |
| **Denetim işlemleri:** Iş Ortağı Merkezi etkinliğinin ve işlemlerinin geçmiş denetim kayıtlarını almayı öğrenin. | [İşlemleri denetleme](audit.md)                     |
| **Cihaz dağıtımları:** Cihaz yapılandırma ilkeleri, cihaz toplu işlemleriyle çalışma ve cihaz meta verileri hakkında bilgi edinin. Bu senaryolar cihaz yapılandırma ilkelerini ekleme, silme, güncelleştirme ve almayı içerir.    | [Cihaz dağıtıma](device-deployment.md)  |
| **Hesaplar ve profiller:** İş ortağı faturalandırma profillerinin, yasal profillerin, MPN profilinin, iş profillerinin veya destek profillerinin nasıl alınacağını veya güncelleyeceğinizi öğrenin. Müşterilerin veya dolaylı satıcıların bir listesini de alabilirsiniz. | [Hesapları ve profilleri yönetme](manage-profiles-and-information.md)                                                                        |
| **Faturalandırma:** Fatura döngüsünü değiştirme, Azure fiyatları ve Azure kullanım kayıtları alma, faturaları alma, ortağın geçerli hesap bakiyesini alma veya müşteri hizmetleri maliyetlerini alma gibi alanlarla ilgili bilgi edinin.  | [Faturalandırmayı yönetme](manage-billing.md)   |
| **Azure harcama:** Azure harcama ve iş ortağı kullanımı, müşteri aboneliklerinin kullanımı, tarifeli kullanım ve müşteri kullanım bütçeleri hakkında bilgi alın. Senaryolar Ayrıca bir müşteri kullanım bütçesini güncelleştirme de içerir. | [Azure harcaması](azure-spending.md)  |
| **Müşteri hesaplarını yönetme:** Müşteri hesabı yönetiminin, müşteri hesaplarını veya müşterinin Kullanıcı hesaplarını oluşturma ve silme, müşteri hesabı ayrıntılarını yönetme ve doğrulama, Kullanıcı hesaplarını yönetme ve lisans atama gibi birçok yönden nasıl yapılacağını öğrenin.  | [Müşterileri yönetme](manage-customers.md)  |
| **Siparişleri yönetme:** Müşteri siparişlerini ve abonelikleri programlı bir şekilde yönetebilmeniz için tüm yolları öğrenin. Bu alan Azure ayırmaları satın alma, sipariş oluşturma, katalogdan teklif alma ve deneme dönüştürme tekliflerini yönetme işlemlerini içerir.   | [Siparişleri yönetme](manage-orders.md)  |
| **Destek sağlama:** Bir müşteri için Hizmetleri yönetmeyi, bir aboneliğe yönelik destek kişilerini alma veya güncelleştirme ve hizmet isteklerini yönetme hakkında bilgi edinin.  | [Destek sağlama](provide-support.md)   |
| **Başvurular:** Başvuru oluşturmayı, başvuruların bir listesini almayı veya bir başvuruyu güncelleştirmeyi öğrenin.  | [Referanslar](/partner/develop/referrals)  |
| **Yardımcı programlar:** Bir adresin nasıl doğrulandığını, pazara göre adres biçimlendirme kuralları alma, etki alanı kullanılabilirliğini doğrulama, tümleştirme korumalı alanından bir müşteri hesabını silme veya Iş Ortağı Merkezi etkinliğinin kaydını alma hakkında bilgi edinin. | [Yardımcı Programlar](utilities.md)  |
| **Güvenlik:** Iş Ortağı Merkezi 'nde Multi-Factor Authentication (MFA) ile ilgili REST API 'Leri hakkında bilgi edinin. Bu API 'Ler, iş ortağı kiracınızdaki her kullanıcı hesabı için MFA 'yı zorlamanıza yardımcı olur.  | [İş ortağı güvenlik gereksinimlerinin durumu](partner-security-requirements.md)  |

## <a name="next-steps"></a>Sonraki adımlar

- [Iş Ortağı Merkezi örneklerine bakın](partner-center-samples.md)
- [Kullanmaya başlama hakkında bilgi edinin](get-started.md)