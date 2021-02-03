---
title: CSP müşteri web vitrini
description: Bu örnek Web sitesi kodu, müşterilerin Microsoft ürünlerine abonelik satın almasını sağlamak için çalışan bir çevrimiçi mağaza gösterir.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768800"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="0ab5a-103">CSP müşteri web vitrini</span><span class="sxs-lookup"><span data-stu-id="0ab5a-103">CSP customer web storefront</span></span>

<span data-ttu-id="0ab5a-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-104">**Applies to:**</span></span>

- <span data-ttu-id="0ab5a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0ab5a-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="0ab5a-106">Bu örnek uygulama yalnızca genel Iş Ortağı Merkezi örneği için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0ab5a-106">This sample app applies only to the global instance of Partner Center.</span></span> <span data-ttu-id="0ab5a-107">Microsoft Bulut Almanya için Iş ortağı merkezi veya ABD Kamu kamu Microsoft Bulut için Iş Ortağı Merkezi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0ab5a-107">It does not apply to Partner Center for Microsoft Cloud Germany or to Partner Center for Microsoft Cloud for US Government.</span></span>

<span data-ttu-id="0ab5a-108">[Iş Ortağı Merkezi storefront](https://github.com/Microsoft/Partner-Center-Storefront) , müşterilerin Microsoft ürünlerine abonelik satın almak için kullanabileceği bir çevrimiçi mağaza için **örnek bir Web sitesidir** .</span><span class="sxs-lookup"><span data-stu-id="0ab5a-108">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="0ab5a-109">[Teklifleri yapılandırmak](#configure-offers), [marka eklemek](#configure-branding) ve [ödeme yöntemi eklemek](#configure-payment-types)için bu **örnek kodu** kendi kullanımınıza göre değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ab5a-109">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding) and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="0ab5a-110">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="0ab5a-110">Sample code</span></span>

<span data-ttu-id="0ab5a-111">GitHub 'dan [Iş Ortağı Merkezi storefront örnek kodunu](https://github.com/Microsoft/Partner-Center-Storefront) indirin.</span><span class="sxs-lookup"><span data-stu-id="0ab5a-111">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="0ab5a-112">Kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ab5a-112">Configure authentication</span></span>

<span data-ttu-id="0ab5a-113">Uygulamayı oluşturmadan önce, [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtmak için Web.config dosyasında aşağıdaki değerleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ab5a-113">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0ab5a-114">Erken geliştirme sırasında veya üretimde test için tümleştirme korumalı alan hesabı ayarlarınızı kullanmanız gerekir (tıp).</span><span class="sxs-lookup"><span data-stu-id="0ab5a-114">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="0ab5a-115">**partnerCenter. ApplicationId**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-115">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="0ab5a-116">**partnerCenter. applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-116">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="0ab5a-117">**partnerCenter. Domain**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-117">**partnerCenter.domain**</span></span>
- <span data-ttu-id="0ab5a-118">**webPortal. ClientID**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-118">**webPortal.clientId**</span></span>
- <span data-ttu-id="0ab5a-119">**webPortal. clientSecret**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-119">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="0ab5a-120">**webPortal. Domain**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-120">**webPortal.domain**</span></span>
- <span data-ttu-id="0ab5a-121">**webPortal. Azurestoraygeconnectionstring**</span><span class="sxs-lookup"><span data-stu-id="0ab5a-121">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="0ab5a-122">Teklifleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ab5a-122">Configure offers</span></span>

<span data-ttu-id="0ab5a-123">(**Microsoftoffer**) teklif kümesini **Offercatalogviewmodel** içinde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ab5a-123">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="0ab5a-124">Marka yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ab5a-124">Configure branding</span></span>

<span data-ttu-id="0ab5a-125">Bu örnek Web sitesi, *BrandingConfiguration.cs* ve *PortalBranding.cs*' de aşağıdaki şirket ve marka bilgilerini izler:</span><span class="sxs-lookup"><span data-stu-id="0ab5a-125">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="0ab5a-126">Kuruluş adı</span><span class="sxs-lookup"><span data-stu-id="0ab5a-126">Organization name</span></span>
- <span data-ttu-id="0ab5a-127">Kuruluş logosu</span><span class="sxs-lookup"><span data-stu-id="0ab5a-127">Organization logo</span></span>
- <span data-ttu-id="0ab5a-128">Üst bilgi görüntüsü</span><span class="sxs-lookup"><span data-stu-id="0ab5a-128">Header image</span></span>
- <span data-ttu-id="0ab5a-129">Gizlilik Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="0ab5a-129">Privacy agreement</span></span>
- <span data-ttu-id="0ab5a-130">İlgili kişinin e-posta adresi</span><span class="sxs-lookup"><span data-stu-id="0ab5a-130">Contact email</span></span>
- <span data-ttu-id="0ab5a-131">İrtibat telefon numarası</span><span class="sxs-lookup"><span data-stu-id="0ab5a-131">Contact phone number</span></span>
- <span data-ttu-id="0ab5a-132">Destek e-postası</span><span class="sxs-lookup"><span data-stu-id="0ab5a-132">Support email</span></span>
- <span data-ttu-id="0ab5a-133">Destek telefon numarası</span><span class="sxs-lookup"><span data-stu-id="0ab5a-133">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="0ab5a-134">Ödeme türlerini yapılandır</span><span class="sxs-lookup"><span data-stu-id="0ab5a-134">Configure payment types</span></span>

<span data-ttu-id="0ab5a-135">Uygulama Şu anda *PayPalGateway.cs* içinde uygulanan bir PayPal ağ geçidi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="0ab5a-135">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>