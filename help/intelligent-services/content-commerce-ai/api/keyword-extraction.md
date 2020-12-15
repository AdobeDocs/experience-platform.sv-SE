---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform, Intelligent Services
title: Extrahering av nyckelord
topic: Developer guide
description: Tjänsten för extrahering av nyckelord extraherar automatiskt nyckelord eller nyckelfraser som bäst beskriver dokumentets ämne när de anges i ett textdokument. För att extrahera nyckelord används en kombination av algoritmer för namngiven enhetsigenkänning (NER) och extrahering av nyckelord utan övervakning.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 2%

---


# Extrahering av nyckelord

>[!NOTE]
>
>[!DNL Content and Commerce AI] är i betaversion. Dokumentationen kan komma att ändras.

Tjänsten för extrahering av nyckelord extraherar automatiskt nyckelord eller nyckelfraser som bäst beskriver dokumentets ämne när de anges i ett textdokument. För att extrahera nyckelord används en kombination av algoritmer för namngiven enhetsigenkänning (NER) och extrahering av nyckelord utan övervakning.

Namngivna entiteter som känns igen av [!DNL Content and Commerce AI] visas i följande tabell:

| Enhetsnamn | Beskrivning |
| --- | --- |
| PERSON | Folk, även påhittade. |
| NORP | Medborgarskap eller religiösa eller politiska grupper. |
| GPE | Länder, städer och stater. |
| LOC | Andra platser än GPE, bergsområden, vattenförekomster. |
| FAC | Byggnader, flygplatser, motorvägar, broar osv. |
| ORG | Företag, myndigheter, institutioner osv. |
| PRODUKT | Objekt, fordon, livsmedel osv. (Inte tjänster.) |
| EVENT | Namngivna orkaner, slag, krig, idrottsevenemang osv. |
| WORK_OF_ART | Boktitlar, låtar osv. |
| LAW | Namngivna dokument som gjorts till lagar. |
| SPRÅK | Valfritt namngivet språk. |

