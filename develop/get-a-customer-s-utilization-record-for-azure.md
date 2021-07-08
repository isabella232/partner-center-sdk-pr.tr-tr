---
title: Müşterinin Azure kullanım kayıtlarını alma
description: Belirli bir süre boyunca bir müşterinin Azure aboneliğinin kullanım kayıtlarını almak için Azure kullanım API 'sini kullanabilirsiniz.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7024bc65976a9b43a62b66c529d271519181ab23
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874933"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="c0d4c-103">Müşterinin Azure kullanım kayıtlarını alma</span><span class="sxs-lookup"><span data-stu-id="c0d4c-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="c0d4c-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c0d4c-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c0d4c-105">Azure kullanım API 'sini kullanarak belirli bir süre için müşterinin Azure aboneliğinin kullanım kayıtlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-105">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0d4c-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c0d4c-106">Prerequisites</span></span>

- <span data-ttu-id="c0d4c-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c0d4c-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-108">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="c0d4c-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c0d4c-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c0d4c-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c0d4c-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c0d4c-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c0d4c-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c0d4c-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="c0d4c-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c0d4c-115">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-115">A subscription identifier.</span></span>

<span data-ttu-id="c0d4c-116">Bu API, rastgele bir zaman aralığı için günlük ve saatlik derecelendirilmemiş tüketim döndürür.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-116">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="c0d4c-117">Ancak, *Bu API Azure planları için desteklenmez*.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-117">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="c0d4c-118">Bir Azure planınız varsa, [Fatura faturalandırılmamış tüketim satırı öğelerini Al](get-invoice-unbilled-consumption-lineitems.md) ve [Fatura için faturalandırılan tüketim satırı öğelerini](get-invoice-billed-consumption-lineitems.md) al makalelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-118">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="c0d4c-119">Bu makalelerde, kaynak başına ölçüm başına her gün bir derecelendirmeden derecelendirilen tüketimin nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-119">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="c0d4c-120">Bu hız tüketimi, Azure kullanım API 'SI tarafından belirtilen günlük gren verilere eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-120">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="c0d4c-121">Fatura tanımlayıcısını, faturalandırılan kullanım verilerini almak için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-121">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="c0d4c-122">Ya da, faturalandırılmamış kullanım tahminleri almak için geçerli ve önceki dönemleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-122">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="c0d4c-123">*Saatlik gren veri ve rastgele tarih aralığı filtreleri şu anda Azure plan aboneliği kaynakları için desteklenmiyor*.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-123">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="c0d4c-124">Azure kullanım API 'SI</span><span class="sxs-lookup"><span data-stu-id="c0d4c-124">Azure utilization API</span></span>

