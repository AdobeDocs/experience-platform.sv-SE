---
keywords: text classification;Text classification
solution: Experience Platform
title: API-slutpunkt för textklassificering
topic: Developer guide
description: När textklassificeringstjänsten anger ett textfragment kan den klassificeras i en eller flera etiketter. Klassificeringen kan vara en enstaka etikett, flera etiketter eller hierarkisk.
translation-type: tm+mt
source-git-commit: 4f7b5ca50171f4948726c44dbf31025011adf35f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# Textklassificering

>[!NOTE]
>
>Innehåll och handel AI är i betaversion. Dokumentationen kan komma att ändras.

När textklassificeringstjänsten anger ett textfragment kan den klassificeras i en eller flera etiketter. Klassificeringen kan vara en enstaka etikett, flera etiketter eller hierarkisk.

Textklassificering använder en [FastText](https://fasttext.cc/) -baserad modell som har tränats med anpassade data.

**API-format**

```http
POST /services/v1/predict
```

**Begäran**

Följande begäran klassificerar text från ett fragment baserat på indataparametrarna som anges i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

>[!CAUTION]
>
>`analyzer_id` bestämmer vilket som [!DNL Sensei Content Framework] används. Kontrollera att du har rätt `analyzer_id` information innan du gör din förfrågan. Kontakta betateamet för Content and Commerce AI om du vill ha dina svar `analyzer_id` för den här tjänsten.

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
| `analyzer_id` | Det [!DNL Sensei] tjänst-ID som din begäran distribueras under. Det här ID:t avgör vilken av dem som [!DNL Sensei Content Frameworks] används. Kontakta Content and Commerce AI-teamet om du vill skapa ett anpassat ID för anpassade tjänster. | Ja |
| `application-id` | ID:t för programmet som skapades. | Ja |
| `data` | En array som innehåller ett JSON-objekt med varje objekt i arrayen som representerar ett dokument. Alla parametrar som skickas som en del av den här arrayen åsidosätter de globala parametrar som anges utanför `data` arrayen. Alla återstående egenskaper som beskrivs nedan kan åsidosättas inifrån `data`. | Ja |
| `language` | Inmatningstextens språk. Standardvärdet är `en`. | Nej |
| `content-type` | Används för att ange om indata är en del av begärandetexten eller en signerad URL för en S3-bucket. Standardvärdet för den här egenskapen är `inline`. | Nej |
| `encoding` | Kodningsformatet för indatatext. Det här kan vara `utf-8` eller `utf-16`. Standardvärdet för den här egenskapen är `utf-8`. | Nej |
| `threshold` | Tröskelvärdet för poäng (0 till 1) över vilket resultaten måste returneras. Använd värdet `0` för att returnera alla resultat. Standardvärdet för den här egenskapen är `0`. | Nej |
| `top-N` | Antalet resultat som ska returneras (får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. När det används tillsammans med `threshold`är antalet resultat som returneras det lägsta av båda begränsningsvärdena. Standardvärdet för den här egenskapen är `0`. | Nej |
| `custom` | Alla anpassade parametrar som ska skickas. Den här egenskapen kräver ett giltigt JSON-objekt för att fungera. | Nej |
| `content-id` | Unikt ID för det dataelement som returneras i svaret. Om detta inte skickas tilldelas ett automatiskt genererat ID. | Nej |
| `content` | Innehållet som används av texturklassificeringstjänsten. Innehållet kan vara rå text (&quot;textbunden&quot; innehållstyp). <br> Om innehållet är en fil på S3 (&#39;s3-bucket&#39; content-type) skickar du den signerade URL:en. | Ja |

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
