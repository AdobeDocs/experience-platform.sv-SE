---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identitetsdata för sekretessförfrågningar
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Identitetsdata för sekretessförfrågningar

För att Adobe Experience Platform Privacy Service ska kunna behandla kundförfrågningar för sina privata data (inklusive förfrågningar om åtkomst, radering eller avanmälan) måste den förses med unika identifierare som länkar en viss kund till deras lagrade privata data i era Adobe Experience Cloud-aktiverade program. Integritetstjänsten använder sedan dessa identifierare för att samla in alla data som lagras under kundens identitet i Experience Cloud och bearbeta dem på kundens begäran.

Det här dokumentet innehåller allmän vägledning om hur du konfigurerar dataåtgärder och använder Adobes tekniker för att effektivt hämta lämplig identitetsinformation för kundsekretessförfrågningar.

## Identiteter och namnutrymmen

När en kund kan interagera med ert varumärke via flera olika kanaler kan det vara svårt att kombinera de olika identifierare som registreras från dessa många interaktioner. Detta kan i sin tur göra det svårt att avgöra vilka data som tillhör en viss person i dina Experience Cloud-program.

När du till exempel hanterar kunddataförfrågningar i Integritetstjänst kan en identitet representera ett cookie-värde som angetts under en Adobe-kontrollerad domän, ett cookie-värde under en tredjepartsdomän och som delas med Adobe, eller en anpassad identifierare som du uttryckligen definierar inom din IMS-organisation.

Det krävs därför att varje identitet som skickas till integritetstjänsten åtföljs av ett **namnutrymme** som innehåller ett sammanhang där identitetsvärdet kopplas till ursprungssystemet. Ett namnutrymme kan representera ett allmänt koncept, t.ex. en e-postadress (&quot;e-post&quot;) eller associera identiteten med ett visst program, t.ex. ett Adobe Advertising Cloud-ID (&quot;AdCloud&quot;) eller ett Adobe Target-ID (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service lagrar globalt definierade och användardefinierade identitetsnamnutrymmen. Mer information om namnutrymmen finns i översikten över [namnutrymmet](../identity-service/namespaces.md). En lista över standardnamnutrymmen och namnutrymmeskvalificerare som ofta används i sekretesssystemet finns i [bilagan](api/appendix.md) i utvecklarhandboken.

## ECID och anmälningstjänst

Adobe Experience Cloud Identity Service fungerar som ett gemensamt identifieringsramverk för Experience Cloud och tilldelar varje besökare ett unikt, beständigt ID. Experience Cloud ID (ECID) spårar en kunds aktivitet med hjälp av en cookie från en annan leverantör, kan unikt identifiera en enhet i flera program och gör att ni kan identifiera samma besökare och deras data i olika Experience Cloud-program. Mer information finns i Översikt över [identitetstjänsten i](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) Experience Cloud.

Med Opt-in Service, ett tillägg till Experience Cloud Identity Service, kan ni konfigurera protokoll för programmet så att besökarna kan avgöra om ni kan ange en cookie på besökarens enhet eller webbläsare. Mer detaljerad information om Opt-in Service, inklusive hur du konfigurerar tjänsten för ditt program, finns i dokumentationen för [Opt-in Service](https://docs.adobe.com/content/help/en/id-service/using/implementation/opt-in-service/optin-overview.html).

När besökarna på webbplatsen har tilldelats ECID:n kan du använda Adobe Privacy JavaScript Library för att hämta dessa ID:n för användning i sekretessförfrågningar, vilket beskrivs i nästa avsnitt.

## Sekretess-JS-bibliotek

Adobe Privacy JavaScript Library innehåller flera funktioner som gör att du kan hämta och ta bort kundidentiteter som lagras i webbläsaren. Biblioteket kan konfigureras för att hämta identitetsinformation från flera Adobe-program, inklusive ECID. Genom att använda återanrop eller löften kan du programmässigt hantera mottagna ID:n och skicka dem till API:t för sekretesstjänsten.

Mer information om JS-bibliotek för sekretess, inklusive kodexempel för flera vanliga användningsområden, finns i översikten över JS-biblioteket för [sekretess](js-library.md).

## Nästa steg

I det här dokumentet finns en kort översikt över de centrala begrepp som används för att hämta kundidentitetsdata för användning i sekretessförfrågningar. Vi rekommenderar att du läser dokumentationslänkarna i varje avsnitt för mer detaljerad information om dessa begrepp och tjänster. Anvisningar om hur du skickar hämtade ID:n till Integritetstjänst för att skapa begäranden om åtkomst, borttagning eller avanmälan finns i [utvecklarhandboken](api/getting-started.md)för Integritetstjänst.