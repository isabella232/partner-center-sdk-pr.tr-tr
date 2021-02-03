---
title: Müşterinin Azure kullanım kayıtlarını alma
description: Belirli bir süre boyunca bir müşterinin Azure aboneliğinin kullanım kayıtlarını almak için Azure kullanım API 'sini kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769341"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="6242c-103">Müşterinin Azure kullanım kayıtlarını alma</span><span class="sxs-lookup"><span data-stu-id="6242c-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="6242c-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="6242c-104">**Applies to:**</span></span>

- <span data-ttu-id="6242c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6242c-105">Partner Center</span></span>
- <span data-ttu-id="6242c-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6242c-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6242c-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6242c-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6242c-108">Azure kullanım API 'sini kullanarak belirli bir süre için müşterinin Azure aboneliğinin kullanım kayıtlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242c-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6242c-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6242c-109">Prerequisites</span></span>

- <span data-ttu-id="6242c-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6242c-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6242c-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="6242c-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="6242c-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6242c-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6242c-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242c-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6242c-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="6242c-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6242c-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6242c-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6242c-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="6242c-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6242c-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="6242c-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6242c-118">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="6242c-118">A subscription identifier.</span></span>

<span data-ttu-id="6242c-119">Bu API, rastgele bir zaman aralığı için günlük ve saatlik derecelendirilmemiş tüketim döndürür.</span><span class="sxs-lookup"><span data-stu-id="6242c-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="6242c-120">Ancak, *Bu API Azure planları için desteklenmez*.</span><span class="sxs-lookup"><span data-stu-id="6242c-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="6242c-121">Bir Azure planınız varsa, [Fatura faturalandırılmamış tüketim satırı öğelerini Al](get-invoice-unbilled-consumption-lineitems.md) ve [Fatura için faturalandırılan tüketim satırı öğelerini](get-invoice-billed-consumption-lineitems.md) al makalelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="6242c-121">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="6242c-122">Bu makalelerde, kaynak başına ölçüm başına her gün bir derecelendirmeden derecelendirilen tüketimin nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="6242c-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="6242c-123">Bu hız tüketimi, Azure kullanım API 'SI tarafından belirtilen günlük gren verilere eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="6242c-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="6242c-124">Fatura tanımlayıcısını, faturalandırılan kullanım verilerini almak için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6242c-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="6242c-125">Ya da, faturalandırılmamış kullanım tahminleri almak için geçerli ve önceki dönemleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242c-125">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="6242c-126">*Saatlik gren veri ve rastgele tarih aralığı filtreleri şu anda Azure plan aboneliği kaynakları için desteklenmiyor*.</span><span class="sxs-lookup"><span data-stu-id="6242c-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="6242c-127">Azure kullanım API 'SI</span><span class="sxs-lookup"><span data-stu-id="6242c-127">Azure utilization API</span></span>

<span data-ttu-id="6242c-128">Bu Azure kullanım API 'SI, kullanımın faturalandırma sisteminde ne zaman raporlanacağı temsil eden bir döneme ait kullanım kayıtlarına erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="6242c-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="6242c-129">Bu, mutabakat dosyası oluşturmak ve hesaplamak için kullanılan kullanım verilerine erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="6242c-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="6242c-130">Ancak fatura sistem mutabakatı dosya mantığı hakkında bilgi sahibi değildir.</span><span class="sxs-lookup"><span data-stu-id="6242c-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="6242c-131">Aynı zaman dilimi için bu API 'den alınan sonuçla eşleşen dosya Özeti sonuçlarının mutabakatını beklememelisiniz.</span><span class="sxs-lookup"><span data-stu-id="6242c-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="6242c-132">Örneğin, faturalandırma sistemi aynı kullanım verilerini alır ve bir mutabakat dosyasında nelerin hesaba katılmaz belirlemek için değer kuralları uygular.</span><span class="sxs-lookup"><span data-stu-id="6242c-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="6242c-133">Bir faturalandırma dönemi kapandığında, fatura döneminin sona ereceği günün sonuna kadar tüm kullanımlar mutabakat dosyasına dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="6242c-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="6242c-134">Fatura dönemi bittikten sonra 24 saat içinde raporlanan ödeme dönemi içinde herhangi bir geç kullanım, bir sonraki mutabakat dosyasında hesaba katılmaz.</span><span class="sxs-lookup"><span data-stu-id="6242c-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="6242c-135">Ortağın faturalandırılma şekli için bkz. [Azure aboneliği için tüketim verilerini alma](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="6242c-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="6242c-136">Bu REST API disk belleğine alınmış.</span><span class="sxs-lookup"><span data-stu-id="6242c-136">This REST API is paged.</span></span> <span data-ttu-id="6242c-137">Yanıt yükü tek bir sayfadan fazlaysa, kullanım kayıtlarının sonraki sayfasını almak için sonraki bağlantıyı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6242c-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

## <a name="c"></a><span data-ttu-id="6242c-138">C\#</span><span class="sxs-lookup"><span data-stu-id="6242c-138">C\#</span></span>

<span data-ttu-id="6242c-139">Azure kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="6242c-139">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="6242c-140">Müşteri KIMLIĞINI ve abonelik KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="6242c-140">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="6242c-141">Kullanım kayıtlarını içeren bir [**Resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) döndürmek için [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="6242c-141">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="6242c-142">Kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı elde edin.</span><span class="sxs-lookup"><span data-stu-id="6242c-142">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="6242c-143">Kaynak koleksiyonu disk belleğine alındığından bu adım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6242c-143">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="6242c-144">**Örnek**: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6242c-144">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6242c-145">**Proje**: Iş Ortağı Merkezi SDK örnekleri</span><span class="sxs-lookup"><span data-stu-id="6242c-145">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="6242c-146">**Sınıf**: GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="6242c-146">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a><span data-ttu-id="6242c-147">Java</span><span class="sxs-lookup"><span data-stu-id="6242c-147">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="6242c-148">Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="6242c-148">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="6242c-149">Daha sonra, kullanım kayıtlarını içeren bir **Resourcecollection** döndürmek için **IAzureUtilizationCollection. Query** işlevini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242c-149">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="6242c-150">Kaynak koleksiyonu disk belleğine alındığından, kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6242c-150">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="6242c-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6242c-151">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="6242c-152">Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="6242c-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="6242c-153">Daha sonra [**Get-Partnercustomersubscriptionkullanımı**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)' nı çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242c-153">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="6242c-154">Bu komut, belirtilen süre boyunca kullanılabilir olan tüm kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="6242c-154">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="6242c-155">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6242c-155">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6242c-156">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6242c-156">Request syntax</span></span>

| <span data-ttu-id="6242c-157">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6242c-157">Method</span></span> | <span data-ttu-id="6242c-158">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6242c-158">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="6242c-159">**Al**</span><span class="sxs-lookup"><span data-stu-id="6242c-159">**GET**</span></span> | <span data-ttu-id="6242c-160">*{BaseUrl}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-id}/gurzations/Azure? başlangıç \_ zamanı = {başlangıç zamanı} &bitiş \_ zamanı = {bitiş zamanı} &ayrıntı düzeyi = {ayrıntı düzeyi} &\_ Ayrıntıları göster = {true}</span><span class="sxs-lookup"><span data-stu-id="6242c-160">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6242c-161">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="6242c-161">URI parameters</span></span>

<span data-ttu-id="6242c-162">Kullanım kayıtlarını almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6242c-162">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="6242c-163">Ad</span><span class="sxs-lookup"><span data-stu-id="6242c-163">Name</span></span> | <span data-ttu-id="6242c-164">Tür</span><span class="sxs-lookup"><span data-stu-id="6242c-164">Type</span></span> | <span data-ttu-id="6242c-165">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6242c-165">Required</span></span> | <span data-ttu-id="6242c-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6242c-166">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="6242c-167">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="6242c-167">customer-tenant-id</span></span> | <span data-ttu-id="6242c-168">string</span><span class="sxs-lookup"><span data-stu-id="6242c-168">string</span></span> | <span data-ttu-id="6242c-169">Yes</span><span class="sxs-lookup"><span data-stu-id="6242c-169">Yes</span></span> | <span data-ttu-id="6242c-170">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="6242c-170">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="6242c-171">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="6242c-171">subscription-id</span></span> | <span data-ttu-id="6242c-172">string</span><span class="sxs-lookup"><span data-stu-id="6242c-172">string</span></span> | <span data-ttu-id="6242c-173">Yes</span><span class="sxs-lookup"><span data-stu-id="6242c-173">Yes</span></span> | <span data-ttu-id="6242c-174">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="6242c-174">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="6242c-175">start_time</span><span class="sxs-lookup"><span data-stu-id="6242c-175">start_time</span></span> | <span data-ttu-id="6242c-176">UTC Tarih-saat fark biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="6242c-176">string in UTC date-time offset format</span></span> | <span data-ttu-id="6242c-177">Yes</span><span class="sxs-lookup"><span data-stu-id="6242c-177">Yes</span></span> | <span data-ttu-id="6242c-178">Kullanım faturalandırma sisteminde ne zaman bildirileceğini temsil eden zaman aralığının başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="6242c-178">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="6242c-179">end_time</span><span class="sxs-lookup"><span data-stu-id="6242c-179">end_time</span></span> | <span data-ttu-id="6242c-180">UTC Tarih-saat fark biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="6242c-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="6242c-181">Yes</span><span class="sxs-lookup"><span data-stu-id="6242c-181">Yes</span></span> | <span data-ttu-id="6242c-182">Kullanım faturalandırma sisteminde bildirilme zamanını temsil eden zaman aralığının sonu.</span><span class="sxs-lookup"><span data-stu-id="6242c-182">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="6242c-183">boyutu</span><span class="sxs-lookup"><span data-stu-id="6242c-183">granularity</span></span> | <span data-ttu-id="6242c-184">dize</span><span class="sxs-lookup"><span data-stu-id="6242c-184">string</span></span> | <span data-ttu-id="6242c-185">No</span><span class="sxs-lookup"><span data-stu-id="6242c-185">No</span></span> | <span data-ttu-id="6242c-186">Kullanım toplamalarının ayrıntı düzeyini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6242c-186">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="6242c-187">Kullanılabilir seçenekler şunlardır: `daily` (varsayılan) ve `hourly` .</span><span class="sxs-lookup"><span data-stu-id="6242c-187">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="6242c-188">show_details</span><span class="sxs-lookup"><span data-stu-id="6242c-188">show_details</span></span> | <span data-ttu-id="6242c-189">boolean</span><span class="sxs-lookup"><span data-stu-id="6242c-189">boolean</span></span> | <span data-ttu-id="6242c-190">No</span><span class="sxs-lookup"><span data-stu-id="6242c-190">No</span></span> | <span data-ttu-id="6242c-191">Örnek düzeyinde kullanım ayrıntılarının kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6242c-191">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="6242c-192">Varsayılan değer: `true`.</span><span class="sxs-lookup"><span data-stu-id="6242c-192">The default is `true`.</span></span> |
| <span data-ttu-id="6242c-193">boyut</span><span class="sxs-lookup"><span data-stu-id="6242c-193">size</span></span> | <span data-ttu-id="6242c-194">sayı</span><span class="sxs-lookup"><span data-stu-id="6242c-194">number</span></span> | <span data-ttu-id="6242c-195">No</span><span class="sxs-lookup"><span data-stu-id="6242c-195">No</span></span> | <span data-ttu-id="6242c-196">Tek bir API çağrısıyla döndürülen toplama sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6242c-196">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="6242c-197">Varsayılan değer 1000’dir.</span><span class="sxs-lookup"><span data-stu-id="6242c-197">The default is 1000.</span></span> <span data-ttu-id="6242c-198">Maksimum değer 1000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="6242c-198">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6242c-199">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6242c-199">Request headers</span></span>

<span data-ttu-id="6242c-200">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6242c-200">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6242c-201">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6242c-201">Request body</span></span>

<span data-ttu-id="6242c-202">Yok</span><span class="sxs-lookup"><span data-stu-id="6242c-202">None</span></span>

### <a name="request-example"></a><span data-ttu-id="6242c-203">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6242c-203">Request example</span></span>

<span data-ttu-id="6242c-204">Aşağıdaki örnek istek, karşılaştırma dosyasının 7/2-8/1 dönemi için göstereceği şeydir benzer sonuçlar üretir.</span><span class="sxs-lookup"><span data-stu-id="6242c-204">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="6242c-205">Bu sonuçlar, tam olarak eşleşmeyebilir (Ayrıntılar için bkz. [Azure kullanım API 'si](#azure-utilization-api) ).</span><span class="sxs-lookup"><span data-stu-id="6242c-205">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="6242c-206">Bu örnek istek, faturalama sisteminde 7/2 (UTC) ve 8/2 (UTC) ile arasında raporlanan kullanım verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="6242c-206">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6242c-207">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6242c-207">REST response</span></span>

<span data-ttu-id="6242c-208">Başarılı olursa, bu yöntem yanıt gövdesinde [Azure kullanım kaydı](azure-utilization-record-resources.md) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="6242c-208">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="6242c-209">Azure kullanım verileri henüz bağımlı bir sistemde kullanıma yoksa, bu yöntem Retry-After bir üst bilgiyle 204 HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="6242c-209">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6242c-210">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6242c-210">Response success and error codes</span></span>

<span data-ttu-id="6242c-211">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="6242c-211">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6242c-212">HTTP durum kodunu, [hata kodu türünü](error-codes.md)ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6242c-212">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="6242c-213">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6242c-213">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
