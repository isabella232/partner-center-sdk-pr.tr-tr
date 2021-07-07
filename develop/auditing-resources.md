---
title: Kaynakları denetleme
description: Denetim İş Ortağı Merkezi kaydını almak için kullanabileceğiniz AuditRecord gibi api denetim kaynakları hakkında İş Ortağı Merkezi öğrenin.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d78a305c2d27dc692c609e30817b34b1f814157
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974361"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Etkinlik kaydını alamanıza yardımcı olan İş Ortağı Merkezi denetleme

Denetim işlemleriyle aşağıdaki kaynakları kullanabilirsiniz.

## <a name="auditrecord"></a>AuditRecord

bir iş ortağı kullanıcı veya uygulama tarafından gerçekleştirilen bir işlem kaydını temsil eder.

| Özellik | Tür | Açıklama |
| --- | --- | ---|
| customerId | string | Müşteriyi tanımlayan GUID biçimli bir dize. |
| Müşteriadı | string | Müşteri adı. |
| userPrincipalName | string | Kullanıcı asıl adı veya kullanıcı tanımlayıcısı. Genellikle bu özellik, internet standardı RFC 822'ye göre e-posta adresi biçiminde bir kullanıcı için İnternet stili oturum açma adıdır. |
| applicationId | string | işlemi gerçekleştirilen uygulamayı tanımlayan bir dize. |
| resourceType | string | İşlem tarafından üzerinde işlem yapılan kaynak türü. Olası değerler: `customer` , , , , , , , `customer_user` , , , , `order` `subscription` , `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` `partner_customer_dap` `customer_directory_role` . |
| resourceOldValue | string | Kaynağın eski değeri. |
| resourceNewValue | string | Kaynağın yeni değeri. |
| operationType | string | Gerçekleştirilen işlem türü. Olası değerler: , , , , (yalnızca korumalı alan tümleştirme `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` hesapları), `remove_partner_customer_relationship` , , , , , , `create_order` , `update_order` , , `create_customer_user` , `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` , `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` `add_user_member` `remove_user_member` . |
| operationDate | UTC tarih-saat biçiminde dize | İşlem gerçekleştirilen tarih ve saat. |
| operationStatus | string | Denetlenen işlem durumu. Olası değerler: `succeeded` , veya , yani işlem hala devam `failed` `progress` ediyor. |
| customizedData  | nesne dizisi | Ek bilgiler. Her nesne iki JSON anahtar-değer çifti içerir: birincisi ve `key` dize değeri, ikincisi ise `value` ve dize değeri. Dizideki nesne sayısı, gerçekleştirilen işlem türüne bağlıdır. |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. |
