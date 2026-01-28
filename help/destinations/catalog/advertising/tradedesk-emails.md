---
title: Trade Desk - CRM-anslutning
description: Aktivera profiler på ert Trade Desk-konto för målgruppsanpassning och undertryckning baserat på CRM-data.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---

# [!DNL Trade Desk] - CRM-anslutning

>[!IMPORTANT]
>
>Det finns två The Trade Desk - CRM-mål i [målkatalogen](/help/destinations/catalog/overview.md).
>
>* Om du hämtar data i EU använder du målet **[!DNL The Trade Desk - CRM (EU)]**.
>* Använd målet **[!DNL The Trade Desk - CRM (NAMER & APAC)]** om du hämtar data i APAC- eller NAMER-regionerna.
>
>Målanslutningen och dokumentationssidan skapas och underhålls av *[!DNL Trade Desk]*-teamet. Kontakta din [!DNL Trade Desk]-representant om du har frågor eller uppdateringsfrågor.

## Översikt {#overview}

Förstå hur du kan aktivera profiler för ditt [!DNL Trade Desk]-konto för målgruppsanpassning och inaktivering baserat på CRM-data.

Den här kopplingen skickar data till [!DNL The Trade Desk] för aktivering av förstahandsdata. [!DNL The Trade Desk] lagrar e-postmeddelanden och telefonnummer i Raw-format (ohashed).

>[!TIP]
>
>Använd målet [!DNL The Trade Desk - CRM] för att skicka CRM-data (till exempel e-post och telefonnummer) och andra identifierare för förstapartsdata som cookies och enhets-ID. Du kan fortsätta använda [Trade Desk-målet](/help/destinations/catalog/advertising/tradedesk.md) i Experience Platform-katalogen för cookies och enhets-ID-mappningar.

## Förhandskrav {#prerequisites}

>[!IMPORTANT]
>
>Innan du kan aktivera målgrupper på The Trade Desk måste du kontakta din [!DNL Trade Desk]-kontoansvarige för att aktivera funktionen. Om du skickar e-post, telefonnummer och UID2/EUID måste du dela det signerade UID2/EUID-avtalet med [!DNL The Trade Desk].

## Krav för ID-matchning {#id-matching-requirements}

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav. Mer information finns i [Översikt över identitetsnamnet](/help/identity-service/features/namespaces.md).

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

Adobe Experience Platform har stöd för både ohashade och hash-kodade e-postadresser och telefonnummer. Följ instruktionerna i avsnittet Krav för ID-matchning och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser.

| Målidentitet | Beskrivning |
|---|---|
| E-post | E-postadresser (klartext) |
| Email_LC_SHA256 | E-postadresser måste hash-kodas med SHA256 och nedsänkt. Du kan inte ändra den här inställningen senare. |
| Telefon (E.164) | Telefonnummer som måste normaliseras i E.164-format. E.164-formatet innehåller ett plustecken (+), en internationell landskod, en lokal områdeskod och ett telefonnummer. Till exempel: (+)(landskod)(riktnummer)(telefonnummer). Den här identifieraren är inte tillgänglig för Trade Desk - First-Party Data (EU). |
| Telefon (SHA256_E.164) | Telefonnummer som redan har normaliserats till E.164-format och sedan hashas med SHA-256, med den resulterande hash Base64-kodade. Den här identifieraren är inte tillgänglig för Trade Desk - First-Party Data (EU). |
| TDID | Cookie-ID i Trade Desk |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | Apple ID för annonsörer |
| UID2 | UID2-råvärdet |
| UID2Token | Den krypterade UID2-token, även kallad reklamtoken. |
| EUID | EU-id-råvärde |
| EUIDToken | Den krypterade EUID-token, även kallad reklamtoken. |
| RampID | RampID med 49 eller 70 tecken (tidigare IdentityLink eller IDL). Det här måste vara ett rampID från LiveRamp som mappas specifikt för The Trade Desk. |
| netID | Användarens netID som en base64-kodad sträng med 70 tecken. Detta ID stöds endast i Europa. |
| FirstID | Användarens First-id, en cookie från första part, som oftast används av utgivare i Frankrike. Detta ID stöds endast i Europa. |

