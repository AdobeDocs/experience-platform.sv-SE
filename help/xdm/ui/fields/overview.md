---
keywords: Experience Platform;home;populära topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field;
solution: Experience Platform
title: Definiera XDM-fält i användargränssnittet
description: Lär dig definiera XDM-fält i Experience Platform användargränssnitt.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 1%

---

# Definiera XDM-fält i användargränssnittet

Med [!DNL Schema Editor] i Adobe Experience Platform användargränssnitt kan du definiera egna fält i anpassade XDM-klasser (Experience Data Model) och schemafältgrupper. Den här guiden beskriver stegen för att definiera XDM-fält i användargränssnittet, inklusive tillgängliga konfigurationsalternativ för varje fälttyp.

## Förhandskrav

Handboken kräver en fungerande förståelse för XDM System. Se [XDM-översikten](../../home.md) för en introduktion till XDM-rollen i Experience Platform-ekosystemet och [grunderna i schemakomposition](../../schema/composition.md) för att lära dig hur klasser och fältgrupper bidrar till fält i XDM-scheman.

Även om det inte krävs för den här guiden rekommenderar vi att du också följer självstudiekursen om att [komponera ett schema i användargränssnittet](../../tutorials/create-schema-ui.md) för att bekanta dig med de olika funktionerna i [!DNL Schema Editor].

## Välj en resurs att lägga till fält i {#select-resource}

