---
title: Azure harcama API 'SI kaynakları
description: CSP iş ortaklarının iş ortağı ve müşteri Azure harcama ve kullanımını bütçelere göre görüntülemek ve yönetmek için Iş Ortağı Merkezi API 'Lerini nasıl kullanabileceğinizi öğrenin.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 472554de1c354559d5bc4b21959c109467891806
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974327"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="f6246-103">Azure harcama API kaynakları bir bütçeye göre iş ortağı veya müşteri harcama ve kullanımını yönetmek için</span><span class="sxs-lookup"><span data-stu-id="f6246-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="f6246-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f6246-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f6246-105">Bulut Çözümü Sağlayıcısı (CSP) iş ortakları, Azure harcamalarını iş ortağı merkezi apı 'leri üzerinden görüntüleyebilir ve yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="f6246-105">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="f6246-106">Ayrıca, müşterilerinin Azure harcama bütçesine göre harcamalarını de görüntüleyebilirler.</span><span class="sxs-lookup"><span data-stu-id="f6246-106">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="f6246-107">Daha fazla bilgi için, [CSP iş ortaklarının müşteri ve iş ortağı hesaplarını ve siparişlerini yönetmek üzere Iş Ortağı Merkezi API 'lerini kullanabileceği senaryolar](scenarios.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f6246-107">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="f6246-108">İş ortağı kullanım yönetimi</span><span class="sxs-lookup"><span data-stu-id="f6246-108">Partner usage management</span></span>

- <span data-ttu-id="f6246-109">**Partnerusagesummary** kaynağını kullanarak [iş ortağı Kullanım Özeti alma](get-a-partner-usage-summary.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-109">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="f6246-110">**CustomerMonthlyUsageRecord** kaynağını kullanarak [tüm müşteriler Için kullanım kayıtları alın](get-a-customer-s-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-110">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="f6246-111">Müşteri kullanım yönetimi</span><span class="sxs-lookup"><span data-stu-id="f6246-111">Customer usage management</span></span>

- <span data-ttu-id="f6246-112">**Customerusagesummary** kaynağını kullanarak [bir müşterinin kullanım özetini alma](get-a-customer-usage-summary.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-112">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="f6246-113">**SubscriptionMonthlyUsageRecord** kaynağını kullanarak [bir müşterinin tüm abonelik kullanım kayıtlarını alın](get-a-customer-subscription-s-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-113">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="f6246-114">Abonelik kullanım yönetimi</span><span class="sxs-lookup"><span data-stu-id="f6246-114">Subscription usage management</span></span>

- <span data-ttu-id="f6246-115">**Subscriptionusagesummary** kaynağını kullanarak [abonelik Kullanım Özeti alma](get-a-customer-subscription-usage-summary.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-115">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="f6246-116">**AzureResourceMonthlyUsageRecord** kaynağını kullanarak [bir abonelik için tüm aylık kullanım kayıtlarını alın](get-all-monthly-usage-records-for-a-subscription.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-116">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="f6246-117">**ResourceUsageRecord** kaynağını kullanarak [bir abonelik Için kullanım verilerini al](get-a-customer-subscription-resource-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-117">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="f6246-118">**MeterUsageRecord** kaynağını kullanarak [bir abonelik Için kullanım verileri alın](get-a-customer-subscription-meter-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-118">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="f6246-119">Azure harcama bütçe yönetimi</span><span class="sxs-lookup"><span data-stu-id="f6246-119">Azure spending budget management</span></span>

- <span data-ttu-id="f6246-120">**Customerusagesummary** kaynağını kullanarak [müşterinin kullanım bütçesini alma](get-a-customer-s-usage-spending-budget.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-120">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="f6246-121">**Customerusagesummary** kaynağını kullanarak [müşterinin kullanım bütçesini güncelleştirme](update-a-customer-s-usage-spending-budget.md)</span><span class="sxs-lookup"><span data-stu-id="f6246-121">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
