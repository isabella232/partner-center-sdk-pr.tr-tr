---
title: İş Ortağı Merkezi REST API'si referansı
description: CSP iş ortaklarının, müşteri hesaplarını daha iyi yönetmek için CRM ve faturalandırma yazılımlarını Microsoft sistemleriyle tümleştirmeye yönelik Iş Ortağı Merkezi REST API 'Lerini nasıl kullanabileceğinizi öğrenin.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 3f83b2b73c3480f76646cae4fcbbcbacd31d4b3f
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769941"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="022bb-103">İş Ortağı Merkezi REST API REST URL 'Leri, REST üstbilgileri, REST kaynakları ve REST olayları için başvuru</span><span class="sxs-lookup"><span data-stu-id="022bb-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="022bb-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="022bb-104">**Applies to:**</span></span>

- <span data-ttu-id="022bb-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="022bb-105">Partner Center</span></span>
- <span data-ttu-id="022bb-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="022bb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="022bb-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="022bb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="022bb-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="022bb-108">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="022bb-109">İş Ortağı Merkezi REST API</span><span class="sxs-lookup"><span data-stu-id="022bb-109">Partner Center REST API</span></span>

<span data-ttu-id="022bb-110">Iş Ortağı Merkezi REST API, bulut çözümü sağlayıcısı (CSP) iş ortaklarının mevcut CRM veya faturalandırma yazılımlarını müşteri hesaplarını yöneten, sipariş alan ve abonelikleri yöneten ve destek isteklerini işleyecek Microsoft sistemleriyle tümleştirmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="022bb-110">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="022bb-111">Örnek kod dahil olmak üzere API 'nin neler yapabilecekleri hakkında daha fazla bilgi için, arka plana genel bakış da dahil olmak üzere [senaryolar](scenarios.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="022bb-111">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="022bb-112">Kodlamaya başlamadan önce, [kullanmaya](get-started.md) başlama konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="022bb-112">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="022bb-113">Bu makale, test ve üretim hesaplarınızı ayarlama, kimlik doğrulama çalışmasını alma ve örnek kodu bulma hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="022bb-113">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

## <a name="topics"></a><span data-ttu-id="022bb-114">Konu başlıkları</span><span class="sxs-lookup"><span data-stu-id="022bb-114">Topics</span></span>

| <span data-ttu-id="022bb-115">Konu</span><span class="sxs-lookup"><span data-stu-id="022bb-115">Topic</span></span> | <span data-ttu-id="022bb-116">Description</span><span class="sxs-lookup"><span data-stu-id="022bb-116">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="022bb-117">İş Ortağı Merkezi REST URL’leri</span><span class="sxs-lookup"><span data-stu-id="022bb-117">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="022bb-118">Iş Ortağı Merkezi 'nin farklı sürümleri için REST API uç noktalarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="022bb-118">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="022bb-119">İş Ortağı Merkezi REST üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="022bb-119">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="022bb-120">REST API tarafından kullanılan istek ve yanıt üst bilgilerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="022bb-120">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="022bb-121">İş Ortağı Merkezi REST kaynakları</span><span class="sxs-lookup"><span data-stu-id="022bb-121">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="022bb-122">REST API kullanmak için gereken nesneleri temsil eden JSON yapılarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="022bb-122">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="022bb-123">İş Ortağı Merkezi REST olayları</span><span class="sxs-lookup"><span data-stu-id="022bb-123">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="022bb-124">Iş Ortağı Merkezi Web kancaları tarafından desteklenen REST kaynak değişiklik olaylarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="022bb-124">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="022bb-125">İş Ortağı Merkezi tarafından desteklenen diller ve yerel ayarlar</span><span class="sxs-lookup"><span data-stu-id="022bb-125">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="022bb-126">Iş Ortağı Merkezi API 'Lerinde desteklenen yerel ayarları, dilleri ve ülke/bölge kodlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="022bb-126">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="022bb-127">İş Ortağı Merkezi web kancaları</span><span class="sxs-lookup"><span data-stu-id="022bb-127">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="022bb-128">Olayları alma, geri aramanın kimliğini doğrulama ve bir olay kaydı oluşturmak, görüntülemek ve güncelleştirmek için Iş Ortağı Merkezi Web kancası API 'Lerini kullanma.</span><span class="sxs-lookup"><span data-stu-id="022bb-128">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |