---
title: İş Ortağı Merkezi etkinliğinin kaydını alma
description: Bir iş ortağı kullanıcı veya uygulama tarafından bir süre içinde gerçekleştirilen işlemlerin kaydını alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aec933d4b681d99080619505792bde56bdd25580
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873981"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="c7cbe-103">İş Ortağı Merkezi etkinliğinin kaydını alma</span><span class="sxs-lookup"><span data-stu-id="c7cbe-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="c7cbe-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c7cbe-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c7cbe-105">Bu makalede, bir iş ortağı kullanıcı veya uygulama tarafından belirli bir süre boyunca gerçekleştirilen işlemlerin kaydını alma işlemi açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-105">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="c7cbe-106">Geçerli tarihten itibaren son 30 güne veya başlangıç tarihi ve/veya bitiş tarihi dahil olmak üzere belirtilen bir tarih aralığına yönelik denetim kayıtlarını almak için bu API'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-106">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="c7cbe-107">Ancak, performans nedenleriyle etkinlik günlüğü veri kullanılabilirliğinin son 90 günle sınırlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-107">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="c7cbe-108">Geçerli tarihten 90 gün önce başlangıç tarihine sahip istekler hatalı bir istek özel durumu (hata kodu: 400) ve uygun bir ileti alır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-108">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7cbe-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c7cbe-109">Prerequisites</span></span>

- <span data-ttu-id="c7cbe-110">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c7cbe-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c7cbe-111">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="c7cbe-112">C\#</span><span class="sxs-lookup"><span data-stu-id="c7cbe-112">C\#</span></span>

