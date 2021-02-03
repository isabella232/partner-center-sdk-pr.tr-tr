---
title: Azure harcama API 'SI kaynakları
description: CSP iş ortaklarının iş ortağı ve müşteri Azure harcama ve kullanımını bütçelere göre görüntülemek ve yönetmek için Iş Ortağı Merkezi API 'Lerini nasıl kullanabileceğinizi öğrenin.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a2995a06473cc6990d1234acd522a3b38a03d3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97769995"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="016ab-103">Azure harcama API kaynakları bir bütçeye göre iş ortağı veya müşteri harcama ve kullanımını yönetmek için</span><span class="sxs-lookup"><span data-stu-id="016ab-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="016ab-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="016ab-104">**Applies to:**</span></span>

- <span data-ttu-id="016ab-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="016ab-105">Partner Center</span></span>
- <span data-ttu-id="016ab-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="016ab-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="016ab-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="016ab-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="016ab-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="016ab-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="016ab-109">Bulut çözümü sağlayıcısı (CSP) iş ortakları, Azure harcamalarını Iş Ortağı Merkezi API 'Leri üzerinden görüntüleyebilir ve yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="016ab-109">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="016ab-110">Ayrıca, müşterilerinin Azure harcama bütçesine göre harcamalarını de görüntüleyebilirler.</span><span class="sxs-lookup"><span data-stu-id="016ab-110">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="016ab-111">Daha fazla bilgi için, [CSP iş ortaklarının müşteri ve iş ortağı hesaplarını ve siparişlerini yönetmek üzere Iş Ortağı Merkezi API 'lerini kullanabileceği senaryolar](scenarios.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="016ab-111">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="016ab-112">İş ortağı kullanım yönetimi</span><span class="sxs-lookup"><span data-stu-id="016ab-112">Partner usage management</span></span>

- <span data-ttu-id="016ab-113">**Partnerusagesummary** kaynağını kullanarak [iş ortağı Kullanım Özeti alma](get-a-partner-usage-summary.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-113">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="016ab-114">**CustomerMonthlyUsageRecord** kaynağını kullanarak [tüm müşteriler Için kullanım kayıtları alın](get-a-customer-s-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-114">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="016ab-115">Müşteri kullanım yönetimi</span><span class="sxs-lookup"><span data-stu-id="016ab-115">Customer usage management</span></span>

- <span data-ttu-id="016ab-116">**Customerusagesummary** kaynağını kullanarak [bir müşterinin kullanım özetini alma](get-a-customer-usage-summary.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-116">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="016ab-117">**SubscriptionMonthlyUsageRecord** kaynağını kullanarak [bir müşterinin tüm abonelik kullanım kayıtlarını alın](get-a-customer-subscription-s-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-117">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="016ab-118">Abonelik kullanım yönetimi</span><span class="sxs-lookup"><span data-stu-id="016ab-118">Subscription usage management</span></span>

- <span data-ttu-id="016ab-119">**Subscriptionusagesummary** kaynağını kullanarak [abonelik Kullanım Özeti alma](get-a-customer-subscription-usage-summary.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-119">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="016ab-120">**AzureResourceMonthlyUsageRecord** kaynağını kullanarak [bir abonelik için tüm aylık kullanım kayıtlarını alın](get-all-monthly-usage-records-for-a-subscription.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-120">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="016ab-121">**ResourceUsageRecord** kaynağını kullanarak [bir abonelik Için kullanım verilerini al](get-a-customer-subscription-resource-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-121">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="016ab-122">**MeterUsageRecord** kaynağını kullanarak [bir abonelik Için kullanım verileri alın](get-a-customer-subscription-meter-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-122">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="016ab-123">Azure harcama bütçe yönetimi</span><span class="sxs-lookup"><span data-stu-id="016ab-123">Azure spending budget management</span></span>

- <span data-ttu-id="016ab-124">**Customerusagesummary** kaynağını kullanarak [müşterinin kullanım bütçesini alma](get-a-customer-s-usage-spending-budget.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-124">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="016ab-125">**Customerusagesummary** kaynağını kullanarak [müşterinin kullanım bütçesini güncelleştirme](update-a-customer-s-usage-spending-budget.md)</span><span class="sxs-lookup"><span data-stu-id="016ab-125">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
