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
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="513e5-103">İş Ortağı Merkezi etkinliğinin kaydını alma</span><span class="sxs-lookup"><span data-stu-id="513e5-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="513e5-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="513e5-104">**Applies To**</span></span>

- <span data-ttu-id="513e5-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="513e5-105">Partner Center</span></span>
- <span data-ttu-id="513e5-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="513e5-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="513e5-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="513e5-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="513e5-108">Bu makalede bir iş ortağı Kullanıcı veya uygulama tarafından bir süre içinde gerçekleştirilen işlem kaydının nasıl yapılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="513e5-108">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="513e5-109">Geçerli tarihten önceki 30 güne ait denetim kayıtlarını veya başlangıç tarihi ile/veya bitiş tarihi dahil ederek belirtilen bir tarih aralığını almak için bu API 'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="513e5-109">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="513e5-110">Bununla birlikte, performans nedenleriyle etkinlik günlüğü veri kullanılabilirliğinin önceki 90 güne sınırlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="513e5-110">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="513e5-111">Geçerli tarihten önce 90 günden daha büyük bir başlangıç tarihi olan istekler, hatalı bir istek özel durumu (hata kodu: 400) ve uygun bir ileti alır.</span><span class="sxs-lookup"><span data-stu-id="513e5-111">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="513e5-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="513e5-112">Prerequisites</span></span>

- <span data-ttu-id="513e5-113">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="513e5-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="513e5-114">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="513e5-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="513e5-115">C\#</span><span class="sxs-lookup"><span data-stu-id="513e5-115">C\#</span></span>

