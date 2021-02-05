---
keywords: Visuell likhet;visuell likhet;ccai api
solution: Experience Platform, Intelligent Services
title: Visuell likhet i API:t för innehåll och handel
topic: Developer guide
description: När en bild anges hittas visuellt liknande bilder från en katalog automatiskt av den visuella likhetstjänsten.
translation-type: tm+mt
source-git-commit: d10c00694b0a3b2a9da693bd59615b533cfae468
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---


# Visuell likhet

>[!NOTE]
>
>[!DNL Content and Commerce AI] är i betaversion. Dokumentationen kan komma att ändras.

När en bild anges hittas visuellt liknande bilder från en katalog automatiskt av den visuella likhetstjänsten.

Följande bild användes i exempelbegäran som visas i det här dokumentet:

![testbild](../images/Query_Image.jpeg)

**API-format**

```http
POST /services/v1/predict
```

**Begäran**

Följande begäran hämtar visuellt liknande bilder från en katalog baserat på indataparametrarna som finns i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

>[!CAUTION]
>
>`analyzer_id` bestämmer vilket som  [!DNL Sensei Content Framework] används. Kontrollera att du har rätt `analyzer_id` innan du gör din begäran. Kontakta Content and Commerce AI beta-teamet för att få ditt `analyzer_id` för den här tjänsten.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
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
      }
    ]
}'
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `analyzer_id` | Det tjänst-ID för [!DNL Sensei] som din begäran distribueras under. Detta ID avgör vilket av [!DNL Sensei Content Frameworks] som används. Kontakta Content and Commerce AI-teamet om du vill skapa ett anpassat ID för anpassade tjänster. | Ja |
| `application-id` | ID:t för det program du skapade. | Ja |
| `data` | En array som innehåller ett JSON-objekt med varje objekt i arrayen som representerar en bild. Alla parametrar som skickas som en del av den här arrayen åsidosätter de globala parametrar som anges utanför `data`-arrayen. Alla återstående egenskaper som beskrivs nedan kan åsidosättas inifrån `data`. | Ja |
| `content-id` | Unikt ID för det dataelement som returneras i svaret. Om detta inte skickas tilldelas ett automatiskt genererat ID. | Nej |
| `content` | Det innehåll som ska analyseras av den visuella likhetstjänsten. Om bilden är en del av begärandetexten använder du `-F file=@<filename>` i rullkommandot för att skicka bilden och låter den här parametern vara en tom sträng. <br> Om bilden är en fil på S3 skickar du den signerade URL:en. När innehållet är en del av begärandetexten bör listan med dataelement bara ha ett objekt. Om fler än ett objekt skickas bearbetas bara det första objektet. | Ja |
| `content-type` | Används för att ange om indata är en del av begärandetexten eller en signerad URL för en S3-bucket. Standardvärdet för den här egenskapen är `inline`. | Nej |
| `encoding` | Indatabildens filformat. För närvarande kan endast JPEG- och PNG-bilder bearbetas. Standardvärdet för den här egenskapen är `jpeg`. | Nej |
| `threshold` | Tröskelvärdet för poäng (0 till 1) över vilket resultaten måste returneras. Använd värdet `0` för att returnera alla resultat. Standardvärdet för den här egenskapen är `0`. | Nej |
| `top-N` | Antalet resultat som ska returneras (får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. När det används tillsammans med `threshold` är antalet resultat som returneras det lägsta av båda begränsningsuppsättningarna. Standardvärdet för den här egenskapen är `0`. | Nej |
| `custom` | Alla anpassade parametrar som ska skickas. | Nej |
| `historic-metadata` | En array som kan skickas som metadata. | Nej |

**Svar**

Ett lyckat svar returnerar en `response`-matris som innehåller `feature_value` och `feature_name` för var och en av de visuellt liknande bilderna i katalogen.

Följande visuellt liknande bilder returnerades i det exempelsvar som visas nedan:

![liknande bilder](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```

