---
keywords: Experience Platform;profil;kundprofil i realtid;enhetlig profil;Enhetlig profil;Enhetlig;Profil;rtcp;aktivera profil;Aktivera profil;Unionsschema;UNIONSPROFIL;Unionsprofil
title: Användargränssnittshandbok för unionsschema
type: Documentation
description: I Adobe Experience Platform användargränssnitt kan du enkelt visa vilket unionsschema som helst i organisationen och förhandsgranska fält, identiteter, relationer och bidragande scheman för en viss klass. Den här guiden innehåller detaljerad information om hur du visar och utforskar fackliga scheman med hjälp av Experience Platform användargränssnitt.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: b7f5f08d5b3632a2d80c39559a5fb5116d9567f8
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 0%

---

# Användargränssnittshandbok för [!UICONTROL Union schema]

I Adobe Experience Platform användargränssnitt kan du enkelt visa vilket unionsschema som helst i organisationen och förhandsgranska fält, identiteter, relationer och bidragande scheman för en viss klass. Den här guiden innehåller detaljerad information om hur du visar och utforskar fackliga scheman med hjälp av Experience Platform användargränssnitt.

## Komma igång {#getting-started}

Den här gränssnittshandboken kräver förståelse av de olika [!DNL Experience Platform]-tjänsterna som används för att hantera kundprofildata i realtid. Innan du läser den här handboken eller arbetar i användargränssnittet bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-Time Customer Profile]](../home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Identity Service]](../../identity-service/home.md): Aktiverar [!DNL Real-Time Customer Profile] genom att brygga identiteter från olika datakällor när de hämtas till [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

## Förstå fackscheman {#understanding-union-schemas}

>[!CONTEXTUALHELP]
>id="rtcdp_collaboration_union_schema"
>title="Unionens system"
>abstract=""

<!-- The above contextual help is used in the Collaboration UI for a read more link. -->

Med kundprofilen i realtid kan ni skapa robusta, centraliserade profiler med kundattribut och tidsstämplade händelser för varje kundinteraktion i alla system som är integrerade med Adobe Experience Platform. Format och struktur för dessa data tillhandahålls av XDM-scheman (Experience Data Model), där varje schema baseras på en XDM-klass och innehåller fält som är kompatibla med den klassen.

Du kan skapa scheman för flera användningsfall, som refererar till samma klass men som innehåller fält som är specifika för deras användning. När ett schema aktiveras för profilen blir det en del av ett unionsschema. Unionsscheman består med andra ord av flera scheman som delar samma klass och har aktiverats för profilen. Med unionsschemat kan du se en sammanslagning av alla fält i scheman som delar samma klass. Kundprofilen i realtid använder unionsschemat för att skapa en helhetsbild av varje enskild kund.

Att arbeta med fackliga scheman kräver en djupgående förståelse av XDM-scheman. Om du vill ha mer information börjar du med att läsa [grunderna för schemakomposition](../../xdm/schema/composition.md).

## Visa unionskartor {#view-union-schemas}

Om du vill navigera till unionsscheman i Experience Platform-användargränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen och sedan fliken **[!UICONTROL Union Schema]**. Fliken [!UICONTROL Union Schema] öppnas och visar unionsschemat för den valda klassen.

![Sidan Unionens schema visas med fliken Profil och Unionsschema markerad.](../images/union-schema/landing.png)

## Välj en klass {#select-a-class}

Om du vill visa unionsschemat för en viss XDM-klass väljer du klassen i listrutan **[!UICONTROL Class]**. På grund av att inte alla klasser har union-scheman är bara klasser med union-scheman (dvs. klasser med scheman som har aktiverats för profil) tillgängliga i listrutan.

När en klass har valts uppdateras det schema som visas så att det återspeglar unionsschemat för den valda klassen. Du kan till exempel välja **[!UICONTROL XDM Individual Profile]** för att visa föreningsschemat för den klassen.

![En listruta som innehåller klasserna i unionsschemat är markerad.](../images/union-schema/class.png)

## Utforska fackscheman {#explore-union-schemas}

Du kan utforska unionsschemat genom att rulla uppåt och nedåt för att visa den fullständiga schemastrukturen och genom att välja en höger vinkelparentes (`>`) för att expandera kapslade fält.

![En uppsättning kapslade fält i unionsschemat har utökats.](../images/union-schema/explore.png)

Markera ett fält om du vill visa information om det, inklusive visningsnamn, datatyp, beskrivning, sökväg, datum när det skapades och senaste ändringsdatum. Du kan även visa en lista med medverkande scheman som innehåller det fält du har markerat.

![Ett unionsschemafält är markerat. Information om det markerade fältet visas på höger sidofält.](../images/union-schema/explore-field.png)

När du väljer namnet på ett bidragsgivande schema visas namnen på de datauppsättningar som är relaterade till det schemat som samlar in data i det valda fältet. Varje datauppsättningsnamn visas som en länk. Om du väljer ett datauppsättningsnamn öppnas aktivitetsfliken för den datauppsättningen i ett nytt fönster.

Mer information om datauppsättningar, inklusive hur du visar datauppsättningsaktivitet och förhandsgranskar datauppsättningsdata i användargränssnittet, finns i [gränssnittsguiden för datauppsättningar](../../catalog/datasets/user-guide.md).

![Listan med datauppsättningar relaterade till schemat är markerad.](../images/union-schema/datasets.png)

## Visa bidragande scheman {#view-contributing-schemas}

Du kan också visa vilka specifika scheman som bidrar till unionsschemat genom att välja **[!UICONTROL All contributing schemas]** för att expandera listan med scheman. Beroende på vilken klass du har valt och hur många scheman din organisation har skapat inom Experience Platform kan det vara en kort lista som innehåller ett enda schema eller en lång lista med många scheman.

![Listan med scheman som bidrar till unionsschemat är markerad.](../images/union-schema/contributing-schemas.png)

Om du väljer namnet på ett specifikt schema markeras de fält i det föreningsschema som är en del av det schema du valde. När ett schema har valts visas unionsschemat nedtonat med svarta fält som anger vilka fält som är en del av det medverkande schemat.

![Det valda bidragande schemat är markerat. Fälten som ingår i det medverkande schemat förblir svarta, medan fälten som inte ingår i det medverkande schemat är nedtonade.](../images/union-schema/select-schema.png)

## Visa identiteter {#view-identities}

Genom användargränssnittet kan du visa en lista med identiteter som ingår i unionsschemat genom att välja **[!UICONTROL Identities]** för att expandera listan.

![Identiteterna som tillhör föreningsschemat är markerade.](../images/union-schema/identities.png)

Om du väljer en enskild identitet från listan uppdateras det visade schemat automatiskt efter behov för att visa identitetsfältet. Detta kan inkludera att utöka flera fält om identitetsfältet är kapslat.

Identitetsfältet markeras i unionsschemat och informationen om identiteten visas till höger på skärmen. Detaljerna innehåller en lista med scheman som innehåller identitetsfältet och du kan gå nedåt för att hitta länkar till datauppsättningar relaterade till det schemat som samlar in data i det valda identitetsfältet.

![Den valda identiteten är markerad. Information om den valda identiteten visas på höger sidofält.](../images/union-schema/select-identity.png)

## Visa relationer {#view-relationships}

Med unionsschemats användargränssnitt kan du även se relationer som har definierats för scheman baserat på den valda schemaklassen. Att definiera en relation är ett sätt att koppla samman två scheman som tillhör olika klasser för att få mer komplexa insikter i kunddata.

Om relationer har etablerats för den valda klassen visas en lista med fält som används för att skapa relationer när du väljer **[!UICONTROL Relationships]**. Alla scheman använder inte eller behöver definierade relationer, så det är vanligt att avsnittet Relationer inte innehåller några fält.

Om du vill veta mer om schemarelationer, inklusive hur du definierar dem med användargränssnittet, kan du besöka [det här dokumentet om schemarelationer](../../xdm/tutorials/relationship-ui.md).

![Relationerna som tillhör föreningsschemat är markerade.](../images/union-schema/relationships.png)

Om du väljer ett relationsfält från listan uppdateras det visade schemat efter behov för att visa det markerade relationsfältet. Detta kan inkludera att expandera flera fält om relationsfältet är kapslat.

![Den valda relationen är markerad. Motsvarande fält för relationen är också markerat.](../images/union-schema/select-relationship.png)

## Nästa steg

Genom att läsa den här guiden kan du nu visa och navigera i unionsscheman med hjälp av användargränssnittet för [!DNL Experience Platform]. Mer information om scheman, inklusive hur de används i hela Experience Platform, får du genom att läsa [XDM-systemöversikten](../../xdm/home.md).