Om du vill definiera nya XDM-fält i användargränssnittet måste du först öppna ett schema i [!DNL Schema Editor]. Beroende på vilka scheman som är tillgängliga för dig i [!DNL Schema Library] kan du välja att [skapa ett nytt schema](../resources/schemas.md#create) eller [välja ett befintligt schema att redigera](../resources/schemas.md#edit).

När du har [!DNL Schema Editor] öppet visas kontroller för att lägga till fält på arbetsytan. Dessa kontroller visas intill schemats namn, liksom alla objekttypsfält som har definierats under den valda klassen eller fältgruppen.

![Schemaredigeraren med tilläggsikonerna markerade.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Om du försöker lägga till ett fält i ett objekt som tillhandahålls av en standardfältgrupp, kommer den fältgruppen att konverteras till en anpassad fältgrupp och den ursprungliga fältgruppen kommer inte längre att vara tillgänglig. Mer information finns i avsnittet [om att lägga till fält i standardfältgrupper](../resources/schemas.md#custom-fields-for-standard-groups) i gränssnittshandboken för scheman.

Om du vill lägga till ett nytt fält i resursen väljer du ikonen **plus (+)** bredvid schemats namn på arbetsytan eller bredvid det objekttypsfält som du vill definiera fältet under.

![Schemaredigeraren med en Lägg till-ikon markerad.](../../images/ui/fields/overview/plus-icon.png)

Beroende på om du lägger till ett fält direkt i ett schema eller dess klass och fältgrupper för beståndsdelar, varierar stegen som krävs för att lägga till fältet. Resten av det här dokumentet fokuserar på hur du konfigurerar ett fälts egenskaper oavsett var det fältet visas i schemat. Mer information om olika sätt att lägga till fält i ett schema finns i följande avsnitt i gränssnittshandboken för scheman:

* [Lägg till fält i fältgrupper](../resources/schemas.md#add-fields)
* [Lägga till fält direkt i ett schema](../resources/schemas.md#add-individual-fields)

## Definiera egenskaperna för ett fält {#define}

När du har valt ikonen **plus (+)** visas en **[!UICONTROL Untitled field]** platshållare på arbetsytan.

![Schemaredigeraren med ett nytt namnlöst fält markerat.](../../images/ui/fields/overview/new-field.png)

I den högra listen under **[!UICONTROL Field properties]** kan du konfigurera informationen för det nya fältet. Följande information krävs för varje fält:

| Fältegenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Field name] | Ett unikt, beskrivande namn för fältet. Observera att fältets namn inte kan ändras när schemat har sparats. Det här värdet används för att identifiera och referera till fältet i koden och i andra efterföljande program<br><br>Namnet bör helst skrivas i camelCase. Det kan innehålla alfanumeriska tecken eller understreck, men **får inte** börja med ett understreck.<ul><li>**Korrigera**: `fieldName`</li><li>**Godtagbart:** `field_name2`, `fieldName_3`</li><li>**Felaktigt**: `_fieldName`</li></ul> |
| [!UICONTROL Display name] | Ett visningsnamn för fältet. Det här namnet kommer att användas för att representera fältet på arbetsytan i Schemaredigeraren. Fältnamnet kan ändras till visningsnamnet med [växlingsknappen för visningsnamn](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Type] | Den typ av data som fältet innehåller. I den här listrutan kan du välja en av de [standardskalärtyper](../../schema/field-constraints.md) som stöds av XDM, eller en av de [datatyper ](../resources/data-types.md) för flera fält som tidigare definierats i [!DNL Schema Registry] .<br>Obs! Om du väljer datatypen Map visas egenskapen [!UICONTROL Map value type] .<br><br>Du kan också välja **[!UICONTROL Advanced type search]** om du vill söka efter och filtrera befintliga datatyper och hitta den önskade typen enklare. |
| [!UICONTROL Map value type] | Det här värdet är obligatoriskt om du väljer [!UICONTROL Map] som datatyp för fältet. Tillgängliga värden för kartan är [!UICONTROL String] och [!UICONTROL Integer]. Välj ett värde i listrutan med tillgängliga alternativ.<br>Mer information om [typspecifika fältegenskaper](#type-specific-properties) finns i översikten över definierade fält. |

{style="table-layout:auto"}

Du kan också välja att ange en beskrivning och anteckningar för varje fält. Använd fältet **[!UICONTROL Description]** för att lägga till kontext och beskriva funktionerna för mappningsdatatypen. Detta bidrar till att implementeringen blir enkel och lättläst. Du kan också lägga till anteckningar som komplement till den inledande beskrivningen. Detta bör ge mer detaljerad och specifik information för att hjälpa utvecklare att förstå, underhålla och använda kartan effektivt i kodbasen. |


>[!NOTE]
>
>Beroende på vilken **[!UICONTROL Type]** du har valt för fältet kan ytterligare konfigurationskontroller visas i den högra listen. Mer information om de här kontrollerna finns i avsnittet [typspecifika fältegenskaper](#type-specific-properties).
>
>Den högra listen innehåller även kryssrutor för att ange särskilda fälttyper. Mer information finns i avsnittet om [särskilda fälttyper](#special).

När du har konfigurerat fältet väljer du **[!UICONTROL Apply]**.

![Avsnittet [!UICONTROL Field properties] i Schemaredigeraren är markerat.](../../images/ui/fields/overview/field-details.png)

Arbetsytan uppdateras för att visa det nya fältet, som finns i ett objekt som har ett namn som är kopplat till ditt unika klientorganisations-ID (visas som `_tenantId` i exemplet nedan). Alla anpassade fält som läggs till i ett schema placeras automatiskt i det här namnutrymmet för att förhindra konflikter med andra fält från klasser och fältgrupper som tillhandahålls av Adobe. Den högra listen visar nu fältets sökväg förutom dess andra egenskaper.

![Ett nytt fält i schemagrafiken och dess motsvarande sökväg i avsnittet [!UICONTROL Field properties] markeras.](../../images/ui/fields/overview/field-added.png)

Du kan fortsätta följa stegen ovan för att lägga till fler fält i schemat. När schemat har sparats sparas även dess basklass och fältgrupper om några ändringar har gjorts i dem.

>[!NOTE]
>
>Alla ändringar du gör i fältgrupperna eller klassen för ett schema kommer att återspeglas i alla andra scheman som använder dem.

## Typspecifika fältegenskaper {#type-specific-properties}

När du definierar ett nytt fält kan ytterligare konfigurationsalternativ visas i den högra listen beroende på vilken **[!UICONTROL Type]** du väljer för fältet. I följande tabell visas de här extra fältegenskaperna tillsammans med deras kompatibla typer:

| Fältegenskap | Kompatibla typer | Beskrivning |
| --- | --- | --- |
| [!UICONTROL Map value type] | [!UICONTROL Map] | Egenskapen [!UICONTROL Map value type] visas bara i användargränssnittet om du väljer värdet för Karta bland alternativen i listrutan [!UICONTROL Type]. Du kan välja mellan värdetyperna String och Integer för kartan.<br>![Schemaredigeraren med fälten för typ och kartvärdestyp markerade.](../../images/ui/fields/overview/map-type.png "Schemaredigeraren med fälten för typ och mappningsvärdestyp markerade."){width="100" zoomable="yes"}<br>Obs! Alla mappningsdatatyper som skapas via API som inte är antingen en sträng eller en heltalstyp visas som datatypen [!UICONTROL Complex]. Du kan inte skapa datatyperna [!UICONTROL Complex] via användargränssnittet. |
| [!UICONTROL Pattern] | [!UICONTROL String] | Ett [reguljärt uttryck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) som värdet för det här fältet måste uppfylla för att accepteras vid förtäring. |
| [!UICONTROL Format] | [!UICONTROL String] | Välj i en lista över fördefinierade format för strängar som värdet måste överensstämma med. Tillgängliga format: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Minimum length] | [!UICONTROL String] | Det minsta antal tecken som strängen måste innehålla för att värdet ska accepteras vid förtäring. |
| [!UICONTROL Maximum length] | [!UICONTROL String] | Det maximala antal tecken som strängen måste innehålla för att värdet ska accepteras vid förtäring. |
| [!UICONTROL Minimum value] | [!UICONTROL Double] | Det lägsta värdet för Double som ska accepteras vid förtäring. Om det inmatade värdet exakt matchar det som anges här, accepteras värdet. När du använder den här begränsningen måste [!UICONTROL Exclusive minimum value] lämnas tom. |
| [!UICONTROL Maximum value] | [!UICONTROL Double] | Det högsta värdet för Double som ska accepteras vid förtäring. Om det inmatade värdet exakt matchar det som anges här, accepteras värdet. När du använder den här begränsningen måste [!UICONTROL Exclusive maximum value] lämnas tom. |
| [!UICONTROL Exclusive minimum value] | [!UICONTROL Double] | Det högsta värdet för Double som ska accepteras vid förtäring. Om det inmatade värdet exakt matchar det som anges här, avvisas värdet. När den här begränsningen används måste [!UICONTROL Minimum value]-begränsningen (icke-exklusiv) lämnas tom. |
| [!UICONTROL Exclusive maximum value] | [!UICONTROL Double] | Det högsta värdet för Double som ska accepteras vid förtäring. Om det inmatade värdet exakt matchar det som anges här, avvisas värdet. När den här begränsningen används måste [!UICONTROL Maximum value]-begränsningen (icke-exklusiv) lämnas tom. |

{style="table-layout:auto"}

## Speciella fälttyper {#special}

Den högra listen innehåller flera kryssrutor för att ange speciella roller för det markerade fältet. Användningsexempel för vissa av dessa alternativ inbegriper viktiga överväganden som rör er datamodelleringsstrategi och hur ni tänker använda Experience Platform-tjänster längre fram i kedjan.

Mer information om dessa specialtyper finns i följande dokumentation:

* [Karta](./map.md)
* [[!UICONTROL Required]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) (endast tillgängligt för strängfält)
* [[!UICONTROL Relationship]](./relationship.md) (endast tillgängligt för strängfält)

Även om det inte är en speciell fälttyp rekommenderar vi att du går till guiden [definierar objekttypsfält](./object.md) för att lära dig mer om hur du definierar kapslade underfält om schemastrukturen används.

## Nästa steg

Den här guiden ger en översikt över hur du definierar XDM-fält i användargränssnittet. Kom ihåg att fält bara kan läggas till i scheman med hjälp av klasser och fältgrupper. Mer information om hur du hanterar de här resurserna i användargränssnittet finns i handböckerna om hur du skapar och redigerar [klasser](../resources/classes.md) och [fältgrupper](../resources/field-groups.md).

Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] finns i översikten för arbetsytan [[!UICONTROL Schemas] ](../overview.md).
