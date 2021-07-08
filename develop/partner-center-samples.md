---
title: İş Ortağı Merkezi örnekleri
description: Api'leri kullanarak hızlıca İş Ortağı Merkezi yardımcı olmak için bir örnek program, C\ yönetilen kod parçacıkları ve REST örnek istekleri ve yanıtları sağlaruz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 36d1c74e12ae680facef1414ce35ac2d6fb5322c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547844"
---
# <a name="partner-center-samples"></a>İş Ortağı Merkezi örnekleri

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Api'leri kullanarak hızla İş Ortağı Merkezi yardımcı olmak için bir örnek program, C# yönetilen kod parçacıkları ve REST örnek istekleri ve yanıtları sağlaruz.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Örnek                                                        | Ayrıntılar                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kod parçacıkları                                                 | Müşteri hesaplarını yönetmek, analiz elde etmek, sipariş vermek, faturalama ve abonelikleri yönetmek, destek sağlamak ve hesapları ve profilleri yönetmek için İş Ortağı Merkezi yönetilen API'sinin nasıl kullanıldığına işaret gösteren işaretçiler ve .NET, Java ve PowerShell kod parçacıkları için bkz. [Senaryolar.](scenarios.md)                                                                          |
| REST örnekleri                                                  | Müşteri hesaplarını yönetmek, analiz almak, sipariş vermek, faturalama ve abonelikleri yönetmek, destek sağlamak ve hesapları ve profilleri yönetmek için İş Ortağı Merkezi REST API'nin nasıl kullanılal olduğunu göstermek üzere örnek istekler ve yanıtlar için bkz. [Senaryolar.](scenarios.md)                                                                                                       |
| [Konsol test uygulaması](console-test-app.md)                       | Bu uygulama C# ve Java ile kullanılabilir, senaryolar bölümünde listelenen tüm senaryolar için kod ve bazı hata işleme sağlar.                                                                        |
| [CSP müşteri web vitrini](csp-customer-web-storefront.md) | Bu site, müşterilerimizin Microsoft ürünlerine abonelik satın almak için kullanabileceği çalışan bir çevrimiçi mağazayı gösterir. CSP Customer Storefront Builder Hızlı Başlangıç Kılavuzu ile kolayca [şirket için bir web sitesi oluşturabilirsiniz.](csp-customer-storefront-builder-quick-start-guide-.md)                                                              |
| Web sitesini depolama                                                | Bu uygulama, iş ortaklarının sunduğu tekliflerin kataloğunu temel alan bir web Bulut Çözümü Sağlayıcısı gösterir. Müşteriler siteniz üzerinden bir mağaza hesabı oluşturabilir ve yazılım abonelikleri sipariş edebilirsiniz.<br/><br/>                  **Kodu al:**<br/> [Örnek kodu indirme](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Yayından önce yapılandırma gerekenler:**<br/><br/> - Kimlik doğrulaması: Uygulama kimliği & gizli<br/> - Markalama: logo ve şirket adı<br/> - Hoş geldiniz iletisi<br/> - Açıklamalar ve fiyatlar da dahil olmak üzere teklifler. Uygulama, liste fiyatlarının geçerli vergileri dahil olduğunu varsayıyor. Alternatif olarak, satın alma sırasında vergiyi hesaplamak için ek mantık ekleyebilirsiniz.<br/> - Ödeme bilgileri: Kendi kredi kartı seçeneklerinizi, PayPal veya diğer ödeme türlerini sağlama. Bu bölümü yapılandırmadan önce Ödeme, sahtekarlık veya [kötüye kullanım kılavuzunu okuyun.](/partner-center/non-payment-fraud-misuse) |