---
keywords: mål; frågor; vanliga frågor; frågor och svar; destinationer faq
title: Vanliga frågor och svar
description: Svar på de vanligaste frågorna om Adobe Experience Platform destinationer
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---

# Vanliga frågor och svar {#faq}

## Översikt {#overview}

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform destinationer. För frågor och felsökning som rör andra [!DNL Platform]-tjänster, inklusive de som har påträffats i alla [!DNL Platform] API:er, se [felsökningsguiden för Experience Platform](../landing/troubleshooting.md).

## Vanliga frågor om destinationer {#general}

### Varför visas olika antal profiler i användargränssnittet i Experience Platform och i de exporterade CSV-filerna?

+++Svar
Detta är ett normalt beteende på grund av hur Experience Platform utför segmentering.

Direktuppspelningssegmentering uppdaterar profilantalet för direktuppspelade målgrupper under hela dagen, medan batchsegmentering uppdaterar profilantalet för batchmålgrupper en gång var 24:e timme.

När målgruppens exportschema skiljer sig från segmenteringsschemat, kommer antalet profiler mellan användargränssnittet och den exporterade [!DNL CSV]-filen att vara olika, särskilt när det gäller direktuppspelade målgrupper.

Mer information finns i [dokumentationen för segmenteringstjänsten](../segmentation/home.md).
+++

### Varför ser jag låga matchningsfrekvenser när en uppdaterad målgrupp inaktiveras och återaktiveras till samma mål?

+++Svar

Avaktiveringen och för en målgrupp från en direktuppspelningsdestination utlöser inte en återfyllning när målgruppen återaktiveras till samma direktuppspelningsmål.

**Exempel**

Du har aktiverat en målgrupp bestående av 10 profiler för en direktuppspelningsdestination.

När ni har aktiverat målgruppen inser ni att ni vill ändra målgruppskonfigurationen, så att ni inaktiverar målgruppen och ändrar dess populationskriterier, vilket leder till en målgruppspopulation på 100 profiler.

Du återaktiverar den uppdaterade målgruppen till samma mål, men eftersom ingen bakgrundsfyllning utlöses får målplatsen inte de ytterligare 90 profilerna.

**Lösning**

För att vara säker på att alla profiler skickas till ditt mål måste du skapa en ny målgrupp med den nya konfigurationen och sedan aktivera den till ditt mål.

+++

### När en målgrupp tas bort från ett mål, finns det någon signal som skickas till målet som anger att målgruppen tas bort?

+++Svar

Nej, det finns inget beroende mellan Experience Platform-målet och kundinstansen i målsystemet. På den mottagande sidan är det enda som tyder på att målsystemet skulle se att det slutade ta emot målgruppsdata.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Vad behöver jag göra innan jag kan aktivera målgrupper i [!DNL Facebook Custom Audiences]?

+++Svar
Innan du kan skicka dina målgrupper till [!DNL Facebook] måste du kontrollera att du uppfyller följande krav:

* Ditt [!DNL Facebook]-användarkonto måste ha behörigheten **[!DNL Manage campaigns]** aktiverad för annonskontot som du tänker använda.
* Affärskontot **Adobe Experience Cloud** måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Mer information finns i [Lägg till partner i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i Facebook-dokumentationen.

  >[!IMPORTANT]
  >
  > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera behörigheten **Hantera kampanjer**. Detta krävs för integreringen av [!DNL Adobe Experience Platform].
* Läs och signera [!DNL Facebook Custom Audiences] användarvillkoren. Det gör du genom att gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].
+++

### Behöver jag lägga till några appar eller pixlar i mitt [!DNL Facebook]-annonserarkonto?

+++Svar
Nej. Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.
+++

### Hur lång tid tar det för Facebook att bearbeta information från Adobe Experience Platform?

+++Svar
Från om med mars 2021 behöver [!DNL Facebook Custom Audiences] upp till en timme på sig att bearbeta information som tagits emot från [!DNL Platform].
+++

### Kan jag använda [!DNL Facebook Custom Audiences] för målgruppsanpassning i andra [!DNL Facebook]-appar, som [!DNL Instagram]?

+++Amswer
Du kan använda målet [!DNL Facebook Custom Audiences] för målgrupper i alla Facebook-appar som stöds av [!DNL Facebook Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] och [!DNL Messenger]. Markeringen av appen som annonsörer vill köra kampanjer på anges på placeringsnivån i [!DNL Facebook Ads Manager].
+++

### Vad är skillnaden mellan anslutningen [!DNL Facebook Custom Audiences] och tillägget [!DNL Facebook Pixel]?

