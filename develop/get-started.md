---
title: başlarken
description: Iş Ortağı Merkezi SDK 'Sı, yönetilen bir API ve iş ortaklarının müşteri, abonelik ve sipariş verilerini yönetmek için kullanması için bir REST API içerir.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c2af1e11dbda19489a27e37c7f3de8ede90fd1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769058"
---
# <a name="get-started"></a>başlarken

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Iş Ortağı Merkezi SDK 'Sı, yönetilen bir API ve iş ortaklarının müşteri, abonelik ve sipariş verilerini yönetmek için kullanması için bir REST API içerir.

## <a name="get-the-code"></a>Kodu alma

[Iş Ortağı Merkezi SDK 'sını indirin](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> Dolaylı satıcılar için Iş Ortağı Merkezi 'ne API erişimi, desteklenen bir senaryo değildir.

## <a name="determine-your-version-of-partner-center"></a>Iş Ortağı Merkezi sürümünüzü belirleme

Iş Ortağı Merkezi 'nin bazı sürümlerinde SDK 'nın tamamı kullanılabilir değildir. Daha fazla bilgi için bkz. [Microsoft Ulusal bulut Için Iş Ortağı Merkezi Için geliştirme](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="get-the-samples"></a>Örnekleri alın

C# parçacıkları, REST örnekleri ve örnek uygulama hakkında daha fazla bilgi için bkz. [Partner Center örnekleri](partner-center-samples.md).

## <a name="test-vs-production"></a>Test ve üretim karşılaştırması

Kodunuzu başlangıçta yazarken ve test ederken, yanlışlıkla şirketiniz ödemekten sorumlu yeni ücretler ödemeniz için tümleştirme korumalı alanı hesabınızı (ve ilgili belirteçleri) kullanmanız gerekir. Bu test ortamı hakkında daha fazla bilgi için bkz. [Iş Ortağı Merkezi 'NDE API erişimi ayarlama](set-up-api-access-in-partner-center.md).

Çözümünüz test edildiğinde ve gerçek müşteri hesaplarında kullanıma hazırlandığında, birincil Iş Ortağı Merkezi hesabınıza karşılık gelen bir Azure AD istemci uygulaması ve gizli anahtarı kullanmanız için belirteçlerinizi güncelleştirmeniz gerekir.

Test ve hata ayıklama hakkında daha fazla bilgi ve test üretimi (tıp) ve tümleştirme korumalı alanı hakkında daha fazla bilgi için bkz. [test ve hata ayıklama](test-and-debug.md).

## <a name="configure-your-authentication"></a>Kimlik bilgilerinizi yapılandırma

Iş Ortağı Merkezi API 'Lerini kullanabilmeniz için Azure AD kimlik doğrulamasını yapılandırmak üzere bkz. [Partner Center kimlik doğrulaması](partner-center-authentication.md).

> [!IMPORTANT]
> Microsoft, Microsoft Azure Multi-Factor Authentication (MFA) mimarisi aracılığıyla bulut çözümü sağlayıcısı (CSP) iş ortaklarının ve Denetim Masası satıcılarının (CPV) kimlik doğrulaması için güvenli ve ölçeklenebilir bir çerçeve sunuyor.
İş ortağı merkezi kimlik doğrulaması için Azure AD 'yi kullanır ve Iş Ortağı Merkezi API 'Lerini kullanmak için kimlik doğrulama ayarlarınızı doğru şekilde yapılandırmanız gerekir.
>
> Daha fazla bilgi için bkz. [güvenli uygulama modelini etkinleştirme](enable-secure-app-model.md).

## <a name="get-help"></a>Yardım alın

İş ortakları, [Iş ortağı MERKEZI SDK Yammer grubunda](https://go.microsoft.com/fwlink/p/?LinkID=717360)destek alabilir. Geliştiriciler, daha fazla kişiselleştirilmiş yardım almak için MPN destek avantajlarını veya Premier Destek kullanabilir.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>İş Ortağı Merkezi API'si ve SDK Erken Benimseyen Programı'na katılma

Iş ortağı özelliklerinin ve özelliklerinin geliştirilmesi konusunda Microsoft ile nasıl işbirliği yapabileceğiniz hakkında bilgi edinmek için bkz. [Iş Ortağı Merkezi API 'si ve SDK erken benimseyen programı 'Na ekleme](early-adopter-program.md).
