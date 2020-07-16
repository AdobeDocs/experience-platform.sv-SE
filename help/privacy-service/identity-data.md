---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identitetsdata för sekretessförfrågningar
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---


# Identitetsdata för sekretessförfrågningar

För att Adobe Experience Platform ska kunna bearbeta kundförfrågningar om sina privata data (inklusive begäran om åtkomst, radering eller avanmälan) måste de förses med unika identifierare som länkar en viss kund till deras lagrade privata data i Adobe Experience Cloud-aktiverade program. [!DNL Privacy Service] [!DNL Privacy Service] använder sedan dessa identifierare för att samla in alla data som lagras under kundens identitet inom [!DNL Experience Cloud]och bearbeta dem efter kundens begäran.

Det här dokumentet innehåller allmän vägledning om hur du konfigurerar dataåtgärder och använder Adobes tekniker för att effektivt hämta lämplig identitetsinformation för kundsekretessförfrågningar.

## Identiteter och namnutrymmen

När en kund kan interagera med ert varumärke via flera olika kanaler kan det vara svårt att kombinera de olika identifierare som registreras från dessa många interaktioner. Detta kan i sin tur göra det svårt att avgöra vilka data som tillhör en viss person i dina [!DNL Experience Cloud] program.

När du till exempel hanterar kunddataförfrågningar i kan en identitet representera en cookie-värdeuppsättning under en Adobe-kontrollerad domän, en cookie-värde under en tredjepartsdomän och som delas med Adobe, eller en anpassad identifierare som du uttryckligen definierar inom din IMS-organisation. [!DNL Privacy Service]

Det krävs därför att varje identitet som skickas till [!DNL Privacy Service] åtföljs av ett **namnutrymme** som innehåller ett sammanhang där identitetsvärdet kopplas till ursprungssystemet. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;E-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-id (&quot;AdCloud&quot;) eller ett Adobe Target-ID (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service lagrar globalt definierade och användardefinierade identitetsnamnutrymmen. Mer information om namnutrymmen finns i översikten över [namnutrymmet](../identity-service/namespaces.md). En lista med standardnamnutrymmen och namnutrymmeskvalificerare som ofta används i [!DNL Privacy Service]finns i [bilagan](api/appendix.md) i utvecklarhandboken.

## ECID och anmälningstjänst

Adobe Experience Cloud [!DNL Identity Service] är ett gemensamt identifieringsramverk för [!DNL Experience Cloud]och tilldelar varje besökare ett unikt, beständigt ID. Med [!DNL Experience Cloud] ID:t (ECID) kan du spåra en kunds aktivitet med hjälp av en cookie från en annan leverantör, identifiera en enhet i flera program och identifiera samma besökare och deras data i olika [!DNL Experience Cloud] program. Mer information finns i översikten [över](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) Experience Cloud Identity Service.

Med Opt-in Service, ett tillägg till [!DNL Experience Cloud Identity Service], kan du konfigurera protokoll för programmet så att besökarna kan avgöra om du kan ange en cookie på besökarens enhet eller webbläsare. Mer detaljerad information om Opt-in Service, inklusive hur du konfigurerar tjänsten för ditt program, finns i dokumentationen för [Opt-in Service](https://docs.adobe.com/content/help/sv-SE/id-service/using/implementation/opt-in-service/optin-overview.html).

När besökarna på webbplatsen har tilldelats ECID:n kan du använda Adobe [!DNL Privacy JavaScript Library] för att hämta dessa ID:n för användning i sekretessförfrågningar, vilket beskrivs i nästa avsnitt.

## [!DNL Privacy JS Library]

Här [!DNL Adobe Privacy JavaScript Library] finns flera funktioner som gör att du kan hämta och ta bort kundidentiteter som är lagrade i webbläsaren. Biblioteket kan konfigureras för att hämta identitetsinformation från flera Adobe-program, inklusive ECID. Genom att använda återanrop eller löften kan du programmässigt hantera hämtade ID:n och skicka dem till [!DNL Privacy Service] API:t.

Mer information om [!DNL Privacy JS Library], inklusive kodexempel för flera vanliga användningsområden finns i översikten över JS-biblioteket för [sekretess](js-library.md).

## Nästa steg

I det här dokumentet finns en kort översikt över de centrala begrepp som används för att hämta kundidentitetsdata för användning i sekretessförfrågningar. Vi rekommenderar att du läser dokumentationslänkarna i varje avsnitt för mer detaljerad information om dessa begrepp och tjänster. Anvisningar om hur du skickar hämtade ID:n [!DNL Privacy Service] för att skapa begäranden om åtkomst, borttagning eller avanmälan finns i [utvecklarhandboken](api/getting-started.md)för Privacy Service.