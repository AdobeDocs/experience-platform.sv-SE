---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure Event Hubs-källkoppling i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Skapa en Azure Event Hubs-källkoppling i användargränssnittet

>[!NOTE]
> Azure Event Hubs-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du autentiserar en Azure Event Hubs-källkoppling (nedan kallad EventHub) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett EventHub-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/streaming/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera din EventHub-källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Den genererade signaturen för delad åtkomst. |
| `namespace` | Namnutrymmet för den EventHub som du försöker komma åt. |

Mer information om dessa värden finns i [det här EventHub-dokumentet](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Anslut ditt EventHub-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt EventHub-konto till Platform.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På fliken *Katalog* visas en rad olika källor som kan anslutas till plattformen. Varje källa visar antalet befintliga konton som är kopplade till dem.

Under kategorin *Cloud Storage* väljer du **Azure Event Hubs** och klickar **på +-ikonen (+)** för att skapa en ny EventHub-anslutning.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Dialogrutan *Anslut till Azure Event Hubs* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På det indataformulär som visas anger du ett namn, en valfri beskrivning och dina EventHub-autentiseringsuppgifter. När du är klar väljer du **Anslut** och tillåt sedan en tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det EventHub-konto som du vill ansluta till och väljer sedan **Nästa** för att fortsätta.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit ditt EventHub-konto till Platform. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/streaming/cloud-storage.md).