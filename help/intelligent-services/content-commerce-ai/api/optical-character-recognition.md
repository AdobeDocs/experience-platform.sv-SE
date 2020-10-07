---
keywords: OCR;text presence;optical character recognition
solution: Experience Platform
title: Optisk teckenigenkänning
topic: Developer guide
description: Tjänsten för textnärvaro/optisk teckenigenkänning (OCR), när en bild anges, kan visa om det finns text i bilden. Om det finns text kan OCR returnera texten
translation-type: tm+mt
source-git-commit: 4d12caf949aeb6619cd27b55855014a61d4e54bb
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---


# Textnärvaro och optisk teckenigenkänning

>[!NOTE]
>
>Innehåll och handel AI är i betaversion. Dokumentationen kan komma att ändras.

Tjänsten för textnärvaro/optisk teckenigenkänning (OCR), när en bild anges, kan visa om det finns text i bilden. Om det finns text kan OCR returnera texten.

Följande bild användes i exempelbegäran som visas i det här dokumentet:

![testbild](../images/shef.jpeg)

**API-format**

```http
POST /services/v1/predict
```

**Begäran**

Följande begäran kontrollerar om det finns text baserad på den indatabild som anges i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

>[!CAUTION]
>
>`analyzer_id` bestämmer vilket som [!DNL Sensei Content Framework] används. Kontrollera att du har rätt `analyzer_id` information innan du gör din förfrågan. Kontakta betateamet för Content and Commerce AI om du vill ha dina svar `analyzer_id` för den här tjänsten.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
    "parameters": {
      "application-id": "1234",
      "content-type": "inline",
      "encoding": "jpeg",
      "threshold": "0",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "0987",
        "content": "inline-image",
        "content-type": "inline",
        "encoding": "jpeg",
        "threshold": "0",
        "top-N": "0",
        "historic-metadata": [],
        "custom": {}
        }]
      }
    }]
  }'
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `analyzer_id` | Det [!DNL Sensei] tjänst-ID som din begäran distribueras under. Det här ID:t avgör vilken av dem som [!DNL Sensei Content Frameworks] används. Kontakta Content and Commerce AI-teamet om du vill skapa ett anpassat ID för anpassade tjänster. | Ja |
| `application-id` | ID:t för det program som skapades. | Ja |
| `data` | En array som innehåller ett JSON-objekt med varje objekt i arrayen som representerar en bild som skickas. Alla parametrar som skickas som en del av den här arrayen åsidosätter de globala parametrar som anges utanför `data` arrayen. Alla återstående egenskaper som beskrivs nedan kan åsidosättas inifrån `data`. | Ja |
| `language` | Inmatningstextens språk. Standardvärdet är `en`. | Nej |
| `content-type` | Används för att ange om indata är en del av begärandetexten eller en signerad URL för en S3-bucket. Standardvärdet för den här egenskapen är `inline`. | Nej |
| `encoding` | Indatabildens filformat. För närvarande kan endast JPEG- och PNG-bilder bearbetas. Standardvärdet för den här egenskapen är `jpeg`. | Nej |
| `threshold` | Tröskelvärdet för poäng (0 till 1) över vilket resultaten måste returneras. Använd värdet `0` för att returnera alla resultat. Standardvärdet för den här egenskapen är `0`. | Nej |
| `top-N` | Antalet resultat som ska returneras (får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. När det används tillsammans med `threshold`är antalet resultat som returneras det lägsta av båda begränsningsvärdena. Standardvärdet för den här egenskapen är `0`. | Nej |
| `custom` | Alla anpassade parametrar som ska skickas. Den här egenskapen kräver ett giltigt JSON-objekt för att fungera. | Nej |
| `content-id` | Unikt ID för det dataelement som returneras i svaret. Om detta inte skickas tilldelas ett automatiskt genererat ID. | Nej |
| `content` | Innehållet kan vara en Raw-bild (&quot;textbunden&quot; innehållstyp). <br> Om innehållet är en fil på S3 (innehållstypen S3-bucket) skickar du den signerade URL:en. | Ja |

**Svar**

Ett godkänt svar returnerar den text som upptäcktes i `feature_value` arrayen. Texten läses och returneras uppifrån och ned från vänster till höger. Det innebär att om &quot;Jag älskar Adobe&quot; upptäcktes returnerar din nyttolast &quot;I&quot;, &quot;Love&quot; och &quot;Adobe&quot; i separata objekt. I objektet får du en `feature_name` som innehåller ordet och en `feature_value` som innehåller ett konfidensmått för texten.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
