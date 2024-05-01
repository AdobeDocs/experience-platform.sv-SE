---
title: Skapa en Azure Event Hubs-källanslutning i användargränssnittet
description: Lär dig hur du skapar en Azure Event Hubs-källanslutning med Adobe Experience Platform-gränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# Skapa en [!DNL Azure Event Hubs] källanslutning i användargränssnittet

>[!IMPORTANT]
>
>The [!DNL Azure Event Hubs] Källan är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

Läs den här självstudiekursen för att lära dig hur du skapar en [!DNL Azure Event Hubs] med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Event Hubs] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/streaming/cloud-storage-streaming.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera [!DNL Event Hubs] källkoppling måste du ange värden för följande anslutningsegenskaper:

>[!BEGINTABS]

>[!TAB Standardautentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| SAS-nyckelnamn | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| SAS-nyckel | Primärnyckeln för [!DNL Event Hubs] namnutrymme. The `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter som konfigurerats för [!DNL Event Hubs] lista som ska fyllas i. |
| Namnutrymme | Namnutrymmet för [!DNL Event Hubs] du försöker komma åt. An [!DNL Event Hubs] namespace innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |

>[!TAB SAS-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| SAS-nyckelnamn | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| SAS-nyckel | Primärnyckeln för [!DNL Event Hubs] namnutrymme. The `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter som konfigurerats för [!DNL Event Hubs] lista som ska fyllas i. |
| Namnutrymme | Namnutrymmet för [!DNL Event Hubs] du försöker komma åt. An [!DNL Event Hubs] namespace innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| Händelsehubbens namn | Namnet på [!DNL Event Hubs] källa. |

Mer information om SAS-autentisering (shared access signatures) för [!DNL Event Hubs], läsa [[!DNL Azure] guide om användning av SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Azure Active Directory-autentisering för händelsehubb]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som du vill begära behörighet från. Ditt klient-ID kan formateras som ett GUID eller som ett eget namn. **Anteckning**: Klient-ID kallas för &quot;katalog-ID&quot; i [!DNL Microsoft Azure] gränssnitt. |
| Klient-ID | Program-ID som tilldelats din app. Du kan hämta detta ID från [!DNL Microsoft Entra ID] portal där du registrerade dina [!DNL Azure Active Directory]. |
| Värde för klienthemlighet | Klienthemligheten som används tillsammans med klient-ID för att autentisera din app. Du kan hämta din klienthemlighet från [!DNL Microsoft Entra ID] portal där du registrerade dina [!DNL Azure Active Directory]. |
| Namnutrymme | Namnutrymmet för [!DNL Event Hubs] du försöker komma åt. An [!DNL Event Hubs] namespace innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |

Mer information om [!DNL Azure Active Directory], läsa [Azure-guide om användning av Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Händelsehubben omfattade Azure Active Directory-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som du vill begära behörighet från. Ditt klient-ID kan formateras som ett GUID eller som ett eget namn. **Anteckning**: Klient-ID kallas för &quot;katalog-ID&quot; i [!DNL Microsoft Azure] gränssnitt. |
| Klient-ID | Program-ID som tilldelats din app. Du kan hämta detta ID från [!DNL Microsoft Entra ID] portal där du registrerade dina [!DNL Azure Active Directory]. |
| Värde för klienthemlighet | Klienthemligheten som används tillsammans med klient-ID för att autentisera din app. Du kan hämta din klienthemlighet från [!DNL Microsoft Entra ID] portal där du registrerade dina [!DNL Azure Active Directory]. |
| Namnutrymme | Namnutrymmet för [!DNL Event Hubs] du försöker komma åt. An [!DNL Event Hubs] namespace innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| Händelsehubbens namn | Namnet på [!DNL Event Hubs] källa. |

Mer information om [!DNL Azure Active Directory], läsa [Azure-guide om användning av Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Event Hubs] konto till Experience Platform.

## Koppla samman [!DNL Event Hubs] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Azure Event Hubs]** och sedan markera **[!UICONTROL Add data]**.

![Källkatalogen med Azure Event Hubs har valts.](../../../../images/tutorials/create/eventhub/catalog.png)

The **[!UICONTROL Connect to Azure Event Hubs]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Välj [!DNL Event Hubs] det konto du vill använda och sedan välja **[!UICONTROL Next]** för att fortsätta.

![En lista över befintliga Azure Event Hubs-källkonton.](../../../../images/tutorials/create/eventhub/existing.png)

### Nytt konto

>[!TIP]
>
>När du har skapat en fil kan du inte ändra autentiseringstypen för en [!DNL Event Hubs] basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en valfri beskrivning av ditt nya [!DNL Event Hubs] konto.

![Det nya gränssnittet för att skapa konton för Azure Event Hubs.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Standardautentisering]

Skapa en [!DNL Event Hubs] konto med standardautentisering, använd [!UICONTROL Account authentication] listrutemeny och välj **[!UICONTROL Standard authentication]**. Ange sedan värden för [!UICONTROL SAS key name], [!UICONTROL SAS key]och [!UICONTROL Namespace].

När du har angett dina autentiseringsuppgifter väljer du **[!UICONTROL Connect to source]**.

![Standardautentiseringsgränssnittet för Azure Event Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS-autentisering]

Skapa en [!DNL Event Hubs] konto med SAS-autentisering, använd [!UICONTROL Account authentication] listrutemeny och välj **[!UICONTROL SAS authentication]**. Ange sedan värden för [!UICONTROL SAS key name], [!UICONTROL SAS key], [!UICONTROL Namespace]och [!UICONTROL Event Hubs name].

När du har angett dina autentiseringsuppgifter väljer du **[!UICONTROL Connect to source]**.

![SAS-autentiseringsgränssnittet för Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Azure Active Directory-autentisering för händelsehubb]

Skapa en [!DNL Event Hubs] konto med Event Hub Azure Active Directory-autentisering, använd [!UICONTROL Account authentication] listrutemeny och välj **[!UICONTROL Event Hub Azure Active Directory]**. Ange sedan värden för [!UICONTROL Tenant ID], [!UICONTROL Client ID], [!UICONTROL Client Secret Value]och [!UICONTROL Namespace].

![Azure Event Hub Azure Active Directory-autentisering](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Händelsehubben omfattade Azure Active Directory-autentisering]

Skapa en [!DNL Event Hubs] konto med Event Hub-omfattande Azure Active Directory-autentisering, använd [!UICONTROL Account authentication] listrutemeny och välj **[!UICONTROL Event Hub Scoped Azure Active Directory]**. Ange sedan värden för [!UICONTROL Tenant ID], [!UICONTROL Client ID], [!UICONTROL Client Secret Value], [!UICONTROL Namespace]och [!UICONTROL Event Hub Name].

![Azure Event Hub omfattade Azure Activity Directory-autentisering](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Nästa steg

Genom att följa den här självstudiekursen har du kopplat samman [!DNL Event Hubs] konto till Experience Platform. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
