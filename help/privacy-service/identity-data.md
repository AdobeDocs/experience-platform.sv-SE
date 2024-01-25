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

För Adobe Experience Platform [!DNL Privacy Service] för att kunna behandla kundförfrågningar om privata data (inklusive begäran om åtkomst, radering eller avanmälan) måste de förses med unika identifierare som länkar en viss kund till deras lagrade privata data i era Adobe Experience Cloud-aktiverade program. [!DNL Privacy Service] använder sedan dessa identifierare för att samla in alla data som lagras under kundens identitet inom [!DNL Experience Cloud]och bearbeta det på kundens begäran.

Det här dokumentet innehåller allmän vägledning om hur du konfigurerar dataåtgärder och använder Adobe-tekniker för att effektivt hämta lämplig identitetsinformation för kundsekretessförfrågningar.

## Identiteter och namnutrymmen

När en kund kan interagera med ert varumärke via flera olika kanaler kan det vara svårt att förena de olika identifierare som registreras från dessa många interaktioner. Detta kan i sin tur göra det svårt att avgöra vilka data som tillhör en viss person i [!DNL Experience Cloud] program.

När du till exempel hanterar kunddataförfrågningar i [!DNL Privacy Service]kan en identitet representera ett cookie-värde som anges under en Adobe-kontrollerad domän, ett cookie-värde under en tredjepartsdomän och delas med Adobe, eller en anpassad identifierare som du uttryckligen definierar inom din organisation.

Varje identitet som skickas till [!DNL Privacy Service] åtföljs av ett namnutrymme som innehåller ett sammanhang där identitetsvärdet kopplas till ursprungssystemet. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-id (&quot;TNTID&quot;).

Adobe Experience Platform identitetstjänst lagrar globalt definierade och användardefinierade identitetsnamnutrymmen. Mer information om namnutrymmen finns i [Översikt över namnutrymmet identity](../identity-service/features/namespaces.md). En lista med standardnamnutrymmen och namnutrymmeskvalificerare som ofta används i [!DNL Privacy Service], se [appendix-avsnitt](api/appendix.md) i API-guiden.

## ECID- och anmälningstjänst

Adobe Experience Cloud [!DNL Identity Service] fungerar som ett gemensamt identifieringsramverk för [!DNL Experience Cloud]och tilldelar varje besökare ett unikt, beständigt ID. The [!DNL Experience Cloud] ID (ECID) spårar en kunds aktivitet med hjälp av en cookie från en annan leverantör, kan unikt identifiera en enhet i flera program och gör att du kan identifiera samma besökare och deras data i olika [!DNL Experience Cloud] program. Se [Översikt över identitetstjänsten i Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) för mer information.

Opt-in Service, ett tillägg till [!DNL Experience Cloud Identity Service]Med kan du konfigurera protokoll för programmet så att besökarna kan avgöra om du kan ställa in en cookie på besökarens enhet eller webbläsare. Mer detaljerad information om Opt-in Service, inklusive hur du konfigurerar tjänsten för ditt program, finns i [Dokumentation för anmälningstjänst](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html).

När besökarna på webbplatsen har tilldelats ECID:n kan du använda Adobe [!DNL Privacy JavaScript Library] för att hämta dessa ID:n för användning i sekretessförfrågningar, vilket beskrivs i nästa avsnitt.

## [!DNL Privacy JS Library]

The [!DNL Adobe Privacy JavaScript Library] innehåller flera funktioner som gör att du kan hämta och ta bort kundidentiteter som är lagrade i webbläsaren. Biblioteket kan konfigureras för att hämta identitetsinformation från flera olika Adobe-program, inklusive ECID. Genom att använda återanrop eller löften kan du programmässigt hantera hämtade ID:n och skicka dem till [!DNL Privacy Service] API.

Mer information om [!DNL Privacy JS Library], inklusive kodexempel för flera vanliga användningsområden, se [Översikt över JS-bibliotek för sekretess](js-library.md).

## Nästa steg

I det här dokumentet finns en kort översikt över de centrala begrepp som används för att hämta kundidentitetsdata för användning i sekretessförfrågningar. Vi rekommenderar att du läser dokumentationslänkarna i varje avsnitt för mer detaljerad information om dessa begrepp och tjänster. För steg om hur du skickar hämtade ID:n till [!DNL Privacy Service] för att skapa begäranden om åtkomst, borttagning eller avanmälan finns i [API-guide för Privacy Service](api/overview.md).
