---
title: Komplettera förstapartsprofiler med attribut som tillhandahålls av partners
description: Lär er hur ni kompletterar förstahandsprofiler med attribut från betrodda datapartners för att förbättra er datamängd, få nya insikter i er kundbas och optimera målgrupperna bättre.
feature: Use Cases, Profile Enrichment
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: 9737508bd8435f4edf0e60a3559c1b4352ccb29f
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 3%

---

# Komplettera förstapartsprofiler med attribut som tillhandahålls av partners

>[!AVAILABILITY]
>
>* Den här funktionen är tillgänglig för kunder som har licens för Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Läs mer om de här paketen i [produktbeskrivningarna](https://helpx.adobe.com/legal/product-descriptions.html) och kontakta din Adobe-representant för mer information.

Komplettera förstahandsprofiler med attribut från betrodda datapartners för att förbättra er grund för data och få nya insikter om er kundbas och få bättre målgruppsoptimering.

![Förbättrade profiler med attribut som tillhandahålls av partner använder en synlig översikt på hög nivå.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Varför ska man tänka på det här användningsexemplet? {#why-this-use-case}

De flesta varumärken, även de som är fullmatade med förstahandsdata, kan dra nytta av att effektivisera sina data och få en bättre förståelse för kunderna, deras beteenden, mönster och önskemål.

Adobe Real-time Customer Data Platform kan hjälpa varumärken att på ett ansvarsfullt sätt komplettera sina egna data med värdefulla insikter, identifierare och attribut från en eller flera betrodda partners.

Adobe förstår att det inte finns någon strategi som passar alla och som möjliggör smidig interoperabilitet med data- och identitetspartners för att främja individanpassad och genomtänkt interaktion i alla faser av kundlivscykeln. Dessa funktioner stöds av ett betrott ramverk för datastyrning som ger en nyanserad kontroll över var och hur partnerdata används. Du kanske vill använda partnerinsikter för segmentering, men inte för personalisering.

Följ till exempel de steg som beskrivs i det här användningsexemplet när du behöver förbättra dina kundregister med demografiska och avsiktliga signaler.

## Förutsättningar och planering

När du funderar på att komplettera dina egna förstahandsprofiler med attribut från datapartners, bör du diskutera och ta upp följande detaljer om dataanrikningsslingan med datapartnern:

* Fundera på var målgruppslistan ska exporteras från Real-Time CDP och delas med dataleverantören. Platsen måste ha stöd för filexport.
* Vilka identifierare förväntas av dataleverantören så att de kan skikta på ytterligare attribut?
* Hur kommer filen som innehåller attribut som tillhandahållits av partner att hämtas tillbaka till Real-Time CDP? Filerna kan till exempel importeras via molnlagringskällans anslutningar som [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) eller [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Hur lång tid har du på dig att förnya attribut som tillhandahållits av partners i Real-Time CDP?

>[!WARNING]
>
>De ytterligare attribut som partnern tillhandahåller och som hämtas in till Real-Time CDP påverkar din *genomsnittliga profilrikedom*. Läs [Real-time Customer Data Platform Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) om du vill ha mer information om profilrikedom.

## Videogenomgång {#video-walkthrough}

I videosjälvstudiekursen nedan får du en genomgång av hur du kan komplettera förstahandsmålgrupper med attribut från partners:

>[!VIDEO](https://video.tv.adobe.com/v/3423075/?learn=on)

## Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

![Förbättrade profiler med attribut som tillhandahålls av partner använder en synlig översikt på hög nivå.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. Som **kund** licensierar du attribut från **dataparten**.
2. Som **kund** utökar du dina profildata och styrningsmodeller så att de passar attribut som tillhandahålls av **partner**.
3. Som **kund** tar du med dig de målgrupper som du vill ska berikas med datapartnern. Vanligtvis är dessa målgrupper inmatade med identifierare som PII-element (Personally Identiitable Information) som e-post, namn, adress och andra.
4. **partnern** lägger till licensierade attribut för de profiler som de kan matcha mot. Ett [partner-ID](/help/identity-service/features/namespaces.md) kan också inkluderas och hämtas till partneromfångets ID-namnområde.
5. Som **kund** läser du in attribut från dataparten till kundprofiler i Real-Time CDP.

## Så här uppnår du användningsfallet: stegvisa instruktioner {#step-by-step-instructions}

Läs igenom avsnitten nedan som innehåller länkar till ytterligare dokumentation för att slutföra varje steg i översikten ovan.

### Licensattribut från partnern {#license-attributes-from-partner}

Det här steget beskrivs i [förutsättningarna](#prerequisites-and-planning) och Adobe antar att du har rätt avtalsavtal på plats med betrodda dataleverantörer för att förstärka dina förstahandsprofiler.

### Utöka era profildata och styrningsmodeller för att passa partnertillhandahållna attribut. {#extend-governance-model}

Nu utökar ni datahanteringsramverket i Real-Time CDP för att passa partnerattribut.

Du har möjlighet att skapa ett nytt schema för klassen **[!UICONTROL XDM Individual Profile]** eller utöka ett befintligt schema av samma typ så att det inkluderar attribut som tillhandahålls av partner. Adobe rekommenderar starkt att du skapar ett nytt schema med en ny uppsättning fältgrupper som bäst representerar de extra attributen från dataleverantören. Detta garanterar att dina dataram är rena och kan utvecklas oberoende av varandra.

Om du vill inkludera attribut som tillhandahålls av partner i ett schema kan du antingen skapa en ny fältgrupp med de attribut du förväntar dig, eller så kan du använda en av de förkonfigurerade fältgrupperna som tillhandahålls av Adobe.

Läs dokumentationssidorna nedan för mer information:

* [Grundläggande om schemakomposition](/help/xdm/schema/composition.md)
* [Översikt över klassen [!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md)
* [Skapa och redigera scheman i användargränssnittet](/help/xdm/ui/resources/schemas.md)
* [Skapa och redigera schemafältgrupper i användargränssnittet](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

I det här steget bör du också tänka på hur er datastyrningsmodell ändras när ni utökar er datahanteringsstrategi så att den omfattar data från tredje part från partnern. Ta en titt på vad du bör tänka på i dokumentationslänkarna nedan:

* (**Kommer snart**) Håll tredjepartsdata i en separat datauppsättning så att det blir enkelt att ta bort och ångra integreringar.
* (**Kommer snart**) Använd funktionen [utgångsdatum](/help/hygiene/ui/dataset-expiration.md) i datauppsättningen för klienter som köpt tillägget för datahygien.
* (**Kommer snart**) Var försiktig när du skapar härledda datauppsättningar som hämtar in data från tredje part, eftersom den enda lösningen för att ta bort data från tredje part är att ta bort hela den härledda datauppsättningen när dessa har blandats.

>[!TIP]
>
>Om du väljer att komplettera dina kundprofiler med en personbaserad identifierare från dataleverantören kan du skapa en ny identitetstyp av typen **[[!UICONTROL Partner ID]](/help/identity-service/features/namespaces.md)**.
>
>Läs mer om partner-ID i avsnittet [identitetstyper](/help/identity-service/features/namespaces.md).
>Läs om [hur du definierar identitetsfält](/help/xdm/ui/fields/identity.md) i användargränssnittet i Experience Platform.

### Exportera målgrupper som du vill ska berikas när du stänger av Personal Identified Information (PII) eller hashed-PII {#export-audiences}

Exportera de målgrupper som ni vill att partnern ska berika. Använd molnlagringsdestinationer som tillhandahålls av Real-Time CDP, till exempel Amazon S3 eller SFTP. Läs följande dokumentationssidor för att slutföra det här steget:

* Dokumentationssida för [Amazon S3-målet](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [Dokumentationssida för SFTP-mål](/help/destinations/catalog/cloud-storage/sftp.md)
* [Ansluta till ett mål](/help/destinations/ui/connect-destination.md)
* Så här [exporterar du data till ett molnlagringsmål](/help/destinations/ui/activate-batch-profile-destinations.md)

### Din datapartner bifogar licensierade attribut för de profiler som de kan matcha mot {#partner-appends-attributes}

I det här steget lägger din datapartner till licensierade attribut för den exporterade målgruppen. Utdata är vanligtvis tillgängliga som en platt fil som kan importeras tillbaka till Real-Time CDP. Läs mer om att [importera filer till Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP lägger in berikade attribut i kundprofilen {#ingest-data}

Ni måste nu importera data från partnern via en källanslutning för att få tillbaka de berikade data till Real-Time CDP och komplettera era profiler med data från partnern.

Några rekommenderade källanslutningar för detta ändamål kan vara:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Begränsningar och felsökning {#limitations-and-troubleshooting}

Observera följande begränsningar när du utforskar användningsfallet som beskrivs på den här sidan:

* Om du väljer att använda partner-ID:n ska du vara medveten om att dessa ID:n inte används när du skapar [identitetsdiagrammet](/help/identity-service/features/identity-graph-viewer.md).

## Andra användningsområden som uppnås genom stöd för partnerdata {#other-use-cases}

Upptäck fler användningsfall tack vare partnerdatastöd i Real-Time CDP:

* Använd datastöd från tredje part i Real-Time CDP för att [utöka din profilbas med profiler för potentiella kunder från datapartner och engagera med dem för att förvärva eller nå nya kunder](/help/rtcdp/partner-data/prospecting.md).
* [Anpassa upplevelser på plats för okända besökare med partnerstödd besökarigenkänning](/help/rtcdp/partner-data/onsite-personalization.md) under besöket utan att användaren behöver autentisera sig eller ha en tidigare historik med varumärket.
* [Utökad aktivering av profiler för potentiella kunder och målgrupper](/help/destinations/ui/activate-prospect-audiences.md) för utvalda mål.
