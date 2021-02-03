---
title: CSP müşteri web vitrini
description: Bu örnek Web sitesi kodu, müşterilerin Microsoft ürünlerine abonelik satın almasını sağlamak için çalışan bir çevrimiçi mağaza gösterir.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768800"
---
# <a name="csp-customer-web-storefront"></a>CSP müşteri web vitrini

**Uygulama hedefi:**

- İş Ortağı Merkezi

> [!NOTE]
> Bu örnek uygulama yalnızca genel Iş Ortağı Merkezi örneği için geçerlidir. Microsoft Bulut Almanya için Iş ortağı merkezi veya ABD Kamu kamu Microsoft Bulut için Iş Ortağı Merkezi için geçerlidir.

[Iş Ortağı Merkezi storefront](https://github.com/Microsoft/Partner-Center-Storefront) , müşterilerin Microsoft ürünlerine abonelik satın almak için kullanabileceği bir çevrimiçi mağaza için **örnek bir Web sitesidir** . [Teklifleri yapılandırmak](#configure-offers), [marka eklemek](#configure-branding) ve [ödeme yöntemi eklemek](#configure-payment-types)için bu **örnek kodu** kendi kullanımınıza göre değiştirebilirsiniz.

## <a name="sample-code"></a>Örnek kod

GitHub 'dan [Iş Ortağı Merkezi storefront örnek kodunu](https://github.com/Microsoft/Partner-Center-Storefront) indirin.

## <a name="configure-authentication"></a>Kimlik doğrulamasını yapılandırma

Uygulamayı oluşturmadan önce, [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtmak için Web.config dosyasında aşağıdaki değerleri güncelleştirin. Erken geliştirme sırasında veya üretimde test için tümleştirme korumalı alan hesabı ayarlarınızı kullanmanız gerekir (tıp).

- **partnerCenter. ApplicationId**
- **partnerCenter. applicationSecret**
- **partnerCenter. Domain**
- **webPortal. ClientID**
- **webPortal. clientSecret**
- **webPortal. Domain**
- **webPortal. Azurestoraygeconnectionstring**

## <a name="configure-offers"></a>Teklifleri yapılandırma

(**Microsoftoffer**) teklif kümesini **Offercatalogviewmodel** içinde yapılandırabilirsiniz.

## <a name="configure-branding"></a>Marka yapılandırma

Bu örnek Web sitesi, *BrandingConfiguration.cs* ve *PortalBranding.cs*' de aşağıdaki şirket ve marka bilgilerini izler:

- Kuruluş adı
- Kuruluş logosu
- Üst bilgi görüntüsü
- Gizlilik Sözleşmesi
- İlgili kişinin e-posta adresi
- İrtibat telefon numarası
- Destek e-postası
- Destek telefon numarası

### <a name="configure-payment-types"></a>Ödeme türlerini yapılandır

Uygulama Şu anda *PayPalGateway.cs* içinde uygulanan bir PayPal ağ geçidi kullanıyor.