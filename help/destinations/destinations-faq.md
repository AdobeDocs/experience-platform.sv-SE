---
keywords: mål; frågor; vanliga frågor; frågor och svar; destinationer faq
title: Frågor och svar
description: Svar på de vanligaste frågorna om Adobe Experience Platform destinationer
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 2%

---

# Frågor och svar {#faq}

## Översikt {#overview}

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform destinationer. För frågor och felsökning relaterade till andra [!DNL Platform] tjänster, inklusive sådana som har påträffats i alla [!DNL Platform] API:er, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

## Vanliga frågor om destinationer {#general}

### Varför visas olika antal profiler i användargränssnittet i Experience Platform och i de exporterade CSV-filerna?

+++Svar Detta är ett normalt beteende på grund av hur Experience Platform utför segmentering.

Direktuppspelningssegmentering uppdaterar profilantalet för direktuppspelade målgrupper under hela dagen, medan batchsegmentering uppdaterar profilantalet för batchmålgrupper en gång var 24:e timme.

När målgruppens exportschema skiljer sig från segmenteringsschemat räknas profilen mellan användargränssnittet och det exporterade [!DNL CSV] filen kommer att vara annorlunda, särskilt när det gäller direktuppspelande målgrupper.

Se [Dokumentation för segmenteringstjänst](../segmentation/home.md) för mer information.
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

+++Svar Innan du kan skicka dina målgrupper till [!DNL Facebook]ska du kontrollera att du uppfyller följande krav:

* Dina [!DNL Facebook] användarkontot måste ha **[!DNL Manage campaigns]** behörighet aktiverad för annonskontot som du tänker använda.
* The **Adobe Experience Cloud** företagskonto måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Se [Lägg till partners i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i Facebook-dokumentationen.

  >[!IMPORTANT]
  >
  > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera **Hantera kampanjer** behörighet. Det krävs för [!DNL Adobe Experience Platform]-integreringen.
* Läs och signera [!DNL Facebook Custom Audiences] Användarvillkor. Gör det genom att gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].
+++

### Måste jag lägga till några appar eller pixlar i [!DNL Facebook] annonserarkonto?

+++Svarsnr Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.
+++

### Hur lång tid tar det för Facebook att bearbeta information från Adobe Experience Platform?

+++Svar från mars 2021, [!DNL Facebook Custom Audiences] behöver upp till en timme för att bearbeta information som tas emot från [!DNL Platform].
+++

### Kan jag använda [!DNL Facebook Custom Audiences] för målgruppsanpassning i andra [!DNL Facebook] appar, som [!DNL Instagram]?

+++Blanksteg Du kan använda [!DNL Facebook Custom Audiences] målgruppsanpassning för olika Facebook-program som stöds av [!DNL Facebook Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]och [!DNL Messenger]. Valet av den app som annonsörer vill köra kampanjer på anges på placeringsnivån i [!DNL Facebook Ads Manager].
+++

### Vad är skillnaden mellan [!DNL Facebook Custom Audiences] anslutning och [!DNL Facebook Pixel] tillägg?

+++Besvara [!DNL Facebook Custom Audiences] anslutningsanvändning [!DNL Platform] identiteter när målgrupper skickas till [!DNL Facebook], samtidigt som [[!DNL Facebook Pixel] anslutning](../destinations/catalog/advertising/facebook-pixel.md) använder [!DNL Facebook] pixlar som är integrerade på en webbplats.

Dessa två integreringar kompletterar varandra och ni kan använda båda för att få bättre målgruppstäckning. Du kan till exempel använda [!DNL Facebook Pixel] tillägg för sökning av besökare på webbplatser som inte har skapat något konto, medan [!DNL Facebook Custom Audiences] kan hjälpa er att inrikta er på befintliga kunder utifrån [!DNL Platform] identiteter.
+++

### Kan Adobe Experience Platform integreras med [!DNL Facebook Custom Audiences] ger du stöd för att hindra användare från att nå en viss publik när de inte längre är kvalificerade för det?**

