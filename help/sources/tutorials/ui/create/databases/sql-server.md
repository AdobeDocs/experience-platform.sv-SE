---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Microsoft SQL Server-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---


# Skapa en [!DNL Microsoft] SQL Server-källanslutning i användargränssnittet

>[!NOTE]
> SQL Server-kopplingen [!DNL Microsoft] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Microsoft] SQL Server-källkoppling (nedan kallad SQL Server) med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en SQL Server-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till SQL Server på [!DNL Platform]måste du ange följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med ditt SQL Server-konto. SQL Server-anslutningssträngsmönstret är: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

Mer information om hur du kommer igång med SQL Server finns i [det här dokumentet](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) .

## Anslut ditt SQL Server-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att skapa en ny inkommande basanslutning som du kan länka ditt SQL Server-konto till [!DNL Platform].

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa inkommande basanslutningar med, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Microsoft SQL Server]** att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande basanslutning väljer du **[!UICONTROL Connect source]**.

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Sidan visas *[!UICONTROL Connect to Microsoft SQL Server]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du basanslutningen med ett namn, en valfri beskrivning och dina SQL Server-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya basanslutningen.

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det SQL Server-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt SQL Server-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Platform](../../dataflow/databases.md).