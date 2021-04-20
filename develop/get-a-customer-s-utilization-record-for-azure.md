---
title: Müşterinin Azure kullanım kayıtlarını alma
description: Belirli bir süre boyunca bir müşterinin Azure aboneliğinin kullanım kayıtlarını almak için Azure kullanım API 'sini kullanabilirsiniz.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23c8d18462081c6d6c95c1d969f269cbb3f8754b
ms.sourcegitcommit: abefe11421edc421491f14b257b2408b4f29b669
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/20/2021
ms.locfileid: "107745601"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="903e5-103">Müşterinin Azure kullanım kayıtlarını alma</span><span class="sxs-lookup"><span data-stu-id="903e5-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="903e5-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="903e5-104">**Applies to:**</span></span>

- <span data-ttu-id="903e5-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="903e5-105">Partner Center</span></span>
- <span data-ttu-id="903e5-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="903e5-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="903e5-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="903e5-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="903e5-108">Azure kullanım API 'sini kullanarak belirli bir süre için müşterinin Azure aboneliğinin kullanım kayıtlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="903e5-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="903e5-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="903e5-109">Prerequisites</span></span>

- <span data-ttu-id="903e5-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="903e5-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="903e5-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="903e5-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="903e5-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="903e5-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="903e5-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="903e5-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="903e5-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="903e5-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="903e5-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="903e5-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="903e5-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="903e5-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="903e5-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="903e5-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="903e5-118">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="903e5-118">A subscription identifier.</span></span>