<span data-ttu-id="513e5-116">Iş Ortağı Merkezi işlemlerinin kaydını almak için, önce almak istediğiniz kayıtların tarih aralığını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="513e5-116">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="513e5-117">Aşağıdaki kod örneği yalnızca bir başlangıç tarihi kullanır, ancak bir bitiş tarihi de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="513e5-117">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="513e5-118">Daha fazla bilgi için bkz. [**sorgu**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="513e5-118">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="513e5-119">Ardından, uygulamak istediğiniz filtre türü için gereken değişkenleri oluşturun ve uygun değerleri atayın.</span><span class="sxs-lookup"><span data-stu-id="513e5-119">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="513e5-120">Örneğin, şirket adı alt dizesini filtrelemek için alt dizeyi tutacak bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="513e5-120">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="513e5-121">Müşteri KIMLIĞINE göre filtrelemek için, KIMLIĞI tutacak bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="513e5-121">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="513e5-122">Aşağıdaki örnekte, bir şirket adı alt dizesi, müşteri KIMLIĞI veya kaynak türüne göre filtrelemek için örnek kod sağlanır.</span><span class="sxs-lookup"><span data-stu-id="513e5-122">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="513e5-123">Bunlardan birini seçin ve diğerlerini yorum yapın.</span><span class="sxs-lookup"><span data-stu-id="513e5-123">Choose one and comment out the others.</span></span> <span data-ttu-id="513e5-124">Her durumda, filtre oluşturmak için önce varsayılan [**oluşturucusunu**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) kullanarak bir [**simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi örnekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="513e5-124">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="513e5-125">Aranacak alanı içeren bir dizeyi ve gösterildiği gibi uygulanacak uygun işleci geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="513e5-125">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="513e5-126">Filtreleyecek dizeyi de sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="513e5-126">You also must provide the string to filter by.</span></span>

<span data-ttu-id="513e5-127">Ardından, denetim kaydı işlemlerine bir arabirim almak için [**Auditrecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) özelliğini kullanın ve filtreyi yürütmek ve sonucun ilk sayfasını temsil eden [**auditrecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) koleksiyonunu almak Için [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) veya [**queryasync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="513e5-127">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="513e5-128">Yöntemi başlangıç tarihini, burada örnekte kullanılmamış bir isteğe bağlı bitiş tarihini ve bir varlıkta bir sorguyu temsil eden bir [**ıquery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="513e5-128">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="513e5-129">Iquery nesnesi yukarıda oluşturulan filtre, [**Queryfactory 'nin**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemine geçirilerek oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="513e5-129">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="513e5-130">Öğelerin ilk sayfasını aldıktan sonra, kalan sayfalarda yinelemek için kullanabileceğiniz bir Numaralandırıcı oluşturmak için [**Numaralandırıcılar. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="513e5-130">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

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

<span data-ttu-id="513e5-131">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="513e5-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="513e5-132">**Proje**: Iş Ortağı Merkezi SDK örnekleri **klasörü**: denetim</span><span class="sxs-lookup"><span data-stu-id="513e5-132">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="513e5-133">REST isteği</span><span class="sxs-lookup"><span data-stu-id="513e5-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="513e5-134">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="513e5-134">Request syntax</span></span>

| <span data-ttu-id="513e5-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="513e5-135">Method</span></span>  | <span data-ttu-id="513e5-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="513e5-136">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="513e5-137">**Al**</span><span class="sxs-lookup"><span data-stu-id="513e5-137">**GET**</span></span> | <span data-ttu-id="513e5-138">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {STARTDATE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="513e5-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="513e5-139">**Al**</span><span class="sxs-lookup"><span data-stu-id="513e5-139">**GET**</span></span> | <span data-ttu-id="513e5-140">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {EndDate} http/1.1</span><span class="sxs-lookup"><span data-stu-id="513e5-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="513e5-141">**Al**</span><span class="sxs-lookup"><span data-stu-id="513e5-141">**GET**</span></span> | <span data-ttu-id="513e5-142">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {endDate} &filtre = {"alan": "COMPANYNAME", "Value": "{searchsubstrıng}", "operator": "Substring"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="513e5-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="513e5-143">**Al**</span><span class="sxs-lookup"><span data-stu-id="513e5-143">**GET**</span></span> | <span data-ttu-id="513e5-144">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {endDate} &filtre = {"alan": "CustomerID", "Value": "{CustomerID}", "operator": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="513e5-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="513e5-145">**Al**</span><span class="sxs-lookup"><span data-stu-id="513e5-145">**GET**</span></span> | <span data-ttu-id="513e5-146">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &EndDate = {endDate} &filtre = {"alan": "ResourceType", "Value": "{ResourceType}", "işleç": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="513e5-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="513e5-147">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="513e5-147">URI parameter</span></span>

<span data-ttu-id="513e5-148">İsteği oluştururken aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="513e5-148">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="513e5-149">Ad</span><span class="sxs-lookup"><span data-stu-id="513e5-149">Name</span></span>      | <span data-ttu-id="513e5-150">Tür</span><span class="sxs-lookup"><span data-stu-id="513e5-150">Type</span></span>   | <span data-ttu-id="513e5-151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="513e5-151">Required</span></span> | <span data-ttu-id="513e5-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="513e5-152">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="513e5-153">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="513e5-153">startDate</span></span> | <span data-ttu-id="513e5-154">date</span><span class="sxs-lookup"><span data-stu-id="513e5-154">date</span></span>   | <span data-ttu-id="513e5-155">No</span><span class="sxs-lookup"><span data-stu-id="513e5-155">No</span></span>       | <span data-ttu-id="513e5-156">Yyyy-AA-GG biçiminde başlangıç tarihi.</span><span class="sxs-lookup"><span data-stu-id="513e5-156">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="513e5-157">Hiçbiri sağlanmazsa, sonuç kümesi, istek tarihinden önce varsayılan olarak 30 gün olur.</span><span class="sxs-lookup"><span data-stu-id="513e5-157">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="513e5-158">Bir filtre sağlandığında bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="513e5-158">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="513e5-159">endDate</span><span class="sxs-lookup"><span data-stu-id="513e5-159">endDate</span></span>   | <span data-ttu-id="513e5-160">date</span><span class="sxs-lookup"><span data-stu-id="513e5-160">date</span></span>   | <span data-ttu-id="513e5-161">No</span><span class="sxs-lookup"><span data-stu-id="513e5-161">No</span></span>       | <span data-ttu-id="513e5-162">Yyyy-AA-GG biçiminde bitiş tarihi.</span><span class="sxs-lookup"><span data-stu-id="513e5-162">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="513e5-163">Bir filtre sağlandığında bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="513e5-163">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="513e5-164">Bitiş tarihi atlanmışsa veya null olarak ayarlandığında, istek en büyük pencereyi döndürür veya günün bitiş tarihi olarak (hangisi daha küçükse) kullanır.</span><span class="sxs-lookup"><span data-stu-id="513e5-164">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="513e5-165">filtre</span><span class="sxs-lookup"><span data-stu-id="513e5-165">filter</span></span>    | <span data-ttu-id="513e5-166">dize</span><span class="sxs-lookup"><span data-stu-id="513e5-166">string</span></span> | <span data-ttu-id="513e5-167">No</span><span class="sxs-lookup"><span data-stu-id="513e5-167">No</span></span>       | <span data-ttu-id="513e5-168">Uygulanacak filtre.</span><span class="sxs-lookup"><span data-stu-id="513e5-168">The filter to apply.</span></span> <span data-ttu-id="513e5-169">Bu parametre kodlanmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="513e5-169">This parameter must be an encoded string.</span></span> <span data-ttu-id="513e5-170">Başlangıç tarihi veya bitiş tarihi sağlandığında bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="513e5-170">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="513e5-171">Filtre sözdizimi</span><span class="sxs-lookup"><span data-stu-id="513e5-171">Filter syntax</span></span>
<span data-ttu-id="513e5-172">Filtre parametresini bir dizi virgülle ayrılmış anahtar-değer çiftleri olarak oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="513e5-172">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="513e5-173">Her anahtar ve değer tek tek tırnak içine alınmalıdır ve iki nokta ile ayrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="513e5-173">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="513e5-174">Filtrenin tamamının kodlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="513e5-174">The entire filter must be encoded.</span></span>

<span data-ttu-id="513e5-175">Kodlanamayan bir örnek şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="513e5-175">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="513e5-176">Aşağıdaki tabloda gerekli anahtar-değer çiftleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="513e5-176">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="513e5-177">Anahtar</span><span class="sxs-lookup"><span data-stu-id="513e5-177">Key</span></span>                 | <span data-ttu-id="513e5-178">Değer</span><span class="sxs-lookup"><span data-stu-id="513e5-178">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="513e5-179">Alan</span><span class="sxs-lookup"><span data-stu-id="513e5-179">Field</span></span>               | <span data-ttu-id="513e5-180">Filtrelenecek alan.</span><span class="sxs-lookup"><span data-stu-id="513e5-180">The field to filter.</span></span> <span data-ttu-id="513e5-181">Desteklenen değerler [istek sözdiziminde](get-a-record-of-partner-center-activity-by-user.md#rest-request)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="513e5-181">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="513e5-182">Değer</span><span class="sxs-lookup"><span data-stu-id="513e5-182">Value</span></span>               | <span data-ttu-id="513e5-183">Filtrelenecek değer.</span><span class="sxs-lookup"><span data-stu-id="513e5-183">The value to filter by.</span></span> <span data-ttu-id="513e5-184">Değerin durumu yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="513e5-184">The case of the value is ignored.</span></span> <span data-ttu-id="513e5-185">Aşağıdaki değer parametreleri, [istek sözdiziminde](get-a-record-of-partner-center-activity-by-user.md#rest-request)gösterildiği gibi desteklenir:</span><span class="sxs-lookup"><span data-stu-id="513e5-185">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="513e5-186">*Searchsubstring* -Şirket adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="513e5-186">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="513e5-187">Şirket adının bir bölümünü eşleştirmek için bir alt dize girebilirsiniz (örneğin, `bri` eşleştirecektir `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="513e5-187">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="513e5-188">**Örnek:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="513e5-188">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="513e5-189">*CustomerID* -müşteri tanımlayıcısını temsil eden bir GUID biçimli dize ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="513e5-189">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="513e5-190">**Örnek:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="513e5-190">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="513e5-191">*ResourceType* -denetim kayıtlarının alınacağı kaynak türüyle değiştirin (örneğin, abonelik).</span><span class="sxs-lookup"><span data-stu-id="513e5-191">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="513e5-192">Kullanılabilir kaynak türleri [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="513e5-192">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="513e5-193">**Örnek:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="513e5-193">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="513e5-194">Operatör</span><span class="sxs-lookup"><span data-stu-id="513e5-194">Operator</span></span>          | <span data-ttu-id="513e5-195">Uygulanacak işleç.</span><span class="sxs-lookup"><span data-stu-id="513e5-195">The operator to apply.</span></span> <span data-ttu-id="513e5-196">Desteklenen işleçler [istek sözdiziminde](get-a-record-of-partner-center-activity-by-user.md#rest-request)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="513e5-196">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="513e5-197">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="513e5-197">Request headers</span></span>

- <span data-ttu-id="513e5-198">Daha fazla bilgi için bkz. [parter Center Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="513e5-198">See [Parter Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="513e5-199">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="513e5-199">Request body</span></span>

<span data-ttu-id="513e5-200">Yok.</span><span class="sxs-lookup"><span data-stu-id="513e5-200">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="513e5-201">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="513e5-201">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="513e5-202">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="513e5-202">REST response</span></span>

<span data-ttu-id="513e5-203">Başarılı olursa, bu yöntem filtreleri karşılayan bir etkinlik kümesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="513e5-203">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="513e5-204">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="513e5-204">Response success and error codes</span></span>

<span data-ttu-id="513e5-205">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="513e5-205">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="513e5-206">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="513e5-206">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="513e5-207">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="513e5-207">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="513e5-208">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="513e5-208">Response example</span></span>

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