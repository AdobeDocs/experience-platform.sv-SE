---
title: Skapa en SFTP Source Connection i användargränssnittet
description: Lär dig hur du skapar en SFTP-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Skapa en [!DNL SFTP]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL SFTP]-källanslutning med Adobe Experience Platform-gränssnittet.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

>[!IMPORTANT]
>
>Du bör undvika radmatningar och radmatningar när du importerar JSON-objekt med en [!DNL SFTP]-källanslutning. Du kan undvika begränsningarna genom att använda ett enda JSON-objekt per rad och flera rader för att skapa filer.

Om du redan har en giltig [!DNL SFTP]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL SFTP] autentiseringsguiden](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) om du vill ha mer information om hur du hämtar autentiseringsuppgifter.

## Anslut till din [!DNL SFTP]-server

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL SFTP]** och sedan **[!UICONTROL Add data]**.

![Experience Platform-källkatalogen med SFTP-källan markerad.](../../../../images/tutorials/create/sftp/catalog.png)

Sidan **[!UICONTROL Connect to SFTP]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det FTP- eller SFTP-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![En lista över befintliga SFTP-konton i Experience Platform-gränssnittet.](../../../../images/tutorials/create/sftp/existing.png)

### Nytt konto

>[!TIP]
>
>* När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL SFTP]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.
>
>* SFTP stöder `ed25519`, `RSA` eller `DSA` OpenSSH-nyckel. Kontrollera att nyckelfilsinnehållet börjar med `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` och slutar med `"-----END [RSA/DSA] PRIVATE KEY-----"`. Om den privata nyckelfilen är en PPK-formatfil använder du PuTTY-verktyget för att konvertera från PPK till OpenSSH-format.

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en valfri beskrivning för det nya [!DNL SFTP]-kontot.

![Den nya kontoskärmen för SFTP](../../../../images/tutorials/create/sftp/new.png)

Källan [!DNL SFTP] stöder både grundläggande autentisering och autentisering via den offentliga nyckeln för SSH.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill använda grundläggande autentisering väljer du **[!UICONTROL Password]** och anger sedan lämpliga värden för följande autentiseringsuppgifter:

* värd
* port
* användarnamn
* lösenord

Under det här steget kan du även konfigurera maximalt antal samtidiga anslutningar, definiera mappsökvägen och aktivera eller inaktivera chunkning för [!DNL SFTP]-servern. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

Mer information om autentisering finns i guiden om [att samla in nödvändiga autentiseringsuppgifter för [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Den nya kontoskärmen för SFTP-källan med grundläggande autentisering](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH-autentisering med offentlig nyckel]

Om du vill använda SSH-autentiseringsuppgifter för offentlig nyckel väljer du **[!UICONTROL SSH public key]** och anger sedan lämpliga värden för följande autentiseringsuppgifter:

* värd
* port
* användarnamn
* privat nyckelinnehåll
* lösenfras

Under det här steget kan du även konfigurera maximalt antal samtidiga anslutningar, definiera mappsökvägen och aktivera eller inaktivera chunkning för [!DNL SFTP]-servern. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

Mer information om autentisering finns i guiden om [att samla in nödvändiga autentiseringsuppgifter för [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Den nya kontoskärmen för SFTP-källan med den offentliga SSH-nyckeln.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt SFTP-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till Experience Platform](../../dataflow/batch/cloud-storage.md).
