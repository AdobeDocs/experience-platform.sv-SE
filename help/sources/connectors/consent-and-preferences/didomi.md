---
title: Didomi Source - översikt
description: Lär dig hur du ansluter Didomi till Adobe Experience Platform med användargränssnittet.
hide: true
hidefromtoc: true
source-git-commit: 44c01678e96f2649dbf731dd4531004c1df28058
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# [!DNL Didomi]


[!DNL Didomi] är en plattform för hantering av samtycke och preferenser som hjälper organisationer att samla in, hantera och genomdriva användarval när det gäller personuppgifter på webbplatser, i appar och för interna verktyg.

Adobe Experience Platform stöder inmatning av data från ett stort antal externa system, inklusive molnlagring, databaser och program som [!DNL Didomi] via ett system med källanslutningar. Använd källor för att autentisera externa system, hantera dataflödet till Experience Platform och säkerställa ett konsekvent och strukturerat inmatningsbeteende för era kunddata.

Använd [!DNL Didomi]-källan för att strömma data om användarsamtycke och inställningar i realtid från [!DNL Didomi] till Experience Platform. Genom [!DNL Didomi]-källan kan ni centralisera och agera utifrån medgivandedata i Experience Platform och därigenom hålla era kundprofiler och arbetsflöden längre fram i kedjan kompatibla och uppdaterade.

![Databearbetningsarkitekturen för Didomi.](../../images/tutorials/create/didomi/flux.jpeg)

## Förhandskrav

Slutför de nödvändiga stegen nedan för att ansluta ditt [!DNL Didomi]-konto till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Didomi]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/ui/overview.md).

### Samla in Adobe API-autentiseringsuppgifter

Om du vill ansluta [!DNL Didomi] till Experience Platform på ett säkert sätt måste du autentisera med dina Adobe API-autentiseringsuppgifter. Dessa autentiseringsuppgifter är nödvändiga för att konfigurera webkroken och konfigurera datainmatning.

Läs guiden [Komma igång med Experience Platform API:er](../../../landing/api-authentication.md) om du vill ha information om hur du kan anropa Experience Platform API:er.

### Skapa ett Experience Platform-schema

>[!TIP]
>
>Du kan hoppa över det här steget om du redan har ett befintligt XDM-schema.

Ett **XDM-schema (Experience Data Model)** definierar strukturen för de data som du skickar från [!DNL Didomi] (t.ex. användar-ID:n, medgivandesyften) till Experience Platform.

Om du vill skapa ett schema väljer du [!UICONTROL Schemas] i den vänstra navigeringen i Experience Platform-gränssnittet och väljer **[!UICONTROL Create schema]**. Välj sedan **[!UICONTROL Standard]** som schematyp och välj sedan **[!UICONTROL Manual]** för att skapa dina fält manuellt. Välj en basklass för schemat och ange ett namn för schemat.

Uppdatera schemat när du har skapat det genom att lägga till något av dina obligatoriska fält. Se till att minst ett fält är ett [!UICONTROL Identity]-fält för att informera Experience Platform om dina primära identitetsvärden. Slutligen måste du aktivera växlingsknappen [!UICONTROL Profile] för att dina data ska kunna lagras.

![create-schema](../../images/tutorials/create/didomi/create-schema.png)

Mer information finns i guiden om att [skapa scheman i användargränssnittet](../../../xdm/tutorials/create-schema-ui.md).

### Skapa en datauppsättning

>[!TIP]
>
>Du kan hoppa över det här steget om du redan har en befintlig datauppsättning.

En **datauppsättning** i Experience Platform används för att lagra inkommande data baserat på det schema som du definierar.

Om du vill skapa en datauppsättning väljer du [!UICONTROL Datasets] i den vänstra navigeringen i Experience Platform-gränssnittet och sedan **[!UICONTROL Create dataset]**. Välj sedan **[!UICONTROL Create dataset from schema]** och välj sedan det schema som du vill koppla till den nya datauppsättningen.

![create-dataset](../../images/tutorials/create/didomi/create-dataset.png)

## Konfigurera HTTP-webkroken på [!DNL Didomi]-konsolen