+++Svar Ja, integreringen stöder borttagning av användare från [!DNL Facebook Custom Audiences] när de inte längre är kvalificerade.
+++

### Hur ska jag hash-koda målgruppsdata innan jag skickar dem till [!DNL Facebook]?

+++Svar
[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL Facebook] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/facebook.md#id-matching-requirements).
+++

### Vilken typ av identiteter kan jag aktivera i [!DNL Facebook Custom Audiences]?

+++Svar
[!DNL Facebook Custom Audiences] stöder aktivering av följande identiteter: hash-kodade e-postmeddelanden, hash-kodade telefonnummer, [!DNL GAID], [!DNL IDFA]och anpassade externa ID:n.
+++

### Kan jag skapa flera Facebook-mål i plattformsgränssnittet för separata Facebook-konton?

+++Besvara Ja. En Facebook-destination i Experience Platform är 1:1 till ett annonskonto i Facebook. Du kan skapa ett separat Facebook-mål för varje Facebook-annonskonto i ditt företag. Följ [självstudiekurs om målanslutning](/help/destinations/ui/connect-destination.md) och ansluta till ett separat Facebook-konto för varje nytt Facebook-mål i användargränssnittet för plattformen. Det finns ingen gräns för hur många Facebook-annonskonton du kan ansluta till.
+++

## Google kundmatchning {#google-customer-match}

### När jag exporterar målgrupper till Google Customer Match, varför visas extra nummer i slutet av målgruppsnamnen i Google gränssnitt?

