---
title: İş Ortağı Merkezi REST API'si referansı
description: CSP iş ortaklarının müşteri hesaplarını daha İş Ortağı Merkezi için CRM ve faturalama yazılımlarını Microsoft sistemleriyle tümleştirip REST API'lerini nasıl kullanabileceğini öğrenin.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 18621fdb94f91f066b69a11f7d557410d653787e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548048"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="b7da3-103">İş Ortağı Merkezi REST API REST URL'leri, REST üst bilgileri, REST kaynakları ve REST olayları için başvuru</span><span class="sxs-lookup"><span data-stu-id="b7da3-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="b7da3-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b7da3-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="b7da3-105">İş Ortağı Merkezi REST API</span><span class="sxs-lookup"><span data-stu-id="b7da3-105">Partner Center REST API</span></span>

<span data-ttu-id="b7da3-106">Bu İş Ortağı Merkezi REST API (CSP) Bulut Çözümü Sağlayıcısı mevcut CRM veya faturalama yazılımlarını müşteri hesaplarını yöneten, siparişler alan, abonelikleri yöneten ve destek isteklerini ele alan Microsoft sistemleriyle tümleştirilmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b7da3-106">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="b7da3-107">Örnek kod da dahil olmak üzere API'nin neler yapaları hakkında daha fazla bilgi için arka plana genel [bakış](scenarios.md) da dahil olmak üzere Senaryolar konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="b7da3-107">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="b7da3-108">Kodlamaya başlamadan önce aşağıdaki [Kullanmaya başlayın](get-started.md) okuyun.</span><span class="sxs-lookup"><span data-stu-id="b7da3-108">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="b7da3-109">Bu makale, test ve üretim hesaplarınızı ayarlama, kimlik doğrulamasının nasıl çalıştığını alma ve örnek kodu bulma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="b7da3-109">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

<span data-ttu-id="b7da3-110">Her API'yi açıklayan bir başvuru kılavuzu için bkz. [İş Ortağı Merkezi REST API.](/rest/api/partner-center-rest/)</span><span class="sxs-lookup"><span data-stu-id="b7da3-110">For a reference guide explaining each API, see [Partner Center REST API](/rest/api/partner-center-rest/).</span></span>

## <a name="topics"></a><span data-ttu-id="b7da3-111">Konu başlıkları</span><span class="sxs-lookup"><span data-stu-id="b7da3-111">Topics</span></span>

| <span data-ttu-id="b7da3-112">Konu</span><span class="sxs-lookup"><span data-stu-id="b7da3-112">Topic</span></span> | <span data-ttu-id="b7da3-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7da3-113">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="b7da3-114">İş Ortağı Merkezi REST API</span><span class="sxs-lookup"><span data-stu-id="b7da3-114">Partner Center REST API</span></span>](/rest/api/partner-center-rest/) | <span data-ttu-id="b7da3-115">Kullanılabilir her bir REST API başvurusu İş Ortağı Merkezi.</span><span class="sxs-lookup"><span data-stu-id="b7da3-115">Reference of each REST API available for Partner Center.</span></span> |
| [<span data-ttu-id="b7da3-116">İş Ortağı Merkezi REST URL’leri</span><span class="sxs-lookup"><span data-stu-id="b7da3-116">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="b7da3-117">Farklı REST API sürümleri için uç noktaları tanımlar İş Ortağı Merkezi.</span><span class="sxs-lookup"><span data-stu-id="b7da3-117">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="b7da3-118">İş Ortağı Merkezi REST üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="b7da3-118">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="b7da3-119">Uygulama tarafından kullanılan istek ve yanıt üst bilgilerini REST API.</span><span class="sxs-lookup"><span data-stu-id="b7da3-119">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="b7da3-120">İş Ortağı Merkezi REST kaynakları</span><span class="sxs-lookup"><span data-stu-id="b7da3-120">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="b7da3-121">REST API'ı kullanmak için gereken nesneleri temsil eden JSON REST API.</span><span class="sxs-lookup"><span data-stu-id="b7da3-121">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="b7da3-122">İş Ortağı Merkezi REST olayları</span><span class="sxs-lookup"><span data-stu-id="b7da3-122">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="b7da3-123">Web kancaları tarafından desteklenen REST kaynak değişikliği İş Ortağı Merkezi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7da3-123">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="b7da3-124">İş Ortağı Merkezi tarafından desteklenen diller ve yerel ayarlar</span><span class="sxs-lookup"><span data-stu-id="b7da3-124">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="b7da3-125">Yerel API'lerde desteklenen yerel kodları, dilleri ve ülke/bölge kodlarını İş Ortağı Merkezi listeler.</span><span class="sxs-lookup"><span data-stu-id="b7da3-125">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="b7da3-126">İş Ortağı Merkezi web kancaları</span><span class="sxs-lookup"><span data-stu-id="b7da3-126">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="b7da3-127">Olay kaydı oluşturmak, görüntülemek ve güncelleştirmek için olayları alma, geri İş Ortağı Merkezi kimliğini doğrulama ve web kancası API'lerini kullanma.</span><span class="sxs-lookup"><span data-stu-id="b7da3-127">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |
