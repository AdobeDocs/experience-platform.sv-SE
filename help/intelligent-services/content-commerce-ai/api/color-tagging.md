---
keywords: Experience Platform;komma igång;content ai;commerce ai;content tagging;color tagging;color extraction;
solution: Experience Platform
title: Färgtaggning i innehållstaggnings-API
description: Färgtaggningstjänsten kan, när den har en bild, beräkna histogrammet för pixelfärger och sortera dem efter dominerande färger i grupper.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# Färgtaggning

Färgtaggningstjänsten kan, när den har en bild, beräkna ett histogram med pixelfärger och sortera dem efter dominerande färger i grupper. Färgerna i bildpixlarna är inkapslade i 40 dominerande färger som representerar färgspektrumet. Ett histogram med färgvärden beräknas sedan bland dessa 40 färger. Tjänsten har två varianter:

**Färgtaggning (fullständig bild)**

Den här metoden extraherar ett färghistogram i hela bilden.

**Färgtaggning (med mask)**

Den här metoden använder en djupinlärningsbaserad förgrundsextraherare för att identifiera objekt i förgrunden. Modellen har utbildats i en katalog med e-handelsbilder. När förgrundsobjektet har extraherats beräknas ett histogram över de dominerande färgerna enligt beskrivningen ovan.

Följande bild användes i exemplet som visas i det här dokumentet:

![testbild](../images/QQAsset1.jpg)

**API-format**

```http
POST /services/v2/predict
```

**Begäran**

I följande exempelbegäran används helbildsmetoden för färgtaggning.

Följande begäran extraherar färger från en bild baserat på indataparametrarna som anges i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `application-id` | ID:t för det program du skapade. | Ja |
| `documents` | En lista med JSON-element där varje objekt i listan representerar ett dokument. | Ja |
| `top_n` | Antalet resultat som ska returneras (detta får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. Vid användning tillsammans med `threshold`, är antalet returnerade resultat det mindre av någon av begränsningsuppsättningarna. Standardvärdet för den här egenskapen är `0`. | Nej |
| `min_coverage` | Tröskelvärde för täckning över vilket resultaten måste returneras. Exkludera parametern för att returnera alla resultat. | Nej |
| `resize_image` | Anger om indatabildens storlek ska ändras. Som standard ändras bildens storlek till 320*320 pixlar innan färgtaggning utförs. I felsökningssyfte kan vi även tillåta att koden körs på en fullständig bild genom att ange värdet False. | Nej |
| `enable_mask` | Aktiverar/inaktiverar färgtaggning i en mask. | Nej |

| Namn | Datatyper | Obligatoriskt | Standard | Värden | Beskrivning |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Försignerad URL för det dokument från vilket nyckelfraser ska extraheras. |
| `sensei:repoType` | string | – | – | HTTPS | Typ av rapport där bilden lagras. |
| `sensei:multipart_field_name` | string | – | – | – | Använd detta när du skickar en bildfil som ett multipart-argument i stället för att använda försignerade URL:er. |
| `dc:format` | string | Ja | – | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | Bildkodningen kontrolleras mot tillåtna indatakodningstyper innan den bearbetas. |

**Svar**

Ett lyckat svar returnerar detaljerna om de extraherade färgerna. Varje färg representeras av en `feature_value` som innehåller följande information:

- Ett färgnamn
- Procentandelen av den här färgen som visas i förhållande till bilden
- Färgens RGB

I det första exempelobjektet nedan är `feature_value` av `Mud_Green,0.069,102,72,95` innebär att den hittade färgen är lera grön, lera grön finns i 6,9 % av bilden och har RGB-värdet 102,72,95.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
      "invocations": [
        {
          "sensei:outputs": {
            "result": {
              "sensei:multipart_field_name": "result",
              "dc:format": "application/json"
            }
          },
          "message": null,
          "status": "200"
        }
      ]
    }
  ],
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
