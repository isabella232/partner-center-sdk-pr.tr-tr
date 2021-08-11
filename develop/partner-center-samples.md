---
title: İş Ortağı Merkezi örnekleri
description: Iş Ortağı Merkezi API 'Leriyle hızlıca çalışmaya başlamanıza yardımcı olması için örnek bir program, C \ yönetilen kod parçacıkları ve REST örnek istekleri ve yanıtları sağlıyoruz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 34e269b1a0e711f82144898441c75d731b8613f70512517e12b6705990b35622
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997609"
---
# <a name="partner-center-samples"></a>İş Ortağı Merkezi örnekleri

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Iş Ortağı Merkezi API 'Leriyle hızlıca çalışmaya başlamanıza yardımcı olması için örnek bir program, C# yönetilen kod parçacıkları ve REST örnek istekleri ve yanıtları sağlıyoruz.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Örnek                                                        | Ayrıntılar                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kod parçacıkları                                                 | Iş Ortağı Merkezi tarafından yönetilen API 'nin müşteri hesaplarını yönetmek, analiz almak, siparişleri yerleştirmek, faturalandırma ve abonelikleri yönetmek, destek sağlamak ve hesapları ve profilleri yönetmek için nasıl kullanılacağını gösteren işaretçiler ve .NET, Java ve PowerShell kod parçacıkları için bkz. [senaryolar](scenarios.md).                                                                          |
| REST örnekleri                                                  | Müşteri hesaplarını yönetmek, analiz almak, siparişleri yerleştirmek, faturalandırma ve abonelikleri yönetmek, destek sağlamak ve hesapları ve profilleri yönetmek için Iş Ortağı Merkezi REST API nasıl kullanacağınızı gösteren örnek istekler ve yanıtlar için bkz. [senaryolar](scenarios.md).                                                                                                       |
| [Konsol test uygulaması](console-test-app.md)                       | Bu uygulama C# ve Java 'da kullanılabilir, senaryolar bölümünde listelenen tüm senaryolar için kod ve bazı hata işleme işlemleri sağlar.                                                                        |
| [CSP müşteri web vitrini](csp-customer-web-storefront.md) | Bu sitede, müşterilerinizin Microsoft ürünlerine abonelik satın almak için kullanabileceği çalışan bir çevrimiçi mağaza gösterilmektedir. [CSP Customer storefront Builder hızlı başlangıç kılavuzu](csp-customer-storefront-builder-quick-start-guide-.md)ile şirketiniz için kolayca bir Web sitesi oluşturabilirsiniz.                                                              |
| Web sitesini depola                                                | bu uygulama, Bulut Çözümü Sağlayıcısı iş ortakları için sunulan tekliflerin kataloğunu temel alan bir web mağazası oluşturmayı gösterir. Müşteriler, siteniz aracılığıyla bir mağaza hesabı oluşturabilir ve yazılım abonelikleri sipariş edebilir.<br/><br/>                  **Kodu alın:**<br/> [Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Sürümden önce yapılandırılacak:**<br/><br/> -Authentication: uygulama KIMLIĞI & gizli<br/> -Marka: logo ve şirket adı<br/> -Hoş geldiniz iletisi<br/> -Teklifler, açıklamalar ve fiyatlar dahil. Uygulama, liste fiyatlarının geçerli vergileri dahil olduğunu varsayar. Alternatif olarak, kullanıma alma sırasında vergiyi hesaplamak için ek Logic de ekleyebilirsiniz.<br/> -ödeme bilgileri: kendi kredi kartı seçeneklerinizi, PayPal veya diğer ödeme türlerini belirtin. Bu bölümü yapılandırmadan önce, [ödeme olmayan, sahtekarlık veya kötüye kullanma](/partner-center/non-payment-fraud-misuse)kılavuzunu okuyun. |