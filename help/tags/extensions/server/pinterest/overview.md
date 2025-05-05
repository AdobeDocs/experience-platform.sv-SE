---
keywords: tillägg för händelsevidarebefordran;pinterest;pinterest tillägg för händelsevidarebefordran
title: Pinterest-tillägg för händelsevidarebefordring
description: Med det här tillägget för vidarebefordran av Adobe Experience Platform-händelser kan du importera händelser till Pinterest för dina verksamhetsbehov.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---

# [!DNL Pinterest]-tillägg för händelsevidarebefordring

[!DNL Pinterest] är en visuell identifieringsmotor för att hitta idéer som recept, heminredning, stilinspiration med mera. Det finns miljarder punkter på [!DNL Pinterest], som också kan delas med andra på [!DNL Pinterest]. Du kan sortera användarinteraktionshändelserna och dra nytta av [!DNL Pinterest Analytics] för att förstå användarbeteendet och köra riktade annonser.

Med tillägget [[!DNL Pinterest] Konverteringar](https://developers.pinterest.com/docs/conversions/conversion-management/) API [för vidarebefordran av händelser](../../../ui/event-forwarding/overview.md) kan du utnyttja data som har samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Pinterest]. Det här dokumentet beskriver tilläggets användningsfall, hur det installeras och hur du integrerar dess funktioner i [regler](../../../ui/managing-resources/rules.md) för vidarebefordran av händelser.

Åtkomsttoken för konvertering är den autentiseringsmetod som används av [!DNL Pinterest] vid interaktion med API:t [!DNL Pinterest].

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Pinterest] för att utnyttja dess funktioner för kundanalys.

Ta till exempel ett marknadsföringsteam i en organisation. Teamet hämtar händelsedata för användarinteraktion från sin webbplats och läser in dem till [!DNL Pinterest] med det här tillägget för händelsevidarebefordran.

Marknadsförings- och analysteam kan sedan utnyttja [!DNL Pinterest] analysfunktioner för att förstå viktiga användarinteraktioner och beteenden, så att ni bättre kan förstå användare och inrikta er på dem för riktade annonskampanjer.

