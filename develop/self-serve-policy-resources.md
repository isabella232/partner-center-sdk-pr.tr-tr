---
title: Self Servis Ilkesi kaynakları
description: Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446726"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="cc89f-103">SelfServePolicy kaynağı</span><span class="sxs-lookup"><span data-stu-id="cc89f-103">SelfServePolicy resource</span></span>

<span data-ttu-id="cc89f-104">Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cc89f-104">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="cc89f-105">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="cc89f-105">SelfServePolicy</span></span>

<span data-ttu-id="cc89f-106">Bir sepet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cc89f-106">Describes a cart.</span></span>

| <span data-ttu-id="cc89f-107">Özellik</span><span class="sxs-lookup"><span data-stu-id="cc89f-107">Property</span></span>              | <span data-ttu-id="cc89f-108">Tür</span><span class="sxs-lookup"><span data-stu-id="cc89f-108">Type</span></span>             | <span data-ttu-id="cc89f-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc89f-109">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc89f-110">kimlik</span><span class="sxs-lookup"><span data-stu-id="cc89f-110">id</span></span>                    | <span data-ttu-id="cc89f-111">string</span><span class="sxs-lookup"><span data-stu-id="cc89f-111">string</span></span>           | <span data-ttu-id="cc89f-112">Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan kendi kendine bir ilke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc89f-112">A self-serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="cc89f-113">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="cc89f-113">SelfServeEntity</span></span>       | <span data-ttu-id="cc89f-114">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="cc89f-114">SelfServeEntity</span></span>  | <span data-ttu-id="cc89f-115">Erişim izni verilen self servis varlığı.</span><span class="sxs-lookup"><span data-stu-id="cc89f-115">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="cc89f-116">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="cc89f-116">Grantor</span></span>               | <span data-ttu-id="cc89f-117">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="cc89f-117">Grantor</span></span>          | <span data-ttu-id="cc89f-118">Erişim veren granör.</span><span class="sxs-lookup"><span data-stu-id="cc89f-118">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="cc89f-119">İzinler</span><span class="sxs-lookup"><span data-stu-id="cc89f-119">Permissions</span></span>           | <span data-ttu-id="cc89f-120">Izin dizisi</span><span class="sxs-lookup"><span data-stu-id="cc89f-120">Array of Permission</span></span>| <span data-ttu-id="cc89f-121">[İzin](#permission) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="cc89f-121">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="cc89f-122">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="cc89f-122">SelfServeEntity</span></span>

<span data-ttu-id="cc89f-123">İzin verilen varlığı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="cc89f-123">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="cc89f-124">Özellik</span><span class="sxs-lookup"><span data-stu-id="cc89f-124">Property</span></span>             | <span data-ttu-id="cc89f-125">Tür</span><span class="sxs-lookup"><span data-stu-id="cc89f-125">Type</span></span>|<span data-ttu-id="cc89f-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc89f-126">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc89f-127">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="cc89f-127">SelfServeEntityType</span></span>  | <span data-ttu-id="cc89f-128">string</span><span class="sxs-lookup"><span data-stu-id="cc89f-128">string</span></span>                           | <span data-ttu-id="cc89f-129">Erişim izni verilen varlık, kabul edilen değerler: müşteri.</span><span class="sxs-lookup"><span data-stu-id="cc89f-129">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="cc89f-130">Değerine</span><span class="sxs-lookup"><span data-stu-id="cc89f-130">TenantID</span></span>             | <span data-ttu-id="cc89f-131">string</span><span class="sxs-lookup"><span data-stu-id="cc89f-131">string</span></span>                           | <span data-ttu-id="cc89f-132">Erişim izni verilen varlığın kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc89f-132">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="cc89f-133">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="cc89f-133">Grantor</span></span>

<span data-ttu-id="cc89f-134">İzinleri veren granayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="cc89f-134">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="cc89f-135">Özellik</span><span class="sxs-lookup"><span data-stu-id="cc89f-135">Property</span></span>             | <span data-ttu-id="cc89f-136">Tür</span><span class="sxs-lookup"><span data-stu-id="cc89f-136">Type</span></span>|<span data-ttu-id="cc89f-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc89f-137">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc89f-138">GrantorType</span><span class="sxs-lookup"><span data-stu-id="cc89f-138">GrantorType</span></span>          | <span data-ttu-id="cc89f-139">string</span><span class="sxs-lookup"><span data-stu-id="cc89f-139">string</span></span>                           | <span data-ttu-id="cc89f-140">Erişim verme, kabul edilen değerler: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="cc89f-140">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="cc89f-141">Değerine</span><span class="sxs-lookup"><span data-stu-id="cc89f-141">TenantID</span></span>             | <span data-ttu-id="cc89f-142">string</span><span class="sxs-lookup"><span data-stu-id="cc89f-142">string</span></span>                           | <span data-ttu-id="cc89f-143">Erişim veren varlığın kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc89f-143">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="cc89f-144">İzin</span><span class="sxs-lookup"><span data-stu-id="cc89f-144">Permission</span></span>

<span data-ttu-id="cc89f-145">Self Servis ilkesindeki bir izni temsil eder.</span><span class="sxs-lookup"><span data-stu-id="cc89f-145">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="cc89f-146">Özellik</span><span class="sxs-lookup"><span data-stu-id="cc89f-146">Property</span></span>             | <span data-ttu-id="cc89f-147">Tür</span><span class="sxs-lookup"><span data-stu-id="cc89f-147">Type</span></span>|<span data-ttu-id="cc89f-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc89f-148">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc89f-149">Kaynak</span><span class="sxs-lookup"><span data-stu-id="cc89f-149">Resource</span></span>             | <span data-ttu-id="cc89f-150">string</span><span class="sxs-lookup"><span data-stu-id="cc89f-150">string</span></span>                           | <span data-ttu-id="cc89f-151">Kaynak erişimine çok fazla: Azurereservedınstances verildi.</span><span class="sxs-lookup"><span data-stu-id="cc89f-151">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="cc89f-152">Eylem</span><span class="sxs-lookup"><span data-stu-id="cc89f-152">Action</span></span>               | <span data-ttu-id="cc89f-153">string</span><span class="sxs-lookup"><span data-stu-id="cc89f-153">string</span></span>                           | <span data-ttu-id="cc89f-154">Şu için eylem erişimi verildi: satın alma</span><span class="sxs-lookup"><span data-stu-id="cc89f-154">The action access is being granted for: Purchase</span></span>                                           |
