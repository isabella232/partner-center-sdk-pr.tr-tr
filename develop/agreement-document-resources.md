---
title: Anlaşma belgesi kaynakları
description: AgreementDocument kaynağı, önizleme ve indirme için bir Microsoft sözleşmesi belgesidir. Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenir.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770030"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="49fcc-104">Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenen anlaşma belgesi kaynakları</span><span class="sxs-lookup"><span data-stu-id="49fcc-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="49fcc-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="49fcc-105">**Applies to:**</span></span>

- <span data-ttu-id="49fcc-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="49fcc-106">Partner Center</span></span>

<span data-ttu-id="49fcc-107">**AgreementDocument** kaynağı şu anda yalnızca *Microsoft genel bulutundaki* iş ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="49fcc-107">The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="49fcc-108">Bu kaynak için geçerli değildir:</span><span class="sxs-lookup"><span data-stu-id="49fcc-108">This resource not applicable to:</span></span>

- <span data-ttu-id="49fcc-109">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="49fcc-109">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="49fcc-110">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="49fcc-110">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="49fcc-111">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="49fcc-111">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="49fcc-112">**AgreementDocument** kaynağı, önizleme ve indirme için kullanılabilen bir Microsoft sözleşmesi belgesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="49fcc-112">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="49fcc-113">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="49fcc-113">AgreementDocument</span></span>

<span data-ttu-id="49fcc-114">Bir **AgreementDocument** kaynağı aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="49fcc-114">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="49fcc-115">Özellik</span><span class="sxs-lookup"><span data-stu-id="49fcc-115">Property</span></span>       | <span data-ttu-id="49fcc-116">Tür</span><span class="sxs-lookup"><span data-stu-id="49fcc-116">Type</span></span>   | <span data-ttu-id="49fcc-117">Description</span><span class="sxs-lookup"><span data-stu-id="49fcc-117">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="49fcc-118">ülke</span><span class="sxs-lookup"><span data-stu-id="49fcc-118">country</span></span> | <span data-ttu-id="49fcc-119">string</span><span class="sxs-lookup"><span data-stu-id="49fcc-119">string</span></span> | <span data-ttu-id="49fcc-120">Bu belgenin geçerli olduğu ülke veya Pazar.</span><span class="sxs-lookup"><span data-stu-id="49fcc-120">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="49fcc-121">language</span><span class="sxs-lookup"><span data-stu-id="49fcc-121">language</span></span> | <span data-ttu-id="49fcc-122">string</span><span class="sxs-lookup"><span data-stu-id="49fcc-122">string</span></span> | <span data-ttu-id="49fcc-123">Bu belgenin yerelleştirildiği dil.</span><span class="sxs-lookup"><span data-stu-id="49fcc-123">The language in which this document is localized.</span></span> |
| <span data-ttu-id="49fcc-124">displayUri</span><span class="sxs-lookup"><span data-stu-id="49fcc-124">displayUri</span></span> | <span data-ttu-id="49fcc-125">string</span><span class="sxs-lookup"><span data-stu-id="49fcc-125">string</span></span> | <span data-ttu-id="49fcc-126">Bir tarayıcıda anlaşma belgesini önizlemek için bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="49fcc-126">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="49fcc-127">downloadUri</span><span class="sxs-lookup"><span data-stu-id="49fcc-127">downloadUri</span></span> |<span data-ttu-id="49fcc-128">string</span><span class="sxs-lookup"><span data-stu-id="49fcc-128">string</span></span> | <span data-ttu-id="49fcc-129">Sözleşme belgesini indirmek için bir bağlantı (Microsoft Word biçiminde).</span><span class="sxs-lookup"><span data-stu-id="49fcc-129">A link to download the agreement document (in Microsoft Word format).</span></span> |
