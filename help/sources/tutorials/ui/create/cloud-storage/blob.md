---
title: Skapa en Azure Blob Source Connection i användargränssnittet
description: Lär dig hur du skapar en Azure Blob-källanslutning med Experience Platform-användargränssnittet.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Skapa en [!DNL Azure Blob]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Blob]-källanslutning (kallas nedan [!DNL Blob]) med Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket för att organisera kundupplevelsedata i Experience Platform.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Blob]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

Experience Platform har stöd för följande filformat som kan importeras från externa lagringsplatser:

* Avgränsaravgränsade värden (DSV): Du kan använda valfri enskild kolumnavgränsare, t.ex. tabb, komma, pipe, semikolon eller hash, för att samla in platta filer i vilket format som helst.
* JavaScript Object Notation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
* Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

Du måste ange giltiga värden för följande autentiseringsuppgifter för att komma åt ditt [!DNL Blob]-lagringsutrymme på Experience Platform:

>[!BEGINTABS]

>[!TAB Autentisering av anslutningssträng]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Anslutningssträng | En sträng som innehåller den auktoriseringsinformation som krävs för att autentisera [!DNL Blob] till Experience Platform. Anslutningssträngsmönstret [!DNL Blob] är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Mer information om anslutningssträngar finns i det här [!DNL Blob]-dokumentet om [konfigurering av anslutningssträngar](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB SAS URI-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| SAS-URI | Den URI för signatur för delad åtkomst som du kan använda som en alternativ autentiseringstyp för att ansluta ditt [!DNL Blob]-konto. SAS-URI-mönstret [!DNL Blob] är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Mer information finns i det här [!DNL Blob]-dokumentet om [signatur-URI:er för delad åtkomst](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Behållare | Namnet på den behållare som du vill tilldela åtkomst till. När du skapar ett nytt konto med källan [!DNL Blob] kan du ange ett behållarnamn som anger användaråtkomst till den undermapp du väljer. |
| Mappsökväg | Sökvägen till mappen som du vill ge åtkomst till. |

>[!ENDTABS]

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att ansluta ditt [!DNL Blob]-lagringsutrymme till Experience Platform

## Anslut ditt [!DNL Blob]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL Azure Blob Storage]** och sedan **[!UICONTROL Add data]**.

![Experience Platform-källkatalogen med Azure Blob Storage-källan vald.](../../../../images/tutorials/create/blob/catalog.png)

Sidan **[!UICONTROL Connect to Azure Blob Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Blob]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/blob/existing.png)

### Nytt konto

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Blob]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en valfri beskrivning för det nya [!DNL Blob]-kontot.

![Den nya kontoskärmen för Azure Blob Storage-källan.](../../../../images/tutorials/create/blob/new.png)

Källan [!DNL Blob] stöder både autentisering av kontonycklar och autentisering med delad åtkomstsignatur (SAS). En kontonyckelbaserad autentisering kräver en anslutningssträng för verifiering, medan en SAS-autentisering använder en URI som tillåter säker delegerad autentisering av ditt konto.

Under det här steget kan du även ange vilka undermappar ditt konto ska ha åtkomst till genom att definiera namnet på behållaren och sökvägen till undermappen.

>[!BEGINTABS]

>[!TAB Anslutningssträng]

Om du vill autentisera med en kontonyckel väljer du **[!UICONTROL Account key authentication]** och anger anslutningssträngen. Under det här steget kan du även ange behållarnamnet och sökvägen till den undermapp som du vill ha åtkomst till. När du är klar väljer du **[!UICONTROL Connect to source]**.

![anslutningssträng](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS URI]

Du kan använda SAS för att skapa autentiseringsuppgifter med olika grad av åtkomst, eftersom en SAS-baserad autentisering gör att du kan ange behörigheter, start- och förfallodatum samt villkor för specifika resurser.

Om du vill autentisera med en signatur för delad åtkomst väljer du **[!UICONTROL Shared access signature authentication]** och anger sedan din SAS-URI. Under det här steget kan du även ange behållarnamnet och sökvägen till den undermapp som du vill ha åtkomst till. När du är klar väljer du **[!UICONTROL Connect to source]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Blob]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till Experience Platform](../../dataflow/batch/cloud-storage.md).
