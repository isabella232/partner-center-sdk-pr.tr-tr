---
title: CSP müşteri web vitrini
description: Bu örnek web sitesi kodu, müşterilerin Microsoft ürünlerine abonelik satın almaları için çalışan bir çevrimiçi mağaza gösterir.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d68f17d707731f426cb980a566b6478790d3507c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973341"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="9e53e-103">CSP müşteri web vitrini</span><span class="sxs-lookup"><span data-stu-id="9e53e-103">CSP customer web storefront</span></span>

<span data-ttu-id="9e53e-104">**Için geçerlidir:** İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9e53e-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="9e53e-105">**Için geçerli değildir:** İş Ortağı Merkezi Microsoft Bulut Almanya | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9e53e-105">**Does not apply to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9e53e-106">Bu örnek uygulama yalnızca uygulamanın genel İş Ortağı Merkezi.</span><span class="sxs-lookup"><span data-stu-id="9e53e-106">This sample app applies only to the global instance of Partner Center.</span></span>

<span data-ttu-id="9e53e-107">Bu [İş Ortağı Merkezi, müşterilerin](https://github.com/Microsoft/Partner-Center-Storefront) Microsoft **ürünlerine abonelik** satın almak için kullanabileceği bir çevrimiçi mağazanın örnek web sitesidir.</span><span class="sxs-lookup"><span data-stu-id="9e53e-107">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="9e53e-108">Teklifleri yapılandırmak, **marka eklemek** ve bir ödeme yöntemi eklemek için bu örnek [kodu](#configure-branding)kendi [kullanımınız için değiştirebilirsiniz.](#configure-payment-types) [](#configure-offers)</span><span class="sxs-lookup"><span data-stu-id="9e53e-108">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding), and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="9e53e-109">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="9e53e-109">Sample code</span></span>

<span data-ttu-id="9e53e-110">[GitHub'den İş Ortağı Merkezi vitrin](https://github.com/Microsoft/Partner-Center-Storefront) örnek kodunu GitHub.</span><span class="sxs-lookup"><span data-stu-id="9e53e-110">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="9e53e-111">Kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e53e-111">Configure authentication</span></span>

<span data-ttu-id="9e53e-112">Uygulamayı derlemeden önce, Web.config dosyasındaki aşağıdaki değerleri, kimlik doğrulamasında oluşturduğunuz Azure AD kimlik doğrulaması [bilgilerini İş Ortağı Merkezi güncelleştirin.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9e53e-112">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e53e-113">Tümleştirme korumalı alan hesabı ayarlarınızı erken geliştirme sırasında veya üretimde (TiP) test etmek için kullansanız iyi olur.</span><span class="sxs-lookup"><span data-stu-id="9e53e-113">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="9e53e-114">**partnerCenter.applicationId**</span><span class="sxs-lookup"><span data-stu-id="9e53e-114">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="9e53e-115">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="9e53e-115">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="9e53e-116">**partnerCenter.domain**</span><span class="sxs-lookup"><span data-stu-id="9e53e-116">**partnerCenter.domain**</span></span>
- <span data-ttu-id="9e53e-117">**webPortal.clientId**</span><span class="sxs-lookup"><span data-stu-id="9e53e-117">**webPortal.clientId**</span></span>
- <span data-ttu-id="9e53e-118">**webPortal.clientSecret**</span><span class="sxs-lookup"><span data-stu-id="9e53e-118">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="9e53e-119">**webPortal.domain**</span><span class="sxs-lookup"><span data-stu-id="9e53e-119">**webPortal.domain**</span></span>
- <span data-ttu-id="9e53e-120">**webPortal.azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="9e53e-120">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="9e53e-121">Teklifleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e53e-121">Configure offers</span></span>

<span data-ttu-id="9e53e-122">Teklif kümelerini (**MicrosoftOffer)** **OfferCatalogViewModel içinde yapılandırabilirsiniz.**</span><span class="sxs-lookup"><span data-stu-id="9e53e-122">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="9e53e-123">Markayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e53e-123">Configure branding</span></span>

<span data-ttu-id="9e53e-124">Bu örnek web sitesi, *BrandingConfiguration.cs* ve *PortalBranding.cs* içinde aşağıdaki şirket ve marka bilgilerini izler:</span><span class="sxs-lookup"><span data-stu-id="9e53e-124">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="9e53e-125">Kuruluş adı</span><span class="sxs-lookup"><span data-stu-id="9e53e-125">Organization name</span></span>
- <span data-ttu-id="9e53e-126">Kuruluş logosu</span><span class="sxs-lookup"><span data-stu-id="9e53e-126">Organization logo</span></span>
- <span data-ttu-id="9e53e-127">Üst bilgi görüntüsü</span><span class="sxs-lookup"><span data-stu-id="9e53e-127">Header image</span></span>
- <span data-ttu-id="9e53e-128">Gizlilik sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="9e53e-128">Privacy agreement</span></span>
- <span data-ttu-id="9e53e-129">İlgili kişinin e-posta adresi</span><span class="sxs-lookup"><span data-stu-id="9e53e-129">Contact email</span></span>
- <span data-ttu-id="9e53e-130">İletişim telefon numarası</span><span class="sxs-lookup"><span data-stu-id="9e53e-130">Contact phone number</span></span>
- <span data-ttu-id="9e53e-131">Destek e-postası</span><span class="sxs-lookup"><span data-stu-id="9e53e-131">Support email</span></span>
- <span data-ttu-id="9e53e-132">Destek telefon numarası</span><span class="sxs-lookup"><span data-stu-id="9e53e-132">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="9e53e-133">Ödeme türlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e53e-133">Configure payment types</span></span>

<span data-ttu-id="9e53e-134">Uygulama şu anda *PayPalGateway.cs* PayPal bir ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e53e-134">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>