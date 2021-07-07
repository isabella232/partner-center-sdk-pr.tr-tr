---
title: Transferuygunluk kaynakları
description: Bir iş ortağı, bir müşteri aboneliğini başka bir ortağa aktarılacak iş ortağıyla istediğinde bir aktarım oluşturabilir.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530217"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="f74d6-103">Transferuygunluk kaynakları</span><span class="sxs-lookup"><span data-stu-id="f74d6-103">TransferEligibility resources</span></span>

<span data-ttu-id="f74d6-104">Bir iş ortağı, bir müşteri aboneliğini başka bir ortağa aktarılacak iş ortağıyla istediğinde bir aktarım oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="f74d6-104">A partner can create a transfer when a customer requests their subscription with the partner to be transferred to another partner.</span></span> <span data-ttu-id="f74d6-105">Bir aboneliğin aktarılmasının uygun olup olmadığını denetlemek için Transferuygunluk kullanın.</span><span class="sxs-lookup"><span data-stu-id="f74d6-105">Use TransferEligibility to check whether a subscription is eligible to be transferred.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="f74d6-106">Transferuygunluk</span><span class="sxs-lookup"><span data-stu-id="f74d6-106">TransferEligibility</span></span>

<span data-ttu-id="f74d6-107">Bir Transferuygunluk tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f74d6-107">Describes a transferEligibility.</span></span>

| <span data-ttu-id="f74d6-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="f74d6-108">Property</span></span>              | <span data-ttu-id="f74d6-109">Tür</span><span class="sxs-lookup"><span data-stu-id="f74d6-109">Type</span></span>             | <span data-ttu-id="f74d6-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f74d6-110">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="f74d6-111">kimlik</span><span class="sxs-lookup"><span data-stu-id="f74d6-111">id</span></span>                    | <span data-ttu-id="f74d6-112">string</span><span class="sxs-lookup"><span data-stu-id="f74d6-112">string</span></span>           | <span data-ttu-id="f74d6-113">Müşterinin abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="f74d6-113">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="f74d6-114">IBir hal</span><span class="sxs-lookup"><span data-stu-id="f74d6-114">isEligible</span></span>            | <span data-ttu-id="f74d6-115">bool</span><span class="sxs-lookup"><span data-stu-id="f74d6-115">bool</span></span>             | <span data-ttu-id="f74d6-116">Aboneliğin aktarım için uygun olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f74d6-116">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="f74d6-117">Nedeni</span><span class="sxs-lookup"><span data-stu-id="f74d6-117">Reason</span></span>                | <span data-ttu-id="f74d6-118">string</span><span class="sxs-lookup"><span data-stu-id="f74d6-118">string</span></span>           | <span data-ttu-id="f74d6-119">Reason özelliği aboneliğin aktarım için uygun olmadığını açıklar.</span><span class="sxs-lookup"><span data-stu-id="f74d6-119">The reason property explains why the subscription isn't eligible for transfer.</span></span> |