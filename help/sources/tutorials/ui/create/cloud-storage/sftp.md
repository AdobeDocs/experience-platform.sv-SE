---
title: Skapa en SFTP-källanslutning i användargränssnittet
description: Lär dig hur du skapar en SFTP-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: e92471b386b857fc21947d352f1c1b88431c68bc
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Skapa en [!DNL SFTP] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL SFTP] källanslutning med Adobe Experience Platform UI.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

>[!IMPORTANT]
>
>Du bör undvika radmatningar och radmatningar när du importerar JSON-objekt med en [!DNL SFTP] källanslutning. Du kan undvika begränsningarna genom att använda ett enda JSON-objekt per rad och flera rader för att skapa filer.

Om du redan har en giltig [!DNL SFTP] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till [!DNL SFTP]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är kopplad till din [!DNL SFTP] server. |
| `port` | The [!DNL SFTP] serverport som du ansluter till. Om det inte anges används standardvärdet `22`. |
| `username` | Användarnamnet med åtkomst till dina [!DNL SFTP] server. |
| `password` | Lösenordet för [!DNL SFTP] server. |
| `privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. Typen av OpenSSH-nyckel måste klassificeras som antingen RSA eller DSA. |
| `passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |
| `maxConcurrentConnections` | Med den här parametern kan du ange en maxgräns för hur många samtidiga anslutningar som plattformen skapar vid anslutning till SFTP-servern. Du måste ange att det här värdet ska vara mindre än gränsen som anges av SFTP. **Anteckning**: När den här inställningen är aktiverad för ett befintligt SFTP-konto påverkas bara framtida dataflöden och inte befintliga dataflöden. |
| Mappsökväg | Sökvägen till mappen som du vill ge åtkomst till. [!DNL SFTP] kan du ange mappsökvägen för att ange användaråtkomst till den undermapp du väljer. |

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa en ny [!DNL SFTP] konto för att ansluta till plattformen.

## Anslut till [!DNL SFTP] server

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL SFTP]** och sedan **[!UICONTROL Add data]**.

![Katalogen för Experience Platform-källor med SFTP-källan markerad.](../../../../images/tutorials/create/sftp/catalog.png)

The **[!UICONTROL Connect to SFTP]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det FTP- eller SFTP-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![En lista över befintliga SFTP-konton i användargränssnittet för Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nytt konto

>[!TIP]
>
>* När du har skapat en fil kan du inte ändra autentiseringstypen för en [!DNL SFTP] basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.
>
>* SFTP stöder en RSA- eller DSA-typ av OpenSSH-nyckel. Se till att nyckelfilens innehåll börjar med `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` och slutar med `"-----END [RSA/DSA] PRIVATE KEY-----"`. Om den privata nyckelfilen är en PPK-formatfil använder du PuTTY-verktyget för att konvertera från PPK till OpenSSH-format.

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en valfri beskrivning av ditt nya [!DNL SFTP] konto.

![Den nya kontoskärmen för SFTP](../../../../images/tutorials/create/sftp/new.png)

The [!DNL SFTP] Källan har stöd för både grundläggande autentisering och autentisering via den offentliga nyckeln för SSH.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill använda grundläggande autentisering väljer du **[!UICONTROL Password]** och ange värden för värd och port att ansluta till, tillsammans med ditt användarnamn och lösenord. Under det här steget kan du även ange sökvägen till den undermapp som du vill ge åtkomst till. När du är klar väljer du **[!UICONTROL Connect to source]**.

![Den nya kontoskärmen för SFTP-källan med grundläggande autentisering](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH-autentisering av offentlig nyckel]

Om du vill använda SSH-autentiseringsuppgifter för offentlig nyckel väljer du **[!UICONTROL SSH public key]**  och ange värden för värd och port, samt din privata nyckelkombination och lösenfras. Under det här steget kan du även ange sökvägen till den undermapp som du vill ge åtkomst till. När du är klar väljer du **[!UICONTROL Connect to source]**.

![Den nya kontoskärmen för SFTP-källan med den offentliga SSH-nyckeln.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt SFTP-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
