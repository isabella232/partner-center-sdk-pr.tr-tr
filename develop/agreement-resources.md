---
title: Anlaşma kaynakları
description: Sözleşme kaynağı, iş ortağı tarafından sunulan sertifika ayrıntıları ile bir Microsoft bulut müşteri anlaşmasını temsil eder.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025640"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="adba8-103">Microsoft bulut müşteri anlaşmasını temsil eden sözleşme kaynakları</span><span class="sxs-lookup"><span data-stu-id="adba8-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="adba8-104">**Uygulama hedefi**: Iş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="adba8-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="adba8-105">**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="adba8-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="adba8-106">**Sözleşme** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="adba8-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="adba8-107">**Sözleşme** kaynağı bir Microsoft bulut müşteri anlaşmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="adba8-107">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="adba8-108">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="adba8-108">Agreement</span></span>

<span data-ttu-id="adba8-109">**Anlaşma** kaynağı, iş ortağı tarafından belirtilen sertifikanın ayrıntılarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="adba8-109">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="adba8-110">Özellik</span><span class="sxs-lookup"><span data-stu-id="adba8-110">Property</span></span>       | <span data-ttu-id="adba8-111">Tür</span><span class="sxs-lookup"><span data-stu-id="adba8-111">Type</span></span>   | <span data-ttu-id="adba8-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="adba8-112">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="adba8-113">userId</span><span class="sxs-lookup"><span data-stu-id="adba8-113">userId</span></span>         | <span data-ttu-id="adba8-114">string</span><span class="sxs-lookup"><span data-stu-id="adba8-114">string</span></span>                         | <span data-ttu-id="adba8-115">İş ortağı kiracısında iş ortağı kuruluşu adına onay sağlayan, oturum açmış kullanıcının nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="adba8-115">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="adba8-116">Iş Ortağı Merkezi, bir anlaşma kaynağı oluşturmak için uygulama + kullanıcı kimlik doğrulaması kullanırken, uygulama + Kullanıcı belirtecinden **UserID** özniteliği değerini otomatik olarak türetir.</span><span class="sxs-lookup"><span data-stu-id="adba8-116">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="adba8-117">primaryContact</span><span class="sxs-lookup"><span data-stu-id="adba8-117">primaryContact</span></span> | [<span data-ttu-id="adba8-118">İletişim</span><span class="sxs-lookup"><span data-stu-id="adba8-118">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="adba8-119">Müşteri kuruluşundan, sözleşmeyi kabul  **eden,** **Soyadı**, **e-posta** ve **PhoneNumber** (isteğe bağlı) dahil olmak üzere Kullanıcı hakkında bilgiler.</span><span class="sxs-lookup"><span data-stu-id="adba8-119">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="adba8-120">Kabul edilen tarih</span><span class="sxs-lookup"><span data-stu-id="adba8-120">dateAgreed</span></span>     | <span data-ttu-id="adba8-121">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="adba8-121">string in UTC date time format</span></span> | <span data-ttu-id="adba8-122">Müşterinin sözleşmeyi kabul ettiği tarih.</span><span class="sxs-lookup"><span data-stu-id="adba8-122">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="adba8-123">TemplateId</span><span class="sxs-lookup"><span data-stu-id="adba8-123">templateId</span></span>     |<span data-ttu-id="adba8-124">string</span><span class="sxs-lookup"><span data-stu-id="adba8-124">string</span></span>                          | <span data-ttu-id="adba8-125">Müşterinin kabul ettiği sözleşmenin benzersiz tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="adba8-125">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="adba8-126">tür</span><span class="sxs-lookup"><span data-stu-id="adba8-126">type</span></span>           |<span data-ttu-id="adba8-127">string</span><span class="sxs-lookup"><span data-stu-id="adba8-127">string</span></span>                          | <span data-ttu-id="adba8-128">Anlaşma türü.</span><span class="sxs-lookup"><span data-stu-id="adba8-128">Agreement type.</span></span> <span data-ttu-id="adba8-129">Şu anda, desteklenen değerler **Microsoftcloudagreement** ve **microsoftcustomeragreement**' i içerir.</span><span class="sxs-lookup"><span data-stu-id="adba8-129">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="adba8-130">agreementLink</span><span class="sxs-lookup"><span data-stu-id="adba8-130">agreementLink</span></span>  | <span data-ttu-id="adba8-131">string</span><span class="sxs-lookup"><span data-stu-id="adba8-131">string</span></span>                         | <span data-ttu-id="adba8-132">Sözleşme şablonunun URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="adba8-132">URL for the agreement template.</span></span>                                                    |
