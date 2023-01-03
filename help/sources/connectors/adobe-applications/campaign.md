---
keywords: Experience Platform;hem;populära ämnen;Adobe Campaign Managed Cloud Services;kampanj;kampanjhanterade tjänster
title: Adobe Campaign Managed Cloud Services
description: Lär dig hur du ansluter Campaign-hanterade Cloud Services till plattformen med användargränssnittet
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Adobe Campaign Managed Cloud Services är en Managed Services-plattform för design av kundupplevelser i olika kanaler och utgör en miljö för visuell kampanjsamordning, interaktionshantering i realtid och flerkanalsmarknadsföring. Besök [Adobe Campaign v8-dokumentation](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) för mer information.

Med Adobe Campaign Managed Cloud Services-källan kan du hämta leveransloggar för Adobe Campaign v8 och spåra loggdata till Adobe Experience Platform.

## Förutsättningar

Innan du kan skapa en källanslutning för att hämta Campaign v8 till Experience Platform måste du först uppfylla följande krav:

* [Konfigurera importen av händelseloggen med Adobe Campaign klientkonsol](#view-delivery-and-tracking-log-data)
* [Skapa ett XDM ExperienceEvent-schema](#create-a-schema)
* [Skapa en datauppsättning](#create-a-dataset)

### Visa loggdata för leverans och spårning {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Du måste ha tillgång till Adobe Campaign v8 Client Console för att kunna visa dina loggdata i Campaign. Besök [Kampanjdokumentation v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) om du vill ha information om hur du hämtar och installerar klientkonsolen.

Logga in på Campaign v8-instansen via klientkonsolen. Under [!DNL Explorer] flik, välja [!DNL Administration] och sedan markera [!DNL Configuration]. Nästa, välj [!DNL Data schemas] och sedan använda `broadLog` filter för namn eller etikett. I listan som visas väljer du källschemat för mottagarleveransloggarna med namnet `broadLogRcp`.

![Klientkonsolen för Adobe Campaign v8 med fliken Utforskaren vald, noderna Administration, Konfiguration och Data utökade och filtreringen inställd på &quot;bred&quot;.](./images/campaign/explorer.png)

Välj sedan **Data** -fliken.

![Adobe Campaign v8-klientkonsolen med datafliken vald.](./images/campaign/data.png)

Högerklicka/tangentbordet i datapanelen för att öppna snabbmenyn. Här väljer du **Konfigurera lista...**

![Adobe Campaign v8-klientkonsolen med snabbmenyn öppen och alternativet Konfigurera lista markerat.](./images/campaign/configure.png)

Listkonfigurationsfönstret visas med ett gränssnitt där du kan lägga till önskade fält i den befintliga listan för att visa data på datapanelen.

![En lista med konfigurationer för mottagarleveransloggar som kan läggas till för visning.](./images/campaign/list-configuration.png)

Nu kan du visa mottagarnas leveransloggar, inklusive de konfigurationsfält som lagts till i föregående steg.

>[!TIP]
>
>Du kan upprepa samma steg, men filtrera efter `tracking` för att visa dina loggdata för spårning.

![Mottagarens leveransloggar visas med information om dess senast ändrade namn, leveranskanal, interna leveransnamn och etikett.](./images/campaign/recipient-delivery-logs.png)

### Skapa ett schema {#create-a-schema}

Skapa sedan ett XDM ExperienceEvent-schema för både leveransloggar och spårningsloggar. Du måste använda fältgruppen för kampanjleveransloggar i leveransloggschemat och fältgruppen för kampanjspårningsloggar i spårningsloggschemat. Du måste också definiera `externalID` -fältet som den primära identiteten för ditt schema.

>[!NOTE]
>
>Ditt XDM ExperienceEvent-schema måste vara profilaktiverat för att dina Campaign-data ska kunna importeras till [!DNL Real-Time Customer Profile].

Detaljerade instruktioner om hur du skapar ett schema finns i guiden [skapa ett XDM-schema i användargränssnittet](../../../xdm/tutorials/create-schema-ui.md).

### Skapa en datauppsättning {#create-a-dataset}

Slutligen måste du skapa en datauppsättning för dina scheman. Detaljerade instruktioner om hur du skapar en datauppsättning finns i guiden [skapa en datauppsättning i användargränssnittet](../../../catalog/datasets/user-guide.md).

## Skapa en Adobe Campaign Managed Cloud Services-källanslutning med hjälp av plattformsgränssnittet

Nu när du har öppnat dina dataloggar i Campaign-klientkonsolen, skapat ett schema och en datauppsättning kan du nu skapa en källanslutning för att överföra dina Campaign Managed Services-data till plattformen.

Detaljerade instruktioner om hur ni kan överföra leveransloggar för Campaign v8 och spårningsloggdata till Experience Platfrom finns i guiden på [skapa en Campaign Managed Services-källanslutning i användargränssnittet](../../tutorials/ui/create/adobe-applications/campaign.md).
