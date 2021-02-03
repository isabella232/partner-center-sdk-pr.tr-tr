---
title: Anlaşma meta veri kaynakları
description: AgreementMetadata kaynak koleksiyonu, iş ortaklarının müşteri kabulünün onayını sağlamak için kullanabileceği anlaşma türlerini açıklar.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768837"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="3e712-103">Anlaşma meta veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="3e712-103">Agreement metadata resources</span></span>

<span data-ttu-id="3e712-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="3e712-104">**Applies to:**</span></span>

- <span data-ttu-id="3e712-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3e712-105">Partner Center</span></span>

<span data-ttu-id="3e712-106">**AgreementMetaData** kaynağı şu anda yalnızca *Microsoft genel bulutundaki* iş ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e712-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="3e712-107">Bu kaynak için geçerli değildir:</span><span class="sxs-lookup"><span data-stu-id="3e712-107">This resource isn't applicable to:</span></span>

- <span data-ttu-id="3e712-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3e712-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3e712-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3e712-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3e712-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3e712-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3e712-111">**AgreementMetaData** koleksiyonu tüm anlaşma türleri hakkında meta veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="3e712-111">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="3e712-112">İş ortakları, bu koleksiyonu müşteri anlaşmalarının kabul edilmesine yönelik onay sağlamak için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="3e712-112">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="3e712-113">**AgreementMetaData** Collection, her iki anlaşma türü (**Microsoft bulut sözleşmesi** ve **Microsoft Müşteri Sözleşmesi**) için meta verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3e712-113">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="3e712-114">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="3e712-114">AgreementMetaData</span></span>

<span data-ttu-id="3e712-115">Döndürülen anlaşma meta verileri aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="3e712-115">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="3e712-116">Özellik</span><span class="sxs-lookup"><span data-stu-id="3e712-116">Property</span></span>      | <span data-ttu-id="3e712-117">Tür</span><span class="sxs-lookup"><span data-stu-id="3e712-117">Type</span></span>               | <span data-ttu-id="3e712-118">Description</span><span class="sxs-lookup"><span data-stu-id="3e712-118">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="3e712-119">TemplateId</span><span class="sxs-lookup"><span data-stu-id="3e712-119">templateId</span></span>    | <span data-ttu-id="3e712-120">string</span><span class="sxs-lookup"><span data-stu-id="3e712-120">string</span></span>             | <span data-ttu-id="3e712-121">Sözleşme şablonunun benzersiz tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="3e712-121">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="3e712-122">tür</span><span class="sxs-lookup"><span data-stu-id="3e712-122">type</span></span>          | <span data-ttu-id="3e712-123">string</span><span class="sxs-lookup"><span data-stu-id="3e712-123">string</span></span>             | <span data-ttu-id="3e712-124">Anlaşma türü.</span><span class="sxs-lookup"><span data-stu-id="3e712-124">Agreement type.</span></span> <span data-ttu-id="3e712-125">Şu anda, desteklenen değerler **Microsoftcloudagreement** ve **microsoftcustomeragreement** (Önizleme) içerir.</span><span class="sxs-lookup"><span data-stu-id="3e712-125">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="3e712-126">agreementLink</span><span class="sxs-lookup"><span data-stu-id="3e712-126">agreementLink</span></span> | <span data-ttu-id="3e712-127">string</span><span class="sxs-lookup"><span data-stu-id="3e712-127">string</span></span>             | <span data-ttu-id="3e712-128">Sözleşme şablonunun URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="3e712-128">URL for the agreement template.</span></span>                                                    |
