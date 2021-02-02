---
keywords: Experience Platform;hem;populära ämnen;ui;UI;XDM;XDM system;Experience data model;Experience data model;experience data model;data model;data model;schema editor;schema editor;schema;schema;scheman;scheman;scheman;skapa;relation;relation;referens;referens;
solution: Experience Platform
title: Definiera en relation mellan två scheman med schemaredigeraren
description: I det här dokumentet finns en självstudiekurs för att definiera en relation mellan två scheman med hjälp av Schemaredigeraren i användargränssnittet i Experience Platform.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# Definiera en relation mellan två scheman med [!DNL Schema Editor]

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer inom strukturen för dina [!DNL Experience Data Model] (XDM)-scheman kan du få komplexa insikter i dina kunddata.

Schemarelationer kan härledas genom användning av unionsschemat och [!DNL Real-time Customer Profile], men detta gäller endast scheman som delar samma klass. Om du vill upprätta en relation mellan två scheman som tillhör olika klasser måste ett dedikerat relationsfält läggas till i ett källschema, som refererar till identiteten för ett målschema.

I det här dokumentet finns en självstudiekurs för att definiera en relation mellan två scheman med hjälp av Schemaredigeraren i användargränssnittet för [!DNL Experience Platform]. Anvisningar om hur du definierar schemarelationer med API:t finns i självstudiekursen om att [definiera en relation med API:t för schemaregister](relationship-api.md).

## Komma igång

Den här självstudiekursen kräver en arbetsförståelse för [!DNL XDM System] och Schemaredigeraren i gränssnittet för [!DNL Experience Platform]. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM System i Experience Platform](../home.md): En översikt över XDM och dess implementering i  [!DNL Experience Platform].
* [Grundläggande om schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [Skapa ett schema med [!DNL Schema Editor]](create-schema-ui.md): En självstudiekurs som handlar om grunderna för att arbeta med  [!DNL Schema Editor].

## Definiera en källa och ett målschema

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. I demonstrationssyfte skapar den här självstudien en relation mellan medlemmar i en organisations lojalitetsprogram (definierat i ett [!DNL Loyalty Members]-schema) och deras favorithotell (definierat i ett [!DNL Hotels]-schema).

>[!IMPORTANT]
>
>För att kunna etablera en relation måste båda scheman ha definierade primära identiteter och vara aktiverade för [!DNL Real-time Customer Profile]. Se avsnittet [Aktivera ett schema för användning i profilen](./create-schema-ui.md#profile) i självstudiekursen för att skapa schema om du behöver hjälp med hur du konfigurerar scheman därefter.

Schemarelationer representeras av ett dedikerat fält i ett **källschema** som refererar till ett annat fält i ett **målschema**. I de följande stegen kommer &quot;[!DNL Loyalty Members]&quot; att vara källschemat, medan &quot;[!DNL Hotels]&quot; fungerar som målschema.

I följande avsnitt beskrivs strukturen för varje schema som används i den här självstudiekursen innan en relation har definierats.

### [!DNL Loyalty Members] schema

Källschemat [!DNL Loyalty Members] baseras på klassen [!DNL XDM Individual Profile] och är det schema som skapades i självstudiekursen för att [skapa ett schema i användargränssnittet](create-schema-ui.md). Det innehåller ett `loyalty`-objekt under namnutrymmet `_tenantId`, som innehåller flera lojalitetsspecifika fält. Ett av dessa fält, `loyaltyId`, fungerar som primär identitet för schemat under namnområdet [!UICONTROL Email]. Som framgår av **[!UICONTROL Schema Properties]** har schemat aktiverats för användning i [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Målschemat [!DNL Hotels] är baserat på en anpassad [!DNL Hotels]-klass och innehåller fält som beskriver ett hotell. Fältet `hotelId` fungerar som primär identitet för schemat under ett anpassat `hotelId`-namnutrymme. Precis som [!DNL Loyalty Members]-schemat har schemat även aktiverats för [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Skapa en relationsblandning

>[!NOTE]
>
>Det här steget krävs bara om källschemat inte har ett dedikerat strängtypsfält som ska användas som referens till målschemat. Om det här fältet redan är definierat i källschemat går du vidare till nästa steg i [som definierar ett relationsfält](#relationship-field).

För att kunna definiera en relation mellan två scheman måste källschemat ha ett dedikerat fält som ska användas som referens till målschemat. Du kan lägga till det här fältet i källschemat genom att skapa en ny blandning.

Börja med att välja **[!UICONTROL Add]** i avsnittet **[!UICONTROL Mixins]**.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Dialogrutan [!UICONTROL Add Mixin] visas. Välj **[!UICONTROL Create new mixin]** härifrån. I textfälten som visas anger du ett visningsnamn och en beskrivning för den nya blandningen. Välj **[!UICONTROL Add mixin]** när du är klar.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Arbetsytan visas igen med &quot;[!DNL Favorite Hotel]&quot; i **[!UICONTROL Mixins]**-avsnittet. Markera namnet på mixen och välj sedan **[!UICONTROL Add field]** bredvid fältet `Loyalty Members` på rotnivå.

![](../images/tutorials/relationship/loyalty-add-field.png)

Ett nytt fält visas på arbetsytan under namnutrymmet `_tenantId`. Under **[!UICONTROL Field properties]** anger du ett fältnamn och ett visningsnamn för fältet och anger dess typ till [!UICONTROL String].

![](../images/tutorials/relationship/relationship-field-details.png)

När du är klar väljer du **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Det uppdaterade `favoriteHotel`-fältet visas på arbetsytan. Välj **[!UICONTROL Save]** för att slutföra ändringarna av schemat.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definiera ett relationsfält för källschemat {#relationship-field}

När ett dedikerat referensfält har definierats i källschemat kan du ange det som ett relationsfält.

Markera fältet `favoriteHotel` på arbetsytan och rulla sedan nedåt under **[!UICONTROL Field properties]** tills kryssrutan **[!UICONTROL Relationship]** visas. Markera kryssrutan för att visa de parametrar som krävs för att konfigurera ett relationsfält.

![](../images/tutorials/relationship/relationship-checkbox.png)

Välj listrutan för **[!UICONTROL Reference schema]** och välj målschemat för relationen (&quot;[!DNL Hotels]&quot; i det här exemplet). Om målschemat är aktiverat för [!DNL Profile] ställs fältet **[!UICONTROL Reference identity namespace]** automatiskt in på namnområdet för målschemats primära identitet. Om schemat inte har någon primär identitet definierad, måste du manuellt välja det namnutrymme som du vill använda i listrutan. Välj **[!UICONTROL Apply]** när du är klar.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Fältet `favoriteHotel` är nu markerat som en relation på arbetsytan, med namnet och referensidentitetens namnområde i målschemat. Välj **[!UICONTROL Save]** om du vill spara ändringarna och slutföra arbetsflödet.

![](../images/tutorials/relationship/relationship-save.png)

## Nästa steg

I den här självstudiekursen har du skapat en 1:1-relation mellan två scheman med [!DNL Schema Editor]. Anvisningar om hur du definierar relationer med API:t finns i självstudiekursen om att [definiera en relation med API:t för schemaregister](relationship-api.md).