---
title: Müşteri sözleşmesinin doğrudan imzalama (doğrudan kabul) durumu.
description: DirectSignedCustomerAgreementStatus kaynağı, müşteri anlaşmasının doğrudan imzalanmasının (doğrudan kabul) durumunu temsil eder.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768795"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a><span data-ttu-id="98c8c-103">Müşteri sözleşmesinin doğrudan imzası (doğrudan kabul) durumu</span><span class="sxs-lookup"><span data-stu-id="98c8c-103">Direct signing (direct acceptance) status of a customer agreement</span></span>

<span data-ttu-id="98c8c-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="98c8c-104">**Applies to:**</span></span>

- <span data-ttu-id="98c8c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98c8c-105">Partner Center</span></span>

<span data-ttu-id="98c8c-106">**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="98c8c-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="98c8c-107">Bu kaynak için *geçerli değildir* :</span><span class="sxs-lookup"><span data-stu-id="98c8c-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="98c8c-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98c8c-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="98c8c-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98c8c-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="98c8c-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98c8c-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="98c8c-111">**DirectSignedCustomerAgreementStatus** kaynağı, müşteri sözleşmesinin doğrudan kabulünün durumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="98c8c-111">The **DirectSignedCustomerAgreementStatus** resource represents the status of the direct acceptance of a customer agreement.</span></span>

## <a name="directsignedcustomeragreementstatus"></a><span data-ttu-id="98c8c-112">DirectSignedCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="98c8c-112">DirectSignedCustomerAgreementStatus</span></span>

<span data-ttu-id="98c8c-113">Bir **DirectSignedCustomerAgreementStatus** kaynağı aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="98c8c-113">A **DirectSignedCustomerAgreementStatus** resource includes the following properties:</span></span>

| <span data-ttu-id="98c8c-114">Özellik</span><span class="sxs-lookup"><span data-stu-id="98c8c-114">Property</span></span>       | <span data-ttu-id="98c8c-115">Tür</span><span class="sxs-lookup"><span data-stu-id="98c8c-115">Type</span></span>   | <span data-ttu-id="98c8c-116">Description</span><span class="sxs-lookup"><span data-stu-id="98c8c-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="98c8c-117">isSigned</span><span class="sxs-lookup"><span data-stu-id="98c8c-117">isSigned</span></span> | <span data-ttu-id="98c8c-118">boolean</span><span class="sxs-lookup"><span data-stu-id="98c8c-118">boolean</span></span> | <span data-ttu-id="98c8c-119">Müşteri sözleşmesinin müşteri tarafından doğrudan imzalanıp imzalanmadığını (kabul edildi) gösterir.</span><span class="sxs-lookup"><span data-stu-id="98c8c-119">Indicates if the customer agreement has been directly signed (accepted) by the customer.</span></span> |
