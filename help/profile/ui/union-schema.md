---
keywords: Experience Platform;profile;real-time customer profile;;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile;Union schema;UNION PROFILE;union profile
title: Användargränssnittsguide för kundprofiler i realtid
topic: guide
description: I Adobe Experience Platform användargränssnitt kan du enkelt visa vilket unionsschema som helst i organisationen och förhandsgranska fält, identiteter, relationer och bidragande scheman för en viss klass. Den här guiden ger detaljerad information om hur du visar och utforskar unionens scheman med hjälp av plattformsgränssnittet.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---


# [!UICONTROL Union schema] Användargränssnittsguide

I Adobe Experience Platform användargränssnitt kan du enkelt visa vilket unionsschema som helst i organisationen och förhandsgranska fält, identiteter, relationer och bidragande scheman för en viss klass. Den här guiden ger detaljerad information om hur du visar och utforskar unionens scheman med hjälp av plattformsgränssnittet.

## Komma igång

Den här gränssnittshandboken kräver en förståelse av de olika [!DNL Experience Platform] tjänster som används för att hantera kundprofildata i realtid. Innan du läser den här handboken eller arbetar i användargränssnittet bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-time Customer Profile]](../home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Identity Service]](../../identity-service/home.md): Möjliggör [!DNL Real-time Customer Profile] genom att överbrygga identiteter från olika datakällor när de hämtas till [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.

## Förstå fackscheman

Med kundprofilen i realtid kan ni skapa robusta, centraliserade profiler med kundattribut och tidsstämplade händelser för varje kundinteraktion i alla system som är integrerade med Adobe Experience Platform. Format och struktur för dessa data tillhandahålls av XDM-scheman (Experience Data Model), där varje schema baseras på en XDM-klass och innehåller fält som är kompatibla med den klassen.

Du kan skapa scheman för flera användningsfall, som refererar till samma klass men som innehåller fält som är specifika för deras användning. När ett schema aktiveras för profilen blir det en del av ett unionsschema. Unionsscheman består med andra ord av flera scheman som delar samma klass och har aktiverats för profilen. Med unionsschemat kan du se en sammanslagning av alla fält i scheman som delar samma klass. Kundprofilen i realtid använder unionsschemat för att skapa en helhetsbild av varje enskild kund.

Att arbeta med fackliga scheman kräver en djupgående förståelse av XDM-scheman. För mer information börjar du med att läsa [grunderna för schemakomposition](../../xdm/schema/composition.md).

## Visa unionskartor

Om du vill navigera till unionsscheman i plattformsgränssnittet väljer du **[!UICONTROL Profiles]** från den vänstra navigeringen och sedan **[!UICONTROL Union Schema]** fliken. Fliken öppnas så att det går att visa unionsschemat för den valda klassen. [!UICONTROL Union Schema]

![](../images/union-schema/union-schema-landing.png)

## Välj en klass

Om du vill visa unionsschemat för en viss XDM-klass väljer du klassen i **[!UICONTROL Class]** listrutan. På grund av att inte alla klasser har union-scheman är bara klasser med union-scheman (dvs. klasser med scheman som har aktiverats för profil) tillgängliga i listrutan.

När en klass har valts uppdateras det schema som visas så att det återspeglar unionsschemat för den valda klassen. Du kan till exempel välja **[!UICONTROL XDM Individual Profile]** att visa föreningsschemat för den klassen.

![](../images/union-schema/union-schema-class.png)

## Utforska fackscheman

Du kan utforska unionsschemat genom att rulla uppåt och nedåt för att visa den fullständiga schemastrukturen och genom att välja en höger vinkelparentes (`>`) för att expandera kapslade fält.

![](../images/union-schema/union-schema-explore.png)

Markera ett fält om du vill visa information om det, inklusive visningsnamn, datatyp, beskrivning, sökväg, datum när det skapades och senaste ändringsdatum. Du kan även visa en lista med medverkande scheman som innehåller det fält du har markerat.

![](../images/union-schema/union-schema-explore-field.png)

När du väljer namnet på ett bidragsgivande schema visas namnen på de datauppsättningar som är relaterade till det schemat som samlar in data i det valda fältet. Varje datauppsättningsnamn visas som en länk. Om du väljer ett datauppsättningsnamn öppnas aktivitetsfliken för den datauppsättningen i ett nytt fönster.

Mer information om datauppsättningar, inklusive hur du visar datauppsättningsaktivitet och förhandsgranskar datauppsättningsdata i användargränssnittet, finns i [användargränssnittshandboken](../../catalog/datasets/user-guide.md)för datauppsättningar.

![](../images/union-schema/union-schema-field-datasets.png)

## Visa bidragande scheman

Du kan också visa vilka specifika scheman som bidrar till unionsschemat genom **[!UICONTROL All contributing schemas]** att välja att expandera listan med scheman. Beroende på vilken klass du har valt och hur många scheman din organisation har skapat inom Platform kan det vara en kort lista som innehåller ett enda schema eller en lång lista med många scheman.

![](../images/union-schema/union-schema-contributing-schemas.png)

Om du väljer namnet på ett specifikt schema markeras de fält i det föreningsschema som är en del av det schema du valde. När ett schema har valts visas unionsschemat nedtonat med svarta fält som anger vilka fält som är en del av det medverkande schemat.

![](../images/union-schema/union-schema-select-schema.png)

## Visa identiteter

Genom användargränssnittet kan du visa en lista med identiteter som ingår i unionsschemat genom att välja **[!UICONTROL Identities]** att expandera listan.

![](../images/union-schema/union-schema-identities.png)

Om du väljer en enskild identitet från listan uppdateras det visade schemat automatiskt efter behov för att visa identitetsfältet. Detta kan inkludera att utöka flera fält om identitetsfältet är kapslat.

Identitetsfältet markeras i unionsschemat och informationen om identiteten visas till höger på skärmen. Detaljerna innehåller en lista med scheman som innehåller identitetsfältet och du kan gå nedåt för att hitta länkar till datauppsättningar relaterade till det schemat som samlar in data i det valda identitetsfältet.

![](../images/union-schema/union-schema-select-identity.png)

## Visa relationer

Med unionsschemats användargränssnitt kan du även se relationer som har definierats för scheman baserat på den valda schemaklassen. Att definiera en relation är ett sätt att koppla samman två scheman som tillhör olika klasser för att få mer komplexa insikter i kunddata.

Om relationer har skapats för den valda klassen visas en lista med fält som används för att skapa relationer när du väljer **[!UICONTROL Relationships]** . Alla scheman använder inte eller behöver definierade relationer, så det är vanligt att avsnittet Relationer inte innehåller några fält.

Om du vill veta mer om schemarelationer, inklusive hur du definierar dem med användargränssnittet, kan du besöka [det här dokumentet om schemarelationer](../../xdm/tutorials/relationship-ui.md).

![](../images/union-schema/union-schema-relationships.png)

Om du väljer ett relationsfält från listan uppdateras det visade schemat efter behov för att visa det markerade relationsfältet. Detta kan inkludera att expandera flera fält om relationsfältet är kapslat.

![](../images/union-schema/union-schema-select-relationship.png)

## Nästa steg

Genom att läsa den här guiden kan du nu visa och navigera i fackliga scheman med hjälp av [!DNL Experience Platform] användargränssnittet. Mer information om scheman, inklusive hur de används i hela plattformen, får du om du börjar med att läsa [systemöversikten](../../xdm/home.md)för XDM.
