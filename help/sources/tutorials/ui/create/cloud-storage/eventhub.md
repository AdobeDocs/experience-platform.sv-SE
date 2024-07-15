---
title: Skapa en Azure Event Hubs Source Connection i användargränssnittet
description: Lär dig hur du skapar en Azure Event Hubs-källanslutning med Adobe Experience Platform-gränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1256f0c76b29edad4808fc4be1d61399bfbae8fa
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Skapa en [!DNL Azure Event Hubs]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL Azure Event Hubs] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

I den här självstudiekursen får du lära dig hur du skapar ett [!DNL Azure Event Hubs]-konto med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Event Hubs]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/streaming/cloud-storage-streaming.md).

### Samla in nödvändiga inloggningsuppgifter

Om du vill autentisera [!DNL Event Hubs]-källkopplingen måste du ange värden för följande anslutningsegenskaper:

>[!BEGINTABS]

>[!TAB Standardautentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| SAS-nyckelnamn | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| SAS-nyckel | Primärnyckeln för namnområdet [!DNL Event Hubs]. `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter konfigurerade för att [!DNL Event Hubs]-listan ska kunna fyllas i. |
| Namnutrymme | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |

>[!TAB SAS-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| SAS-nyckelnamn | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| SAS-nyckel | Primärnyckeln för namnområdet [!DNL Event Hub]. `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter konfigurerade för att [!DNL Event Hubs]-listan ska kunna fyllas i. |
| Namnutrymme | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| Händelsehubbens namn | Fyll i ditt [!DNL Azure Event Hub]-namn. Läs [Microsoft-dokumentationen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) om du vill ha mer information om [!DNL Event Hub]-namn. |

>[!TAB Händelsehubben Azure Active Directory-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som du vill begära behörighet från. Ditt klient-ID kan formateras som ett GUID eller som ett eget namn. **Obs!** Klient-ID kallas för &quot;katalog-ID&quot; i gränssnittet [!DNL Microsoft Azure]. |
| Klient-ID | Program-ID som tilldelats din app. Du kan hämta detta ID från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| Värde för klienthemlighet | Klienthemligheten som används tillsammans med klient-ID för att autentisera din app. Du kan hämta din klienthemlighet från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| Namnutrymme | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |

Mer information om [!DNL Azure Active Directory] finns i [Azure-guiden om hur du använder Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Händelsehubben har omfattat Azure Active Directory Auth]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som du vill begära behörighet från. Ditt klient-ID kan formateras som ett GUID eller som ett eget namn. **Obs!** Klient-ID kallas för &quot;katalog-ID&quot; i gränssnittet [!DNL Microsoft Azure]. |
| Klient-ID | Program-ID som tilldelats din app. Du kan hämta detta ID från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| Värde för klienthemlighet | Klienthemligheten som används tillsammans med klient-ID för att autentisera din app. Du kan hämta din klienthemlighet från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| Namnutrymme | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| Händelsehubbens namn | Fyll i ditt [!DNL Azure Event Hub]-namn. Läs [Microsoft-dokumentationen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) om du vill ha mer information om [!DNL Event Hub]-namn. |

Mer information om [!DNL Azure Active Directory] finns i [Azure-guiden om hur du använder Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL Event Hubs]-konto till Experience Platform.

## Anslut ditt [!DNL Event Hubs]-konto

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL Azure Event Hubs]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen med Azure Event Hubs har valts.](../../../../images/tutorials/create/eventhub/catalog.png)

Dialogrutan **[!UICONTROL Connect to Azure Event Hubs]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto markerar du det [!DNL Event Hubs]-konto som du vill använda och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![En lista över befintliga Azure Event Hubs-källkonton.](../../../../images/tutorials/create/eventhub/existing.png)

### Nytt konto

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Event Hubs]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en valfri beskrivning för det nya [!DNL Event Hubs]-kontot.

![Det nya gränssnittet för att skapa konto för Azure Event Hubs.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Standardautentisering]

Om du vill skapa ett [!DNL Event Hubs]-konto med standardautentisering använder du listrutan [!UICONTROL Account authentication] och väljer sedan **[!UICONTROL Standard authentication]**. Ange sedan värden för [!UICONTROL SAS key name], [!UICONTROL SAS key] och [!UICONTROL Namespace].

När du har angett autentiseringsuppgifterna väljer du **[!UICONTROL Connect to source]**.

![Standardautentiseringsgränssnittet för Azure Event Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS-autentisering]

Om du vill skapa ett [!DNL Event Hubs]-konto med SAS-autentisering använder du listrutan [!UICONTROL Account authentication] och väljer sedan **[!UICONTROL SAS authentication]**. Ange sedan värden för [!UICONTROL SAS key name], [!UICONTROL SAS key], [!UICONTROL Namespace] och [!UICONTROL Event Hubs name].

När du har angett autentiseringsuppgifterna väljer du **[!UICONTROL Connect to source]**.

![SAS-autentiseringsgränssnittet för Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Händelsehubben Azure Active Directory-autentisering]

Om du vill skapa ett [!DNL Event Hubs]-konto med Event Hub Azure Active Directory-autentisering använder du listrutan [!UICONTROL Account authentication] och väljer sedan **[!UICONTROL Event Hub Azure Active Directory]**. Ange sedan värden för [!UICONTROL Tenant ID], [!UICONTROL Client ID], [!UICONTROL Client Secret Value] och [!UICONTROL Namespace].

![Azure Event Hub Azure Active Directory Authentication](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Händelsehubben har omfattat Azure Active Directory Auth]

Om du vill skapa ett [!DNL Event Hubs]-konto med Azure Active Directory-autentisering som omfattar händelsehubben använder du listrutan [!UICONTROL Account authentication] och väljer sedan **[!UICONTROL Event Hub Scoped Azure Active Directory]**. Ange sedan värden för [!UICONTROL Tenant ID], [!UICONTROL Client ID], [!UICONTROL Client Secret Value], [!UICONTROL Namespace] och [!UICONTROL Event Hub Name].

![Azure Event Hub har omfattat Azure Activity Directory-autentisering](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Nästa steg

Genom att följa den här självstudiekursen har du anslutit ditt [!DNL Event Hubs]-konto till Experience Platform. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
