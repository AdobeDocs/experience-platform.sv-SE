---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Färgextrahering
topic: Developer guide
description: Tjänsten för extrahering av nyckelord extraherar automatiskt nyckelord eller nyckelfraser som bäst beskriver dokumentets ämne när de anges i ett textdokument. För att extrahera nyckelord används en kombination av algoritmer för namngiven enhetsigenkänning (NER) och extrahering av nyckelord utan övervakning.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 2%

---


# Extrahering av nyckelord

>[!NOTE]
>
>[!DNL Content and Commerce AI] är i betaversion. Dokumentationen kan komma att ändras.

Tjänsten för extrahering av nyckelord extraherar automatiskt nyckelord eller nyckelfraser som bäst beskriver dokumentets ämne när de anges i ett textdokument. För att extrahera nyckelord används en kombination av algoritmer för namngiven enhetsigenkänning (NER) och extrahering av nyckelord utan övervakning.

**Oövervakad extrahering av nyckelord**

För oövervakad extrahering av nyckelord används [[!DNL YAKE]](http://yake.inesctec.pt/) . [!DNL YAKE] är en snabb och korrekt automatisk extraheringsmetod utan övervakning som används för att välja de viktigaste nyckelorden från ett dokument. Nyckelordsutdragen [!DNL YAKE] filtreras sedan så att endast tio fraser markeras.

**Identifiering av namngiven enhet**

För namngiven entitetsigenkänning används [[!DNL spaCy]](https://spacy.io/)OntoNotes-modellen. Den här modellen tilldelar kontextspecifika tokenvektorer, POS-taggar (part-of-tal), beroendeanalys och namngivna entiteter. OntoNotes-modellen är en av de viktigaste [!DNL spaCy] modellerna. Mer information om OntoNotes-modellen finns [här](https://spacy.io/models/en).

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

Resultaten från [!DNL OntoNotes] kombineras med nyckelorden från [!DNL YAKE]och returneras sedan i rangordningsordning efter deras prioritet.

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
| `application-id` | ID:t för programmet som skapades. | Ja |
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

## Bilaga {#appendix}

Följande tabell innehåller tillgängliga parametrar som kan användas inifrån `custom`.

| Namn | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `min-n` | Det minsta antalet ord som krävs i nyckelorden. | Nej |
| `entity-types` | Typer av entiteter som ska returneras. Se tabellen för igenkänning av namngiven entitet i början av det här dokumentet. | Nej |