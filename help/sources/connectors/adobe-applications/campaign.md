---
keywords: Experience Platform;hem;populära ämnen;Adobe Campaign Managed Cloud Services;kampanj;kampanjhanterade tjänster
title: Adobe Campaign Managed Cloud Services
description: Lär dig hur du ansluter Campaign Managed Cloud Services till Experience Platform via användargränssnittet
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: 1d29cdd39075aad937d078aa116ec2f6e6ec6a56
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

Adobe Campaign Managed Cloud Services erbjuder en hanterad plattform för att utforma flerkanaliga kundupplevelser med stöd för visuell kampanjsamordning, interaktionshantering i realtid och flerkanalsmarknadsföring. Mer information finns i [Adobe Campaign v8-dokumentationen](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=sv).

Med Adobe Campaign Managed Cloud Services källanslutning kan du importera och spåra loggdata från Adobe Campaign v8 till Adobe Experience Platform. Den här kopplingen fungerar som en batchkälla inom plattformen.

## Förutsättningar

Innan du kan skapa en källanslutning för att överföra Campaign v8 till Experience Platform måste du först uppfylla följande krav:

* [Konfigurera importen av händelseloggen med Adobe Campaign klientkonsol](#view-delivery-and-tracking-log-data)
* [Skapa ett XDM ExperienceEvent-schema](#create-a-schema)
* [Skapa en datauppsättning](#create-a-dataset)

### Visa loggdata för leverans och spårning {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Du måste ha tillgång till Adobe Campaign v8 Client Console för att kunna visa dina loggdata i Campaign. Besök [dokumentationen för Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=sv-SE) om du vill ha information om hur du hämtar och installerar klientkonsolen.

Logga in på Campaign v8-instansen via klientkonsolen. Under fliken [!DNL Explorer] väljer du [!DNL Administration] och sedan [!DNL Configuration]. Välj sedan [!DNL Data schemas] och använd sedan filtret `broadLog` för namn eller etikett. I listan som visas väljer du källschemat för mottagarleveransloggarna med namnet `broadLogRcp`.

![Klientkonsolen Adobe Campaign v8 med fliken Utforskaren vald, noderna Administration, Konfiguration och Data expanderade och filtreringen angavs till &quot;bred&quot;.](./images/campaign/explorer.png)

Välj sedan fliken **Data**.

![Adobe Campaign v8-klientkonsolen med datafliken vald.](./images/campaign/data.png)

Högerklicka/tangentbordet i datapanelen för att öppna snabbmenyn. Här väljer du **Konfigurera lista..**

![Adobe Campaign v8-klientkonsolen med snabbmenyn öppen och alternativet Konfigurera lista markerat.](./images/campaign/configure.png)

Listkonfigurationsfönstret visas med ett gränssnitt där du kan lägga till önskade fält i den befintliga listan för att visa data på datapanelen.

![En lista med konfigurationer för mottagarleveransloggar som kan läggas till för visning.](./images/campaign/list-configuration.png)

Nu kan du visa mottagarnas leveransloggar, inklusive de konfigurationsfält som lagts till i föregående steg.

>[!TIP]
>
>Du kan upprepa samma steg, men filtrera efter `tracking` om du vill visa loggdata för spårningen.

![Mottagarens leveransloggar visas med information om dess senast ändrade namn, leveranskanal, interna leveransnamn och etikett.](./images/campaign/recipient-delivery-logs.png)

### Skapa ett schema {#create-a-schema}

Skapa sedan ett XDM ExperienceEvent-schema för både leveransloggar och spårningsloggar. Du måste använda fältgruppen för kampanjleveransloggar i leveransloggschemat och fältgruppen för kampanjspårningsloggar i spårningsloggschemat. Du måste också definiera fältet `externalID` som den primära identiteten för ditt schema.

>[!NOTE]
>
>Ditt XDM ExperienceEvent-schema måste vara profilaktiverat för att dina Campaign-data ska kunna importeras till [!DNL Real-Time Customer Profile].

Detaljerade instruktioner om hur du skapar ett schema finns i guiden om att [skapa ett XDM-schema i användargränssnittet](../../../xdm/tutorials/create-schema-ui.md).

### Skapa en datauppsättning {#create-a-dataset}

Slutligen måste du skapa en datauppsättning för dina scheman. Detaljerade instruktioner om hur du skapar en datauppsättning finns i guiden om att [skapa en datauppsättning i användargränssnittet](../../../catalog/datasets/user-guide.md).

## Förväntad fördröjning för Adobe Campaign Managed Cloud Services-källa {#latency}

Sluttotal latens från en Campaign-händelse till datatillgänglighet i Experience Platform är vanligtvis 15-30 minuter i standardkonfigurationer (inklusive 15 minuters replikering, export av mikrobatchar och ett schemalagt Experience Platform-dataflöde), med normala datavolymer och utan eftersläpning. Detta är en nästan realtidsprocess som uppnås genom schemalagd synkronisering av mikrobatchar (vanligtvis i tiominutersintervall), men det är inte kontinuerlig direktuppspelning.

| Scenario | Information | Förväntad fördröjning |
| --- | --- | --- |
| Kampanjhändelse genereras i en instans av en mellanleverantör/meddelandecenter | En leverans- eller spårningshändelse (skicka, öppna, klicka osv.) inträffar på en körningsnod för Campaign v8 (mitten/meddelandecenter). | Realtid i Campaign-miljön (visas för närvarande inte i Experience Platform). |
| Replikering från körningsmiljön till Campaign-marknadsföringsdatabasen | Händelsedata replikeras från mitten/meddelandecenter till Campaign-marknadsföringsdatabasen ([!DNL Snowflake] eller [!DNL Postgres], beroende på kundens storlek). Standardintegreringsmönster förutsätter ett regelbundet replikeringsjobb. | ~15 minuter, baserat på den vanliga 15-minutersperioden för replikering. |
| Exportera från Campaign-marknadsföringsdatabas till landningszon (till exempel [!DNL Data Landing Zone], [!DNL Amazon S3] eller [!DNL Azure Blob]) | Ett exportarbetsflöde (Export Service) i Campaign körs enligt ett schema för att extrahera nya/ändrade leveransloggar och spåra dem och skriva dem som mikrobatchar till en filbaserad landningszon. | Minuter, plus exportschemats intervall. |
| Experience Platform källdataflöde hämtar exporterade filer | Adobe Campaign Managed Cloud Services-källan har konfigurerats som ett batchdataflöde i Experience Platform [!DNL Flow Service]. Den skannar regelbundet in landningszonen, importerar nya filer och skriver dem i de konfigurerade ExperienceEvent-datamängderna. Övervakning visar &quot;lyckade batchar&quot; och &quot;misslyckade batchar&quot;. | Minuter, plus datumflödets schemaintervall. |
| Tillgängliga data i data Lake och Real-Time Customer Profile | När batchen har importerats landas posterna i datasjön och (om datauppsättningen är profilaktiverad) läggs in i kundprofilen i realtid. Standardavtal för Experience Platform-licensavtal för batchanvändning och profilförtäring gäller. | Inom samma körfönster som dataflödet, dvs. kort efter att batchkörningen har slutförts. Poster blir vanligtvis tillgängliga på några minuter för tjänster längre fram i kedjan. |

{style="table-layout:auto"}

## Skapa en källanslutning till Adobe Campaign Managed Cloud Services med hjälp av Experience Platform användargränssnitt

Nu när du har öppnat dina dataloggar i Campaign-klientkonsolen, skapat ett schema och en datauppsättning kan du nu skapa en källanslutning för att överföra dina Campaign Managed Services-data till Experience Platform.

Detaljerade instruktioner om hur du överför data i leveransloggar för Campaign v8 och spårningsloggar till Experience Platfrom finns i [guiden om hur du skapar en Campaign Managed Services-källanslutning i användargränssnittet](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>Det finns ett versalt fall där interaktionen mellan en nyligen borttagen e-postmottagare med ett e-postmeddelande kan återimportera personuppgifter till Experience Platform. I vissa fall kan detta återaktivera marknadsföring för den användaren.
>
>* Det här scenariot är bara aktivt mellan den tidpunkt då en sekretessförfrågan har utförts i Experience Platform och den tidpunkt då den har körts i Adobe Campaign Classic. När begäran har körts i Campaign finns det en kontroll som kontrollerar att posten inte exporteras till Campaign. Vänligen skicka in en GDPR-begäran på nytt efter 72 timmar efter exekveringen för att lösa detta.
