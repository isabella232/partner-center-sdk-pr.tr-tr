---
title: İş Ortağı Merkezi REST API’si değişiklik günlüğü
description: Bu sayfada Iş Ortağı Merkezi REST API 'Lerinde yapılan değişiklikler listelenir
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572004"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="87e31-103">Iş Ortağı Merkezi REST API 'Lerinde Aralık 2020 değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="87e31-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="87e31-104">Iş Ortağı Merkezi REST API 'Lerinde yapılan değişiklikler için buraya bakın.</span><span class="sxs-lookup"><span data-stu-id="87e31-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="87e31-105">Eğitim Fiyatlandırma uygunluğu API 'Lerine yönelik geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="87e31-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="87e31-106">Ne değişti?</span><span class="sxs-lookup"><span data-stu-id="87e31-106">What has changed?</span></span>

<span data-ttu-id="87e31-107">Şu anda Iş Ortağı Merkezi API 'sinin eğitim müşterilerinin uygunluğunu doğrulamak için GET ve PUT nitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="87e31-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="87e31-108">Nitelik al API 'sinde hiçbir değişiklik olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="87e31-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="87e31-109">Ancak, YERLEŞTIRME API 'sine bir dönüş durumu ekledik.</span><span class="sxs-lookup"><span data-stu-id="87e31-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="87e31-110">GET-değişmez.</span><span class="sxs-lookup"><span data-stu-id="87e31-110">GET - doesn't change.</span></span>
- <span data-ttu-id="87e31-111">PUT-Return Case eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="87e31-111">PUT - return case will be added.</span></span>

<span data-ttu-id="87e31-112">Bu API 'Ler, aşağıda açıklandığı gibi yeni API 'Ler ile değiştirilerek, Şubat 2021 ' un sonunda kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="87e31-112">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="87e31-113">Etkilenen senaryolar:</span><span class="sxs-lookup"><span data-stu-id="87e31-113">Scenarios impacted:</span></span>

<span data-ttu-id="87e31-114">Select SKU 'Larında eğitim fiyatlandırması için Müşteri uygunluğu</span><span class="sxs-lookup"><span data-stu-id="87e31-114">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="87e31-115">Ayrıntı açıklamaları</span><span class="sxs-lookup"><span data-stu-id="87e31-115">Detail descriptions</span></span>

<span data-ttu-id="87e31-116">İki yeni GET ve POST nitelikleri API 'si tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="87e31-116">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="87e31-117">Yeni API 'Ler **nitelik** değil, **nitelikleri** kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="87e31-117">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="87e31-118">API 'Ler, FY21 S2 'de test için kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="87e31-118">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="87e31-119">Nitelikleri al</span><span class="sxs-lookup"><span data-stu-id="87e31-119">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="87e31-120">Yanıt örneği:</span><span class="sxs-lookup"><span data-stu-id="87e31-120">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="87e31-121">Yanıt alanları:</span><span class="sxs-lookup"><span data-stu-id="87e31-121">Response fields:</span></span> 

- <span data-ttu-id="87e31-122">VettingStatus değerleri: onaylandı, reddedildi, ınreview, vb.</span><span class="sxs-lookup"><span data-stu-id="87e31-122">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="87e31-123">VettingReason değerleri:</span><span class="sxs-lookup"><span data-stu-id="87e31-123">VettingReason values:</span></span>
   - <span data-ttu-id="87e31-124">Eğitim müşterisi değil</span><span class="sxs-lookup"><span data-stu-id="87e31-124">Not an Education Customer</span></span>
   - <span data-ttu-id="87e31-125">Artık eğitim müşterisi yok</span><span class="sxs-lookup"><span data-stu-id="87e31-125">No longer an Education Customer</span></span>
   - <span data-ttu-id="87e31-126">Eğitim müşterisi değil-Inceleme sonrası</span><span class="sxs-lookup"><span data-stu-id="87e31-126">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="87e31-127">Eğitim müşterisi olacak şekilde kısıtlıdır</span><span class="sxs-lookup"><span data-stu-id="87e31-127">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="87e31-128">Akademik etki alanı değil</span><span class="sxs-lookup"><span data-stu-id="87e31-128">Not an Academic Domain</span></span>
   - <span data-ttu-id="87e31-129">Uygun bir kitaplık değil</span><span class="sxs-lookup"><span data-stu-id="87e31-129">Not an eligible Library</span></span>
   - <span data-ttu-id="87e31-130">Uygun Museum değil</span><span class="sxs-lookup"><span data-stu-id="87e31-130">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="87e31-131">GÖNDERI nitelikleri</span><span class="sxs-lookup"><span data-stu-id="87e31-131">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="87e31-132">Yanıt örneği:</span><span class="sxs-lookup"><span data-stu-id="87e31-132">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="87e31-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87e31-133">Next steps</span></span>

[<span data-ttu-id="87e31-134">İş Ortağı Merkezi REST API'si referansı</span><span class="sxs-lookup"><span data-stu-id="87e31-134">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
