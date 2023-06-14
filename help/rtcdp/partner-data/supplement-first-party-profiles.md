---
title: (Beta) Komplettera förstapartsprofiler med attribut som tillhandahålls av partners
description: Lär er hur ni kompletterar förstahandsprofiler med attribut från betrodda datapartners för att förbättra er datamängd, få nya insikter i er kundbas och optimera målgrupperna bättre.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 2a072ce9351a84263a50597967b994162de18d81
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---

# Komplettera förstapartsprofiler med attribut som tillhandahålls av partners

>[!AVAILABILITY]
>
>* Den här betafunktionen är tillgänglig för kunder som har licens för Real-Time CDP (App Service), Adobe Experience Platform Activation, CDP i realtid, Real-Time CDP Prime, Real-Time CDP Ultimate. Läs mer om dessa paket i [produktbeskrivningar](https://helpx.adobe.com/legal/product-descriptions.html) och kontakta Adobe för mer information.

Komplettera förstahandsprofiler med attribut från betrodda datapartners för att förbättra er grund för data och få nya insikter om er kundbas och få bättre målgruppsoptimering.

![Förbättrade profiler med attribut som tillhandahålls av partners använder en omfattande visuell översikt.](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## Krav och planering {#prerequisites-and-planning}

När du funderar på att komplettera dina egna förstahandsprofiler med attribut från datapartners, bör du diskutera och ta upp följande detaljer om dataanrikningsslingan med datapartnern:

* Fundera på var målgruppslistan ska exporteras från Real-Time CDP och delas med dataleverantören. Platsen måste ha stöd för filexport.
* Vilka identifierare förväntas av dataleverantören så att de kan skikta på ytterligare attribut?
* Hur kommer filen som innehåller attribut som tillhandahållits av partner att hämtas tillbaka till CDP i realtid? Filerna kan till exempel importeras via molnlagringskällans anslutningar, som [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) eller [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Hur lång tid har du på dig att förnya attribut som tillhandahållits av partners i Real-Time CDP?

>[!WARNING]
>
>De ytterligare attribut som partnern lägger in i Real-Time CDP påverkar *genomsnittlig profilrikedom*. Läs [Real-time Customer Data Platform produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) för mer information om profilrikedom.

## Hur man uppnår detta: överblick på hög nivå {#achieve-the-use-case-high-level}

![Förbättrade profiler med attribut som tillhandahålls av partners använder en omfattande visuell översikt.](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. Som **kund** licensierar du attribut från **datapartner**.
2. Som **kund** kan ni utöka profildata och styrningsmodell för att passa **partner**-provided-attribut.
3. Som **kund** kan ni ta med er de målgrupper ni vill ska berikas med datapartnern. Vanligtvis är dessa målgrupper inmatade med identifierare som PII-element (Personally Identiitable Information) som e-post, namn, adress och andra.
4. The **partner** lägger till licensierade attribut för de profiler som de kan matcha mot. Alternativt kan du [Partner-ID](/help/identity-service/namespaces.md) kan inkluderas och importeras i partneromfångets ID-namnutrymme.
5. Som **kund** läser du in attribut från datapartnern i kundprofiler i Real-Time CDP.

## Hur man uppnår detta: Stegvisa instruktioner {#step-by-step-instructions}

Läs igenom avsnitten nedan som innehåller länkar till ytterligare dokumentation för att slutföra varje steg i översikten ovan.

### Licensattribut från partnern {#license-attributes-from-partner}

Det här steget beskrivs i [krav](#prerequisites-and-planning) och Adobe antar att ni har rätt avtalsavtal med betrodda dataleverantörer för att utöka era förstahandsprofiler.

### Utöka era profildata och styrningsmodeller för att passa partnertillhandahållna attribut. {#extend-governance-model}

Nu utökar ni datahanteringsramverket i Real-Time CDP för att passa partnerattribut.

Du kan skapa ett nytt schema för **[!UICONTROL XDM Individual Profile]** eller utöka ett befintligt schema av samma typ för att inkludera attribut som tillhandahålls av partner. Adobe rekommenderar starkt att du skapar ett nytt schema med en ny uppsättning fältgrupper som bäst representerar de extra attributen från dataleverantören. Detta garanterar att dina dataram är rena och kan utvecklas oberoende av varandra.

Om du vill inkludera attribut som tillhandahålls av partner i ett schema kan du antingen skapa en ny fältgrupp med de attribut du förväntar dig, eller så kan du använda en av de förkonfigurerade fältgrupperna som tillhandahålls av Adobe.

Läs dokumentationssidorna nedan för mer information:

* [Grundläggande om schemakomposition](/help/xdm/schema/composition.md)
* [Översikt över [!UICONTROL XDM Individual Profile] class](/help/xdm/classes/individual-profile.md)
* [Skapa och redigera scheman i användargränssnittet](/help/xdm/ui/resources/schemas.md)
* [Skapa och redigera schemafältgrupper i användargränssnittet](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

I det här steget bör du också tänka på hur er datastyrningsmodell ändras när ni utökar er datahanteringsstrategi så att den omfattar data från tredje part från partnern. Ta en titt på vad du bör tänka på i dokumentationslänkarna nedan:

* (**Kommer snart**) Förvara tredjepartsdata i en separat datauppsättning så att det blir enkelt att ta bort dem och ångra integreringar.
* (**Kommer snart**) Använd [TTL (Time-to-live)](/help/hygiene/ui/dataset-expiration.md) på datauppsättningen för kunder som köpt tillägget för datahygien.
* (**Kommer snart**) Var försiktig när du skapar härledda datauppsättningar som hämtar in data från tredje part, eftersom den enda lösningen för att ta bort data från tredje part är att ta bort hela den härledda datauppsättningen när de har blandats ihop.

>[!TIP]
>
>Om du väljer att komplettera dina kundprofiler med en personbaserad identifierare från dataleverantören kan du skapa en ny identitetstyp av typen **[[!UICONTROL Partner ID]](/help/identity-service/namespaces.md)**.
>
>Läs mer om partner-ID i [Avsnitt för identitetstyper](/help/identity-service/namespaces.md).
>Läs om [definiera identitetsfält](/help/xdm/ui/fields/identity.md) i användargränssnittet i Experience Platform.

### Exportera målgrupper som du vill ska berikas när du stänger av Personal Identified Information (PII) eller hashed-PII {#export-audiences}

Exportera de målgrupper som ni vill att partnern ska berika. Använd molnlagringsdestinationer som tillhandahålls av CDP i realtid, till exempel Amazon S3 eller SFTP. Läs följande dokumentationssidor för att slutföra det här steget:

* [Amazon S3-mål](/help/destinations/catalog/cloud-storage/amazon-s3.md) dokumentsida
* [SFTP-mål](/help/destinations/catalog/cloud-storage/sftp.md) dokumentsida
* Så här gör du [ansluta till ett mål](/help/destinations/ui/connect-destination.md)
* Så här gör du [exportera data till ett molnlagringsmål](/help/destinations/ui/activate-batch-profile-destinations.md)

### Din datapartner bifogar licensierade attribut för de profiler som de kan matcha mot {#partner-appends-attributes}

I det här steget lägger din datapartner till licensierade attribut för den exporterade målgruppen. Utdata är vanligtvis tillgängliga som en platt fil som kan importeras tillbaka till Real-Time CDP. Läs mer om [importera filer till Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP lägger in berikade attribut i kundprofilen {#ingest-data}

Ni måste nu importera data från partnern via en källanslutning för att få tillbaka de berikade data till Real-Time CDP och komplettera era profiler med data från partnern.

Några rekommenderade källanslutningar för detta ändamål kan vara:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Begränsningar och felsökning {#limitations-and-troubleshooting}

Observera följande begränsningar när du utforskar användningsfallet som beskrivs på den här sidan:

* Om du väljer att använda partner-ID:n ska du vara medveten om att dessa ID:n inte används när du skapar dina [identitetsdiagram](/help/identity-service/ui/identity-graph-viewer.md).

## Andra användningsområden som uppnås genom stöd för partnerdata {#other-use-cases}

Upptäck fler användningsfall tack vare partnerdatastöd i Real-Time CDP:

* (**Kommer snart**) [!BADGE Beta]{type=Informative}**Utnyttja partnerstöd** för att personalisera upplevelser på plats under besöket och för återannonsering på annan plats, utan att användaren behöver autentisera sig eller ha en tidigare historia med varumärket.
* (**Kommer snart**) [!BADGE Beta]{type=Informative}**Utökad aktivering** använda partner-ID:n för att publicera ekosystem som inte accepterar PII eller hashas PII.