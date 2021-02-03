---
title: İlişkiler kaynakları
description: İlişkilerle ilgili kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768878"
---
# <a name="relationships-resources"></a><span data-ttu-id="befcc-103">İlişkiler kaynakları</span><span class="sxs-lookup"><span data-stu-id="befcc-103">Relationships resources</span></span>

<span data-ttu-id="befcc-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="befcc-104">**Applies To**</span></span>

- <span data-ttu-id="befcc-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="befcc-105">Partner Center</span></span>

<span data-ttu-id="befcc-106">İlişkilerle ilgili kaynakları açıklar.</span><span class="sxs-lookup"><span data-stu-id="befcc-106">Describes resources related to relationships.</span></span>

## <a name="partnerrelationship"></a><span data-ttu-id="befcc-107">PartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="befcc-107">PartnerRelationship</span></span>

<span data-ttu-id="befcc-108">İki iş ortağı arasındaki ilişkiyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="befcc-108">Represents a relationship between two partners.</span></span>

| <span data-ttu-id="befcc-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="befcc-109">Property</span></span>         | <span data-ttu-id="befcc-110">Tür</span><span class="sxs-lookup"><span data-stu-id="befcc-110">Type</span></span>                                                           | <span data-ttu-id="befcc-111">Description</span><span class="sxs-lookup"><span data-stu-id="befcc-111">Description</span></span>                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="befcc-112">kimlik</span><span class="sxs-lookup"><span data-stu-id="befcc-112">id</span></span>               | <span data-ttu-id="befcc-113">string</span><span class="sxs-lookup"><span data-stu-id="befcc-113">string</span></span>                                                         | <span data-ttu-id="befcc-114">İş ortağı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="befcc-114">The partner identifier.</span></span> <span data-ttu-id="befcc-115">İş ortağı tanımlayıcısı, ilişkinin alıcı (Kimden) tarafında olan iş ortağının Kiracı kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="befcc-115">The partner identifier specifies the tenant id of the partner who is in the recipient (from) side of the relationship.</span></span> |
| <span data-ttu-id="befcc-116">location</span><span class="sxs-lookup"><span data-stu-id="befcc-116">location</span></span>         | <span data-ttu-id="befcc-117">string</span><span class="sxs-lookup"><span data-stu-id="befcc-117">string</span></span>                                                         | <span data-ttu-id="befcc-118">İş ortağının konumu.</span><span class="sxs-lookup"><span data-stu-id="befcc-118">The location of the partner.</span></span>                                                                                                                   |
| <span data-ttu-id="befcc-119">Mpnıd</span><span class="sxs-lookup"><span data-stu-id="befcc-119">mpnId</span></span>            | <span data-ttu-id="befcc-120">string</span><span class="sxs-lookup"><span data-stu-id="befcc-120">string</span></span>                                                         | <span data-ttu-id="befcc-121">Ortağın Microsoft İş Ortağı Ağı (MPN) tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="befcc-121">The Microsoft Partner Network (MPN) identifier of the partner.</span></span>                                                                                 |
| <span data-ttu-id="befcc-122">name</span><span class="sxs-lookup"><span data-stu-id="befcc-122">name</span></span>             | <span data-ttu-id="befcc-123">string</span><span class="sxs-lookup"><span data-stu-id="befcc-123">string</span></span>                                                         | <span data-ttu-id="befcc-124">Ortağın adı.</span><span class="sxs-lookup"><span data-stu-id="befcc-124">The name of the partner.</span></span>                                                                                                                       |
| <span data-ttu-id="befcc-125">relationshipType</span><span class="sxs-lookup"><span data-stu-id="befcc-125">relationshipType</span></span> | <span data-ttu-id="befcc-126">string</span><span class="sxs-lookup"><span data-stu-id="befcc-126">string</span></span>                                                         | <span data-ttu-id="befcc-127">İlişki türü.</span><span class="sxs-lookup"><span data-stu-id="befcc-127">The type of relationship.</span></span>                                                                                                                      |
| <span data-ttu-id="befcc-128">state</span><span class="sxs-lookup"><span data-stu-id="befcc-128">state</span></span>            | <span data-ttu-id="befcc-129">string</span><span class="sxs-lookup"><span data-stu-id="befcc-129">string</span></span>                                                         | <span data-ttu-id="befcc-130">İlişkinin durumu (örneğin `active` ).</span><span class="sxs-lookup"><span data-stu-id="befcc-130">The state of the relationship (for example `active`).</span></span>                                                                                                 |
| <span data-ttu-id="befcc-131">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="befcc-131">attributes</span></span>       | [<span data-ttu-id="befcc-132">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="befcc-132">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="befcc-133">Meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="befcc-133">The metadata attributes.</span></span>                                                                                                                       |

## <a name="relationshiprequest"></a><span data-ttu-id="befcc-134">RelationshipRequest</span><span class="sxs-lookup"><span data-stu-id="befcc-134">RelationshipRequest</span></span>

<span data-ttu-id="befcc-135">Müşterinin bir iş ortağıyla ilişki kurabilbileceği URL 'YI sağlar.</span><span class="sxs-lookup"><span data-stu-id="befcc-135">Provides the URL by which a customer can establish a relationship with a partner.</span></span>

| <span data-ttu-id="befcc-136">Özellik</span><span class="sxs-lookup"><span data-stu-id="befcc-136">Property</span></span>   | <span data-ttu-id="befcc-137">Tür</span><span class="sxs-lookup"><span data-stu-id="befcc-137">Type</span></span>                                                           | <span data-ttu-id="befcc-138">Description</span><span class="sxs-lookup"><span data-stu-id="befcc-138">Description</span></span>                   |
|------------|----------------------------------------------------------------|-------------------------------|
| <span data-ttu-id="befcc-139">url</span><span class="sxs-lookup"><span data-stu-id="befcc-139">url</span></span>        | <span data-ttu-id="befcc-140">string</span><span class="sxs-lookup"><span data-stu-id="befcc-140">string</span></span>                                                         | <span data-ttu-id="befcc-141">İlişki isteği URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="befcc-141">The relationship request URL.</span></span> |
| <span data-ttu-id="befcc-142">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="befcc-142">attributes</span></span> | [<span data-ttu-id="befcc-143">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="befcc-143">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="befcc-144">Meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="befcc-144">The metadata attributes.</span></span>      |
