---
keywords: Experience Platform;hem;populära ämnen;ui;UI;XDM;XDM system;Experience data model;Experience data model;experience data model;data model;datamodell;schema editor;schema;schema;scheman;scheman;scheman;scheman;skapa;relation;relation;referens;referens;
solution: Experience Platform
title: Definiera en relation mellan två scheman med Schemaredigeraren
description: I det här dokumentet finns en självstudiekurs för att definiera en relation mellan två scheman med Schemaredigeraren i Experience Platform användargränssnitt.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---

# Definiera en 1:1-relation mellan två scheman med [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Schemarelationer"
>abstract="Scheman som tillhör olika klasser kan länkas till sammanhanget via relationsfält, vilket gör att du kan skapa mer komplexa segmenteringsregler. Mer information om schemarelationer finns i dokumentationen."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Referensschema"
>abstract="Välj det schema som du vill skapa en relation med. Det här schemat kan vara en annan klass än det aktuella schemat. Mer information om schemarelationer finns i dokumentationen."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Namnutrymme för referensidentitet"
>abstract="Namnutrymmet (typen) för referensschemats primära identitetsfält. Referensschemat måste ha ett etablerat primärt identitetsfält för att kunna delta i en relation. Mer information om schemarelationer finns i dokumentationen."

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer i strukturen för dina [!DNL Experience Data Model] (XDM)-scheman kan du få komplexa insikter i dina kunddata.

Schemarelationer kan härledas genom användning av unionsschemat och [!DNL Real-Time Customer Profile], men detta gäller endast scheman som delar samma klass. För att upprätta en relation mellan två scheman som tillhör olika klasser måste ett dedikerat relationsfält läggas till i ett källschema, som refererar till identiteten för det andra relaterade schemat.