Mer information om användningsfall som är specifika för [!DNL Pinterest] finns i dokumentationen för [[!DNL Pinterest] användningsfall](https://business.pinterest.com/en/success-stories).

## Krav för [!DNL Pinterest] {#prerequisites}

Du måste ha ett giltigt [!DNL Pinterest] [företagskonto](https://help.pinterest.com/en/business/article/get-a-business-account) för att kunna använda det här tillägget. Gå till registreringssidan [[!DNL Pinterest] för att registrera dig och skapa ett konto om du inte redan har ett.](https://www.pinterest.com/business/create/)

Du behöver också ett [!DNL Pinterest]-utvecklarkonto, som måste kopplas till ditt [!DNL Pinterest]-företagskonto. Mer information om hur du associerar ditt utvecklarkonto med ditt företagskonto finns i [[!DNL Pinterest &#x200B;] utvecklarkontot](https://developers.pinterest.com/account-setup/).

### Samla nödvändig konfigurationsinformation {#configuration-details}

Följande indata krävs för att ansluta Experience Platform till [!DNL Pinterest]:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| ID för annonskonto | Ditt [!DNL Pinterest] Ads-konto-ID. Mer information finns i [[!DNL Pinterest] dokumentationen](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). | 123456789012 |
| Åtkomsttoken för konvertering | Åtkomsttoken för konvertering av [!DNL Pinterest]. Mer information finns i [[!DNL Pinterest] Konverterings-API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) -dokumentet. <br> **Du behöver bara göra detta en gång eftersom denna token inte upphör att gälla.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installera och konfigurera tillägget [!DNL Pinterest] {#install}

Om du vill installera tillägget [skapar du en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller väljer en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. Välj **[!UICONTROL Install]** på kortet för tillägget [!DNL Pinterest] på fliken **[!UICONTROL Catalog]**.

![Katalog som visar tillägget [!DNL Pinterest] med [!UICONTROL Install] markerat.](../../../images/extensions/server/pinterest/install.png)

### Konfigurera tillägget [!DNL Pinterest]

>[!IMPORTANT]
>
>Beroende på implementeringsbehoven kan du behöva skapa ett schema, dataelement och en datauppsättning innan du konfigurerar tillägget. Granska alla konfigurationssteg innan du startar för att avgöra vilka enheter du måste konfigurera för ditt användningsfall.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. Välj **[!UICONTROL Configure]** på kortet för tillägget [!DNL Pinterest] på fliken [!UICONTROL Installed]**.

Tillägget ![[!DNL Pinterest] visas på fliken [!UICONTROL Install] med [!UICONTROL Configure] markerat.](../../../images/extensions/server/pinterest/configure.png)

På nästa skärm anger du de [!UICONTROL Ads Account Id] och [!UICONTROL Conversion Access Token] som du tidigare samlade in i avsnittet [konfigurationsinformation](#configuration-details). När du är klar väljer du **[!UICONTROL Save]**.

![Skärmen [!DNL Pinterest] [!UICONTROL Configure] som markerar indatafälten [!UICONTROL Ads Account Id] och [!UICONTROL Conversion Access Token].](../../../images/extensions/server/pinterest/input.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som avgör när och hur händelser skickas till [!DNL Pinterest].

Skapa en ny [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]** lägger du till en ny åtgärd och anger tillägget till **[!UICONTROL Pinterest]**. Om du vill skicka Edge Network-händelser till [!DNL Pinterest] anger du **[!UICONTROL Action Type]** till **[!UICONTROL Send Event].**

![Skapandet av [!DNL Pinterest] [!UICONTROL Send Event]-regeln.](../../../images/extensions/server/pinterest/rule.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen. Du måste mappa händelseegenskaperna [!DNL Pinterest] till dataelementen som du tidigare har skapat.

### [!UICONTROL Event Data]

Följande händelsedata krävs för att skapa den nya regeln:

| Fältnamn | Beskrivning | Exempel |
| --- | --- | --- | 
| [!UICONTROL Event Name] | Typ av användarhändelse. Det här kan vara vilken händelsetyp som helst, men om du vill utnyttja [!DNL Pinterest Analytics] rekommenderar vi att du använder [[!DNL Pinterest] händelsekoder](https://help.pinterest.com/en/business/article/add-event-codes) | * utcheckning <br> * add_to_cart <br> * page_visit <br> * registrering <br> * [användardefinierad händelse] |
| [!UICONTROL Action Source] | Källan som anger var konverteringshändelsen inträffade. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Event Time] | Detta avser händelsetiden. Standardtidsformatet som används är UNIX, i formatet `<seconds>.<miliseconds>` beroende på din lokala tidszon. Mer information finns i [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 anger 1433188255 sekunder och 500 millisekunder efter epok, eller måndag, 1 juni 2015, kl. 7:50:55 PM GMT. |
| [!UICONTROL Event ID] | En unik id-sträng som identifierar den här händelsen och kan användas för att ta bort händelser som importerats via både konverterings-API:t och Pinterest-spårning. Utan detta räknas händelsens data sannolikt två gånger och kommer att rapportera måttlig uppblåsning. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | Ett JSON-objekt som innehåller anpassade egenskaper för händelsen. Välj mellan att tillhandahålla rå JSON eller att använda en förenklad uppsättning indata för nyckelvärden. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![Det [!DNL Pinterest] [!UICONTROL Event Data] som markeras i regelåtgärden.](../../../images/extensions/server/pinterest/event-data.png)

Följande händelseegenskaper kan konfigureras:

| Fältnamn | Beskrivning |
| --- | --- |
| Händelse-Source-URL | URL för webbkonverteringshändelsen. |
| Programarkiv-ID | App-ID:t för appbutiken. |
| Programnamn | Programmets namn. |
| Programversion | Versionen av programmet. |
| Enhetsmärke | Varumärke för den enhet som används av användaren. |
| Enhetsbärare | Användarens mobiloperatör för sin enhet. |
| Enhetsmodell | Modell för användarens enhet. |
| Enhetstyp | Typ av enhet som används av användaren. |
| OS-version | Version av enhetens operativsystem. |
| Användarspråk | ISO-639-1-språkkod med två tecken som anger användarens språk. |

### [!UICONTROL User Data]

Följande användardata kan anges av obligatoriska fält:

| Fältnamn | Beskrivning | Exempel |
| --- | --- | --- | 
| [!UICONTROL Email] | Användarens e-postadress eller en SHA256-hash av användarens e-postadress. | ebd543592...f2b7e1 |
| [!UICONTROL Mobile Adverstising IDs] | Sha256 hash of user&#39;s &quot;Google Advertising IDs&quot; (GAID) or &quot;Apple Identifier for Advertisers&quot; (IDFAs) | ebd543592...f2b7e1 |
| [!UICONTROL Client IP Address] | Användarens IP-adress, som kan vara antingen i IPv4- eller IPv6-format. Används för matchning. | 192.168.0.1 |
| [!UICONTROL Client User Agent] | Användaragentsträngen för användarens webbläsare. | Mozilla/5.0 (plattform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | Ett JSON-objekt som innehåller annan kundinformation. Välj mellan att tillhandahålla rå JSON eller att använda en förenklad uppsättning indata för nyckelvärden. | { &quot;ph&quot;: &quot;122333445&quot; } |

![Det [!DNL Pinterest] [!UICONTROL User Data] som markeras i regelåtgärden.](../../../images/extensions/server/pinterest/user-data.png)

De egenskaper för kundinformation som kan konfigureras är:

| Fältnamn | Beskrivning |
| --- | --- |
| Telefon | Användarens kontaktnummer. Endast siffror accepteras och ska anges med landskod, riktnummer och nummer. |
| Kön | Kön kan anges som antingen&quot;f&quot; för hona,&quot;m&quot; för hane eller&quot;n&quot; för icke-binära. |
| Födelsedatum | Födelsedatum, angivet som år, månad och dag. |
| Efternamn | Användarens efternamn. |
| Förnamn | Användarens förnamn. |
| Ort | Användarens bosättningsort. Detta används mest för faktureringsändamål. |
| Läge | Användarens tillstånd, som anges med två bokstäver i gemener. |
| Postnummer | Användarens postnummer, som främst används för fakturering. |
| Land | ISO-3166-landskod med två tecken som anger användarens land. |
| Externt ID | Unikt ID från annonsören som identifierar en användare i sitt space. Till exempel användar-ID, lojalitets-ID. |
| Klicka på ID | Den unika identifieraren som lagras i _epik cookie på din domän eller i &amp;epik= query-parametern i URL:en. |

>[!IMPORTANT]
>
>Innan data skickas till API-slutpunkten [!DNL Pinterest] kommer tillägget att hash-koda och normalisera värdena för följande fält: E-post, Telefonnummer, Förnamn, Efternamn, Kön, Födelsedatum, Ort, Delstat, Postnummer, Land och Externt ID. Tillägget kommer inte att hash-koda värdet för dessa fält om det redan finns en SHA256-sträng.

### [!UICONTROL Custom Data]

Följande anpassade data kan anges för regeln:

| Fältnamn | Beskrivning |
| --- | --- |
| Valuta | ISO-4217-valutakoden. Om detta inte anges kommer [!DNL Pinterest] att ange annonsöerns valuta som angavs när kontot skapades som standard. |
| Värde | Händelsens totala värde. Accepteras som en sträng i begäran. Detta tolkas som en dubbelsiffra. |
| Söksträng | Söksträngen som är relaterad till användarkonverteringshändelsen. |
| Order-ID | Beställnings-ID. Om du skickar `order_id` kan [!DNL Pinterest] deduplicera händelser vid behov. |
| Antal produkter | Totalt antal produkter för händelsen. Det totala antalet objekt som köpts i en utcheckningshändelse. |
| Innehålls-ID | Lista (matris) med produkt-ID:n. |
| Innehåll | En lista (array) med objekt som innehåller information om produkter, till exempel pris och kvantitet. |

![Det [!DNL Pinterest] [!UICONTROL Custom Data] som markeras i regelåtgärden.](../../../images/extensions/server/pinterest/custom-data.png)

## Validera data i [!DNL Pinterest]

När regeln för vidarebefordran av händelser har skapats och körts kontrollerar du om händelsen som skickades till [!DNL Pinterest]-API:t visas som förväntat i [!DNL Pinterest]-gränssnittet.

Om händelsesamlingen och integreringen av [!DNL Experience Platform] lyckades, kommer du att se händelser i användargränssnittet för [!DNL Pinterest].

![Händelsehanteraren [!DNL Pinterest]](../../../images/extensions/server/pinterest/event-history.png)

Du kan gå igenom och visa distributionen av händelsedata för [!DNL Pinterest] ytterligare.

![Datadistributionen [!DNL Pinterest]](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Nästa steg

I den här guiden beskrivs hur du installerar och konfigurerar tillägget [!DNL Pinterest] för vidarebefordran av händelser i användargränssnittet. Mer information finns i den officiella dokumentationen:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] API-översikt för konvertering](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
