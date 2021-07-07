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
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Azure harcama API kaynakları bir bütçeye göre iş ortağı veya müşteri harcama ve kullanımını yönetmek için 

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bulut Çözümü Sağlayıcısı (CSP) iş ortakları, Azure harcamalarını iş ortağı merkezi apı 'leri üzerinden görüntüleyebilir ve yönetebilir. Ayrıca, müşterilerinin Azure harcama bütçesine göre harcamalarını de görüntüleyebilirler.

Daha fazla bilgi için, [CSP iş ortaklarının müşteri ve iş ortağı hesaplarını ve siparişlerini yönetmek üzere Iş Ortağı Merkezi API 'lerini kullanabileceği senaryolar](scenarios.md)bölümüne bakın.

## <a name="partner-usage-management"></a>İş ortağı kullanım yönetimi

- **Partnerusagesummary** kaynağını kullanarak [iş ortağı Kullanım Özeti alma](get-a-partner-usage-summary.md)
- **CustomerMonthlyUsageRecord** kaynağını kullanarak [tüm müşteriler Için kullanım kayıtları alın](get-a-customer-s-usage-records.md)

## <a name="customer-usage-management"></a>Müşteri kullanım yönetimi

- **Customerusagesummary** kaynağını kullanarak [bir müşterinin kullanım özetini alma](get-a-customer-usage-summary.md)
- **SubscriptionMonthlyUsageRecord** kaynağını kullanarak [bir müşterinin tüm abonelik kullanım kayıtlarını alın](get-a-customer-subscription-s-usage-records.md)

## <a name="subscription-usage-management"></a>Abonelik kullanım yönetimi

- **Subscriptionusagesummary** kaynağını kullanarak [abonelik Kullanım Özeti alma](get-a-customer-subscription-usage-summary.md)
- **AzureResourceMonthlyUsageRecord** kaynağını kullanarak [bir abonelik için tüm aylık kullanım kayıtlarını alın](get-all-monthly-usage-records-for-a-subscription.md)
- **ResourceUsageRecord** kaynağını kullanarak [bir abonelik Için kullanım verilerini al](get-a-customer-subscription-resource-usage-records.md)
- **MeterUsageRecord** kaynağını kullanarak [bir abonelik Için kullanım verileri alın](get-a-customer-subscription-meter-usage-records.md)

## <a name="azure-spending-budget-management"></a>Azure harcama bütçe yönetimi

- **Customerusagesummary** kaynağını kullanarak [müşterinin kullanım bütçesini alma](get-a-customer-s-usage-spending-budget.md)
- **Customerusagesummary** kaynağını kullanarak [müşterinin kullanım bütçesini güncelleştirme](update-a-customer-s-usage-spending-budget.md)