[!DNL Webhooks] låter dig prenumerera på händelser som utlösts på [!DNL Didomi]-plattformen när användare interagerar med sina medgivandeinställningar. När en relevant händelse inträffar - till exempel när en användare ger eller återkallar sitt samtycke - skickar [!DNL Didomi] en HTTP POST-begäran i realtid som innehåller en JSON-nyttolast till den konfigurerade [!DNL webhook]-slutpunkten.

![didomi-console](../../images/tutorials/create/didomi/didomi-console.png)

För att säkerställa kompatibilitet med Experience Platform måste din webkrok uppfylla följande krav.

| Fält | Beskrivning | Exempel |
| --- | --- | --- | 
| Klienthemlighet | Den hemliga nyckel som är kopplad till dina Adobe API-autentiseringsuppgifter. | `d8f3b2e1-4c9a-4a7f-9b2e-8f1c3d2a1b6e` |
| API-nyckel | Den offentliga API-nyckel som används för att autentisera begäranden till Adobe-tjänster. |
| Typ av bidrag | Den metod som används för att hämta en åtkomsttoken från auktoriseringsservern. Ange det här värdet till `client_credentials`. | `client_credentials` |
| Omfång | Behörighetsomfattningarna definierar de specifika behörigheter eller åtkomstnivåer som ett program begär från API-providern. | `openid,AdobeID,read_organizations,additional_info.projectedProductContext,session` |
| Autentiseringshuvud | De ytterligare rubriker som krävs för Adobe-tokenbegäran. | `{"Content-type": "application/x-www-form-urlencoded"}` |
| Token-URL | Din Adobe-tokenslutpunkt. | `https://ims-na1.adobelogin.com/ims/token/v3` |
| URL för slutpunkt | Den sista Adobe Connector-URL:en (tillhandahålls i slutet av installationen). | `https://dcs.adobedc.net/collection/your-adobe-endpoint-id` |

{style="table-layout:auto"}

Konfigurera sedan följande alternativ för [!DNL webhook].

| Fält | Beskrivning | Värde |
| ---| --- | --- | 
| Begäranrubriker | De anpassade rubrikerna för [!DNL webhook]. Se till att du inkluderar `x-adobe-flow-id`. Du kan hämta det här värdet när [dataflödet har skapats](../../tutorials/ui/create/consent-and-preferences/didomi.md#retrieve-the-streaming-endpoint-url). | `{"Content-Type": "application/json", "Cache-Control": "no-cache", "x-adobe-flow-id": "{DATAFLOW_ID}"}` |
| Förenkla | Den här egenskapen måste kontrolleras eftersom den ser till att [!DNL webhook]-data skickas som ett platt objekt. | Aktiverad |
| Händelsetyper | Välj den specifika gruppen med [!DNL Didomi] händelser (`event.*` eller `user.*`) som ska utlösa [!DNL webhook]. Använd `event.*` för att spåra samtycke eller ändringar av inställningar och använd `user.*` för att spåra uppdateringar av användarprofiler. Det här valet krävs för att säkerställa att endast kompatibla händelser skickas till Adobe. Adobe har bara stöd för ett schema per dataflöde, så om du väljer båda händelsetyperna kan det leda till inmatningsfel. | Listan över händelsetyper som stöds är: <ul><li>`Event.created`</li><li>`Event.updated`</li><li>`Event.deleted`</li><li>`User.created`</li><li>`User.updated`</li><li>`User.deleted`</li></ul> |

### Hämta exempelnyttolastfilen {#download-the-sample-payload-file}

Baserat på den valda händelsegruppen hämtar du **exempelnyttolastfilen** direkt från [!DNL Didomi]-konsolen. Den här filen representerar datastrukturen och kommer att användas under schemat och mappningsstegen i Adobe.

| **Händelsegrupp** | **Exempelfil att hämta** | **Filtreringsalternativ** |
| --- | ---| --- |
| `event.*` | Hämta ett exempel för `event.created` | Filtrera bara för `event.*` händelser |
| `user.*` | Hämta ett exempel för `user.created` | Filtrera bara för `user.*` händelser |

## Anslut ditt [!DNL Didomi]-konto till Experience Platform

Läs guiden [Ansluta [!DNL Didomi] till Experience Platform](../../tutorials/ui/create/consent-and-preferences/didomi.md) om du vill veta hur du skapar en källanslutning och importerar data om samtycke och inställningar från [!DNL Didomi] till Experience Platform.