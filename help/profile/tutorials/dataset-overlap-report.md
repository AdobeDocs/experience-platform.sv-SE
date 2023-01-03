---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;rapportering;dataset overlap report;profildata
title: Generera överlappningsrapport för datauppsättning
type: Tutorial
description: I den här självstudien beskrivs de steg som krävs för att generera överlappningsrapporten för datauppsättningen med hjälp av kundprofils-API:t i realtid.
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# Generera överlappningsrapport för datauppsättning

Rapporten om överlappning av datauppsättningar ger synlighet i sammansättningen av organisationens [!DNL Profile] lagra genom att visa de datauppsättningar som bidrar mest till den adresserbara målgruppen (profiler).

Förutom att ge insikter om era data kan den här rapporten hjälpa er att vidta åtgärder för att optimera er licensanvändning, som att sätta en gräns för vissa data.

I den här självstudien beskrivs de steg som krävs för att generera överlappningsrapporten för datauppsättningen med hjälp av [!DNL Real-Time Customer Profile] API och tolka resultaten för er organisation.

## Komma igång

För att kunna använda Adobe Experience Platform API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att samla in de värden du behöver för de önskade rubrikerna. Mer information om Experience Platform API:er finns i [komma igång med dokumentation för plattforms-API:er](../../landing/api-guide.md).

Nödvändiga rubriker för alla API-anrop i den här självstudiekursen är:

* `Authorization: Bearer {ACCESS_TOKEN}`: The `Authorization` header kräver en åtkomsttoken som föregås av ordet `Bearer`. Ett nytt åtkomsttokenvärde måste genereras var 24:e timme.
* `x-api-key: {API_KEY}`: The `API Key` kallas också `Client ID` och är ett värde som bara behöver genereras en gång.
* `x-gw-ims-org-id: {ORG_ID}`: The `IMS Org` kallas även `Organization ID` och behöver bara genereras en gång.

När du har slutfört självstudiekursen för autentisering och samlat in värden för de huvuden som behövs kan du börja ringa anrop till Real-Time Customer API.

## Generera överlappningsrapport för datauppsättning med kommandoraden

Om du är van vid att använda kommandoraden kan du använda följande cURL-begäran för att generera överlappningsrapporten för datauppsättningen genom att utföra en GET-begäran på `/previewsamplestatus/report/dataset/overlap`.

**Begäran**

Följande begäran använder `date` parameter för att returnera den senaste rapporten för det angivna datumet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett HTTP-statusfel 404 (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

**Svar**

En lyckad begäran returnerar HTTP-status 200 (OK) och datasetet överlappar rapporten. Rapporten innehåller en `data` -objekt, som innehåller kommaavgränsade listor med datauppsättningar och deras respektive profilantal. Mer information om hur du läser rapporten finns i avsnittet om [tolka data för dataset som överlappar rapportdata](#interpret-the-report) senare i den här självstudiekursen.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Generera överlappningsrapport för datauppsättning med Postman

Postman är en samarbetsplattform för API-utveckling och är användbart för att visualisera API-anrop. Den kan laddas ned kostnadsfritt från [Postman webbplats](https://www.postman.com) och erbjuder ett användargränssnitt som är enkelt att använda för att utföra API-anrop. Följande skärmbilder använder Postman gränssnitt.

**Begäran**

Om du vill begära en överlappande datauppsättningsrapport med Postman utför du följande steg:

* Använd listrutan och välj GET som begärandetyp.
* Ange önskade rubriker i dialogrutan `KEY` kolumn:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Ange de värden du genererade under autentiseringen i dialogrutan `VALUE` kolumn, ersätta klammerparenteser (`{{ }}`) och allt innehåll inom klammerparenteserna.
* Ange sökvägen till begäran med eller utan den valfria `date` parameter:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   eller
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett HTTP-statusfel 404 (Hittades inte). Om inget datum anges returneras den senaste rapporten. <br/>Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

När begärandetypen, rubrikerna, värdena och sökvägen är klara väljer du **Skicka** för att skicka API-begäran och generera rapporten.

![](../images/dataset-overlap-report/postman-request.png)

**Svar**

En lyckad begäran returnerar HTTP-status 200 (OK) och datasetet överlappar rapporten. Rapporten innehåller en `data` -objekt, som innehåller kommaavgränsade listor med datauppsättningar och deras respektive profilantal. Mer information om hur du läser rapporten finns i avsnittet om [tolka data för dataset som överlappar rapportdata](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Tolka rapportdata som överlappar datamängden {#interpret-the-report}

Den genererade överlappningsrapporten för datauppsättningar innehåller en tidsstämpel som visar rapportens datum och tid och ett dataobjekt som innehåller unika kombinationer av datauppsättnings-ID:n som kommaseparerade listor. I följande avsnitt finns ytterligare information om rapportens komponenter.

### Rapporttidsstämpel

The `reportTimestamp` matchar datumet som anges i API-begäran, eller, om inget datum anges, tidsstämpeln för den senaste rapporten.

### Lista över datauppsättnings-ID:n

The `data` -objektet innehåller unika kombinationer av datauppsättnings-ID:n som kommaavgränsade listor med respektive profilantal för den kombinationen av datauppsättningar.

>[!NOTE]
>
>Summan av alla profilantal som är associerade med varje rad i dataset överlappningsrapport ska vara lika med det totala antalet profiler i organisationen.

Ta följande exempel för att tolka rapportens resultat:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Den här rapporten innehåller följande information:

* Det finns 123 profiler med data från följande datauppsättningar: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Det finns 454 412 profiler som består av data från dessa två datauppsättningar: `5d92921872831c163452edc8` och `5eb2cdc6fa3f9a18a7592a98`.
* Det finns 107 profiler som endast består av data från datauppsättningen `5eeda0032af7bb19162172a7`.
* Det finns totalt 454 642 profiler i organisationen.

## Nästa steg

När du är klar med den här självstudiekursen kan du nu generera en överlappande datauppsättningsrapport med hjälp av kundprofils-API:t i realtid. Om du vill veta mer om hur du arbetar med profildata i både API:t och användargränssnittet i Experience Platform börjar du med att läsa [Profilöversikt - dokumentation](../home.md).
