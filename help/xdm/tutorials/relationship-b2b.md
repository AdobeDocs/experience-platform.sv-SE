---
title: Definiera en relation mellan två scheman i kunddataplattformen B2B Edition i realtid
description: Lär dig hur du definierar en många-till-ett-relation mellan två scheman i Real-time Customer Data Platform B2B Edition.
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Definiera en relation mellan två scheman i Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition är för närvarande i betaversion. Dokumentationen och funktionerna kan komma att ändras.

>[!NOTE]
>
>Om du inte använder Real-time Customer Data Platform B2B Edition läser du i guiden [skapa en annan relation än B2B](./relationship-ui.md) istället.

Real-time Customer Data Platform B2B Edition innehåller flera Experience Data Model-klasser (XDM) som samlar in grundläggande B2B-datatabeller, inklusive [konton](../classes/b2b/business-account.md), [möjligheter](../classes/b2b/business-opportunity.md), [kampanjer](../classes/b2b/business-campaign.md) med mera. Genom att skapa scheman som baseras på dessa klasser och aktivera dem för användning i [kundprofil för realtid](../../profile/home.md), kan du sammanfoga data från olika källor till en enhetlig representation som kallas ett unionsschema.

Unionsscheman kan dock bara innehålla fält som hämtats av scheman som delar samma klass. Det är här som schemarelationer kommer in. Genom att implementera relationer i dina B2B-scheman kan du beskriva hur dessa affärsenheter relaterar till varandra och kan inkludera attribut från flera klasser i fall där segmentering används längre fram i kedjan.

I följande diagram visas ett exempel på hur de olika B2B-klasserna kan relatera till varandra i en grundläggande implementering:

![B2B-klassrelationer](../images/tutorials/relationship-b2b/classes.png)

I den här självstudiekursen beskrivs stegen för att definiera ett många-till-ett-förhållande mellan två scheman i CDP B2B Edition i realtid.

