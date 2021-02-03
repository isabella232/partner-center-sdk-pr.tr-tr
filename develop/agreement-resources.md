---
title: Anlaşma kaynakları
description: Sözleşme kaynağı, iş ortağı tarafından sunulan sertifika ayrıntıları ile bir Microsoft bulut müşteri anlaşmasını temsil eder.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770019"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="94306-103">Microsoft bulut müşteri anlaşmasını temsil eden sözleşme kaynakları</span><span class="sxs-lookup"><span data-stu-id="94306-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="94306-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="94306-104">**Applies to:**</span></span>

- <span data-ttu-id="94306-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="94306-105">Partner Center</span></span>

<span data-ttu-id="94306-106">**Sözleşme** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="94306-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="94306-107">Şunları yapmak için geçerli değildir:</span><span class="sxs-lookup"><span data-stu-id="94306-107">It isn't applicable to:</span></span>

- <span data-ttu-id="94306-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="94306-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="94306-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="94306-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="94306-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="94306-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="94306-111">**Sözleşme** kaynağı bir Microsoft bulut müşteri anlaşmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94306-111">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="94306-112">Sözleşme</span><span class="sxs-lookup"><span data-stu-id="94306-112">Agreement</span></span>

<span data-ttu-id="94306-113">**Anlaşma** kaynağı, iş ortağı tarafından belirtilen sertifikanın ayrıntılarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94306-113">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="94306-114">Özellik</span><span class="sxs-lookup"><span data-stu-id="94306-114">Property</span></span>       | <span data-ttu-id="94306-115">Tür</span><span class="sxs-lookup"><span data-stu-id="94306-115">Type</span></span>   | <span data-ttu-id="94306-116">Description</span><span class="sxs-lookup"><span data-stu-id="94306-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="94306-117">userId</span><span class="sxs-lookup"><span data-stu-id="94306-117">userId</span></span>         | <span data-ttu-id="94306-118">string</span><span class="sxs-lookup"><span data-stu-id="94306-118">string</span></span>                         | <span data-ttu-id="94306-119">İş ortağı kiracısında iş ortağı kuruluşu adına onay sağlayan, oturum açmış kullanıcının nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="94306-119">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="94306-120">Iş Ortağı Merkezi, bir anlaşma kaynağı oluşturmak için uygulama + kullanıcı kimlik doğrulaması kullanırken, uygulama + Kullanıcı belirtecinden **UserID** özniteliği değerini otomatik olarak türetir.</span><span class="sxs-lookup"><span data-stu-id="94306-120">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="94306-121">primaryContact</span><span class="sxs-lookup"><span data-stu-id="94306-121">primaryContact</span></span> | [<span data-ttu-id="94306-122">İletişim</span><span class="sxs-lookup"><span data-stu-id="94306-122">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="94306-123">Müşteri kuruluşundan, sözleşmeyi kabul  **eden,** **Soyadı**, **e-posta** ve **PhoneNumber** (isteğe bağlı) dahil olmak üzere Kullanıcı hakkında bilgiler.</span><span class="sxs-lookup"><span data-stu-id="94306-123">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="94306-124">Kabul edilen tarih</span><span class="sxs-lookup"><span data-stu-id="94306-124">dateAgreed</span></span>     | <span data-ttu-id="94306-125">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="94306-125">string in UTC date time format</span></span> | <span data-ttu-id="94306-126">Müşterinin sözleşmeyi kabul ettiği tarih.</span><span class="sxs-lookup"><span data-stu-id="94306-126">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="94306-127">TemplateId</span><span class="sxs-lookup"><span data-stu-id="94306-127">templateId</span></span>     |<span data-ttu-id="94306-128">string</span><span class="sxs-lookup"><span data-stu-id="94306-128">string</span></span>                          | <span data-ttu-id="94306-129">Müşterinin kabul ettiği sözleşmenin benzersiz tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="94306-129">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="94306-130">tür</span><span class="sxs-lookup"><span data-stu-id="94306-130">type</span></span>           |<span data-ttu-id="94306-131">string</span><span class="sxs-lookup"><span data-stu-id="94306-131">string</span></span>                          | <span data-ttu-id="94306-132">Anlaşma türü.</span><span class="sxs-lookup"><span data-stu-id="94306-132">Agreement type.</span></span> <span data-ttu-id="94306-133">Şu anda, desteklenen değerler **Microsoftcloudagreement** ve **microsoftcustomeragreement**' i içerir.</span><span class="sxs-lookup"><span data-stu-id="94306-133">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="94306-134">agreementLink</span><span class="sxs-lookup"><span data-stu-id="94306-134">agreementLink</span></span>  | <span data-ttu-id="94306-135">string</span><span class="sxs-lookup"><span data-stu-id="94306-135">string</span></span>                         | <span data-ttu-id="94306-136">Sözleşme şablonunun URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="94306-136">URL for the agreement template.</span></span>                                                    |