+++Svar
[!DNL Facebook Custom Audiences]-anslutningen använder [!DNL Platform] identiteter när målgrupper skickas till [!DNL Facebook], medan [[!DNL Facebook Pixel] anslutningen](../destinations/catalog/advertising/facebook-pixel.md) använder den [!DNL Facebook]-pixel som är integrerad i en webbplats.

Dessa två integreringar kompletterar varandra, och ni kan använda båda för att få bättre täckning. Du kan till exempel använda tillägget [!DNL Facebook Pixel] för att söka efter webbplatsbesökare som inte har skapat något konto, medan [!DNL Facebook Custom Audiences] kan hjälpa dig att rikta in dig på befintliga kunder baserat på [!DNL Platform]-identiteter.
+++

### Stöder Adobe Experience Platform-integreringen med [!DNL Facebook Custom Audiences] diskvalificering av användare från en målgrupp när de inte längre är kvalificerade för det?**

+++Svar
Ja, integreringen stöder borttagning av användare från [!DNL Facebook Custom Audiences] när de inte längre är kvalificerade.
+++

### Hur ska jag hash-koda målgruppsdata innan jag skickar dem till [!DNL Facebook]?

+++Svar
[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas i klartext. Därför kan målgrupper som är aktiverade för [!DNL Facebook] inaktiveras för *hashed*-identifierare, som e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/facebook.md#id-matching-requirements).
+++

### Vilken typ av identiteter kan jag aktivera i [!DNL Facebook Custom Audiences]?

+++Svar
[!DNL Facebook Custom Audiences] har stöd för aktivering av följande identiteter: hash-kodade e-postmeddelanden, hashade telefonnummer, [!DNL GAID], [!DNL IDFA] och anpassade externa ID:n.
+++

### Kan jag skapa flera Facebook-mål i plattformsgränssnittet för separata Facebook-konton?

+++Svar
Ja. En Facebook-destination i Experience Platform är 1:1 till ett annonskonto i Facebook. Du kan skapa ett separat Facebook-mål för varje Facebook-annonskonto i ditt företag. Följ självstudiekursen [för målanslutning](/help/destinations/ui/connect-destination.md) och anslut till ett separat Facebook-konto för varje nytt Facebook-mål i plattformsgränssnittet. Det finns ingen gräns för hur många Facebook-annonskonton du kan ansluta till.
+++

## Google kundmatchning {#google-customer-match}

### När jag exporterar målgrupper till Google Customer Match, varför visas extra nummer i slutet av målgruppsnamnen i Google gränssnitt?

+++Svar
Google kräver att publiknamnen är unika. Siffrorna som du ser är [UNIX-tidsstämplar](https://www.unixtimestamp.com/) och de läggs till för att publiknamnen ska vara unika, om du har mappat samma målgrupp till flera Google-mål.
+++

## LinkedIn Matched Auditions {#linkedin}

### Behöver jag lägga till några appar eller pixlar i mitt [!DNL LinkedIn]-annonserarkonto?

+++Svar
Nej. Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.
+++

### Vad behöver jag göra innan jag kan aktivera målgrupper i [!DNL LinkedIn Matched Audiences]?

+++Svar
Innan du kan använda målet [!UICONTROL LinkedIn Matched Audience] måste du kontrollera att ditt [!DNL LinkedIn Campaign Manager]-konto har behörighetsnivån [!DNL Creative Manager] eller högre.

Mer information om hur du redigerar användarbehörigheter för [!DNL LinkedIn Campaign Manager] finns i [Lägg till, redigera och ta bort användarbehörigheter för Advertising-konton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.
+++

### Hur ska jag hash-koda målgruppsdata innan jag skickar dem till [!DNL LinkedIn]?

+++Svar
[!DNL LinkedIn] kräver att ingen personligt identifierbar information (PII) skickas i klartext. Därför kan målgrupper som är aktiverade för [!DNL LinkedIn] inaktiveras för *hashed*-identifierare, som e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/linkedin.md#id-matching-requirements).
+++

### Vilken typ av identiteter kan jag aktivera i [!DNL LinkedIn]?

+++Svar
[!DNL LinkedIn Matched Audiences] stöder aktivering av följande identiteter: hash-kodade e-postmeddelanden, [!DNL GAID] och [!DNL IDFA].

+++

## Personalisering på samma sida och nästa sida via Adobe Target och anpassade Personalization-destinationer {#same-next-page-personalization}

### Måste jag använda Experience Platform Web SDK för att skicka målgrupper och attribut till Adobe Target?

+++Svar
Nej, [Web SDK](../web-sdk/home.md) krävs inte för att aktivera målgrupper för [Adobe Target](catalog/personalization/adobe-target-connection.md).

Om [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) används i stället för Web SDK stöds endast nästa sessionspersonalisering.

För [anpassning av hela och nästa sida](ui/activate-edge-personalization-destinations.md) måste du antingen använda [Web SDK](../web-sdk/home.md) eller [Edge Network Server API](../server-api/overview.md). Mer implementeringsinformation finns i dokumentationen om att [aktivera målgrupper mot kantmål](ui/activate-edge-personalization-destinations.md).
+++

### Finns det någon gräns för hur många attribut jag kan skicka från Real-time Customer Data Platform till Adobe Target eller ett anpassat Personalization-mål?

+++Svar
Ja, personalisering på samma sida och nästa sida stöder maximalt 30 attribut per sandlåda när målgrupper aktiveras för Adobe Target eller anpassade Personalization-destinationer. Mer information om aktiveringsskydd finns i [skyddsdokumentationen](guardrails.md#edge-destinations-activation).
+++

### Vilka typer av attribut stöds för aktivering (t.ex. arrayer, kartor etc.)?

+++Svar
För närvarande stöds bara statiska attribut med ett värde, till exempel `person.name.firstName`. Matrisattribut stöds för närvarande inte.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### När jag har skapat en målgrupp i Experience Platform, hur lång tid tar det för den målgruppen att bli tillgänglig för kantsegmentering?

+++Svar
Målgruppsdefinitioner sprids till [Edge Network](../web-sdk/home.md) på upp till en timme. Men om en målgrupp aktiveras inom den första timmen kan vissa besökare som är kvalificerade för målgruppen missas.
+++

### Var kan jag se de aktiverade attributen i Adobe Target?

+++Svar
Attribut kommer att vara tillgängliga för användning i Target i erbjudanden från [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) och [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).
+++

### Kan jag skapa ett mål utan ett datastream och sedan lägga till ett datastream till samma mål vid en senare tidpunkt?

+++Svar
Detta stöds för närvarande inte via målgränssnittet. Om du behöver hjälp kan du kontakta din Adobe-representant.
+++

### Vad händer om jag tar bort ett Adobe Target-mål?

+++Svar
När du tar bort ett mål tas alla målgrupper och attribut som är mappade under målet bort från Adobe Target och de tas också bort från Edge Network.
+++

### Fungerar integreringen med Edge Network Server API?

+++Svar
Ja, Edge Network Server-API:t fungerar med det anpassade Personalization-målet. Eftersom profilattribut kan innehålla känsliga data krävs det att du använder API:t för Edge Network Server för datainsamling för att skydda dessa data. Dessutom måste alla API-anrop göras i en [autentiserad kontext](../server-api/authentication.md).
+++

### Jag kan bara ha en kopplingsregel som är aktiv i farten. Kan jag bygga målgrupper som använder en annan sammanslagningspolicy och ändå skicka dem till Adobe Target som direktuppspelade målgrupper?

+++Svar
Nej. Alla målgrupper som du vill aktivera för Adobe Target måste använda en [kopplingsprincip](../profile/merge-policies/ui-guide.md) som är aktiv.
+++

### Tillämpas etiketter och tvångsåtgärder (DULE) och godkännandeprinciper för dataanvändning?

+++Svar
Ja. [Datastyrnings- och sambandsprinciper](../data-governance/home.md) som skapas och associeras med de valda marknadsföringsåtgärderna styr aktiveringen av de valda attributen.
+++

### Är [!DNL Adobe Target] och [!DNL Custom Personalization] mål [!DNL HIPAA]-kompatibla?

+++Svar
[!DNL Adobe Target] är inte [!DNL HIPPA]-kompatibel med [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). Kunderna bör kontrollera med sina egna juridiska team vad gäller [!DNL HIPPA]-beredskap för anpassade optimeringskanaler innan de använder kantanpassning via [!DNL Adobe Target] eller [!DNL Custom Personalization]-destinationer.

För användningsfall där hantering av medgivandeprinciper måste tillämpas i stor skala måste kunderna köpa [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] funktioner säljs som en avancerad uppsättning funktioner och kan inte köpas separat.

Den här tjänsten innehåller kundhanterade nycklar och förhöjda tröskelvärden för hantering av kundens datalängd.

Destinationerna [!DNL Adobe Target] och [!DNL Custom Personalization] är integrerade med etiketterna för dataanvändning i [Experience Platform](../data-governance/labels/overview.md) och [efterlevnadstjänsten för profiler för samtycke](../data-governance/enforcement/overview.md). De här funktionerna är tillgängliga för alla kunder.




+++

