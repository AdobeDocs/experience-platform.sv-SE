---
keywords: e-post;E-post;e-post;e-postadresser;slutrutnätsmål
title: SendGrid-anslutning
description: Med SendGrid-målet kan du exportera dina egna data och aktivera dem i SendGrid för dina affärsbehov.
exl-id: 6f22746f-2043-4a20-b8a6-097d721f2fe7
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 0%

---

# [!DNL SendGrid] anslutning

## Översikt {#overview}

[SendGrid](https://www.sendgrid.com) är en populär plattform för kundkommunikation för transaktioner och marknadsföring.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL SendGrid Marketing Contacts API]](https://api.sendgrid.com/v3/marketing/contacts), som gör att du kan exportera dina e-postprofiler från första part och aktivera dem inom en ny SendGrid-målgrupp för dina affärsbehov.

SendGrid använder API-bearer-token som en autentiseringsmekanism för att kommunicera med SendGrid API:t.

## Förutsättningar {#prerequisites}

Följande objekt krävs innan du börjar konfigurera målet.

1. Du måste ha ett SendGrid-konto.
   * Gå till SendGrid [registrering](https://signup.sendgrid.com/) om du vill registrera och skapa ett SendGrid-konto, om du inte redan har ett.
1. När du har loggat in på SendGrid-portalen måste du också generera en API-token.
1. Navigera till webbplatsen SendGrid och gå till **[!DNL Settings]** > **[!DNL API Keys]** sida. Du kan även läsa [Dokumentation för SendGrid](https://app.sendgrid.com/settings/api_keys) för att få tillgång till rätt avsnitt i SendGrid-appen.
1. Slutligen väljer du **[!DNL Create API Key]** -knappen.
   * Se [Dokumentation för SendGrid](https://docs.sendgrid.com/ui/account-and-settings/api-keys#creating-an-api-key)om du behöver hjälp med vilka åtgärder som ska utföras.
   * Om du vill generera API-nyckeln via programmering kan du läsa [Dokumentation för SendGrid](https://docs.sendgrid.com/api-reference/api-keys/create-api-keys).

![](../../assets/catalog/email-marketing/sendgrid/01-api-key.jpg)

Innan du aktiverar data till SendGrid-målet måste du ha en [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som [!DNL Experience Platform]. Se även [gränser](#limits) längre ned på denna sida.

>[!IMPORTANT]
>
>* Det SendGrid-API som används för att skapa distributionslistan från e-postprofiler kräver att unika e-postadresser anges i varje profil. Detta är oberoende av om det används som ett värde för *e-post* eller *alternativ e-postadress*. Eftersom SendGrid-anslutningen stöder mappningar för både e-postadresser och alternativa e-postadresser måste du se till att alla e-postadresser som används är unika inom varje profil i *Datauppsättning*. Annars, när e-postprofilerna skickas till SendGrid, resulterar det i ett fel och den e-postprofilen kommer inte att finnas i dataexporten.
>
>* Det finns för närvarande ingen funktion för att ta bort profiler från SendGrid när de tas bort från målgrupper i Experience Platform.

## Identiteter som stöds {#supported-identities}

SendGrid stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| e-post | E-postadress | Observera att både oformaterad text och SHA256-hashade e-postadresser stöds av [!DNL Adobe Experience Platform]. Om källfältet för Experience-plattformen innehåller ohashade attribut ska du kontrollera **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen.<br/><br/> Observera att **SendGrid** stöder inte hash-kodade e-postadresser, så endast oformaterade textdata utan omformning skickas till målet. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda SendGrid-målet finns det exempel på användningsområden som [!DNL Experience Platform] kunder kan lösa genom att använda den här destinationen.

### Skapa en marknadsföringslista för flera marknadsföringsaktiviteter

Marknadsföringsteam som använder SendGrid kan skapa en e-postlista i SendGrid och fylla i den med e-postadresser. Den utskickslista som nu skapas i SendGrid kan sedan användas för flera marknadsföringsaktiviteter.

## Anslut till mål {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

1. I [!DNL Adobe Experience Platform] konsol, navigera till **Destinationer**.

1. Välj **Katalog** flik och sök efter *SendGrid*. Välj sedan **Konfigurera**. När du har upprättat en anslutning till målet ändras gränssnittsetiketten till **Aktivera segment**.
   ![](../../assets/catalog/email-marketing/sendgrid/02-catalog.jpg)

1. En guide visas som hjälper dig att konfigurera SendGrid-målet. Skapa det nya målet genom att välja **Konfigurera nytt mål**.
   ![](../../assets/catalog/email-marketing/sendgrid/03.jpg)

1. Välj **Nytt konto** och fylla i **Bearer Token** värde. Det här värdet är SendGrid *API-nyckel* som tidigare omnämns i [kravsektion](#prerequisites).
   ![](../../assets/catalog/email-marketing/sendgrid/04.jpg)

1. Välj **Anslut till mål**. Om SendGrid *API-nyckel* om du anger att det är giltigt visas ett **Ansluten** status med en grön bockmarkering kan du sedan gå vidare till nästa steg för att fylla i ytterligare informationsfält.

![](../../assets/catalog/email-marketing/sendgrid/05.jpg)

### Fyll i målinformation {#destination-details}

while [konfigurera](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Det namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En valfri beskrivning som hjälper dig att identifiera det här målet i framtiden.

![](../../assets/catalog/email-marketing/sendgrid/06.jpg)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

Se bilden nedan för mer information om det här målet.

1. Välj en eller flera målgrupper att exportera till SendGrid.
   ![](../../assets/catalog/email-marketing/sendgrid/11.jpg)

1. I **[!UICONTROL Mapping]** steg, efter markering **[!UICONTROL Add new mapping]** visas mappningssidan som mappar XDM-källfälten till API-målfälten för SendGrid. Bilderna nedan visar hur du mappar identitetsnamnutrymmen mellan Experience Platform och SendGrid. Se till att **[!UICONTROL Source field]** *E-post* ska mappas till **[!UICONTROL Target field]** *external_id* enligt nedan.
   ![](../../assets/catalog/email-marketing/sendgrid/13.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/14.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/15.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/16.jpg)

1. Du kan också mappa det önskade [!DNL Adobe Experience Platform] attribut som du vill exportera till SendGrid-målet.
   ![](../../assets/catalog/email-marketing/sendgrid/17.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/18.jpg)

1. När mappningarna är klara väljer du **[!UICONTROL Next]** för att gå vidare till granskningsskärmen.
   ![](../../assets/catalog/email-marketing/sendgrid/22.png)

1. Välj **[!UICONTROL Finish]** för att slutföra installationen.
   ![](../../assets/catalog/email-marketing/sendgrid/23.jpg)

Den omfattande listan över attributmappningar som stöds och som kan ställas in för [SendGrid Marketing Contacts > Add or Update Contact API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact) är under.

| Källfält | Målfält | Typ | Beskrivning | Gränser |
|---|---|---|---|---|
| xdm:<br/> homeAddress.street1 | xdm:<br/> address_line_1 | Sträng | Adressens första rad. | Maximal längd:<br/> 100 tecken |
| xdm:<br/> homeAddress.street2 | xdm:<br/> address_line_2 | Sträng | En valfri andra rad för adressen. | Maximal längd:<br/> 100 tecken |
| xdm:<br/> _extconndev.alternate_emails | xdm:<br/> alternativ_e-post | Array med strängen | Ytterligare e-postmeddelanden som är kopplade till kontakten. | <ul><li>Max: 5 objekt</li><li>Min: 0 objekt</li></ul> |
| xdm:<br/> homeAddress.city | xdm:<br/> stad | Sträng | Kontaktens stad. | Maximal längd:<br/> 60 tecken |
| xdm:<br/> homeAddress.country | xdm:<br/> land | Sträng | Kontaktens land. Kan vara ett fullständigt namn eller en förkortning. | Maximal längd:<br/> 50 tecken |
| identityMap:<br/> E-post | Identitet:<br/> external_id | Sträng | Kontaktens primära e-postadress. Detta måste vara en giltig e-postadress. | Maximal längd:<br/> 254 tecken |
| xdm:<br/> person.name.firstName | xdm:<br/> first_name | Sträng | Kontaktens namn | Maximal längd:<br/> 50 tecken |
| xdm:<br/> person.name.lastName | xdm:<br/> last_name | Sträng | Kontaktens familj | Maximal längd:<br/> 50 tecken |
| xdm:<br/> homeAddress.mailCode | xdm:<br/> mail_code | Sträng | Kontaktens postnummer eller annat postnummer. | |
| xdm:<br/> homeAddress.stateProvince | xdm:<br/> state_Province_region | Sträng | Kontaktens delstat, provins eller region. | Maximal längd:<br/> 50 tecken |

## Validera dataexporten i SendGrid {#validate}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över destinationer.
   ![](../../assets/catalog/email-marketing/sendgrid/25.jpg)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![](../../assets/catalog/email-marketing/sendgrid/26.jpg)

1. Växla till **[!DNL Activation data]** väljer du ett målgruppsnamn.
   ![](../../assets/catalog/email-marketing/sendgrid/27.jpg)

1. Övervaka målgruppssammanfattningen och kontrollera att antalet profiler motsvarar antalet som skapas i datauppsättningen.
   ![](../../assets/catalog/email-marketing/sendgrid/28.jpg)

1. The [SendGrid Marketing Lists > Create List API](https://docs.sendgrid.com/api-reference/lists/create-list) används för att skapa unika kontaktlistor i SendGrid genom att koppla värdet för *list_name* och tidsstämpeln för dataexporten. Navigera till SendGrid-webbplatsen och kontrollera om den nya kontaktlistan som överensstämmer med namnmönstret skapas.
   ![](../../assets/catalog/email-marketing/sendgrid/29.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/30.jpg)

1. Markera den nya kontaktlistan och kontrollera om den nya e-postposten från datauppsättningen som du skapade fylls i i den nya kontaktlistan.

1. Kontrollera också några e-postmeddelanden för att verifiera om fältmappningen är korrekt.
   ![](../../assets/catalog/email-marketing/sendgrid/31.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/32.jpg)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Detta SendGrid-mål utnyttjar API:erna nedan:
* [SendGrid Marketing Lists > Create List API](https://docs.sendgrid.com/api-reference/lists/create-list)
* [SendGrid Marketing Contacts > Add or Update Contact API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact)

### Gränser {#limits}

* The [SendGrid Marketing Contacts > Add or Update Contact API](https://api.sendgrid.com/v3/marketing/contacts) kan ta emot 30 000 kontakter eller 6 MB data, beroende på vilket som är lägst.
