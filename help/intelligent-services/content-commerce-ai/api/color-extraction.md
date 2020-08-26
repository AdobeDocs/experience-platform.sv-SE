---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;color extraction;Color extraction
solution: Experience Platform
title: Färgextrahering
topic: Developer guide
description: Färgextraheringstjänsten kan, när den har en bild, beräkna histogrammet för pixelfärger och sortera dem efter dominerande färger i grupper.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---


# Färgextrahering

>[!NOTE]
>
>[!DNL Content and Commerce AI] är i betaversion. Dokumentationen kan komma att ändras.

Färgextraheringstjänsten kan, när den har en bild, beräkna ett histogram med pixelfärger och sortera dem efter dominerande färger i grupper. Färgerna i bildpixlarna är inkapslade i 40 dominerande färger som representerar färgspektrumet. Ett histogram med färgvärden beräknas sedan bland dessa 40 färger. Tjänsten har två varianter:

**Färgextrahering (fullständig bild)**

Den här metoden extraherar ett färghistogram i hela bilden.

**Färgextrahering (med mask)**

Den här metoden använder en djupinlärningsbaserad förgrundsextraherare för att identifiera objekt i förgrunden. Modellen har utbildats i en katalog med e-handelsbilder. När förgrundsobjektet har extraherats beräknas ett histogram över de dominerande färgerna enligt beskrivningen ovan.

Följande bild användes i exemplet som visas i det här dokumentet:

![testbild](../images/QQAsset1.jpg)

**API-format**

```http
POST /services/v1/predict
```

**Begäran**

I följande exempelbegäran används helbildsmetoden för färgextrahering.

Följande begäran extraherar färger från en bild baserat på indataparametrarna som anges i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

>[!CAUTION]
>
>`analyzer_id` bestämmer vilket som [!DNL Sensei Content Framework] används. Kontrollera att du har rätt `analyzer_id` information innan du gör din förfrågan. För färgextraheringstjänsten är `analyzer_id` ID:
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
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
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `analyzer_id` | Det [!DNL Sensei] tjänst-ID som din begäran distribueras under. Det här ID:t avgör vilken av dem som [!DNL Sensei Content Frameworks] används. Kontakta Content and Commerce AI-teamet om du vill skapa ett anpassat ID för anpassade tjänster. | Ja |
| `application-id` | ID:t för det program du skapade. | Ja |
| `data` | En array som innehåller JSON-objekt. Varje objekt i arrayen representerar en bild. Alla parametrar som skickas som en del av den här arrayen åsidosätter de globala parametrar som anges utanför `data` arrayen. Alla återstående egenskaper som beskrivs nedan kan åsidosättas inifrån `data`. | Ja |
| `content-id` | Unikt ID för det dataelement som returneras i svaret. Om detta inte skickas tilldelas ett automatiskt genererat ID. | Nej |
| `content` | Det innehåll som ska analyseras av färgextraheringstjänsten. Om bilden är en del av den begärda brödtexten använder du `-F file=@<filename>` i rullningskommandot för att skicka bilden och lämnar den här parametern som en tom sträng. <br> Om bilden är en fil på S3 skickar du den signerade URL:en. När innehållet är en del av begärandetexten bör listan med dataelement bara ha ett objekt. Om fler än ett objekt skickas bearbetas bara det första objektet. | Ja |
| `content-type` | Används för att ange om indata är en del av begärandetexten eller en signerad URL för en S3-bucket. Standardvärdet för den här egenskapen är `inline`. | Nej |
| `encoding` | Indatabildens filformat. För närvarande kan endast JPEG- och PNG-bilder bearbetas. Standardvärdet för den här egenskapen är `jpeg`. | Nej |
| `threshold` | Tröskelvärdet för poäng (0 till 1) över vilket resultaten måste returneras. Använd värdet `0` för att returnera alla resultat. Standardvärdet för den här egenskapen är `0`. | Nej |
| `top-N` | Antalet resultat som ska returneras (får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. När det används tillsammans med `threshold`är antalet resultat som returneras det lägsta av båda begränsningsvärdena. Standardvärdet för den här egenskapen är `0`. | Nej |
| `custom` | Alla anpassade parametrar som ska skickas. | Nej |
| `historic-metadata` | En array som kan skickas som metadata. | Nej |

**Svar**

Ett lyckat svar returnerar detaljerna om de extraherade färgerna. Varje färg representeras av en `feature_value` nyckel som innehåller följande information:

- Ett färgnamn
- Procentandelen av den här färgen som visas i förhållande till bilden
- Färgens RGB-värde

I det första exempelobjektet nedan `feature_value` betyder `White,0.59,251,251,243` det att färgen är vit, vit i 59 % av bilden och har ett RGB-värde på 251 251 243.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `content_id` | Namnet på den bild som överfördes i din POST. |
| `feature_value` | En array vars objekt innehåller nycklar med samma egenskapsnamn. Dessa tangenter innehåller en sträng som representerar färgnamnet, en procentandel som den här färgen visas i förhållande till den bild som skickas i `content_id`och färgens RGB-värde. |
