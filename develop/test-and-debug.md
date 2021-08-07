---
title: Tümleştirme korumalı alanıyla test ve hata ayıklama
description: Yanlışlıkla yeni ücretlerle İş Ortağı Merkezi kodunuzu test etmek ve hata ayıklamak için İş Ortağı Merkezi tümleştirme korumalı alan hesabınız (ve ilgili belirteçler) kullanmayı öğrenin.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1a446f1d9a9d7370be2715305ccbaa71b09cfd45957cf8663afb42a23706a7be
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989279"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Beklenmeyen ücretlerden kaçınmak için İş Ortağı Merkezi tümleştirme korumalı alanınız ile test etme ve hata ayıklama

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Kodunuzu test etmek için tümleştirme korumalı alan İş Ortağı Merkezi (ve karşılık gelen belirteçler) kullanarak yanlışlıkla ödemeden şirketin sorumlu olduğu yeni ücretler ödemeniz gerekir. Bu üretimde test (TiP) ortamı hakkında daha fazla bilgi için bkz. [İş Ortağı Merkezi.](set-up-api-access-in-partner-center.md)

## <a name="integration-sandbox-constraints"></a>Tümleştirme korumalı alanı kısıtlamaları

Otomatik derleme doğrulama testleri çalıştıracak, üretimde test gerçekleştirecek veya tümleştirme korumalı alanda el ile test gerçekleştirecek olursanız, tümleştirme korumalı alanı için maksimum sınırlara ulaşabilirsiniz. Bu limitler 75 müşteri, müşteri başına 5 abonelik ve abonelik başına 25 lisanstır.

25 lisans sınırı, korumalı alanda 25 lisansı aşan en düşük lisans gereksinimine sahip bir teklif alamay anlamına gelir. Bu sınırlama denemeleri içerir.

Korumalı Alan ortamlarında çeşitli fatura ve mutabakat dosyaları mevcuttur, ancak bunların hepsi eski veya modern platformlarda kullanılamaz. Daha fazla bilgi için aşağıdaki tabloyu doğrulayın.

| **Dosyalar**                    | **Eski'de kullanılabilir** | **Modern'de kullanılabilir** |
| ---------------------------- | ------------------------ | ------------------------ |
| Fatura PDF dosyası                  | Hayır                       | Yes                      |
| Fatura Mutabakat Dosyası | Hayır                       | Yes                      |
| Fatura Tahmin Dosyası       | Hayır                       | Yes                      |
| Günlük Faturalandırıldı Kullanım Dosyası     | Hayır                       | Yes                      |
| Günlük Bilgisiz Kullanım Dosyası   | Hayır                       | Yes                      |


### <a name="azure-plan"></a>Azure planı

Varsayılan olarak iş ortakları kendi korumalı alan hesaplarını kullanarak Azure planları sağlayamaz. Bunu kendi korumalı alan hesaplarıyla yapması gereken iş ortaklarının erişim için başvurması gerekir. Erişime uygulamak için, Microsoft hesabı yöneticinize veya iş ilgili kişinize ulaşın. Daha önce korumalı alan hesaplarında Microsoft Azure (MS-AZR-0145P) abonelikleri sağlama erişimi için başvuru yapan iş ortaklarının yeniden erişim için başvurması gerekmeyecektir. Bu kullanıcılara Azure planlarını otomatik olarak sağlama erişimi sağlandı.

Korumalı alan hesapları Azure planları sağlama onayına sahip iş ortakları için aşağıdaki sınırlar geçerlidir:

- Her korumalı alan iş ortağı hesabının tüm müşteri kiracılarında (planlar müşteriler arasında nasıl dağıtılır olursa olsun) en fazla 10 Azure planı olabilir.

- Doğrudan fatura iş ortağı müşteri kiracısı başına en fazla bir Azure planı oluşturabilir.

- Dolaylı sağlayıcı, müşteri kiracısı başına en fazla üç Azure planı oluşturabilir (Kayıt İş Ortağı olarak belirtilen farklı dolaylı kurumsal bayiler için).

- Her Azure planı en fazla üç Azure aboneliğine sahip olabilir.

