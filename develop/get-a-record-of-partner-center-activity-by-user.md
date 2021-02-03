---
title: İş Ortağı Merkezi etkinliğinin kaydını alma
description: Bir iş ortağı Kullanıcı veya uygulama tarafından, bir süre boyunca gerçekleştirilen işlem kaydını alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f37eae8bb96c1c1e7008e8c566b085e25d8807d
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769532"
---
# <a name="get-a-record-of-partner-center-activity"></a>İş Ortağı Merkezi etkinliğinin kaydını alma

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede bir iş ortağı Kullanıcı veya uygulama tarafından bir süre içinde gerçekleştirilen işlem kaydının nasıl yapılacağı açıklanır.

Geçerli tarihten önceki 30 güne ait denetim kayıtlarını veya başlangıç tarihi ile/veya bitiş tarihi dahil ederek belirtilen bir tarih aralığını almak için bu API 'yi kullanın. Bununla birlikte, performans nedenleriyle etkinlik günlüğü veri kullanılabilirliğinin önceki 90 güne sınırlı olduğunu unutmayın. Geçerli tarihten önce 90 günden daha büyük bir başlangıç tarihi olan istekler, hatalı bir istek özel durumu (hata kodu: 400) ve uygun bir ileti alır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

Iş Ortağı Merkezi işlemlerinin kaydını almak için, önce almak istediğiniz kayıtların tarih aralığını oluşturun. Aşağıdaki kod örneği yalnızca bir başlangıç tarihi kullanır, ancak bir bitiş tarihi de ekleyebilirsiniz. Daha fazla bilgi için bkz. [**sorgu**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) yöntemi. Ardından, uygulamak istediğiniz filtre türü için gereken değişkenleri oluşturun ve uygun değerleri atayın. Örneğin, şirket adı alt dizesini filtrelemek için alt dizeyi tutacak bir değişken oluşturun. Müşteri KIMLIĞINE göre filtrelemek için, KIMLIĞI tutacak bir değişken oluşturun.

Aşağıdaki örnekte, bir şirket adı alt dizesi, müşteri KIMLIĞI veya kaynak türüne göre filtrelemek için örnek kod sağlanır. Bunlardan birini seçin ve diğerlerini yorum yapın. Her durumda, filtre oluşturmak için önce varsayılan [**oluşturucusunu**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) kullanarak bir [**simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi örnekleyebilirsiniz. Aranacak alanı içeren bir dizeyi ve gösterildiği gibi uygulanacak uygun işleci geçirmeniz gerekir. Filtreleyecek dizeyi de sağlamanız gerekir.

Ardından, denetim kaydı işlemlerine bir arabirim almak için [**Auditrecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) özelliğini kullanın ve filtreyi yürütmek ve sonucun ilk sayfasını temsil eden [**auditrecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) koleksiyonunu almak Için [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) veya [**queryasync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) yöntemini çağırın. Yöntemi başlangıç tarihini, burada örnekte kullanılmamış bir isteğe bağlı bitiş tarihini ve bir varlıkta bir sorguyu temsil eden bir [**ıquery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesini geçirin. Iquery nesnesi yukarıda oluşturulan filtre, [**Queryfactory 'nin**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemine geçirilerek oluşturulur.

Öğelerin ilk sayfasını aldıktan sonra, kalan sayfalarda yinelemek için kullanabileceğiniz bir Numaralandırıcı oluşturmak için [**Numaralandırıcılar. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) metodunu kullanın.

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

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **klasörü**: denetim

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {STARTDATE} http/1.1                                                                                                     |
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {EndDate} http/1.1                                                                                   |
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {endDate} &filtre = {"alan": "COMPANYNAME", "Value": "{searchsubstrıng}", "operator": "Substring"} http/1.1 |
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {endDate} &filtre = {"alan": "CustomerID", "Value": "{CustomerID}", "operator": "Equals"} http/1.1          |
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {endDate} &filtre = {"alan": "ResourceType", "Value": "{ResourceType}", "işleç": "Equals"} http/1.1      |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki sorgu parametrelerini kullanın.

| Ad      | Tür   | Gerekli | Açıklama                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Başlangıç | date   | No       | Yyyy-AA-GG biçiminde başlangıç tarihi. Hiçbiri sağlanmazsa, sonuç kümesi, istek tarihinden önce varsayılan olarak 30 gün olur. Bir filtre sağlandığında bu parametre isteğe bağlıdır.                                          |
| endDate   | date   | No       | Yyyy-AA-GG biçiminde bitiş tarihi. Bir filtre sağlandığında bu parametre isteğe bağlıdır. Bitiş tarihi atlanmışsa veya null olarak ayarlandığında, istek en büyük pencereyi döndürür veya günün bitiş tarihi olarak (hangisi daha küçükse) kullanır. |
| filtre    | dize | No       | Uygulanacak filtre. Bu parametre kodlanmış bir dize olmalıdır. Başlangıç tarihi veya bitiş tarihi sağlandığında bu parametre isteğe bağlıdır.                                                                                              |

### <a name="filter-syntax"></a>Filtre sözdizimi
Filtre parametresini bir dizi virgülle ayrılmış anahtar-değer çiftleri olarak oluşturmanız gerekir. Her anahtar ve değer tek tek tırnak içine alınmalıdır ve iki nokta ile ayrılmalıdır. Filtrenin tamamının kodlanmış olması gerekir.

Kodlanamayan bir örnek şuna benzer:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

Aşağıdaki tabloda gerekli anahtar-değer çiftleri açıklanmaktadır:

| Anahtar                 | Değer                             |
|:--------------------|:----------------------------------|
| Alan               | Filtrelenecek alan. Desteklenen değerler [istek sözdiziminde](get-a-record-of-partner-center-activity-by-user.md#rest-request)bulunabilir.                                         |
| Değer               | Filtrelenecek değer. Değerin durumu yok sayılır. Aşağıdaki değer parametreleri, [istek sözdiziminde](get-a-record-of-partner-center-activity-by-user.md#rest-request)gösterildiği gibi desteklenir:<br/><br/>                                                                *Searchsubstring* -Şirket adıyla değiştirin. Şirket adının bir bölümünü eşleştirmek için bir alt dize girebilirsiniz (örneğin, `bri` eşleştirecektir `Fabrikam, Inc` ).<br/>**Örnek:**`"Value":"bri"`<br/><br/>                                                                *CustomerID* -müşteri tanımlayıcısını temsil eden bir GUID biçimli dize ile değiştirin.<br/>**Örnek:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *ResourceType* -denetim kayıtlarının alınacağı kaynak türüyle değiştirin (örneğin, abonelik). Kullanılabilir kaynak türleri [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)içinde tanımlanır.<br/>**Örnek:**`"Value":"Subscription"`                                 |
| Operatör          | Uygulanacak işleç. Desteklenen işleçler [istek sözdiziminde](get-a-record-of-partner-center-activity-by-user.md#rest-request)bulunabilir.   |

### <a name="request-headers"></a>İstek üst bilgileri

- Daha fazla bilgi için bkz. [parter Center Rest üst bilgileri](headers.md) .

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

Başarılı olursa, bu yöntem filtreleri karşılayan bir etkinlik kümesi döndürür.

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