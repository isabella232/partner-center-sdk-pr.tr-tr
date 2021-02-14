---
title: Tümleştirme korumalı alanı ile test ve hata ayıklama
description: Yanlışlıkla yeni ücret ödemeniz için kodunuzu test etmek ve hatalarını ayıklamak için Iş Ortağı Merkezi tümleştirme korumalı alanı hesabınızı (ve ilgili belirteçleri) nasıl kullanacağınızı öğrenin.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3ff4a7ec3ad984b09c60d3d820423c614fb8020d
ms.sourcegitcommit: 9f8ba784171ab4f980ed0c60ef6f2323849c4a98
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100499890"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Beklenmeyen ücretler ödemekten kaçınmak için Iş Ortağı Merkezi tümleştirme korumalı alanı ile test edin ve hata ayıklayın

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Kodunuzu test etmek için, Iş Ortağı Merkezi 'nde tümleştirme korumalı alanı hesabınızı (ve ilgili belirteçleri) kullanmanız gerekir, böylece yanlışlıkla şirketiniz ödemekten sorumlu yeni ücretler ödemeniz gerekmez. Bu üretim testi (tıp) ortamı hakkında daha fazla bilgi için bkz. [Iş Ortağı Merkezi 'NDE API erişimi ayarlama](set-up-api-access-in-partner-center.md).

## <a name="integration-sandbox-constraints"></a>Tümleştirme korumalı alanı kısıtlamaları

Otomatik derleme doğrulama testlerini çalıştırır, üretimde test yapın veya tümleştirme korumalı alanında el ile test yaparsanız, tümleştirme korumalı alanı için en fazla sınıra ulaşabilirsiniz. Bu limitlerde 75 müşteri, müşteri başına 5 abonelik ve abonelik başına 25 lisans bulunur.

25 lisans sınırı, en az 25 lisans gereksinimini aşan, korumalı alanda bir teklif edinemeyeceğiniz anlamına gelir. Bu sınırlama, denemeleri içerir.

Korumalı alan ortamlarında sunulan çeşitli fatura ve mutabakat dosyaları vardır ancak bunların hepsi eski veya modern platformlarda kullanılabilir değildir. Daha fazla bilgi için aşağıdaki tabloyu doğrulayın.

| **Dosyalar**                    | **Eski sürümünde kullanılabilir** | **Modern 'te kullanılabilir** |
| ---------------------------- | ------------------------ | ------------------------ |
| Fatura PDF dosyası                  | Hayır                       | Yes                      |
| Fatura mutabakatı dosyası | Hayır                       | Yes                      |
| Tahmin dosyası fatura       | Hayır                       | Yes                      |
| Günlük faturalandırılan kullanım dosyası     | Hayır                       | Yes                      |
| Günlük faturalanmamış kullanım dosyası   | Hayır                       | Yes                      |


### <a name="azure-plan"></a>Azure planı

Varsayılan olarak, iş ortakları, Azure planlarını Sandbox hesaplarını kullanarak sağlayamaz. Bu şekilde, bu şekilde iş Sandbox hesabı için yapması gereken iş ortakları erişim için geçerlidir. Erişim için uygulamak üzere Microsoft hesabı yöneticinize veya iş iletişim ekibine ulaşın. Kullanım alanı hesaplarında Microsoft Azure sağlama (MS-AZR-0145P) aboneliklerine erişim için daha önce uygulamış olan iş ortaklarının, erişim için de uygulanması gerekmez. Azure planlarını otomatik olarak sağlamaya yönelik erişim izni verilecektir.

Korumalı alan hesaplarının Azure planlarını sağlamak üzere onaylandığı iş ortakları için aşağıdaki sınırlar geçerlidir:

- Her bir korumalı alan iş ortağı hesabı, tüm müşteri kiracılarında en fazla 10 Azure planına sahip olabilir (planların müşteriler arasında nasıl dağıtılduğuna bakılmaksızın).

- Doğrudan fatura ortağı, her müşteri kiracısı için bir adet Azure planı oluşturabilir.

- Dolaylı bir sağlayıcı, müşteri kiracısı başına en fazla üç Azure planı oluşturabilir (kayıt ortağı olarak belirtilen farklı dolaylı satıcılar için).

- Her Azure planının en fazla üç Azure aboneliği olabilir.

- Sandbox hesabınız kapsamındaki her CSP Azure aboneliği, veri merkezi başına dört sanal makine (VM) çekirdekle sınırlıdır. Bu nedenle, dörtten fazla VM çekirdeği gerektiren VM SKU 'Larını sağlayamazsınız. GPU çekirdekleri gibi bazı özel sanal makine SKU 'Ları da hariç tutulur.

- Her bir korumalı alan iş ortağı hesabının, tüm Azure planlarında faturalandırma döngülerine göre $2000 (USD) harcama limiti vardır. Bir iş ortağı harcama limitine ulaştığında, bir sonraki fatura döngüsüne kadar tüm Azure planları geçici olarak devre dışı bırakılır.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Bulut çözümü sağlayıcısı (CSP) Azure abonelik teklifleri

CSP Azure aboneliği teklifleri artık varsayılan olarak Sandbox hesaplarına uygun değildir. Bunlar sırasıyla Microsoft genel bulutu, Almanya bulutu ve kamu bulutu 'nda CSP Azure abonelikleri için MS-AZR-0146P, MS-AZR-DE-0146P ve MS-AZR-USGOV-0146P içerir. Bu tekliflere erişmesi gereken iş ortakları, erişim için uygulanmalıdır. Erişim için uygulamak üzere Microsoft hesabı Yöneticisi veya iş kişiniz ile tartışın.