- Korumalı alan hesabınız altındaki her CSP Azure aboneliği, veri merkezi başına dört sanal makine (VM) çekirdeğiyle sınırlıdır. Bu nedenle, dörtten fazla VM çekirdeği gerektiren VM SKUS'ları sağamaz. GPU çekirdekleri gibi belirli özel VM S SU'ları da dışlanır.

- Her korumalı alan iş ortağı hesabının tüm Azure planlarında faturalama döngüsü başına 2000 ABD doları (USD) harcama limiti vardır. İş ortağı harcama sınırına ulaştığında, sonraki faturalama döngüsüne kadar tüm Azure planları geçici olarak devre dışı bırakılır.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Bulut Çözümü Sağlayıcısı (CSP) Azure abonelik teklifleri

CSP Azure abonelik teklifleri artık korumalı alan hesapları için varsayılan olarak kullanılamaz. Bunlar sırasıyla Microsoft Genel Bulut, Almanya Bulutu ve Kamu Bulutu'nun CSP Azure abonelikleri için MS-AZR-0146P, MS-AZR-DE-0146P ve MS-AZR-USGOV-0146P'tir. Korumalı alan hesabıyla bu tekliflere erişmesi gereken iş ortaklarının erişim için başvurması gerekir. Erişime uygulamak için yöneticinizle veya Microsoft hesabı kişisi ile iletişime geçin.

CsP Azure aboneliği teklifleri için korumalı alan hesapları onaylanmış iş ortakları için aşağıdaki sınırlar geçerlidir:

- En fazla 375 etkin aboneliğiniz (müşteri başına 75 müşteri x 5 abonelik) olabilir. Ancak bunlardan yalnızca 10'ları CSP Azure abonelikleri olabilir.

- CSP Azure aboneliği 200 ABD doları Azure kullanımına ulaştığında kaynakları bir sonraki faturalama döngüsüne kadar geçici olarak devre dışı bırakılır. Hala etkin bir abonelik olarak kabul edilir ve 10 etkin Azure aboneliği sınırına dahil edilir.

- Korumalı alan hesabınız altındaki her CSP Azure aboneliği, veri merkezi başına dört sanal makine (VM) çekirdeğiyle sınırlıdır. Bu nedenle, dörtten fazla VM çekirdeği gerektiren VM SKUS'ları sağamaz. GPU çekirdekleri gibi belirli özel VM S SU'ları da dışlanır.

> [!Important]
> 1 Ağustos 2018'den önce korumalı alan hesaplarıyla sağlanan tüm mevcut CSP Azure abonelikleri artık desteklemeyecek ve 16 Ekim - 31 Ekim 2018 tarihleri arasında Microsoft tarafından sağlamaları silinecek. Aboneliklerin sağlandıktan sonra yeniden etkinleştirilemez ve ilişkili verilere artık erişilemez. Bu abonelikler altında depolanan değerli verilere sahip iş ortaklarının 16 Ekim 2018'den önce verileri depolaması gerekir.

### <a name="azure-reserved-vm-instance"></a>Azure Ayrılmış VM örneği

Korumalı alan [hesabınızla bir Azure Ayrılmış VM](purchase-azure-reservations.md) örneği satın alırsanız müşteri başına iki VM örneğiyle sınırlıdır. Ayrıca yalnızca aşağıdaki Azure Ayrılmış VM örneği ürünü SKI'lerinden seçim yapabilirsiniz:

| Ürün Başlığı  | Geçerli Tarih  | Sku Başlığı                                               | Bölge [ArmRegionName] | Örnek Anahtarı [ArmSkuName] | Süre | Tüketim Ölçümü Kimliği       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, KR Güney, 1 yıl    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, ABD Doğu, 1 yıl     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, ABD Batı 2, 1 yıl   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f464029778888 |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, ABD Orta Kuzey, 1 yıl    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B Serisi       | 12/1/2017 0:00  | Ayrılmış VM örneği, Standard_B1s, CA Doğu, 1 yıl     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Ticari market ürünleri için abonelikler

Üretimde, ticari market [SaaS](create-subscription-azure-marketplace-products.md)ürünlerine abonelik oluşturduktan sonra, kurulum işlemini tamamlamak için İş Ortağı Merkezi'den kişiselleştirilmiş etkinleştirme bağlantısını almalı ve yayımcının sitesini ziyaret edebilirsiniz. Abonelik faturalandırması, yalnızca kurulum tamamlandıktan sonra başlayacaktır.

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