>[!NOTE]
>
>Om du planerar att bearbeta PDF-filer går du vidare till instruktionerna för extrahering [av](#pdf-extraction) PDF-nyckelord i det här dokumentet. Stöd för ytterligare filtyper som docx, ppt, amd xml ställs in på att släppas vid ett senare datum.

**API-format**

```http
POST /services/v1/predict
```

**Begäran**

Följande begäran extraherar nyckelord från ett dokument baserat på indataparametrarna som anges i nyttolasten.

Förenklad JSON för indatafilen:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

>[!CAUTION]
>
>`analyzer_id` bestämmer vilket som [!DNL Sensei Content Framework] används. Kontrollera att du har rätt `analyzer_id` information innan du gör din förfrågan. För nyckelordsextraheringstjänsten är `analyzer_id` ID:
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

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
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `analyzer_id` | Det [!DNL Sensei] tjänst-ID som din begäran distribueras under. Det här ID:t avgör vilken av dem som [!DNL Sensei Content Frameworks] används. Kontakta Content and Commerce AI-teamet om du vill skapa ett anpassat ID för anpassade tjänster. | Ja |
| `application-id` | ID:t för det skapade programmet. | Ja |
| `data` | En array som innehåller ett JSON-objekt med varje objekt i arrayen som representerar ett dokument. Alla parametrar som skickas som en del av den här arrayen åsidosätter de globala parametrar som anges utanför `data` arrayen. Alla återstående egenskaper som beskrivs nedan kan åsidosättas inifrån `data`. | Ja |
| `language` | Inmatningstextens språk. Standardvärdet är `en`. | Nej |
| `content-type` | Används för att ange om indata är en del av begärandetexten eller en signerad URL för en S3-bucket. Standardvärdet för den här egenskapen är `inline`. | Ja |
| `encoding` | Kodningsformatet för indatatext. Det här kan vara `utf-8` eller `utf-16`. Standardvärdet för den här egenskapen är `utf-8`. | Nej |
| `threshold` | Tröskelvärdet för poäng (0 till 1) över vilket resultaten måste returneras. Använd värdet `0` för att returnera alla resultat. Standardvärdet för den här egenskapen är `0`. | Nej |
| `top-N` | Antalet resultat som ska returneras (får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. När det används tillsammans med `threshold`är antalet resultat som returneras det lägsta av båda begränsningsvärdena. Standardvärdet för den här egenskapen är `0`. | Nej |
| `custom` | Alla anpassade parametrar som ska skickas. Den här egenskapen kräver ett giltigt JSON-objekt för att fungera. Mer information om anpassade parametrar finns i [bilagan](#appendix) . | Nej |
| `content-id` | Unikt ID för det dataelement som returneras i svaret. Om detta inte skickas tilldelas ett automatiskt genererat ID. | Nej |
| `content` | Innehållet som används av nyckelordsextraheringstjänsten. Innehållet kan vara rå text (&quot;textbunden&quot; innehållstyp). <br> Om innehållet är en fil på S3 (&#39;s3-bucket&#39; content-type) skickar du den signerade URL:en. När innehållet är en del av begärandetexten bör listan med dataelement bara ha ett objekt. Om fler än ett objekt skickas bearbetas bara det första objektet. | Ja |

**Svar**

Ett lyckat svar returnerar ett JSON-objekt som innehåller extraherade nyckelord i `response` arrayen.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## Extrahering av PDF-nyckelord {#pdf-extraction}

Nyckelordsextraheringstjänsten stöder PDF-filer, men du måste använda ett nytt AnalyzerID för PDF-filer och ändra dokumenttypen till PDF. Se exemplet nedan för mer information.

**API-format**

```http
POST /services/v1/predict
```

**Begäran**

Följande begäran extraherar nyckelord från ett PDF-dokument baserat på indataparametrarna i nyttolasten.

>[!CAUTION]
>
>`analyzer_id` bestämmer vilket som [!DNL Sensei Content Framework] används. Kontrollera att du har rätt `analyzer_id` information innan du gör din förfrågan. Vid extrahering av PDF-nyckelord är `analyzer_id` ID:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| Egenskap | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `analyzer_id` | Det [!DNL Sensei] tjänst-ID som din begäran distribueras under. Det här ID:t avgör vilken av dem som [!DNL Sensei Content Frameworks] används. Kontakta Content and Commerce AI-teamet om du vill skapa ett anpassat ID för anpassade tjänster. | Ja |
| `application-id` | ID:t för det skapade programmet. | Ja |
| `data` | En array som innehåller ett JSON-objekt med varje objekt i arrayen som representerar ett dokument. Alla parametrar som skickas som en del av den här arrayen åsidosätter de globala parametrar som anges utanför `data` arrayen. Alla återstående egenskaper som beskrivs nedan kan åsidosättas inifrån `data`. | Ja |
| `language` | Inmatningsspråk. Standardvärdet är `en` (engelska). | Nej |
| `content-type` | Används för att ange innehållstypen för indata. Den här bör anges till `file`. | Ja |
| `encoding` | Inmatningens kodningsformat. Den här bör anges till `pdf`. Fler kodningstyper är inställda på att stödjas vid ett senare datum. | Ja |
| `threshold` | Tröskelvärdet för poäng (0 till 1) över vilket resultaten måste returneras. Använd värdet `0` för att returnera alla resultat. Standardvärdet för den här egenskapen är `0`. | Nej |
| `top-N` | Antalet resultat som ska returneras (får inte vara ett negativt heltal). Använd värdet `0` för att returnera alla resultat. När det används tillsammans med `threshold`är antalet resultat som returneras det lägsta av båda begränsningsvärdena. Standardvärdet för den här egenskapen är `0`. | Nej |
| `custom` | Alla anpassade parametrar som ska skickas. Den här egenskapen kräver ett giltigt JSON-objekt för att fungera. Mer information om anpassade parametrar finns i [bilagan](#appendix) . | Nej |
| `content-id` | Unikt ID för det dataelement som returneras i svaret. Om detta inte skickas tilldelas ett automatiskt genererat ID. | Nej |
| `content` | Den här bör anges till `file`. | Ja |

**Svar**

Ett lyckat svar returnerar ett JSON-objekt som innehåller extraherade nyckelord i `response` arrayen.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

Mer information och ett exempel på hur du använder PDF-extrahering med instruktioner om hur du konfigurerar, distribuerar och integrerar med AEM molntjänst. Besök [CCAI PDF-extraheringsarbetarens digitalarkiv](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Bilaga {#appendix}

Följande tabell innehåller tillgängliga parametrar som kan användas inifrån `custom`.

| Namn | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `min-n` | Det minsta antalet ord som krävs i nyckelorden. | Nej |
| `entity-types` | Typer av entiteter som ska returneras. Se tabellen för igenkänning av namngiven entitet i början av det här dokumentet. | Nej |