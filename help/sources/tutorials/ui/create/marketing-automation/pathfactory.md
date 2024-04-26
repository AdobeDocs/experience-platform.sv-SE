---
title: Anslut ditt PathFactory-konto till Experience Platform via användargränssnittet
description: Lär dig hur du ansluter ditt PathFactory-konto till Experience Platform via användargränssnittet.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# Koppla samman [!DNL PathFactory] konto till Experience Platform via användargränssnittet

Den här självstudiekursen innehåller steg för hur du ansluter [!DNL PathFactory] Besökare, sessioner och sidvisningsdata till Adobe Experience Platform via användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL PathFactory] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [för automatiserad marknadsföring till Experience Platform med hjälp av användargränssnittet](../../dataflow/marketing-automation.md).

### Samla in nödvändiga autentiseringsuppgifter {#gather-credentials}

För att få åtkomst till ditt PathFactory-konto på plattformen måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Användarnamn | Ditt användarnamn för PathFactory-kontot. Detta är nödvändigt för att identifiera ditt konto i systemet. |
| Lösenord | Lösenordet som är kopplat till ditt PathFactory-konto. Säkerställ att detta skyddas för att förhindra obehörig åtkomst. |
| Domän | Domänen som är associerad med ditt PathFactory-konto. Detta refererar vanligtvis till den unika identifieraren i din PathFactory-URL. |
| Åtkomsttoken | En unik token som används för API-autentisering för att säkerställa säker kommunikation mellan dina system och PathFactory. |
| API-slutpunkter | Särskilda API-slutpunkter för dataåtkomst: Besökare, sessioner och sidvyer. Varje slutpunkt motsvarar olika datauppsättningar som du kan hämta. **Obs!** Dessa är fördefinierade av [!DNL PathFactory] och är specifika för de data som du avser att få tillgång till: <ul><li>**Slutpunkt för besökare**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Slutpunkt för sessioner**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Slutpunkt för sidvisning**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Detaljerad vägledning om hur du skyddar och använder dina inloggningsuppgifter och information om hur du skaffar och uppdaterar din åtkomsttoken finns på [PathFactory Support Center](https://support.pathfactory.com/categories/adobe/). Den här resursen innehåller omfattande guider om hur du hanterar dina inloggningsuppgifter och säkerställer effektiv och säker API-integrering.


## Koppla samman [!DNL PathFactory] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visar en mängd olika källor som stöds av Experience Platform.

Du kan välja lämplig kategori i listan med kategorier. Du kan också använda sökfältet för att filtrera efter en viss källa.

Under [!UICONTROL Marketing automation] kategori, välj **[!UICONTROL PathFactory]** och sedan **[!UICONTROL Set up]**.

![Källkatalogen med PathFactory-källan vald.](../../../../images/tutorials/create/pathfactory/catalog.png)

The **[!UICONTROL Connect to PathFactory]** visas. På den här sidan kan du antingen skapa ett nytt konto eller använda ett befintligt konto.

### Nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange ett namn för ditt konto, en valfri beskrivning och autentiseringsuppgifter som motsvarar dina [!DNL PathFactory] konto.

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet där du kan autentisera ett nytt konto för PathFactory.](../../../../images/tutorials/create/pathfactory/new.png)

### Befintligt konto

Om du redan har ett befintligt konto väljer du **[!UICONTROL Existing account]** och välj sedan det konto som du vill använda i listan som visas.

![Det befintliga kontogränssnittet där du kan välja från en lista med befintliga PathFactory-konton.](../../../../images/tutorials/create/pathfactory/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning mellan [!DNL PathFactory] konto och Experience Platform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att ta in data för automatiserad marknadsföring i Experience Platform](../../dataflow/marketing-automation.md).
