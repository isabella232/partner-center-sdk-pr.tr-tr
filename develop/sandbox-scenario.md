---
title: Satıcı ilişkisini destekleyen iş ortağı korumalı özellikleri
description: İş ortağı korumalı alanı, iş ortağı ve müşteri arasındaki ilişkileri destekleyebilir
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711874"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a>Satıcı ilişkisini destekleyen iş ortağı korumalı özellikleri

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, iş ortağı ve müşteri arasındaki satıcı ilişkileri için korumalı alanda nelerin desteklendiği açıklanır. 

## <a name="prerequisites"></a>Önkoşullar

- İş Ortağı Merkezi hesabı kimlik bilgileri. Sandbox senaryosu hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
- Bir müşteri KIMLIĞI (müşteri-Kiracı kimliği). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard/home)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI (müşteri-Kiracı kimliği) ile aynıdır.
- Bir müşteri, tıp tümleştirme korumalı alanından silinmeden önce tüm Azure ayrılmış sanal makine örneklerinin ve yazılım satın alma siparişlerinin iptal edilmesi gerekir.

## <a name="scenarios-supporting-reseller-relationship"></a>Satıcı Ilişkisini destekleyen senaryolar

1.  Korumalı alan doğrudan fatura ortakları ve dolaylı sağlayıcılar, Sandbox müşterisi ile ilişkiler oluşturabilir. 
2.  Korumalı alan doğrudan fatura ortakları ve dolaylı sağlayıcılar, korumalı alan müşterilerini davet edemez.



### <a name="in-the-sandbox"></a>Korumalı alanda

**Doğrudan fatura ortakları**:

• Mevcut müşteriler eklenebilir

• Yeni müşterilerle ilişkiler isteyemezsiniz

**Dolaylı sağlayıcılar**:

• Mevcut müşteriler eklenebilir

• Yeni müşterilerle ilişkiler isteyemezsiniz

• Dolaylı bir satıcı ile bir ilişkiye sahip olamaz

**Dolaylı satıcı**: (çok yakında)

• Mevcut müşterilerle ilişkilerine sahip olabilir

• Yeni ilişkiler isteyemezsiniz veya yeni müşteriler ekleyemez

### <a name="in-partner-center"></a>Iş Ortağı Merkezi 'nde

**Doğrudan fatura ortakları**:

• Yeni müşteriler ekleyebilir

• Yeni müşterilerle ilişkiler talep edebilir

**Dolaylı sağlayıcılar**:

• Yeni müşteriler ekleyebilir

• Yeni müşterilerle ilişkiler talep edebilir

• Dolaylı satıcılarla ilişkiler alabilir

**Dolaylı satıcılar**:

• Yeni müşteriler eklenemiyor

• Yeni müşterilerle ilişkiler talep edebilir

3. Korumalı alan doğrudan fatura ortağı ve dolaylı sağlayıcılar, Iş Ortağı Merkezi kullanıcı arabiriminden ve API 'den satıcı ilişkisini kaldırabilir.

4. Korumalı alan satıcı Ilişkisini kaldır müşteri AP 'sini Sil ' i çağırır. Bu işlem ilişkiyi kaldırır ve müşteri kiracısını siler. {baseURL}/v1/Customers/{Customer-Tenant-ID}

Ayrıntılar için müşterinin [satıcı Ilişkilerini kaldır ilişkisini](remove-a-reseller-relationship-with-a-customer.md) izleyin. Ancak, ürün ve Sandbox özellikleri arasında bazı farklılıklar vardır.

### <a name="request-syntax"></a>ISTEK SÖZDIZIMI

|**Yöntem**|**Silme**|
|-------------|------------|
|Sil|{baseURL}/v1/Customers/{Customer-Tenant-ID} |

İstek gövdesi yok

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](./error-codes.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Azure Market ürünleri için korumalı alan aboneliklerini etkinleştirin](activate-sandbox-subscription-azure-marketplace-products.md)

- [Korumalı alan 'dan bir siparişi iptal etme](cancel-an-order-from-the-integration-sandbox.md)

- [Test etme ve hata ayıklama](test-and-debug.md)