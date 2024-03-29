---
keywords: Experience Platform;hem;populära ämnen;ui;UI;XDM;XDM system;Experience data model;Experience data model;experience data model;data model;data model;schema editor;schema editor;schema;schema;scheman;scheman;scheman;skapa;relation;relation;referens;referens;
solution: Experience Platform
title: Definiera en relation mellan två scheman med Schemaredigeraren
description: I det här dokumentet finns en självstudiekurs för att definiera en relation mellan två scheman med hjälp av Schemaredigeraren i användargränssnittet i Experience Platform.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1137'
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

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Definiera dessa relationer inom strukturen för din [!DNL Experience Data Model] (XDM)-scheman gör att ni kan få komplexa insikter om era kunddata.

När schemarelationer kan härledas genom användning av unionsschemat och [!DNL Real-Time Customer Profile]gäller detta endast scheman som delar samma klass. För att upprätta en relation mellan två scheman som tillhör olika klasser måste ett dedikerat relationsfält läggas till i ett källschema, som refererar till identiteten för det andra relaterade schemat.

>[!NOTE]
>
>Om både käll- och målschemat tillhör samma klass bör ett dedikerat relationsfält **not** användas. I det här fallet använder du gränssnittet för unionsschemat för att se relationen. Instruktioner om hur du gör detta finns i [visa relationer](../../profile/ui/union-schema.md#view-relationships) i gränssnittsguiden för unionsschemat.

I det här dokumentet finns en självstudiekurs för att definiera en relation mellan två scheman med hjälp av Schemaredigeraren i [!DNL Experience Platform] användargränssnitt. Anvisningar om hur du definierar schemarelationer med API:t finns i självstudiekursen om [definiera en relation med API:t för schemaregister](relationship-api.md).

>[!NOTE]
>
>Anvisningar om hur du skapar en många-till-ett-relation i Adobe Real-time Customer Data Platform B2B Edition finns i guiden på [skapa B2B-relationer](./relationship-b2b.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av [!DNL XDM System] och Schemaredigeraren i [!DNL Experience Platform] Gränssnitt. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM-system i Experience Platform](../home.md): En översikt över XDM och dess implementering i [!DNL Experience Platform].
* [Grunderna för schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [Skapa ett schema med [!DNL Schema Editor]](create-schema-ui.md): En självstudiekurs som handlar om grunderna i att arbeta med [!DNL Schema Editor].

## Definiera en källa och ett referensschema

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. I den här självstudiekursen skapas en relation mellan medlemmar i en organisations lojalitetsprogram (definieras i en[!DNL Loyalty Members]schema) och deras favorithotell (definieras i en[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>För att upprätta en relation måste båda scheman ha definierade primära identiteter och aktiveras för [!DNL Real-Time Customer Profile]. Se avsnittet om [aktivera ett schema för användning i profil](./create-schema-ui.md#profile) i självstudiekursen för att skapa scheman om du behöver hjälp med hur du konfigurerar dina scheman därefter.

Schemarelationer representeras av ett dedikerat fält i en **källschema** som pekar på ett annat fält i ett **referensschema**. I följande steg: &quot;[!DNL Loyalty Members]&quot; blir källschemat, medan &quot;[!DNL Hotels]&quot; fungerar som referensschema.

I följande avsnitt beskrivs strukturen för varje schema som används i den här självstudiekursen innan en relation har definierats.

### [!DNL Loyalty Members] schema

Källschemat &quot;[!DNL Loyalty Members]&quot; baseras på [!DNL XDM Individual Profile] klass, som innehåller fält som beskriver medlemmar i ett bonusprogram. Ett av dessa fält, `personalEmail.addess`, fungerar som primär identitet för schemat under [!UICONTROL Email] namnutrymme. Som framgår av **[!UICONTROL Schema Properties]**, har det här schemat aktiverats för användning i [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Referensschemat &quot;[!DNL Hotels]&quot; är baserad på en anpassad &quot;[!DNL Hotels]och innehåller fält som beskriver ett hotell. För att kunna delta i en relation måste referensschemat också ha en primär identitet definierad och vara aktiverat för [!UICONTROL Profile]. I detta fall `_tenantId.hotelId`fungerar som primär identitet för schemat med hjälp av en anpassad[!DNL Hotel ID]&quot; identity namespace.

![Aktivera för profil](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Mer information om hur du skapar anpassade identitetsnamnutrymmen finns i [Identitetstjänstens dokumentation](../../identity-service/features/namespaces.md#manage-namespaces).

## Skapa en relationsfältgrupp

>[!NOTE]
>
>Det här steget krävs bara om källschemat inte har ett dedikerat fält av strängtyp som ska användas som pekare till referensschemats primära identitet. Om det här fältet redan är definierat i källschemat går du vidare till nästa steg i [definiera ett relationsfält](#relationship-field).

För att kunna definiera en relation mellan två scheman måste källschemat ha ett dedikerat fält som anger referensschemats primära identitet. Du kan lägga till det här fältet i källschemat genom att skapa en ny schemafältgrupp eller utöka en befintlig.

När det gäller [!DNL Loyalty Members] schema, ett nytt `preferredHotel` fältet läggs till för att ange den lojalitetsmedlems önskade hotell för företagsbesök. Börja med att välja plusikonen (**+**) bredvid källschemats namn.

![](../images/tutorials/relationship/loyalty-add-field.png)

En ny fältplatshållare visas på arbetsytan. Under **[!UICONTROL Field properties]**, ange ett fältnamn och ett visningsnamn för fältet och ange dess typ till &quot;[!UICONTROL String]&quot;. Under **[!UICONTROL Assign to]** väljer du en befintlig fältgrupp som ska utökas eller skriver in ett unikt namn för att skapa en ny fältgrupp. I det här fallet en ny[!DNL Preferred Hotel]fältgruppen skapas.

![](../images/tutorials/relationship/relationship-field-details.png)

När du är klar väljer du **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Den uppdaterade `preferredHotel` visas på arbetsytan under `_tenantId` eftersom det är ett anpassat fält. Välj **[!UICONTROL Save]** för att slutföra ändringarna av schemat.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definiera ett relationsfält för källschemat {#relationship-field}

När ett dedikerat referensfält har definierats i källschemat kan du ange det som ett relationsfält.

>[!NOTE]
>
>Stegen nedan beskriver hur du definierar ett relationsfält med kontrollerna för höger skena på arbetsytan. Om du har tillgång till Real-Time CDP B2B Edition kan du även definiera en personlig relation med [samma dialogruta](./relationship-b2b.md#relationship-field) som när du skapar många-till-en-relationer.

Välj `preferredHotel` på arbetsytan och rulla sedan nedåt under **[!UICONTROL Field properties]** tills **[!UICONTROL Relationship]** visas. Markera kryssrutan för att visa de parametrar som krävs för att konfigurera ett relationsfält.

![](../images/tutorials/relationship/relationship-checkbox.png)

Välj listrutan för **[!UICONTROL Reference schema]** och välj referensschema för relationen (&quot;[!DNL Hotels]&quot; i detta exempel). Under **[!UICONTROL Reference identity namespace]** markerar du namnområdet för referensschemats identitetsfält (i det här fallet &quot;[!DNL Hotel ID]&quot;). Välj **[!UICONTROL Apply]** när du är klar.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

The `preferredHotel` fältet markeras nu som en relation på arbetsytan med namnet på referensschemat. Välj **[!UICONTROL Save]** för att spara ändringarna och slutföra arbetsflödet.

![](../images/tutorials/relationship/relationship-save.png)

## Nästa steg

I den här självstudiekursen har du skapat en 1:1-relation mellan två scheman med hjälp av [!DNL Schema Editor]. Anvisningar om hur du definierar relationer med API:t finns i självstudiekursen om [definiera en relation med API:t för schemaregister](relationship-api.md).
