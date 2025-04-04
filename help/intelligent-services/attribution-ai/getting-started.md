---
keywords: Experience Platform;komma igång;attribuering;populära ämnen
feature: Attribution AI
title: Komma igång med attribut-AI
description: Följande handledningar kräver förståelse för de olika Adobe Experience Platform-tjänster som används för att använda Attribution AI. Innan du börjar med självstudiekurserna bör du läsa följande dokument.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Komma igång med Attribution AI

Följande guider kräver en förståelse för de olika [!DNL Adobe Experience Platform]-tjänsterna som används med Attribution AI. Innan du börjar med självstudiekurserna bör du läsa följande dokument:

- [Systemöversikt för Experience Data Model (XDM)](../../xdm/home.md): XDM är det grundläggande ramverk som gör att [!DNL Adobe Experience Cloud], som drivs av Experience Platform, kan leverera rätt budskap till rätt person i rätt kanal vid exakt rätt tidpunkt. Metoden som Experience Platform bygger på, XDM System, använder Experience Data Model-scheman för Experience Platform tjänster.
- [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Det här dokumentet innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att komponera scheman som ska användas i [!DNL Adobe Experience Platform].
- [Skapar scheman](../../xdm/tutorials/create-schema-ui.md): Den här självstudiekursen beskriver stegen för att skapa ett schema med Schemaredigeraren i Experience Platform.

Attribution AI kräver att datauppsättningar följer CEE-schemat (Consumer Experience Events), som är en [XDM-schemafältgrupp (Experience Data Model)](../../xdm/home.md). Kontakta Adobe support på attributionai-support@adobe.com för att implementera eller göra ändringar i dessa data. Om det finns uppgifter om medieleveranser kan du göra ytterligare analyser, till exempel inkrementella intäkter och avkastning. Om det finns tillgängliga kundprofildata kan du tilldela krediter till kundprofilnivån ytterligare.

## Terminologi

- **Konverteringshändelse:** Alla digitala event eller digitala interaktioner som kunderna gör för att ange en milstolpe mot ett mål, till exempel konferensregistreringar. Ytterligare exempel är betalda konverteringar, kostnadsfria kontoregistreringar eller kvalificering för en egenskap.

- **Touchpoint:** Alla digitala händelser eller digitala interaktioner som kunderna gör på vägen mot ett mål. Exemplen omfattar tidigare köprelaterade marknadsföringssatsningar, visningar av webbannonsering och betalda sökklickningar.

## Hämtar AI-poäng för attribut

>[!NOTE]
>
>Om du inte behöver hämta råresultat kan du hoppa över det här steget och fortsätta till [nästa steg](#next-steps).

Hämtning av AI-poäng för attribuering görs via en kombination av API-anrop. För att kunna anropa Experience Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla Experience Platform API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Experience Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md) i felsökningsguiden för Experience Platform.

## Åtkomstkontroll {#access-control}

När du använder rollbaserad åtkomstkontroll ger behörigheterna **Visa attribut-AI** och **Hantera attribut-AI** åtkomst till olika funktioner för attribut-AI. Med **Hantera attribut-AI** kan du **skapa**, **klona**, **redigera**, **ta bort**, **aktivera** eller **inaktivera** en instans, och med **Visa attribut-AI** kan du **läsa** eller **visa** det. Åtgärderna **create**, **edit** och **delete** registreras av granskningsloggar.

Mer information om hur du tilldelar behörigheter för åtkomstkontroll](../../../help/access-control/home.md) finns i dokumentationen. Du kan även läsa om hur du [använder granskningsloggar för att övervaka åtkomst och aktivitet](../../../help/landing/governance-privacy-security/audit-logs/overview.md).[

## Nästa steg {#next-steps}

När du är klar och har alla dina autentiseringsuppgifter och scheman på plats börjar du med att följa [AI-gränssnittshandboken för Attribution](./user-guide.md). I den här guiden får du hjälp med att skapa en instans och skicka in den för utbildning och poängsättning.
