---
title: Definiera en relation mellan två scheman i Real-time Customer Data Platform B2B Edition
description: Lär dig hur du definierar en många-till-ett-relation mellan två scheman i Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 0%

---

# Definiera en många-till-ett-relation mellan två scheman i Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Referensschema"
>abstract="Välj det schema som du vill skapa en relation med. Beroende på schemats klass kan den även ha befintliga relationer med andra enheter i B2B-kontexten. Läs dokumentationen för att lära dig hur B2B-schemaklasser relaterar till varandra."

Adobe Real-time Customer Data Platform B2B Edition innehåller flera XDM-klasser (Experience Data Model) som samlar in grundläggande B2B-datatabeller, inklusive [konton](../classes/b2b/business-account.md), [möjligheter](../classes/b2b/business-opportunity.md), [kampanjer](../classes/b2b/business-campaign.md), med mera. Genom att skapa scheman baserade på dessa klasser och aktivera dem för användning i [Kundprofil i realtid](../../profile/home.md)kan du sammanfoga data från olika källor till en enhetlig representation som kallas för ett unionsschema.

Unionsscheman kan dock bara innehålla fält som hämtats av scheman som delar samma klass. Det är här som schemarelationer kommer in. Genom att implementera relationer i dina B2B-scheman kan du beskriva hur dessa affärsenheter relaterar till varandra och kan inkludera attribut från flera klasser i fall där segmentering sker nedåt.

I följande diagram visas ett exempel på hur de olika B2B-klasserna kan relatera till varandra i en grundläggande implementering:

![B2B-klassrelationer](../images/tutorials/relationship-b2b/classes.png)

I den här självstudiekursen beskrivs stegen för att definiera ett många-till-ett-förhållande mellan två scheman i Real-Time CDP B2B Edition.