{style="table-layout:auto"}

## Krav för e-posthashning {#email-hashing}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform eller använda obearbetade e-postadresser.

Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [gruppimporten](/help/ingestion/batch-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Ta bort inledande och avslutande blanksteg.
* Konvertera alla ASCII-tecken till gemener.
* Ta bort följande tecken från användarnamnsdelen i e-postadressen i `gmail.com`:

      * Perioden (`.`) tecken (ASCII-kod 46). Du kan till exempel normalisera &quot;jane.doe@gmail.com&quot; till &quot;janedoe@gmail.com&quot;.
     * Plustecknet (`+`) (ASCII-kod 43) och alla efterföljande tecken. Till exempel normalisera &quot;janedoe+home@gmail.com&quot; till &quot;janedoe@gmail.com&quot;.
  

## Normalisering av telefonnummer och krav på hashning {#phone-hashing}

Det här behöver du veta om att överföra telefonnummer:

* Du måste normalisera telefonnummer innan du skickar dem i en begäran, oavsett om du skickar dem som hashas eller ohashas i en begäran.
* Om du vill överföra normaliserade, hash-kodade och kodade data måste du skicka telefonnummer som Base64-kodade SHA-256-hashvärden för de normaliserade telefonnumren.

Oavsett om du vill överföra telefonnummer i Raw-format eller hashas måste du normalisera dem.

>[!IMPORTANT]
>
>Normalisering före hashning säkerställer att det genererade ID-värdet alltid är detsamma och att data kan matchas korrekt.

Det här behöver du veta om normalisering av telefonnummer:

* UID2 Operator godkänner telefonnummer i E.164-format, som är det internationella telefonnummerformatet som garanterar global unicitet.
* E.164-telefonnummer kan innehålla högst 15 siffror.
* Normaliserade E.164-telefonnummer använder följande syntax: `[+][country code][subscriber number including area code]` utan blanksteg, bindestreck, parenteser eller andra specialtecken. Här är några exempel:

      * USA: 1 (234) 567-8901 normaliseras till +12345678901.
     * Singapore: 65 1243 5678 normaliseras till +6512345678.
     * Australien: mobiltelefonnummer 0491 570 006 normaliseras för att lägga till landskoden och ta bort inledande nolla: +61491570006.
     * UK: Mobiltelefonnummer 07812 345678 normaliseras för att lägga till landskoden och ta bort inledande nolla: +447812345678.
  
Kontrollera att det normaliserade telefonnumret är UTF-8, inte något annat kodningssystem, till exempel UTF-16.

Hash för ett telefonnummer är en Base64-kodad SHA-256-hash av ett normaliserat telefonnummer. Telefonnumret normaliseras först, hashas med SHA-256-algoritmen och sedan kodas de resulterande byten av hash-värdet med Base64-kodning. Observera att Base64-kodningen tillämpas på byte i hash-värdet, inte på den hex-kodade strängbeteckningen.
I följande tabell visas ett exempel på ett enkelt telefonnummer för indata och resultatet när varje steg används för att få fram ett säkert, ogenomskinligt värde.

| Typ | Exempel | Kommentarer och användning |
|---|---|---|
| Råtelefonnummer | 1 (234) 567-8901 | Det här är startpunkten. |
| Normaliserat telefonnummer | +12345678901 | Normalisering är alltid det första steget. |
| SHA-256-hash av normaliserat telefonnummer | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | Denna 64-teckensträng är en hex-kodad representation av 32-byte SHA-256. |
| Hex till Base64 SHA-256-kodning av normaliserat och hashad telefonnummer | EObwtHBUqDNZR33LNSMdtt5cafsYFuGMY4ZLenlue4 | Denna 44-teckensträng är en Base64-kodad representation av 32-byte SHA-256. SHA-256-hash är ett hexadecimalt värde. Du måste använda en Base64-kodare som tar ett hexadecimalt värde som indata. Använd den här kodningen för phone_hash-värden som skickas i begärandetexten. |

>[!IMPORTANT]
>
>När du använder Base64-kodning måste du se till att använda en funktion som har ett hexadecimalt värde som indata. Om du använder en funktion som tar text som indata blir resultatet en längre sträng som inte är giltig i UID2.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (e-post eller hashad e-post) som används i Trade Desk-målet. |
| Exportfrekvens | **[!UICONTROL Daily Batch]** | När en profil uppdateras i Experience Platform baserat på målgruppsutvärdering uppdateras profilen (identiteterna) en gång om dagen nedströms till målplattformen. Läs mer om [batchexport](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

### Autentisera till mål {#authenticate}

CRM-målet [!DNL The Trade Desk] är en daglig batchfilöverföring och kräver ingen autentisering av användaren.

### Fyll i målinformation {#fill-in-details}

Innan du kan skicka, eller aktivera, målgruppsdata till ett mål måste du skapa en anslutning till din egen målplattform. När [konfigurerar](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) för det här målet måste du ange följande information:

* **[!UICONTROL Account Type]**: Välj alternativet **[!UICONTROL Existing Account]**.
* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Advertiser ID]**: din [!DNL Trade Desk Advertiser ID], som antingen kan delas av din [!DNL Trade Desk]-kontohanterare eller hittas under [!DNL Advertiser Preferences] i [!DNL Trade Desk]-gränssnittet.

![Experience Platform UI-skärmbild som visar hur du fyller i målinformation.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

När du ansluter till målet är det helt valfritt att ange en datastyrningsprincip. Mer information finns i Experience Platform [datastyrningsöversikt](/help/data-governance/policies/overview.md).

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för exportmål för gruppprofiler](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till ett mål.

På sidan **[!UICONTROL Scheduling]** kan du konfigurera schemat och filnamnen för varje målgrupp som du exporterar. Det är obligatoriskt att konfigurera schemat, men det är valfritt att konfigurera filnamnet.

![Experience Platform UI-skärmbild för att schemalägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alla målgrupper som är aktiverade på [!DNL The Trade Desk] CRM-målet ställs automatiskt in på en daglig frekvens och fullständig filexport.

![Experience Platform UI-skärmbild för att schemalägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

På sidan **[!UICONTROL Mapping]** måste du välja attribut eller identitetsnamnutrymmen från källkolumnen och mappa till målkolumnen.

![Experience Platform UI-skärmbild för att kartlägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Nedan visas ett exempel på korrekt identitetsmappning när målgrupper aktiveras till CRM-målet [!DNL The Trade Desk].

Välja käll- och målfält:

| Source | Målfält |
|---|---|
| E-post | e-post |
| Email_LC_SHA256 | hashed_email |
| Telefon (E.164) | telefon |
| Telefon (SHA256_E.164) | hashed_phone |
| TDID | tdid |
| GAID | daid |
| IDFA | idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | euid |
| EUIDToken | euid_token |
| RampID | idl |
| ID5 | id5 |
| netID | net_id |
| FirstID | first_id |


## Validera dataexport {#validate}

Om du vill verifiera att data exporteras korrekt från Experience Platform och till [!DNL The Trade Desk] kan du hitta målgrupperna på fliken Adobe 1PD i biblioteket [!DNL The Trade Desk] Advertiser Data and identity. Så här söker du efter motsvarande ID i användargränssnittet för [!DNL Trade Desk]:

1. Välj först fliken **[!UICONTROL Libraries]** och granska avsnittet **[!UICONTROL Advertiser data and identity]**.
2. Klicka på **[!UICONTROL Adobe 1PD]** så listas alla målgrupper som är aktiverade för [!DNL The Trade Desk].
3. Segmentnamnet eller segment-ID från Experience Platform visas som segmentnamn i användargränssnittet för [!DNL Trade Desk].

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).
