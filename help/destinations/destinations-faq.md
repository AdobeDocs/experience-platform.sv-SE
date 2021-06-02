---
keywords: Destinationer. frågor, Frågor och svar. faq, mål faq
title: Frågor och svar
seo-title: Frågor och svar
description: Svar på de vanligaste frågorna om Adobe Experience Platform destinationer
seo-description: Svar på de vanligaste frågorna om Adobe Experience Platform destinationer
source-git-commit: a01b53758f4ad42272c39f71a08021d30900e7af
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 5%

---


# Frågor och svar {#faq}

## Översikt {#overview}

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform destinationer. För frågor och felsökning som rör andra [!DNL Platform]-tjänster, inklusive de som har påträffats i alla [!DNL Platform] API:er, se [felsökningsguiden för Experience Platform](../landing/troubleshooting.md).

## Vanliga frågor om destinationer {#general}

**Varför visas olika antal profiler i användargränssnittet i Experience Platform och i de exporterade CSV-filerna?**

Detta är ett normalt beteende på grund av hur Experience Platform utför segmentering.

Direktuppspelningssegmentering uppdaterar profilantalet för direktuppspelningssegment under hela dagen, medan batchsegmentering uppdaterar profilantalet för batchsegment en gång var 24:e timme.

När segmentets exportschema skiljer sig från segmenteringsschemat kommer antalet profiler mellan användargränssnittet och den exporterade [!DNL CSV]-filen att vara olika, särskilt när det gäller direktuppspelningssegment.

Mer information finns i [dokumentationen för segmenteringstjänsten](../segmentation/home.md).

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Vad behöver jag göra innan jag kan aktivera målgrupper i  [!DNL Facebook Custom Audiences]?**

Innan du kan skicka målgruppssegment till [!DNL Facebook] måste du kontrollera att du uppfyller följande krav:

* Ditt [!DNL Facebook]-användarkonto måste ha behörigheten **[!DNL Manage campaigns]** aktiverad för det annonskonto som du tänker använda.
* Företagskontot **Adobe Experience Cloud** måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Mer information finns i [Lägg till partner i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i Facebook-dokumentationen.
   >[!IMPORTANT]
   >
   > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera behörigheten **Hantera kampanjer**. Det krävs för [!DNL Adobe Experience Platform]-integreringen.
* Läs och signera [!DNL Facebook Custom Audiences] användarvillkoren. Gör det genom att gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].

**Behöver jag lägga till några appar eller pixlar i mitt  [!DNL Facebook] annonserarkonto?**

Nej. Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.

**Hur lång tid tar det för Facebook att bearbeta information från Adobe Experience Platform?**

Från om med mars 2021 behöver [!DNL Facebook Custom Audiences] upp till en timme på sig att bearbeta information som tagits emot från [!DNL Platform].

**Kan jag använda  [!DNL Facebook Custom Audiences] för målgruppsanpassning i andra  [!DNL Facebook] appar, som  [!DNL Instagram]?**

Du kan använda målet [!DNL Facebook Custom Audiences] för målgrupper i alla Facebook-program som stöds av [!DNL Facebook Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] och [!DNL Messenger]. Valet av den app som annonsörer vill köra kampanjer på anges på placeringsnivån i [!DNL Facebook Ads Manager].

**Vad är skillnaden mellan  [!DNL Facebook Custom Audiences] anslutningen och  [!DNL Facebook Pixel] tillägget?**

[!DNL Facebook Custom Audiences]-anslutningen använder [!DNL Platform]-identiteter när målgrupper skickas till [!DNL Facebook], medan [[!DNL Facebook Pixel] anslutningen](../destinations/catalog/advertising/facebook-pixel.md) använder pixeln [!DNL Facebook] som är integrerad i en webbplats.

Dessa två integreringar kompletterar varandra och ni kan använda båda för att få bättre målgruppstäckning. Du kan till exempel använda tillägget [!DNL Facebook Pixel] för att söka efter webbplatsbesökare som inte har skapat något konto, medan [!DNL Facebook Custom Audiences] kan hjälpa dig att rikta in dig på befintliga kunder baserat på [!DNL Platform]-identiteter.

**Är Adobe Experience Platform-integreringen med  [!DNL Facebook Custom Audiences] stöd för att hindra användare från att nå en viss målgrupp när de inte längre är berättigade till det?**

Ja, integreringen stöder borttagning av användare från [!DNL Facebook Custom Audiences] när de inte längre är kvalificerade.

**Hur ska jag hash-koda målgruppsdata innan jag skickar dem till  [!DNL Facebook]?**

[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför kan målgrupper som är aktiverade för [!DNL Facebook] vara avstängda från *hash*-identifierare, till exempel e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/facebook.md#id-matching-requirements).

**Vilken sorts identiteter kan jag aktivera i  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] har stöd för aktivering av följande identiteter: hash-kodade e-postmeddelanden, hashade telefonnummer  [!DNL GAID]och  [!DNL IDFA]anpassade externa ID:n.

## linkedIn Matched Auditions {#linkedin}

**Behöver jag lägga till några appar eller pixlar i mitt  [!DNL LinkedIn] annonserarkonto?**

Nej. Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.

**Vad behöver jag göra innan jag kan aktivera målgrupper i  [!DNL LinkedIn Matched Audiences]?**

Innan du kan använda målet [!UICONTROL LinkedIn Matched Audience] måste du kontrollera att ditt [!DNL LinkedIn Campaign Manager]-konto har behörighetsnivån [!DNL Creative Manager] eller högre.

Mer information om hur du redigerar dina [!DNL LinkedIn Campaign Manager]-användarbehörigheter finns i [Lägg till, redigera och ta bort användarbehörigheter för annonskonton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.

**Hur ska jag hash-koda målgruppsdata innan jag skickar dem till  [!DNL LinkedIn]?**

[!DNL LinkedIn] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför kan målgrupper som är aktiverade för [!DNL LinkedIn] vara avstängda från *hash*-identifierare, till exempel e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/linkedin.md#id-matching-requirements).

**Vilken sorts identiteter kan jag aktivera i  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] har stöd för aktivering av följande identiteter: hash emails,  [!DNL GAID]och  [!DNL IDFA].