<span data-ttu-id="c0d4c-125">Bu Azure kullanım API 'SI, kullanımın faturalandırma sisteminde ne zaman raporlanacağı temsil eden bir döneme ait kullanım kayıtlarına erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-125">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="c0d4c-126">Bu, mutabakat dosyası oluşturmak ve hesaplamak için kullanılan kullanım verilerine erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-126">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="c0d4c-127">Ancak fatura sistem mutabakatı dosya mantığı hakkında bilgi sahibi değildir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-127">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="c0d4c-128">Aynı zaman dilimi için bu API 'den alınan sonuçla eşleşen dosya Özeti sonuçlarının mutabakatını beklememelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-128">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="c0d4c-129">Örneğin, faturalandırma sistemi aynı kullanım verilerini alır ve bir mutabakat dosyasında nelerin hesaba katılmaz belirlemek için değer kuralları uygular.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-129">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="c0d4c-130">Bir faturalandırma dönemi kapandığında, fatura döneminin sona ereceği günün sonuna kadar tüm kullanımlar mutabakat dosyasına dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-130">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="c0d4c-131">Fatura dönemi bittikten sonra 24 saat içinde raporlanan ödeme dönemi içinde herhangi bir geç kullanım, bir sonraki mutabakat dosyasında hesaba katılmaz.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-131">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="c0d4c-132">Ortağın faturalandırılma şekli için bkz. [Azure aboneliği için tüketim verilerini alma](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="c0d4c-132">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="c0d4c-133">Bu REST API disk belleğine alınmış.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-133">This REST API is paged.</span></span> <span data-ttu-id="c0d4c-134">Yanıt yükü tek bir sayfadan fazlaysa, kullanım kayıtlarının sonraki sayfasını almak için sonraki bağlantıyı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-134">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

### <a name="scenario-partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a><span data-ttu-id="c0d4c-135">Senaryo: Iş ortağı A, Azure eski aboneliğinin (145P) faturalama sahipliğini B ortağına aktardı</span><span class="sxs-lookup"><span data-stu-id="c0d4c-135">Scenario: Partner A has transferred billing ownership of Azure Legacy Subscription (145P) to Partner B</span></span>

<span data-ttu-id="c0d4c-136">Bir iş ortağı, Azure eski aboneliğinin faturalandırma sahipliğini başka bir ortağa aktarıyorsa yeni iş ortağı aktarılan abonelik için kullanım API 'sini çağırdığında, Azure Yetkilendirme KIMLIĞI yerine ticari abonelik KIMLIĞI (Iş Ortağı Merkezi hesabında gösterilir) kullanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-136">If a partner transfers billing ownership of an Azure legacy subscription to another partner, when new the new partner calls Utilization API for transferred subscription they have to use Commerce Subscription ID (which shows up in their Partner Center account) rather than the Azure Entitlement ID.</span></span> <span data-ttu-id="c0d4c-137">Azure Yetkilendirme KIMLIĞI, Iş ortağı B yalnızca müşterinin Azure portal (AOBO) adına yönetici olduklarında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-137">Azure Entitlement ID appears for Partner B only when they are Admin on behalf of (AOBO) to Customer's Azure portal.</span></span> 

<span data-ttu-id="c0d4c-138">Aktarılan abonelik için kullanım API 'sini başarılı bir şekilde çağırmak için, yeni iş ortağının ticaret abonelik KIMLIĞINI kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-138">To successfully call the Utilization API for the transferred subscription, the new partner needs to use the Commerce Subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="c0d4c-139">C\#</span><span class="sxs-lookup"><span data-stu-id="c0d4c-139">C\#</span></span>

<span data-ttu-id="c0d4c-140">Azure kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="c0d4c-140">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="c0d4c-141">Müşteri KIMLIĞINI ve abonelik KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-141">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="c0d4c-142">Kullanım kayıtlarını içeren bir [**Resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) döndürmek için [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-142">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="c0d4c-143">Kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı elde edin.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-143">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="c0d4c-144">Kaynak koleksiyonu disk belleğine alındığından bu adım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-144">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="c0d4c-145">**Örnek**: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="c0d4c-145">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="c0d4c-146">**Project**: iş ortağı merkezi SDK örnekleri</span><span class="sxs-lookup"><span data-stu-id="c0d4c-146">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="c0d4c-147">**Sınıf**: GetAzureSubscriptionUtilization. cs</span><span class="sxs-lookup"><span data-stu-id="c0d4c-147">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

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

## <a name="java"></a><span data-ttu-id="c0d4c-148">Java</span><span class="sxs-lookup"><span data-stu-id="c0d4c-148">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="c0d4c-149">Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-149">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="c0d4c-150">Daha sonra, kullanım kayıtlarını içeren bir **Resourcecollection** döndürmek için **IAzureUtilizationCollection. Query** işlevini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-150">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="c0d4c-151">Kaynak koleksiyonu disk belleğine alındığından, kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-151">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="c0d4c-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0d4c-152">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="c0d4c-153">Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-153">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="c0d4c-154">Daha sonra [**Get-Partnercustomersubscriptionkullanımı**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)' nı çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-154">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="c0d4c-155">Bu komut, belirtilen süre boyunca kullanılabilir olan tüm kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-155">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="c0d4c-156">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c0d4c-156">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c0d4c-157">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c0d4c-157">Request syntax</span></span>

| <span data-ttu-id="c0d4c-158">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c0d4c-158">Method</span></span> | <span data-ttu-id="c0d4c-159">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c0d4c-159">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="c0d4c-160">**Al**</span><span class="sxs-lookup"><span data-stu-id="c0d4c-160">**GET**</span></span> | <span data-ttu-id="c0d4c-161">*{BaseUrl}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-id}/gurzations/Azure? başlangıç \_ zamanı = {başlangıç zamanı} &bitiş \_ zamanı = {bitiş zamanı} &ayrıntı düzeyi = {ayrıntı düzeyi} &\_ Ayrıntıları göster = {true}</span><span class="sxs-lookup"><span data-stu-id="c0d4c-161">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="c0d4c-162">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="c0d4c-162">URI parameters</span></span>

