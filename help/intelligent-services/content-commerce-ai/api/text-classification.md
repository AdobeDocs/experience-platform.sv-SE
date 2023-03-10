---
keywords: textklassificering;Textklassificering
solution: Experience Platform
title: Textklassificering i API:t för innehåll och handel
description: När textklassificeringstjänsten anger ett textfragment kan den klassificeras i en eller flera etiketter. Klassificeringen kan vara en enstaka etikett, flera etiketter eller hierarkisk.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# Textklassificering

>[!NOTE]
>
>Innehåll och handel AI är i betaversion. Dokumentationen kan komma att ändras.

När textklassificeringstjänsten anger ett textfragment kan den klassificeras i en eller flera etiketter. Klassificeringen kan vara en enstaka etikett, flera etiketter eller hierarkisk.

**API-format**

```http
POST /services/v1/predict
```

**Begäran**

Följande begäran klassificerar text från ett fragment baserat på indataparametrarna som anges i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

>[!CAUTION]
>
>`analyzer_id` avgör [!DNL Sensei Content Framework] används. Kontrollera att du har rätt `analyzer_id` innan du gör din begäran. Kontakta Content and Commerce AI beta team för att få ditt `analyzer_id` för den här tjänsten.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\", 
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `analyzer_id` | The [!DNL Sensei] tjänst-ID som din begäran distribueras under. Detta ID avgör vilket av [!DNL Sensei Content Frameworks] används. Kontakta Content and Commerce AI-teamet om du vill skapa ett anpassat ID för anpassade tjänster. | Ja |
| `application-id` | ID:t för det program som skapades. | Ja |
| `data` | En array som innehåller ett JSON-objekt med varje objekt i arrayen som representerar ett dokument. Alla parametrar som skickas som en del av den här arrayen åsidosätter de globala parametrar som anges utanför `data` array. Alla återstående egenskaper som beskrivs nedan i den här tabellen kan åsidosättas inifrån `data`. | Ja |
| `language` | Inmatningstextens språk. Standardvärdet är `en`. | Nej |
| `content-type` | Används för att ange om indata är en del av begärandetexten eller en signerad URL för en S3-bucket. Standardvärdet för den här egenskapen är `inline`. | Nej |
| `encoding` | Kodningsformatet för indatatext. Det här kan `utf-8` eller `utf-16`. Standardvärdet för den här egenskapen är `utf-8`. | Nej |
| `threshold` | Tröskelvärdet för poäng (0 till 1) över vilket resultaten måste returneras. Använd värdet `0` för att returnera alla resultat. Standardvärdet för den här egenskapen är `0`. | Nej |
| `top-N` | Antalet resultat som ska returneras (får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. Vid användning tillsammans med `threshold`, är antalet returnerade resultat det mindre av någon av begränsningsuppsättningarna. Standardvärdet för den här egenskapen är `0`. | Nej |
| `custom` | Alla anpassade parametrar som ska skickas. Den här egenskapen kräver ett giltigt JSON-objekt för att fungera. | Nej |
| `content-id` | Unikt ID för det dataelement som returneras i svaret. Om detta inte skickas tilldelas ett automatiskt genererat ID. | Nej |
| `content` | Innehållet som används av texturklassificeringstjänsten. Innehållet kan vara rå text (&#39;inline&#39; content-type). <br> Om innehållet är en fil på S3 (&#39;s3-bucket&#39; content-type) skickar du den signerade URL:en. | Ja |

**Svar**

Ett lyckat svar returnerar den klassificerade texten i en svarsarray.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
