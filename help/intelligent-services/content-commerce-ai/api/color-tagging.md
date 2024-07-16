---
keywords: Experience Platform;komma igång;content;content tagging;color tagging;color extraction;
solution: Experience Platform
title: Färgtaggning i API:t för innehållstaggning
description: När en bild anges kan du med tjänsten Färgtaggning beräkna histogrammet för pixelfärger och sortera dem efter dominerande färger i grupper.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Färgtaggning

Färgtaggningstjänsten kan, när den har en bild, beräkna ett histogram med pixelfärger och sortera dem efter dominerande färger i grupper. Färgerna i bildpixlarna är inkapslade i 40 dominerande färger som representerar färgspektrumet. Ett histogram med färgvärden beräknas sedan bland dessa 40 färger. Tjänsten har två varianter:

**Färgtaggning (fullständig bild)**

Med den här metoden extraheras ett färghistogram över hela bilden.

**Färgtaggning (med mask)**

Den här metoden använder en djupinlärningsbaserad förgrundsextraherare för att identifiera objekt i förgrunden. När förgrundsobjekten har extraherats beräknas ett histogram över de dominerande färgerna för både förgrunds- och bakgrundsregionerna, tillsammans med hela bilden.

**Tonextrahering**

Förutom varianterna ovan kan du konfigurera tjänsten så att den hämtar ett histogram med toner för:

- Den övergripande bilden (när en fullständig bildvariant används)
- Den övergripande bilden samt för- och bakgrundsregionerna (när du använder varianten med maskering)

Följande bild användes i exemplet som visas i det här dokumentet:

![testbild](../images/QQAsset1.jpg)

**API-format**

```http
POST /services/v2/predict
```

**Begäran - fullständig bildvariant**

I följande exempelbegäran används helbildsmetoden för färgtaggning och färger extraheras från en bild baserat på indataparametrarna i nyttolasten. Se tabellen under exempelnyttolasten för mer information om de indataparametrar som visas.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**Svar - fullständig bildvariant**

Ett lyckat svar returnerar detaljerna om de extraherade färgerna. Varje färg representeras av en `feature_value`-nyckel som innehåller följande information:

- Ett färgnamn
- Procentandelen av den här färgen som visas i förhållande till bilden
- Färgens RGB

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`innebär att den hittade färgen är vit, vilket finns i 58,34 % av bilden, och har ett genomsnittligt RGB-värde på 254, 254, 243.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

Observera att resultatet här har extraherad färg på det&quot;övergripande&quot; bildområdet.

**Begäran - maskerad bildvariant**

I följande exempelbegäran används maskeringsmetoden för färgtaggning. Detta aktiveras genom att parametern `enable_mask` ställs in på `true` i begäran.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>[!NOTE]
>
>Dessutom är parametern `retrieve_tone` inställd på `true` i ovanstående begäran. Detta gör att vi kan hämta ett histogram för tonfördelning över varma, neutrala och svala toner i bildens övergripande, för- och bakgrundsregioner.

**Response - maskerad bildvariant**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

Förutom färgerna från den övergripande bilden kan du nu även se färger från förgrunds- och bakgrundsregionerna. Eftersom tonhämtning är aktiverad för vart och ett av de ovanstående områdena kan du även hämta en tons histogram.

**Indataparametrar**

| Namn | Datatyp | Obligatoriskt | Standard | Värden | Beskrivning |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Ja | – | Se nedan | Lista med JSON-element där varje objekt i listan representerar ett dokument. |
| `top_n` | tal | Nej | 0 | Icke-negativt heltal | Antal resultat som ska returneras. 0, för att returnera alla resultat. Vid användning tillsammans med tröskelvärde blir antalet returnerade resultat mindre än någon av gränserna. |
| `min_coverage` | tal | Nej | 0,05 | Realnummer | Tröskelvärde för täckning över vilket resultaten måste returneras. Exkludera parameter för att returnera alla resultat. |
| `resize_image` | tal | Nej | True | Sant/falskt | Anger om indatabildens storlek ska ändras eller inte. Som standard ändras bildens storlek till 320*320 pixlar innan färgextraheringen utförs. I felsökningssyfte kan vi även tillåta att koden körs på en fullständig bild genom att ange det här till `False`. |
| `enable_mask` | tal | Nej | Falskt | Sant/falskt | Aktiverar/inaktiverar färgextrahering |
| `retrieve_tone` | tal | Nej | Falskt | Sant/falskt | Aktiverar/inaktiverar tonextrahering |

**Dokumentobjekt**

| Namn | Datatyp | Obligatoriskt | Standard | Värden | Beskrivning |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Dokumentets försignerade URL. |
| `sensei:repoType` | string | – | – | HTTPS | Typ av rapport där bilden lagras. |
| `sensei:multipart_field_name` | string | – | – | – | Använd detta när du skickar bildfilen som ett multipart-argument i stället för att använda försignerade URL:er. |
| `dc:format` | string | Ja | – | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | Bildkodningen kontrolleras mot tillåtna indatakodningstyper innan den bearbetas. |