<span data-ttu-id="c0d4c-163">Kullanım kayıtlarını almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-163">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="c0d4c-164">Ad</span><span class="sxs-lookup"><span data-stu-id="c0d4c-164">Name</span></span> | <span data-ttu-id="c0d4c-165">Tür</span><span class="sxs-lookup"><span data-stu-id="c0d4c-165">Type</span></span> | <span data-ttu-id="c0d4c-166">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c0d4c-166">Required</span></span> | <span data-ttu-id="c0d4c-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c0d4c-167">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="c0d4c-168">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="c0d4c-168">customer-tenant-id</span></span> | <span data-ttu-id="c0d4c-169">string</span><span class="sxs-lookup"><span data-stu-id="c0d4c-169">string</span></span> | <span data-ttu-id="c0d4c-170">Yes</span><span class="sxs-lookup"><span data-stu-id="c0d4c-170">Yes</span></span> | <span data-ttu-id="c0d4c-171">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-171">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="c0d4c-172">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="c0d4c-172">subscription-id</span></span> | <span data-ttu-id="c0d4c-173">string</span><span class="sxs-lookup"><span data-stu-id="c0d4c-173">string</span></span> | <span data-ttu-id="c0d4c-174">Yes</span><span class="sxs-lookup"><span data-stu-id="c0d4c-174">Yes</span></span> | <span data-ttu-id="c0d4c-175">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="c0d4c-176">start_time</span><span class="sxs-lookup"><span data-stu-id="c0d4c-176">start_time</span></span> | <span data-ttu-id="c0d4c-177">UTC Tarih-saat fark biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="c0d4c-177">string in UTC date-time offset format</span></span> | <span data-ttu-id="c0d4c-178">Yes</span><span class="sxs-lookup"><span data-stu-id="c0d4c-178">Yes</span></span> | <span data-ttu-id="c0d4c-179">Kullanım faturalandırma sisteminde ne zaman bildirileceğini temsil eden zaman aralığının başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-179">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="c0d4c-180">end_time</span><span class="sxs-lookup"><span data-stu-id="c0d4c-180">end_time</span></span> | <span data-ttu-id="c0d4c-181">UTC Tarih-saat fark biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="c0d4c-181">string in UTC date-time offset format</span></span> | <span data-ttu-id="c0d4c-182">Yes</span><span class="sxs-lookup"><span data-stu-id="c0d4c-182">Yes</span></span> | <span data-ttu-id="c0d4c-183">Kullanım faturalandırma sisteminde bildirilme zamanını temsil eden zaman aralığının sonu.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-183">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="c0d4c-184">boyutu</span><span class="sxs-lookup"><span data-stu-id="c0d4c-184">granularity</span></span> | <span data-ttu-id="c0d4c-185">dize</span><span class="sxs-lookup"><span data-stu-id="c0d4c-185">string</span></span> | <span data-ttu-id="c0d4c-186">No</span><span class="sxs-lookup"><span data-stu-id="c0d4c-186">No</span></span> | <span data-ttu-id="c0d4c-187">Kullanım toplamalarının ayrıntı düzeyini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-187">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="c0d4c-188">Kullanılabilir seçenekler şunlardır: `daily` (varsayılan) ve `hourly` .</span><span class="sxs-lookup"><span data-stu-id="c0d4c-188">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="c0d4c-189">show_details</span><span class="sxs-lookup"><span data-stu-id="c0d4c-189">show_details</span></span> | <span data-ttu-id="c0d4c-190">boolean</span><span class="sxs-lookup"><span data-stu-id="c0d4c-190">boolean</span></span> | <span data-ttu-id="c0d4c-191">Hayır</span><span class="sxs-lookup"><span data-stu-id="c0d4c-191">No</span></span> | <span data-ttu-id="c0d4c-192">Örnek düzeyinde kullanım ayrıntılarının kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-192">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="c0d4c-193">Varsayılan değer: `true`.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-193">The default is `true`.</span></span> |
| <span data-ttu-id="c0d4c-194">boyut</span><span class="sxs-lookup"><span data-stu-id="c0d4c-194">size</span></span> | <span data-ttu-id="c0d4c-195">sayı</span><span class="sxs-lookup"><span data-stu-id="c0d4c-195">number</span></span> | <span data-ttu-id="c0d4c-196">Hayır</span><span class="sxs-lookup"><span data-stu-id="c0d4c-196">No</span></span> | <span data-ttu-id="c0d4c-197">Tek bir API çağrısıyla döndürülen toplama sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-197">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="c0d4c-198">Varsayılan değer 1000’dir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-198">The default is 1000.</span></span> <span data-ttu-id="c0d4c-199">Maksimum değer 1000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-199">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c0d4c-200">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c0d4c-200">Request headers</span></span>

<span data-ttu-id="c0d4c-201">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c0d4c-201">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c0d4c-202">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c0d4c-202">Request body</span></span>

<span data-ttu-id="c0d4c-203">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="c0d4c-203">None</span></span>

### <a name="request-example"></a><span data-ttu-id="c0d4c-204">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c0d4c-204">Request example</span></span>

<span data-ttu-id="c0d4c-205">Aşağıdaki örnek istek, karşılaştırma dosyasının 7/2-8/1 dönemi için göstereceği şeydir benzer sonuçlar üretir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-205">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="c0d4c-206">Bu sonuçlar, tam olarak eşleşmeyebilir (Ayrıntılar için bkz. [Azure kullanım API 'si](#azure-utilization-api) ).</span><span class="sxs-lookup"><span data-stu-id="c0d4c-206">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="c0d4c-207">Bu örnek istek, faturalama sisteminde 7/2 (UTC) ve 8/2 (UTC) ile arasında raporlanan kullanım verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-207">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="c0d4c-208">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c0d4c-208">REST response</span></span>

<span data-ttu-id="c0d4c-209">Başarılı olursa, bu yöntem yanıt gövdesinde [Azure kullanım kaydı](azure-utilization-record-resources.md) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-209">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="c0d4c-210">Azure kullanım verileri henüz bağımlı bir sistemde kullanıma yoksa, bu yöntem Retry-After bir üst bilgiyle 204 HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-210">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c0d4c-211">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c0d4c-211">Response success and error codes</span></span>

<span data-ttu-id="c0d4c-212">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-212">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c0d4c-213">HTTP durum kodunu, [hata kodu türünü](error-codes.md)ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0d4c-213">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="c0d4c-214">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c0d4c-214">Response example</span></span>

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
