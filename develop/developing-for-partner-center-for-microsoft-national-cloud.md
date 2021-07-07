---
title: Microsoft Ulusal bulutları için Iş Ortağı Merkezi için geliştirme
description: Microsoft Ulusal bulutları için Iş Ortağı Merkezi için geliştirme yaparken iş ortağı Merkezi SDK farkları.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d38a35fb88b4835716e429aeed731a0d55d9a669
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906451"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Microsoft Ulusal bulutları için Iş Ortağı Merkezi için geliştirme

**Uygulama hedefi**: 21Vianet tarafından işletilen Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

İş Ortağı Merkezi 'nin bir SDK belgeleri kümesi vardır. Ancak, bazı işlevler Microsoft Ulusal bulutları için Iş Ortağı Merkezi sürümlerinde kullanılamayabilir.

Geliştiricilerin aşağıdaki Iş ortağı merkezi sürümleri için SDK değişikliklerini göz önünde bulundurmanız gerekir:

- [21Vianet tarafından çalıştırılan İş Ortağı Merkezi](#partner-center-operated-by-21vianet)
- [Microsoft Bulut Almanya için İş Ortağı Merkezi](#partner-center-for-microsoft-cloud-germany)
- [Microsoft Cloud for US Government için İş Ortağı Merkezi](#partner-center-for-microsoft-cloud-for-us-government)

Her Iş Ortağı Merkezi SDK makalesinde ilgili Iş ortağı merkezi sürümleri listelenir. Her yönetilen başvuru makalesi, **gereksinimler** bölümünde geçerli Iş Ortağı Merkezi sürümlerini de listeler.

## <a name="partner-center-operated-by-21vianet"></a>21Vianet tarafından çalıştırılan İş Ortağı Merkezi

*21Vianet tarafından işletilen* iş *Ortağı Merkezi ve iş* ortağı merkezi arasındaki iş ortakları arasındaki farklar şunlardır:

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için bir parolayı program aracılığıyla sıfırlayamazsınız.

- Azure abonelikleri kullanılamıyor.

- Müşterinizin kullanıcısına ilişkin lisansları yönetemezsiniz. bunun yerine, müşterilerinizin lisanslarını yönetmek için Office 365 yönetim merkezini kullanması gerekir.

- Tüm destek istekleri, 21Vianet tarafından işletilen Iş Ortağı Merkezi aracılığıyla yönetilir. Hizmet istekleri ve hizmet güncelleştirmeleri uygulanmaz.

## <a name="partner-center-for-microsoft-cloud-germany"></a>Microsoft Bulut Almanya için İş Ortağı Merkezi

> [!IMPORTANT]
> Müşterilerin ihtiyaçlarına bağlı olarak, Almanya için bulut stratejimiz, genel bulut teklifimiz ile tutarlı olan Almanya 'daki yeni bulut bölgelerinin teslimatını odaklamaktadır. Bu odak sayesinde, artık yeni müşterileri kabul etmiyoruz veya mevcut Almanya Microsoft Bulut yeni hizmetleri dağıtacağız. Mevcut müşteriler, gerekli güvenlik güncelleştirmeleriyle korunabilediğimiz geçerli bulut hizmetlerini kullanmaya devam edebilir.
>
> İleri doğru hareket eden yeni müşteriler kullanılabilir hale geldiğinde mevcut Avrupa bölgelerini veya Almanya 'daki yeni bölgeleri kullanma seçeneğine sahiptir. Daha fazla bilgi için bkz. [Microsoft, Almanya 'daki yeni veri merkezlerinden bulut hizmetleri sunma](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

*Microsoft bulut Almanya için* Iş *Ortağı Merkezi* ve iş ortağı merkezi arasındaki iş ortakları arasındaki farklar şunlardır:

- İş ortakları, müşteri kuruluşu için Kullanıcı oluşturamaz veya rol atayabilir.
  - İş ortakları alanları okuyabilir, ancak yazamaz veya güncelleştiremez.
  - iş ortaklarının, Office 365 yönetim merkezinde veya Azure portal aracılığıyla müşterilerinin kullanıcılarını el ile oluşturması veya güncelleştirmesi gerekir. [Azure Active Directory belgelerine](/azure/active-directory/)bakın.

- Microsoft Bulut Almanya portalı veya API 'Leri için Iş Ortağı Merkezi 'ni kullanarak müşterinizin kullanıcılarına yönelik lisansları yönetemezsiniz. bunun yerine, lisanslarını yönetmek için Office 365 yönetim merkezi veya Azure etkin doğrudan grup lisans yönetimi 'ni (çok yakında) kullanmanız gerekir.
  - (isteğe bağlı) Azure AD Graph API kullanabilirsiniz. Bkz. [bir kullanıcıya lisans atama](/graph/api/user-assignlicense). Microsoft Bulut almanya için iş ortağı merkezi için yerine Graph uç noktasını kullandığınızdan emin olun `https://graph.cloudapi.de` `https://graph.windows.net` .

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için bir parolayı program aracılığıyla sıfırlayamazsınız. Office 365 yönetim merkezini veya Azure portal kullanın. Bkz. [Azure Active Directory Kullanıcı parolasını sıfırlama](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). 1. adım için Microsoft Bulut Almanya Azure portal oturum açmalısınız.

- Geliştiricilerin, Microsoft Bulut Almanya için Iş Ortağı Merkezi uygulamasındaki Iş Ortağı Merkezi API/SDK işlevini bütünleştirmek için uygulama KIMLIKLERINI el ile kaydetmesi gerekir. Daha fazla bilgi için bkz. [Microsoft Ulusal bulut Için Iş Ortağı Merkezi için uygulama ayrıntılarını kaydetme](create-apps-for-partner-center-for-microsoft-national-clouds.md).

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Microsoft Cloud for US Government için İş Ortağı Merkezi

Microsoft Cloud for US Government iş *ortağı merkezi* ve iş *ortağı merkezi* arasındaki iş ortakları arasındaki farklar şunlardır:

- Office 365 abonelikler şu anda Microsoft Cloud for US Government için iş ortağı merkezi için kullanılamaz.

- Microsoft Cloud for US Government destekleyen mevcut iş ortakları, Microsoft Cloud for US Government için iş ortağı merkezi 'nde yeni hesaplar oluşturmanız gerekir.

- Microsoft Cloud for US Government müşteriler tek bir iş ortağıyla transact olmalıdır.
  - Microsoft Cloud for US Government senaryolarındaki mevcut bir müşteriyle çok kanallı ve çoklu iş ortağı ve istek ilişkisi geçerli değildir. bu sınırlama Office 365 şu anda kullanılamıyor.

- İş ortakları, müşteri kuruluşu için Kullanıcı oluşturamaz veya rol atayabilir.
  - İş ortakları alanları okuyabilir, ancak yazamaz veya güncelleştiremez. İş ortaklarının, müşterilerinin kullanıcılarını Azure portal el ile oluşturması veya güncelleştirmesi gerekir. [Azure Active Directory belgelerine](/azure/active-directory/)bakın.

- Bir müşteri kullanıcısı veya tam iş ortağı kullanıcısı için bir parolayı program aracılığıyla sıfırlayamazsınız. Azure portalını kullanın. Bkz. [Azure Active Directory Kullanıcı parolasını sıfırlama](/azure/active-directory/active-directory-users-reset-password-azure-portal). 1. adım için Azure portal Microsoft Cloud for US Government oturum açmalısınız.

- Microsoft Cloud for US Government için iş ortağı merkezi REST uç noktaları, iş ortağı merkezi ile aynıdır: `https://api.partnercenter.microsoft.com` .

- Geliştiricilerin, Microsoft Cloud for US Government için Iş Ortağı Merkezi uygulamasındaki Iş Ortağı Merkezi API/SDK işlevini bütünleştirmek için uygulama KIMLIKLERINI el ile kaydetmesi gerekir. Daha fazla bilgi için bkz. [Microsoft Ulusal bulut Için Iş Ortağı Merkezi için uygulama ayrıntılarını kaydetme](create-apps-for-partner-center-for-microsoft-national-clouds.md).
