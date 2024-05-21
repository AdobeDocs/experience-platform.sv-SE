---
title: Google PubSub Source Overview
description: Lär dig hur du ansluter Google PubSub till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: c8fc447631f5382d49022b525a10edeadbd5ab46
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# [!DNL Google PubSub] källa

>[!IMPORTANT]
>
>The [!DNL Google PubSub] Källan är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

Adobe Experience Platform erbjuder anslutningsmöjligheter för molnleverantörer som [!DNL AWS], [!DNL Google Cloud Platform]och [!DNL Azure], vilket gör att ni kan överföra data från dessa system till Platform för användning i tjänster och destinationer längre fram i kedjan.

Lagringskällor i molnet kan hämta dina data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i källarbetsflödet. Plattformen gör att du kan hämta in data från [!DNL Google PubSub] i realtid.

## Förutsättningar {#prerequisites}

I det här avsnittet beskrivs den nödvändiga konfiguration som du måste slutföra innan du kan ansluta [!DNL Google PubSub] konto till Experience Platform.

### Skapa tjänstkonto {#create-service-account}

A **tjänstkonto** är en typ av konto som ofta används av ett program eller en beräkning av arbetsbelastning, i stället för en person. Ett tjänstkonto identifieras av dess e-postadress, som är unik för kontot.

* Å ena sidan är tjänstkonton **huvudkonton** - du kan ge tjänstkonton åtkomst till [!DNL Google Cloud] resurser. Du kan till exempel tilldela ett tjänstkonto rollen Beräkna administratör `(roles/compute.admin)` på ett visst projekt. Detta gör att tjänstkontot kan hantera beräkningsmotorresurser i just det projektet.
* Å andra sidan är tjänstkonton också resurser - du kan ge andra huvudkonton behörighet att komma åt tjänstkontot. Du kan till exempel ge en användare rollen Tjänstkontoanvändare `(roles/iam.serviceAccountUser)` på ett tjänstkonto för att användaren ska kunna koppla tjänstkontot till resurser. Du kan även tilldela en användare rollen som tjänstkontoadministratör `(roles/iam.serviceAccountAdmin)` om du vill att användaren ska kunna utföra åtgärder som att visa, redigera, inaktivera och ta bort tjänstkontot.

Mer information om hur du fastställer rätt autentiseringstyp för ditt användningsfall finns i [[!DNL Google] guide om autentiseringsmetoder](https://cloud.google.com/docs/authentication).

Följ stegen nedan för att skapa ett tjänstkonto:

Navigera först till [!DNL IAM] sidan på [!DNL Google Developer Console] och sedan **[!DNL Create Service Account]**.

![Fönstret Skapa tjänstkonto i Google Developer Console](../../images/tutorials/create/google-pubsub/create-service-account.png)

Ange sedan ett visningsnamn och ett ID för ditt tjänstkonto och välj **[!DNL Create and Continue]**.

![Information om tjänstkontot i Google Developer Console](../../images/tutorials/create/google-pubsub/service-account-details.png)

### Generera servicekontonycklar {#generate-service-account-keys}

Om du vill generera nycklar för ditt tjänstkonto väljer du nyckelländrubriken på sidan för tjänstkonton. Välj **[!DNL Add key]** och sedan **[!DNL Create new key]** i listrutan. Du kan också använda den här panelen för att överföra en befintlig nyckel.

![Fönstret Lägg till nyckel i Google Developer Console](../../images/tutorials/create/google-pubsub/add-key.png)

När det är klart visas ett meddelande om att den privata nyckeln har sparats på datorn och att en fil kommer att hämtas. Du kan sedan använda innehållet i den här filen som inloggningsuppgifter när du skapar [!DNL Google PubSub] på Experience Platform.

### Bevilja behörigheter på ämne- och prenumerationsnivå {#grant-permissions}

Om du vill bevilja behörigheter på ämne- och prenumerationsnivå går du till ämneskonsolsidan och väljer **[!DNL Show info panel]**. Nästa, under [!DNL Permissions] flik, välja [!DNL Add Principal] och lägg sedan till tjänstkontots huvudnamn tillsammans med behörigheterna.

![I popup-fönstret i Google Developer Console kan du tilldela behörigheter på ämnes- och prenumerationsnivå](../../images/tutorials/create/google-pubsub/add-principal.png)

## Konfigurationer för optimala [!DNL Google PubSub usage] {#optimal-configurations}

I det här avsnittet beskrivs de konfigurationer du rekommenderas att göra för att optimera din användning av [!DNL Google PubSub] källa på Experience Platform.

### Prenumerationsegenskaper {#subscription-properties}

Använd [!DNL Google Developer Console] till **öka bekräftelsedeadline**. Detta gör att [!DNL Google Publisher] vänta i enlighet med den tid som du konfigurerar innan du skickar meddelandet igen. Denna fördröjning bidrar till att minska onödig belastning på abonnentnivå.

![Tidsgränsen för bekräftelsen i Google Developer Console.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

Aktivera **[!DNL exactly one delivery]**. Den här konfigurationen informerar [!DNL Google Publisher] för att garantera att meddelanden som skickas till prenumerationen inte skickas igen innan bekräftelsemeddelandet går ut. Du kan använda den här inställningen för att se till att bekräftelsemeddelanden inte skickas igen till prenumerationen.

![Exakt en leveranskonfigurationssida i Google Developer Console.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

Du kan aktivera **[!DNL Retry after exponential backoff delay]** för att minska risken för att servern överbelastas ytterligare. Du kan aktivera den här konfigurationen i dialogrutan [!DNL Google Developer Console] för att på ett bättre sätt minska tillfälliga fel (tillfälliga fel som normalt löser sig själva) genom att ge systemet mer tid att återställa innan ett nytt anslutningsförsök görs.

![Fönstret Prova princip igen i Google Developer Console.](../../images/tutorials/create/google-pubsub/retry-policy.png)

Du måste **ange att prenumerationsmeddelandets varaktighet ska vara 24 timmar eller mer** för att säkerställa att data som inte är kända inte går förlorade vid toppbelastningar. Dessutom **aktivera ett ämne för oåterkalleliga brev** för att säkerställa att dataförlust inte inträffar ens i sällsynta fall.

>[!IMPORTANT]
>
>Du kan bara skapa ett källdataflöde per [!DNL Google PubSub] prenumeration. Om du återanvänder en prenumeration, även i sandlådor, går data förlorade.

## Anslut [!DNL Google PubSub] till Experience Platform

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google PubSub] till Plattform med API:er eller användargränssnittet:

### Använda API:er

* [Skapa en Google PubSub-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

* [Skapa en Google PubSub-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
