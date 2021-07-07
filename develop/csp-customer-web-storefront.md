---
title: CSP müşteri web vitrini
description: Bu örnek web sitesi kodu, müşterilerin Microsoft ürünlerine abonelik satın almaları için çalışan bir çevrimiçi mağaza gösterir.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d68f17d707731f426cb980a566b6478790d3507c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973341"
---
# <a name="csp-customer-web-storefront"></a>CSP müşteri web vitrini

**Için geçerlidir:** İş Ortağı Merkezi

**Için geçerli değildir:** İş Ortağı Merkezi Microsoft Bulut Almanya | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu örnek uygulama yalnızca uygulamanın genel İş Ortağı Merkezi.

Bu [İş Ortağı Merkezi, müşterilerin](https://github.com/Microsoft/Partner-Center-Storefront) Microsoft **ürünlerine abonelik** satın almak için kullanabileceği bir çevrimiçi mağazanın örnek web sitesidir. Teklifleri yapılandırmak, **marka eklemek** ve bir ödeme yöntemi eklemek için bu örnek [kodu](#configure-branding)kendi [kullanımınız için değiştirebilirsiniz.](#configure-payment-types) [](#configure-offers)

## <a name="sample-code"></a>Örnek kod

[GitHub'den İş Ortağı Merkezi vitrin](https://github.com/Microsoft/Partner-Center-Storefront) örnek kodunu GitHub.

## <a name="configure-authentication"></a>Kimlik doğrulamasını yapılandırma

Uygulamayı derlemeden önce, Web.config dosyasındaki aşağıdaki değerleri, kimlik doğrulamasında oluşturduğunuz Azure AD kimlik doğrulaması [bilgilerini İş Ortağı Merkezi güncelleştirin.](partner-center-authentication.md) Tümleştirme korumalı alan hesabı ayarlarınızı erken geliştirme sırasında veya üretimde (TiP) test etmek için kullansanız iyi olur.

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## <a name="configure-offers"></a>Teklifleri yapılandırma

Teklif kümelerini (**MicrosoftOffer)** **OfferCatalogViewModel içinde yapılandırabilirsiniz.**

## <a name="configure-branding"></a>Markayı yapılandırma

Bu örnek web sitesi, *BrandingConfiguration.cs* ve *PortalBranding.cs* içinde aşağıdaki şirket ve marka bilgilerini izler:

- Kuruluş adı
- Kuruluş logosu
- Üst bilgi görüntüsü
- Gizlilik sözleşmesi
- İlgili kişinin e-posta adresi
- İletişim telefon numarası
- Destek e-postası
- Destek telefon numarası

### <a name="configure-payment-types"></a>Ödeme türlerini yapılandırma

Uygulama şu anda *PayPalGateway.cs* PayPal bir ağ geçidi kullanır.