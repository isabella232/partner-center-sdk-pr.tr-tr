---
title: İş Ortağı Merkezi etkinliğinin kaydını alma
description: Bir iş ortağı kullanıcı veya uygulama tarafından bir süre içinde gerçekleştirilen işlemlerin kaydını alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5d965fc226d326998212ef0f027160d50f69d5e84360c8a9d09c27a76c63310d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991081"
---
# <a name="get-a-record-of-partner-center-activity"></a>İş Ortağı Merkezi etkinliğinin kaydını alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu makalede, bir iş ortağı kullanıcı veya uygulama tarafından belirli bir süre boyunca gerçekleştirilen işlemlerin kaydını alma işlemi açıklanmıştır.

Geçerli tarihten itibaren son 30 güne veya başlangıç tarihi ve/veya bitiş tarihi dahil olmak üzere belirtilen bir tarih aralığına yönelik denetim kayıtlarını almak için bu API'yi kullanın. Ancak, performans nedenleriyle etkinlik günlüğü veri kullanılabilirliğinin son 90 günle sınırlı olduğunu unutmayın. Geçerli tarihten 90 gün önce başlangıç tarihine sahip istekler hatalı bir istek özel durumu (hata kodu: 400) ve uygun bir ileti alır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="c"></a>C\#

Bu işlemlerin İş Ortağı Merkezi almak için, önce almak istediğiniz kayıtların tarih aralığını seçin. Aşağıdaki kod örneği yalnızca bir başlangıç tarihi kullanır, ancak bir bitiş tarihi de dahildir. Daha fazla bilgi için [**bkz. Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) yöntemi. Ardından, uygulamak istediğiniz filtre türü için ihtiyacınız olan değişkenleri oluşturun ve uygun değerleri attayin. Örneğin, şirket adı alt dizeye göre filtrelemek için alt dizeyi tutmak için bir değişken oluşturun. Müşteri kimliğine göre filtrelemek için kimliği tutmak için bir değişken oluşturun.

Aşağıdaki örnekte, bir şirket adı alt dize, müşteri kimliği veya kaynak türüne göre filtrelemek için örnek kod sağlanmıştır. Birini seçin ve diğerlerini açıklamaya alma. Her durumda, ilk olarak filtreyi oluşturmak için varsayılan [](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) oluşturucusu kullanarak [**bir SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi örneği oluştururuz. Aranacak alanı ve uygulanacak uygun işleci içeren bir dizeyi aşağıda gösterildiği gibi geçmeniz gerekir. Ayrıca, filtrelemek için dizesini de sağlanız gerekir.

Ardından, kayıt işlemlerini denetlemeye yönelik bir arabirim almak için [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) özelliğini kullanın ve filtreyi yürütmek ve sonucun ilk sayfasını temsil eden [**AuditRecord'ların**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) koleksiyonunu almak için [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) veya [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) yöntemini çağırabilirsiniz. yöntemine başlangıç tarihini, buradaki örnekte kullanılmayan isteğe bağlı bir bitiş tarihini ve bir varlık üzerinde sorguyu temsil eden [**bir IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesini iletir. IQuery nesnesi, yukarıda oluşturulan filtre [**QueryFactory'nin**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery yöntemine geçerek**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) oluşturulur.

Öğelerin ilk sayfasına sahip olduktan sonra, kalan sayfalarda yinelerken kullanabileceğiniz bir numaralayıcı oluşturmak için [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) yöntemini kullanın.

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Klasörü:** Denetim

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1                                                                                                     |
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1                                                                                   |
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1 |
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1          |
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1      |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki sorgu parametrelerini kullanın.

| Ad      | Tür   | Gerekli | Açıklama                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Startdate | date   | No       | yyyy-mm-dd biçiminde başlangıç tarihi. Hiçbiri sağlanmayacaksa, sonuç kümesi varsayılan olarak istek tarihinden 30 gün önce olur. Bir filtre sağlanmalıdır, bu parametre isteğe bağlıdır.                                          |
| Bitiştarihi   | date   | No       | yyyy-mm-dd biçiminde bitiş tarihi. Bir filtre sağlanmalıdır, bu parametre isteğe bağlıdır. Bitiş tarihi atlanırsa veya null olarak ayarlanırsa istek maksimum pencereyi döndürür veya bugün bitiş tarihi olarak (hangisi daha düşükse) kullanır. |
| filtre    | dize | No       | Uygulanacak filtre. Bu parametre kodlanmış bir dize olmalıdır. Başlangıç tarihi veya bitiş tarihi sağlanmalıdır, bu parametre isteğe bağlıdır.                                                                                              |

### <a name="filter-syntax"></a>Filtre söz dizimi
Filtre parametresini virgülle ayrılmış bir dizi anahtar-değer çifti olarak oluşturabilirsiniz. Her anahtar ve değer ayrı ayrı tırnak içine alınarak iki nokta üst üste ile ayrılarak ayrılabilir. Filtrenin tamamı kodlanmış olması gerekir.

Kodlanmamış bir örnek şu şekildedir:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

Aşağıdaki tabloda gerekli anahtar-değer çiftleri açıkmektedir:

| Anahtar                 | Değer                             |
|:--------------------|:----------------------------------|
| Alan               | Filtrenin yer alan. Desteklenen değerler İstek söz [dizimsinde bulunabilir.](get-a-record-of-partner-center-activity-by-user.md#rest-request)                                         |
| Değer               | Filtreye göre değer. Değerin durumu yoksayılır. Aşağıdaki değer parametreleri İstek söz dizimsinde gösterildiği [gibi de destekledik:](get-a-record-of-partner-center-activity-by-user.md#rest-request)<br/><br/>                                                                *searchSubstring* - yerine şirketin adını yazın. Şirket adının bir bölümüyle eşleşmesi için bir alt dize girsiniz (örneğin, `bri` ile `Fabrikam, Inc` eşler).<br/>**Örnek:** `"Value":"bri"`<br/><br/>                                                                *customerId* - Müşteri tanımlayıcısını temsil eden GUID biçimli bir dizeyle değiştirin.<br/>**Örnek:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *resourceType* - Denetim kayıtlarının alınıp alınmayacak kaynak türüyle (örneğin, Abonelik) değiştirin. Kullanılabilir kaynak türleri ResourceType içinde [tanımlanır.](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)<br/>**Örnek:** `"Value":"Subscription"`                                 |
| Operatör          | Uygulanacak işleç. Desteklenen işleçler İstek söz [dizimsinde bulunabilir.](get-a-record-of-partner-center-activity-by-user.md#rest-request)   |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha fazla bilgi için [bkz. Parter Center REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem filtreleri karşılar bir dizi etkinlik döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```