---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exempel på ETL-omformningar
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Exempel på ETL-omformningar

I den här artikeln visas följande exempelomformningar som en utvecklare av Extract, Transform, Load (ETL) kan stöta på.

## Platt CSV till hierarki

### Exempelfiler

Exempel på CSV- och JSON-filer finns i den offentliga ETL Reference- [!DNL GitHub] rapporten från Adobe:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

### Exempel på CSV

Följande CRM-data har exporterats som `CRM_profiles.csv`:

```shell
TITLE   F_NAME  L_NAME  GENDER  DOB EMAIL   CRMID   ECID    LOYALTYID   ECID2   PHONE   STREET  CITY    STATE   COUNTRY ZIP LAT LONG
Mr  Ewart   Bennedsen   M   2004-09-25  ebennedsenex@jiathis.com    71a16013-d805-7ece-9ac4-8f2cd66e8eaa    87098882279810196101440938110216748923  2e33192000007456-0365c00000000000   55019962992006103186215643814973128178  256-284-7231    72 Buhler Crossing  Anniston    Alabama US  36205   33.708276   -85.7922905
Dr  Novelia Ansteys F   1987-10-31  nansteysdk@spotify.com  2eeb6532-82e1-0d58-8955-bf97de66a6f5    50829196174854544323574004005273946998  2e3319208000765b-3811c00000000001   65233136134594262632703695260919939885  704-181-6371    79 Northfield Hill  Charlotte   North Carolina  US  28299   35.2188655  -80.8108885
Mr  Ulises  Mochan  M   1996-03-20  umochanco@gnu.org   6f393075-addb-bdd6-73f8-31c393b700f5    70086119428645095847094710218289660855  2e33192080003023-26b2000000000002   82011353387947708954389153068944017636  720-837-4159    00671 Mifflin Trail Lacolle Qu√©bec CA  E5A 45.08338    -73.36585
Mrs Friederike  Durrell F   1979-01-3   fdurrellbj@utexas.edu   33d018ec-5fed-f1a3-56aa-079370a9511b    50164729868919217963697788808932473456  2e33192080006dfc-0cdf400000000003   64452712468609735658703639722261004071  798-528-3458    47 Fremont Hill Independencia   Veracruz Llave  MX  91891   19.3803931  -99.1476905
Rev Evita   Bingall F   1974-02-28  ebingallod@mac.com  8c93db88-f328-8efb-dc73-d5654d371cbe    74973364195185450328832136951985519627  2e331920800038db-0559e00000000004   58945501950285346322834356669253860483  397-178-5897    56 Crescent Oaks Court  Buenavista  Oaxaca  MX  71730   19.4458447  -99.1497665
Mr  Eugenie Bechley F   1969-05-19  ebechley9r@telegraph.co.uk  b0c76a3f-6526-0ad0-e050-48143b687d18    67119779213799783658184754966135750376  2e331920800001a4-24b2800000000005   59715249079109455676103900762283358508  718-374-7456    5760 Southridge Junction    Staten Island   New York    US  10310   40.6307451  -74.1181235
Dr  Cammi   Haslen  F   1973-12-17  chaslenqv@ehow.com  56059cd5-5006-ce5f-2f5f-15b4d856a204    61747117963243728095047674165570746095  2e33192080007c25-2ec0600000000006   86268258269066295956223980330791223320  865-538-8291    83 Veith Street Knoxville   Tennessee   US  37995   35.95   -84.05
```

### Mappning

Mappningskraven för CRM-data beskrivs i följande tabell och innehåller följande omformningar:
- Identitetskolumner till `identityMap` egenskaper
- Födelsedatum (DOB) till år och månad
- Strängar till dubbletter eller korta heltal.

| CSV-kolumn | XDM-sökväg | Dataformatering |
| ---------- | -------- | --------------- |
| RUBRIK | person.name.courtesyTitle | Kopiera som sträng |
| F_NAME | person.name.firstName | Kopiera som sträng |
| L_NAME | person.name.lastName | Kopiera som sträng |
| GENDER | person.gender | Transformera kön som motsvarande person.genusuppräkningsvärde |
| DOB | person.bornDayAndMonth: &quot;MM-DD&quot;<br/>person.födelsedatum: &quot;YYY-MM-DD&quot;<br/>person.födelseår: YYYY | Omvandla födelsedagenDayAndMonth som<br/>stringTransform<br/>födelsedatum somstringTransform födelseår som kort int |
| E-POST | personalEmail.address | Kopiera som sträng |
| CRMID | identityMap.CRMID[{&quot;id&quot;:x, primär:false}] | Kopiera som sträng till CRMID-matris i identityMap och ange Primary som false |
| ECID | identityMap.ECID[{&quot;id&quot;:x, primär: false}] | Kopiera som sträng till första posten i ECID-matrisen i identityMap och ange Primary som false |
| LOYALTYID | identityMap.LOYALTYID[{&quot;id&quot;:x, primär:true}] | Kopiera som sträng till LOYALTYID-matris i identityMap och ange Primary som true |
| ECID2 | identityMap.ECID[{&quot;id&quot;:x, primär:false}] | Kopiera som sträng till andra posten i ECID-matrisen i identityMap och ange Primary till false |
| TELEFON | homePhone.number | Kopiera som sträng |
| STREET | homeAddress.street1 | Kopiera som sträng |
| ORT | homeAddress.city | Kopiera som sträng |
| LÄGE | homeAddress.stateProvince | Kopiera som sträng |
| LAND | homeAddress.country | Kopiera som sträng |
| ZIP | homeAddress.postalCode | Kopiera som sträng |
| LAT | homeAddress.latitude | Konvertera till dubbel |
| LÅNG | homeAddress.longitude | Konvertera till dubbel |


