---
title: Anslut Didomi till Experience Platform
description: Lär dig hur du ansluter ditt Didomi-konto till Experience Platform med användargränssnittet.
last-substantial-update: 2025-07-29T00:00:00Z
badge: Beta
exl-id: 1374574f-c8ba-4cf5-bad0-94a884f5c0a6
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Anslut [!DNL Didomi] till Experience Platform

>[!AVAILABILITY]
>
>Källan [!DNL Didomi] är i betaversion. Läs [villkoren](../../../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Didomi]-konto till Adobe Experience Platform med hjälp av källarbetsytan i användargränssnittet.

>[!IMPORTANT]
>
>* Dokumentationssidan skapades av *Didomi*-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *support@didomi.io*.
>* Stegvisa instruktioner för hur du skapar anslutningen finns i [dokumentationen för Didomi Adobe-källanslutningen](https://developers.didomi.io/integrations/third-party-apps/preference-management-platform-integrations/Adobe-source-connector).

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Konfigurera ditt [!DNL Didomi]-konto

Innan du kan fortsätta bör du kontrollera att du har läst och slutfört de nödvändiga stegen som beskrivs i [[!DNL Didomi] översikten](../../../../connectors/consent-and-preferences/didomi.md#prerequisites) för att ansluta ditt konto till Experience Platform.

## Navigera i källkatalogen

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL Didomi] går du till kategorin *[!UICONTROL Databases]*, markerar **[!UICONTROL Didomi]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![source-connector-list](../../../../images/tutorials/create/didomi/source-connector-list.png)

## Lägg till källdataschemat

Använd sedan gränssnittet *[!UICONTROL Select data]* för att överföra JSON-filen som [hämtades i de nödvändiga stegen](../../../../connectors/consent-and-preferences/didomi.md#download-the-sample-payload-file).

Du kan använda förhandsvisningsgränssnittet för att visa nyttolastens filstruktur. När du är klar väljer du **[!UICONTROL Next]**.

![add-data-schema](../../../../images/tutorials/create/didomi/add-data-schema.png)

## Ange information om dataflöde

Därefter måste du ange information om datauppsättningen och dataflödet.

### Information om datauppsättning

En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Data som har inhämtats till Experience Platform lagras i datasjön som datauppsättningar.

Under det här steget kan du antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

>[!NOTE]
>
>Oavsett om du använder en befintlig datauppsättning eller skapar en ny datauppsättning måste du se till att din datauppsättning är **aktiverad för**-profilinmatning.

+++Välj om du vill ha steg för att aktivera profilintagning, feldiagnostik och partiell förtäring.

Om din datauppsättning är aktiverad för kundprofil i realtid kan du under det här steget växla **[!UICONTROL Profile dataset]** för att aktivera dina data för profilinmatning. Du kan också använda det här steget för att aktivera **[!UICONTROL Error diagnostics]** och **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Välj **[!UICONTROL Error diagnostics]** om du vill instruera källan att skapa feldiagnostik som du kan referera till senare när du övervakar datauppsättningsaktiviteten och dataflödesstatusen.
* **[!UICONTROL Partial ingestion]**: Partiell gruppinmatning är möjligheten att importera data som innehåller fel, upp till ett visst konfigurerbart tröskelvärde. Med den här funktionen kan du importera alla korrekta data till Experience Platform, medan alla felaktiga data batchas separat med information om varför de är ogiltiga.

+++

### Information om dataflöde

När datauppsättningen har konfigurerats måste du ange information om dataflödet, inklusive ett namn, en valfri beskrivning och aviseringskonfigurationer.

![dataflödesinformation](../../../../images/tutorials/create/didomi/dataflow-details.png)

| Dataflödeskonfigurationer | Beskrivning |
| --- | --- |
| Dataflödesnamn | Dataflödets namn.  Som standard används namnet på filen som importeras. |
| Beskrivning | (Valfritt) En kort beskrivning av dataflödet. |
| Aviseringar | Experience Platform kan skapa händelsebaserade aviseringar som användare kan prenumerera på. Dessa alternativ är alla ett öppet dataflöde som utlöser dem.  Mer information finns i [varningsöversikten](../../alerts.md) <ul><li>**Källdataflödeskörning Start**: Välj den här aviseringen för att få ett meddelande när dataflödeskörningen börjar.</li><li>**Källdataflödet har körts**: Välj den här aviseringen om du vill få ett meddelande om dataflödet slutar utan fel.</li><li>**Körningsfel för källdataflöde**: Välj den här aviseringen för att få ett meddelande om dataflödet avslutas med fel.</li></ul> |

{style="table-layout:auto"}

## Mappning

Använd mappningsgränssnittet för att mappa källdata till rätt schemafält innan data importeras till Experience Platform.  Mer information finns i [mappningsguiden i användargränssnittet](../../../../../data-prep/ui/mapping.md)

Mappning används specifikt för att överföra **måldata** från [!DNL Didomi] till Experience Platform-datauppsättningen. Dessa syften representerar användarens val av samtycke (t.ex. för analys, personalisering, annonsering) och är de enda godkända mappningsfälten i den här integreringen.

Använd [webbkroknyttolasten som hämtats](../../../../connectors/consent-and-preferences/didomi.md#download-the-sample-payload-file) från webkrofginställningarna i [!DNL Didomi] för att mappa varje [!DNL Didomi] syfte till rätt fält i Adobe-datauppsättningen.

När du är klar väljer du **[!UICONTROL Next]**.

![mapping-details](../../../../images/tutorials/create/didomi/mapping-details.png)

## Granska

Steget *[!UICONTROL Review]* visas så att du kan granska informationen om dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar kontonamnet, källplattformen och källnamnet.
* **[!UICONTROL Assign dataset and map fields]**: Visar måldatauppsättningen och det schema som datauppsättningen följer.

När du har bekräftat att informationen är korrekt väljer du **[!UICONTROL Finish]**.

## Hämta URL för direktuppspelningsslutpunkt

När anslutningen har skapats visas informationssidan för källor. På den här sidan visas information om din nya anslutning, inklusive tidigare körda dataflöden, ID och URL för direktuppspelningsslutpunkt.

## Slutför konfigurationen på Adobe

När dataflödet har skapats går du till katalogen *[!UICONTROL Sources]* och väljer **[!UICONTROL Dataflows]**. Använd dataflödeskatalogen för att hitta [!DNL Didomi]-dataflödet och komma åt *[!UICONTROL Dataflow activity]*-gränssnittet. Använd sedan panelen *[!UICONTROL Properties]* till höger och hämta värden för följande:

* [!UICONTROL Streaming endpoint]
* [!UICONTROL Dataflow ID]

I Experience Platform-gränssnittet:

1. När du är klar med konfigurationen granskar du de konfigurationsparametrar som saknades i den första webkrok-konfigurationen.
2. När de här värdena är tillgängliga går du tillbaka till Didomi och uppdaterar webbkrokkonfigurationen.

![konfigurationsklar](../../../../images/tutorials/create/didomi/configuration-done.png)

## Uppdatera webbkrokkonfigurationen

När konfigurationen är klar går du tillbaka till [!DNL Didomi]-konsolen och uppdaterar webkrockkonfigurationen med **URL:en för direktuppspelningsslutpunkten** och **dataflödes-ID**.

När detta är klart börjar [!DNL Didomi] skicka händelser för samtyckeshantering och inställningshantering via integreringen, och data lagras i din Adobe-datauppsättning.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att hämta batchdata från din [!DNL Didomi]-källa till Experience Platform. Ytterligare resurser finns i dokumentationen nedan.

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det för att visa information om hur mycket data som har importerats, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen [Övervaka konton och dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

### Uppdatera ditt dataflöde

Om du vill uppdatera konfigurationer för schemaläggning, mappning och allmän information för dina dataflöden går du till självstudiekursen [Uppdatera källornas dataflöden i användargränssnittet](../../update-dataflows.md).

### Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med funktionen **[!UICONTROL Delete]** som finns på arbetsytan i **[!UICONTROL Dataflows]**. Mer information om hur du tar bort dataflöden finns i självstudiekursen [Ta bort dataflöden i användargränssnittet](../../delete.md).
