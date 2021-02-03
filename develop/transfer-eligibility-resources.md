---
title: Transferuygunluk kaynakları
description: Bir iş ortağı, bir müşteri aboneliğini başka bir iş ortağına aktarmaya istediğinde bir aktarım oluşturur.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768962"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="03cc4-103">Transferuygunluk kaynakları</span><span class="sxs-lookup"><span data-stu-id="03cc4-103">TransferEligibility resources</span></span>

<span data-ttu-id="03cc4-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="03cc4-104">**Applies to:**</span></span>

- <span data-ttu-id="03cc4-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="03cc4-105">Partner Center</span></span>

<span data-ttu-id="03cc4-106">Bir iş ortağı, bir müşteri aboneliğini başka bir iş ortağına aktarmaya istediğinde bir aktarım oluşturur.</span><span class="sxs-lookup"><span data-stu-id="03cc4-106">A partner creates a transfer when a customer wants their subscription with the partner to be transferred to another partner.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="03cc4-107">Transferuygunluk</span><span class="sxs-lookup"><span data-stu-id="03cc4-107">TransferEligibility</span></span>

<span data-ttu-id="03cc4-108">Bir Transferuygunluk tanımlar.</span><span class="sxs-lookup"><span data-stu-id="03cc4-108">Describes a transferEligibility.</span></span>

| <span data-ttu-id="03cc4-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="03cc4-109">Property</span></span>              | <span data-ttu-id="03cc4-110">Tür</span><span class="sxs-lookup"><span data-stu-id="03cc4-110">Type</span></span>             | <span data-ttu-id="03cc4-111">Description</span><span class="sxs-lookup"><span data-stu-id="03cc4-111">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="03cc4-112">kimlik</span><span class="sxs-lookup"><span data-stu-id="03cc4-112">id</span></span>                    | <span data-ttu-id="03cc4-113">string</span><span class="sxs-lookup"><span data-stu-id="03cc4-113">string</span></span>           | <span data-ttu-id="03cc4-114">Müşterinin abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="03cc4-114">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="03cc4-115">IBir hal</span><span class="sxs-lookup"><span data-stu-id="03cc4-115">isEligible</span></span>            | <span data-ttu-id="03cc4-116">bool</span><span class="sxs-lookup"><span data-stu-id="03cc4-116">bool</span></span>             | <span data-ttu-id="03cc4-117">Aboneliğin aktarım için uygun olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="03cc4-117">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="03cc4-118">Nedeni</span><span class="sxs-lookup"><span data-stu-id="03cc4-118">Reason</span></span>                | <span data-ttu-id="03cc4-119">string</span><span class="sxs-lookup"><span data-stu-id="03cc4-119">string</span></span>           | <span data-ttu-id="03cc4-120">Reason özelliği aboneliğin aktarım için uygun olmadığını açıklar.</span><span class="sxs-lookup"><span data-stu-id="03cc4-120">The reason property explains why the subscription isn't eligible for transfer.</span></span> |