---
title: Sözleşme belgesi kaynakları
description: AgreementDocument kaynağı, önizleme ve indirme için bir Microsoft sözleşmesi belgesidir. Microsoft genel bulut İş Ortağı Merkezi tarafından de destekler.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 1a81da4f75594f241669db831125bd437872561c
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025675"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="14557-104">Microsoft genel buluta İş Ortağı Merkezi tarafından desteklenen sözleşme belgesi kaynakları</span><span class="sxs-lookup"><span data-stu-id="14557-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="14557-105">**Için geçerlidir:** İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="14557-105">**Applies to**: Partner Center</span></span>

<span data-ttu-id="14557-106">**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="14557-106">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="14557-107">**AgreementDocument kaynağı** şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14557-107">The **AgreementDocument** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="14557-108">**AgreementDocument kaynağı,** önizleme ve indirme için kullanılabilen bir Microsoft sözleşmesi belgesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="14557-108">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="14557-109">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="14557-109">AgreementDocument</span></span>

<span data-ttu-id="14557-110">**Bir AgreementDocument** kaynağı aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="14557-110">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="14557-111">Özellik</span><span class="sxs-lookup"><span data-stu-id="14557-111">Property</span></span>       | <span data-ttu-id="14557-112">Tür</span><span class="sxs-lookup"><span data-stu-id="14557-112">Type</span></span>   | <span data-ttu-id="14557-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="14557-113">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14557-114">ülke</span><span class="sxs-lookup"><span data-stu-id="14557-114">country</span></span> | <span data-ttu-id="14557-115">string</span><span class="sxs-lookup"><span data-stu-id="14557-115">string</span></span> | <span data-ttu-id="14557-116">Bu belgenin geçerli olduğu ülke veya pazar.</span><span class="sxs-lookup"><span data-stu-id="14557-116">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="14557-117">language</span><span class="sxs-lookup"><span data-stu-id="14557-117">language</span></span> | <span data-ttu-id="14557-118">string</span><span class="sxs-lookup"><span data-stu-id="14557-118">string</span></span> | <span data-ttu-id="14557-119">Bu belgenin yerelleştirilmiş olduğu dil.</span><span class="sxs-lookup"><span data-stu-id="14557-119">The language in which this document is localized.</span></span> |
| <span data-ttu-id="14557-120">displayUri</span><span class="sxs-lookup"><span data-stu-id="14557-120">displayUri</span></span> | <span data-ttu-id="14557-121">string</span><span class="sxs-lookup"><span data-stu-id="14557-121">string</span></span> | <span data-ttu-id="14557-122">Bir tarayıcıda sözleşme belgesinin önizlemesini görüntülemek için bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="14557-122">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="14557-123">downloadUri</span><span class="sxs-lookup"><span data-stu-id="14557-123">downloadUri</span></span> |<span data-ttu-id="14557-124">string</span><span class="sxs-lookup"><span data-stu-id="14557-124">string</span></span> | <span data-ttu-id="14557-125">Sözleşme belgesini indirme bağlantısı (Microsoft Word).</span><span class="sxs-lookup"><span data-stu-id="14557-125">A link to download the agreement document (in Microsoft Word format).</span></span> |