+++Svar Google kräver att målgruppsnamnen är unika. Siffrorna du ser är [UNIX-tidsstämplar](https://www.unixtimestamp.com/) och de läggs till så att målgruppsnamnen förblir unika om du mappar samma målgrupp till flera Google-destinationer.
+++

## LinkedIn Matched Auditions {#linkedin}

### Måste jag lägga till några appar eller pixlar i [!DNL LinkedIn] annonserarkonto?

+++Svarsnr Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.
+++

### Vad behöver jag göra innan jag kan aktivera målgrupper i [!DNL LinkedIn Matched Audiences]?

+++Svar Innan du kan använda [!UICONTROL LinkedIn Matched Audience] mål, se till att [!DNL LinkedIn Campaign Manager] kontot har [!DNL Creative Manager] behörighetsnivå eller högre.

Så här redigerar du [!DNL LinkedIn Campaign Manager] användarbehörigheter, se [Lägg till, redigera och ta bort användarbehörigheter på annonskonton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.
+++

### Hur ska jag hash-koda målgruppsdata innan jag skickar dem till [!DNL LinkedIn]?

+++Svar
[!DNL LinkedIn] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL LinkedIn] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/linkedin.md#id-matching-requirements).
+++

### Vilken typ av identiteter kan jag aktivera i [!DNL LinkedIn]?

+++Svar
[!DNL LinkedIn Matched Audiences] stöder aktivering av följande identiteter: hash-kodade e-postmeddelanden, [!DNL GAID]och [!DNL IDFA].

+++

## Personalisering på samma sida och nästa sida via Adobe Target och anpassade anpassningsmål {#same-next-page-personalization}

### Måste jag använda Experience Platform Web SDK för att skicka målgrupper och attribut till Adobe Target?

+++svarsnr, [Web SDK](../edge/home.md) behöver inte aktivera målgrupper till [Adobe Target](catalog/personalization/adobe-target-connection.md).

Om [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) används i stället för Web SDK, men endast nästa sessionspersonalisering stöds.

För [personalisering på samma sida och nästa sida](ui/activate-edge-personalization-destinations.md) användningsfall måste du använda antingen [Web SDK](../edge/home.md) eller [API för Edge Network Server](../server-api/overview.md). Läs dokumentationen om [aktivera målgrupper mot kantmål](ui/activate-edge-personalization-destinations.md) om du vill ha mer information om implementeringen.
+++

### Finns det någon gräns för hur många attribut jag kan skicka från Real-time Customer Data Platform till Adobe Target eller ett anpassat anpassningsmål?

+++Svar Ja, personalisering på samma sida och nästa sida har stöd för högst 30 attribut per sandlåda, när målgrupper aktiveras till Adobe Target eller anpassade personaliseringsmål. Läs mer om aktiveringsskydd i [dokumentation för skyddsutkast](guardrails.md#edge-destinations-activation).
+++

### Vilka typer av attribut stöds för aktivering (t.ex. arrayer, kartor etc.)?

+++Svara För närvarande stöds endast statiska attribut med ett värde, till exempel `person.name.firstName`. Matrisattribut stöds för närvarande inte.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### När jag har skapat en målgrupp i Experience Platform, hur lång tid tar det för den målgruppen att bli tillgänglig för kantsegmentering?

+++Besvara målgruppsdefinitioner sprids till [Edge Network](../edge/home.md) på upp till en timme. Men om en målgrupp aktiveras inom den första timmen kan vissa besökare som är kvalificerade för målgruppen missas.
+++

### Var kan jag se de aktiverade attributen i Adobe Target?

+++svarsattribut kommer att vara tillgängliga för användning i Target i [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) och [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html) erbjudanden.
+++

### Kan jag skapa ett mål utan ett datastream och sedan lägga till ett datastream till samma mål vid en senare tidpunkt?

+++Svar Det här stöds för närvarande inte via målgränssnittet. Om du behöver hjälp kan du kontakta din Adobe-representant.
+++

### Vad händer om jag tar bort ett Adobe Target-mål?

+++Svar När du tar bort ett mål tas alla målgrupper och attribut som mappas under målet bort från Adobe Target och de tas även bort från Edge Network.
+++

### Fungerar integreringen med Edge Network Server API?

+++Besvara Ja, Edge Network Server API fungerar med anpassat anpassningsmål. Eftersom profilattribut kan innehålla känsliga data, kräver Custom Personalization-målet att du använder Edge Network Server API för datainsamling för att skydda dessa data. Dessutom måste alla API-anrop göras i en [autentiserad kontext](../server-api/authentication.md).
+++

### Jag kan bara ha en kopplingsregel som är aktiv i farten. Kan jag bygga målgrupper som använder en annan sammanslagningspolicy och ändå skicka dem till Adobe Target som direktuppspelade målgrupper?

+++Svarsnr Alla målgrupper som du vill aktivera för Adobe Target måste använda en [sammanfogningsprincip](../profile/merge-policies/ui-guide.md).
+++

### Tillämpas etiketter och tvångsåtgärder (DULE) och godkännandeprinciper för dataanvändning?

+++Besvara Ja. The [Datastyrnings- och godkännandeprinciper](../data-governance/home.md) som har skapats och associerats med de valda marknadsföringsåtgärderna styr aktiveringen av de valda attributen.
+++

### Är [!DNL Adobe Target] och [!DNL Custom Personalization] mål [!DNL HIPAA]-kompatibel?

+++Svar
[!DNL Adobe Target] är inte [!DNL HIPPA]-kompatibel med [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). Kunderna bör höra med sina egna jurister om [!DNL HIPPA]-beredskap för anpassade optimeringskanaler innan ni använder kantanpassning via [!DNL Adobe Target] eller [!DNL Custom Personalization] destinationer.

I de fall där samtyckespolicyhantering måste tillämpas i stor skala måste kunderna köpa [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] funktioner säljs som en avancerad uppsättning funktioner och kan inte köpas separat.

Den här tjänsten innehåller kundhanterade nycklar och förhöjda tröskelvärden för hantering av kundens datalängd.

The [!DNL Adobe Target] och [!DNL Custom Personalization] destinationerna är integrerade med [Etiketter för dataanvändning i Experience Platform](../data-governance/labels/overview.md) och [Tvingande bekräftelsetjänst](../data-governance/enforcement/overview.md). De här funktionerna är tillgängliga för alla kunder.




+++

