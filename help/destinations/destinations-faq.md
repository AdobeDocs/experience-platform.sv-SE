---
keywords: Destinationer. frågor, Frågor och svar. faq, mål faq
title: Frågor och svar
seo-title: Frequently asked questions
description: Svar på de vanligaste frågorna om Adobe Experience Platform destinationer
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 8f9a601a833149c83d465f68d16ca362ed730b8a
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 4%

---

# Frågor och svar {#faq}

## Översikt {#overview}

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform destinationer. För frågor och felsökning relaterade till andra [!DNL Platform] tjänster, inklusive sådana som har påträffats i alla [!DNL Platform] API:er, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

## Vanliga frågor om destinationer {#general}

**Varför visas olika antal profiler i användargränssnittet i Experience Platform och i de exporterade CSV-filerna?**

Detta är ett normalt beteende på grund av hur Experience Platform utför segmentering.

Direktuppspelningssegmentering uppdaterar profilantalet för direktuppspelningssegment under hela dagen, medan batchsegmentering uppdaterar profilantalet för batchsegment en gång var 24:e timme.

När segmentets exportschema skiljer sig från segmenteringsschemat, räknas profilen mellan användargränssnittet och det exporterade [!DNL CSV] filen kommer att vara annorlunda, särskilt när det gäller direktuppspelningssegment.

Se [Dokumentation för segmenteringstjänst](../segmentation/home.md) för mer information.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Vad behöver jag göra innan jag kan aktivera målgrupper i [!DNL Facebook Custom Audiences]?**

Innan du kan skicka målgruppssegment till [!DNL Facebook]måste du uppfylla följande krav:

* Dina [!DNL Facebook] användarkontot måste ha **[!DNL Manage campaigns]** behörighet aktiverad för annonskontot som du tänker använda.
* The **Adobe Experience Cloud** företagskonto måste läggas till som annonspartner i [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Se [Lägg till partners i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i Facebook-dokumentationen.
   >[!IMPORTANT]
   >
   > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera **Hantera kampanjer** behörighet. Det krävs för [!DNL Adobe Experience Platform]-integreringen.
* Läs och signera [!DNL Facebook Custom Audiences] Användarvillkor. Gör det genom att gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].

**Måste jag lägga till några appar eller pixlar i [!DNL Facebook] annonserarkonto?**

Nej. Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.

**Hur lång tid tar det för Facebook att bearbeta information från Adobe Experience Platform?**

Från om med mars 2021 [!DNL Facebook Custom Audiences] behöver upp till en timme för att bearbeta information som tas emot från [!DNL Platform].

**Kan jag använda [!DNL Facebook Custom Audiences] för målgruppsanpassning i andra [!DNL Facebook] appar, som [!DNL Instagram]?**

Du kan använda [!DNL Facebook Custom Audiences] målgruppsanpassning för olika Facebook-program som stöds av [!DNL Facebook Custom Audiences], inklusive [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]och [!DNL Messenger]. Valet av den app som annonsörer vill köra kampanjer på anges på placeringsnivån i [!DNL Facebook Ads Manager].

**Vad är skillnaden mellan [!DNL Facebook Custom Audiences] anslutning och [!DNL Facebook Pixel] tillägg?**

The [!DNL Facebook Custom Audiences] anslutningsanvändning [!DNL Platform] identiteter när målgrupper skickas till [!DNL Facebook], samtidigt som [[!DNL Facebook Pixel] anslutning](../destinations/catalog/advertising/facebook-pixel.md) använder [!DNL Facebook] pixlar som är integrerade på en webbplats.

Dessa två integreringar kompletterar varandra och ni kan använda båda för att få bättre målgruppstäckning. Du kan till exempel använda [!DNL Facebook Pixel] tillägg för sökning av besökare på webbplatser som inte har skapat något konto, medan [!DNL Facebook Custom Audiences] kan hjälpa er att inrikta er på befintliga kunder utifrån [!DNL Platform] identiteter.

**Kan Adobe Experience Platform integreras med [!DNL Facebook Custom Audiences] ger du stöd för att hindra användare från att nå en viss publik när de inte längre är kvalificerade för det?**

Ja, integreringen stöder borttagning av användare från [!DNL Facebook Custom Audiences] när de inte längre är kvalificerade.

**Hur ska jag hash-koda målgruppsdata innan jag skickar dem till [!DNL Facebook]?**

[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL Facebook] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/facebook.md#id-matching-requirements).

**Vilken typ av identiteter kan jag aktivera i [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] har stöd för aktivering av följande identiteter: hash-kodade e-postmeddelanden, hashade telefonnummer, [!DNL GAID], [!DNL IDFA]och anpassade externa ID:n.

**Kan jag skapa flera Facebook-mål i plattformsgränssnittet för separata Facebook-konton?**

En Facebook-destination i Experience Platform är 1:1 till ett annonskonto i Facebook. Du kan skapa ett separat Facebook-mål för varje Facebook-annonskonto i ditt företag. Följ [självstudiekurs om målanslutning](/help/destinations/ui/connect-destination.md) och ansluta till ett separat Facebook-konto för varje nytt Facebook-mål i användargränssnittet för plattformen.

## linkedIn Matched Auditions {#linkedin}

**Måste jag lägga till några appar eller pixlar i [!DNL LinkedIn] annonserarkonto?**

Nej. Eftersom detta inte är en pixelbaserad integrering behöver du inte lägga till några pixlar i annonskontot.

**Vad behöver jag göra innan jag kan aktivera målgrupper i [!DNL LinkedIn Matched Audiences]?**

Innan du kan använda [!UICONTROL LinkedIn Matched Audience] mål, se till att [!DNL LinkedIn Campaign Manager] kontot har [!DNL Creative Manager] behörighet eller högre.

Så här redigerar du [!DNL LinkedIn Campaign Manager] användarbehörigheter, se [Lägg till, redigera och ta bort användarbehörigheter på annonskonton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.

**Hur ska jag hash-koda målgruppsdata innan jag skickar dem till [!DNL LinkedIn]?**

[!DNL LinkedIn] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför aktiverades målgrupperna [!DNL LinkedIn] kan vara avstängd *hash* identifierare, till exempel e-postadresser eller telefonnummer.

Detaljerade förklaringar av kraven för ID-matchning finns i [Krav för ID-matchning](catalog/social/linkedin.md#id-matching-requirements).

**Vilken typ av identiteter kan jag aktivera i [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] har stöd för aktivering av följande identiteter: hash-kodade e-postmeddelanden, [!DNL GAID]och [!DNL IDFA].
