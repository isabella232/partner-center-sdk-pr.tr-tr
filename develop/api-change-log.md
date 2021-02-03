---
title: İş Ortağı Merkezi REST API’si değişiklik günlüğü
description: Bu sayfada Iş Ortağı Merkezi REST API 'Lerinde yapılan değişiklikler listelenir
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: 79359414276a1259117a8f506bbfae4441cdcbed
ms.sourcegitcommit: f8ca3a14a763013fefafd3262d0a740881d1d7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97770282"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="21b0e-103">Iş Ortağı Merkezi REST API 'Lerinde Aralık 2020 değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="21b0e-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="21b0e-104">Iş Ortağı Merkezi REST API 'Lerinde yapılan değişiklikler için buraya bakın.</span><span class="sxs-lookup"><span data-stu-id="21b0e-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="21b0e-105">Eğitim Fiyatlandırma uygunluğu API 'Lerine yönelik geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="21b0e-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="21b0e-106">Ne değişti?</span><span class="sxs-lookup"><span data-stu-id="21b0e-106">What has changed?</span></span>

<span data-ttu-id="21b0e-107">Şu anda Iş Ortağı Merkezi API 'sinin eğitim müşterilerinin uygunluğunu doğrulamak için GET ve PUT nitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="21b0e-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="21b0e-108">Nitelik al API 'sinde hiçbir değişiklik olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="21b0e-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="21b0e-109">Ancak, YERLEŞTIRME API 'sine bir dönüş durumu ekledik.</span><span class="sxs-lookup"><span data-stu-id="21b0e-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="21b0e-110">GET-değişmez.</span><span class="sxs-lookup"><span data-stu-id="21b0e-110">GET - doesn't change.</span></span> [<span data-ttu-id="21b0e-111">Geçerli API makalesi</span><span class="sxs-lookup"><span data-stu-id="21b0e-111">Current API article</span></span>](get-a-customer-s-qualification.md)
- <span data-ttu-id="21b0e-112">PUT-Return Case eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="21b0e-112">PUT - return case will be added.</span></span> [<span data-ttu-id="21b0e-113">Geçerli API makalesi</span><span class="sxs-lookup"><span data-stu-id="21b0e-113">Current API article</span></span>](update-a-customer-s-qualification.md)

<span data-ttu-id="21b0e-114">Bu API 'Ler, aşağıda açıklandığı gibi yeni API 'Ler ile değiştirilerek, Şubat 2021 ' un sonunda kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="21b0e-114">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="21b0e-115">Etkilenen senaryolar:</span><span class="sxs-lookup"><span data-stu-id="21b0e-115">Scenarios impacted:</span></span>

<span data-ttu-id="21b0e-116">Select SKU 'Larında eğitim fiyatlandırması için Müşteri uygunluğu</span><span class="sxs-lookup"><span data-stu-id="21b0e-116">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="21b0e-117">Ayrıntı açıklamaları</span><span class="sxs-lookup"><span data-stu-id="21b0e-117">Detail descriptions</span></span>

<span data-ttu-id="21b0e-118">İki yeni GET ve POST nitelikleri API 'si tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="21b0e-118">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="21b0e-119">Yeni API 'Ler **nitelik** değil, **nitelikleri** kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="21b0e-119">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="21b0e-120">API 'Ler, FY21 S2 'de test için kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="21b0e-120">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="21b0e-121">Nitelikleri al</span><span class="sxs-lookup"><span data-stu-id="21b0e-121">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="21b0e-122">Yanıt örneği:</span><span class="sxs-lookup"><span data-stu-id="21b0e-122">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="21b0e-123">Yanıt alanları:</span><span class="sxs-lookup"><span data-stu-id="21b0e-123">Response fields:</span></span> 

- <span data-ttu-id="21b0e-124">VettingStatus değerleri: onaylandı, reddedildi, ınreview, vb.</span><span class="sxs-lookup"><span data-stu-id="21b0e-124">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="21b0e-125">VettingReason değerleri:</span><span class="sxs-lookup"><span data-stu-id="21b0e-125">VettingReason values:</span></span>
   - <span data-ttu-id="21b0e-126">Eğitim müşterisi değil</span><span class="sxs-lookup"><span data-stu-id="21b0e-126">Not an Education Customer</span></span>
   - <span data-ttu-id="21b0e-127">Artık eğitim müşterisi yok</span><span class="sxs-lookup"><span data-stu-id="21b0e-127">No longer an Education Customer</span></span>
   - <span data-ttu-id="21b0e-128">Eğitim müşterisi değil-Inceleme sonrası</span><span class="sxs-lookup"><span data-stu-id="21b0e-128">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="21b0e-129">Eğitim müşterisi olacak şekilde kısıtlıdır</span><span class="sxs-lookup"><span data-stu-id="21b0e-129">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="21b0e-130">Akademik etki alanı değil</span><span class="sxs-lookup"><span data-stu-id="21b0e-130">Not an Academic Domain</span></span>
   - <span data-ttu-id="21b0e-131">Uygun bir kitaplık değil</span><span class="sxs-lookup"><span data-stu-id="21b0e-131">Not an eligible Library</span></span>
   - <span data-ttu-id="21b0e-132">Uygun Museum değil</span><span class="sxs-lookup"><span data-stu-id="21b0e-132">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="21b0e-133">GÖNDERI nitelikleri</span><span class="sxs-lookup"><span data-stu-id="21b0e-133">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="21b0e-134">Yanıt örneği:</span><span class="sxs-lookup"><span data-stu-id="21b0e-134">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="21b0e-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21b0e-135">Next steps</span></span>

[<span data-ttu-id="21b0e-136">İş Ortağı Merkezi REST API'si referansı</span><span class="sxs-lookup"><span data-stu-id="21b0e-136">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
