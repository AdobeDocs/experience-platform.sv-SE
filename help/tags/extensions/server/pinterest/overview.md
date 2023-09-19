---
keywords: tillägg för händelsevidarebefordran;pinterest;pinterest tillägg för händelsevidarebefordran
title: Pinterest-tillägg för händelsevidarebefordring
description: Med det här tillägget för vidarebefordran av Adobe Experience Platform-händelser kan du importera händelser till Pinterest för dina verksamhetsbehov.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 2%

---

# [!DNL Pinterest] tillägg för händelsevidarebefordring

[!DNL Pinterest] är en motor för visuell identifiering som att hitta idéer som recept, heminredning, stilinspiration med mera. Det finns miljarder stift på [!DNL Pinterest], som också kan delas med andra [!DNL Pinterest]. Du kan sammanställa användarinteraktionshändelserna och använda [!DNL Pinterest Analytics] för att förstå användarbeteende och köra riktade annonser.

The [[!DNL Pinterest] Konverteringar](https://developers.pinterest.com/docs/conversions/conversion-management/) API [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Pinterest]. Det här dokumentet beskriver tilläggets användningsfall, hur det installeras och hur du integrerar dess funktioner i din händelsevidarebefordran [regler](../../../ui/managing-resources/rules.md).

Åtkomsttoken för konverteringar är den autentiseringsmetod som används av [!DNL Pinterest] när du interagerar med [!DNL Pinterest] API.

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Pinterest] för att utnyttja sina funktioner för kundanalys.

Ta till exempel ett marknadsföringsteam i en organisation. Teamet samlar in data om användarinteraktionshändelser från sin webbplats och läser in dessa i [!DNL Pinterest] med det här tillägget för vidarebefordran av händelser.

Marknadsförings- och analysteam kan sedan utnyttja [!DNL Pinterest] Analysfunktioner för att förstå viktiga användarinteraktioner och beteenden, så att ni bättre kan förstå användarna och inrikta dem på riktade annonskampanjer.

