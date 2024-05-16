---
title: Skapa en Microsoft SQL Server-källanslutning i användargränssnittet
description: Lär dig hur du skapar en Microsoft SQL Server-källanslutning med Adobe Experience Platform gränssnitt.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---

# Skapa en [!DNL Microsoft SQL Server] källanslutning i användargränssnittet

Läs den här självstudiekursen för att lära dig hur du kopplar samman [!DNL Microsoft SQL Server] till Adobe Experience Platform via användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL SQL Server] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till [!DNL SQL Server] på [!DNL Platform]måste du ange följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Anslutningssträng | Anslutningssträngen som är associerad med din [!DNL Microsoft SQL Server] konto. Ditt anslutningssträngsmönster beror på om du använder servernamn eller instansnamn för datakällan:<ul><li>Anslutningssträng med servernamn: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Anslutningssträng med instansnamn:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Mer information om hur du kommer igång finns i [this [!DNL SQL Server] dokument](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Koppla samman [!DNL SQL Server] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *Databaser* kategori, välj **[!DNL Microsoft SQL Server]** och sedan markera **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visas **[!UICONTROL Set up]** när en viss källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Microsoft SQL Server-källan vald.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

The **[!UICONTROL Connect to Microsoft SQL Server]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

>[!BEGINTABS]

>[!TAB Skapa ett nytt konto]

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange ett namn, en valfri beskrivning och dina autentiseringsuppgifter.

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet med källanslutningsinformationen angiven och markerad.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Använd ett befintligt konto]

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och välj sedan det konto som du vill använda i den befintliga kontokatalogen.

Välj **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontogränssnittet som visar en lista över befintliga konton.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL SQL Server] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
