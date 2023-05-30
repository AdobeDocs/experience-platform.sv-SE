---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field;
solution: Experience Platform
title: Definiera XDM-fält i användargränssnittet
description: Lär dig hur du definierar XDM-fält i användargränssnittet för Experience Platform.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 765079f084dce316d321fbac5aee9e387373ba00
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 2%

---

# Definiera XDM-fält i användargränssnittet

The [!DNL Schema Editor] i Adobe Experience Platform användargränssnitt kan du definiera egna fält i anpassade Experience Data Model-klasser (XDM) och schemafältgrupper. Den här guiden beskriver stegen för att definiera XDM-fält i användargränssnittet, inklusive tillgängliga konfigurationsalternativ för varje fälttyp.

## Förutsättningar

Handboken kräver en fungerande förståelse för XDM System. Se [XDM - översikt](../../home.md) en introduktion till XDM:s roll i Experience Platform-ekosystemet, och [grunderna för schemakomposition](../../schema/composition.md) om du vill lära dig hur klasser och fältgrupper bidrar till fält i XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen på [skapa ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Välj en resurs att lägga till fält i {#select-resource}

Om du vill definiera nya XDM-fält i användargränssnittet måste du först öppna ett schema i [!DNL Schema Editor]. Beroende på vilka scheman som är tillgängliga för dig i [!DNL Schema Library]kan du välja att [skapa ett nytt schema](../resources/schemas.md#create) eller [välj ett befintligt schema att redigera](../resources/schemas.md#edit).

När du har [!DNL Schema Editor] öppna visas kontroller för att lägga till fält på arbetsytan. Dessa kontroller visas intill schemats namn, liksom alla objekttypsfält som har definierats under den valda klassen eller fältgruppen.

![](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Om du försöker lägga till ett fält i ett objekt som tillhandahålls av en standardfältgrupp, kommer den fältgruppen att konverteras till en anpassad fältgrupp och den ursprungliga fältgruppen kommer inte längre att vara tillgänglig. Se avsnittet om [lägga till fält i standardfältgrupper](../resources/schemas.md#custom-fields-for-standard-groups) i gränssnittshandboken för scheman för mer information.

Om du vill lägga till ett nytt fält i resursen väljer du **plus (+)** -ikonen bredvid schemats namn på arbetsytan eller bredvid det objekttypsfält som du vill definiera fältet under.

![](../../images/ui/fields/overview/plus-icon.png)

Beroende på om du lägger till ett fält direkt i ett schema eller dess klass och fältgrupper för beståndsdelar, varierar stegen som krävs för att lägga till fältet. Resten av det här dokumentet fokuserar på hur du konfigurerar ett fälts egenskaper oavsett var det fältet visas i schemat. Mer information om olika sätt att lägga till fält i ett schema finns i följande avsnitt i gränssnittshandboken för scheman:

* [Lägg till fält i fältgrupper](../resources/schemas.md#add-fields)
* [Lägga till fält direkt i ett schema](../resources/schemas.md#add-individual-fields)

## Definiera egenskaperna för ett fält {#define}

När du har valt **plus (+)** ikon, en **[!UICONTROL Untitled field]** platshållaren visas på arbetsytan.

![](../../images/ui/fields/overview/new-field.png)

I den högra listen under **[!UICONTROL Field properties]** kan du konfigurera informationen för det nya fältet. Följande information krävs för varje fält:

| Fältegenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Field name] | Ett unikt, beskrivande namn för fältet. Observera att fältets namn inte kan ändras när schemat har sparats. Det här värdet används för att identifiera och referera till fältet i koden och i andra program längre fram i kedjan<br><br>Namnet ska helst skrivas i camelCase. Den kan innehålla alfanumeriska tecken, bindestreck eller understreck, men den **får inte** börja med ett understreck.<ul><li>**Korrigera**: `fieldName`</li><li>**Godtagbart:** `field_name2`, `Field-Name`, `field-name_3`</li><li>**Felaktig**: `_fieldName`</li></ul> |
| [!UICONTROL Display name] | Ett visningsnamn för fältet. Det här namnet kommer att användas för att representera fältet på arbetsytan i Schemaredigeraren. Fältnamnet kan ändras till visningsnamnet med [växla visningsnamn](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Type] | Den typ av data som fältet innehåller. I den här listrutan kan du välja något av [standardtyper av skalärbilder](../../schema/field-constraints.md) stöds av XDM, eller ett av flera fält [datatyper](../resources/data-types.md) som tidigare har definierats i [!DNL Schema Registry].<br><br>Du kan också välja **[!UICONTROL Advanced type search]** om du vill söka efter och filtrera befintliga datatyper och hitta den önskade typen enklare. |

{style="table-layout:auto"}

Du kan även tillhandahålla ett tillval som är läsbart för människor **[!UICONTROL Description]** till fältet för att ge mer kontext till fältets avsedda användningsfall.

>[!NOTE]
>
>Beroende på **[!UICONTROL Type]** som du har valt för fältet kan ytterligare konfigurationskontroller visas i den högra listen. Se avsnittet om [typspecifika fältegenskaper](#type-specific-properties) för mer information om dessa kontroller.
>
>Den högra listen innehåller även kryssrutor för att ange särskilda fälttyper. Se avsnittet om [specialfälttyper](#special) för mer information.

När du har konfigurerat fältet väljer du **[!UICONTROL Apply]**.

![](../../images/ui/fields/overview/field-details.png)

Arbetsytan uppdateras för att visa det nya fältet, som finns i ett objekt som har ett namn som är kopplat till ditt unika innehavar-ID (visas som `_tenantId` i exemplet nedan). Alla anpassade fält som läggs till i ett schema placeras automatiskt i det här namnutrymmet för att förhindra konflikter med andra fält från klasser och fältgrupper som tillhandahålls av Adobe. Den högra listen visar nu fältets sökväg förutom dess andra egenskaper.

![](../../images/ui/fields/overview/field-added.png)

Du kan fortsätta följa stegen ovan för att lägga till fler fält i schemat. När schemat har sparats sparas även dess basklass och fältgrupper om några ändringar har gjorts i dem.

>[!NOTE]
>
>Alla ändringar du gör i fältgrupperna eller klassen för ett schema kommer att återspeglas i alla andra scheman som använder dem.

## Typspecifika fältegenskaper {#type-specific-properties}

När du definierar ett nytt fält kan ytterligare konfigurationsalternativ visas i den högra listen beroende på **[!UICONTROL Type]** du väljer för fältet. I följande tabell visas de här extra fältegenskaperna tillsammans med deras kompatibla typer:

| Fältegenskap | Kompatibla typer | Beskrivning |
| --- | --- | --- |
| [!UICONTROL Default value] | [!UICONTROL String], [!UICONTROL Double], [!UICONTROL Long], [!UICONTROL Integer], [!UICONTROL Short], [!UICONTROL Byte], [!UICONTROL Boolean] | Ett standardvärde som tilldelas det här fältet om inget annat värde anges vid inmatningen. Värdet måste överensstämma med fältets valda typ.<br><br>Standardvärdena sparas inte i datauppsättningen vid tidpunkten för inmatningen eftersom de kan ändras över tid. De standardvärden som anges i schemat härleds av plattformstjänster och program som är längre fram i kedjan när de läser data från datauppsättningen. Om attributet har ett NULL-värde när data efterfrågas med hjälp av tjänsten Query, men standardvärdet är inställt på `5` på schemanivå förväntas frågetjänsten returnera `5` i stället för NULL. Observera att detta för närvarande inte är enhetligt i alla AEP-tjänster. |
| [!UICONTROL Pattern] | [!UICONTROL String] | A [reguljärt uttryck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) att värdet för detta fält måste överensstämma med för att kunna accepteras vid förtäring. |
| [!UICONTROL Format] | [!UICONTROL String] | Välj i en lista över fördefinierade format för strängar som värdet måste överensstämma med. Tillgängliga format: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Minimum length] | [!UICONTROL String] | Det minsta antalet tecken som strängen måste innehålla för att värdet ska accepteras vid förtäring. |
| [!UICONTROL Maximum length] | [!UICONTROL String] | Det maximala antal tecken som strängen måste innehålla för att värdet ska accepteras vid förtäring. |
| [!UICONTROL Minimum value] | [!UICONTROL Double] | Det lägsta värdet för Double som ska accepteras vid förtäring. Om det inmatade värdet exakt matchar det som anges här, accepteras värdet. När du använder den här begränsningen visas[!UICONTROL Exclusive minimum value]-begränsningen måste lämnas tom. |
| [!UICONTROL Maximum value] | [!UICONTROL Double] | Det högsta värdet för Double som ska accepteras vid intag. Om det inmatade värdet exakt matchar det som anges här, accepteras värdet. När du använder den här begränsningen visas[!UICONTROL Exclusive maximum value]-begränsningen måste lämnas tom. |
| [!UICONTROL Exclusive minimum value] | [!UICONTROL Double] | Det högsta värdet för Double som ska accepteras vid intag. Om det inmatade värdet exakt matchar det som anges här, avvisas värdet. När du använder den här begränsningen visas[!UICONTROL Minimum value]&quot; (icke-exklusiv) begränsning måste lämnas tom. |
| [!UICONTROL Exclusive maximum value] | [!UICONTROL Double] | Det högsta värdet för Double som ska accepteras vid intag. Om det inmatade värdet exakt matchar det som anges här, avvisas värdet. När du använder den här begränsningen visas[!UICONTROL Maximum value]&quot; (icke-exklusiv) begränsning måste lämnas tom. |

{style="table-layout:auto"}

## Speciella fälttyper {#special}

Den högra listen innehåller flera kryssrutor för att ange speciella roller för det markerade fältet. Användningsexempel för vissa av dessa alternativ inbegriper viktiga överväganden som rör er datamodelleringsstrategi och hur ni tänker använda plattformstjänster längre fram i kedjan.

Mer information om dessa specialtyper finns i följande dokumentation:

* [[!UICONTROL Required]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) (Endast tillgängligt för strängfält)
* [[!UICONTROL Relationship]](./relationship.md) (Endast tillgängligt för strängfält)

Även om det inte är en speciell fälttyp rekommenderar vi att du går till guiden på [definiera objekttypsfält](./object.md) om du vill veta mer om hur du definierar kapslade underfält om schemastrukturen.

## Nästa steg

Den här guiden ger en översikt över hur du definierar XDM-fält i användargränssnittet. Kom ihåg att fält bara kan läggas till i scheman med hjälp av klasser och fältgrupper. Om du vill veta mer om hur du hanterar de här resurserna i användargränssnittet läser du i handböckerna om hur du skapar och redigerar [klasser](../resources/classes.md) och [fältgrupper](../resources/field-groups.md).

Mer information om funktionerna i [!UICONTROL Schemas] arbetsytan, se [[!UICONTROL Schemas] arbetsyta - översikt](../overview.md).
