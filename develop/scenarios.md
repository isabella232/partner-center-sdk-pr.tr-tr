---
title: İş Ortağı Merkezi API senaryoları
description: Program iş Bulut Çözümü Sağlayıcısı müşteri hesaplarını, siparişleri, İş Ortağı Merkezi ve faturalamayı program aracılığıyla yönetmek için İş Ortağı Merkezi API'sini nasıl kullanabileceğini öğrenin.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d74400a975323d5f0f276dbdece3621d8b47a609
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547487"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>İş Ortağı Merkezi hesaplarını program aracılığıyla yönetmenizi sağlar

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | Orta Microsoft Cloud for US Government

Bu makalede, Bulut Çözümü Sağlayıcısı programı iş ortaklarının İş Ortağı Merkezi API'sini kullanarak aşağıdaki gibi alanları yönettikleri açıklanmıştır:

- Müşteri hesapları
- Siparişler
- Abonelikler
- Destek
- Faturalandırma

Farklı özellikler içeren İş Ortağı Merkezi sürümleri vardır. Tüm senaryolar tüm sürümlerde İş Ortağı Merkezi. Daha fazla bilgi edinmek için [bkz. Microsoft Ulusal İş Ortağı Merkezi için geliştirme.](developing-for-partner-center-for-microsoft-national-cloud.md)

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>İş Ortağı Merkezi SDK'sı tarafından desteklenen senaryolar

Aşağıdaki senaryoların hepsi üç farklı şekilde tamamlanır:

- Panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)

- Yönetilen API'yi İş Ortağı Merkezi kullanarak.

- Program aracılığıyla İş Ortağı Merkezi REST API.

| Bu desteklenen senaryolar hakkında bilgi edinmek için:  | Şu kaynağa bakın:     |
|----------------------------------|--------------------------|
| **Analiz:** Azure kullanımı, abonelikler, lisanslar veya referanslar hakkında analiz verilerini alma hakkında bilgi edinin.         | [Analiz](usage-analytics.md)  |
| **Denetim işlemleri:** Etkinlik ve işlemlerin geçmiş denetim kayıtlarını İş Ortağı Merkezi öğrenin. | [İşlemleri denetleme](audit.md)                     |
| **Cihaz dağıtımları:** Cihaz yapılandırma ilkeleri, cihaz toplu işleri ve cihaz meta verileri ile çalışma hakkında bilgi edinebilirsiniz. Bu senaryolar cihaz yapılandırma ilkeleri ekleme, silme, güncelleştirme ve alma senaryolarını içerir.    | [Cihaz dağıtıma](device-deployment.md)  |
| **Hesaplar ve profiller:** İş ortağı faturalama profillerini, yasal profilleri, MPN profilini, iş profillerini veya destek profillerini nasıl alalı veya güncelleştirebilirsiniz. Ayrıca müşterilerin veya dolaylı kurumsal bayilerin listesini de alabilirsiniz. | [Hesapları ve profilleri yönetme](manage-profiles-and-information.md)                                                                        |
| **Faturalama:** Faturalama döngüsünü değiştirme, Azure ücretlerini ve Azure kullanım kayıtlarını alma, faturaları alma, iş ortağının geçerli hesap bakiyesini alma veya müşteri hizmetleri maliyetlerini alma gibi alanlar hakkında bilgi edinin.  | [Faturalandırmayı yönetme](manage-billing.md)   |
| **Azure harcaması:** Azure harcaması ve iş ortağı kullanımı, müşteri aboneliklerinin kullanımı, tarifeli kullanım ve müşteri kullanım bütçeleri hakkında bilgi edinin. Senaryolar ayrıca müşteri kullanım bütçesini güncelleştirmeyi de içerir. | [Azure harcaması](azure-spending.md)  |
| **Müşteri hesaplarını yönetme:** Müşteri hesapları oluşturma ve silme, müşteri hesabı ayrıntılarını yönetme ve doğrulama, kullanıcı hesaplarını yönetme ve lisans atama gibi birçok müşteri hesabı yönetimini nasıl gerçekleştirebilirsiniz?  | [Müşterileri yönetme](manage-customers.md)  |
| **Siparişleri yönetme:** Müşteri siparişlerini ve aboneliklerini program aracılığıyla yönetebilirsiniz. Bu alan Azure rezervasyonları satın alma, sipariş oluşturma, katalogdan teklif alma ve deneme dönüştürme tekliflerini yönetmeyi içerir.   | [Siparişleri yönetme](manage-orders.md)  |
| **Destek sağlama:** Bir müşteri için hizmetleri yönetmeyi, bir abonelik için destek kişilerini alma veya güncelleştirme ve hizmet isteklerini yönetme hakkında bilgi alın.  | [Destek sağlama](provide-support.md)   |
| **Referanslar:** Referans oluşturma, referans listesini öğrenme veya bir referansı güncelleştirme.  | [Referanslar](/partner/develop/referrals)  |
| **Yardımcı Programlar:** Bir adresi doğrulamayı, pazara göre adres biçimlendirme kurallarını öğrenin, etki alanı kullanılabilirliğini doğrulayın, tümleştirme korumalı alandan bir müşteri hesabını silin veya etkinlik kaydını İş Ortağı Merkezi öğrenin. | [Yardımcı Programlar](utilities.md)  |
| **Güvenlik:** Çok faktörlü kimlik doğrulaması (MFA) ile ilgili REST API'ler hakkında bilgi İş Ortağı Merkezi. Bu API'ler, iş ortağı kiracınız için her kullanıcı hesabı için MFA'nın zorunlu kılınmanıza yardımcı olur.  | [İş ortağı güvenlik gereksinimleri durumu](partner-security-requirements.md)  |

## <a name="next-steps"></a>Sonraki adımlar

- [Bkz. İş Ortağı Merkezi örnekleri](partner-center-samples.md)
- [Çalışmaya başlamayı öğrenin](get-started.md)