<span data-ttu-id="903e5-119">Bu API, rastgele bir zaman aralığı için günlük ve saatlik derecelendirilmemiş tüketim döndürür.</span><span class="sxs-lookup"><span data-stu-id="903e5-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="903e5-120">Ancak, *Bu API Azure planları için desteklenmez*.</span><span class="sxs-lookup"><span data-stu-id="903e5-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="903e5-121">Bir Azure planınız varsa, [Fatura faturalandırılmamış tüketim satırı öğelerini alma](get-invoice-unbilled-consumption-lineitems.md) ve [Fatura için faturalandırılan tüketim satırı öğelerini](get-invoice-billed-consumption-lineitems.md) alma makalelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="903e5-121">If you have an Azure plan, see the articles [Get invoice un-billed consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="903e5-122">Bu makalelerde, kaynak başına ölçüm başına her gün bir derecelendirmeden derecelendirilen tüketimin nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="903e5-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="903e5-123">Bu hız tüketimi, Azure kullanım API 'SI tarafından belirtilen günlük gren verilere eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="903e5-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="903e5-124">Fatura tanımlayıcısını, faturalandırılan kullanım verilerini almak için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="903e5-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="903e5-125">Veya, faturalandırılmamış kullanım tahminleri almak için geçerli ve önceki dönemleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="903e5-125">Or, you can use current and previous periods to get un-billed usage estimates.</span></span> <span data-ttu-id="903e5-126">*Saatlik gren veri ve rastgele tarih aralığı filtreleri şu anda Azure plan aboneliği kaynakları için desteklenmiyor*.</span><span class="sxs-lookup"><span data-stu-id="903e5-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="903e5-127">Azure kullanım API 'SI</span><span class="sxs-lookup"><span data-stu-id="903e5-127">Azure utilization API</span></span>

<span data-ttu-id="903e5-128">Bu Azure kullanım API 'SI, kullanımın faturalandırma sisteminde ne zaman raporlanacağı temsil eden bir döneme ait kullanım kayıtlarına erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="903e5-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="903e5-129">Bu, mutabakat dosyası oluşturmak ve hesaplamak için kullanılan kullanım verilerine erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="903e5-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="903e5-130">Ancak fatura sistem mutabakatı dosya mantığı hakkında bilgi sahibi değildir.</span><span class="sxs-lookup"><span data-stu-id="903e5-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="903e5-131">Aynı zaman dilimi için bu API 'den alınan sonuçla eşleşen dosya Özeti sonuçlarının mutabakatını beklememelisiniz.</span><span class="sxs-lookup"><span data-stu-id="903e5-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="903e5-132">Örneğin, faturalandırma sistemi aynı kullanım verilerini alır ve bir mutabakat dosyasında nelerin hesaba katılmaz belirlemek için değer kuralları uygular.</span><span class="sxs-lookup"><span data-stu-id="903e5-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="903e5-133">Bir faturalandırma dönemi kapandığında, fatura döneminin sona ereceği günün sonuna kadar tüm kullanımlar mutabakat dosyasına dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="903e5-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="903e5-134">Fatura dönemi bittikten sonra 24 saat içinde raporlanan ödeme dönemi içinde herhangi bir geç kullanım, bir sonraki mutabakat dosyasında hesaba katılmaz.</span><span class="sxs-lookup"><span data-stu-id="903e5-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="903e5-135">Ortağın faturalandırılma şekli için bkz. [Azure aboneliği için tüketim verilerini alma](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="903e5-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="903e5-136">Bu REST API disk belleğine alınmış.</span><span class="sxs-lookup"><span data-stu-id="903e5-136">This REST API is paged.</span></span> <span data-ttu-id="903e5-137">Yanıt yükü tek bir sayfadan fazlaysa, kullanım kayıtlarının sonraki sayfasını almak için sonraki bağlantıyı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="903e5-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

### <a name="scenario--partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a><span data-ttu-id="903e5-138">Senaryo: Iş ortağı A, Azure eski aboneliğinin (145P) faturalama sahipliğini B ortağına aktardı</span><span class="sxs-lookup"><span data-stu-id="903e5-138">Scenario : Partner A has transferred billing ownership of Azure Legacy Subscription (145P) to Partner B</span></span>

<span data-ttu-id="903e5-139">Bir iş ortağı, Azure eski aboneliğinin faturalandırma sahipliğini başka bir ortağa aktarıyorsa yeni iş ortağı aktarılan abonelik için kullanım API 'sini çağırdığında, Azure Yetkilendirme KIMLIĞI yerine ticari abonelik KIMLIĞI (Iş Ortağı Merkezi hesabında gösterilir) kullanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="903e5-139">If a partner transfers billing ownership of an Azure legacy subscription to another partner, when new the new partner calls Utilization API for transferred subscription they have to use Commerce Subscription ID (which shows up in their Partner Center account) rather than the Azure Entitlement ID.</span></span> <span data-ttu-id="903e5-140">Azure Yetkilendirme KIMLIĞI, Iş ortağı B yalnızca müşterinin Azure portal (AOBO) adına yönetici olduklarında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="903e5-140">Azure Entitlement ID appears for Partner B only when they are Admin on behalf of (AOBO) to Customer's Azure portal.</span></span> 

<span data-ttu-id="903e5-141">Aktarılan abonelik için kullanım API 'sini başarılı bir şekilde çağırmak için, yeni iş ortağının ticaret abonelik KIMLIĞINI kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="903e5-141">To successfully call the Utilization API for the transferred subscription, the new partner needs to use the Commerce Subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="903e5-142">C\#</span><span class="sxs-lookup"><span data-stu-id="903e5-142">C\#</span></span>

<span data-ttu-id="903e5-143">Azure kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="903e5-143">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="903e5-144">Müşteri KIMLIĞINI ve abonelik KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="903e5-144">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="903e5-145">Kullanım kayıtlarını içeren bir [**Resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) döndürmek için [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="903e5-145">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="903e5-146">Kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı elde edin.</span><span class="sxs-lookup"><span data-stu-id="903e5-146">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="903e5-147">Kaynak koleksiyonu disk belleğine alındığından bu adım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="903e5-147">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="903e5-148">**Örnek**: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="903e5-148">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="903e5-149">**Proje**: Iş Ortağı Merkezi SDK örnekleri</span><span class="sxs-lookup"><span data-stu-id="903e5-149">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="903e5-150">**Sınıf**: GetAzureSubscriptionUtilization. cs</span><span class="sxs-lookup"><span data-stu-id="903e5-150">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

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

## <a name="java"></a><span data-ttu-id="903e5-151">Java</span><span class="sxs-lookup"><span data-stu-id="903e5-151">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="903e5-152">Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="903e5-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="903e5-153">Daha sonra, kullanım kayıtlarını içeren bir **Resourcecollection** döndürmek için **IAzureUtilizationCollection. Query** işlevini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="903e5-153">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="903e5-154">Kaynak koleksiyonu disk belleğine alındığından, kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="903e5-154">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="903e5-155">PowerShell</span><span class="sxs-lookup"><span data-stu-id="903e5-155">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="903e5-156">Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="903e5-156">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="903e5-157">Daha sonra [**Get-Partnercustomersubscriptionkullanımı**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)' nı çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="903e5-157">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="903e5-158">Bu komut, belirtilen süre boyunca kullanılabilir olan tüm kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="903e5-158">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="903e5-159">REST isteği</span><span class="sxs-lookup"><span data-stu-id="903e5-159">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="903e5-160">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="903e5-160">Request syntax</span></span>

| <span data-ttu-id="903e5-161">Yöntem</span><span class="sxs-lookup"><span data-stu-id="903e5-161">Method</span></span> | <span data-ttu-id="903e5-162">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="903e5-162">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="903e5-163">**Al**</span><span class="sxs-lookup"><span data-stu-id="903e5-163">**GET**</span></span> | <span data-ttu-id="903e5-164">*{BaseUrl}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-id}/gurzations/Azure? başlangıç \_ zamanı = {başlangıç zamanı} &bitiş \_ zamanı = {bitiş zamanı} &ayrıntı düzeyi = {ayrıntı düzeyi} &\_ Ayrıntıları göster = {true}</span><span class="sxs-lookup"><span data-stu-id="903e5-164">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="903e5-165">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="903e5-165">URI parameters</span></span>

<span data-ttu-id="903e5-166">Kullanım kayıtlarını almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="903e5-166">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="903e5-167">Ad</span><span class="sxs-lookup"><span data-stu-id="903e5-167">Name</span></span> | <span data-ttu-id="903e5-168">Tür</span><span class="sxs-lookup"><span data-stu-id="903e5-168">Type</span></span> | <span data-ttu-id="903e5-169">Gerekli</span><span class="sxs-lookup"><span data-stu-id="903e5-169">Required</span></span> | <span data-ttu-id="903e5-170">Açıklama</span><span class="sxs-lookup"><span data-stu-id="903e5-170">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="903e5-171">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="903e5-171">customer-tenant-id</span></span> | <span data-ttu-id="903e5-172">string</span><span class="sxs-lookup"><span data-stu-id="903e5-172">string</span></span> | <span data-ttu-id="903e5-173">Yes</span><span class="sxs-lookup"><span data-stu-id="903e5-173">Yes</span></span> | <span data-ttu-id="903e5-174">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="903e5-174">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="903e5-175">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="903e5-175">subscription-id</span></span> | <span data-ttu-id="903e5-176">string</span><span class="sxs-lookup"><span data-stu-id="903e5-176">string</span></span> | <span data-ttu-id="903e5-177">Yes</span><span class="sxs-lookup"><span data-stu-id="903e5-177">Yes</span></span> | <span data-ttu-id="903e5-178">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="903e5-178">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="903e5-179">start_time</span><span class="sxs-lookup"><span data-stu-id="903e5-179">start_time</span></span> | <span data-ttu-id="903e5-180">UTC Tarih-saat fark biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="903e5-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="903e5-181">Yes</span><span class="sxs-lookup"><span data-stu-id="903e5-181">Yes</span></span> | <span data-ttu-id="903e5-182">Kullanım faturalandırma sisteminde ne zaman bildirileceğini temsil eden zaman aralığının başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="903e5-182">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="903e5-183">end_time</span><span class="sxs-lookup"><span data-stu-id="903e5-183">end_time</span></span> | <span data-ttu-id="903e5-184">UTC Tarih-saat fark biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="903e5-184">string in UTC date-time offset format</span></span> | <span data-ttu-id="903e5-185">Yes</span><span class="sxs-lookup"><span data-stu-id="903e5-185">Yes</span></span> | <span data-ttu-id="903e5-186">Kullanım faturalandırma sisteminde bildirilme zamanını temsil eden zaman aralığının sonu.</span><span class="sxs-lookup"><span data-stu-id="903e5-186">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="903e5-187">boyutu</span><span class="sxs-lookup"><span data-stu-id="903e5-187">granularity</span></span> | <span data-ttu-id="903e5-188">dize</span><span class="sxs-lookup"><span data-stu-id="903e5-188">string</span></span> | <span data-ttu-id="903e5-189">No</span><span class="sxs-lookup"><span data-stu-id="903e5-189">No</span></span> | <span data-ttu-id="903e5-190">Kullanım toplamalarının ayrıntı düzeyini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="903e5-190">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="903e5-191">Kullanılabilir seçenekler şunlardır: `daily` (varsayılan) ve `hourly` .</span><span class="sxs-lookup"><span data-stu-id="903e5-191">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="903e5-192">show_details</span><span class="sxs-lookup"><span data-stu-id="903e5-192">show_details</span></span> | <span data-ttu-id="903e5-193">boolean</span><span class="sxs-lookup"><span data-stu-id="903e5-193">boolean</span></span> | <span data-ttu-id="903e5-194">No</span><span class="sxs-lookup"><span data-stu-id="903e5-194">No</span></span> | <span data-ttu-id="903e5-195">Örnek düzeyinde kullanım ayrıntılarının kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="903e5-195">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="903e5-196">Varsayılan değer: `true`.</span><span class="sxs-lookup"><span data-stu-id="903e5-196">The default is `true`.</span></span> |
| <span data-ttu-id="903e5-197">boyut</span><span class="sxs-lookup"><span data-stu-id="903e5-197">size</span></span> | <span data-ttu-id="903e5-198">sayı</span><span class="sxs-lookup"><span data-stu-id="903e5-198">number</span></span> | <span data-ttu-id="903e5-199">No</span><span class="sxs-lookup"><span data-stu-id="903e5-199">No</span></span> | <span data-ttu-id="903e5-200">Tek bir API çağrısıyla döndürülen toplama sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="903e5-200">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="903e5-201">Varsayılan değer 1000’dir.</span><span class="sxs-lookup"><span data-stu-id="903e5-201">The default is 1000.</span></span> <span data-ttu-id="903e5-202">Maksimum değer 1000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="903e5-202">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="903e5-203">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="903e5-203">Request headers</span></span>

<span data-ttu-id="903e5-204">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="903e5-204">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="903e5-205">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="903e5-205">Request body</span></span>

<span data-ttu-id="903e5-206">Yok</span><span class="sxs-lookup"><span data-stu-id="903e5-206">None</span></span>

### <a name="request-example"></a><span data-ttu-id="903e5-207">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="903e5-207">Request example</span></span>

<span data-ttu-id="903e5-208">Aşağıdaki örnek istek, karşılaştırma dosyasının 7/2-8/1 dönemi için göstereceği şeydir benzer sonuçlar üretir.</span><span class="sxs-lookup"><span data-stu-id="903e5-208">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="903e5-209">Bu sonuçlar, tam olarak eşleşmeyebilir (Ayrıntılar için bkz. [Azure kullanım API 'si](#azure-utilization-api) ).</span><span class="sxs-lookup"><span data-stu-id="903e5-209">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="903e5-210">Bu örnek istek, faturalama sisteminde 7/2 (UTC) ve 8/2 (UTC) ile arasında raporlanan kullanım verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="903e5-210">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="903e5-211">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="903e5-211">REST response</span></span>

<span data-ttu-id="903e5-212">Başarılı olursa, bu yöntem yanıt gövdesinde [Azure kullanım kaydı](azure-utilization-record-resources.md) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="903e5-212">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="903e5-213">Azure kullanım verileri henüz bağımlı bir sistemde kullanıma yoksa, bu yöntem Retry-After bir üst bilgiyle 204 HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="903e5-213">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="903e5-214">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="903e5-214">Response success and error codes</span></span>

<span data-ttu-id="903e5-215">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="903e5-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="903e5-216">HTTP durum kodunu, [hata kodu türünü](error-codes.md)ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="903e5-216">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="903e5-217">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="903e5-217">Response example</span></span>

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
