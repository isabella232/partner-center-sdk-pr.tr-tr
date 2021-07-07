---
title: Kurumsal Bayi ilişkisi için korumalı alan özellikleri
description: İş ortağı korumalı alanı, iş ortağı ile müşteri arasındaki ilişkileri destekleyene sahip
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aa6c4fb9ef71bacfad7e0f1510fec15f6af60a05
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547402"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a>Kurumsal Bayi ilişkisi için korumalı alan özellikleri

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu makalede iş ortağı ile müşteri arasındaki kurumsal bayi ilişkileri için Korumalı Alan'da desteklenenler açıklanmıştır. 

## <a name="prerequisites"></a>Önkoşullar

- İş Ortağı Merkezi kimlik bilgileri. Korumalı alan senaryosu hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
- Müşteri kimliği (customer-tenant-id). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard/home) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği (customer-tenant-id) ile aynıdır.
- İpucu Azure Ayrılmış Sanal Makine Örnekleri alanından müşteri silmeden önce tüm yazılım satın alma siparişlerini ve yazılım satın alma siparişlerini iptal etmeniz gerekir.

## <a name="scenarios-supporting-reseller-relationship"></a>Kurumsal Bayi İlişkisi Destekleyen Senaryolar

1.  Korumalı Alan Doğrudan Fatura İş Ortakları ve Dolaylı Sağlayıcılar, Korumalı Alan müşterisi ile ilişkiler oluşturabilir. 
2.  Korumalı Alan Doğrudan Fatura İş Ortakları ve Dolaylı Sağlayıcılar Korumalı Alan müşterilerini davetamaz.

3. Korumalı Alan Doğrudan Fatura İş Ortağı ve Dolaylı Sağlayıcılar, kurumsal bayi ilişkisini kullanıcı arabiriminden İş Ortağı Merkezi API'den kaldırabilir.

4. Korumalı Alan Kurumsal Bayi İlişkisi Silme müşteri AP'lerini çağıracak. Bu, ilişkiyi kaldırır ve müşteri kiracısı silinir. {baseURL}/v1/Customers/{customer-Tenant-id}


    ### <a name="in-the-sandbox"></a>Korumalı Alanda

    **Doğrudan fatura iş ortakları:**

    - Mevcut müşterileri ekleyebilir

    - Yeni müşterilerle ilişki isteği bulunamaz

    **Dolaylı sağlayıcılar:**

    - Mevcut müşterileri ekleyebilir

    - Yeni müşterilerle ilişki isteği bulunamaz

    - Dolaylı kurumsal bayi ile ilişki bulunamaz

    **Dolaylı kurumsal bayi:** 

    -   Mevcut müşterilerle ilişkileri olabilir

    -   Yeni ilişkiler isteği veya yeni müşteri ekleme

    ### <a name="in-partner-center"></a>İş Ortağı Merkezi

    **Doğrudan fatura iş ortakları:**

    -   Yeni müşteriler ekleyebilir

    -   Yeni müşterilerle ilişki isteğide olabilir

    **Dolaylı sağlayıcılar:**

    -   Yeni müşteriler ekleyebilir

    -   Yeni müşterilerle ilişki isteğide olabilir

    -   Dolaylı kurumsal bayilerle ilişki olabilir

    **Dolaylı kurumsal bayiler:**

    -   Yeni müşteri ekley bilmiyorum

    -   Yeni müşterilerle ilişki isteğide olabilir


Ayrıntılar için [müşterinin Kurumsal Bayi](remove-a-reseller-relationship-with-a-customer.md) İlişkilerini Kaldır'ı izleyin. Ancak Product ve Sandbox özellikleri arasında bazı farklar vardır.

### <a name="request-syntax"></a>İSTEK SÖZ DIZIMI

|**Yöntem**|**Silme**|
|-------------|------------|
|Sil|{baseURL}/v1/Customers/{customer-Tenant-id} |

İstek gövdesi Yok

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](./error-codes.md)

## <a name="next-steps"></a>Sonraki adımlar

- [Azure Market ürünleri için Korumalı alan aboneliklerini etkinleştirme](activate-sandbox-subscription-azure-marketplace-products.md)

- [Korumalı Alandan siparişi iptal etme](cancel-an-order-from-the-integration-sandbox.md)

- [Test etme ve hata ayıklama](test-and-debug.md)