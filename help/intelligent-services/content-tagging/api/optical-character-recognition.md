---
keywords: OCR;text presence;optical character recognition
solution: Experience Platform
title: Textnärvaro och optisk teckenigenkänning
description: I API:t för innehållstaggning kan OCR-tjänsten (Text Presence/Optical Character Recognition) visa om det finns text i en viss bild. Om det finns text kan OCR returnera texten.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: feebf4c20d20afcdcfe4523e0b61bff5b999084c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Textnärvaro och optisk teckenigenkänning

Tjänsten för textnärvaro/optisk teckenigenkänning (OCR) kan, när den har en bild, visa om det finns text i bilden. Om det finns text kan OCR returnera texten.

Följande bild användes i exempelbegäran som visas i det här dokumentet:

![Exempelbild](../images/sample_image.png)

**API-format**

```http
POST /services/v2/predict
```

**Begäran**

Följande begäran kontrollerar om det finns text baserad på den indatabild som anges i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

Körning med textbunden bild:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**Svar**

Ett godkänt svar returnerar texten som upptäcktes i `tags` lista för varje bild som skickades i begäran. Om det inte finns någon text i en viss bild `is_text_present` är 0 och `tags` är en tom lista.

[result0, result1, ...]: lista med svar för varje indatadokument. Varje resultat är en ordlista med nycklar:

1. request_element_id: motsvarande index till indatafilen för det här svaret, 0 för den första bilden i dokumentlistan för begäran, 1 för nästa och så vidare.
2. taggar: lista med ordlistor. Varje ordlista har två nycklar: text, som är ett känt ord från bilden, och relevans, som beräknas som den del av den extraherade textens begränsningsram som är i jämförelse med hela bilden. 0,01 skulle motsvara en text som upptar minst 1 % av bilden.
3. is_text_present: 0 eller 1 beroende på om det finns text i bilden. Om taggarna är 0 är listan tom.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
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
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.05604639115920341
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**Begäran**

Följande begäran kontrollerar om det finns text baserad på den indatabild som anges i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

Körning med URL:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
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
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `documents` | Lista med JSON-element där varje objekt i listan representerar en bild. Alla parametrar som skickas som en del av den här listan åsidosätter den globala parametern som anges utanför listan för motsvarande listelement. | Ja |
| `sensei:multipart_field_name` | field_name att läsa indatafilens sökväg från. | Ja |
| `repo:path` | Försignerad URL till bildresurs. | Ja |
| `sensei:repoType` | &quot;HTTP&quot; (för presigned-url). | Nej |
| `dc:format` | Kodat format för indatabilden. Endast bildformat som jpeg, jpg, png och tiff tillåts för bildkodning. dc:format matchas mot tillåtna format. | Nej |
| `correct_with_dictionary` | Om orden ska korrigeras med en engelsk ordbok? Om detta inte är aktiverat kan det finnas risk för att ord som inte är engelska identifieras. Standardvärdet är Sant: aktiverad.) Observera att när ordlistan är aktiverad behöver du inte alltid få ett engelskt ord. Vi försöker rätta till det, men om det inte går inom ett visst redigeringsavstånd, returnerar vi det ursprungliga ordet. | Nej |
| `filter_with_dictionary` | Om orden ska filtreras så att de bara innehåller orden från den engelska ordboken? Om detta är aktiverat kommer de returnerade orden alltid att tillhöra den stora engelska som innehåller 470 kB-ord. | Nej |
| `min_probability` | Hur stor är den minsta sannolikheten för de identifierade orden? Endast de ord som extraheras från bilden och som har större sannolikhet än min_sannolikhet returneras av tjänsten. Standardvärdet är 0,2. | Nej |
| `min_relevance` | Vilken är den minsta relevansen för de identifierade orden? Endast de ord som extraheras från bilden och har större relevans än min_relevant returneras av tjänsten. Standardvärdet är 0,01. Relevansen beräknas som andelen av den extraherade textens begränsningsram jämfört med hela bilden. 0,01 skulle motsvara en text som upptar minst 1 % av bilden. | Nej |

| Namn | Datatyper | Obligatoriskt | Standard | Värden | Beskrivning |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Försignerad URL för bilden som texten ska extraheras från. |
| `sensei:repoType` | string | – | – | HTTPS | Typ av rapport där bilden lagras. |
| `sensei:multipart_field_name` | string | – | – | – | Använd detta när du skickar bilden som ett multipart-argument i stället för att använda försignerade URL:er. |
| `dc:format` | string | Ja | – | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | Bildkodningen kontrolleras mot tillåtna indatakodningstyper innan den bearbetas. |