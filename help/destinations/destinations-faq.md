---
keywords: Destinationer. frågor, Frågor och svar. faq, mål faq
title: Frågor och svar
description: Svar på de vanligaste frågorna om Adobe Experience Platform destinationer
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '1392'
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

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Vad behöver jag göra innan jag kan aktivera målgrupper i [!DNL Facebook Custom Audiences]?

+++Svar Innan du kan skicka dina målgrupper till [!DNL Facebook]måste du uppfylla följande krav:

* Dina [!DNL Facebook] användarkontot måste ha **[!DNL Manage campaigns]** behörighet aktiverad för annonskontot som du tänker använda.
* The **Adobe Experience Cloud** företagskonto måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Se [Lägg till partners i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i Facebook-dokumentationen.
  >[!IMPORTANT]
  >
  > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera **Hantera kampanjer** behörighet. Det krävs för [!DNL Adobe Experience Platform]-integreringen.
* Läs och signera [!DNL Facebook Custom Audiences] Användarvillkor. Gör det genom att gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].
+++

### Måste jag lägga till några appar eller pixlar i [!DNL Facebook] annonserarkonto?

+++Svarsnummer Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.
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
[!DNL Facebook Custom Audiences] har stöd för aktivering av följande identiteter: hash-kodade e-postmeddelanden, hashade telefonnummer, [!DNL GAID], [!DNL IDFA]och anpassade externa ID:n.
+++

### Kan jag skapa flera Facebook-mål i plattformsgränssnittet för separata Facebook-konton?

+++Besvara Ja. En Facebook-destination i Experience Platform är 1:1 till ett annonskonto i Facebook. Du kan skapa ett separat Facebook-mål för varje Facebook-annonskonto i ditt företag. Följ [självstudiekurs om målanslutning](/help/destinations/ui/connect-destination.md) och ansluta till ett separat Facebook-konto för varje nytt Facebook-mål i användargränssnittet för plattformen. Det finns ingen gräns för hur många Facebook-annonskonton du kan ansluta till.
+++

## Google kundmatchning {#google-customer-match}

### När jag exporterar målgrupper till Google Customer Match, varför visas extra nummer i slutet av målgruppsnamnen i Google gränssnitt?

+++Svar Google kräver att målgruppsnamnen är unika. Siffrorna du ser är [UNIX-tidsstämplar](https://www.unixtimestamp.com/) och de läggs till så att målgruppsnamnen förblir unika om du mappar samma målgrupp till flera Google-destinationer.
+++

## linkedIn Matched Auditions {#linkedin}

### Måste jag lägga till några appar eller pixlar i [!DNL LinkedIn] annonserarkonto?

+++Svarsnummer Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.
+++

### Vad behöver jag göra innan jag kan aktivera målgrupper i [!DNL LinkedIn Matched Audiences]?

+++Svar Innan du kan använda [!UICONTROL LinkedIn Matched Audience] mål, se till att [!DNL LinkedIn Campaign Manager] kontot har [!DNL Creative Manager] behörighet eller högre.

Så här redigerar du [!DNL LinkedIn Campaign Manager] användarbehörigheter, se [Lägg till, redigera och ta bort användarbehörigheter på annonskonton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.
+++

### Hur ska jag hash-koda målgruppsdata innan jag skickar dem till [!DNL LinkedIn]?

+++Svar
[!DNL LinkedIn] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL LinkedIn] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/linkedin.md#id-matching-requirements).
+++

### Vilken typ av identiteter kan jag aktivera i [!DNL LinkedIn]?

+++Svar
[!DNL LinkedIn Matched Audiences] har stöd för aktivering av följande identiteter: hash-kodade e-postmeddelanden, [!DNL GAID]och [!DNL IDFA].
+++

## Personalisering på samma sida och nästa sida via Adobe Target och anpassade anpassningsmål {#same-next-page-personalization}

### Måste jag använda Experience Platform Web SDK för att skicka målgrupper och attribut till Adobe Target?

+++svarsnr, [Web SDK](../edge/home.md) behöver inte aktivera målgrupper till [Adobe Target](catalog/personalization/adobe-target-connection.md).

Om [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=en) används i stället för Web SDK, men endast nästa sessionspersonalisering stöds.

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

+++Besvara målgruppsdefinitioner sprids till [Edge Network](../edge/home.md) på upp till en timme. Men om en målgrupp aktiveras inom den första timmen kan vissa besökare som skulle ha kvalificerat sig för målgruppen missas.
+++

### Var kan jag se de aktiverade attributen i Adobe Target?

+++svarsattribut kommer att vara tillgängliga för användning i Target i [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) och [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=en) erbjudanden.
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

+++Svarsnummer Alla målgrupper som du vill aktivera för Adobe Target måste använda en [sammanfogningsprincip](../profile/merge-policies/ui-guide.md).
+++

### Tillämpas etiketter och tvångsåtgärder (DULE) och godkännandeprinciper för dataanvändning?

+++Besvara Ja. The [Datastyrnings- och godkännandeprinciper](../data-governance/home.md) som har skapats och associerats med de valda marknadsföringsåtgärderna styr aktiveringen av de valda attributen.
+++