<span data-ttu-id="c7cbe-113">Bu işlemlerin İş Ortağı Merkezi almak için, önce almak istediğiniz kayıtların tarih aralığını seçin.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-113">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="c7cbe-114">Aşağıdaki kod örneği yalnızca bir başlangıç tarihi kullanır, ancak bir bitiş tarihi de dahildir.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-114">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="c7cbe-115">Daha fazla bilgi için [**bkz. Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-115">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="c7cbe-116">Ardından, uygulamak istediğiniz filtre türü için ihtiyacınız olan değişkenleri oluşturun ve uygun değerleri attayin.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-116">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="c7cbe-117">Örneğin, şirket adı alt dizeye göre filtrelemek için alt dizeyi tutmak için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-117">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="c7cbe-118">Müşteri kimliğine göre filtrelemek için kimliği tutmak için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-118">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="c7cbe-119">Aşağıdaki örnekte, bir şirket adı alt dize, müşteri kimliği veya kaynak türüne göre filtrelemek için örnek kod sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-119">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="c7cbe-120">Birini seçin ve diğerlerini açıklamaya alma.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-120">Choose one and comment out the others.</span></span> <span data-ttu-id="c7cbe-121">Her durumda, ilk olarak filtreyi oluşturmak için varsayılan [](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) oluşturucusu kullanarak [**bir SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi örneği oluştururuz.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-121">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="c7cbe-122">Aranacak alanı ve uygulanacak uygun işleci içeren bir dizeyi aşağıda gösterildiği gibi geçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-122">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="c7cbe-123">Ayrıca, filtrelemek için dizesini de sağlanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-123">You also must provide the string to filter by.</span></span>

<span data-ttu-id="c7cbe-124">Ardından, kayıt işlemlerini denetlemeye yönelik bir arabirim almak için [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) özelliğini kullanın ve filtreyi yürütmek ve sonucun ilk sayfasını temsil eden [**AuditRecord'ların**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) koleksiyonunu almak için [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) veya [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-124">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="c7cbe-125">yöntemine başlangıç tarihini, buradaki örnekte kullanılmayan isteğe bağlı bir bitiş tarihini ve bir varlık üzerinde sorguyu temsil eden [**bir IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesini iletir.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-125">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="c7cbe-126">IQuery nesnesi, yukarıda oluşturulan filtre [**QueryFactory'nin**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery yöntemine geçerek**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-126">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="c7cbe-127">Öğelerin ilk sayfasına sahip olduktan sonra, kalan sayfalarda yinelerken kullanabileceğiniz bir numaralayıcı oluşturmak için [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-127">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

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

<span data-ttu-id="c7cbe-128">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c7cbe-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c7cbe-129">**Project:** İş Ortağı Merkezi SDK'sı Samples **Klasörü:** Denetim</span><span class="sxs-lookup"><span data-stu-id="c7cbe-129">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="c7cbe-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c7cbe-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c7cbe-131">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="c7cbe-131">Request syntax</span></span>

| <span data-ttu-id="c7cbe-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c7cbe-132">Method</span></span>  | <span data-ttu-id="c7cbe-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c7cbe-133">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c7cbe-134">**Al**</span><span class="sxs-lookup"><span data-stu-id="c7cbe-134">**GET**</span></span> | <span data-ttu-id="c7cbe-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c7cbe-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="c7cbe-136">**Al**</span><span class="sxs-lookup"><span data-stu-id="c7cbe-136">**GET**</span></span> | <span data-ttu-id="c7cbe-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c7cbe-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="c7cbe-138">**Al**</span><span class="sxs-lookup"><span data-stu-id="c7cbe-138">**GET**</span></span> | <span data-ttu-id="c7cbe-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c7cbe-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="c7cbe-140">**Al**</span><span class="sxs-lookup"><span data-stu-id="c7cbe-140">**GET**</span></span> | <span data-ttu-id="c7cbe-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c7cbe-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="c7cbe-142">**Al**</span><span class="sxs-lookup"><span data-stu-id="c7cbe-142">**GET**</span></span> | <span data-ttu-id="c7cbe-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c7cbe-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="c7cbe-144">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="c7cbe-144">URI parameter</span></span>

<span data-ttu-id="c7cbe-145">İsteği oluştururken aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-145">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="c7cbe-146">Ad</span><span class="sxs-lookup"><span data-stu-id="c7cbe-146">Name</span></span>      | <span data-ttu-id="c7cbe-147">Tür</span><span class="sxs-lookup"><span data-stu-id="c7cbe-147">Type</span></span>   | <span data-ttu-id="c7cbe-148">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c7cbe-148">Required</span></span> | <span data-ttu-id="c7cbe-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c7cbe-149">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c7cbe-150">Startdate</span><span class="sxs-lookup"><span data-stu-id="c7cbe-150">startDate</span></span> | <span data-ttu-id="c7cbe-151">date</span><span class="sxs-lookup"><span data-stu-id="c7cbe-151">date</span></span>   | <span data-ttu-id="c7cbe-152">Hayır</span><span class="sxs-lookup"><span data-stu-id="c7cbe-152">No</span></span>       | <span data-ttu-id="c7cbe-153">yyyy-mm-dd biçiminde başlangıç tarihi.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-153">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="c7cbe-154">Hiçbiri sağlanmayacaksa, sonuç kümesi varsayılan olarak istek tarihinden 30 gün önce olur.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-154">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="c7cbe-155">Bir filtre sağlanmalıdır, bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-155">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="c7cbe-156">Bitiştarihi</span><span class="sxs-lookup"><span data-stu-id="c7cbe-156">endDate</span></span>   | <span data-ttu-id="c7cbe-157">date</span><span class="sxs-lookup"><span data-stu-id="c7cbe-157">date</span></span>   | <span data-ttu-id="c7cbe-158">Hayır</span><span class="sxs-lookup"><span data-stu-id="c7cbe-158">No</span></span>       | <span data-ttu-id="c7cbe-159">yyyy-mm-dd biçiminde bitiş tarihi.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-159">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="c7cbe-160">Bir filtre sağlanmalıdır, bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-160">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="c7cbe-161">Bitiş tarihi atlanırsa veya null olarak ayarlanırsa istek maksimum pencereyi döndürür veya bugün bitiş tarihi olarak (hangisi daha düşükse) kullanır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-161">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="c7cbe-162">filtre</span><span class="sxs-lookup"><span data-stu-id="c7cbe-162">filter</span></span>    | <span data-ttu-id="c7cbe-163">dize</span><span class="sxs-lookup"><span data-stu-id="c7cbe-163">string</span></span> | <span data-ttu-id="c7cbe-164">No</span><span class="sxs-lookup"><span data-stu-id="c7cbe-164">No</span></span>       | <span data-ttu-id="c7cbe-165">Uygulanacak filtre.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-165">The filter to apply.</span></span> <span data-ttu-id="c7cbe-166">Bu parametre kodlanmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-166">This parameter must be an encoded string.</span></span> <span data-ttu-id="c7cbe-167">Başlangıç tarihi veya bitiş tarihi sağlanmalıdır, bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-167">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="c7cbe-168">Filtre söz dizimi</span><span class="sxs-lookup"><span data-stu-id="c7cbe-168">Filter syntax</span></span>
<span data-ttu-id="c7cbe-169">Filtre parametresini virgülle ayrılmış bir dizi anahtar-değer çifti olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-169">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="c7cbe-170">Her anahtar ve değer ayrı ayrı tırnak içine alınarak iki nokta üst üste ile ayrılarak ayrılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-170">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="c7cbe-171">Filtrenin tamamı kodlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-171">The entire filter must be encoded.</span></span>

<span data-ttu-id="c7cbe-172">Kodlanmamış bir örnek şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="c7cbe-172">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="c7cbe-173">Aşağıdaki tabloda gerekli anahtar-değer çiftleri açıkmektedir:</span><span class="sxs-lookup"><span data-stu-id="c7cbe-173">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="c7cbe-174">Anahtar</span><span class="sxs-lookup"><span data-stu-id="c7cbe-174">Key</span></span>                 | <span data-ttu-id="c7cbe-175">Değer</span><span class="sxs-lookup"><span data-stu-id="c7cbe-175">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="c7cbe-176">Alan</span><span class="sxs-lookup"><span data-stu-id="c7cbe-176">Field</span></span>               | <span data-ttu-id="c7cbe-177">Filtrenin yer alan.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-177">The field to filter.</span></span> <span data-ttu-id="c7cbe-178">Desteklenen değerler İstek söz [dizimsinde bulunabilir.](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="c7cbe-178">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="c7cbe-179">Değer</span><span class="sxs-lookup"><span data-stu-id="c7cbe-179">Value</span></span>               | <span data-ttu-id="c7cbe-180">Filtreye göre değer.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-180">The value to filter by.</span></span> <span data-ttu-id="c7cbe-181">Değerin durumu yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-181">The case of the value is ignored.</span></span> <span data-ttu-id="c7cbe-182">Aşağıdaki değer parametreleri İstek söz dizimsinde gösterildiği [gibi de destekledik:](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="c7cbe-182">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="c7cbe-183">*searchSubstring* - yerine şirketin adını yazın.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-183">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="c7cbe-184">Şirket adının bir bölümüyle eşleşmesi için bir alt dize girsiniz (örneğin, `bri` ile `Fabrikam, Inc` eşler).</span><span class="sxs-lookup"><span data-stu-id="c7cbe-184">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="c7cbe-185">**Örnek:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="c7cbe-185">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="c7cbe-186">*customerId* - Müşteri tanımlayıcısını temsil eden GUID biçimli bir dizeyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-186">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="c7cbe-187">**Örnek:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="c7cbe-187">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="c7cbe-188">*resourceType* - Denetim kayıtlarının alınıp alınmayacak kaynak türüyle (örneğin, Abonelik) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-188">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="c7cbe-189">Kullanılabilir kaynak türleri ResourceType içinde [tanımlanır.](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)</span><span class="sxs-lookup"><span data-stu-id="c7cbe-189">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="c7cbe-190">**Örnek:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="c7cbe-190">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="c7cbe-191">Operatör</span><span class="sxs-lookup"><span data-stu-id="c7cbe-191">Operator</span></span>          | <span data-ttu-id="c7cbe-192">Uygulanacak işleç.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-192">The operator to apply.</span></span> <span data-ttu-id="c7cbe-193">Desteklenen işleçler İstek söz [dizimsinde bulunabilir.](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="c7cbe-193">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="c7cbe-194">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c7cbe-194">Request headers</span></span>

- <span data-ttu-id="c7cbe-195">Daha fazla bilgi için [bkz. Parter Center REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c7cbe-195">For more information, see [Parter Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c7cbe-196">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c7cbe-196">Request body</span></span>

<span data-ttu-id="c7cbe-197">Yok.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-197">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c7cbe-198">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c7cbe-198">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c7cbe-199">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c7cbe-199">REST response</span></span>

<span data-ttu-id="c7cbe-200">Başarılı olursa, bu yöntem filtreleri karşılar bir dizi etkinlik döndürür.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-200">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c7cbe-201">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c7cbe-201">Response success and error codes</span></span>

<span data-ttu-id="c7cbe-202">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-202">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c7cbe-203">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7cbe-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c7cbe-204">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c7cbe-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c7cbe-205">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c7cbe-205">Response example</span></span>

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