### Utdata-XDM

I följande exempel visas de två första raderna i CSV-filen som omvandlats till XDM, vilket visas i `CRM_profiles.json`:

```json
{
   "person": {
      "name": {
         "courtesyTitle": "Mr",
         "firstName": "Ewart",
         "lastName": "Bennedsen"
      },
      "gender": "male",
      "birthDayAndMonth": "09-25",
      "birthDate": "2004-09-25",
      "birthYear": 2004
   },
   "identityMap": {
      "CRMID": [{
         "id": "71a16013-d805-7ece-9ac4-8f2cd66e8eaa",
         "primary": false
      }],
      "ECID": [{
         "id": "87098882279810196101440938110216748923",
         "primary": false
      },
      {
         "id": "55019962992006103186215643814973128178",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e33192000007456-0365c00000000000",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "256-284-7231"
   },
   "personalEmail": {
      "address": "ebennedsenex@jiathis.com"
   },
   "homeAddress": {
      "street1": "72 Buhler Crossing",
      "city": "Anniston",
      "stateProvince": "Alabama",
      "country": "US",
      "postalCode": "36205",
      "_schema": {
         "latitude": 33.708276,
         "longitude": -85.7922905
      }
   }
},{
   "person": {
      "name": {
         "courtesyTitle": "Dr",
         "firstName": "Novelia",
         "lastName": "Ansteys"
      },
      "gender": "female",
      "birthDayAndMonth": "10-31",
      "birthDate": "1987-10-31",
      "birthYear": 1987
   },
   "identityMap": {
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
         "primary": false
      }],
      "ECID": [{
         "id": "50829196174854544323574004005273946998",
         "primary": false
      },
      {
         "id": "65233136134594262632703695260919939885",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "704-181-6371"
   },
   "personalEmail": {
      "address": "nansteysdk@spotify.com"
   },
   "homeAddress": {
      "street1": "79 Northfield Hill",
      "city": "Charlotte",
      "stateProvince": "North Carolina",
      "country": "US",
      "postalCode": "28299",
      "_schema": {
         "latitude": 35.2188655,
         "longitude": -80.8108888
      }
   }
}
```

## Dataframe till XDM-schema

Hierarkin för en databildruta (till exempel en Parquet-fil) måste matcha hierarkin för det XDM-schema som överförs till.

### Exempeldataram

Strukturen för följande exempeldatabildruta har mappats till ett schema som implementerar [!DNL XDM Individual Profile] klassen och innehåller de vanligaste fälten som är associerade med scheman av den typen.

```python
[
    StructField("person", StructType(
        [
            StructField("name", StructType(
                [
                    StructField("courtesyTitle", StringType()),
                    StructField("firstName", StringType()),
                    StructField("lastName", StringType())
                ]
            )),
            StructField("gender", StringType()),
            StructField("birthDayAndMonth", StringType()),
            StructField("birthDate", StringType()),
            StructField("birthYear", LongType())
        ]
    )),
    StructField("identityMap", MapType(
        StructField("CRMID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("ECID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("LOYALTYID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        ))
    )),
    StructField("homePhone", StructType(
        [
            StructField("number", StringType())
        ]
    )),
    StructField("personalEmail", StructType(
        [
            StructField("address", StringType())
        ]
    )),
    StructField("homeAddress", StructType(
        [
            StructField("street1", StringType()),
            StructField("city", StringType()),
            StructField("stateProvince", StringType()),
            StructField("country", StringType()),
            StructField("postalCode", StringType()),
            StructField("_schema", StructType(
                [
                    StructField("latitude", DoubleType()),
                    StructField("latitude", DoubleType()),
                ]
            ))
        ]
    ))    
]
```

När du konstruerar en databildruta för användning i Adobe Experience Platform är det viktigt att se till att dess hierarkiska struktur är exakt densamma som i ett befintligt XDM-schema för att fälten ska kunna mappas korrekt.

## Identiteter till identitetskarta

### Array med identiteter

```json
[
  {
    "xdm:id": "someone1@example.com",
    "xdm:namespace": {
      "xdm:code": "Email"
    }
  },
  {
    "xdm:id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
    "xdm:namespace": {
      "xdm:code": "CRMID"
    }
  },
  {
    "xdm:id": "2e3319208000765b-3811c00000000001",
    "xdm:namespace": {
      "xdm:code": "LOYALTYID"
    }
  }
]
```

### Mappning

Mappningskraven för arrayen med identiteter beskrivs i följande tabell:

| Identitetsfält | identityMap-fält | Datatyper |
| -------------- | ----------------- | --------- |
| identiteter[0].id | [identityMapEmail][{"id"}] | kopiera som sträng |
| identiteter[1].id | [identityMapCRMID][{"id"}] | kopiera som sträng |
| identities[2].id | [identityMapLOYALTYID][{"id"}] | kopiera som sträng |

### Utdata-XDM

Nedan visas arrayen med identiteter som omvandlats till XDM:

```JSON
"identityMap": {
      "Email": [{
         "id": "someone1@example.com"
      }],
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5"
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001"
      }]
   }
```

