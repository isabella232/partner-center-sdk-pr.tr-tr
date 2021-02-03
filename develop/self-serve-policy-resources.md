---
title: Self Servis Ilkesi kaynakları
description: Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768951"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="116c0-103">SelfServePolicy kaynağı</span><span class="sxs-lookup"><span data-stu-id="116c0-103">SelfServePolicy resource</span></span>

<span data-ttu-id="116c0-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="116c0-104">**Applies to:**</span></span>

- <span data-ttu-id="116c0-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="116c0-105">Partner Center</span></span>

<span data-ttu-id="116c0-106">Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="116c0-106">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="116c0-107">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="116c0-107">SelfServePolicy</span></span>

<span data-ttu-id="116c0-108">Bir sepet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="116c0-108">Describes a cart.</span></span>

| <span data-ttu-id="116c0-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="116c0-109">Property</span></span>              | <span data-ttu-id="116c0-110">Tür</span><span class="sxs-lookup"><span data-stu-id="116c0-110">Type</span></span>             | <span data-ttu-id="116c0-111">Description</span><span class="sxs-lookup"><span data-stu-id="116c0-111">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="116c0-112">kimlik</span><span class="sxs-lookup"><span data-stu-id="116c0-112">id</span></span>                    | <span data-ttu-id="116c0-113">string</span><span class="sxs-lookup"><span data-stu-id="116c0-113">string</span></span>           | <span data-ttu-id="116c0-114">Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan self servis ilke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="116c0-114">A self serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="116c0-115">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="116c0-115">SelfServeEntity</span></span>       | <span data-ttu-id="116c0-116">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="116c0-116">SelfServeEntity</span></span>  | <span data-ttu-id="116c0-117">Erişim izni verilen self servis varlığı.</span><span class="sxs-lookup"><span data-stu-id="116c0-117">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="116c0-118">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="116c0-118">Grantor</span></span>               | <span data-ttu-id="116c0-119">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="116c0-119">Grantor</span></span>          | <span data-ttu-id="116c0-120">Erişim veren granör.</span><span class="sxs-lookup"><span data-stu-id="116c0-120">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="116c0-121">İzinler</span><span class="sxs-lookup"><span data-stu-id="116c0-121">Permissions</span></span>           | <span data-ttu-id="116c0-122">Izin dizisi</span><span class="sxs-lookup"><span data-stu-id="116c0-122">Array of Permission</span></span>| <span data-ttu-id="116c0-123">[İzin](#permission) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="116c0-123">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="116c0-124">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="116c0-124">SelfServeEntity</span></span>

<span data-ttu-id="116c0-125">İzin verilen varlığı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="116c0-125">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="116c0-126">Özellik</span><span class="sxs-lookup"><span data-stu-id="116c0-126">Property</span></span>             | <span data-ttu-id="116c0-127">Tür</span><span class="sxs-lookup"><span data-stu-id="116c0-127">Type</span></span>|<span data-ttu-id="116c0-128">Description</span><span class="sxs-lookup"><span data-stu-id="116c0-128">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="116c0-129">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="116c0-129">SelfServeEntityType</span></span>  | <span data-ttu-id="116c0-130">string</span><span class="sxs-lookup"><span data-stu-id="116c0-130">string</span></span>                           | <span data-ttu-id="116c0-131">Erişim izni verilen varlık, kabul edilen değerler: müşteri.</span><span class="sxs-lookup"><span data-stu-id="116c0-131">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="116c0-132">Değerine</span><span class="sxs-lookup"><span data-stu-id="116c0-132">TenantID</span></span>             | <span data-ttu-id="116c0-133">string</span><span class="sxs-lookup"><span data-stu-id="116c0-133">string</span></span>                           | <span data-ttu-id="116c0-134">Erişim izni verilen varlığın kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="116c0-134">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="116c0-135">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="116c0-135">Grantor</span></span>

<span data-ttu-id="116c0-136">İzinleri veren granayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="116c0-136">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="116c0-137">Özellik</span><span class="sxs-lookup"><span data-stu-id="116c0-137">Property</span></span>             | <span data-ttu-id="116c0-138">Tür</span><span class="sxs-lookup"><span data-stu-id="116c0-138">Type</span></span>|<span data-ttu-id="116c0-139">Description</span><span class="sxs-lookup"><span data-stu-id="116c0-139">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="116c0-140">GrantorType</span><span class="sxs-lookup"><span data-stu-id="116c0-140">GrantorType</span></span>          | <span data-ttu-id="116c0-141">string</span><span class="sxs-lookup"><span data-stu-id="116c0-141">string</span></span>                           | <span data-ttu-id="116c0-142">Erişim verme, kabul edilen değerler: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="116c0-142">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="116c0-143">Değerine</span><span class="sxs-lookup"><span data-stu-id="116c0-143">TenantID</span></span>             | <span data-ttu-id="116c0-144">string</span><span class="sxs-lookup"><span data-stu-id="116c0-144">string</span></span>                           | <span data-ttu-id="116c0-145">Erişim veren varlığın kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="116c0-145">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="116c0-146">İzin</span><span class="sxs-lookup"><span data-stu-id="116c0-146">Permission</span></span>

<span data-ttu-id="116c0-147">Self Servis ilkesindeki bir izni temsil eder.</span><span class="sxs-lookup"><span data-stu-id="116c0-147">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="116c0-148">Özellik</span><span class="sxs-lookup"><span data-stu-id="116c0-148">Property</span></span>             | <span data-ttu-id="116c0-149">Tür</span><span class="sxs-lookup"><span data-stu-id="116c0-149">Type</span></span>|<span data-ttu-id="116c0-150">Description</span><span class="sxs-lookup"><span data-stu-id="116c0-150">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="116c0-151">Kaynak</span><span class="sxs-lookup"><span data-stu-id="116c0-151">Resource</span></span>             | <span data-ttu-id="116c0-152">string</span><span class="sxs-lookup"><span data-stu-id="116c0-152">string</span></span>                           | <span data-ttu-id="116c0-153">Kaynak erişimine çok fazla: Azurereservedınstances verildi.</span><span class="sxs-lookup"><span data-stu-id="116c0-153">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="116c0-154">Eylem</span><span class="sxs-lookup"><span data-stu-id="116c0-154">Action</span></span>               | <span data-ttu-id="116c0-155">string</span><span class="sxs-lookup"><span data-stu-id="116c0-155">string</span></span>                           | <span data-ttu-id="116c0-156">Şu için eylem erişimi verildi: satın alma</span><span class="sxs-lookup"><span data-stu-id="116c0-156">The action access is being granted for: Purchase</span></span>                                           |
