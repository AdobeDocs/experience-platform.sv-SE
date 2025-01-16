---
title: Skapa ett högklassigt centrum med sandlådeverktyg
description: Skapa ett center för hög kvalitet med sandlådeverktyg genom att skapa ett"gyllene sandlådepaket" som standardiserar metodtips för flera sandlådor.
source-git-commit: f0cbee2663682f0afae6d7e4b174f250fcb3df53
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# Skapa ett högklassigt centrum med sandlådeverktyg

Skapa ett center för hög kvalitet med sandlådeverktyg genom att skapa ett&quot;gyllene sandlådepaket&quot; som standardiserar metodtips för flera sandlådor.

![Översikt över att exportera paket mellan olika organisationer](../images/use-cases/packages-across-orgs.png)

## Varför ska man tänka på det här användningsexemplet? {#why-this-use-case}

Många stora företag eller företag använder flera sandlådor för olika organisationer, team, regioner och utvecklingsmiljöer. Med kraften i [sandlådeverktyg](../ui/sandbox-tooling.md) kan du skapa ett paket med en gyllene sandlåda för att säkerställa konsekvens, kompatibilitet och anpassning av organisationens standarder över flera sandlådor.

Det här gyllene sandlådepaketet skapar ett center av hög kvalitet för att effektivt dela nyckelkonfigurationer. Med sandlådeverktyg kan du enkelt importera paket till flera sandlådor. Du kan även dela ditt paket med andra organisationer för att säkerställa en bred enhetlighet.

Följ de steg som beskrivs i det här användningsexemplet för att skapa ett eget paket med en gyllene sandlåda.

## Branschexempel {#industry-example}

Som exempel kan nämnas en bank som fungerar i olika regioner, som Nordamerika, Europa och Afrika. Varje marknad eller region har sin egen Adobe Experience Platform-instans. Banken vill ha en centraliserad datamodell som hanteras av en global grupp arkitekter där en enda version av datamodellen kan lanseras på alla marknader.

Den här banken väljer att använda verktyg för säkerhetssandlådor för att skapa och underhålla ett paket med en gyllene sandlåda. Detta bidrar till effektiv utveckling, möjliggör enhetliga datamodeller och säkerställer konsekvens i alla regioner.

## Förutsättningar och planering {#prerequisites-and-planning}

När du planerar att skapa ett eget center för hög kvalitet inom din organisation bör du tänka på följande under planeringsprocessen:

- Identifiera de bästa metoderna och konfigurationerna som ska ingå i ditt paket.
- Skapa en sandlåda med alla relevanta och validerade konfigurationer som ska anges som den gyllene sandlådan.
- Om det behövs kan ni få synpunkter från intressenter och komma överens om era grundläggande standarder.

### UI-funktionalitet, plattformskomponenter och Experience Cloud-produkter som du kommer att använda {#ui-functionality-and-elements}

För att implementera det här användningsexemplet måste du använda flera områden i Adobe Experience Platform. Kontrollera att du har de [attributbaserade åtkomstkontrollsbehörigheterna](../../access-control/abac/overview.md) som krävs för alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

- [Verktyg i sandlådan](../ui/sandbox-tooling.md)
- [Sandlådehantering](../ui/user-guide.md)
- [Datauppsättningar](../../catalog/datasets/overview.md)
- [Scheman](../../xdm//home.md)
- [Målgrupper](../../segmentation/home.md)
- [Resor från Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

1. Skapa baslinjekonfigurationen som representerar de bästa metoderna i en gyllene sandlåda. Detta kan omfatta objekt som datauppsättningar, scheman, målgrupper eller resor.
2. Exportera konfigurationen till ett paket med sandlådeverktyg.
3. Importera det här paketet till alla relevanta sandlådor.
4. Om du har flera organisationer kan du dela det här paketet i alla dina organisationer.
5. Övervaka import och export och spåra ändringar via granskningsloggar.
6. Uppdatera regelbundet din gyllene sandlåda i takt med att standarderna utvecklas för att säkerställa att alla sandlådor är anpassade efter bästa praxis.

## Så här uppnår du användningsfallet: stegvisa instruktioner {#step-by-step-instructions}

Läs igenom avsnitten nedan som innehåller länkar till ytterligare dokumentation för att slutföra varje steg i översikten ovan.

### Skapa din gyllene sandlåda

Det första steget i att skapa ett högklassigt center är att skapa din gyllene sandlåda. Den här sandlådan bör innehålla de baslinjekonfigurationer som representerar dina bästa metoder. Om du vill skapa den här gyllene sandlådan följer du guiden om att [skapa en ny sandlåda](../ui/user-guide.md#create-a-new-sandbox) i Experience Platform.

När din sandlåda har skapats börjar du skapa baslinjeobjektskonfigurationer, till exempel [scheman](../../xdm/ui/resources/schemas.md#create-a-new-schema), [datauppsättningar](../../catalog/datasets/user-guide.md#create-a-dataset) eller [målgrupper](../../segmentation/ui/segment-builder.md). Kontrollera dina konfigurationer innan du fortsätter.

### Exportera sandlådan till ett paket

Nu när sandlådan innehåller dina baslinjeobjektskonfigurationer är den klar att exporteras till ett paket med hjälp av sandlådeverktyg. Följ guiden om [att exportera en hel sandlåda](../ui/sandbox-tooling.md#export-an-entire-sandbox) för att skapa ditt paket med den gyllene sandlådan.

### Importera ditt paket till relevanta sandlådor

Nu när ditt paket har skapats kan du importera det till dina relevanta sandlådor. Det bästa sättet är att importera ett paket som innehåller en hel sandlåda till en tom sandlåda. Med sandlådeverktyg kan du enkelt [importera ett helt sandlådepaket](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package) till en sandlåda direkt i Experience Platform.

### Dela paket mellan olika organisationer

Med sandlådeverktygen kan du dela paket som du har skapat i olika organisationer. Följ [guiden för paketdelning](../../sandboxes/ui/sharing-packages-across-orgs.md) för att dela ditt paket med den gyllene sandlådan.

### Övervaka import och export via granskningsloggar

När du importerar eller exporterar ditt paket kan du övervaka statusen för jobben med kontrollpanelen **[!UICONTROL Jobs]** i Experience Platform. Mer information om övervakning av jobb finns i guiden [Övervaka importinformation](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details).

### Uppdatera guldsandlådan regelbundet

Nu när ditt paket med den gyllene sandlådan är klart har du etablerat ett standardiserat center för hög kvalitet som du kan fortsätta importera till sandlådor eller dela mellan olika organisationer. När era bästa metoder ändras och utvecklas är det viktigt att regelbundet uppdatera baslinjeobjektskonfigurationerna i din gyllene sandlåda. När du uppdaterar sandlådan kan du skapa nya versioner av ditt paket med den gyllene sandlådan på samma sätt.

>[!NOTE]
>
> Stegen ovan följer processen i Experience Platform användargränssnitt. Du kan följa samma steg med API:t via olika slutpunkter. Mer information om hur du gör varje begäran via API finns i `sandboxes` [slutpunktshandboken](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/api/sandboxes#create) och `packages` [slutpunktshandboken](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages) .

## Andra användningsområden som uppnås genom stöd för partnerdata {#other-use-cases}

Utforska fler användningsfall som aktiveras via sandlådeverktyg:

- [Säkerhetskopiera objektkonfigurationer med sandlådeverktyg](./backup-object-configuration.md)