Sandbox hesapları CSP Azure aboneliği teklifleri için onaylanmış iş ortakları için aşağıdaki sınırlar geçerlidir:

- En fazla 375 etkin abonelik (müşteri başına 75 müşteriler x 5 abonelik) olabilir. Ancak, CSP Azure abonelikleri yalnızca 10 ' u içerebilir.

- CSP Azure aboneliği, Azure kullanımının $200 ' ine eriştiğinde, kaynakları bir sonraki fatura döngüsüne kadar geçici olarak devre dışı bırakılır. Hala etkin bir abonelik olarak değerlendirilir ve 10 etkin Azure aboneliği sınırına doğru sayılır.

- Sandbox hesabınız kapsamındaki her CSP Azure aboneliği, veri merkezi başına dört sanal makine (VM) çekirdekle sınırlıdır. Bu nedenle, dörtten fazla VM çekirdeği gerektiren VM SKU 'Larını sağlayamazsınız. GPU çekirdekleri gibi bazı özel sanal makine SKU 'Ları da hariç tutulur.

> [!Important]
> 1 Ağustos 2018 ' den önceki korumalı alan hesapları ile sağlanan tüm mevcut CSP Azure abonelikleri artık desteklenmemektedir ve Microsoft tarafından, 16 Ekim 2018 arasında hazırlanacaktır. Abonelikler sağlandıktan sonra, yeniden etkinleştirilemez ve ilişkili veriler artık erişilebilir değildir. Bu Abonelikler altında depolanan değerli verileri olan iş ortakları, 16 Ekim 2018 tarihinden önce verileri yedeklemeli olmalıdır.

### <a name="azure-reserved-vm-instance"></a>Azure ayrılmış VM örneği

Korumalı alan hesabınızla [bir Azure ayrılmış sanal makine örneği satın](purchase-azure-reservations.md) aldıysanız, müşteri BAŞıNA iki VM örneğiyle sınırlı olursunuz. Yalnızca aşağıdaki Azure ayrılmış VM örneğinden Ürün SKU 'Ları arasından seçim yapabilirsiniz:

| Ürün başlığı  | Geçerlilik tarihi  | SKU başlığı                                               | Bölge [ArmRegionName] | Örnek anahtarı [ArmSkuName] | Süre | Tüketim ölçüm kimliği       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, KR Güney, 1 yıl    | Koreagüney             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, ABD Doğu, 1 yıl     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, ABD Batı 2, 1 yıl   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4FA3-a323-f46402977888 |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, ABD Orta Kuzey, 1 yıl    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43F1-aa96-7c1b1b1395a7 |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, CA Doğu, 1 yıl     | Canadadoğu             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Ticari Market ürünleri için abonelikler

Üretimde, [ticari Market SaaS ürünlerine bir abonelik oluşturduktan](create-subscription-azure-marketplace-products.md)sonra, Iş Ortağı Merkezi 'nden kişiselleştirilmiş bir etkinleştirme bağlantısı almanız ve kurulum işlemini tamamlaması için yayımcının sitesini ziyaret etmeniz gerekir. Abonelik faturalandırması, yalnızca kurulum tamamlandıktan sonra başlayacaktır.

CSP korumalı alan ortamında ISV 'Ler ile tümleştirme yoktur. Iş Ortağı Merkezi 'nden bir etkinleştirme bağlantısı almaya çalışırsanız, bir kukla bağlantı döndürülür. Bu kukla bağlantıyı, yayımcının sitesindeki kurulum işlemini tamamlayacak şekilde kullanamazsınız. Ticari Market SaaS ürünlerine yönelik aboneliklerin faturalandırmasını test etmek üzere tümleştirme korumalı alanı hesabını kullanmak için, bkz. bunun yerine [ticari Market ürünleri için bir korumalı alan aboneliğini etkinleştirme](activate-sandbox-subscription-azure-marketplace-products.md) . Aboneliğin faturalandırılması, başarıyla etkinleştirilmesinden sonra başlayacaktır.

Test çalıştırınızın sonunda temizlemek için, bir sonraki test turunda boşluk olacak şekilde aşağıdaki makalelere bakın:

- [Tümleştirme korumalı alandan bir müşteri hesabını silme](delete-a-customer-account-from-the-integration-sandbox.md)

- [Abonelik miktarını azaltma](change-the-quantity-of-a-subscription.md)

- Aboneliği kaldırabilmeniz için [askıya alın](suspend-a-subscription.md) .

## <a name="best-practices-for-rest-development"></a>REST geliştirmesi için en iyi uygulamalar

- İsteğinizi, yanıtı ve yanıtta HTTP durum kodunda herhangi bir hata olup olmadığını görmek için bir ağ izleme aracı kullanın. Hata işleme hakkında daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

- Iş Ortağı Merkezi REST API yapılan her çağrı için yeni bir bağıntı KIMLIĞI kullanın. Bu uygulama daha iyi günlüğe kaydetmeyi sağlar ve hata ayıklama sırasında yardımcı olur. Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Yaygın REST sorunları için sorun giderme ipuçları

- URL ve API sürümü de dahil olmak üzere tüm üst bilgi özelliklerini gözden geçirin.

- Gerektiğinde özelliklerin eklendiğinden ve doğru biçimlendirildiğinden emin olun.

- Yanlış dizi biçimlendirmesi yaygın bir hatadır.

- **ETags** geçicidir ve sonuç olarak depolanmamalıdır. Bir işlev çağrısı **ETags** gerektirdiğinde, kaynağı yeniden alarak en son **ETags** değerini kullanın. **ETags** değerleri bir dize gibi çift tırnak içine eklenmelidir:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
