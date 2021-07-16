---
title: Fatura faturalanmamış ticari tüketim satırı öğelerini Al
description: Iş Ortağı Merkezi API 'Lerini kullanarak belirli bir faturaya ait faturalandırılmamış ticari tüketim çizgisi öğe ayrıntılarının bir koleksiyonunu alabilirsiniz.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7c74bedfd6412fc5954ed2ddc1388936e418fa3
ms.sourcegitcommit: 722992eea6f8ea366dc088e5dd1ee63c17d56f61
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/15/2021
ms.locfileid: "114224777"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a>Fatura faturalanmamış ticari tüketim satırı öğelerini Al

Faturalandırılmamış ticari tüketim satırı öğe ayrıntılarının koleksiyonunu alma.

Ayrıca, faturalandırılmamış ticari tüketim çizgisi öğelerinin (açık kullanım satırı öğeleri olarak da bilinir) programlı bir şekilde ayrıntılarını almak için aşağıdaki yöntemleri kullanabilirsiniz.

>[!NOTE]
>Günlük olarak derecelendirilen kullanımlar, Iş Ortağı Merkezi 'nde veya API aracılığıyla erişilecek 24 saat sürer.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

Belirtilen faturaya ait satır öğelerini almak için:

1. Belirtilen faturaya yönelik işlemleri faturalamak için bir arabirim almak üzere [**Byıd**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) yöntemini çağırın.

2. Fatura nesnesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.

**Fatura nesnesi** belirtilen faturaya ait tüm bilgileri içerir. **Sağlayıcı** , faturalandırılmamış ayrıntı bilgisinin kaynağını tanımlar (örneğin, **Onetime**). **Invoineıtemtype** türü belirtir (örneğin, **Usagelineitem**).

Aşağıdaki örnek kod, **ınvogıtems** koleksiyonunu işlemek için bir **foreach** döngüsü kullanır. Her bir **Faturaöğeside** her bir faturaya ait ayrı bir satır öğesi koleksiyonu alınır.

Bir **InvoiceDetail** örneğine karşılık gelen satır öğelerinin bir koleksiyonunu almak için:

1. Örneğe ait **Billingprovider** ve **ınvoineıtemtype** 'ı [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metoduna geçirin.

2. İlişkili satır öğelerini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.
3. Aşağıdaki örnekte gösterildiği gibi koleksiyonun çapraz geçişini yapmak için bir Numaralandırıcı oluşturun.

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

Benzer bir örnek için bkz.:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Project: **iş ortağı merkezi SDK örnekleri**
- Sınıf: **GetUnBilledConsumptionReconLineItemsPaging. cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

Kullanım durumunuza bağlı olarak REST isteğiniz için aşağıdaki sözdizimleri kullanılabilir. Daha fazla bilgi için her bir sözdizimi için açıklamalara bakın.

| Yöntem  | İstek URI'si                                                                                                                                                                                              | Sözdizimi kullanım durumunun açıklaması                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturaın/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &period = {PERIOD} http/1.1                       | Verilen faturaya ait her satır öğesinin tam listesini döndürmek için bu sözdizimini kullanın.                                                    |
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &süre = {period} &boyut = {SIZE} http/1.1           | Büyük faturalar için bu sözdizimini kullanın. Satır öğelerinin disk belleğine alınmış bir listesini döndürmek için bu söz dizimini belirtilen boyut ve 0 tabanlı bir uzaklığa göre kullanın. |
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &period = {period} &boyut = {size} &Seekoperation = ileri | Kullanılarak mutabakat satır öğelerinin sonraki sayfasını almak için bu sözdizimini kullanın `seekOperation = "Next"` .                                  |

#### <a name="uri-parameters"></a>URI parametreleri

İsteği oluştururken aşağıdaki URI ve sorgu parametrelerini kullanın.

| Ad                   | Tür   | Gerekli | Açıklama                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sağlayıcısını               | string | Evet      | Sağlayıcı: "**Onetime**".                                                                                                                                                                                                               |
| fatura-satır-öğe türü | string | Evet      | Fatura ayrıntısı türü: "**Usagelineıtems**", "**usagelineıtems**".                                                                                                                                                                    |
| currencyCode           | string | Evet      | Faturalandırılmamış satır öğelerinin para birimi kodu.                                                                                                                                                                                             |
| dönem                 | string | Evet      | Faturalandırılmamış keşfi için süre (örneğin: **geçerli**, **önceki**). Fatura döngüsünün faturalandırılmamış kullanım verilerini (01/01/2020 – 01/31/2020), Ocak ayında **"geçerli,"** diğer **"önceki** " olarak seçin. |
| boyut                   | sayı | Hayır       | Döndürülecek en fazla öğe sayısı. Varsayılan boyut 2000 ' dir.                                                                                                                                                                           |
| seekOperation          | dize | No       | `seekOperation=Next`Mutabakat satır öğelerinin sonraki sayfasını almak için ayarlayın.                                                                                                                                                                |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt satır öğesi ayrıntıları koleksiyonunu içerir.

*Satır **öğesi için**, **satın alma** değeri **Yeni** ile eşlenir ve değer **iadesi** **iptal** edilecek şekilde eşlenir.*

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

## <a name="request-response-examples"></a>İstek-yanıt örnekleri

### <a name="request-response-example-1"></a>İstek-yanıt örneği 1

Aşağıdaki ayrıntılar Bu örnek için geçerlidir:

- **Sağlayıcı**: **Onetime**
- **Faturaışgıtemtype**: **usagelineıtems**
- **Dönem**: **önceki**

#### <a name="request-example-1"></a>İstek örneği 1

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a>Yanıt örneği 1

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 0,
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemTypce": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a>İstek-yanıt örneği 2

Aşağıdaki ayrıntılar Bu örnek için geçerlidir:

- **Sağlayıcı**: **Onetime**
- **Faturaışgıtemtype**: **usagelineıtems**
- **Dönem**: **önceki**
- **Seekoperation**: **İleri**

#### <a name="request-example-2"></a>İstek örneği 2

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a>Yanıt örneği 2

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
