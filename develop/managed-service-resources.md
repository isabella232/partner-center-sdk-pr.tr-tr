---
title: Yönetilen hizmet kaynakları
description: Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768861"
---
# <a name="managed-service-resources"></a><span data-ttu-id="bf36f-104">Yönetilen hizmet kaynakları</span><span class="sxs-lookup"><span data-stu-id="bf36f-104">Managed service resources</span></span>

<span data-ttu-id="bf36f-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="bf36f-105">**Applies To**</span></span>

- <span data-ttu-id="bf36f-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bf36f-106">Partner Center</span></span>
- <span data-ttu-id="bf36f-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bf36f-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="bf36f-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bf36f-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="bf36f-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bf36f-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bf36f-110">Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir.</span><span class="sxs-lookup"><span data-stu-id="bf36f-110">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="bf36f-111">İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="bf36f-111">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="bf36f-112">ManagedService</span><span class="sxs-lookup"><span data-stu-id="bf36f-112">ManagedService</span></span>

<span data-ttu-id="bf36f-113">Yönetilen bir hizmeti açıklar.</span><span class="sxs-lookup"><span data-stu-id="bf36f-113">Describes a managed service.</span></span>

| <span data-ttu-id="bf36f-114">Özellik</span><span class="sxs-lookup"><span data-stu-id="bf36f-114">Property</span></span>   | <span data-ttu-id="bf36f-115">Tür</span><span class="sxs-lookup"><span data-stu-id="bf36f-115">Type</span></span>                | <span data-ttu-id="bf36f-116">Description</span><span class="sxs-lookup"><span data-stu-id="bf36f-116">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="bf36f-117">Id</span><span class="sxs-lookup"><span data-stu-id="bf36f-117">Id</span></span>         | <span data-ttu-id="bf36f-118">string</span><span class="sxs-lookup"><span data-stu-id="bf36f-118">string</span></span>              | <span data-ttu-id="bf36f-119">Yönetilen hizmet kimliği.</span><span class="sxs-lookup"><span data-stu-id="bf36f-119">The managed service id.</span></span>                                  |
| <span data-ttu-id="bf36f-120">Name</span><span class="sxs-lookup"><span data-stu-id="bf36f-120">Name</span></span>       | <span data-ttu-id="bf36f-121">string</span><span class="sxs-lookup"><span data-stu-id="bf36f-121">string</span></span>              | <span data-ttu-id="bf36f-122">Yönetilen hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="bf36f-122">The name of the managed service.</span></span>                         |
| <span data-ttu-id="bf36f-123">Adýdýr</span><span class="sxs-lookup"><span data-stu-id="bf36f-123">GroupName</span></span>  | <span data-ttu-id="bf36f-124">string</span><span class="sxs-lookup"><span data-stu-id="bf36f-124">string</span></span>              | <span data-ttu-id="bf36f-125">Hizmetin ait olduğu grubun adı.</span><span class="sxs-lookup"><span data-stu-id="bf36f-125">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="bf36f-126">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="bf36f-126">Links</span></span>      | <span data-ttu-id="bf36f-127">Managedservicelmürekkepler</span><span class="sxs-lookup"><span data-stu-id="bf36f-127">ManagedServiceLinks</span></span> | <span data-ttu-id="bf36f-128">Yönetilen hizmete karşılık gelen kaynak bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="bf36f-128">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="bf36f-129">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="bf36f-129">Attributes</span></span> | <span data-ttu-id="bf36f-130">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="bf36f-130">ResourceAttributes</span></span>  | <span data-ttu-id="bf36f-131">Sözleşmeye karşılık gelen meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="bf36f-131">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="bf36f-132">Managedservicelmürekkepler</span><span class="sxs-lookup"><span data-stu-id="bf36f-132">ManagedServiceLinks</span></span>

<span data-ttu-id="bf36f-133">Hizmet desteği sağlamak için, yetkilendirilmiş yönetici izinlerine sahip ortağa izin veren bağlantıları içerir.</span><span class="sxs-lookup"><span data-stu-id="bf36f-133">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="bf36f-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="bf36f-134">Property</span></span>      | <span data-ttu-id="bf36f-135">Tür</span><span class="sxs-lookup"><span data-stu-id="bf36f-135">Type</span></span> | <span data-ttu-id="bf36f-136">Description</span><span class="sxs-lookup"><span data-stu-id="bf36f-136">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="bf36f-137">AdminService</span><span class="sxs-lookup"><span data-stu-id="bf36f-137">AdminService</span></span>  | <span data-ttu-id="bf36f-138">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="bf36f-138">Link</span></span> | <span data-ttu-id="bf36f-139">Yönetim hizmeti URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="bf36f-139">The admin service URI.</span></span>      |
| <span data-ttu-id="bf36f-140">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="bf36f-140">ServiceHealth</span></span> | <span data-ttu-id="bf36f-141">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="bf36f-141">Link</span></span> | <span data-ttu-id="bf36f-142">Hizmet durumu URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="bf36f-142">The service health URI.</span></span>     |
| <span data-ttu-id="bf36f-143">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="bf36f-143">ServiceTicket</span></span> | <span data-ttu-id="bf36f-144">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="bf36f-144">Link</span></span> | <span data-ttu-id="bf36f-145">Hizmet bileti URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="bf36f-145">The service ticket URI.</span></span>     |
| <span data-ttu-id="bf36f-146">Kendi</span><span class="sxs-lookup"><span data-stu-id="bf36f-146">Self</span></span>          | <span data-ttu-id="bf36f-147">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="bf36f-147">Link</span></span> | <span data-ttu-id="bf36f-148">Self URI.</span><span class="sxs-lookup"><span data-stu-id="bf36f-148">The self URI.</span></span>               |
| <span data-ttu-id="bf36f-149">Sonraki</span><span class="sxs-lookup"><span data-stu-id="bf36f-149">Next</span></span>          | <span data-ttu-id="bf36f-150">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="bf36f-150">Link</span></span> | <span data-ttu-id="bf36f-151">Öğelerin sonraki sayfası.</span><span class="sxs-lookup"><span data-stu-id="bf36f-151">The next page of items.</span></span>     |
| <span data-ttu-id="bf36f-152">Önceki</span><span class="sxs-lookup"><span data-stu-id="bf36f-152">Previous</span></span>      | <span data-ttu-id="bf36f-153">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="bf36f-153">Link</span></span> | <span data-ttu-id="bf36f-154">Öğelerin önceki sayfası.</span><span class="sxs-lookup"><span data-stu-id="bf36f-154">The previous page of items.</span></span> |