>[!NOTE]
>
>I den här självstudiekursen fokuseras på hur du manuellt skapar relationer mellan B2B-scheman i plattformsgränssnittet. Om du hämtar in data från en B2B-källanslutning kan du använda ett verktyg för automatisk generering för att skapa nödvändiga scheman, identiteter och relationer i stället. Mer information om hur du använder verktyget för automatisk generering](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) finns i källdokumentationen för B2B-namnutrymmen och scheman.[

## Komma igång

Den här självstudiekursen kräver en arbetsförståelse för [!DNL XDM System] och Schemaredigeraren i gränssnittet för [!DNL Experience Platform]. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM System i Experience Platform](../home.md): En översikt över XDM och dess implementering i  [!DNL Experience Platform].
* [Grundläggande om schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [Skapa ett schema med [!DNL Schema Editor]](create-schema-ui.md): En självstudiekurs som beskriver grunderna i hur du skapar och redigerar scheman i användargränssnittet.

## Definiera en källa och ett målschema

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. I demonstrationssyfte skapar den här självstudien en relation mellan affärsmöjligheter (som definieras i ett [!DNL Opportunities]-schema) och deras associerade företagskonto (som definieras i ett [!DNL Accounts]-schema).

Schemarelationer representeras av ett dedikerat fält i ett **källschema** som refererar till det primära identitetsfältet i ett **målschema**. I följande steg fungerar &quot;[!DNL Opportunities]&quot; som källschema, medan &quot;[!DNL Accounts]&quot; fungerar som målschema.

### Identiteter i B2B-relationer

För att kunna etablera en relation måste båda scheman ha definierade primära identiteter och vara aktiverade för [!DNL Real-time Customer Profile]. När du anger en primär identitet för en B2B-enhet bör du tänka på att strängbaserade enhets-ID:n kan överlappa om du samlar in dem över olika system eller platser, vilket kan leda till datakonflikter i Platform.

För att ta hänsyn till detta innehåller alla standardklasser av B2B nyckelfält som överensstämmer med datatypen [[!UICONTROL B2B Source]](../data-types/b2b-source.md). Den här datatypen innehåller fält för en strängidentifierare för B2B-enheten tillsammans med annan sammanhangsberoende information om identifierarens källa. Ett av dessa fält, `sourceKey`, sammanfogar värdena för de andra fälten i datatypen för att skapa en helt unik identifierare för entiteten. Det här fältet ska alltid användas som primär identitet för B2B-entitetsscheman.

![sourceKey-fält](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>När [du anger ett XDM-fält som en identitet](../ui/fields/identity.md) måste du ange ett identitetsnamnutrymme för att definiera identiteten under. Detta kan vara ett standardnamnutrymme från Adobe eller ett anpassat namnutrymme som definieras av din organisation. I praktiken är namnutrymmet helt enkelt en kontextuell sträng och kan anges till vilket värde som helst, förutsatt att det är användbart för din organisation för att kategorisera identitetstypen. Mer information finns i översikten för [identitetsnamnutrymmen](../../identity-service/namespaces.md).

I följande avsnitt beskrivs strukturen för varje schema som används i den här självstudiekursen innan en relation har definierats. Observera var de primära identiteterna har definierats i schemastrukturen och vilka anpassade namnutrymmen de använder.

### [!DNL Opportunities] schema

Källschemat [!DNL Opportunities] är baserat på klassen [!UICONTROL XDM Business Opportunity]. Ett av fälten som tillhandahålls av klassen, `opportunityKey`, fungerar som identifierare för schemat. Fältet `sourceKey` under `opportunityKey`-objektet anges som schemats primära identitet under ett anpassat namnområde med namnet [!DNL B2B Opportunity].
Som framgår av **[!UICONTROL Schema Properties]** har schemat aktiverats för användning i [!DNL Real-time Customer Profile].

![Schema för affärsmöjligheter](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Målschemat [!DNL Accounts] är baserat på klassen [!UICONTROL XDM Account]. Fältet `accountKey` på rotnivå innehåller det `sourceKey` som fungerar som dess primära identitet under ett anpassat namnutrymme med namnet [!DNL B2B Account]. Det här schemat har också aktiverats för användning i profilen.

![Kontoschema](../images/tutorials/relationship-b2b/accounts.png)

## Definiera ett relationsfält för källschemat {#relationship-field}

För att kunna definiera en relation mellan två scheman måste källschemat ha ett dedikerat fält som refererar till målschemats primära identitet. StandardB2B-klasser innehåller dedikerade källnyckelfält för vanliga affärsföretag. Klassen [!UICONTROL XDM Business Opportunity] innehåller till exempel källnyckelfält för ett relaterat konto (`accountKey`) och en relaterad kampanj (`campaignKey`). Du kan också lägga till andra [!UICONTROL B2B Source]-fält i schemat genom att använda anpassade fältgrupper om du behöver fler än standardkomponenterna.

>[!NOTE]
>
>För närvarande kan endast många-till-ett-relationer definieras från ett källschema till ett målschema. För en-till-många-relationer måste du definiera relationsfältet i schemat som representerar&quot;många&quot;.

Om du vill ange ett relationsfält väljer du pilikonen (![pilikon](../images/tutorials/relationship-b2b/arrow.png)) bredvid fältet i fråga på arbetsytan. När det gäller schemat [!DNL Opportunities] är det här `accountKey.sourceKey`-fältet eftersom målet är att upprätta en många-till-ett-relation med ett konto.

![Relationsknapp](../images/tutorials/relationship-b2b/relationship-button.png)

En dialogruta visas där du kan ange information om relationen. Relationstypen ställs automatiskt in på **[!UICONTROL Many-to-one]**.

![Dialogrutan Relation](../images/tutorials/relationship-b2b/relationship-dialog.png)

Använd sökfältet under **[!UICONTROL Reference Schema]** för att hitta namnet på målschemat. När du markerar målschemats namn uppdateras fältet **[!UICONTROL Reference Identity Namespace]** automatiskt till namnområdet för schemats primära identitet.

![Referensschema](../images/tutorials/relationship-b2b/reference-schema.png)

Under **[!UICONTROL Relationship Name From Current Schema]** och **[!UICONTROL Relationship Name From Reference Schema]** anger du egna namn för relationen i kontexten för käll- respektive målscheman. När du är klar väljer du **[!UICONTROL Save]** för att tillämpa ändringarna och spara schemat.

![Relationsnamn](../images/tutorials/relationship-b2b/relationship-name.png)

Arbetsytan visas igen med relationsfältet markerat med det egna namn du angav tidigare. Relationsnamnet visas även under den vänstra listen för enkel referens.

![Relation används](../images/tutorials/relationship-b2b/relationship-applied.png)

Om du visar strukturen för målschemat visas relationsmarkören bredvid schemats primära identitetsfält och i den vänstra listen.

![Markör för målschemarelation](../images/tutorials/relationship-b2b/destination-relationship.png)

## Nästa steg

I den här självstudiekursen har du skapat en många-till-ett-relation mellan två scheman med [!DNL Schema Editor]. När data har importerats med datauppsättningar som baseras på dessa scheman och data har aktiverats i datalagret för profilen, kan du använda attribut från båda scheman för användning av segmentering i flera klasser. Mer information finns i dokumentationen om CDP B2B Edition i realtid.
