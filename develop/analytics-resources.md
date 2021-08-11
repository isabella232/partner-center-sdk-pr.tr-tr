---
title: Analiz kaynakları
description: İş ortağı merkezi kaynakları, kullanım, dağıtım ve tüketim hakkındaki verileri içerir. İş ortakları ve müşterilerin lisans dağıtımı ve kullanımı hakkındaki öngörüleri içerir.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: fc665e8e4468648f71f242992780fbc66a02522a0b8b957a5ce68147ab33eaac
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993206"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Lisans kullanımı, dağıtımı ve tüketimi hakkında rapor etmenize yardımcı olan analitik API kaynakları

Burada tanımlanan kaynaklar kullanımı, dağıtımı ve tüketimi raporlamak için kullanılan verileri içerir.

## <a name="partnerlicensesdeploymentinsights"></a>Partnerlicensesdeploymentınsıghts

**Partnerlicensesdeploymentinsıghts** kaynağı, lisans dağıtımı hakkında iş ortağı düzeyi öngörüleri içerir.

| Özellik                  | Tür                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Eşit oranda bulunan Deploymentpercent | sayı                                                         | Dağıtılan lisansların yüzdesi.                                                |
| Lisanssesseski              | sayı                                                         | Satılan lisansların sayısı.                                                        |
| processedDateTime         | UTC Tarih-saat biçiminde dize                                 | Verilerin toplanalındığı tarih ve saat.                                     |
| HizmetAdı               | string                                                         | Hizmet adı (örneğin: O365, CRM).                                                  |
| kanalla                   | string                                                         | Hizmetin kanal adı (örneğin: satıcı).                                    |
| öznitelikler                | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. "ObjectType" içerir: "Partnerlicensesdeploymentınsıghts" |

## <a name="partnerlicensesusageinsights"></a>Partnerlicensesusageınsights

**Partnerlicensesusageresource** , lisans kullanımı hakkında iş ortağı düzeyi öngörüleri içerir.

| Özellik                     | Tür                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| Eşit oranda bulunan Licensesusage yüzdesi | sayı                                                         | Dağıtılan lisansların yüzdesi.                                           |
| workloadName                 | string                                                         | İş yükü adı (örneğin: Exchange).                                             |
| processedDateTime            | UTC Tarih-saat biçiminde dize                                 | Verilerin toplanalındığı tarih ve saat.                                |
| HizmetAdı                  | string                                                         | Hizmet adı (örneğin: O365, CRM).                                             |
| kanalla                      | string                                                         | Hizmetin kanal adı (örneğin: satıcı).                               |
| öznitelikler                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. "ObjectType" içerir: "Partnerlicensesusageınsights" |

## <a name="customerlicensesdeploymentinsights"></a>Customerlicensesdeploymentınsıghts

**Customerlicensesdeploymentinsıghts** kaynağı, lisans dağıtımıyla ilgili müşteri düzeyi öngörüleri içerir.

| Özellik          | Tür                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Licensesdağıtıldı  | sayı                                                         | Dağıtılan lisansların sayısı.                                                     |
| Lisanssesseski      | sayı                                                         | Satılan lisansların sayısı.                                                         |
| deploymentPercent | sayı                                                         | Dağıtılan lisansların yüzdesi.                                        |
| customerId        | string                                                         | Müşteri tanımlayıcısı.                                                             |
| customerName      | string                                                         | Müşteri adı.                                                                   |
| productName       | string                                                         | Ürün adı.                                                                    |
| serviceCode       | string                                                         | Lisansın hizmet kodu.                                                     |
| processedDateTime | UTC Tarih-saat biçiminde dize                                 | Verilerin toplanalındığı tarih ve saat.                                      |
| HizmetAdı       | string                                                         | Hizmet adı (örneğin: O365, CRM).                                                   |
| kanalla           | string                                                         | Hizmetin kanal adı (örneğin: satıcı).                                     |
| öznitelikler        | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. "ObjectType" içerir: "Customerlicensesdeploymentinsıghts" |

## <a name="customerlicensesusageinsights"></a>Customerlicensesusageınsights

**Customerlicensesusageınsights** kaynağı, lisans kullanımı hakkında müşteri düzeyi öngörüleri içerir.

| Özellik          | Tür                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | string                                                         | İş yükü kodu.                                                              |
| workloadName      | sayı                                                         | İş yükü adı (örneğin: Exchange).                                              |
| usagePercent      | sayı                                                         | Kullanılan lisansların ayarlanmış yüzdesi.                                       |
| licensesActive    | sayı                                                         | Etkin lisansların sayısı.                                                  |
| licensesQualified | sayı                                                         | Nitelikli lisans sayısı.                                               |
| customerId        | string                                                         | Müşteri tanımlayıcısı.                                                        |
| Müşteriadı      | string                                                         | Müşteri adı.                                                              |
| Productname       | string                                                         | Ürün adı.                                                               |
| serviceCode       | string                                                         | Lisansın hizmet kodu.                                                |
| processedDateTime | UTC tarih-saat biçiminde dize                                 | Verilerin toplanmış olduğu tarih ve saat.                                 |
| Hizmetadı       | string                                                         | Hizmet adı (örneğin: o365, crm).                                              |
| Kanal           | string                                                         | Hizmetin kanal adı (örneğin: kurumsal bayi).                                |
| öznitelikler        | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. "objectType" içerir: "CustomerLicensesUsageInsights" |