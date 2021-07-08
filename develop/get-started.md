---
title: başlarken
description: Bu İş Ortağı Merkezi SDK'sı müşteri, abonelik ve sipariş verilerini yönetmek REST API iş ortaklarının kullanabileceği bir api ve yönetilen API içerir.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b5d05f26d63574ef876519091dc1c33c05f36e25
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548762"
---
# <a name="get-started"></a><span data-ttu-id="a7641-103">başlarken</span><span class="sxs-lookup"><span data-stu-id="a7641-103">Get started</span></span>

<span data-ttu-id="a7641-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a7641-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a7641-105">Bu İş Ortağı Merkezi SDK'sı müşteri, abonelik ve sipariş verilerini yönetmek REST API iş ortaklarının kullanabileceği bir api ve yönetilen API içerir.</span><span class="sxs-lookup"><span data-stu-id="a7641-105">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="a7641-106">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="a7641-106">Get the code</span></span>

[<span data-ttu-id="a7641-107">Uygulamayı İş Ortağı Merkezi SDK'sı</span><span class="sxs-lookup"><span data-stu-id="a7641-107">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="a7641-108">Dolaylı kurumsal İş Ortağı Merkezi api erişimi desteklenen bir senaryo değildir.</span><span class="sxs-lookup"><span data-stu-id="a7641-108">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="a7641-109">İş Ortağı Merkezi sürümü İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a7641-109">Determine your version of Partner Center</span></span>

<span data-ttu-id="a7641-110">Bazı İş Ortağı Merkezi SDK'nın tamamı mevcut değildir.</span><span class="sxs-lookup"><span data-stu-id="a7641-110">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="a7641-111">Daha fazla bilgi için [bkz. Microsoft Ulusal İş Ortağı Merkezi için geliştirme.](developing-for-partner-center-for-microsoft-national-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="a7641-111">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="a7641-112">Örnekleri alın</span><span class="sxs-lookup"><span data-stu-id="a7641-112">Get the samples</span></span>

<span data-ttu-id="a7641-113">C# kod parçacıkları, REST örnekleri ve örnek uygulama hakkında daha fazla bilgi için [bkz. İş Ortağı Merkezi örnekleri.](partner-center-samples.md)</span><span class="sxs-lookup"><span data-stu-id="a7641-113">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="a7641-114">Test ve üretim</span><span class="sxs-lookup"><span data-stu-id="a7641-114">Test vs. production</span></span>

<span data-ttu-id="a7641-115">Kodunuzu yazarken ve test ederken, yanlışlıkla şirketin ödemeden sorumlu olduğu yeni ücretler ödemeden önce tümleştirme korumalı alan hesabınız (ve buna karşılık gelen belirteçler) kullansanız iyi olur.</span><span class="sxs-lookup"><span data-stu-id="a7641-115">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="a7641-116">Bu test ortamı hakkında daha fazla bilgi için bkz. Api [erişimini İş Ortağı Merkezi.](set-up-api-access-in-partner-center.md)</span><span class="sxs-lookup"><span data-stu-id="a7641-116">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="a7641-117">Çözümünüz test edildi ve gerçek müşteri hesaplarda kullanıma hazır olduğunda, Azure AD istemci uygulamasını ve Birincil hesap hesabınıza karşılık gelen gizli bir gizli anahtar kullanmak için belirteçlerinizi güncelleştirmeniz İş Ortağı Merkezi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7641-117">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="a7641-118">Üretimde Test (TiP) ve Tümleştirme Korumalı Alanı hakkında daha fazla bilgi dahil olmak üzere test ve hata ayıklama hakkında ipuçları ve öneriler için bkz. Test ve [hata ayıklama.](test-and-debug.md)</span><span class="sxs-lookup"><span data-stu-id="a7641-118">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="a7641-119">Kimlik doğrulamanızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7641-119">Configure your authentication</span></span>

<span data-ttu-id="a7641-120">İş Ortağı Merkezi API'lerini kullanmak üzere Azure AD kimlik doğrulamanızı yapılandırmak için [bkz. İş Ortağı Merkezi doğrulaması.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a7641-120">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7641-121">Microsoft, çok faktörlü kimlik doğrulaması (MFA) mimarisi aracılığıyla bulut çözümü sağlayıcısı (CSP) iş ortaklarının ve denetim masası satıcılarının (CPV) Microsoft Azure güvenli ve ölçeklenebilir bir çerçeve sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a7641-121">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="a7641-122">İş Ortağı Merkezi kimlik doğrulaması için Azure AD'yi ve İş Ortağı Merkezi API'lerini kullanmak için kimlik doğrulama ayarlarınızı doğru yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7641-122">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="a7641-123">Daha fazla bilgi için [bkz. Güvenli uygulama modelini etkinleştirme.](enable-secure-app-model.md)</span><span class="sxs-lookup"><span data-stu-id="a7641-123">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="a7641-124">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="a7641-124">Get help</span></span>

<span data-ttu-id="a7641-125">İş ortakları, iş ortakları İş Ortağı Merkezi SDK'sı Yammer [olabilir.](https://go.microsoft.com/fwlink/p/?LinkID=717360)</span><span class="sxs-lookup"><span data-stu-id="a7641-125">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="a7641-126">Geliştiriciler daha kişiselleştirilmiş yardım almak için MPN destek avantajlarını veya destek avantajlarını Premier Destek.</span><span class="sxs-lookup"><span data-stu-id="a7641-126">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="a7641-127">İş Ortağı Merkezi API'si ve SDK Erken Benimseyen Programı'na katılma</span><span class="sxs-lookup"><span data-stu-id="a7641-127">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="a7641-128">İş ortağı özellikleri ve özelliklerinin geliştirilmesinde Microsoft ile nasıl işbirliği yap bulunabilirsiniz? için bkz. [İş Ortağı Merkezi API'si ve SDK Erken Benimseyen Programı'ne katılma.](early-adopter-program.md)</span><span class="sxs-lookup"><span data-stu-id="a7641-128">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
