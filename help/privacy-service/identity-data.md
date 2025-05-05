---
keywords: Experience Platform;hem;populära ämnen;ECID;ecid
solution: Experience Platform
title: Identitetsdata för sekretessförfrågningar
description: Det här dokumentet innehåller allmän vägledning om hur du konfigurerar dataåtgärder och använder Adobe-tekniker för att effektivt hämta lämplig identitetsinformation för kundsekretessförfrågningar.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Identitetsdata för sekretessförfrågningar

För att Adobe Experience Platform [!DNL Privacy Service] ska kunna bearbeta kundförfrågningar för sina privata data (inklusive begäran om åtkomst, borttagning eller avanmälan) måste den förses med unika identifierare som länkar en viss kund till deras lagrade privata data i program som är aktiverade i Adobe Experience Cloud. [!DNL Privacy Service] använder sedan dessa identifierare för att samla in alla data som lagras under kundens identitet inom [!DNL Experience Cloud] och bearbeta dem enligt kundens begäran.

Det här dokumentet innehåller allmän vägledning om hur du konfigurerar dataåtgärder och använder Adobe-tekniker för att effektivt hämta lämplig identitetsinformation för kundsekretessförfrågningar.

## Identiteter och namnutrymmen

När en kund kan interagera med ert varumärke via flera olika kanaler kan det vara svårt att förena de olika identifierare som registreras från dessa många interaktioner. Detta kan i sin tur göra det svårt att avgöra vilka data som tillhör en viss person i dina [!DNL Experience Cloud]-program.

När du till exempel hanterar kunddatabegäranden i [!DNL Privacy Service] kan en identitet representera ett cookie-värde som angetts under en Adobe-kontrollerad domän, ett cookie-värde under en tredjepartsdomän och som delas med Adobe, eller en anpassad identifierare som du uttryckligen definierar inom din organisation.

Det krävs därför att varje identitet som skickas till [!DNL Privacy Service] åtföljs av ett namnutrymme som tillhandahåller kontext genom att identitetsvärdet kopplas till ursprungssystemet. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Adobe Experience Platform identitetstjänst lagrar globalt definierade och användardefinierade identitetsnamnutrymmen. Mer information om namnutrymmen finns i [översikten över namnutrymmet identity](../identity-service/features/namespaces.md). En lista över standardnamnutrymmen och namnutrymmeskvalificerare som ofta används i [!DNL Privacy Service] finns i avsnittet [ appendix ](api/appendix.md) i API-handboken.

## ECID- och anmälningstjänst

Adobe Experience Cloud [!DNL Identity Service] fungerar som ett gemensamt identifieringsramverk för [!DNL Experience Cloud] och tilldelar varje besökare ett unikt, beständigt ID. [!DNL Experience Cloud]-ID:t (ECID) spårar en kunds aktivitet med hjälp av en cookie från en annan leverantör, kan unikt identifiera en enhet i flera program och gör att du kan identifiera samma besökare och deras data i olika [!DNL Experience Cloud] -program. Mer information finns i [Översikt över identitetstjänsten i Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=sv-SE).

Med anmälningstjänsten, ett tillägg till [!DNL Experience Cloud Identity Service], kan du konfigurera protokoll för ditt program så att besökarna kan avgöra om du kan ange en cookie på besökarens enhet eller webbläsare. Mer detaljerad information om Opt-in-tjänsten, inklusive hur du konfigurerar tjänsten för ditt program, finns i [dokumentationen för Opt-in-tjänsten](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=sv-SE).

När webbplatsbesökarna har tilldelats ECID:n kan du använda Adobe [!DNL Privacy JavaScript Library] för att hämta dessa ID:n för användning i sekretessförfrågningar, vilket beskrivs i nästa avsnitt.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library] innehåller flera funktioner som gör att du kan hämta och ta bort kundidentiteter som är lagrade i webbläsaren. Biblioteket kan konfigureras för att hämta identitetsinformation från flera olika Adobe-program, inklusive ECID. Genom att använda återanrop eller löften kan du programmässigt hantera hämtade ID:n och skicka dem till [!DNL Privacy Service] API:t.

Mer information om [!DNL Privacy JS Library], inklusive kodexempel för flera vanliga användningsområden, finns i [Översikt över JS-bibliotek för sekretess](js-library.md).

## Nästa steg

I det här dokumentet finns en kort översikt över de centrala begrepp som används för att hämta kundidentitetsdata för användning i sekretessförfrågningar. Vi rekommenderar att du läser dokumentationslänkarna i varje avsnitt för mer detaljerad information om dessa begrepp och tjänster. Anvisningar om hur du skickar hämtade ID:n till [!DNL Privacy Service] för att skapa begäranden om åtkomst, borttagning eller avanmälan finns i [Privacy Services-API-handboken](api/overview.md).
