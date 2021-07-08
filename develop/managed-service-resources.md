---
title: Yönetilen hizmet kaynakları
description: Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548133"
---
# <a name="managed-service-resources"></a><span data-ttu-id="d9776-104">Yönetilen hizmet kaynakları</span><span class="sxs-lookup"><span data-stu-id="d9776-104">Managed service resources</span></span>

<span data-ttu-id="d9776-105">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d9776-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d9776-106">Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir.</span><span class="sxs-lookup"><span data-stu-id="d9776-106">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="d9776-107">İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d9776-107">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="d9776-108">ManagedService</span><span class="sxs-lookup"><span data-stu-id="d9776-108">ManagedService</span></span>

<span data-ttu-id="d9776-109">Yönetilen bir hizmeti açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9776-109">Describes a managed service.</span></span>

| <span data-ttu-id="d9776-110">Özellik</span><span class="sxs-lookup"><span data-stu-id="d9776-110">Property</span></span>   | <span data-ttu-id="d9776-111">Tür</span><span class="sxs-lookup"><span data-stu-id="d9776-111">Type</span></span>                | <span data-ttu-id="d9776-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d9776-112">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="d9776-113">Id</span><span class="sxs-lookup"><span data-stu-id="d9776-113">Id</span></span>         | <span data-ttu-id="d9776-114">string</span><span class="sxs-lookup"><span data-stu-id="d9776-114">string</span></span>              | <span data-ttu-id="d9776-115">Yönetilen hizmet KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d9776-115">The managed service ID.</span></span>                                  |
| <span data-ttu-id="d9776-116">Name</span><span class="sxs-lookup"><span data-stu-id="d9776-116">Name</span></span>       | <span data-ttu-id="d9776-117">string</span><span class="sxs-lookup"><span data-stu-id="d9776-117">string</span></span>              | <span data-ttu-id="d9776-118">Yönetilen hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="d9776-118">The name of the managed service.</span></span>                         |
| <span data-ttu-id="d9776-119">Adýdýr</span><span class="sxs-lookup"><span data-stu-id="d9776-119">GroupName</span></span>  | <span data-ttu-id="d9776-120">string</span><span class="sxs-lookup"><span data-stu-id="d9776-120">string</span></span>              | <span data-ttu-id="d9776-121">Hizmetin ait olduğu grubun adı.</span><span class="sxs-lookup"><span data-stu-id="d9776-121">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="d9776-122">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="d9776-122">Links</span></span>      | <span data-ttu-id="d9776-123">Managedservicelmürekkepler</span><span class="sxs-lookup"><span data-stu-id="d9776-123">ManagedServiceLinks</span></span> | <span data-ttu-id="d9776-124">Yönetilen hizmete karşılık gelen kaynak bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="d9776-124">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="d9776-125">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="d9776-125">Attributes</span></span> | <span data-ttu-id="d9776-126">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="d9776-126">ResourceAttributes</span></span>  | <span data-ttu-id="d9776-127">Sözleşmeye karşılık gelen meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="d9776-127">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="d9776-128">Managedservicelmürekkepler</span><span class="sxs-lookup"><span data-stu-id="d9776-128">ManagedServiceLinks</span></span>

<span data-ttu-id="d9776-129">Hizmet desteği sağlamak için, yetkilendirilmiş yönetici izinlerine sahip ortağa izin veren bağlantıları içerir.</span><span class="sxs-lookup"><span data-stu-id="d9776-129">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="d9776-130">Özellik</span><span class="sxs-lookup"><span data-stu-id="d9776-130">Property</span></span>      | <span data-ttu-id="d9776-131">Tür</span><span class="sxs-lookup"><span data-stu-id="d9776-131">Type</span></span> | <span data-ttu-id="d9776-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d9776-132">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="d9776-133">AdminService</span><span class="sxs-lookup"><span data-stu-id="d9776-133">AdminService</span></span>  | <span data-ttu-id="d9776-134">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="d9776-134">Link</span></span> | <span data-ttu-id="d9776-135">Yönetim hizmeti URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="d9776-135">The admin service URI.</span></span>      |
| <span data-ttu-id="d9776-136">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="d9776-136">ServiceHealth</span></span> | <span data-ttu-id="d9776-137">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="d9776-137">Link</span></span> | <span data-ttu-id="d9776-138">Hizmet durumu URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="d9776-138">The service health URI.</span></span>     |
| <span data-ttu-id="d9776-139">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="d9776-139">ServiceTicket</span></span> | <span data-ttu-id="d9776-140">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="d9776-140">Link</span></span> | <span data-ttu-id="d9776-141">Hizmet bileti URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="d9776-141">The service ticket URI.</span></span>     |
| <span data-ttu-id="d9776-142">Kendi</span><span class="sxs-lookup"><span data-stu-id="d9776-142">Self</span></span>          | <span data-ttu-id="d9776-143">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="d9776-143">Link</span></span> | <span data-ttu-id="d9776-144">Self-URI.</span><span class="sxs-lookup"><span data-stu-id="d9776-144">The self-URI.</span></span>               |
| <span data-ttu-id="d9776-145">Sonraki</span><span class="sxs-lookup"><span data-stu-id="d9776-145">Next</span></span>          | <span data-ttu-id="d9776-146">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="d9776-146">Link</span></span> | <span data-ttu-id="d9776-147">Öğelerin sonraki sayfası.</span><span class="sxs-lookup"><span data-stu-id="d9776-147">The next page of items.</span></span>     |
| <span data-ttu-id="d9776-148">Önceki</span><span class="sxs-lookup"><span data-stu-id="d9776-148">Previous</span></span>      | <span data-ttu-id="d9776-149">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="d9776-149">Link</span></span> | <span data-ttu-id="d9776-150">Öğelerin önceki sayfası.</span><span class="sxs-lookup"><span data-stu-id="d9776-150">The previous page of items.</span></span> |

