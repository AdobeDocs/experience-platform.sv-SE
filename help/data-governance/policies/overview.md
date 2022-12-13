---
keywords: Experience Platform;hem;populära ämnen;modul;DULE
solution: Experience Platform
title: Översikt över dataanvändningsprinciper
topic-legacy: policies
description: Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom Adobe Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# Översikt över policyer för dataanvändning {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Begränsa dataanvändning"
>abstract="Typen av dataanvändningspolicy utvärderar specifika marknadsföringsåtgärder som tillämpas på datastyrningsetiketter för att begränsa dataanvändningen för marknadsföringsaktiviteter."

För att dataanvändningsetiketter effektivt ska stödja regelefterlevnad måste dataanvändningsprinciper implementeras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data i [!DNL Experience Platform].

Det finns två typer av principer:

* **[!UICONTROL Data governance policy]**: Begränsa aktiveringen av data baserat på den marknadsföringsåtgärd som utförs och de dataanvändningsetiketter som medföljer data i fråga.
* **[!UICONTROL Consent policy]**: Filtrera de profiler som kan aktiveras för [mål](../../destinations/home.md) baserat på kundernas samtycke eller önskemål

>[!NOTE]
>
>Dataanvändningsprinciper ska inte förväxlas med [åtkomstkontrollprinciper](../../access-control/abac/end-to-end-guide.md#policy), som avgör om vissa plattformsanvändare i organisationen kan få åtkomst till vissa datafält och konfigureras via [!UICONTROL Permissions] -fliken.

Det här dokumentet innehåller en översikt över dataanvändningsprinciper på hög nivå och länkar till ytterligare dokumentation om hur du arbetar med principer i gränssnittet eller API:t.

## Marknadsföringsåtgärder {#marketing-actions}

Marknadsföringsåtgärder (kallas även användningsfall för marknadsföring) inom ramen för datastyrningsramen är åtgärder som [!DNL Experience Platform] dataanvändare kan använda, som din organisation vill begränsa dataanvändningen för. En dataanvändningsprincip definieras därför enligt följande:

1. En specifik marknadsföringsåtgärd
2. De villkor under vilka åtgärden begränsas

Ett exempel på en marknadsföringsåtgärd kan vara en önskan att exportera en datauppsättning till en tredjepartstjänst. Om det finns en policy som säger att vissa typer av data (t.ex. PII) inte kan exporteras, och du försöker exportera en datauppsättning som innehåller en I-etikett (identitetsdata), får du ett svar från [!DNL Policy Service] att en dataanvändningspolicy har överträtts.

>[!NOTE]
>
>Marknadsföringsåtgärder begränsar inte användningen av data. De måste inkluderas i aktiverade dataanvändningspolicyer för att dessa åtgärder ska kunna utvärderas för policyöverträdelser.

När dataanvändningen sker i er organisations tjänst bör relevanta marknadsföringsåtgärder anges så att eventuella policyöverträdelser kan identifieras. Du kan sedan använda [API för principtjänst](https://www.adobe.io/experience-platform-apis/references/policy-service/) om du vill söka efter policyöverträdelser i integreringen.

>[!NOTE]
>
>Ni kan ställa in användningsfall för marknadsföring på destinationer för att automatisera regelefterlevnaden. Se [destinationsdokumentation](../../destinations/home.md) om du vill ha mer information om konfigurationsalternativen för ditt särskilda mål.

I bilagan till det här dokumentet finns en lista med [tillgängliga Adobe-definierade marknadsföringsåtgärder](#core-actions). Du kan också definiera egna anpassade marknadsföringsåtgärder med [!DNL Policy Service] API eller [!DNL Experience Platform] användargränssnitt. Mer information om hur du arbetar med marknadsföringsåtgärder och -policyer finns i nästa avsnitt.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Hantera dataanvändningspolicyer {#manage}

När dataanvändningsetiketterna har tillämpats kan dataavdelningarna använda [!DNL Policy Service] API eller [!DNL Experience Platform] Gränssnitt för att hantera och utvärdera principer som relaterar till marknadsföringsåtgärder som vidtas på data som innehåller dataanvändningsetiketter. Du kan skapa och uppdatera profiler, fastställa en profils status och arbeta med marknadsföringsåtgärder för att utvärdera om en viss åtgärd bryter mot en dataanvändningspolicy.

>[!IMPORTANT]
>
>Alla dataanvändningsprinciper (inklusive huvudprinciper som tillhandahålls av Adobe) inaktiveras som standard. För att en enskild princip ska kunna användas måste du manuellt aktivera den principen via API:t eller användargränssnittet.

Stegvisa instruktioner om hur du arbetar med marknadsföringsåtgärder och dataanvändningspolicyer i API:t finns i självstudiekursen om [skapa och utvärdera dataanvändningsprinciper](create.md). Mer information finns i nyckelåtgärderna i [!DNL Policy Service] API, se [Utvecklarhandbok för principtjänst](../api/getting-started.md).

Information om hur du arbetar med marknadsföringsåtgärder och -policyer finns i [!DNL Platform] Gränssnitt, se [användarhandbok för dataanvändningsprincip](./user-guide.md).

## Nästa steg

Detta dokument innehåller en introduktion till dataanvändningsprinciper inom ramverket för datastyrning. Du kan nu fortsätta att läsa den processdokumentation som är länkad till i den här handboken för att lära dig mer om hur du arbetar med policyer i API:t och användargränssnittet.

## Bilaga

Följande avsnitt innehåller ytterligare information om dataanvändningsprinciper.

### Adobe-definierade marknadsföringsåtgärder {#core-actions}

Tabellen nedan beskriver de viktigaste marknadsföringsåtgärderna som tillhandahålls av Adobe.

>[!NOTE]
>
>De viktigaste marknadsföringsåtgärderna bör ses som en startpunkt för att hjälpa er att identifiera vilka användarprofiler som ska skapas och kontrollera om det finns överträdelser. Definitionerna och hur de tolkas beror på organisationens behov och policyer.

| Marknadsföringsåtgärd | Beskrivning |
| --- | --- |
| Analytics  | En åtgärd som använder data för analysändamål, som att mäta, analysera och rapportera om kundens användning av organisationens webbplatser eller appar. |
| Kombinera med direkt identifierbara data | En åtgärd som kombinerar all personligt identifierbar information med anonyma data. Kontrakt för data som hämtas från annonsnätverk, annonsservrar och tredjepartsleverantörer av data innehåller ofta särskilda avtalsförbud för användning av sådana data med direkt identifierbara data. |
| Målgruppsövergripande | En åtgärd som använder data för annonsanpassning mellan webbplatser. En kombination av data från flera platser, inklusive en kombination av data på plats och data utanför platsen eller en kombination av data från flera källor utanför platsen, kallas data mellan olika platser. Data från olika webbplatser samlas in och behandlas vanligtvis för att man ska kunna dra slutsatser om användarnas intressen. |
| Datavetenskap | En åtgärd som använder data för arbetsflöden inom datavetenskap. Vissa avtal innehåller uttryckliga förbud mot dataanvändning för datavetenskap. Ibland formuleras dessa i termer som förbjuder användning av data för artificiell intelligens (AI), maskininlärning (ML) eller modellering. |
| E-postmarknadsföring | En åtgärd som använder data i e-postriktade kampanjer. |
| Exportera till tredje part | En åtgärd som exporterar data till processorer och enheter som inte har direkta relationer med kunder. Många dataleverantörer har villkor i avtalen som förbjuder export av data som de ursprungligen samlades in från. Kontrakt för sociala nätverk begränsar till exempel ofta överföringen av data som du får från dem. |
| Annonsering på plats | En åtgärd som använder data för annonser på plats, inklusive urval och leverans av annonser på organisationens webbplatser eller i appar, eller för att mäta leveransen och effektiviteten av sådana annonser. |
| Personalisering på plats | En åtgärd som använder data för innehållspersonalisering på plats. Personalisering på plats är alla data som används för att dra slutsatser om användarnas intressen, och används för att välja vilket innehåll eller vilka annonser som betjänas baserat på dessa slutsatser. |
| Segmentmatchning | En åtgärd som använder data för Adobe Experience Platform Segment Match, som gör att två eller flera plattformsanvändare kan utbyta segmentdata. Genom att aktivera profiler som refererar till den här åtgärden kan du begränsa vilka data som används för segmentmatchning. Om huvudprincipen &quot;Begränsa datadelning&quot; till exempel är aktiverad, kan alla data med en [C11-etikett](../labels/reference.md#c11) kan inte användas för segmentmatchning. |
| Personalisering med en identitet | En åtgärd som kräver att en enda identitet används för personalisering i stället för att sammanfoga identiteter från flera källor. |