>[!NOTE]
>
>Om både käll- och målschemat tillhör samma klass ska ett dedikerat relationsfält **inte** användas. I det här fallet använder du gränssnittet för unionsschemat för att se relationen. Instruktioner om hur du gör detta finns i avsnittet [Visa relationer](../../profile/ui/union-schema.md#view-relationships) i gränssnittsguiden för unionsscheman.

I det här dokumentet finns en självstudiekurs för att definiera en relation mellan två scheman med hjälp av Schemaredigeraren i användargränssnittet för [!DNL Experience Platform]. Anvisningar om hur du definierar schemarelationer med API:t finns i självstudiekursen [om hur du definierar en relation med API:t för schemaregister](relationship-api.md).

>[!NOTE]
>
>Anvisningar om hur du skapar en många-till-en-relation i Adobe Real-Time Customer Data Platform B2B edition finns i handboken [Skapa B2B-relationer](./relationship-b2b.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av [!DNL XDM System] och Schemaredigeraren i [!DNL Experience Platform]-gränssnittet. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM-system i Experience Platform](../home.md): En översikt över XDM och dess implementering i [!DNL Experience Platform].
* [Grunderna i schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [Skapa ett schema med  [!DNL Schema Editor]](create-schema-ui.md): En självstudiekurs som beskriver grunderna för att arbeta med [!DNL Schema Editor].

## Definiera en källa och ett referensschema

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. I demonstrationssyfte skapar den här självstudien en relation mellan medlemmar i en organisations lojalitetsprogram (definierat i ett [!DNL Loyalty Members]-schema) och deras favorithotell (definierat i ett [!DNL Hotels]-schema).

>[!IMPORTANT]
>
>För att kunna upprätta en relation måste båda scheman ha definierade primära identiteter och vara aktiverade för [!DNL Real-Time Customer Profile]. Se avsnittet [Aktivera ett schema för användning i profilen](./create-schema-ui.md#profile) i självstudiekursen för att skapa schema om du behöver hjälp med hur du konfigurerar dina scheman därefter.

Schemarelationer representeras av ett dedikerat fält i ett **källschema** som pekar på ett annat fält i ett **referensschema**. I de följande stegen blir [!DNL Loyalty Members] källschemat, medan [!DNL Hotels] fungerar som referensschema.

I följande avsnitt beskrivs strukturen för varje schema som används i den här självstudiekursen innan en relation har definierats.

### [!DNL Loyalty Members]-schema

Källschemat [!DNL Loyalty Members] baseras på klassen [!DNL XDM Individual Profile] som innehåller fält som beskriver medlemmar i ett lojalitetsprogram. Ett av dessa fält, `personalEmail.addess`, fungerar som primär identitet för schemat under namnområdet [!UICONTROL Email]. Som framgår av **[!UICONTROL Schema Properties]** har det här schemat aktiverats för användning i [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels]-schema

Referensschemat [!DNL Hotels] baseras på en anpassad [!DNL Hotels]-klass och innehåller fält som beskriver ett hotell. För att kunna delta i en relation måste referensschemat också ha en primär identitet definierad och vara aktiverat för [!UICONTROL Profile]. I det här fallet fungerar `_tenantId.hotelId` som primär identitet för schemat med ett anpassat [!DNL Hotel ID]-ID-namnområde.

![Aktivera för profilen](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Mer information om hur du skapar anpassade identitetsnamnutrymmen finns i [dokumentationen för identitetstjänsten](../../identity-service/features/namespaces.md#manage-namespaces).

## Skapa en relationsfältgrupp

>[!NOTE]
>
>Det här steget krävs bara om källschemat inte har ett dedikerat fält av strängtyp som ska användas som pekare till referensschemats primära identitet. Om det här fältet redan är definierat i källschemat går du vidare till nästa steg i [som definierar ett relationsfält](#relationship-field).

För att kunna definiera en relation mellan två scheman måste källschemat ha ett dedikerat fält som anger referensschemats primära identitet. Du kan lägga till det här fältet i källschemat genom att skapa en ny schemafältgrupp eller utöka en befintlig.

När det gäller schemat [!DNL Loyalty Members] läggs ett nytt `preferredHotel`-fält till för att ange den lojalitetsmedlemmens önskade hotell för företagsbesök. Börja med att markera plusikonen (**+**) bredvid källschemats namn.

![](../images/tutorials/relationship/loyalty-add-field.png)

En ny fältplatshållare visas på arbetsytan. Under **[!UICONTROL Field properties]** anger du ett fältnamn och ett visningsnamn för fältet och anger dess typ till [!UICONTROL String]. Under **[!UICONTROL Assign to]** väljer du en befintlig fältgrupp som ska utökas eller skriver ett unikt namn för att skapa en ny fältgrupp. I det här fallet skapas en ny fältgrupp, [!DNL Preferred Hotel].

![](../images/tutorials/relationship/relationship-field-details.png)

När du är klar väljer du **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Det uppdaterade fältet `preferredHotel` visas på arbetsytan under ett `_tenantId`-objekt eftersom det är ett anpassat fält. Välj **[!UICONTROL Save]** om du vill slutföra ändringarna av schemat.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definiera ett relationsfält för källschemat {#relationship-field}

När ett dedikerat referensfält har definierats i källschemat kan du ange det som ett relationsfält.

>[!NOTE]
>
>Relationer stöds bara i strängfält och strängmatrisfält.

Markera fältet `preferredHotel` på arbetsytan och välj sedan **[!UICONTROL Add relationship]** i sidofältet **[!UICONTROL Field properties]**.

![Schemaredigeraren med Lägg till relation är markerad i sidofältet för fältegenskaper.](../images/tutorials/relationship/add-relationship.png)

Dialogrutan [!UICONTROL Add relationship] visas. I den här dialogrutan kan du ange obligatoriska parametrar för konfigurering av ett relationsfält. För Real-Time CDP B2C-användare kan du **endast** ange en 1:1-relation mellan käll- och referensschemat.

>[!NOTE]
>
>Om du har tillgång till Real-Time CDP B2B edition kan du använda kontrollerna till höger på arbetsytan för att definiera ett relationsfält och skapa en många-till-ett-relation med dialogrutan [samma](./relationship-b2b.md#relationship-field).

![Dialogrutan Lägg till relation.](../images/tutorials/relationship/add-relationship-dialog.png)

Använd listrutan för **[!UICONTROL Reference schema]** och välj referensschema för relationen (&quot;[!DNL Hotels]&quot; i det här exemplet).

>[!NOTE]
>
>Endast scheman som innehåller en primär identitet inkluderas i listrutan för referensschema. Skyddet förhindrar att du av misstag skapar en relation med ett schema som inte är korrekt konfigurerat än.

Referensschemats identitetsnamnområde (i det här fallet [!DNL Hotel ID]) fylls i automatiskt under **[!UICONTROL Reference identity namespace]**. Välj **[!UICONTROL Apply]** när du är klar.

![Dialogrutan Lägg till relation med relationsparametrarna konfigurerade och Använd är markerad.](../images/tutorials/relationship/apply-relationship.png)

Fältet `preferredHotel` är nu markerat som en relation på arbetsytan, med namnet på referensschemat. Välj **[!UICONTROL Save]** om du vill spara ändringarna och slutföra arbetsflödet.

![Schemaredigeraren med relationsreferenserna och Spara är markerade.](../images/tutorials/relationship/relationship-save.png)

### Redigera ett befintligt relationsfält {#edit-relationship}

Om du vill ändra referensschemat markerar du ett fält med en befintlig relation och väljer sedan **[!UICONTROL Edit relationship]** i sidofältet **[!UICONTROL Field properties]**.

![Schemaredigeraren med redigeringsrelationen markerad.](../images/tutorials/relationship/edit-relationship.png)

Dialogrutan [!UICONTROL Edit relationship] visas. Härifrån kan du följa processen som beskrivs i [definiera ett relationsfält](#relationship-field) eller ta bort relationen. Välj **[!UICONTROL Delete relationship]** om du vill ta bort relationen till referensschemat.

![Dialogrutan Redigera relation.](../images/tutorials/relationship/edit-relationship-dialog.png)

## Filtrera och söka efter relationer {#filter-and-search}

Du kan filtrera och söka efter specifika relationer inom dina scheman från fliken [!UICONTROL Relationships] på arbetsytan i [!UICONTROL Schemas]. Du kan använda den här vyn för att snabbt hitta och hantera dina relationer. Läs dokumentet om [att utforska schemaresurser](../ui/explore.md#lookup) för detaljerade instruktioner om filtreringsalternativen.

![Fliken Relationer på arbetsytan Scheman.](../images/tutorials/relationship-b2b/relationship-tab.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en 1:1-relation mellan två scheman med hjälp av [!DNL Schema Editor]. Anvisningar om hur du definierar relationer med API:t finns i självstudiekursen [om hur du definierar en relation med API:t för schemaregister](relationship-api.md).
