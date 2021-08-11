---
title: CSP müşteri web vitrini
description: Bu örnek Web sitesi kodu, müşterilerin Microsoft ürünlerine abonelik satın almasını sağlamak için çalışan bir çevrimiçi mağaza gösterir.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07020c365db2ad578e7ff75602519d06eabb2a3bebf0913899fcd8b5345a0365
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995212"
---
# <a name="csp-customer-web-storefront"></a>CSP müşteri web vitrini

**Uygulama hedefi**: Iş Ortağı Merkezi

**İçin geçerlidir**: Microsoft bulut Almanya için Iş Ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bu örnek uygulama yalnızca genel Iş Ortağı Merkezi örneği için geçerlidir.

[Iş Ortağı Merkezi storefront](https://github.com/Microsoft/Partner-Center-Storefront) , müşterilerin Microsoft ürünlerine abonelik satın almak için kullanabileceği bir çevrimiçi mağaza için **örnek bir Web sitesidir** . [Teklifleri yapılandırmak](#configure-offers), [marka eklemek](#configure-branding)ve [bir ödeme yöntemi eklemek](#configure-payment-types)için bu **örnek kodu** kendi kullanımınıza göre değiştirebilirsiniz.

## <a name="sample-code"></a>Örnek kod

[Iş Ortağı Merkezi storefront örnek kodunu](https://github.com/Microsoft/Partner-Center-Storefront) GitHub adresinden indirin.

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

Bu örnek Web sitesi, *Brandingconfiguration. cs* ve *portalmarka. cs*' deki aşağıdaki şirket ve marka bilgilerini izler:

- Kuruluş adı
- Kuruluş logosu
- Üst bilgi görüntüsü
- Gizlilik Sözleşmesi
- İlgili kişinin e-posta adresi
- İrtibat telefon numarası
- Destek e-postası
- Destek telefon numarası

### <a name="configure-payment-types"></a>Ödeme türlerini yapılandır

uygulama şu anda *paypalgateway. cs* dosyasında uygulanan bir PayPal ağ geçidi kullanıyor.