>[!NOTE]
>
>Om du inte använder Real-time Customer Data Platform B2B Edition eller vill skapa en personlig relation läser du i guiden på [skapa en personlig relation](./relationship-ui.md) i stället.
>
>I den här självstudiekursen fokuseras på hur du manuellt skapar relationer mellan B2B-scheman i plattformsgränssnittet. Om du hämtar in data från en B2B-källanslutning kan du använda ett verktyg för automatisk generering för att skapa nödvändiga scheman, identiteter och relationer i stället. I källdokumentationen om B2B-namnutrymmen och scheman finns mer information om [med verktyget för autogenerering](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av [!DNL XDM System] och Schemaredigeraren i [!DNL Experience Platform] Gränssnitt. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM-system i Experience Platform](../home.md): En översikt över XDM och dess implementering i [!DNL Experience Platform].
* [Grunderna för schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [Skapa ett schema med [!DNL Schema Editor]](create-schema-ui.md): En självstudiekurs som beskriver grunderna i hur du skapar och redigerar scheman i användargränssnittet.

## Definiera en källa och ett referensschema

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. I den här självstudiekursen skapas en relation mellan affärsmöjligheter (definieras i en[!DNL Opportunities]&quot; schema) och deras associerade företagskonto (definieras i en &quot;[!DNL Accounts]&quot; schema).

Schemarelationer representeras av ett dedikerat fält i en **källschema** som refererar till det primära identitetsfältet för en **referensschema**. I följande steg: &quot;[!DNL Opportunities]&quot; fungerar som källschema, medan &quot;[!DNL Accounts]&quot; fungerar som referensschema.

### Identiteter i B2B-relationer

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Namnutrymme för referensidentitet"
>abstract="Namnutrymmet (typen) för referensschemats primära identitetsfält. Referensschemat måste ha ett etablerat primärt identitetsfält för att kunna delta i en relation. Mer information om identiteter i B2B-relationer finns i dokumentationen."

För att en relation ska kunna upprättas måste referensschemat ha en definierad primär identitet. När du anger en primär identitet för en B2B-enhet bör du tänka på att strängbaserade enhets-ID:n kan överlappa om du samlar in dem över olika system eller platser, vilket kan leda till datakonflikter i Platform.

För att ta hänsyn till detta innehåller alla standardklasser för B2B&quot;nyckelfält&quot; som följer [[!UICONTROL B2B Source] datatyp](../data-types/b2b-source.md). Den här datatypen innehåller fält för en strängidentifierare för B2B-enheten tillsammans med annan sammanhangsberoende information om identifierarens källa. Ett av dessa fält, `sourceKey`, sammanfogar värdena för de andra fälten i datatypen så att en helt unik identifierare skapas för entiteten. Det här fältet ska alltid användas som primär identitet för B2B-entitetsscheman.

![sourceKey-fält](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>När [ange ett XDM-fält som en identitet](../ui/fields/identity.md)måste du ange ett ID-namnutrymme för att definiera identiteten under. Detta kan vara ett standardnamnutrymme från Adobe eller ett anpassat namnutrymme som definieras av din organisation. I praktiken är namnutrymmet helt enkelt en kontextuell sträng och kan anges till vilket värde som helst, förutsatt att det är användbart för din organisation för att kategorisera identitetstypen. Se översikten på [identitetsnamnutrymmen](../../identity-service/features/namespaces.md) för mer information.

I följande avsnitt beskrivs strukturen för varje schema som används i den här självstudiekursen innan en relation har definierats. Observera var de primära identiteterna har definierats i schemastrukturen och vilka anpassade namnutrymmen de använder.

### [!DNL Opportunities] schema

Källschemat &quot;[!DNL Opportunities]&quot; baseras på [!UICONTROL XDM Business Opportunity] klassen. Ett av fälten i klassen, `opportunityKey`, fungerar som identifierare för schemat. I synnerhet `sourceKey` fält under `opportunityKey` objektet anges som schemats primära identitet under ett anpassat namnområde som kallas [!DNL B2B Opportunity].

Som framgår av **[!UICONTROL Schema Properties]**, har det här schemat aktiverats för användning i [!DNL Real-Time Customer Profile].

![Schema för affärsmöjligheter](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Referensschemat &quot;[!DNL Accounts]&quot; baseras på [!UICONTROL XDM Account] klassen. Rotnivån `accountKey` fältet innehåller `sourceKey` som fungerar som sin primära identitet under ett anpassat namnutrymme som kallas [!DNL B2B Account]. Det här schemat har också aktiverats för användning i profilen.

![Kontoschema](../images/tutorials/relationship-b2b/accounts.png)

## Definiera ett relationsfält för källschemat {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Relationsnamn från aktuellt schema"
>abstract="En etikett som beskriver relationen från det aktuella schemat till referensschemat (till exempel Relaterat konto). Den här etiketten används i profil och segmentering för att ge kontext till data från relaterade B2B-enheter. Mer information om hur du skapar B2B-schemarelationer finns i dokumentationen."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Relationsnamn från referensschema"
>abstract="En etikett som beskriver relationen från referensschemat till det aktuella schemat (till exempel Relaterade affärsmöjligheter). Den här etiketten används i profil och segmentering för att ge kontext till data från relaterade B2B-enheter. Mer information om hur du skapar B2B-schemarelationer finns i dokumentationen."

För att kunna definiera en relation mellan två scheman måste källschemat ha ett dedikerat fält som anger den primära identiteten för referensschemat. StandardB2B-klasser innehåller dedikerade källnyckelfält för vanliga affärsföretag. Till exempel [!UICONTROL XDM Business Opportunity] klassen innehåller källnyckelfält för ett relaterat konto (`accountKey`) och en relaterad kampanj (`campaignKey`). Du kan dock även lägga till andra [!UICONTROL B2B Source] fält till schemat genom att använda anpassade fältgrupper om du behöver fler än standardkomponenterna.

>[!NOTE]
>
>För närvarande kan endast många-till-ett- och en-till-en-relationer definieras från ett källschema till ett referensschema. För en-till-många-relationer måste du definiera relationsfältet i schemat som representerar&quot;många&quot;.

Om du vill ange ett relationsfält väljer du pilen (![Pilikon](../images/tutorials/relationship-b2b/arrow.png)) bredvid fältet i fråga på arbetsytan. När det gäller [!DNL Opportunities] schema, det här är `accountKey.sourceKey` eftersom målet är att skapa en många-till-en-relation med ett konto.

![Relationsknapp](../images/tutorials/relationship-b2b/relationship-button.png)

En dialogruta visas där du kan ange information om relationen. Relationstypen ställs automatiskt in på **[!UICONTROL Many-to-one]**.

![Dialogrutan Relation](../images/tutorials/relationship-b2b/relationship-dialog.png)

Under **[!UICONTROL Reference Schema]** använder du sökfältet för att hitta namnet på referensschemat. När du markerar referensschemats namn visas **[!UICONTROL Reference Identity Namespace]** fältet uppdateras automatiskt till namnområdet för schemats primära identitet.

![Referensschema](../images/tutorials/relationship-b2b/reference-schema.png)

Under **[!UICONTROL Relationship Name From Current Schema]** och **[!UICONTROL Relationship Name From Reference Schema]**, anger egna namn för relationen i samband med käll- respektive referensscheman. När du är klar väljer du **[!UICONTROL Save]** för att tillämpa ändringarna och spara schemat.

![Relationsnamn](../images/tutorials/relationship-b2b/relationship-name.png)

Arbetsytan visas igen med relationsfältet markerat med det egna namn du angav tidigare. Relationsnamnet visas även under den vänstra listen för enkel referens.

![Relation används](../images/tutorials/relationship-b2b/relationship-applied.png)

Om du visar referensschemats struktur visas relationsmarkören bredvid schemats primära identitetsfält och i den vänstra listen.

![Markör för målschemarelation](../images/tutorials/relationship-b2b/destination-relationship.png)

## Nästa steg

I den här självstudiekursen har du skapat en många-till-ett-relation mellan två scheman med hjälp av [!DNL Schema Editor]. När data har importerats med datauppsättningar baserade på dessa scheman och data har aktiverats i datalagret kan du använda attribut från båda scheman för [användning av segmentering i flera klasser](../../rtcdp/segmentation/b2b.md).
