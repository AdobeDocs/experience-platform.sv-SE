---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definiera en relation mellan två scheman med schemaredigeraren
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Definiera en relation mellan två scheman med Schemaredigeraren

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer i strukturen för era XDM-scheman (Experience Data Model) kan ni få komplexa insikter i era kunddata.

I det här dokumentet finns en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med Schemaredigeraren i användargränssnittet i Experience Platform. Anvisningar om hur du definierar schemarelationer med API:t finns i självstudiekursen om hur du [definierar en relation med API:t](relationship-api.md)för schemaregister.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för XDM-systemet och Schemaredigeraren i användargränssnittet i Experience Platform. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM System i Experience Platform](../home.md): En översikt över XDM och dess implementering i Experience Platform.
* [Grundläggande om schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [Skapa ett schema med Schemaredigeraren](create-schema-ui.md): En självstudiekurs som beskriver grunderna i att arbeta med Schemaredigeraren.

## Definiera en källa och ett målschema

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. I demonstrationssyfte skapar den här självstudiekursen en relation mellan medlemmar i en organisations lojalitetsprogram (som definieras i ett&quot;Loyalty Members&quot;-schema) och deras favorithotell (som definieras i ett&quot;Hotels&quot;-schema).

Schemarelationer representeras av ett **källschema** med ett fält som refererar till ett annat fält i ett **målschema**. I de följande stegen kommer &quot;Lojalitetsmedlemmar&quot; att vara källschemat, medan &quot;Hotels&quot; fungerar som målschema.

I följande avsnitt beskrivs strukturen för varje schema som används i den här självstudiekursen innan en relation har definierats.

### Bonusmedlemsschema

Källschemat&quot;Förmånsmedlemmar&quot; är det schema som skapades i självstudiekursen för att [skapa ett schema i användargränssnittet](create-schema-ui.md). Det innehåller ett&quot;loyalty&quot;-objekt under namnutrymmet &quot;\_tenantId&quot;, som innehåller flera lojalitetsspecifika fält. Ett av dessa fält, &quot;loyaltyId&quot;, fungerar som primär identitet för schemat under namnområdet &quot;Email&quot;. Så som visas under _Schemaegenskaper_ har schemat aktiverats för användning i [kundprofilen](../../profile/home.md)i realtid.

![](../images/tutorials/relationship/loyalty-members.png)

### Hotellschema

Målschemat &quot;Hotels&quot; innehåller fält som beskriver ett hotell, inklusive adress, märke, antal rum och stjärngradering. Fältet&quot;hotelId&quot; fungerar som primär identitet för schemat under namnområdet&quot;ECID&quot;. Till skillnad från&quot;lojalitetsmedlemmar&quot; har det här schemat inte aktiverats för kundprofil i realtid.

![](../images/tutorials/relationship/hotels.png)

## Skapa en relationsblandning

>[!NOTE]
>
>Det här steget krävs bara om källschemat inte har ett dedikerat strängtypsfält som ska användas som referens till ett annat schema. Om det här fältet redan är definierat i källschemat går du vidare till nästa steg när du [definierar ett relationsfält](#relationship-field).

För att kunna definiera en relation mellan två scheman måste källschemat ha ett dedikerat fält som ska användas som referens till målschemat. Du kan lägga till det här fältet i källschemat genom att skapa en ny blandning.

Börja med att klicka på **Lägg** till i _avsnittet Blandningar_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Dialogrutan _Lägg till mixning_ visas. Klicka på **Skapa ny mixning** härifrån. I textfälten som visas anger du ett visningsnamn och en beskrivning för den nya blandningen. Klicka på **Lägg till mixning** när du är klar.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Arbetsytan visas igen med&quot;lojalitetsförhållande&quot; i avsnittet _Blandningar_ . Klicka på blandningsnamnet och klicka sedan på **Lägg till fält** bredvid rotnivåfältet&quot;Lojalitetsmedlemmar&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Ett nytt fält visas på arbetsytan under namnutrymmet &quot;\_tenantId&quot;. Under _Fältegenskaper_ anger du ett fältnamn och ett visningsnamn för fältet och anger dess typ till &quot;String&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

När du är klar klickar du på **Använd**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Det uppdaterade fältet&quot;loyaltyRelationship&quot; visas på arbetsytan. Klicka på **Spara** för att slutföra ändringarna av schemat.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definiera ett relationsfält för källschemat {#relationship-field}

När ett dedikerat referensfält har definierats i källschemat kan du ange det som ett relationsfält.

Klicka på referensfältet på arbetsytan och rulla sedan nedåt under _Fältegenskaper_ tills kryssrutan **Relation** visas. Markera kryssrutan för att visa de parametrar som krävs för att konfigurera ett relationsfält.

![](../images/tutorials/relationship/relationship-checkbox.png)

Klicka på listrutan för **referensschema** och välj målschema för relationen (&quot;Hotels&quot; i det här exemplet). Om målschemat är unionsaktiverat ställs fältet **Referensidentitetsnamnområde** automatiskt in på namnområdet för målschemats primära identitet. Om schemat inte har någon primär identitet definierad, måste du manuellt välja det namnutrymme som du vill använda i listrutan. Klicka på **Använd** när du är klar.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Fältet visas som en relation på arbetsytan med namnet och namnområdet för referensidentiteten i målschemat. Klicka på **Spara** för att spara ändringarna och slutföra arbetsflödet.

![](../images/tutorials/relationship/relationship-save.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en 1:1-relation mellan två scheman med hjälp av Schemaredigeraren. Anvisningar om hur du definierar relationer med API:t finns i självstudiekursen om hur du [definierar en relation med API:t](relationship-api.md)för schemaregister.