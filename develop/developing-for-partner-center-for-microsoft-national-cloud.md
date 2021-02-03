---
title: Microsoft Ulusal bulutları için Iş Ortağı Merkezi için geliştirme
description: Microsoft Ulusal bulutları için Iş Ortağı Merkezi için geliştirme yaparken iş ortağı Merkezi SDK farkları.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7882846de0c591b21fe73345f560613f535d1788
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769412"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Microsoft Ulusal bulutları için Iş Ortağı Merkezi için geliştirme

**Uygulama hedefi:**

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

İş Ortağı Merkezi 'nin bir SDK belgeleri kümesi vardır. Ancak, bazı işlevler Microsoft Ulusal bulutları için Iş Ortağı Merkezi sürümlerinde kullanılamayabilir.

Geliştiricilerin aşağıdaki Iş ortağı merkezi sürümleri için SDK değişikliklerini göz önünde bulundurmanız gerekir:

- [21Vianet tarafından çalıştırılan iş ortağı Merkezi](#partner-center-operated-by-21vianet)
- [Microsoft Bulut Almanya için İş Ortağı Merkezi](#partner-center-for-microsoft-cloud-germany)
- [Microsoft Cloud for US Government için İş Ortağı Merkezi](#partner-center-for-microsoft-cloud-for-us-government)

Her Iş Ortağı Merkezi SDK makalesinde ilgili Iş ortağı merkezi sürümleri listelenir. Her yönetilen başvuru makalesi, **gereksinimler** bölümünde geçerli Iş Ortağı Merkezi sürümlerini de listeler.

## <a name="partner-center-operated-by-21vianet"></a>21Vianet tarafından çalıştırılan iş ortağı Merkezi

*21Vianet tarafından işletilen* iş *Ortağı Merkezi ve iş* ortağı merkezi arasındaki iş ortakları arasındaki farklar şunlardır:

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için bir parolayı program aracılığıyla sıfırlayamazsınız.

- Azure abonelikleri kullanılamıyor.

- Müşterinizin kullanıcısına ilişkin lisansları yönetemezsiniz. Bunun yerine, müşterilerinizin lisanslarını yönetmek için Office 365 Yönetim merkezini kullanması gerekir.

- Tüm destek istekleri, 21Vianet tarafından işletilen Iş Ortağı Merkezi aracılığıyla yönetilir. Hizmet istekleri ve hizmet güncelleştirmeleri uygulanmaz.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Microsoft Bulut Almanya için İş Ortağı Merkezi

> [!IMPORTANT]
> Müşterilerin ihtiyaçlarına bağlı olarak, Almanya için bulut stratejimiz, genel bulut teklifimiz ile tutarlı olan Almanya 'daki yeni bulut bölgelerinin teslimatını odaklamaktadır. Bu odak sayesinde, artık yeni müşterileri kabul etmiyoruz veya mevcut Almanya Microsoft Bulut yeni hizmetleri dağıtacağız. Mevcut müşteriler, gerekli güvenlik güncelleştirmeleriyle korunabilediğimiz geçerli bulut hizmetlerini kullanmaya devam edebilir.
>
> İleri doğru hareket eden yeni müşteriler kullanılabilir hale geldiğinde mevcut Avrupa bölgelerini veya Almanya 'daki yeni bölgeleri kullanma seçeneğine sahiptir. Daha fazla bilgi için bkz. [Microsoft, Almanya 'daki yeni veri merkezlerinden bulut hizmetleri sunma](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

*Microsoft bulut Almanya için* Iş *Ortağı Merkezi* ve iş ortağı merkezi arasındaki iş ortakları arasındaki farklar şunlardır:

- İş ortakları, müşteri kuruluşu için Kullanıcı oluşturamaz veya rol atayabilir.
  - İş ortakları alanları okuyabilir, ancak yazamaz veya güncelleştiremez.
  - İş ortaklarının, müşterilerinin kullanıcılarını Office 365 Yönetim merkezinde veya Azure portal aracılığıyla el ile oluşturması veya güncelleştirmesi gerekir. [Azure Active Directory belgelerine](/azure/active-directory/)bakın.

- Microsoft Bulut Almanya portalı veya API 'Leri için Iş Ortağı Merkezi 'ni kullanarak müşterinizin kullanıcılarına yönelik lisansları yönetemezsiniz. Bunun yerine, lisanslarını yönetmek için Office 365 Yönetim merkezini veya Azure Active doğrudan grup lisans yönetimi 'ni (yakında kullanıma sunulacak) kullanmanız gerekir.
  - (İsteğe bağlı) Azure AD Graph API kullanabilirsiniz. Bkz. [bir kullanıcıya lisans atama](/graph/api/user-assignlicense). Microsoft Bulut Almanya için Iş Ortağı Merkezi için yerine grafik uç noktasını kullandığınızdan emin olun `https://graph.cloudapi.de` `https://graph.windows.net` .

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için bir parolayı program aracılığıyla sıfırlayamazsınız. Office 365 Yönetim merkezini veya Azure portal kullanın. Bkz. [Azure Active Directory Kullanıcı parolasını sıfırlama](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). 1. adım için Microsoft Bulut Almanya Azure portal oturum açmalısınız.

- Geliştiricilerin, Microsoft Bulut Almanya için Iş Ortağı Merkezi uygulamasındaki Iş Ortağı Merkezi API/SDK işlevini bütünleştirmek için uygulama KIMLIKLERINI el ile kaydetmesi gerekir. Daha fazla bilgi için bkz. [Microsoft Ulusal bulut Için Iş Ortağı Merkezi için uygulama ayrıntılarını kaydetme](create-apps-for-partner-center-for-microsoft-national-clouds.md).

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Microsoft Cloud for US Government için İş Ortağı Merkezi

*ABD hükümeti için Microsoft bulut* Iş *Ortağı Merkezi* ve iş ortağı merkezi arasındaki iş ortakları arasındaki farklar şunlardır:

- Office 365 abonelikleri, ABD kamu için Microsoft Bulut Iş Ortağı Merkezi için şu anda kullanılamıyor.

- ABD kamu sektörü için Microsoft Bulut destekleyen mevcut iş ortakları, ABD Kamu kamu Microsoft Bulut için Iş Ortağı Merkezi 'nde yeni hesaplar oluşturmanızı sağlamalıdır.

- ABD devlet müşterilerinin Microsoft Bulut tek bir iş ortağıyla Transact olması gerekir.
  - ABD kamu senaryolarında Microsoft Bulut içindeki mevcut müşteriyle çok kanallı ve çoklu iş ortağı ve istek ilişkisi geçerli değildir. Bu sınırlama, Office 365 Şu anda kullanılabilir değil.

- İş ortakları, müşteri kuruluşu için Kullanıcı oluşturamaz veya rol atayabilir.
  - İş ortakları alanları okuyabilir, ancak yazamaz veya güncelleştiremez. İş ortaklarının, müşterilerinin kullanıcılarını Azure portal el ile oluşturması veya güncelleştirmesi gerekir. [Azure Active Directory belgelerine](/azure/active-directory/)bakın.

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için bir parolayı program aracılığıyla sıfırlayamazsınız. Azure portal kullanın. Bkz. [Azure Active Directory Kullanıcı parolasını sıfırlama](/azure/active-directory/active-directory-users-reset-password-azure-portal). 1. adım için ABD hükümeti için Microsoft Bulut Azure portal oturum açmalısınız.

- ABD kamu için Microsoft Bulut Iş Ortağı Merkezi REST uç noktaları, Iş Ortağı Merkezi ile aynıdır: `https://api.partnercenter.microsoft.com` .

- Geliştiriciler, ABD kamu sektörü için Iş ortağı Microsoft Bulut merkezi uygulamasındaki Iş Ortağı Merkezi API/SDK işlevini bütünleştirmek üzere uygulama KIMLIKLERINI el ile kaydetmelidir. Daha fazla bilgi için bkz. [Microsoft Ulusal bulut Için Iş Ortağı Merkezi için uygulama ayrıntılarını kaydetme](create-apps-for-partner-center-for-microsoft-national-clouds.md).
