---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Insikter om Adobe Experience Platform-observationer
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---


# Översikt över Adobe Experience Platform Insights

Insikter om observerbarhet är ett RESTful-API som gör att du kan visa viktiga mätvärden för observerbarhet i Adobe Experience Platform. Dessa mätvärden ger insikter om [!DNL Platform] användningsstatistik, hälsokontroller av [!DNL Platform] tjänster, historiska trender och resultatindikatorer för olika [!DNL Platform] funktioner.

I det här dokumentet visas ett exempel på hur du anropar API:t för Insights. En fullständig lista över observationsslutpunkter finns i API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)observabilitetsinsikter.

## Komma igång

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../sandboxes/home.md).

* x-sandbox-name: `{SANDBOX_NAME}`

## Hämta mätvärden för observerbarhet

Du kan hämta mätvärden för observerbarhet genom att göra en GET-begäran till `/metrics` slutpunkten i API:t för observabilitetsinsikter.

**API-format**

När du använder `/metrics` slutpunkten måste minst en parameter för metrisk begäran anges. Andra frågeparametrar är valfria för filtrering av resultat.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{METRIC}` | Det mätvärde som du vill visa. När du kombinerar flera mätvärden i ett enda anrop måste du använda ett et-tecken (`&`) för att separera enskilda mätvärden. Exempel, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | Identifieraren för en viss [!DNL Platform] resurs vars mätvärden du vill visa. Detta ID kan vara valfritt, obligatoriskt eller inte tillämpligt beroende på vilka mätvärden som används. En lista över tillgängliga mätvärden, samt vilka ID:n som stöds (både obligatoriska och valfria) för varje mätvärde finns i referensdokumentet om [tillgängliga mätvärden](metrics.md). |
| `{DATE_RANGE}` | Datumintervallet för de mätvärden som du vill visa, i ISO 8601-format (till exempel `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med objekt, där var och en innehåller en tidsstämpel inom det angivna `dateRange` och motsvarande värden för de mått som anges i sökvägen för begäran. Om en `id` resurs är inkluderad [!DNL Platform] i den begärda sökvägen gäller resultaten endast den aktuella resursen. Om `id` utelämnas gäller resultatet alla tillämpliga resurser i IMS-organisationen.

```json
{
    "id": "5cf8ab4ec48aba145214abeb",
    "imsOrgId": "{IMS_ORG}",
    "timeseries": {
        "granularity": "MONTH",
        "items": [
            {
                "timestamp": "2019-06-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1125,
                    "timeseries.ingestion.dataset.size": 32320
                }
            },
            {
                "timestamp": "2019-05-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1003,
                    "timeseries.ingestion.dataset.size": 31409
                }
            },
            {
                "timestamp": "2019-04-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-03-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-02-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 390,
                    "timeseries.ingestion.dataset.size": 16801
                }
            }
        ],
        "_page": null,
        "_links": null
    },
    "stats": {}
}
```

## Nästa steg

Det här dokumentet innehåller en översikt över API:t för observabilitet. I dokumentet om [tillgängliga mätvärden](metrics.md) finns en fullständig lista med mätvärden som kan användas i API:t.