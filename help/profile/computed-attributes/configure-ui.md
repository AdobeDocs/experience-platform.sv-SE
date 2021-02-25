---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Konfigurera ett beräknat attributfält
topic: guide
type: Dokumentation
description: Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. För att kunna konfigurera ett beräknat attribut måste du först identifiera fältet som innehåller det beräknade attributvärdet. Det här fältet kan skapas med hjälp av en mixin för att lägga till fältet i ett befintligt schema, eller genom att markera ett fält som du redan har definierat i ett schema.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---


# (Alfa) Konfigurera ett beräknat attributfält i användargränssnittet

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

För att kunna konfigurera ett beräknat attribut måste du först identifiera fältet som innehåller det beräknade attributvärdet. Det här fältet kan skapas med hjälp av en mixin för att lägga till fältet i ett befintligt schema, eller genom att markera ett fält som du redan har definierat i ett schema.

>[!NOTE]
>
>Beräknade attribut kan inte läggas till i fält i Adobe-definierade blandningar. Fältet måste finnas i namnutrymmet `tenant`, vilket innebär att det måste vara ett fält som du definierar och lägger till i ett schema.

För att kunna definiera ett beräknat attributfält måste schemat vara aktiverat för [!DNL Profile] och visas som en del av unionsschemat för den klass som schemat baseras på. Mer information om [!DNL Profile]-aktiverade scheman och fackföreningar finns i [!DNL Schema Registry]-utvecklarguiden på [som aktiverar ett schema för profil och visning av fackscheman](../../xdm/api/getting-started.md). Vi rekommenderar även att du läser avsnittet [om föreningar](../../xdm/schema/composition.md) i dokumentationen för schemakomposition.

Arbetsflödet i den här självstudien använder ett [!DNL Profile]-aktiverat schema och följer stegen för att definiera en ny blandning som innehåller det beräknade attributfältet och säkerställa att det är rätt namnutrymme. Om du redan har ett fält i rätt namnutrymme i ett profilaktiverat schema kan du fortsätta direkt till steget för [att skapa ett beräknat attribut](#create-a-computed-attribute).

## Visa ett schema

Stegen som följer använder Adobe Experience Platform användargränssnitt för att hitta ett schema, lägga till en blandning och definiera ett fält. Om du föredrar att använda API:t [!DNL Schema Registry] kan du läsa [Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md) för steg om hur du skapar en blandning, lägger till en blandning i ett schema och aktiverar ett schema för användning med [!DNL Real-time Customer Profile].

I användargränssnittet klickar du på **[!UICONTROL Schemas]** i den vänstra listen och använder sökfältet på fliken **[!UICONTROL Browse]** för att snabbt hitta det schema du vill uppdatera.

![](../images/computed-attributes/Schemas-Browse.png)

När du har hittat schemat klickar du på dess namn för att öppna [!DNL Schema Editor] där du kan redigera schemat.

![](../images/computed-attributes/Schema-Editor.png)

## Skapa en blandning

Om du vill skapa en ny blandning klickar du på **[!UICONTROL Add]** bredvid **[!UICONTROL Mixins]** i **[!UICONTROL Composition]**-avsnittet till vänster i redigeraren. Dialogrutan **[!UICONTROL Add mixin]** öppnas där du kan se befintliga mixar. Klicka på alternativknappen för **[!UICONTROL Create new mixin]** för att definiera din nya blandning.

Ge blandningen ett namn och en beskrivning och klicka på **[!UICONTROL Add mixin]** när du är klar.

![](../images/computed-attributes/Add-mixin.png)

## Lägg till ett beräknat attributfält i schemat

Din nya blandning ska nu visas i avsnittet [!UICONTROL Mixins] under [!UICONTROL Composition]. Klicka på namnet på mixen och flera **[!UICONTROL Add field]**-knappar visas i **[!UICONTROL Structure]**-delen av redigeraren.

Välj **[!UICONTROL Add field]** bredvid schemats namn om du vill lägga till ett fält på den översta nivån. Du kan också välja att lägga till fältet var som helst i det schema du vill.

När du har klickat på **[!UICONTROL Add field]** öppnas ett nytt objekt med namnet för ditt klient-ID, som visar att fältet finns i rätt namnutrymme. Inom det objektet visas ett **[!UICONTROL New field]**-värde. Detta gäller fältet där du definierar det beräknade attributet.

![](../images/computed-attributes/New-field.png)

## Konfigurera fältet

Använd avsnittet **[!UICONTROL Field properties]** till höger om redigeraren för att ange den information som behövs för det nya fältet, inklusive namn, visningsnamn och typ.

>[!NOTE]
>
>Fälttypen måste vara av samma typ som det beräknade attributvärdet. Om det beräknade attributvärdet till exempel är en sträng måste fältet som definieras i schemat vara en sträng.

När du är klar klickar du på **[!UICONTROL Apply]** och fältets namn och typ visas i **[!UICONTROL Structure]**-delen av redigeraren.

![](../images/computed-attributes/Apply.png)

## Aktivera schema för [!DNL Profile]

Kontrollera att schemat har aktiverats för [!DNL Profile] innan du fortsätter. Klicka på schemanamnet i avsnittet **[!UICONTROL Structure]** i redigeraren så att fliken **[!UICONTROL Schema Properties]** visas. Om skjutreglaget **[!UICONTROL Profile]** är blått har schemat aktiverats för [!DNL Profile].

>[!NOTE]
>
>Det går inte att ångra aktiveringen av ett schema för [!DNL Profile], så om du klickar på skjutreglaget när det har aktiverats behöver du inte riskera att det inaktiveras.

![](../images/computed-attributes/Profile.png)

Nu kan du klicka på **[!UICONTROL Save]** för att spara det uppdaterade schemat och fortsätta med resten av självstudiekursen med API:t.

## Nästa steg

Nu när du har skapat ett fält där ditt beräknade attributvärde ska lagras kan du skapa det beräknade attributet med API-slutpunkten `/computedattributes`. Följ stegen i [API-slutpunktshandboken för beräknade attribut för detaljerade steg för att skapa ett beräknat attribut i API:t.](ca-api.md)