---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Konfigurera ett beräknat attributfält
type: Documentation
description: Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. För att kunna konfigurera ett beräknat attribut måste du först identifiera fältet som innehåller det beräknade attributvärdet. Det här fältet kan skapas med en schemafältgrupp för att lägga till fältet i ett befintligt schema, eller genom att markera ett fält som du redan har definierat i ett schema.
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# (Alfa) Konfigurera ett beräknat attributfält i användargränssnittet

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

För att kunna konfigurera ett beräknat attribut måste du först identifiera fältet som innehåller det beräknade attributvärdet. Det här fältet kan skapas med en schemafältgrupp för att lägga till fältet i ett befintligt schema, eller genom att markera ett fält som du redan har definierat i ett schema.

>[!NOTE]
>
>Beräknade attribut kan inte läggas till i fält i fältgrupper som definieras av Adobe. Fältet måste finnas i `tenant` namnutrymme, vilket innebär att det måste vara ett fält som du definierar och lägger till i ett schema.

Schemat måste aktiveras för att ett beräknat attributfält ska kunna definieras [!DNL Profile] och visas som en del av unionsschemat för den klass som schemat baseras på. Mer information om [!DNL Profile]-aktiverade scheman och fackföreningar, gå igenom avsnittet i [!DNL Schema Registry] utvecklarguide på [aktivera ett schema för profil och visning av fackscheman](../../xdm/api/getting-started.md). Vi rekommenderar även att du granskar [sektion om fackföreningar](../../xdm/schema/composition.md) i schemakompositionsdokumentationen.

Arbetsflödet i den här självstudiekursen använder en [!DNL Profile]-enabled schema och följer stegen för att definiera en ny fältgrupp som innehåller det beräknade attributfältet och kontrollera att det är rätt namnutrymme. Om du redan har ett fält i rätt namnutrymme i ett profilaktiverat schema kan du fortsätta direkt till steget för [skapa ett beräknat attribut](#create-a-computed-attribute).

## Visa ett schema

Stegen som följer använder Adobe Experience Platform användargränssnitt för att hitta ett schema, lägga till en fältgrupp och definiera ett fält. Om du föredrar att använda [!DNL Schema Registry] API, se [Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md) för steg om hur du skapar en fältgrupp, lägger till en fältgrupp i ett schema och aktiverar ett schema för användning med [!DNL Real-Time Customer Profile].

I användargränssnittet klickar du på **[!UICONTROL Schemas]** till vänster och använd sökfältet på **[!UICONTROL Browse]** för att snabbt hitta det schema du vill uppdatera.

![](../images/computed-attributes/Schemas-Browse.png)

När du har hittat schemat klickar du på dess namn för att öppna [!DNL Schema Editor] där du kan redigera schemat.

![](../images/computed-attributes/Schema-Editor.png)

## Skapa en fältgrupp

Om du vill skapa en ny fältgrupp klickar du på **[!UICONTROL Add]** nästa **[!UICONTROL Field groups]** i **[!UICONTROL Composition]** till vänster om redigeraren. Då öppnas **[!UICONTROL Add field group]** där du kan se befintliga fältgrupper. Klicka på alternativknappen för **[!UICONTROL Create new field group]** för att definiera din nya fältgrupp.

Ge fältgruppen ett namn och en beskrivning och klicka på **[!UICONTROL Add field group]** när det är klart.

![](../images/computed-attributes/Add-field-group.png)

## Lägg till ett beräknat attributfält i schemat

Din nya fältgrupp ska nu visas i[!UICONTROL Field groups]&quot; under &quot;[!UICONTROL Composition]&quot;. Klicka på namnet på fältgruppen och flera **[!UICONTROL Add field]** knapparna visas i **[!UICONTROL Structure]** i redigeraren.

Välj **[!UICONTROL Add field]** bredvid schemats namn för att lägga till ett fält på den översta nivån, eller så kan du välja att lägga till fältet var som helst i det schema du föredrar.

Efter klickning **[!UICONTROL Add field]** Ett nytt objekt öppnas med namnet för ditt klient-ID som visar att fältet finns i rätt namnutrymme. Inom det objektet **[!UICONTROL New field]** visas. Detta gäller fältet där du definierar det beräknade attributet.

![](../images/computed-attributes/New-field.png)

## Konfigurera fältet

Använda **[!UICONTROL Field properties]** till höger om redigeraren anger du den information som behövs för det nya fältet, inklusive namn, visningsnamn och typ.

>[!NOTE]
>
>Fälttypen måste vara av samma typ som det beräknade attributvärdet. Om det beräknade attributvärdet till exempel är en sträng måste fältet som definieras i schemat vara en sträng.

När du är klar klickar du på **[!UICONTROL Apply]** och fältets namn, liksom dess typ, visas i **[!UICONTROL Structure]** i redigeraren.

![](../images/computed-attributes/Apply.png)

## Aktivera schema för [!DNL Profile]

Kontrollera att schemat har aktiverats för innan du fortsätter [!DNL Profile]. Klicka på schemanamnet i **[!UICONTROL Structure]** så att **[!UICONTROL Schema Properties]** visas. Om **[!UICONTROL Profile]** skjutreglaget är blått, schemat har aktiverats för [!DNL Profile].

>[!NOTE]
>
>Aktivera ett schema för [!DNL Profile] kan inte ångras, så om du klickar på skjutreglaget när det har aktiverats behöver du inte riskera att det inaktiveras.

![](../images/computed-attributes/Profile.png)

Nu kan du klicka **[!UICONTROL Save]** för att spara det uppdaterade schemat och fortsätta med resten av självstudiekursen med API:t.

## Nästa steg

Nu när du har skapat ett fält där ditt beräknade attributvärde ska lagras kan du skapa det beräknade attributet med hjälp av `/computedattributes` API-slutpunkt. Följ stegen i [API-slutpunktsguide för beräknade attribut](ca-api.md).