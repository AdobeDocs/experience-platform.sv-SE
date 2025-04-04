---
title: Google PubSub Source Overview
description: Lär dig hur du ansluter Google PubSub till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# [!DNL Google PubSub]-källa

>[!IMPORTANT]
>
>Källan [!DNL Google PubSub] är tillgänglig i källkatalogen för användare som har köpt Real-Time CDP Ultimate.

Adobe Experience Platform erbjuder inbyggd anslutning för molnleverantörer som [!DNL AWS], [!DNL Google Cloud Platform] och [!DNL Azure], vilket gör att du kan överföra data från dessa system till Experience Platform för användning i underordnade tjänster och destinationer.

Lagringskällor i molnet kan överföra dina data till Experience Platform utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i källarbetsflödet. Med Experience Platform kan du hämta in data från [!DNL Google PubSub] i realtid.

## Förhandskrav {#prerequisites}

I det här avsnittet beskrivs den nödvändiga konfiguration som du måste slutföra innan du kan ansluta ditt [!DNL Google PubSub]-konto till Experience Platform.

### Skapa tjänstkonto {#create-service-account}

Ett **tjänstkonto** är en typ av konto som ofta används av ett program eller en beräkning av arbetsbelastning, i stället för en person. Ett tjänstkonto identifieras av dess e-postadress, som är unik för kontot.

* Å ena sidan är tjänstkonton **huvudkonton** - du kan ge tjänstkonton åtkomst till [!DNL Google Cloud] resurser. Du kan till exempel bevilja ett tjänstkonto rollen Compute Admin `(roles/compute.admin)` för ett visst projekt. Detta gör att tjänstkontot kan hantera beräkningsmotorresurser i just det projektet.
* Å andra sidan är tjänstkonton också resurser - du kan ge andra huvudkonton behörighet att komma åt tjänstkontot. Du kan till exempel tilldela en användare användarrollen för tjänstkontot `(roles/iam.serviceAccountUser)` på ett tjänstkonto så att användaren kan koppla tjänstkontot till resurserna. Du kan också tilldela en användare rollen som tjänstkontoadministratör `(roles/iam.serviceAccountAdmin)` så att användaren kan slutföra uppgifter som visa, redigera, inaktivera och ta bort tjänstkontot.

Mer information om hur du fastställer rätt autentiseringstyp för ditt användningsfall finns i [[!DNL Google] handboken om autentiseringsmetoder](https://cloud.google.com/docs/authentication).

Följ stegen nedan för att skapa ett tjänstkonto:

Navigera först till sidan [!DNL IAM] i [!DNL Google Developer Console] och välj sedan **[!DNL Create Service Account]**.

![Fönstret Skapa tjänstkonto i Google Developer Console](../../images/tutorials/create/google-pubsub/create-service-account.png)

Ange sedan ett visningsnamn och ett ID för ditt tjänstkonto och välj **[!DNL Create and Continue]**.

![Tjänstkontoinformationen i Google Developer Console](../../images/tutorials/create/google-pubsub/service-account-details.png)

### Generera servicekontonycklar {#generate-service-account-keys}

Om du vill generera nycklar för ditt tjänstkonto väljer du nyckelländrubriken på sidan för tjänstkonton. Därifrån väljer du **[!DNL Add key]** och sedan **[!DNL Create new key]** i listrutan. Du kan också använda den här panelen för att överföra en befintlig nyckel.

![Fönstret Lägg till nyckel i Google Developer Console](../../images/tutorials/create/google-pubsub/add-key.png)

När det är klart visas ett meddelande om att den privata nyckeln har sparats på datorn och att en fil kommer att hämtas. Du kan sedan använda innehållet i den här filen som autentiseringsuppgifter när du skapar ditt [!DNL Google PubSub]-konto på Experience Platform.

### Bevilja behörigheter på ämne- och prenumerationsnivå {#grant-permissions}

Om du vill bevilja behörigheter på ämne- och prenumerationsnivå går du till ämneskonsolsidan och väljer **[!DNL Show info panel]**. Välj sedan [!DNL Add Principal] på fliken [!DNL Permissions] och lägg till tjänstkontots huvudnamn tillsammans med behörigheterna.

![Popup-fönstret i Google Developer Console där du kan bevilja behörigheter på ämne- och prenumerationsnivå](../../images/tutorials/create/google-pubsub/add-principal.png)

## Konfigurationer för optimal [!DNL Google PubSub usage] {#optimal-configurations}

I det här avsnittet beskrivs de konfigurationer som du rekommenderas att göra för att optimera din användning av källan [!DNL Google PubSub] på Experience Platform.

### Prenumerationsegenskaper {#subscription-properties}

Använd [!DNL Google Developer Console] för att **öka bekräftelsedeadline**. Detta gör att [!DNL Google Publisher] kan vänta i enlighet med den tid som du konfigurerar innan meddelandet skickas igen. Denna fördröjning bidrar till att minska onödig belastning på abonnentnivå.

![Tidsgränsen för bekräftelsen i Google Developer Console.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

Aktivera **[!DNL exactly one delivery]**. Den här konfigurationen informerar [!DNL Google Publisher] för att garantera att meddelanden som skickas till prenumerationen inte skickas igen innan bekräftelsens deadline går ut. Du kan använda den här inställningen för att se till att bekräftelsemeddelanden inte skickas igen till prenumerationen.

![Exakt en leveranskonfigurationssida i Google Developer Console.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

Du kan aktivera **[!DNL Retry after exponential backoff delay]** för att minska risken för att servern överbelastas ytterligare. Du kan aktivera den här konfigurationen i [!DNL Google Developer Console] för att bättre mildra tillfälliga fel (tillfälliga fel som normalt löser sig själva) genom att ge systemet mer tid att återställa innan du försöker med en annan anslutning.

![Fönstret Prova igen i Google Developer Console.](../../images/tutorials/create/google-pubsub/retry-policy.png)

Du måste **ange att kvarhållningstiden för prenumerationsmeddelanden ska vara 24 timmar eller mer** för att se till att obekräftade data inte går förlorade vid toppbelastningar. Dessutom **aktiverar ett oförändrat bokstavstecken** för att säkerställa att dataförluster inte inträffar ens i sällsynta kantfall.

>[!IMPORTANT]
>
>Du kan bara skapa ett källdataflöde per [!DNL Google PubSub]-prenumeration. Om du återanvänder en prenumeration, även i sandlådor, går data förlorade.

## Anslut [!DNL Google PubSub] till Experience Platform

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google PubSub] till Experience Platform med API:er eller användargränssnittet:

### Använda API:er

* [Skapa en Google PubSub-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

* [Skapa en Google PubSub-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
