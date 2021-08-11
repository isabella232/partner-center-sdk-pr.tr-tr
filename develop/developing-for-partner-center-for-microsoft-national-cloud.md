---
title: Microsoft Ulusal İş Ortağı Merkezi için geliştirme
description: İş Ortağı Merkezi SDK'sı Microsoft Ulusal Bulutları için İş Ortağı Merkezi geliştirme arasındaki farklar.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8b9b3c3b9a1a1173cf8f3e79f60e629e3d34ea13ecce2e7a2c74924bde2b7d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994872"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Microsoft Ulusal İş Ortağı Merkezi için geliştirme

21Vianet İş Ortağı Merkezi tarafından çalıştırılan | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

İş Ortağı Merkezi SDK belgeleri kümesi vardır. Ancak, Bazı işlevler Microsoft Ulusal Bulutlar için İş Ortağı Merkezi sürümlerinde kullanılamıyor olabilir.

Geliştiricilerin sdk'nın aşağıdaki sürümleri için değişikliklerini göz önünde İş Ortağı Merkezi:

- [21Vianet tarafından çalıştırılan İş Ortağı Merkezi](#partner-center-operated-by-21vianet)
- [Microsoft Bulut Almanya için İş Ortağı Merkezi](#partner-center-for-microsoft-cloud-germany)
- [Microsoft Cloud for US Government için İş Ortağı Merkezi](#partner-center-for-microsoft-cloud-for-us-government)

Her İş Ortağı Merkezi SDK'sı ilgili sürümler İş Ortağı Merkezi listeler. Her yönetilen başvuru makalesi, Gereksinimler bölümünde İş Ortağı Merkezi sürümleri **de** listeler.

## <a name="partner-center-operated-by-21vianet"></a>21Vianet tarafından çalıştırılan İş Ortağı Merkezi

*21Vianet* *tarafından İş Ortağı Merkezi* İş Ortağı Merkezi iş ortakları arasındaki farklar:

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için program aracılığıyla parola sıfırlayabilirsiniz.

- Azure'a abonelikler kullanılamaz.

- Müşterinizin kullanıcı lisanslarını yönetesiniz. Bunun yerine, müşterilerin lisanslarını yönetmek Office 365 merkezi yönetim merkezini kullanmaları gerekir.

- Tüm destek istekleri 21Vianet İş Ortağı Merkezi yönetilen ağ üzerinden yönetilir. Hizmet istekleri ve hizmet güncelleştirmeleri geçerli değildir.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Microsoft Bulut Almanya için İş Ortağı Merkezi

> [!IMPORTANT]
> Müşterilerin ihtiyaçlarına göre Almanya için bulut stratejimiz, küresel bulut teklifimiz ile tutarlı olan yeni bulut bölgelerinin Almanya'da teslimi üzerine odaklanacak. Bu odak noktasıyla, artık şu anda kullanılabilen Microsoft Bulut Almanya'da yeni müşteri kabul etmeyecek veya yeni hizmet dağıtmayacağız. Mevcut müşteriler bugün kullanılabilen geçerli bulut hizmetlerini kullanmaya devam edebilir. Bu hizmetleri gerekli güvenlik güncelleştirmeleriyle koruyacağız.
>
> Daha sonra yeni müşteriler, kullanılabilir olduğunda şu anda kullanılabilir olan Avrupa bölgelerini veya Almanya'daki yeni bölgeleri kullanma seçeneğine sahip olur. Daha fazla bilgi için bkz. [Microsoft bulut hizmetlerini Almanya'da yeni veri merkezlerinden sağlıyor](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

Microsoft Bulut Almanya için *İş Ortağı Merkezi* İş Ortağı Merkezi *arasındaki iş ortakları arasındaki farklar:*

- İş ortakları, müşterilerinin kuruluşu için kullanıcı oluşturama ya da rol atamaz.
  - İş ortakları alanları okuyabilir, ancak yazamaz veya güncelleştiramaz.
  - İş ortaklarının müşteri kullanıcılarını yönetim merkezinde veya Office 365 el ile oluşturması veya güncelleştirmesi Azure portal. Bkz. [Azure Active Directory Belgeleri.](/azure/active-directory/)

- Microsoft Bulut Almanya portalı veya API'leri için İş Ortağı Merkezi kullanıcılarının lisanslarını yönetesiniz. Bunun yerine, lisanslarını yönetmek Office 365 yönetim merkezini veya Azure Active Directly Group lisans yönetimini (çok yakında) kullanabilirsiniz.
  - (İsteğe bağlı) Azure AD api'sini Graph kullanabilirsiniz. Bkz. [Kullanıcıya Lisans Atama.](/graph/api/user-assignlicense) Microsoft İş Ortağı Merkezi için, yerine uygulama uç noktasını Graph emin `https://graph.cloudapi.de` `https://graph.windows.net` olun.

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için program aracılığıyla parola sıfırlayabilirsiniz. Office 365 yönetim merkezini veya Azure portal. Bkz. [Azure Active Directory'de bir kullanıcının parolasını sıfırlama.](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal) 1. adım için Microsoft Bulut Almanya için Azure portal oturum açmanız gerekir.

- Geliştiricilerin Microsoft Bulut Almanya'ya İş Ortağı Merkezi api/SDK işlevselliğini uygulamalarıyla tümleştiren uygulama İş Ortağı Merkezi el ile kaydetmesi gerekir. Daha fazla bilgi için [bkz. Microsoft Ulusal Bulut İş Ortağı Merkezi için uygulama ayrıntılarını kaydetme.](create-apps-for-partner-center-for-microsoft-national-clouds.md)

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Microsoft Cloud for US Government için İş Ortağı Merkezi

İş ortakları için İş Ortağı Merkezi *ve* *İş Ortağı Merkezi arasındaki Microsoft Cloud for US Government* farklar:

- Office 365 abonelikler şu anda İş Ortağı Merkezi için Microsoft Cloud for US Government.

- Yeni hesap oluşturma Microsoft Cloud for US Government mevcut iş ortaklarının yeni hesaplar oluşturması İş Ortağı Merkezi için Microsoft Cloud for US Government.

- Microsoft Cloud for US Government tek bir iş ortağıyla işlemde olması gerekir.
  - Çok kanallı ve çok iş parçası olan ve mevcut müşteriyle istek ilişkisi Microsoft Cloud for US Government senaryolar geçerli değildir. Bu sınırlamanın nedeni Office 365 şu anda mevcut değildir.

- İş ortakları, müşterilerinin kuruluşu için kullanıcı oluşturama ya da rol atamaz.
  - İş ortakları alanları okuyabilir, ancak yazamaz veya güncelleştiramaz. İş ortaklarının müşteri kullanıcılarını el ile oluşturması veya güncelleştirmesi Azure portal. Bkz. [Azure Active Directory Belgeleri.](/azure/active-directory/)

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için program aracılığıyla parola sıfırlayabilirsiniz. Azure portalını kullanın. Bkz. [Azure Active Directory'de bir kullanıcının parolasını sıfırlama.](/azure/active-directory/active-directory-users-reset-password-azure-portal) 1. adım için, oturum açma Azure portal oturum Microsoft Cloud for US Government.

- İş Ortağı Merkezi için REST Microsoft Cloud for US Government, İş Ortağı Merkezi ile aynıdır: `https://api.partnercenter.microsoft.com` .

- Geliştiricilerin uygulama kimliklerini el ile kaydeden geliştiricilerin İş Ortağı Merkezi api/SDK işlevselliğini uygulamalarında İş Ortağı Merkezi için Microsoft Cloud for US Government. Daha fazla bilgi için [bkz. Microsoft Ulusal Bulut İş Ortağı Merkezi için uygulama ayrıntılarını kaydetme.](create-apps-for-partner-center-for-microsoft-national-clouds.md)
