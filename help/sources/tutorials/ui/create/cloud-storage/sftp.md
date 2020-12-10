---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Skapa en SFTP-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en SFTP-källanslutning med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: 7b638f0516804e6a2dbae3982d6284a958230f42
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# Skapa en SFTP-källanslutning i användargränssnittet

>[!NOTE]
>
>SFTP-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

I den här självstudiekursen beskrivs hur du skapar en SFTP-källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig SFTP-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till SFTP måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är associerad med SFTP-servern. |
| `username` | Användarnamnet som ger åtkomst till din SFTP-server. |
| `password` | Lösenordet för SFTP-servern. |
| `privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. SSH-filens OpenSSH-format (RSA/DSA). |
| `passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt SFTP-konto för att ansluta till plattformen.

## Anslut till SFTP-servern

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsytan. På [!UICONTROL Catalog] skärmen visas en mängd olika källor som du kan skapa ett inkommande konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under [!UICONTROL Cloud storage] kategorin **[!UICONTROL SFTP]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny SFTP-anslutning.

![katalog](../../../../images/tutorials/create/sftp/catalog.png)

Sidan visas **[!UICONTROL Connect to SFTP]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

SFTP-anslutningen ger dig olika typer av autentisering för åtkomst. Under **[!UICONTROL Account authentication]** Välj **[!UICONTROL Password]** att använda en lösenordsbaserad autentiseringsuppgift.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Du kan också välja **[offentlig SSH-nyckel]** och ansluta ditt SFTP-konto med en kombination av [!UICONTROL Private key content] och [!UICONTROL Passphrase].

>[!IMPORTANT]
>
>SFTP-anslutningen stöder en RSA/DSA OpenSSH-nyckel. Se till att nyckelfilens innehåll börjar med `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Om den privata nyckelfilen är en PPK-formatfil använder du PuTTY-verktyget för att konvertera från PPK till OpenSSH-format.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Innehåll för privat nyckel | A Base64 encoded SSH private key content. Den privata SSH-nyckeln ska vara i OpenSSH-format. |
| Lösenfras | Anger lösenordsfrasen eller lösenordet som den privata nyckeln ska dekrypteras om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det FTP- eller SFTP-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/sftp/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt FTP- eller SFTP-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).