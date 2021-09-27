---
keywords: Experience Platform;hem;populära ämnen;SFTP;sftp
solution: Experience Platform
title: Skapa en SFTP-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en SFTP-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Skapa en [!DNL SFTP]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL SFTP]-källanslutning med Adobe Experience Platform-gränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

>[!IMPORTANT]
>
>Du bör undvika radmatningar och vagnreturer när du importerar JSON-objekt med en [!DNL SFTP]-källanslutning. Du kan undvika begränsningarna genom att använda ett enda JSON-objekt per rad och flera rader för att skapa filer.

Om du redan har en giltig [!DNL SFTP]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till [!DNL SFTP] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är associerad med din [!DNL SFTP]-server. |
| `port` | Den [!DNL SFTP]-serverport som du ansluter till. Om det inte anges är standardvärdet `22`. |
| `username` | Användarnamnet som ger åtkomst till din [!DNL SFTP]-server. |
| `password` | Lösenordet för din [!DNL SFTP]-server. |
| `privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. Typen av OpenSSH-nyckel måste klassificeras som antingen RSA eller DSA. |
| `passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt [!DNL SFTP]-konto för att ansluta till plattformen.

## Anslut till din [!DNL SFTP]-server

Välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] innehåller en mängd olika källor som du kan skapa ett inkommande konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL SFTP]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/sftp/catalog.png)

Sidan **[!UICONTROL Connect to SFTP]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det FTP- eller SFTP-konto som du vill ansluta till och fortsätter sedan med **[!UICONTROL Next]**.

![befintlig](../../../../images/tutorials/create/sftp/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en valfri beskrivning för ditt nya [!DNL SFTP]-konto.

#### Autentisera med lösenord

[!DNL SFTP] stöder olika autentiseringstyper för åtkomst. Under **[!UICONTROL Account authentication]** väljer du **[!UICONTROL Password]** och anger sedan värden för värd och port att ansluta till tillsammans med ditt användarnamn och lösenord.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### Autentisera med den offentliga SSH-nyckeln

Om du vill använda SSH-offentliga nyckelbaserade autentiseringsuppgifter väljer du **[!UICONTROL SSH public key]** och anger värden för värd och port, samt innehållet i din privata nyckel och lösenfras.

>[!IMPORTANT]
>
>SFTP stöder en RSA- eller DSA-typ av OpenSSH-nyckel. Kontrollera att nyckelfilens innehåll börjar med `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` och slutar med `"-----END [RSA/DSA] PRIVATE KEY-----"`. Om den privata nyckelfilen är en PPK-formatfil använder du PuTTY-verktyget för att konvertera från PPK till OpenSSH-format.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Innehåll för privat nyckel | Base64-kodat innehåll för privat SSH-nyckel. Typen av OpenSSH-nyckel måste klassificeras som antingen RSA eller DSA. |
| Lösenfras | Anger lösenordsfrasen eller lösenordet som den privata nyckeln ska dekrypteras om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som dess värde. |


## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt SFTP-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