Mer information om användningsfall för [!DNL Pinterest], se [[!DNL Pinterest] användningsfall](https://business.pinterest.com/en/success-stories) dokumentation.

## [!DNL Pinterest] krav {#prerequisites}

Du måste ha en giltig [!DNL Pinterest] [företagskonto](https://help.pinterest.com/en/business/article/get-a-business-account) för att kunna använda det här tillägget. Gå till [[!DNL Pinterest] registreringssida](https://www.pinterest.com/business/create/) för att registrera och skapa ett konto om du inte redan har ett.

Du behöver också en [!DNL Pinterest] utvecklarkonto, som måste kopplas till ditt [!DNL Pinterest] företagskonto. Om du vill associera ditt utvecklarkonto med ditt företagskonto kan du läsa [[!DNL Pinterest ] utvecklarkonto](https://developers.pinterest.com/account-setup/).

### Samla nödvändig konfigurationsinformation {#configuration-details}

För att ansluta Experience Platform till [!DNL Pinterest]krävs följande indata:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| ID för annonskonto | Dina [!DNL Pinterest] ID för annonskonto. Se [[!DNL Pinterest] dokumentation](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) för vägledning. | 123456789012 |
| Åtkomsttoken för konvertering | Dina [!DNL Pinterest] Åtkomsttoken för konvertering. Se [[!DNL Pinterest] Konverterings-API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) dokument för vägledning. <br> **Du behöver bara göra detta en gång eftersom denna token inte upphör att gälla.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installera och konfigurera [!DNL Pinterest] extension {#install}

Installera tillägget genom att [skapa en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller välj en befintlig egenskap att redigera i stället.

I vänster navigering väljer du **[!UICONTROL Extensions]**. Välj **[!UICONTROL Install]** på kortet för [!DNL Pinterest] i **[!UICONTROL Catalog]** -fliken.

![Katalog som visar [!DNL Pinterest] tillägg med [!UICONTROL Install] markerad.](../../../images/extensions/server/pinterest/install.png)

### Konfigurera [!DNL Pinterest] extension

>[!IMPORTANT]
>
>Beroende på implementeringsbehoven kan du behöva skapa ett schema, dataelement och en datauppsättning innan du konfigurerar tillägget. Granska alla konfigurationssteg innan du startar för att avgöra vilka enheter du måste konfigurera för ditt användningsfall.

I vänster navigering väljer du **[!UICONTROL Extensions]**. Välj **[!UICONTROL Configure]** på kortet för [!DNL Pinterest] i [!UICONTROL Installed]**.

![[!DNL Pinterest] som visas i [!UICONTROL Install] tabba med [!UICONTROL Configure] markerad.](../../../images/extensions/server/pinterest/configure.png)

På nästa skärm anger du [!UICONTROL Ads Account Id] och [!UICONTROL Conversion Access Token] som du tidigare samlat i [konfigurationsinformation](#configuration-details) -avsnitt. När du är klar väljer du **[!UICONTROL Save]**.

![The [!DNL Pinterest] [!UICONTROL Configure] skärmmarkering [!UICONTROL Ads Account Id] och [!UICONTROL Conversion Access Token] indatafält.](../../../images/extensions/server/pinterest/input.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som bestämmer när och hur händelserna ska skickas till [!DNL Pinterest].

Skapa ett nytt [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]**, lägga till en ny åtgärd och ange tillägget till **[!UICONTROL Pinterest]**. Skicka Edge Network-händelser till [!DNL Pinterest], ange **[!UICONTROL Action Type]** till **[!UICONTROL Send Event].**

![The [!DNL Pinterest] [!UICONTROL Send Event] skapa regel.](../../../images/extensions/server/pinterest/rule.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen. Du måste mappa [!DNL Pinterest] händelseegenskaper för de dataelement som du skapade tidigare.

### [!UICONTROL Event Data]

Följande händelsedata krävs för att skapa den nya regeln:

| Fältnamn | Beskrivning | Exempel |
| --- | --- | --- | 
| [!UICONTROL Event Name] | Typ av användarhändelse. Detta kan dock vara vilken händelsetyp som helst för att utnyttja [!DNL Pinterest Analytics] rekommenderas att använda [[!DNL Pinterest] händelsekoder](https://help.pinterest.com/en/business/article/add-event-codes) | * utcheckning <br> * add_to_cart <br> * page_visit <br> * registrering <br> * [Användardefinierad händelse] |
| [!UICONTROL Action Source] | Källan som anger var konverteringshändelsen inträffade. | * app_android <br> * app_ios <br> * webb <br> * offline |
| [!UICONTROL Event Time] | Detta avser händelsetiden. Standardtidsformatet som används är UNIX, i formatet `<seconds>.<miliseconds>` beroende på lokal tidszon. Mer information finns i [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 anger 1433188255 sekunder och 500 millisekunder efter epok, eller måndag, 1 juni 2015, 7:50:55 PM GMT. |
| [!UICONTROL Event ID] | En unik id-sträng som identifierar den här händelsen och kan användas för att ta bort händelser som importerats via både konverterings-API:t och Pinterest-spårning. Utan detta räknas händelsens data sannolikt två gånger och kommer att rapportera måttlig uppblåsning. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | Ett JSON-objekt som innehåller anpassade egenskaper för händelsen. Välj mellan att tillhandahålla rå JSON eller att använda en förenklad uppsättning indata för nyckelvärden. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![The [!DNL Pinterest] [!UICONTROL Event Data] markerat i regelåtgärden.](../../../images/extensions/server/pinterest/event-data.png)

Följande händelseegenskaper kan konfigureras:

| Fältnamn | Beskrivning |
| --- | --- |
| URL för händelsekälla | URL för webbkonverteringshändelsen. |
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
| [!UICONTROL Mobile Adverstising IDs] | Sha256 hash of user&#39;s &quot;Google Advertising IDs&quot; (GAIDs) or &quot;Apple Identifier for Advertisers&quot; (IDFAs) | ebd543592...f2b7e1 |
| [!UICONTROL Client IP Address] | Användarens IP-adress, som kan vara antingen i IPv4- eller IPv6-format. Används för matchning. | 192.168.0.1 |
| [!UICONTROL Client User Agent] | Användaragentsträngen för användarens webbläsare. | Mozilla/5.0 (plattform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | Ett JSON-objekt som innehåller annan kundinformation. Välj mellan att tillhandahålla rå JSON eller att använda en förenklad uppsättning indata för nyckelvärden. | { &quot;ph&quot;: &quot;122333445&quot; } |

![The [!DNL Pinterest] [!UICONTROL User Data] markerat i regelåtgärden.](../../../images/extensions/server/pinterest/user-data.png)

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
>Innan data skickas till [!DNL Pinterest] API-slutpunkten kommer tillägget att hash-koda och normalisera värdena för följande fält: E-post, Telefonnummer, Förnamn, Efternamn, Kön, Födelsedatum, Ort, Delstat, Postnummer, Land och Externt ID. Tillägget kommer inte att hash-koda värdet för dessa fält om det redan finns en SHA256-sträng.

### [!UICONTROL Custom Data]

Följande anpassade data kan anges för regeln:

| Fältnamn | Beskrivning |
| --- | --- |
| Valuta | ISO-4217-valutakoden. Om detta inte anges, [!DNL Pinterest] används som standard för annonserarens valuta som angavs när kontot skapades. |
| Värde | Händelsens totala värde. Accepteras som en sträng i begäran. Detta tolkas som en dubbelsiffra. |
| Söksträng | Söksträngen som är relaterad till användarkonverteringshändelsen. |
| Order-ID | Beställnings-ID. Skickar `order_id` hjälper [!DNL Pinterest] deduplicera händelser när det behövs. |
| Antal produkter | Totalt antal produkter för händelsen. Det totala antalet objekt som köpts i en utcheckningshändelse. |
| Innehålls-ID | Lista (matris) med produkt-ID:n. |
| Innehåll | En lista (array) med objekt som innehåller information om produkter, till exempel pris och kvantitet. |

![The [!DNL Pinterest] [!UICONTROL Custom Data] markerat i regelåtgärden.](../../../images/extensions/server/pinterest/custom-data.png)

## Validera data i [!DNL Pinterest]

När regeln för vidarebefordran av händelser har skapats och körts validerar du om händelsen som skickades till [!DNL Pinterest] API visas som förväntat i [!DNL Pinterest] Gränssnitt.

Om händelsesamlingen och [!DNL Experience Platform] integreringen lyckades, du kommer att se händelser i [!DNL Pinterest] Gränssnitt.

![The [!DNL Pinterest] händelsehanterare](../../../images/extensions/server/pinterest/event-history.png)

Du kan gå igenom och visa [!DNL Pinterest] distribution av händelsedata.

![The [!DNL Pinterest] datadistribution](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Nästa steg

I den här guiden beskrivs hur du installerar och konfigurerar [!DNL Pinterest] tillägg för händelsevidarebefordran i användargränssnittet. Mer information finns i den officiella dokumentationen:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] API-översikt för konverteringar](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
