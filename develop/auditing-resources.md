---
title: Kaynakları denetleme
description: Iş Ortağı Merkezi etkinliğinin kaydını almak için kullanabileceğiniz AuditRecord gibi Iş Ortağı Merkezi API denetim kaynakları hakkında bilgi edinin.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c4b39cbc4d69447fbc8e6ef4528dd6dce11cd3f4
ms.sourcegitcommit: fa183a942f51cab8bdb42dbe7da4c8eab550e0a0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2021
ms.locfileid: "98759176"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Iş Ortağı Merkezi etkinliğinin kaydını almanıza yardımcı olan kaynakları denetleme

**Uygulama hedefi:**

- İş Ortağı Merkezi

Aşağıdaki kaynakları denetim işlemleriyle birlikte kullanabilirsiniz.

## <a name="auditrecord"></a>AuditRecord

Bir iş ortağı Kullanıcı veya uygulama tarafından gerçekleştirilen bir işlemin kaydını temsil eder.

| Özellik | Tür | Açıklama |
| --- | --- | ---|
| customerId | string | Müşteriyi tanımlayan GUID biçimli bir dize. |
| customerName | string | Müşteri adı. |
| userPrincipalName | string | Kullanıcı asıl adı veya Kullanıcı tanımlayıcısı. Genellikle, bu özellik Internet standart RFC 822 ' i temel alan bir e-posta adresi biçimindeki Kullanıcı için Internet stili bir oturum açma adıdır. |
| applicationId | string | İşlemi gerçekleştiren uygulamayı tanımlayan bir dize. |
| resourceType | string | İşlemin üzerinde işlem yaptığı kaynak türü. Olası değerler: `customer` , `customer_user` , `order` , `subscription` , `license` , `third_party_add_on` , `mpn_association` , `transfer` , `application` , `application_credential` , `partner_user` , `partner_relationship` , `partner_customer_dap` . |
| resourceOldValue | string | Kaynağın eski değeri. |
| resourceNewValue | string | Kaynağın yeni değeri. |
| operationType | string | Gerçekleştirilen işlem türü. Olası değerler: `update_customer_qualification` , `update_subscription` , `upgrade_subscription` , `convert_trial_subscription` , `add_customer` , `update_customer_billing_profile` , `update_customer_partner_contract_company_name` , `update_customer_spending_budget` , `delete_customer` (yalnızca Sandbox tümleştirme hesapları), `remove_partner_customer_relationship` , `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,, |
| operationDate | UTC Tarih-saat biçiminde dize | İşlemin gerçekleştirildiği tarih ve saat. |
| operationStatus | string | Denetlenen işlemin durumu. Olası değerler: `succeeded` , `failed` , veya `progress` işlemin devam ettiği anlamına gelir. |
| customizedData  | nesne dizisi | Ek bilgi. Her nesne iki JSON anahtar-değer çifti içerir: ilki `key` ve bir dize değeri, ikincisi `value` ve bir dize değeri. Dizideki nesne sayısı, gerçekleştirilen işlem türüne bağlıdır. |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. |
