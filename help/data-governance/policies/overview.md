---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över policyer för dataanvändning
topic: policies
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# Översikt över policyer för dataanvändning

För att dataanvändningsetiketter effektivt ska stödja regelefterlevnad måste dataanvändningsprinciper implementeras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom [!DNL Experience Platform].

Det här dokumentet innehåller en översikt över dataanvändningsprinciper på hög nivå och länkar till ytterligare dokumentation om hur du arbetar med principer i gränssnittet eller API:t.

## Marknadsföringsåtgärder {#marketing-actions}

**Marknadsföringsåtgärder**(kallas även **användningsfall** för marknadsföring) inom ramen för datastyrningsramverket är åtgärder som en [!DNL Experience Platform] datakonsument kan vidta och som din organisation vill begränsa dataanvändningen för. En dataanvändningsprincip definieras därför enligt följande:

1. En specifik marknadsföringsåtgärd
2. Etiketter för dataanvändning som åtgärden är begränsad från att utföras mot

Ett exempel på en marknadsföringsåtgärd kan vara en önskan att exportera en datauppsättning till en tredjepartstjänst. Om det finns en policy som säger att vissa typer av data (t.ex. personligt identifierbar information (PII)) inte kan exporteras, och du försöker exportera en datauppsättning som innehåller en I-etikett (identitetsdata), kommer du att få ett svar från användaren om [!DNL Policy Service] att en dataanvändningspolicy har överträttts.

>[!NOTE]
>
>Marknadsföringsåtgärder begränsar inte användningen av data. De måste inkluderas i aktiverade dataanvändningspolicyer för att dessa åtgärder ska kunna utvärderas för policyöverträdelser.

När dataanvändningen sker i er organisations tjänst bör relevanta marknadsföringsåtgärder anges så att eventuella policyöverträdelser kan identifieras. Du kan sedan använda API:t [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service för att kontrollera om integreringen har skett.

>[!NOTE]
>
>Om du använder [!DNL Real-time Customer Data Platform]kan du konfigurera användningsfall för marknadsföring på destinationer för att automatisera regelefterlevnaden. Mer information finns i dokumentet om [datastyrning i CDP](../../rtcdp/privacy/data-governance-overview.md) i realtid.

I bilagan till det här dokumentet finns en lista med [tillgängliga Adobe-definierade marknadsföringsåtgärder](#core-actions). Du kan också definiera egna anpassade marknadsföringsåtgärder med DULE [!DNL Policy Service] API eller [!DNL Experience Platform ]användargränssnittet. Mer information om hur du arbetar med marknadsföringsåtgärder och -policyer finns i nästa avsnitt.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Hantera dataanvändningspolicyer {#manage}

När dataanvändningsetiketterna har tillämpats kan datahanterarna använda DULE [!DNL Policy Service] API eller [!DNL Experience Platform] UI för att hantera och utvärdera principer som relaterar till marknadsföringsåtgärder som vidtas på data som innehåller dataanvändningsetiketter. Du kan skapa och uppdatera profiler, fastställa en profils status och arbeta med marknadsföringsåtgärder för att utvärdera om en viss åtgärd bryter mot en dataanvändningspolicy.

>[!IMPORTANT]
>
>Alla dataanvändningspolicyer (inklusive kärnpolicyer från Adobe) är inaktiverade som standard. För att en enskild princip ska kunna användas måste du manuellt aktivera den principen via API:t eller användargränssnittet.

Stegvisa instruktioner om hur du arbetar med marknadsföringsåtgärder och dataanvändningspolicyer i API:t finns i självstudiekursen om hur du [skapar och utvärderar dataanvändningspolicyer](create.md). Mer information om nyckelåtgärder som tillhandahålls av [!DNL Policy Service] API:t finns i utvecklarhandboken [för](../api/getting-started.md)principtjänsten.

Mer information om hur du arbetar med marknadsföringsåtgärder och -profiler i [!DNL Platform] användargränssnittet finns i användarhandboken för [dataanvändningspolicyn](./user-guide.md).

## Nästa steg

Det här dokumentet innehåller en introduktion till dataanvändningsprinciper i DULE-ramverket. Du kan nu fortsätta att läsa den processdokumentation som är länkad till i den här handboken för att lära dig mer om hur du arbetar med policyer i API:t och användargränssnittet.

## Bilaga

Följande avsnitt innehåller ytterligare information om dataanvändningsprinciper.

### Adobe-definierade marknadsföringsåtgärder {#core-actions}

Tabellen nedan beskriver de viktigaste marknadsföringsåtgärderna som tillhandahålls av Adobe.

>[!NOTE]
>
>De viktigaste marknadsföringsåtgärderna bör ses som en startpunkt för att hjälpa er att identifiera vilka användarprofiler som ska skapas och kontrollera om det finns överträdelser. Definitionerna och hur de tolkas beror på organisationens behov och policyer.

| Marknadsföringsåtgärd | Beskrivning |
| --- | --- |
| Analyser | En åtgärd som använder data för analysändamål, som att mäta, analysera och rapportera om kundens användning av organisationens webbplatser eller appar. |
| Kombinera med PII | En åtgärd som kombinerar all personligt identifierbar information med anonyma data. Kontrakt för data som hämtas från annonsnätverk, annonsservrar och tredjepartsleverantörer av data innehåller ofta särskilda avtalsförbud för användning av sådana data med direkt identifierbara data. |
| Målgruppsövergripande | En åtgärd som använder data för annonsanpassning mellan webbplatser. En kombination av data från flera platser, inklusive en kombination av data på plats och data utanför platsen eller en kombination av data från flera källor utanför platsen, kallas data mellan olika platser. Data från olika webbplatser samlas in och behandlas vanligtvis för att man ska kunna dra slutsatser om användarnas intressen. |
| Datavetenskap | En åtgärd som använder data för arbetsflöden inom datavetenskap. Vissa avtal innehåller uttryckliga förbud mot dataanvändning för datavetenskap. Ibland formuleras dessa i termer som förbjuder användning av data för artificiell intelligens (AI), maskininlärning (ML) eller modellering. |
| E-postmarknadsföring | En åtgärd som använder data i e-postriktade kampanjer. |
| Exportera till tredje part | En åtgärd som exporterar data till processorer och enheter som inte har direkta relationer med kunder. Många dataleverantörer har villkor i avtalen som förbjuder export av data som de ursprungligen samlades in från. Kontrakt för sociala nätverk begränsar till exempel ofta överföringen av data som du får från dem. |
| Annonsering på plats | En åtgärd som använder data för annonser på plats, inklusive urval och leverans av annonser på organisationens webbplatser eller i appar, eller för att mäta leveransen och effektiviteten av sådana annonser. |
| Personalisering på plats | En åtgärd som använder data för innehållspersonalisering på plats. Personalisering på plats är alla data som används för att dra slutsatser om användarnas intressen, och används för att välja vilket innehåll eller vilka annonser som betjänas baserat på dessa slutsatser. |
| Personalisering med en identitet | En åtgärd som kräver att en enda identitet används för personalisering i stället för att sammanfoga identiteter från flera källor. |
