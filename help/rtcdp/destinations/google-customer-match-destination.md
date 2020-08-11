---
title: Google Customer Match Destination
seo-title: Google Customer Match Destination
description: Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Googles egna och styrda egenskaper, som Search, Shopping, Gmail och YouTube.
seo-description: Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Googles egna och styrda egenskaper, som Search, Shopping, Gmail och YouTube.
translation-type: tm+mt
source-git-commit: 31eb03c6625f820c9729caf5181c56e748e853a5
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---


# Google Customer Match Destination

## Översikt {#overview}

[Med Google Customer Match](https://support.google.com/google-ads/answer/6379332?hl=en) kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Googles egna och styrda egendomar, som: [!DNL Search], [!DNL Shopping], [!DNL Gmail]och [!DNL YouTube].

![Google Customer Match destination in the Real-time CDP UI](/help/rtcdp/destinations/assets/google-customer-match-catalog.png)

## Användningsexempel

För att du bättre ska förstå hur och när du ska använda [!DNL Google Customer Match] målet finns det exempel på användning som kunder med kunddataplattformen Adobe Real-time kan lösa med den här funktionen.


### Användningsfall 1

Ett sportklädvarumärke vill nå befintliga kunder genom [!DNL Google Search] [!DNL Google Shopping] och personalisera erbjudanden och objekt baserat på deras tidigare köp och webbhistorik. Kläddervarumärket kan importera e-postadresser från sin egen CRM till Adobe CDP i realtid, bygga segment utifrån sina egna offlinedata och skicka dessa segment för [!DNL Google Customer Match] användning i olika delar [!DNL Search] och [!DNL Shopping]optimera sina annonsutgifter.

### Användningsfall nr 2

Ett framstående teknikföretag har just släppt en ny telefon. För att marknadsföra den nya telefonmodellen vill de öka medvetenheten om de nya funktionerna i telefonen för kunder som äger tidigare modeller av sina telefoner.

För att befordra releasen överför de e-postadresser från sin CRM-databas till CDP i realtid i Adobe, med e-postadresserna som identifierare. Segment skapas baserat på kunder som äger äldre telefonmodeller och skickas till [!DNL Google Customer Match] så att de kan rikta sig till befintliga kunder, kunder som äger äldre telefonmodeller samt liknande kunder på [!DNL YouTube].

## Datastyrning för [!DNL Google Customer Match] destinationer {#data-governance}

Destinationerna i CDP i realtid i Adobe kan ha vissa regler och skyldigheter för data som skickas till eller tas emot från målplattformen. Du ansvarar för att förstå begränsningar och skyldigheter för dina data och hur du använder dessa data i Adobe Experience Platform och målplattformen. Adobe Experience Platform tillhandahåller datastyrningsverktyg som hjälper er att hantera vissa av dessa dataanvändningsskyldigheter. [Läs mer](/help/data-governance/labels/overview.md) om verktyg och policyer för datastyrning.

## Aktiveringstyp och identiteter {#activation-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer osv.) används i [!DNL Google Customer Match] målet.

**Identiteter** - du kan använda råa eller hashad e-post som kund-ID i Google

## [!DNL Google Customer Match] kontokrav {#google-account-prerequisites}

Innan du konfigurerar ett [!DNL Google Customer Match] mål i realtid-CDP måste du kontrollera att du läser och följer Googles användarpolicy [!DNL Customer Match]som beskrivs i [Googles supportdokumentation](https://support.google.com/google-ads/answer/6299717).

### Tillåtelselista {#allowlist}

>[!NOTE]
>
>Det är obligatoriskt att lägga till i Googles tillåtelselista innan du ställer in ditt första [!DNL Google Customer Match] mål i Adobe Real-time CDP. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar [!DNL Google Customer Match] destinationen i realtid för Adobe CDP måste du kontakta Google och följa instruktionerna i [Use Customer Match partners för att överföra dina data](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) i Googles dokumentation.


### Krav för e-posthashning {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google kräver att ingen personligt identifierbar information (PII) skickas i klartext. Därför måste de målgrupper som aktiverats för [!DNL Google Customer Match] kapas av *hash-* e-postadresser. Du kan välja att hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller så kan du välja att arbeta med e-postadresser i klartext i Experience Platform och låta algoritmen hash-koda dem när de aktiveras.

Mer information om Googles hash-krav och andra begränsningar för aktivering finns i följande avsnitt i Googles dokumentation:

* [[!DNL Customer Match] med e-postadress, adress eller användar-ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] överväganden](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [](/help/ingestion/batch-ingestion/overview.md) batchimporten och översikten över [det](/help/ingestion/streaming-ingestion/overview.md)vanligaste inmatningsproblemet.

Om du väljer att hash-koda e-postadresserna själv måste du se till att följa kraven för Google som beskrivs i länkarna ovan.


>[!IMPORTANT]
>
>Om du väljer att inte hash-koda e-postadresser gör Adobe Real-time CDP det åt dig när du aktiverar segment till [!DNL Google Customer Match]. I [aktiveringsarbetsflödet](/help/rtcdp/destinations/google-customer-match-destination.md#activate-segments) (se steg 5) väljer du det `Email` alternativ som visas nedan för e-postadresser *med* oformaterad text och `Email_LC_SHA256` för *hash-adresser*.


![Hindrar vid aktivering](/help/rtcdp/destinations/assets/identity-mapping.png)

## Anslut till mål {#connect-destination}

1. Bläddra till **[!UICONTROL Destinations]** kategorin i **[!UICONTROL Catalog]**> **[!UICONTROL Advertising]** . Markera [!DNL Google Customer Match]och markera sedan **[!UICONTROL Configure]**.

   ![Anslut till Googles kundmatchningsmål](/help/rtcdp/destinations/assets/connect-google-customer-match.png)

2. Om du tidigare har konfigurerat en anslutning till ditt **mål i** kontosteget [!DNL Google Customer Match] markerar du **[!UICONTROL Existing Account]** och väljer den befintliga anslutningen. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till [!DNL Google Customer Match]. Välj **[!UICONTROL Connect to destination]** att logga in och ansluta Adobe Experience Cloud till ditt [!DNL Google Ad] konto.

   >[!NOTE]
   >
   >CDP i realtid i Adobe stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt [!DNL Google Ad] konto. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till Google Customer Match-målet - autentiseringssteg](/help/rtcdp/destinations/assets/google-customer-match-pre-connect-view.png)

3. När dina inloggningsuppgifter har bekräftats och Adobe Experience Cloud är anslutet till ditt Google-konto kan du välja **[!UICONTROL Next]** att fortsätta till **[!UICONTROL Setup]** steget.

   ![Autentiseringsuppgifterna har bekräftats](/help/rtcdp/destinations/assets/google-customer-match-connection-success.png)

4. I **[!UICONTROL Authentication]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet och fyller i din Google-fil **[!UICONTROL Account ID]**. <br> I det här steget kan du även välja vilket som helst **[!UICONTROL Marketing use case]** som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](/help/data-governance/policies/overview.md#core-actions). <br> Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   >[!IMPORTANT]
   >
   > För [!DNL Google Customer Match] destinationer. **[!UICONTROL Account ID]** är ditt kund-ID hos Google. Formatet på ID:t är xxx-xxx-xxxx.

   ![Koppla ihop Google-kunder - autentiseringssteg](/help/rtcdp/destinations/assets/google-customer-match-authentication-step.png)

5. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till [!DNL Google Customer Match]](#activate-segments), för resten av arbetsflödet.


## Aktivera segment för att [!DNL Google Customer Match] {#activate-segments}

Så här aktiverar du segment till [!DNL Google Customer Match]:

1. I **[!UICONTROL Destinations > Browse]** väljer du det [!DNL Google Customer Match] mål där du vill aktivera segmenten.
2. Klicka på målets namn. Då kommer du till aktiveringsflödet.
   ![activate-flow](/help/rtcdp/destinations/assets/google-customer-match-activate-flow.png)Observera att om det redan finns ett aktiveringsflöde för ett mål kan du se de segment som för närvarande skickas till målet. Välj **[!UICONTROL Edit activation]** i den högra listen och följ stegen nedan för att ändra aktiveringsinformationen.
3. Välj **[!UICONTROL Activate]**;
4. I **[!UICONTROL Activate destination]** arbetsflödet på **[!UICONTROL Select Segments]** sidan väljer du vilka segment som ska skickas till [!DNL Google Customer Match].
   ![segment-till-mål](/help/rtcdp/destinations/assets/activate-segments-google-customer-match.png)
5. I **[!UICONTROL Identity mapping]** steget väljer du vilka attribut som ska inkluderas som en identitet i det här målet. Välj **[!UICONTROL Add new mapping]** och bläddra i ditt schema, välj e-post och/eller hashad e-post och mappa dem till motsvarande målidentitet
   ![inledande skärm för identitetsmappning](/help/rtcdp/destinations/assets/gcm-identity-mapping.png) <br> 
   *E-postadress för oformaterad text som primär identitet*: Om du har oformaterad text (ej hash-kodade) e-postadresser som primär identitet i ditt schema, markerar du e-postfältet i ditt schema **[!UICONTROL Source Attributes]** och mappar till e-postfältet i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan:
   ![välj e-postadress för oformaterad text](/help/rtcdp/destinations/assets/gcm-raw-email.gif) <br> 
   *Hash-kodad e-postadress som primär identitet*: Om du har hash-kodat e-postadresser som primär identitet i ditt schema, markerar du det hash-kodade e-postfältet i ditt schema **[!UICONTROL Source Attributes]** och mappar till fältet Email_LC_SHA256 i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan:
   ![välj identitet för hash-kodade e-postmeddelanden](/help/rtcdp/destinations/assets/gcm-hashed-emails.gif) <br> 
6. På **[!UICONTROL Segment schedule]** sidan kan du ange startdatum för att skicka data till målet.
7. På **[!UICONTROL Review]** sidan visas en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta urvalet och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker CDP i realtid efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](/help/rtcdp/privacy/data-governance-overview.md#enforcement) i dokumentationsavsnittet för datastyrning.

![bekräfta-val](/help/rtcdp/destinations/assets/data-policy-violation.png)

Om inga principöverträdelser har identifierats markerar du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![bekräfta-val](/help/rtcdp/destinations/assets/gcm-review.png)


<!--

Insert in Step 6 when mobile device ID activation is available

    >[!IMPORTANT]
    >
    >If you select mobile device IDs (GAID or IDFA) as primary identity in the Identity mapping step, you must also provide an Application Id in this step. If you selected GAID as identity, see [Set the Application ID](https://developer.android.com/studio/build/application-id) in the Android developer documentation. IF you selected IDFA as identity, see [App ID](https://developer.android.com/studio/build/application-id) in the Apple developer documentation.

    ![segment schedule page](/help/rtcdp/destinations/assets/gcm-segment-schedule.png) 

-->

## Verifiera att segmentaktiveringen lyckades {#verify-activation}

När aktiveringsflödet är klart växlar du till ditt **[!UICONTROL Google Ads]** konto. De aktiverade segmenten visas nu som kundlistor på ditt Google-konto. Observera att beroende på segmentstorleken kommer vissa målgrupper inte att fyllas i om det inte finns fler än 100 aktiva användare att betjäna.