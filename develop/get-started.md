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
# <a name="get-started"></a><span data-ttu-id="3706e-103">başlarken</span><span class="sxs-lookup"><span data-stu-id="3706e-103">Get started</span></span>

<span data-ttu-id="3706e-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="3706e-104">**Applies To**</span></span>

- <span data-ttu-id="3706e-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3706e-105">Partner Center</span></span>
- <span data-ttu-id="3706e-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3706e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3706e-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3706e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3706e-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3706e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3706e-109">Iş Ortağı Merkezi SDK 'Sı, yönetilen bir API ve iş ortaklarının müşteri, abonelik ve sipariş verilerini yönetmek için kullanması için bir REST API içerir.</span><span class="sxs-lookup"><span data-stu-id="3706e-109">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="3706e-110">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="3706e-110">Get the code</span></span>

[<span data-ttu-id="3706e-111">Iş Ortağı Merkezi SDK 'sını indirin</span><span class="sxs-lookup"><span data-stu-id="3706e-111">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="3706e-112">Dolaylı satıcılar için Iş Ortağı Merkezi 'ne API erişimi, desteklenen bir senaryo değildir.</span><span class="sxs-lookup"><span data-stu-id="3706e-112">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="3706e-113">Iş Ortağı Merkezi sürümünüzü belirleme</span><span class="sxs-lookup"><span data-stu-id="3706e-113">Determine your version of Partner Center</span></span>

<span data-ttu-id="3706e-114">Iş Ortağı Merkezi 'nin bazı sürümlerinde SDK 'nın tamamı kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="3706e-114">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="3706e-115">Daha fazla bilgi için bkz. [Microsoft Ulusal bulut Için Iş Ortağı Merkezi Için geliştirme](developing-for-partner-center-for-microsoft-national-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="3706e-115">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="3706e-116">Örnekleri alın</span><span class="sxs-lookup"><span data-stu-id="3706e-116">Get the samples</span></span>

<span data-ttu-id="3706e-117">C# parçacıkları, REST örnekleri ve örnek uygulama hakkında daha fazla bilgi için bkz. [Partner Center örnekleri](partner-center-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3706e-117">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="3706e-118">Test ve üretim karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="3706e-118">Test vs. production</span></span>

<span data-ttu-id="3706e-119">Kodunuzu başlangıçta yazarken ve test ederken, yanlışlıkla şirketiniz ödemekten sorumlu yeni ücretler ödemeniz için tümleştirme korumalı alanı hesabınızı (ve ilgili belirteçleri) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3706e-119">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="3706e-120">Bu test ortamı hakkında daha fazla bilgi için bkz. [Iş Ortağı Merkezi 'NDE API erişimi ayarlama](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="3706e-120">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="3706e-121">Çözümünüz test edildiğinde ve gerçek müşteri hesaplarında kullanıma hazırlandığında, birincil Iş Ortağı Merkezi hesabınıza karşılık gelen bir Azure AD istemci uygulaması ve gizli anahtarı kullanmanız için belirteçlerinizi güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3706e-121">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="3706e-122">Test ve hata ayıklama hakkında daha fazla bilgi ve test üretimi (tıp) ve tümleştirme korumalı alanı hakkında daha fazla bilgi için bkz. [test ve hata ayıklama](test-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="3706e-122">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="3706e-123">Kimlik bilgilerinizi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3706e-123">Configure your authentication</span></span>

<span data-ttu-id="3706e-124">Iş Ortağı Merkezi API 'Lerini kullanabilmeniz için Azure AD kimlik doğrulamasını yapılandırmak üzere bkz. [Partner Center kimlik doğrulaması](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3706e-124">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3706e-125">Microsoft, Microsoft Azure Multi-Factor Authentication (MFA) mimarisi aracılığıyla bulut çözümü sağlayıcısı (CSP) iş ortaklarının ve Denetim Masası satıcılarının (CPV) kimlik doğrulaması için güvenli ve ölçeklenebilir bir çerçeve sunuyor.</span><span class="sxs-lookup"><span data-stu-id="3706e-125">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="3706e-126">İş ortağı merkezi kimlik doğrulaması için Azure AD 'yi kullanır ve Iş Ortağı Merkezi API 'Lerini kullanmak için kimlik doğrulama ayarlarınızı doğru şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3706e-126">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="3706e-127">Daha fazla bilgi için bkz. [güvenli uygulama modelini etkinleştirme](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="3706e-127">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="3706e-128">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="3706e-128">Get help</span></span>

<span data-ttu-id="3706e-129">İş ortakları, [Iş ortağı MERKEZI SDK Yammer grubunda](https://go.microsoft.com/fwlink/p/?LinkID=717360)destek alabilir.</span><span class="sxs-lookup"><span data-stu-id="3706e-129">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="3706e-130">Geliştiriciler, daha fazla kişiselleştirilmiş yardım almak için MPN destek avantajlarını veya Premier Destek kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="3706e-130">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="3706e-131">İş Ortağı Merkezi API'si ve SDK Erken Benimseyen Programı'na katılma</span><span class="sxs-lookup"><span data-stu-id="3706e-131">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="3706e-132">Iş ortağı özelliklerinin ve özelliklerinin geliştirilmesi konusunda Microsoft ile nasıl işbirliği yapabileceğiniz hakkında bilgi edinmek için bkz. [Iş Ortağı Merkezi API 'si ve SDK erken benimseyen programı 'Na ekleme](early-adopter-program.md).</span><span class="sxs-lookup"><span data-stu-id="3706e-132">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
