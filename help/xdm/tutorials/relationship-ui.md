---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definiera en relation mellan två scheman med schemaredigeraren
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# Definiera en relation mellan två scheman med [!DNL Schema Editor]

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer inom strukturen för era [!DNL Experience Data Model] (XDM) scheman kan ni få komplexa insikter i era kunddata.

Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med hjälp av [!DNL Schema Editor] i [!DNL Experience Platform] användargränssnittet. Anvisningar om hur du definierar schemarelationer med API:t finns i självstudiekursen om hur du [definierar en relation med API:t](relationship-api.md)för schemaregister.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för [!DNL XDM System] och [!DNL Schema Editor] för [!DNL Experience Platform] användargränssnittet. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM System i Experience Platform](../home.md): En översikt över XDM och dess implementering i Experience Platform.
* [Grundläggande om schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [Skapa ett schema med Schemaredigeraren](create-schema-ui.md): En självstudiekurs som handlar om grunderna för att arbeta med [!DNL Schema Editor].

## Definiera en källa och ett målschema

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. I demonstrationssyfte skapar den här självstudien en relation mellan medlemmar i en organisations lojalitetsprogram (definieras i ett&quot;[!UICONTROL Loyalty Members]&quot; schema) och deras favorithotell (definieras i ett&quot;Hotels&quot;-schema).

Schemarelationer representeras av ett fält **[!UICONTROL source schema]** som refererar till ett annat fält i ett **[!UICONTROL destination schema]**. I de följande stegen kommer&quot;[!UICONTROL Loyalty Members]&quot; att vara källschemat, medan&quot;Hotels&quot; fungerar som målschema.

I följande avsnitt beskrivs strukturen för varje schema som används i den här självstudiekursen innan en relation har definierats.

### [!UICONTROL Loyalty Members] schema

Källschemat &quot;[!UICONTROL Loyalty Members]&quot; är det schema som skapades i självstudiekursen för att [skapa ett schema i användargränssnittet](create-schema-ui.md). Det innehåller ett&quot;[!UICONTROL loyalty]&quot;-objekt under namnutrymmet&quot;[!UICONTROL \_tenantId]&quot;, som innehåller flera lojalitetsspecifika fält. Ett av dessa fält, &quot;[!UICONTROL loyaltyId]&quot;, fungerar som primär identitet för schemat under namnområdet &quot;[!UICONTROL Email]&quot;. Så som visas under _Schemaegenskaper_ har schemat aktiverats för användning i [!DNL Real-time Customer Profile](../../profile/home.md).

![](../images/tutorials/relationship/loyalty-members.png)

### Hotellschema

Målschemat &quot;[!UICONTROL Hotels]&quot; innehåller fält som beskriver ett hotell, inklusive adress, märke, antal rum och stjärngradering. Fältet &quot;[!UICONTROL hotelId]&quot; fungerar som primär identitet för schemat under namnområdet &quot;ECID&quot;. Till skillnad från&quot;[!UICONTROL Loyalty Members]&quot; har schemat inte aktiverats för [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Skapa en relationsblandning

>[!NOTE]
>
>Det här steget krävs bara om källschemat inte har ett dedikerat strängtypsfält som ska användas som referens till ett annat schema. Om det här fältet redan är definierat i källschemat går du vidare till nästa steg när du [definierar ett relationsfält](#relationship-field).

För att kunna definiera en relation mellan två scheman måste källschemat ha ett dedikerat fält som ska användas som referens till målschemat. Du kan lägga till det här fältet i källschemat genom att skapa en ny blandning.

Börja med att klicka **[!UICONTROL Add]** i avsnittet _Blandningar_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Dialogrutan [!UICONTROL _Lägg till mixning _]visas. Klicka här **[!UICONTROL Create New Mixin]**. I textfälten som visas anger du ett visningsnamn och en beskrivning för den nya blandningen. Klicka **[!UICONTROL Add Mixin]**när du är klar.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Arbetsytan visas igen med&quot;[!UICONTROL Loyalty Relationship]&quot; i avsnittet _Blandningar_ . Klicka på blandningsnamnet och klicka sedan på **[!UICONTROL Add Field]** bredvid rotnivåfältet &quot;[!UICONTROL Loyalty Members]&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Ett nytt fält visas på arbetsytan under namnutrymmet&quot;[!UICONTROL \_tenantId]&quot;. Under [!UICONTROL _Fältegenskaper _]anger du ett fältnamn och ett visningsnamn för fältet och anger dess typ till &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

När du är klar klickar du på **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Det uppdaterade fältet&quot;[!UICONTROL loyaltyRelationship]&quot; visas på arbetsytan. Klicka **[!UICONTROL Save]** för att slutföra ändringarna av schemat.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definiera ett relationsfält för källschemat {#relationship-field}

När ett dedikerat referensfält har definierats i källschemat kan du ange det som ett relationsfält.

Klicka på referensfältet på arbetsytan och rulla sedan nedåt under _[!UICONTROL Field Properties]_tills **[!UICONTROL Relationship]**kryssrutan visas. Markera kryssrutan för att visa de parametrar som krävs för att konfigurera ett relationsfält.

![](../images/tutorials/relationship/relationship-checkbox.png)

Klicka på listrutan för **[!UICONTROL Reference Schema]** och välj målschema för relationen (&quot;[!UICONTROL Hotels]&quot; i det här exemplet). Om målschemat är föreningsaktiverat ställs fältet automatiskt in på **[!UICONTROL Reference Identity Namespace]** namnområdet för målschemats primära identitet. Om schemat inte har någon primär identitet definierad, måste du manuellt välja det namnutrymme som du vill använda i listrutan. Klicka **[!UICONTROL Apply]** när du är klar.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Fältet visas som en relation på arbetsytan med namnet och namnområdet för referensidentiteten i målschemat. Klicka **[!UICONTROL Save]** för att spara ändringarna och slutföra arbetsflödet.

![](../images/tutorials/relationship/relationship-save.png)

## Nästa steg

I den här självstudiekursen har du skapat en 1:1-relation mellan två scheman med hjälp av [!DNL Schema Editor]. Anvisningar om hur du definierar relationer med API:t finns i självstudiekursen om hur du [definierar en relation med API:t](relationship-api.md)för schemaregister.