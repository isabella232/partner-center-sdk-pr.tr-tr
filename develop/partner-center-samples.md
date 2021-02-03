---
title: İş Ortağı Merkezi örnekleri
description: Iş Ortağı Merkezi API 'Leriyle hızlıca çalışmaya başlamanıza yardımcı olması için örnek bir program, C \ yönetilen kod parçacıkları ve REST örnek istekleri ve yanıtları sağlıyoruz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2098544e8607eabc4d25d90dcd7cad41510778a9
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769496"
---
# <a name="partner-center-samples"></a>İş Ortağı Merkezi örnekleri

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Iş Ortağı Merkezi API 'Leriyle hızlıca çalışmaya başlamanıza yardımcı olması için örnek bir program, C# yönetilen kod parçacıkları ve REST örnek istekleri ve yanıtları sağlıyoruz.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Örnek                                                        | Ayrıntılar                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kod parçacıkları                                                 | Iş Ortağı Merkezi tarafından yönetilen API 'nin müşteri hesaplarını yönetmek, analiz almak, siparişleri yerleştirmek, faturalandırma ve abonelikleri yönetmek, destek sağlamak ve hesapları ve profilleri yönetmek için nasıl kullanılacağını gösteren işaretçiler ve .NET, Java ve PowerShell kod parçacıkları için bkz. [senaryolar](scenarios.md).                                                                          |
| REST örnekleri                                                  | Müşteri hesaplarını yönetmek, analiz almak, siparişleri yerleştirmek, faturalandırma ve abonelikleri yönetmek, destek sağlamak ve hesapları ve profilleri yönetmek için Iş Ortağı Merkezi REST API nasıl kullanacağınızı gösteren örnek istekler ve yanıtlar için bkz. [senaryolar](scenarios.md).                                                                                                       |
| [Konsol test uygulaması](console-test-app.md)                       | Bu uygulama C# ve Java 'da kullanılabilir, senaryolar bölümünde listelenen tüm senaryolar için kod ve bazı hata işleme işlemleri sağlar.                                                                        |
| [CSP müşteri web vitrini](csp-customer-web-storefront.md) | Bu sitede, müşterilerinizin Microsoft ürünlerine abonelik satın almak için kullanabileceği çalışan bir çevrimiçi mağaza gösterilmektedir. [CSP Customer storefront Builder hızlı başlangıç kılavuzu](csp-customer-storefront-builder-quick-start-guide-.md)ile şirketiniz için kolayca bir Web sitesi oluşturabilirsiniz.                                                              |
| Web sitesini depola                                                | Bu uygulama, bulut çözümü sağlayıcısı iş ortakları tarafından kullanılabilen tekliflerin kataloğuna göre bir Web deposunun nasıl oluşturulacağını gösterir. Müşteriler, siteniz aracılığıyla bir mağaza hesabı oluşturabilir ve yazılım abonelikleri sipariş edebilir.<br/><br/>                  **Kodu alın:**<br/> [Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Sürümden önce yapılandırılacak:**<br/><br/> -Authentication: uygulama KIMLIĞI & gizli<br/> -Marka: logo ve şirket adı<br/> -Hoş geldiniz iletisi<br/> -Teklifler, açıklamalar ve fiyatlar dahil. Uygulama, liste fiyatlarının geçerli vergileri dahil olduğunu varsayar. Alternatif olarak, kullanıma alma sırasında vergiyi hesaplamak için ek Logic de ekleyebilirsiniz.<br/> -Ödeme bilgileri: kendi kredi kartı seçeneklerinizi, PayPal kodunuzu veya diğer ödeme türlerini belirtin. Bu bölümü yapılandırmadan önce lütfen [ödeme olmayan kılavuz, sahtekarlık veya kötüye kullanımı](/partner-center/non-payment-fraud-misuse)okuyun. |