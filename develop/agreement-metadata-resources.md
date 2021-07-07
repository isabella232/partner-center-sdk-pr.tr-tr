---
title: Sözleşme meta veri kaynakları
description: AgreementMetadata kaynak koleksiyonu, iş ortaklarının müşteri kabulünü onaylaması için kullanabileceği sözleşme türlerini açıklar.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025641"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="d385f-103">Sözleşme meta veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="d385f-103">Agreement metadata resources</span></span>

<span data-ttu-id="d385f-104">**Için geçerlidir:** İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d385f-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="d385f-105">**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d385f-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d385f-106">**AgreementMetaData** kaynağı şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d385f-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span> 

<span data-ttu-id="d385f-107">**AgreementMetaData koleksiyonu,** tüm anlaşma türleri hakkında meta veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d385f-107">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="d385f-108">İş ortakları bu koleksiyonu kullanarak müşterinin sözleşme kabulünü onaylar.</span><span class="sxs-lookup"><span data-stu-id="d385f-108">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="d385f-109">**AgreementMetaData koleksiyonu,** hem sözleşme türleri **(** hem de Microsoft Bulut Anlaşması) için **meta Microsoft Müşteri Sözleşmesi** döndürür.</span><span class="sxs-lookup"><span data-stu-id="d385f-109">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="d385f-110">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="d385f-110">AgreementMetaData</span></span>

<span data-ttu-id="d385f-111">Döndürülen sözleşme meta verileri aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="d385f-111">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="d385f-112">Özellik</span><span class="sxs-lookup"><span data-stu-id="d385f-112">Property</span></span>      | <span data-ttu-id="d385f-113">Tür</span><span class="sxs-lookup"><span data-stu-id="d385f-113">Type</span></span>               | <span data-ttu-id="d385f-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d385f-114">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="d385f-115">templateId</span><span class="sxs-lookup"><span data-stu-id="d385f-115">templateId</span></span>    | <span data-ttu-id="d385f-116">string</span><span class="sxs-lookup"><span data-stu-id="d385f-116">string</span></span>             | <span data-ttu-id="d385f-117">Anlaşma şablonunun benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d385f-117">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="d385f-118">tür</span><span class="sxs-lookup"><span data-stu-id="d385f-118">type</span></span>          | <span data-ttu-id="d385f-119">string</span><span class="sxs-lookup"><span data-stu-id="d385f-119">string</span></span>             | <span data-ttu-id="d385f-120">Anlaşma türü.</span><span class="sxs-lookup"><span data-stu-id="d385f-120">Agreement type.</span></span> <span data-ttu-id="d385f-121">Şu anda desteklenen değerler **Arasında MicrosoftCloudAgreement ve** **MicrosoftCustomerAgreement** (önizleme) yer alır.</span><span class="sxs-lookup"><span data-stu-id="d385f-121">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="d385f-122">agreementLink</span><span class="sxs-lookup"><span data-stu-id="d385f-122">agreementLink</span></span> | <span data-ttu-id="d385f-123">string</span><span class="sxs-lookup"><span data-stu-id="d385f-123">string</span></span>             | <span data-ttu-id="d385f-124">Anlaşma şablonunun URL'si.</span><span class="sxs-lookup"><span data-stu-id="d385f-124">URL for the agreement template.</span></span>                                                    |
