---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;miljö;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Miljödatatyp
description: Läs mer om datatypen Environment XDM.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# [!UICONTROL Environment] datatyp

[!UICONTROL Environment] är en standard-XDM-datatyp som beskriver den omgivande miljön för en observerad händelse, som särskilt beskriver tillfällig information som nätverks- och programversioner.

>[!IMPORTANT]
>
>Alla värden ska justeras mot [DeviceAtlas](https://deviceatlas.com) databas, licensierad av Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_dc` | Objekt | Ett objekt som innehåller ett enda fält, `language`, som anger vilket språk som används i miljön för att representera användarens språkliga, geografiska eller kulturella preferenser för datapresentation. Språk anges i språkkoden enligt definitionen i [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Webbläsarinformation](./browser-details.md) | Beskriver den webbläsarspecifika informationen om miljön, till exempel webbläsarnamn, version, JavaScript-version, användaragentsträng och språk. |
| `ISP` | Sträng | Namnet på användarens internetleverantör. |
| `carrier` | Sträng | Namnet på mobilnätets operatör eller MNO (även kallat trådlös tjänsteleverantör, trådlös operatör, mobilföretag eller mobilnätsoperatör) som säljer och levererar kommunikationstjänster till användaren. |
| `colorDepth` | Heltal | Antalet bitar som används för varje färgkomponent i en enda pixel. |
| `connectionType` | Sträng | Internetanslutningstypen. Godkända värden är: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Sträng | Domänen för användarens Internet-leverantör. |
| `ipV4` | Sträng | Den numeriska etikett som tilldelats en enhet som deltar i ett datornätverk som använder Internet Protocol för kommunikation (32-bitars). |
| `ipV6` | Sträng | Den numeriska etikett som tilldelats en enhet som deltar i ett datornätverk som använder Internet Protocol för kommunikation (128-bitars). |
| `operatingSystem` | Sträng | Namnet på det operativsystem som användes när observationen gjordes. Attributet får inte innehålla versionsinformation som `10.5.3`, men innehåller i stället&quot;edition&quot;, som `Ultimate` eller `Professional`. |
| `operatingSystemVendor` | Sträng | Namnet på operativsystemets leverantör som användes när observationen gjordes. |
| `operatingSystemVersion` | Sträng | Den fullständiga versionsidentifieraren för det operativsystem som användes när observationen gjordes. Versioner är vanligtvis numeriskt sammansatta men kan vara i ett leverantörsdefinierat format. |
| `type` | Sträng | Typ av programmiljö. Se [appendix](#type) för godkända värden. |
| `viewportHeight` | Heltal | Den lodräta storleken i pixlar på fönstret som upplevelsen visades inuti. För en webbvyhändelse är detta höjden på webbläsarens visningsruta. |
| `viewPortWidth` | Heltal | Den vågräta storleken i pixlar på fönstret som upplevelsen visades inuti. För en webbvyhändelse är detta bredden på webbläsarens visningsruta. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Bilaga

Följande avsnitt innehåller ytterligare information om [!UICONTROL Device] datatyp.

## Godkända värden för typ {#type}

I följande tabell visas godkända värden för `type` och deras innebörd:

| Värde | Beskrivning |
| --- | --- |
| `browser` | Webbläsare |
| `application` | Program |
| `iot` | Sakernas internet |
| `external` | Externt system |
| `widget` | Programtillägg |
